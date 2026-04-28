---
title: 'Aufspaltung des Zahlungs-POC: Architektur- und Design-Entscheidungen'
description: Erfahren Sie, wie der Split-Payment-POC den Synchronisierungs-Checkout mit Commerce und I/O-gesteuerte Schritte mit App Builder zuordnet, einschließlich Erweiterungsattributen, REST und fünf Plug-in-Edge-Fällen.
feature: App Builder, Eventing, Extensibility, Paas, Payments, REST
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Tutorial
duration: 293
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 1e2c7e0e6d0f2d174b88406ce3fb7c787676ecee
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 1%

---

# Aufspaltung des Zahlungs-POC: Architektur- und Design-Entscheidungen

Auf dieser Seite werden die architektonischen Optionen hinter dem aufgeteilten Zahlungsnachweis des Konzepts erläutert. Lesen Sie es, bevor Sie die Build-Eingabeaufforderungen in dieser Reihe verwenden, damit Sie verstehen, wie jede Komponente strukturiert ist und wie Sie die Muster in Ihrem eigenen Projekt anpassen können.

## Das Grundprinzip

Bei dem Machbarkeitsnachweis geht es nicht um die eleganteste Split-Zahlungsimplementierung. Es geht darum zu zeigen **wie man ohne eine Big-Bang-Umschreibung mit der Umstellung der Commerce-Logik auf App Builder**.

Die Regel, die durchgängig angewendet wird, lautet:

> **Wenn etwas synchron im Commerce-Anfragezyklus laufen muss oder Commerce-interne APIs aufrufen muss, die keine saubere externe Oberfläche haben, bleibt es in PHP. Alles andere wandert nach App Builder.**

## Was lebt in Commerce (PHP) und warum

### &#x200B;1. Kreditantrag speichern: `PlaceOrderPlugin`

