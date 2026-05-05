---
title: Schritt-für-Schritt-Implementierungshandbuch für Split Payment POC
description: 'Erfahren Sie, wie Sie den aufgeteilten Zahlungs-POC implementieren, um nach Abschluss der Einrichtung folgende Punkte zu berücksichtigen: Module, Umgebungen, Orchestrator, Verifizierung und optionale Benutzeroberfläche.'
feature: App Builder, Eventing, Extensibility
topic: Commerce, Architecture, App Builder, Development
role: Developer
level: Intermediate
doc-type: Tutorial
duration: 480
jira: KT-20902
last-substantial-update: 2026-04-30T00:00:00Z
source-git-commit: 27811c05f066c95a60ac309472d6488295fb2c96
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---

# Schritt-für-Schritt-Implementierungshandbuch für Split Payment POC

Diese Seite ist die Checkliste für Ihre Implementierung. Es wird davon ausgegangen, dass Sie bereits die [Übersicht](./overview.md) und die [vollständige Demo](./full-demo.md) gesehen haben und dass Ihre Commerce-Site und Ihr App Builder-Projekt beide bereit sind. Die einzelnen Tutorial-Seiten enthalten vollständige Details zu jedem Thema unten - verwenden Sie diese Seite, um zu wissen, was zu tun ist und in welcher Reihenfolge.

## Bevor Sie beginnen

