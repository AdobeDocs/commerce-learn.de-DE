---
title: 'Aufspaltung des Zahlungs-POC: Experience Cloud UI-Erweiterung - KI-Eingabeaufforderung'
description: 'Erfahren Sie, wie Sie mit dieser optionalen Eingabeaufforderung die Aufspaltungszahlung in Commerce Admin einbetten können: Admin-Benutzeroberfläche, SDK, IMS, OAuth, Akzeptieren und Ablehnen und das Simulationsskript.'
feature: App Builder, Admin Workspace, Extensibility, Paas, REST
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Tutorial
duration: 192
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 629bbb6fe26f128e346d85c857111c2f8dbb6d76
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# Aufspaltung des Zahlungs-POC: Experience Cloud UI-Erweiterung - KI-Eingabeaufforderung

Dies ist der optionale Schritt, bei dem das Bedienfeld „Aufspaltung“ für Zahlungsaufträge mithilfe der `commerce-checkout-starter-kit` und des `commerce-backend-ui-1` in die **[!UICONTROL Adobe Commerce]** Admin Shell (Experience Cloud) eingebettet wird. Das eigenständige [Demo-Dashboard](./orchestrator-prompt.md) von App Builder Orchestrator deckt denselben Akzeptieren- und Ablehnungsfluss ohne Admin-Shell-Integration ab.

## So verwenden Sie diese Eingabeaufforderung

Kopieren Sie alles von **PROMPT START** bis **Ende der Eingabeaufforderung** in Cursor oder Claude. Führen Sie die Eingabeaufforderung im `commerce-checkout-starter-kit/` aus.

## Vor der Ausführung

* Dieser Pfad benötigt **IMS**-Anmeldeinformationen zusätzlich zu den OAuth-Werten (siehe [Aufspaltung des Zahlungs-POC: Umgebungsvariablen-Referenz](./env-reference.md) für die `commerce-checkout-starter-kit` Variablen).
* Schließen Sie [Zahlungs-POC aufteilen: App Builder Orchestrator-KI-Eingabeaufforderung](./orchestrator-prompt.md) zuerst ab, wenn Sie dasselbe `payment-accept` und `payment-decline` Verhalten vergleichen möchten. Die Benutzeroberflächenerweiterung verwendet diese Logik mit `COMMERCE_INTEGRATION_*` Umfeldnamen.


## Die Eingabeaufforderung

**PROMPT START**


Sie generieren die SDK-Erweiterung der `commerce-backend-ui-1` Admin-Benutzeroberfläche für den Split-Payment-PoC. Diese Erweiterung bettet ein Dashboard für aufgeteilte Zahlungsaufträge mithilfe der `@adobe/aio-app-dev-toolkit`- und `@adobe/commerce-backend-ui-1` aus dem Commerce Checkout Starter Kit in die Adobe Commerce Admin Shell ein.

**Basisprojekt:** `commerce-checkout-starter-kit/`
**Erweiterungsordner:** `commerce-checkout-starter-kit/commerce-backend-ui-1/`


### Was diese Erweiterung bietet

1. **Admin-Auftragsraster** — Ein benutzerdefiniertes Menüelement in der Commerce Admin Shell, in dem Zahlungsaufträge mit `split_cash_status = 'pending'` aufgeteilt werden
2. **Auftragsdetailansicht** - Zeigt die Aufschlüsselung der Zahlungen (Barbetrag, Kontogutschrift, Status) neben der Bestellung an
3. **Akzeptieren/Ablehnen** - Schaltflächen, die die `payment-accept` aufrufen und App Builder-Aktionen über OAuth 1.0a `payment-decline`


### Zu erzeugende Dateistruktur

```
commerce-checkout-starter-kit/commerce-backend-ui-1/
├── ext.config.yaml
├── README.md
├── .env.simulation.example
├── actions/
│   ├── utils.js
│   ├── commerce/
│   │   └── index.js           ← IMS-based Commerce REST (order listing)
│   ├── payment-accept/
│   │   ├── commerce-client.js ← OAuth 1.0a (accept/decline)
│   │   └── index.js
│   ├── payment-decline/
│   │   └── index.js
│   └── registration/
│       └── index.js
├── scripts/
│   ├── README.md
│   └── simulate-split-payment.mjs
└── web-src/
    ├── index.html
    ├── package.json
    ├── .parcelrc
    └── src/
        ├── index.jsx
        ├── index.css
        ├── utils.js
        ├── exc-runtime.js
        ├── config.json
        ├── constants/
        │   └── extension.js
        ├── components/
        │   ├── App.jsx
        │   ├── ExtensionRegistration.jsx
        │   ├── MainPage.jsx
        │   ├── SplitPaymentDashboard.jsx
        │   └── SplitPaymentOrderDetail.jsx
        └── hooks/
            └── useSplitPaymentOrders.js
```