Store-Guthaben wird mit `Magento\CustomerBalance\Api\BalanceManagementInterface::apply()` auf den Warenkorb angewendet. Diese Methode funktioniert nur für einen **aktiven** Warenkorb. Der Warenkorb wird zum Zeitpunkt der Bestellung inaktiv. App Builder erhält das E/A *Ereignis (nachdem* die Bestellung aufgegeben wurde. Daher ist es nicht möglich, eine Gutschrift von App Builder zu beantragen.

**Die Lektion** Alles, was den Warenkorbstatus vor der Bestellplatzierung ändern muss, muss in Commerce ausgeführt werden. Es gibt keine Problemumgehung.

### &#x200B;2. Synchroner Schwellenwertwächter: `CheckoutPlugin`

Die Prüfung des Bestellschwellenwerts von 100 USD muss den Kunden bei der Zahlungsstufe blockieren, bevor er **[!UICONTROL Place Order]** auswählt. Die Antwort muss im Commerce-Anfragezyklus synchron sein. App Builder ist ereignisgesteuert und asynchron, sodass in diesem Moment kein sofortiger Fehler zurückgegeben werden kann.

App Builder *auch* validiert den Schwellenwert (als Audit), aber das Kundenerlebnis hängt davon ab, dass die Commerce-Prüfung zuerst ausgeführt wird.

### &#x200B;3. Benutzerdefinierte REST-Endpunkte: `webapi.xml` und `SplitPaymentManagement`

The following endpoints must:

* Invoke `SplitInvoiceService` (invoices that use the Commerce internal invoice service)
* Invoke `ShipOrder::execute()` (Commerce&#39;s internal shipment service)
* Update order state and status with Commerce&#39;s order state machine

`/V1/split-payment/orders/:id/cash-received` und `/V1/split-payment/orders/:id/cash-decline`

There is no clean public REST layer for that behavior, so Commerce exposes the endpoints. App Builder calls them.

### 4. Split amounts on quote and order: observers and plugins

Commerce needs the split amounts (`split_store_credit_amount`, `split_cash_amount`, `split_cash_status`) on the order, both for the REST responses App Builder reads and for the **[!UICONTROL Admin]** order view. The amounts are attached with extension attributes and are copied from the quote to the order in an observer on `sales_model_service_quote_submit_before`.

## What lives in App Builder and why

### 1. Event-driven order processing: `payment-orchestrator`

After `sales_order_place_before` fires, App Builder receives the event. It re-validates the threshold (as an audit), records a *cash pending* comment on the order, and updates order status. None of that requires new PHP, only REST back into Commerce.

### 2. Cash acceptance: `payment-accept`

When an ERP (or an operator in the dashboard) confirms cash was received, `payment-accept` calls `POST /V1/split-payment/orders/:id/cash-received`. Invoice, shipment, and order status are handled in Commerce. App Builder is the trigger.

### 3. Cash decline: `payment-decline`

`payment-decline` calls `POST /V1/split-payment/orders/:id/cash-decline` and Commerce cancels the order. Same pattern as cash acceptance.

### 4. Operator dashboard: `demo-dashboard`

A self-contained HTML dashboard served from an App Builder web action. It fetches orders that are waiting on cash from Commerce REST and provides **[!UICONTROL Accept]** / **[!UICONTROL Decline]** actions that call the App Builder actions above. Commerce **[!UICONTROL Admin]** ist nicht erforderlich.

## Der Schwellenwert: zweimal absichtlich erzwungen

```text
Customer at checkout
        |
        v
[Commerce: CheckoutPlugin]     <- Synchronous, blocks immediately, user sees error
        |
        |  (if somehow bypassed: direct API call, and so on)
        v
[Order placed] -> I/O Event -> [App Builder: payment-orchestrator]
                                        |
                                        v
                              [evaluateThreshold()]  <- Async audit, records failure comment
```

**Commerce steuert den für Benutzende gerichteten Schutz; App Builder steuert die Prüfung nach der Platzierung.** Das ist Absicht.

## Der Store-Abspann: Warum es in PHP bleibt

```text
What you might think would work (it does not):
  Order placed -> I/O Event -> App Builder -> PUT /V1/carts/:id/store-credit
  (Fails: cart is inactive after place order)

What actually works:
  AroundPlaceOrder plugin
  -> BalanceManagementInterface::apply($cartId, $amount)  <- cart is still active
  -> place order
  -> order placed
  -> I/O event: App Builder (store credit is already applied)
```

Die `store-credit.js` Datei im Orchestrator dokumentiert dies. Es ist ein No-op-Stub mit Kommentaren, die erklären, warum es nicht verwendet wird.

## Erweiterungsattribute: der Kleber

Aufspaltungsbeträge bewegen sich durch das System bei Erweiterungsattributen:

```text
Checkout JavaScript (Knockout)
    |  POST /V1/split-payment/set
    v
SplitPaymentSession (PHP session)
    |  AroundPlaceOrder reads the session
    v
CartInterface extension attributes
    |  `sales_model_service_quote_submit_before` observer
    v
OrderInterface extension attributes -> `sales_order` flat columns
    |  I/O event payload includes these fields
    v
App Builder `payment-orchestrator` reads the split amounts
```

## Datenmodell

**`sales_order`flache Spalten, die dieses Modul hinzufügt**

| Spalte | Typ | Zweck |
| --- | --- | --- |
| `split_store_credit_amount` | floaten | Angewandte Gutschrift speichern |
| `split_cash_amount` | floaten | Fälliger Barbetrag |
| `split_cash_status` | varchar | `pending`, `received` oder `declined` |
| `split_sc_invoice_id` | int | Entitäts-ID der Filialgutschrift-Rechnung |
| `split_cash_invoice_id` | int | Entitäts-ID der Kassenrechnung |

**Erweiterungsattribute** (in `CartInterface`, `OrderInterface` und `OrderPaymentInterface`)

* `split_store_credit_amount` (float)
* `split_cash_amount` (float)
* `split_cash_status` (Zeichenfolge)

## Payload-Felder des I/O-Ereignisses

`observer.sales_order_place_before` wird in `io_events.xml` konfiguriert, um Folgendes in das Ereignis einzuschließen:

```xml
entity_id, quote_id, increment_id, subtotal,
split_store_credit_amount, split_cash_amount, split_cash_status
```

App Builder verwendet `entity_id` als Auftrags-ID und `split_store_credit_amount` und `split_cash_amount` für die Schwellenwertvalidierung.

## Die fünf Randfälle des Konzeptnachweises umfassen

### 1. `CapCustomerBalanceCollectPlugin`

Der native **[!UICONTROL Customer balance]**-Gesamt-Collector von Commerce kann zu viel anwenden (er kann den vollständigen verfügbaren Saldo sehen, nicht den sitzungsdeklarierten Aufspaltungsbetrag). Dieses Plug-in begrenzt den Betrag auf den in der Sitzung deklarierten Wert.

### 2. `FixSplitPaymentGrandTotalPlugin`

Nachdem das Store-Guthaben angewendet wurde, kann der **[!UICONTROL Grand Total]** auf den bargeldlosen Betrag fallen. Die Checkout-JavaScript muss die Bestellsumme für die Aufspaltungsvalidierung (*)* diese Änderung berechnen. Das Plug-in wird nach der Gesamterfassung ausgeführt und korrigiert die Anzeige, während der JavaScript `grand_total` nicht vertraut und den Wert aus Zwischensummensegmenten rekonstruiert.

### 3. `FixInvoiceCustomerBalanceAfterTotalsPlugin`

Wenn die Rechnungssummen zurückgezogen werden, kann die Gutschrift des Geschäfts zweimal vorgenommen werden. Dieses Plug-in korrigiert `customer_balance_amount` auf Rechnungen.

### 4. `SplitPaymentZeroTotalPlugin`

Nachdem die Gutschrift für den Store angewendet wurde, kann die **[!UICONTROL Grand Total]** für den Warenkorb $0 sein (vollständige Gutschrift für den Store). Die **[!UICONTROL Zero subtotal checkout]** von Commerce kann in diesem Fall Code blockieren. Dieses Plug-in ermöglicht COD, wenn der Barbetrag der Sitzung größer als 0 ist.

### &#x200B;5. Erinnerung vor `BalanceManagementInterface::apply()` zitieren

`apply()` vergleicht den Betrag mit dem aktuellen **[!UICONTROL Grand Total]**. Wenn die Summe bereits nur der Cash-Teil ist, kann `apply()` fehlschlagen oder die Obergrenze einschränken. `PlaceOrderPlugin` setzt die Gesamtreparatur vorübergehend aus, während der Saldo angewendet wird, mithilfe eines Sitzungs-Flags (`beginBalanceApply` / `endBalanceApply`).


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
