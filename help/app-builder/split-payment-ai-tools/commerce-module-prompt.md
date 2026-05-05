---
title: 'Aufspaltung des Zahlungs-POC: Commerce-Modul-KI-Eingabeaufforderung'
description: Erfahren Sie, wie Sie mit dieser Eingabeaufforderung Client_SplitPayment generieren. REST, Plug-ins, Checkout-JavaScript, E/A-Ereignisse und Aktivieren, Kompilieren und Bereitstellen von Befehlen.
feature: App Builder, Backend Development, Eventing, Extensibility, Paas, REST, Orders
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Tutorial
duration: 503
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 8dfbf2694378aae76c91afa11bfee7d93077d8ba
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 1%

---

# Aufspaltung des Zahlungs-POC: Commerce-Modul-KI-Eingabeaufforderung

Verwenden Sie diese Seite, um die vollständige Eingabeaufforderung zu kopieren, die das `Client_SplitPayment` Modul „In-Process“ generiert: REST, Sitzungsbehandlung, **[!UICONTROL Checkout]** und **[!UICONTROL Admin]** für den Konzeptnachweis für aufgeteilte Zahlungen. Der Benutzer-Workflow verbleibt in App Builder.

## So verwenden Sie diese Eingabeaufforderung

Kopieren Sie alles von **PROMPT START** bis **Ende der Eingabeaufforderung** nach Cursor (mit Claude) oder direkt nach Claude. Führen Sie sie aus dem Stammverzeichnis Ihres Commerce-Projekts oder aus einem Verzeichnis aus, in dem die API Dateien erstellen kann.

## Vor der Ausführung anpassen

* Ersetzen Sie `Client` durch den tatsächlichen Anbieternamen.
* Ändern Sie `SplitPayment`, wenn Sie einen anderen Modulnamen verwenden möchten.
* Wenn die Site ein benutzerdefiniertes Design verwendet, müssen die Layout-XML- und RequireJS-Pfade möglicherweise geändert werden.
* Wenn Ihre **[!UICONTROL Cash on delivery]** einen anderen Code als `cashondelivery` verwendet, aktualisieren Sie `payment-method-helper.js`.


## Die Eingabeaufforderung

**PROMPT START**

Sie generieren ein vollständiges, produktionsfähiges Adobe Commerce 2.4.5+ In-Process-Modul für eine Split-Payment-Funktion. Dieses Modul ist der dünne PHP-Adapter, der die richtige REST-Oberfläche bereitstellt und die richtigen Daten zum richtigen Zeitpunkt im Commerce-Lebenszyklus anbringt. Die gesamte Workflow-Logik des Benutzers lebt in Adobe App Builder (nicht in diesem Modul).

**Modulidentität:**
* Anbieter: `Client`
* Modul: `SplitPayment`
* Vollständiger Name: `Client_SplitPayment`
* Namespace: `Client\SplitPayment`
* Speicherort: `app/code/Client/SplitPayment/`
* Abhängigkeiten: `Magento_Checkout`, `Magento_CustomerBalance`, `Magento_Sales`, `Magento_Quote`, `Magento_WebApi`, `Magento_AdobeCommerceEventsClient`

Generieren Sie jede Datei, die in der folgenden Dateistruktur aufgeführt ist. Lassen Sie keine Datei aus. Verwenden Sie `declare(strict_types=1)` in allen PHP-Dateien.


### Zu erzeugende Dateistruktur