### Backend-Aktionen

**`actions/commerce/index.js`** - IMS-authentifizierter Commerce REST
* Verwendet das vom SDK-Kontext der Admin-Benutzeroberfläche bereitgestellte IMS-Token zum Aufrufen von Commerce REST
* Abrufen der Auftragsliste mit `split_cash_status` Filter
* Gibt die Auftragsliste als JSON zurück.

**`actions/payment-accept/commerce-client.js`** - OAuth 1.0a-Client
* Gleiche Implementierung wie `split-payment-orchestrator/actions/payment-orchestrator/commerce-client.js`
* Verwendet `COMMERCE_INTEGRATION_*` Präfix env vars (um von IMS-Anmeldeinformationen zu unterscheiden)

**`actions/payment-accept/index.js`** — Aktion akzeptieren
* Gleiche Logik wie `split-payment-orchestrator/actions/payment-accept/index.js`
* Aufrufe `POST /V1/split-payment/orders/:orderId/cash-received` über OAuth 1.0a

**`actions/payment-decline/index.js`** — Aktion ablehnen
* Aufrufe `POST /V1/split-payment/orders/:orderId/cash-decline`

**`actions/registration/index.js`** - Registrierung bei der Admin-Benutzeroberfläche von SDK
* Registriert die Erweiterung in der Commerce Admin Shell
* Fügt einen Menüeintrag unter Bestellungen für das Dashboard für aufgeteilte Zahlungen hinzu


### React-Frontend-Komponenten

**`SplitPaymentDashboard.jsx`**
* Listet ausstehende aufgespaltete Zahlungsaufträge in einer Spektrum-ähnlichen Tabelle auf
* Spalten: Bestellnr. (INCREMENT_ID), Datum, Kunde, fällig, Filialguthaben, Status
* Akzeptieren und Ablehnen-Schaltflächen pro Zeile
* Ruft Backend-Aktionen über Helper zum `web-src/src/utils.js` auf
* Zeigt den Lade-/Fehlerstatus an; wird nach Abschluss der Aktion aktualisiert

**`SplitPaymentOrderDetail.jsx`**
* Zeigt aufgeteilte Zahlungsdetails für eine einzelne Bestellung an
* Zeigt: Geldbetrag, Speichergutschrift, aktueller split_cash_status

**`useSplitPaymentOrders.js`** — React Hook
* Ruft aufgeteilte Zahlungsaufträge von `actions/commerce/index.js` ab
* Gibt `{ orders, loading, error, refresh }`


### Simulationsscript

**`scripts/simulate-split-payment.mjs`**

Ein Node.js-ESM-Skript zum direkten Testen von Commerce-REST-Aufrufen (ohne App Builder zu verwenden). Verwendet dieselbe OAuth 1.0a-Signierung wie die App Builder-Aktionen.

Befehle:
* `node simulate-split-payment.mjs help` - Verwendung anzeigen
* `node simulate-split-payment.mjs list` — Auflisten aktueller Bestellungen mit aufgeteilten Zahlungsdaten
* `node simulate-split-payment.mjs show <orderId>` - Aufspaltete Zahlungsfelder für einen bestimmten Auftrag anzeigen (entity_id)
* `node simulate-split-payment.mjs accept <orderId>` - Aufruf `cash-received` Endpunkts
* `node simulate-split-payment.mjs decline <orderId>` - Aufruf `cash-decline` Endpunkts

Liest die Anmeldeinformationen von `commerce-backend-ui-1/.env.simulation` (Kopie von `.env.simulation.example`).

**`.env.simulation.example`:**

```dotenv
COMMERCE_BASE_URL=https://your-store.example.com
COMMERCE_CONSUMER_KEY=
COMMERCE_CONSUMER_SECRET=
COMMERCE_ACCESS_TOKEN=
COMMERCE_ACCESS_TOKEN_SECRET=
```


### `ext.config.yaml`

Konfigurieren Sie die Erweiterung mit:
* Der `commerce-backend-ui-1` Erweiterungstyp
* Die vier Backend-Aktionen (`commerce`, `payment-accept`, `payment-decline`, `registration`)
* `require-adobe-auth: true` für alle Aktionen außer `registration`
* Eingabebindungen aus der Umgebung für `COMMERCE_INTEGRATION_*` Anmeldedaten


### Nach dem Generieren von Dateien

```bash
cd commerce-checkout-starter-kit
npm install
cp .env.dist .env
# Fill in IMS credentials and COMMERCE_INTEGRATION_* credentials
aio app deploy
```

### Ende der Eingabeaufforderung


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
