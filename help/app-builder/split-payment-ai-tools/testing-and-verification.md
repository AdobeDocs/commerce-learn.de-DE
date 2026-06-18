---
title: Aufspaltung des Zahlungs-POC — Test- und Verifizierungshandbuch
description: Erfahren Sie, wie Sie den aufgeteilten Zahlungs-POC überprüfen. Commerce-Installation, REST, Checkout, Schwellenwert, Annahme und Ablehnung von Simulationen, Demo-Dashboard und App Builder-Protokolle.
feature: App Builder, Configuration, Extensibility, Paas, Payments, REST, Orders
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, User
level: Intermediate
doc-type: Tutorial
duration: 359
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 63ac13d8c5a97ee81dcdd1f3785a9875aaf2a4db
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 0%

---

# Split Payment POC: Test- und Verifizierungshandbuch

Dieses Handbuch führt Sie durch die Überprüfung, ob jede Komponente korrekt funktioniert, und zwar in der Reihenfolge, in der sie getestet werden soll. Beginnen Sie von unten (Commerce-Modul) und arbeiten Sie nach oben (App Builder).


## Schritt 1: Überprüfen der Commerce-Modulinstallation

Nach Ausführung von `bin/magento setup:upgrade` und `bin/magento setup:di:compile`:

```bash
# Confirm module is enabled
bin/magento module:status Client_SplitPayment

# Confirm db_schema columns were added
bin/magento doctrine:schema:validate
# or check directly:
mysql -u <user> -p <dbname> -e "DESCRIBE sales_order;" | grep split
```

Erwartete Ausgabe: vier Spalten, beginnend mit `split_` in `sales_order` sichtbar.


## Schritt 2: Überprüfen der Commerce Admin-Konfiguration

In Commerce Admin:
1. **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Payment Methods]** — Bestätigen, dass **[!UICONTROL Cash On Delivery]** mit `Cash` aktiviert ist
2. **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Customers]** > **[!UICONTROL Customer Configuration]** > **[!UICONTROL Store Credit Options]** — Bestätigung aktiviert
3. Bestätigen Sie, dass Ihr Testkunde über ein Filialguthaben verfügt: **[!UICONTROL Customers]** > **[!UICONTROL All Customers]** > *[Kunde]* > **[!UICONTROL Store Credit]**


## Schritt 3: Überprüfen, ob REST-Endpunkte zugänglich sind

Verwenden Sie curl , um zu bestätigen, dass die Endpunkte reagieren (sie werden nicht autorisierte Anfragen ablehnen, aber eine 401 bestätigt, dass sie korrekt weitergeleitet werden):

```bash
# Should return 401 (not 404) — endpoint exists but requires auth
curl -X POST https://your-store.example.com/rest/V1/split-payment/orders/1/cash-received

# Should return 200 or session-based response — anonymous endpoint
curl -X POST https://your-store.example.com/rest/V1/split-payment/set \
  -H "Content-Type: application/json" \
  -d '{"storeCreditAmount": 0, "cashAmount": 0}'
```


## Schritt 4: Testen der Checkout-Benutzeroberfläche

1. Melden Sie sich bei der Storefront als Testkunde an (der über Storeguthaben verfügt)
2. Produkt zum Warenkorb hinzufügen (insgesamt unter 100 $ nach Versand + Steuer)
3. Zur Kasse gehen
4. Wählen Sie beim Zahlungsschritt &quot;**&quot;** oder „Nachnahme„)
5. Überprüfen Sie, ob die Aufspaltungszahlungsfelder angezeigt werden:
   * Ihr Ladenguthaben wird angezeigt
   * Das Feld „Barbetrag“ ist mit der Bestellsumme vorausgefüllt.
   * Feld „Gutschrift für diese Bestellung speichern“ mit 0,00 $ (da bar = gesamte Bestellsumme)
6. Reduzieren Sie den Barbetrag (geben Sie z. B. 10 $ für eine Bestellung von 50 $ ein).
7. Überprüfen Sie, ob der Store-Guthabenanteil auf $40.00 aktualisiert wird.
8. Überprüfen Sie, ob die Meldung angezeigt wird: `"The remaining $40.00 will automatically be applied from your store credit."`

**Testvalidierung:**
* Geben Sie einen Barbetrag ein, der größer ist als die Fehlermeldung → Bestellsumme
* Geben Sie einen Barbetrag ein, der mehr Speichergutschrift erfordert als → Fehlermeldung verfügbar ist
* Bargeld = 0 → Fehler eingeben (oder die Speichergutschrift deckt die gesamte Bestellung ab)


## Schritt 5 — Prüfschwellenwertbegrenzer