```
app/code/Client/SplitPayment/
├── registration.php
├── composer.json
├── Api/
│   ├── Data/SplitPaymentInterface.php
│   └── SplitPaymentManagementInterface.php
├── Block/
│   └── Order/SplitPaymentInfo.php
├── Controller/
│   └── Checkout/StoreCreditBalance.php
├── etc/
│   ├── acl.xml
│   ├── config.xml
│   ├── db_schema.xml
│   ├── db_schema_whitelist.json
│   ├── di.xml
│   ├── events.xml
│   ├── extension_attributes.xml
│   ├── io_events.xml
│   ├── module.xml
│   ├── webapi.xml
│   └── frontend/
│       └── routes.xml
├── Model/
│   ├── SplitPaymentData.php
│   ├── SplitPaymentManagement.php
│   ├── Service/
│   │   └── SplitInvoiceService.php
│   └── Session/
│       └── SplitPaymentSession.php
├── Observer/
│   ├── AutoInvoiceStoreCreditOnOrderPlace.php
│   └── CopySplitPaymentToOrder.php
├── Plugin/
│   ├── CheckoutPlugin.php
│   ├── OrderRepositoryPlugin.php
│   ├── PlaceOrderPlugin.php
│   ├── Adminhtml/
│   │   └── OrderPaymentPlugin.php
│   ├── Checkout/
│   │   └── LayoutProcessorPlugin.php
│   ├── CustomerBalance/
│   │   └── CapCustomerBalanceCollectPlugin.php
│   ├── Payment/
│   │   ├── Block/
│   │   │   └── AdminSplitPaymentTitlePlugin.php
│   │   └── Checks/
│   │       └── SplitPaymentZeroTotalPlugin.php
│   ├── Quote/
│   │   └── FixSplitPaymentGrandTotalPlugin.php
│   └── Sales/
│       └── FixInvoiceCustomerBalanceAfterTotalsPlugin.php
├── Setup/
│   └── Patch/
│       └── Data/
│           └── AddSplitPaymentOrderAttribute.php
└── view/
    └── frontend/
        ├── requirejs-config.js
        ├── layout/
        │   └── sales_order_view.xml
        ├── templates/
        │   └── order/
        │       └── split-payment-info.phtml
        └── web/
            ├── js/
            │   ├── model/
            │   │   └── payment-method-helper.js
            │   └── view/
            │       └── payment/
            │           ├── cashondelivery-method.js
            │           └── split-payment.js
            └── template/
                └── payment/
                    ├── cashondelivery.html
                    └── split-payment.html
```


### Verhaltensspezifikationen

#### &#x200B;1. Datenbankschema (`etc/db_schema.xml`)

Fügen Sie diese Spalten zu `sales_order` hinzu (Ressource: `sales`):

| Spalte | Typ | nullable | Kommentar |
|---|---|---|---|
| `split_store_credit_amount` | DECIMAL(12,4) | Ja | Gutschriftanteil speichern |
| `split_cash_amount` | DECIMAL(12,4) | Ja | fälliger Kassenanteil |
| `split_cash_status` | varchar(32) | Ja | `pending` / `received` / `declined` |
| `split_sc_invoice_id` | int unsigniert | Ja | Entitäts-ID der Gutschriftsrechnung speichern |
| `split_cash_invoice_id` | int unsigniert | Ja | Entitäts-ID der Kassenrechnung |

Generieren Sie auch die `db_schema_whitelist.json` für diese Spalten.

#### &#x200B;2. Erweiterungsattribute (`etc/extension_attributes.xml`)

Fügen Sie `split_store_credit_amount` (float), `split_cash_amount` (float), `split_cash_status` (string) zu hinzu:
* `Magento\Quote\Api\Data\CartInterface`
* `Magento\Sales\Api\Data\OrderInterface`
* `Magento\Sales\Api\Data\OrderPaymentInterface`

#### &#x200B;3. REST-Endpunkte (`etc/webapi.xml`)

```xml
POST /V1/split-payment/set              → anonymous (session-scoped)
POST /V1/split-payment/orders/:orderId/cash-received  → Magento_Sales::actions
POST /V1/split-payment/orders/:orderId/cash-decline   → Magento_Sales::cancel
```

Alle drei sind `Client\SplitPayment\Api\SplitPaymentManagementInterface` zugeordnet.

#### &#x200B;4. I/O-Ereignisse (`etc/io_events.xml`)