Bestätigen Sie alles Folgende, bevor Sie eine Eingabeaufforderung oder einen Befehl ausführen. Auf [&#x200B; Seite „Voraussetzungen und Setup](./prerequisites-and-setup.md) werden die einzelnen Elemente detailliert behandelt.

**Commerce-Seite**

* [ ] Adobe Commerce 2.4.5 oder höher
* [ ] I/O Eventing aktiviert und bereitgestellt (nur Commerce Cloud - `ENABLE_EVENTING: true` in `.magento.env.yaml` erforderlich)
* [ ] **Nachnahme** in Admin aktiviert, wobei der Titel genau auf `Cash` gesetzt ist
* [ Gutschrift für ] in Admin aktiviert
* [ ] Testkunde hat mindestens $50 Speicherguthaben
* [ ] Commerce-Integration erstellt, aktiviert und alle vier OAuth-Werte sicher gespeichert

**App Builder-Seite**

* [ ] App Builder-Projekt ist in Adobe Developer Console vorhanden
* [ ] zum Arbeitsbereich hinzugefügter Adobe I/O Events-Service
* [ ] Commerce als Ereignisanbieter verbunden
* [ ] `aio login` abgeschlossen; korrekter Arbeitsbereich mit `aio app use` ausgewählt
* [ ] Node.js 18 oder höher installiert; `aio` CLI installiert (`npm install -g @adobe/aio-cli`)

Wenn etwas oben Genanntes fehlt, stoppen Sie hier und schließen Sie es zuerst ab.

## Phase 1: Erstellen des Commerce-Moduls

**Was dies tut:** Erzeugt das `Client_SplitPayment` PHP-Modul, das die Checkout-Benutzeroberfläche, die Store-Kreditanwendung, REST-Endpunkte und das I/O-Ereignis-Abonnement verwaltet. Dies ist der Thin-In-Commerce-Adapter. Alle Benutzer-Workflows verbleiben in App Builder.

### Schritt 1.1 - Passen Sie die Eingabeaufforderung für Ihr Projekt an

Öffnen Sie die Seite [Commerce Module AI Prompt](./commerce-module-prompt.md) und beachten Sie Folgendes, bevor Sie die Prompt kopieren:

* Ersetzen Sie in der Eingabeaufforderung `Client` durch den tatsächlichen Anbieternamen.
* Ersetzen Sie `SplitPayment` , wenn Sie einen anderen Modulnamen verwenden möchten
* Wenn es sich bei Ihrem Design nicht um Luma handelt, müssen der `LayoutProcessorPlugin`-Einfügepfad und die RequireJS-Zuordnungen möglicherweise angepasst werden
* Wenn Ihre Cash on Delivery-Methode einen anderen Code als `cashondelivery` verwendet, aktualisieren Sie `payment-method-helper.js`

### Schritt 1.2 - Eingabeaufforderung ausführen

Kopieren Sie die vollständige Eingabeaufforderung von **PROMPT START** nach **End of prompt** und fügen Sie sie in den Cursor (mit Claude) oder direkt in Claude ein. Führen Sie sie aus dem Stammverzeichnis Ihres Commerce-Projekts aus, damit die KI Dateien unter `app/code/` erstellen kann.

### Schritt 1.3 — Modul aktivieren und installieren

Führen Sie diese Befehle aus Ihrem Commerce-Projekt-Stammverzeichnis aus:

```bash
bin/magento module:enable Client_SplitPayment
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento setup:static-content:deploy -f
bin/magento cache:flush
```

### Schritt 1.4 — Überprüfen der korrekten Installation des Moduls

```bash
# Confirm the module is active
bin/magento module:status Client_SplitPayment

# Confirm the split_ columns were added to sales_order
mysql -u <user> -p <dbname> -e "DESCRIBE sales_order;" | grep split
```

Es sollten fünf Spalten angezeigt werden: `split_store_credit_amount`, `split_cash_amount`, `split_cash_status`, `split_sc_invoice_id` und `split_cash_invoice_id`.

Bestätigen Sie dann in einem Browser, dass die Aufspaltungs-Zahlungsfelder an der Kasse angezeigt werden, wenn ein angemeldeter Kunde mit Store-Guthaben **Bargeld** als Zahlungsmethode auswählt.

## Phase 2 - Konfigurieren von Umgebungsvariablen

**Funktion:** Bereitet die vom App Builder Orchestrator, dem Simulationsskript und (optional) der Experience Cloud-Benutzeroberflächenerweiterung verwendeten Berechtigungsdateien vor. In jeder `.env`-Datei werden die gleichen vier OAuth-Werte aus Ihrer Commerce-Integration verwendet.

Die vollständige Liste [&#x200B; Variablen pro Komponente finden &#x200B;](./env-reference.md) in der „Umgebungsvariablen-Referenz .

### Schritt 2.1 - Orchestrierungs-`.env` erstellen

In Ihrem `split-payment-orchestrator/`:

```bash
cp .env.example .env
```

Füllen Sie alle Werte aus:

| Variable | Bezugsquellen |
|---|---|
| `COMMERCE_BASE_URL` | Ihre Store-URL - kein Schrägstrich |
| `COMMERCE_CONSUMER_KEY` | Commerce Admin > System > Integrationen |
| `COMMERCE_CONSUMER_SECRET` | Gleich — wird nur bei Aktivierung angezeigt |
| `COMMERCE_ACCESS_TOKEN` | selbe |
| `COMMERCE_ACCESS_TOKEN_SECRET` | selbe |
| `PAYMENT_THRESHOLD` | Muss mit `split_payment/general/threshold` in Commerce übereinstimmen (Standard: `100`) |
| `DEMO_UI_SECRET` | Optional - falls festgelegt, wie in der Dashboard-URL `?secret=` erforderlich |

### Schritt 2.2 - Simulationsskript-`.env` erstellen

```bash
cp commerce-backend-ui-1/.env.simulation.example commerce-backend-ui-1/.env.simulation
```

Geben Sie `COMMERCE_BASE_URL` und die vier OAuth-Werte (dieselben Anmeldeinformationen wie oben) ein.

## Phase 3: Erstellen des App Builder Orchestration

**Funktion:** Erzeugt das `split-payment-orchestrator` App Builder-Projekt: den `payment-orchestrator` I/O Event Consumer, die `payment-accept` und `payment-decline` Web-Aktionen sowie die Benutzeroberfläche des `demo-dashboard`-Benutzers.

### Schritt 3.1 - Orchestrierungsaufforderung ausführen

Öffnen Sie die Seite mit der Eingabeaufforderung für die App Builder Orchestrator-[&#128279;](./orchestrator-prompt.md). Kopieren Sie die vollständige Eingabeaufforderung und führen Sie sie aus dem Verzeichnis `split-payment-orchestrator/` aus.

### Schritt 3.2 - Installieren von Abhängigkeiten und Bereitstellen

```bash
cd split-payment-orchestrator
npm install
# Confirm .env is filled in (from Phase 2, Step 2.1)
aio app deploy
```

Nach der Bereitstellung druckt `aio app deploy` die Aktions-URLs. Notieren Sie sich die `demo-dashboard` URL - Sie benötigen sie in Phase 4.

### Schritt 3.3 — Registrierung der Veranstaltung bestätigen

Öffnen Sie in Adobe Developer Console Ihren App Builder-Projektarbeitsbereich. Bestätigen **unter** Ereignisse“, dass die `Split payment — sales order place before` vorhanden und an die `payment-orchestrator` gebunden ist.

## Phase 4 — Testen des vollständigen Durchflusses

Führen Sie die Überprüfungsschritte der Reihe nach durch. Das [Test- und Verifizierungshandbuch](./testing-and-verification.md) enthält die vollständigen cURL-Befehle, die Verwendung des Simulationsskripts und die Referenz zur Fehlerbehebung für jeden der folgenden Schritte.

### Schritt 4.1 — Überprüfen, ob REST-Endpunkte routbar sind

```bash
# Expect 401, not 404 — the endpoint exists but requires auth
curl -X POST https://your-store.example.com/rest/V1/split-payment/orders/1/cash-received
```

### Schritt 4.2 — Testen der Checkout-Benutzeroberfläche

1. Melden Sie sich bei der Storefront als Testkunde an (der Kunde mit Gutschrift im Store)
2. Produkt zum Warenkorb hinzufügen mit einer Gesamtsumme von unter 100 $ nach Versand und Steuer
3. Wählen Sie beim Zahlungsschritt &quot;**&quot;**
4. Bestätigen Sie, dass die aufgeteilten Zahlungsfelder angezeigt werden: Saldo angezeigt, Bargeld vorausgefüllt, Guthaben bei $0 speichern
5. Reduzieren Sie den Barbetrag und bestätigen Sie, dass der Gutschriftanteil des Geschäfts korrekt aktualisiert wird

### Schritt 4.3 — Schwellenwertbegrenzer prüfen

Fügen Sie Produkte mit einem Gesamtwert von mehr als 100 USD hinzu, gehen Sie zur Kasse, wählen Sie „Bargeld“ aus und versuchen Sie, die Bestellung aufzugeben. Die `"Payment could not be processed. Please try again or contact support."` muss angezeigt werden.

### Schritt 4.4 — Aufspaltung des Zahlungsauftrags testen

Erstellen Sie einen Warenkorb unter $100, geben Sie eine Cash/Store-Kreditaufteilung ein und geben Sie die Bestellung auf. Bestätigen Sie in Commerce Admin Folgendes:

* Bestellstatus ist `pending_payment`
* Auf der Bestellung sind zwei Kommentare aus App Builder zu sehen:
   1. `"Cash payment of $X.XX pending. Awaiting admin confirmation."`
   2. `"Split payment orchestration completed. Order awaiting cash confirmation."`

Wenn keine App Builder-Kommentare angezeigt werden, überprüfen Sie die Protokolle mit `aio app logs`, bevor Sie fortfahren.

### Schritt 4.5 — Testannahme über Simulationsskript

```bash
# Find your order's entity_id
node commerce-backend-ui-1/scripts/simulate-split-payment.mjs list

# Accept the payment
node commerce-backend-ui-1/scripts/simulate-split-payment.mjs accept <entity_id>
```

Bestätigen Sie in Commerce Admin Folgendes:

* Bestellstatus in `processing` geändert
* Verlaufskommentar: `"Cash payment of $X.XX received."`
* Barrechnung auf der Registerkarte „Rechnungen“ sichtbar
* Sendung auf der Registerkarte „Sendungen“ (falls zutreffend)

### Schritt 4.6 — Testrückgang über Simulationsskript

Geben Sie eine weitere Testreihenfolge ein, dann:

```bash
node commerce-backend-ui-1/scripts/simulate-split-payment.mjs decline <entity_id>
```

Bestätigen Sie, dass der Bestellstatus `canceled` und `split_cash_status` `declined` ist.

### Schritt 4.7 - Demo-Dashboard testen

Öffnen Sie die Dashboard-URL aus Schritt 3.2. Mit ausstehender Bestellung im System:

1. Bestätigen Sie, dass die Reihenfolge in der Liste Ausstehend angezeigt wird
2. Klicken Sie **Akzeptieren** und bestätigen Sie, dass die Bestellung in Commerce zu `processing` verschoben wird
3. Erteilen Sie eine neue Bestellung, kehren Sie zum Dashboard zurück und klicken Sie auf **Ablehnen** — Stornierung bestätigen

## Phase 5 (optional) - Hinzufügen der Experience Cloud-Benutzeroberflächenerweiterung

In dieser Phase wird das Benutzer-Dashboard in die Commerce Admin Shell eingebettet, anstatt die eigenständige `demo-dashboard` zu verwenden. Überspringen Sie diese Phase, wenn das eigenständige Dashboard Ihren Anforderungen entspricht.

### Schritt 5.1 — Voraussetzungen überprüfen

Die Experience Cloud UI-Erweiterung erfordert zusätzlich zu den OAuth-Integrationswerten IMS-Anmeldeinformationen. Lesen Sie die Seite [Experience Cloud UI Extension AI Prompt](./experience-cloud-ui-prompt.md) , bevor Sie die Eingabeaufforderung ausführen, und achten Sie auf die `OAUTH_CLIENT_ID` und die zugehörigen IMS-Variablen.

### Schritt 5.2 - Benutzeroberflächenerweiterungs-Eingabeaufforderung ausführen

Kopieren Sie die vollständige Eingabeaufforderung von **PROMPT START** nach **End of prompt** und führen Sie sie im `commerce-checkout-starter-kit/` aus.

### Schritt 5.3 — Bereitstellen

```bash
cd commerce-checkout-starter-kit
npm install
cp .env.dist .env
# Fill in IMS credentials and COMMERCE_INTEGRATION_* credentials
aio app deploy
```

## Kurzanleitung zur Fehlerbehebung

| Symptom | Zu überprüfende erste Elemente |
|---|---|
| Aufspaltete Zahlungsfelder werden nicht an der Kasse angezeigt | Anfordern von JS-Fehlern in der Browser-Konsole; auch `bin/magento cache:flush` ausführen |
| `"Payment could not be processed"` | `PlaceOrderPlugin` oder `BalanceManagementInterface` - Fügen Sie in `PlaceOrderPlugin` eine temporäre Debug-Protokollierung hinzu |
| Keine App Builder-Kommentare zur Bestellung | Führen Sie `aio app logs` aus, um zu sehen, ob das Ereignis ausgelöst wurde und welche Aktion zurückgegeben wurde |
| `403` aus Commerce REST in App Builder | Schnelle IP-Zulassungsauflistung - zuerst mit dem Simulationsskript testen. Wenn das funktioniert, besteht das Problem in der Sperrung der Ausgangs-IP |
| `"The signature is invalid"` aus Commerce | Bestätigen, dass `COMMERCE_BASE_URL` keinen Schrägstrich enthält; Bestätigen, dass die Integration aktiviert ist |
| Bestellungen werden nicht im Demo-Dashboard angezeigt | Überprüfen, ob `extension_attributes.split_cash_status` in einer direkten `GET /rest/V1/orders`-Antwort angezeigt wird |

Umfassende Informationen zur Fehlerbehebung finden Sie im [Test- und Verifizierungshandbuch](./testing-and-verification.md#common-issues-and-fixes).

{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