1. Produkte mit einer Gesamtsumme von mehr als 100 $ hinzufügen (Zwischensumme + Versand + Steuer > 100 $)
2. Gehen Sie zur Kasse, wählen Sie **Bargeld**
3. Versuch, die Bestellung aufzugeben
4. Überprüfen Sie, ob die Fehlermeldung angezeigt wird: `"Payment could not be processed. Please try again or contact support."`
5. Überprüfen, ob der Warenkorb beibehalten wird (Kunde kann den Warenkorb weiterhin anpassen und es erneut versuchen)


## Schritt 6: Aufspaltung des Zahlungsauftrags testen

1. Warenkorb unter $100 erstellen (beim Kunden mit Shop-Guthaben angemeldet)
2. Bargeld an der Kasse auswählen
3. Geben Sie einen Geldbetrag ein, der kleiner ist als die Bestellsumme (z. B. 10 USD einer Bestellung von 45 USD)
4. Bestätigen Sie, dass die Store-Kreditmeldung angezeigt wird
5. Klicken Sie **Bestellung aufgeben**

Überprüfen Sie nach der Bestellplatzierung in Commerce Admin:
* Bestellung befindet sich im Status `pending_payment`
* Bestellung hat zwei Verlaufskommentare:
   1. `"Cash payment of $X.XX pending. Awaiting admin confirmation."` (aus App Builder `payment-orchestrator`)
   2. `"Split payment orchestration completed. Order awaiting cash confirmation."` (aus App Builder)
* Die aufgeteilten Zahlungsbeträge sind im Block „Bestellzahlung“ sichtbar

> **Wenn keine App Builder-Kommentare angezeigt werden:** Überprüfen Sie die App Builder-Aktionsprotokolle mit `aio app logs`. Das Ereignis wurde möglicherweise nicht ausgelöst oder die Aktion weist möglicherweise einen Fehler auf.


## Schritt 7 — Akzeptieren von Tests über ein Simulationsskript

Das Simulationsskript ist die schnellste Möglichkeit, den Akzeptanz-/Ablehnungsfluss ohne die vollständige Benutzeroberfläche zu testen.

```bash
cd commerce-checkout-starter-kit
cp commerce-backend-ui-1/.env.simulation.example commerce-backend-ui-1/.env.simulation
# Edit .env.simulation with your credentials

# List recent orders (find your test order entity_id)
node commerce-backend-ui-1/scripts/simulate-split-payment.mjs list

# Show split payment fields for a specific order
node commerce-backend-ui-1/scripts/simulate-split-payment.mjs show 42

# Accept the cash payment
node commerce-backend-ui-1/scripts/simulate-split-payment.mjs accept 42
```

Überprüfen Sie nach dem Akzeptieren in der Commerce Admin-Bestellansicht:
* Bestellstatus ist `processing`
* Verlaufskommentar: `"Cash payment of $X.XX received."`
* Erstellte Kassenrechnung (sichtbar auf der Registerkarte „Rechnungen„)
* Sendung erstellt (auf der Registerkarte „Sendungen“ sichtbar, falls zutreffend)
* Verlaufskommentar: `"Split payment: cash portion invoiced #XXXXXXXX."`
* Verlaufskommentar: `"Split payment: shipment created after cash was accepted (App Builder / API)."`


## Schritt 8 — Ablehnungstest mithilfe eines Simulationsskripts

Geben Sie eine weitere Testreihenfolge ein (wie in Schritt 6). Gehen Sie dann wie folgt vor:

```bash
node commerce-backend-ui-1/scripts/simulate-split-payment.mjs decline <orderId>
```

Nach der Ablehnung in Commerce Admin überprüfen:
* Bestellstatus ist `canceled`
* Verlaufskommentar: `"Cash payment declined (simulated fraud check)."`
* `split_cash_status` = `declined`


## Schritt 9 - Demo-Dashboard testen

Nach der Bereitstellung des `split-payment-orchestrator` druckt `aio app deploy` die Aktions-URLs.

Öffnen Sie die `demo-dashboard`-URL in einem Browser:

```
https://[runtime-host]/api/v1/web/split_payment_orchestrator/demo-dashboard
```

Wenn `DEMO_UI_SECRET` festgelegt ist:

```
https://[runtime-host]/api/v1/web/split_payment_orchestrator/demo-dashboard?secret=<your-secret>
```

Mit ausstehender Bestellung:
1. Das Dashboard sollte die Reihenfolge in der Liste Ausstehend anzeigen
2. Klicken Sie **&quot;**&quot;, → in Commerce in `processing` verschoben werden soll.
3. Erneut bestellen und auf **Ablehnen** klicken, → die Bestellung in Commerce `canceled` werden soll


## Schritt 10: App Builder-Aktionsprotokolle testen

```bash
# Follow logs in real-time
aio app logs --tail

# Or view last invocations
aio runtime activation list --limit 10
aio runtime activation logs <activation-id>
```

Suchen Sie für die `payment-orchestrator` nach:

```
[INFO] Split payment orchestration finished { orderId: '42' }
```