`observer.sales_order_place_before` abonnieren und Felder einschließen:
`entity_id`, `quote_id`, `increment_id`, `subtotal`, `split_store_credit_amount`, `split_cash_amount`, `split_cash_status`

#### &#x200B;5. `SplitPaymentSession` — Sitzungs-Wrapper

Speichert deklarierte aufgeteilte Beträge in der Kassensitzung. Muss Folgendes offenlegen:
* `setAmounts(float $storeCredit, float $cash): void`
* `getAmounts(): array` — gibt `['store_credit' => float, 'cash' => float]` zurück
* `clear(): void`
* `beginBalanceApply(): void` - Legt eine Markierung fest, die das Plug-in „Grand Total Fix“ während des Antrags auf Gutschrift speichern unterdrückt
* `endBalanceApply(): void`
* `isBalanceApplyInProgress(): bool`

#### &#x200B;6. `SplitPaymentManagement` — REST-Controller

**`setSplitPayment(float $storeCreditAmount, float $cashAmount, ?string $cartId = null): bool`**
* Validiert den Warenkorb, der zur aktuellen Sitzung gehört (durch Vergleich numerischer und maskierter Anführungszeichen-IDs)
* Speichert Beträge in `SplitPaymentSession`
* Gibt bei Erfolg `true` zurück; gibt bei Fehlschlag `LocalizedException` mit allgemeiner Meldung aus.

**`markCashReceived(int $orderId): bool`**
* Lädt Reihenfolge nach `entity_id`
* Validiert `split_cash_status === 'pending'`
* Setzt Status auf `received`, Status auf `processing`
* Fügt einen Verlaufskommentar hinzu: `"Cash payment of $X.XX received."`
* Aufrufe `SplitInvoiceService::createCashPortionInvoice($orderId)`
* Fügt einen Kommentar mit der Inkrement-ID der Kassenrechnung hinzu
* Anrufe `createShipmentIfPossible($orderId)` - Erstellt eine Lieferung mit `ShipOrder::execute()`, wenn versandfähige Artikel vorhanden sind
* Gibt `true` zurück; gibt bei einem Fehler eine generische `LocalizedException` aus.

**`markCashDeclined(int $orderId): bool`**
* Ladereihenfolge
* Validiert `split_cash_status === 'pending'`
* Validiert `$order->canCancel()`
* Setzt den Status auf `declined`, fügt Kommentar hinzu: `"Cash payment declined (simulated fraud check)."`
* Speichert die Bestellung
* Aufrufe `OrderManagement::cancel($orderId)`
* Gibt `true` zurück; löst bei einem Fehler eine generische `LocalizedException` aus

#### &#x200B;7. `PlaceOrderPlugin` — aroundPlaceOrder auf `QuoteManagement`

Dies ist das wichtigste Plug-in. Ausführungen `aroundPlaceOrder`:

1. Angebot laden; falls nicht aktiv, sofort `$proceed()` aufrufen
2. `SplitPaymentSession::getAmounts()` lesen
3. Wenn das Angebot `customer_balance_amount_used > 0` wird, rufen Sie `BalanceManagementInterface::remove($cartId)` auf (`LocalizedException` behandeln — als allgemeine Nachricht protokollieren und erneut auslösen)
4. `recollectQuoteForBalanceOperation()` aufrufen — lädt Angebot, ruft `collectTotals()` auf, speichert (innerhalb von `beginBalanceApply()` / `endBalanceApply()`, um das Plug-in für die Gesamtreparatur zu unterdrücken)
5. Falls `$storeCredit > 0`, `BalanceManagementInterface::apply($cartId, $storeCredit)` aufrufen (Fehler beheben)
6. Angebot neu laden; Erweiterungsattribute festlegen: `split_store_credit_amount`, `split_cash_amount`, `split_cash_status = 'pending'`
7. `payment->additional_information['client_split_payment']` als `['store_credit' => x, 'cash' => y]` speichern
8. Zitat speichern
9. `$proceed()`, ID der Erfassungsreihenfolge
10. `SplitPaymentSession::clear()`
11. Kennung der Rücksendung