Für `payment-accept` oder `payment-decline`:

```
[INFO] Cash payment accepted on Commerce via REST { orderId: '42' }
```


## Häufige Probleme und Fehlerbehebungen

### „Die Signatur ist ungültig“ von Commerce OAuth

**Ursache:** Uhrzeitabweichung zwischen App Builder Runtime und Commerce oder ein OAuth-Signierfehler.

**Beheben:**
* Bestätigen, `COMMERCE_BASE_URL` keinen Schrägstrich aufweist
* Bestätigen Sie, dass die vier OAuth-Anmeldeinformationen für eine (aktivierte _-Integration_.
* Testen Sie zunächst mit dem Simulationsskript . Wenn das Skript funktioniert, App Builder jedoch nicht, wird wahrscheinlich eine nicht geladene env-Variable ausgegeben (überprüfen Sie `aio app deploy` Ausgabe auf fehlende env vars)

### Aufspaltung der Zahlungsfelder wird nicht an der Kasse angezeigt

**Ursache:** LayoutProcessorPlugin-Einfügepfade stimmen nicht mit Ihrem Checkout-Layout überein.

**Beheben:**
* Überprüfen der Browser-Konsole auf „RequireJS“-Fehler beim Laden von `Client_SplitPayment/js/view/payment/split-payment`
* `bin/magento setup:static-content:deploy` erfolgreich abgeschlossen
* Leer-Cache: `bin/magento cache:flush`
* Wenn Ihr Design einen benutzerdefinierten Checkout hat, muss der `LayoutProcessorPlugin` Pfad zum Einspeisen der Komponente möglicherweise angepasst werden

### Warenkorb-Guthaben wird nicht angewendet / „Zahlung konnte nicht verarbeitet werden“ bei Bestellung

**Ursache:** Normalerweise funktioniert eines der Plug-ins für den Edge-Fall nicht ordnungsgemäß.

**Überprüfen:**
1. Gibt `SplitPaymentSession` die korrekten Beträge zurück? Temporäre Debug-Protokollierung in `PlaceOrderPlugin` hinzufügen
2. Wird `FixSplitPaymentGrandTotalPlugin` ausgeführt und wirkt sich dies auf die Angebotssumme aus, bevor `BalanceManagementInterface::apply()` aufgerufen wird? Die `beginBalanceApply()` sollte sie unterdrücken.
3. Ist das Kundenbilanzmodul in Commerce aktiviert?

### App Builder-Aktion empfängt Ereignis, aber orderId fehlt

**Ursache:** Die Liste der `io_events.xml` Felder enthält keine `entity_id` oder die Payload-Form des Ereignisses hat sich geändert.

**Beheben:**
* Bestätigen, `io_events.xml` `entity_id` in die Feldliste einfügt
* Melden Sie sich in der Aktion vorübergehend `JSON.stringify(params)`, um die vollständige Payload-Form anzuzeigen
* Überprüfen Sie, ob die `extractValue()` die richtige Verschachtelungsebene findet

### Bestellungen werden nicht im Demo-Dashboard angezeigt

**Ursache:** Commerce REST `orders` Suchkriterien geben keine Bestellungen zurück oder `split_cash_status` Feld nicht in der REST-Antwort.

**Beheben:**
* Überprüfen, `OrderRepositoryPlugin` Erweiterungsattribute korrekt geladen werden
* Direkt testen: `GET /rest/V1/orders?searchCriteria[pageSize]=5` und überprüfen, ob `extension_attributes.split_cash_status` in der Antwort angezeigt wird
* Vergewissern Sie sich, dass `extension_attributes.xml` das `split_cash_status` Attribut in `OrderInterface` korrekt deklariert.


## Verifizierungs-Checkliste

* [ ] `split_*` Spalten sichtbar in `sales_order` Tabelle
* [ ] REST-Endpunkte geben 401 (nicht 404) zurück, wenn sie ohne Authentifizierung aufgerufen werden
* [ ] Aufspaltung der Zahlungs-Benutzeroberfläche wird an der Kasse gerendert, wenn „Bargeld“ ausgewählt wird
* [ ] Validierungsnachrichten funktionieren (Überzahlung, unzureichende Gutschrift)
* [ ] Schwellenwertwächter blockiert Bestellungen > $100
* [ ] aufgegebene Bestellung hat `pending_payment` Status und App Builder-Kommentare
* [ ] `simulate-split-payment.mjs list` zeigt den Testauftrag mit aufgeteilten Beträgen an
* [ ] `simulate-split-payment.mjs accept <id>` verschiebt Bestellung mit Rechnung und Versand nach `processing`
* [ ] `simulate-split-payment.mjs decline <id>` storniert die Bestellung
* [ ] Demo-Dashboard listet ausstehende Bestellungen auf und akzeptiert/verweigert Arbeit über die Benutzeroberfläche


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