#### &#x200B;8. `CopySplitPaymentToOrder` — Beobachter auf `sales_model_service_quote_submit_before`

Liest aufgeteilte Beträge aus Sitzungs- → Zahlungs-Zusatzinformationen → Angebotserweiterungsattributen (in dieser Prioritätsreihenfolge). Schreibt `split_store_credit_amount`, `split_cash_amount`, `split_cash_status = 'pending'` in das Bestellobjekt.

#### &#x200B;9. `AutoInvoiceStoreCreditOnOrderPlace` — Beobachter auf `sales_order_place_after`

Wenn der Auftrag nach der Auftragserteilung über einen Store-Guthabenbetrag (`split_store_credit_amount > 0`) verfügt, rufen Sie `SplitInvoiceService::createStoreCreditPortionInvoice($orderId)` an, um den Store-Guthabenanteil sofort zu fakturieren.

#### 10. `SplitInvoiceService`

**`createStoreCreditPortionInvoice(int $orderId): ?int`**
Erstellt eine Rechnung nur für den Gutschriftanteil des Geschäfts. Setzt `customer_balance_amount` auf der Rechnung auf den Gutschriftsbetrag. Registriert und speichert die Rechnung. Gibt bei einem Fehler die Rechnungsentitäts-ID oder null aus (Protokoll; nicht erneut auslösen).

**`createCashPortionInvoice(int $orderId): ?int`**
Erstellt eine Rechnung für den Baranteil (die verbleibenden Auftragspositionen/Beträge, die nicht von der SC-Rechnung abgedeckt sind). Registriert und speichert. Gibt bei einem Fehler die Entitäts-ID oder null zurück.

#### &#x200B;11. `CheckoutPlugin` — `PaymentInformationManagement`

Plug-in auf `Magento\Checkout\Model\PaymentInformationManagement::savePaymentInformationAndPlaceOrder`. Bevor Sie fortfahren:
* Laden des Angebots aus der Checkout-Sitzung
* Abrufen des konfigurierten Schwellenwerts: `Magento\Framework\App\Config\ScopeConfigInterface::getValue('split_payment/general/threshold')`, `100`
* Wenn `$quote->getGrandTotal() > $threshold`, werfen Sie `LocalizedException('Payment could not be processed. Please try again or contact support.')`

#### &#x200B;12. `CapCustomerBalanceCollectPlugin` — auf `Customerbalance` Gesamtbetrag

Nach der Ausführung des nativen Sammelvorgangs für den Kundensaldo ist die Obergrenze auf `customer_balance_amount_used` zu `SplitPaymentSession::getAmounts()['store_credit']`. Dadurch wird verhindert, dass Commerce den gesamten Kundensaldo überzieht, wenn der Kunde einen kleineren Anteil des Filialguthabens angegeben hat.

#### &#x200B;13. `FixSplitPaymentGrandTotalPlugin` — `Quote\Address\Total\Grand`

Nach der Gesamterhebung der Gesamtsumme: Wenn eine Aufspaltungszahlungssitzung vorhanden ist und `isBalanceApplyInProgress()` „false“ ist, setzen Sie die Gesamtsumme des Angebots auf den Barbetrag der Sitzung. Dadurch wird in der Benutzeroberfläche an der Kasse nur angezeigt, was in bar fällig ist.

#### &#x200B;14. `FixInvoiceCustomerBalanceAfterTotalsPlugin` — `Sales\Model\Order\Invoice`

Wenn die zugehörige Bestellung der Rechnung nach dem Einzug der Rechnungssummen einen `split_sc_invoice_id` aufweist, korrigieren Sie die `customer_balance_amount` auf der Rechnung, um eine doppelte Zuordnung der Warenkorbgutschrift zu verhindern.

#### &#x200B;15. `SplitPaymentZeroTotalPlugin` — `Payment\Model\Checks\ZeroTotal`

Nachnahme bei `SplitPaymentSession::getAmounts()['cash'] > 0` zulassen, auch wenn die Gesamtsumme des Angebots 0 USD beträgt (da die gesamte Bestellung durch eine Gutschrift im Geschäft abgedeckt ist).

#### &#x200B;16. `LayoutProcessorPlugin` — `Checkout\Block\Checkout\LayoutProcessor`

Nachdem das Layout verarbeitet wurde:
* Fügen Sie die `Client_SplitPayment/js/view/payment/split-payment` Komponente in die `additional` untergeordneten Elemente der Komponente `cashondelivery` Zahlungsmethode unter `components.checkout.children.steps.children.billing-step.children.payment.children.renders.children.offline-payments.children.cashondelivery.children.additional` ein.
* Entfernen Sie die native UI-Komponente „Store-Guthaben“ (`customerBalance`, `useStoreCredit`) aus dem Zahlungsschritt - die Split-Zahlungskomponente steuert die Anzeige/Anwendung der Store-Guthaben

#### &#x200B;17. `OrderRepositoryPlugin` — `OrderRepositoryInterface`

Hydrieren Sie nach dem `get()` und `getList()` die Erweiterungsattribute der Bestellung aus den flachen `sales_order` (`split_store_credit_amount`, `split_cash_amount`, `split_cash_status`).

#### &#x200B;18. `AdminSplitPaymentTitlePlugin` — `Payment\Block\Info`

Wenn nach `getTitle()` Rückgabe die Zahlungsmethode `cashondelivery` ist und die Bestellung eine aufgeteilte Zahlung aufweist, hängen Sie `" (Split: Cash $X.XX + Store Credit $Y.YY)"` an den Titel an.

#### &#x200B;19. `OrderPaymentPlugin` — `Sales\Block\Adminhtml\Order\Payment`

Hängen Sie in `_beforeToHtml` oder über „afterToHtml“ die aufgeteilten Zahlungsdetails (Barbetrag, Kreditbetrag speichern, Status) an den Zahlungsblock &quot;HTML&quot; in der Commerce Admin-Auftragsansicht an.

#### &#x200B;20. Storefront Store-Guthabencontroller

`Controller/Checkout/StoreCreditBalance.php` — Strecke: `GET /splitpayment/checkout/storecreditbalance`

Gibt JSON zurück: `{"balance": float, "logged_in": bool}`. Wenn der Kunde nicht angemeldet ist, gibt `{"balance": 0, "logged_in": false}` zurück. Liest den Saldo aus `Magento\CustomerBalance\Model\Balance`.

Registrieren Sie die Frontend-Route in `etc/frontend/routes.xml` bei `frontName="splitpayment"`.

#### &#x200B;21. Checkout-KnockoutJS-Komponente — `split-payment.js`

Eine `uiComponent`, die:
* Ermittelt, wann die `cashondelivery` Zahlungsmethode ausgewählt ist (`quote.paymentMethod.subscribe`)
* Lädt den Speicherguthaben-Saldo des Kunden über `GET /splitpayment/checkout/storecreditbalance`
* Füllen Sie das Feld Barbetrag mit der vollständigen Bestellsumme vorab aus (berechnet aus `total_segments` ohne `grand_total` und `customerbalance` - verwendet `grand_total` nie direkt, da dies auf den Barrest gesetzt werden kann).
* Wenn der Kunde die Eingabe des Barbetrags ändert: Berechnet den erforderlichen Warenkredit = Bestellsumme − Bargeld; validiert; Beiträge zu `POST /V1/split-payment/set`
* Zeigt Validierungsnachrichten für: Bargeld > Bestellsumme, unzureichende Speichergutschrift, nicht angemeldet
* Zeigt eine Erfolgsmeldung an, wenn eine gültige Aufspaltung eingegeben wird: `"The remaining $X.XX will automatically be applied from your store credit."`
* Wird zurückgesetzt, wenn eine andere Zahlungsmethode ausgewählt wird (veröffentlicht `{storeCreditAmount: 0, cashAmount: 0}`, um die Sitzung zu löschen)

#### 22. `cashondelivery-method.js`

Erweitert `Magento_OfflinePayments/js/view/payment/offline-payments`. Verwendet `payment-method-helper.js` zur Erkennung des Bargeldmethodencodes. Registriert `split-payment` Komponente in ihrer `additional`.

#### 23. `payment-method-helper.js`

Dienstprogramm gibt `getCashMethodCode()` zurück — prüft `window.checkoutConfig.paymentMethods` auf `cashondelivery`; kehrt bei Bedarf auf `checkmo` zurück.

#### &#x200B;24. `cashondelivery.html` Vorlage

Standard-CSV-Vorlage, aber enthält `<!-- ko foreach: getRegion('additional') -->` Region, damit die untergeordnete Komponente für aufgeteilte Zahlungen gerendert werden kann.

#### &#x200B;25. `split-payment.html` Vorlage

KnockoutJS-Vorlage für die Aufspaltungszahlungsfelder:
* Anzeige des Kontostands des verfügbaren Speichers
* Eingabe des Barbetrags (Nummer, Schritt 0.01)
* Anzeige des Gutschriftanteils speichern (schreibgeschützt)
* Automatische Anwendung der Store-Gutschrift-Nachricht (wird angezeigt, wenn die Aufspaltung gültig ist, und Store-Gutschrift > 0)
* Validierungsfehlermeldung

#### 26. `requirejs-config.js`

Karten:
* `Client_SplitPayment/js/view/payment/split-payment` → Komponente
* `Client_SplitPayment/js/view/payment/cashondelivery-method` → der COD-Überschreibung
* `Client_SplitPayment/js/model/payment-method-helper` → Helfers

#### 27. `etc/config.xml`

Standardwerte der Systemkonfiguration:

```xml
<split_payment>
  <general>
    <threshold>100</threshold>
    <enabled>1</enabled>
  </general>
</split_payment>
```


### Wichtige Implementierungshinweise

**Store-Kreditantrag muss `BalanceManagementInterface` verwenden, nicht die direkte Modellbearbeitung.** `BalanceManagementInterface::apply()` handhabt die Sitzung, die Validierung und die Neuberechnung des Warenkorbs automatisch.

**`PlaceOrderPlugin`muss `aroundPlaceOrder` (nicht `beforePlaceOrder`) verwenden.** Das Store-Guthaben muss angewendet werden, während der Warenkorb noch aktiv ist, und das muss garantiert werden, bevor `$proceed()` aufgerufen wird.

**Das Sitzungs-Flag-Muster für `beginBalanceApply`/`endBalanceApply` ist wichtig.** Andernfalls läuft `FixSplitPaymentGrandTotalPlugin` während der `collectTotals()` innerhalb des Saldovorgangs und setzt die Gesamtsumme auf den Rest des Bargelds, was dazu führt, dass `BalanceManagementInterface::apply()` scheitert oder den Kredit begrenzt wird.

**Geben Sie dem Kunden niemals interne Fehlerdetails an.** Alle `catch`, die REST-Antworten zuführen, müssen `LocalizedException('Payment could not be processed. Please try again or contact support.')`.

**`entity_id`ist die numerische Datenbank-ID.** REST-Aufrufe aus App Builder verwenden immer `entity_id`, nicht `increment_id`.

**`SplitInvoiceService`sollten Fehler erfassen und protokollieren, anstatt sie zu propagieren.** Fehlgeschlagene Rechnungserstellung sollte eine bereits platzierte Bestellung nicht stornieren - protokollieren Sie den Fehler und lassen Sie ihn vom Administrator manuell bearbeiten.


### Nach dem Generieren von Dateien

Führen Sie diese Befehle im Commerce-Projektstamm aus:

```bash
bin/magento module:enable Client_SplitPayment
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento setup:static-content:deploy -f
bin/magento cache:flush
```

### Ende der Eingabeaufforderung


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
