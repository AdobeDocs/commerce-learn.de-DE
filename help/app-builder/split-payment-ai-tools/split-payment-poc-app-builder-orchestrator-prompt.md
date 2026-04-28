---
title: 'Aufspaltung des Zahlungs-POC: App Builder Orchestrator-KI-Eingabeaufforderung'
description: 'Erfahren Sie, wie Sie mit dieser Eingabeaufforderung die Split-Payment-Orchestrator-App erstellen können: E/A-Ereignisse, Payment-Orchestrator, Web-Aktionen, Demo-Dashboard und Mobile-App-Bereitstellung.'
feature: App Builder, Configuration, Eventing, Extensibility, Paas, REST
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Tutorial
duration: 421
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: beb22335cec97141b46ddbbca97d21b216c55a80
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Aufspaltung des Zahlungs-POC: App Builder Orchestrator-KI-Eingabeaufforderung

Verwenden Sie diese Seite, um die vollständige Eingabeaufforderung zu kopieren, die das Projekt **split-payment-orchestrator** generiert: die Web-Aktionen **payment-orchestrator** I/O Event Consumer, **payment-accepted** und **payment-decreased**, **demo-dashboard** und den Commerce REST-Client.

## So verwenden Sie diese Eingabeaufforderung

Kopieren Sie alles von **PROMPT START** bis **Ende der Eingabeaufforderung** nach Cursor (mit Claude) oder direkt nach Claude. Führen Sie die Eingabeaufforderung aus dem `split-payment-orchestrator/` Verzeichnis (dem App Builder-Projektstamm) aus.

## Vor der Ausführung

* Beenden [Zahlungs-POC aufteilen: Voraussetzungen und Einrichtung der Umgebung](split-payment-poc-prerequisites-and-setup.md).
* Halten Sie [Zahlungs-POC: Umgebungsvariablen referenzieren](split-payment-poc-env-reference.md) und `.env` Datei im Projekt bereit.


## Die Eingabeaufforderung

**PROMPT START**


Sie generieren ein vollständiges Adobe App Builder-Programm zur Orchestrierung von Split-Zahlungen in Adobe Commerce. Diese Anwendung empfängt E/A-Ereignisse von Commerce, verarbeitet aufgeteilte Zahlungsentscheidungen und ruft über REST wieder zu Commerce auf.

**Projekt:** `split-payment-orchestrator`
**runtime:** Node.js 18
**Schlüsselabhängigkeiten:** `@adobe/aio-sdk ^6.0.0`, `got ^11.8.6`, `oauth-1.0a ^2.2.6`

Generieren Sie alle unten aufgeführten Dateien. Die Anwendung muss mit Adobe I/O Runtime (`aio app deploy`) funktionieren.


### Zu erzeugende Dateistruktur

```
split-payment-orchestrator/
├── package.json
├── app.config.yaml
├── .env.example
└── actions/
    ├── payment-orchestrator/
    │   ├── index.js         ← I/O Event entry point
    │   ├── commerce-client.js
    │   ├── threshold.js
    │   ├── cash-payment.js
    │   ├── order-update.js
    │   └── store-credit.js  ← Deprecated stub; kept for reference
    ├── payment-accept/
    │   └── index.js
    ├── payment-decline/
    │   └── index.js
    └── demo-dashboard/
        └── index.js
```


### `package.json`

```json
{
  "name": "split-payment-orchestrator",
  "version": "1.0.0",
  "private": true,
  "description": "Adobe App Builder action — split payment PoC orchestrator",
  "engines": { "node": ">=18" },
  "scripts": {
    "deploy": "NODE_OPTIONS=--disable-warning=DEP0040 aio app deploy",
    "aio": "NODE_OPTIONS=--disable-warning=DEP0040 aio"
  },
  "dependencies": {
    "@adobe/aio-sdk": "^6.0.0",
    "@adobe/exc-app": "^1.5.9",
    "got": "^11.8.6",
    "oauth-1.0a": "^2.2.6"
  }
}
```


### `app.config.yaml`

Definieren Sie vier Aktionen im `split_payment_orchestrator`:

**`payment-orchestrator`**
* `web: "no"` (Nur I/O Event Trigger - nicht direkt über HTTP aufrufbar)
* `runtime: nodejs:18`
* `require-adobe-auth: true`, `final: true`
* Eingaben aus der Umgebung: `LOG_LEVEL`, `COMMERCE_BASE_URL`, `COMMERCE_CONSUMER_KEY`, `COMMERCE_CONSUMER_SECRET`, `COMMERCE_ACCESS_TOKEN`, `COMMERCE_ACCESS_TOKEN_SECRET`, `PAYMENT_THRESHOLD`

**`payment-accept`**
* `web: "yes"` (HTTP-Web-Aktion - über Dashboard oder ERP aufrufbar)
* `runtime: nodejs:18`
* `require-adobe-auth: true`, `final: true`
* Gleiche Eingaben für Commerce-Anmeldeinformationen (keine `PAYMENT_THRESHOLD`)

**`payment-decline`**
* `web: "yes"`
* `runtime: nodejs:18`
* `require-adobe-auth: true`, `final: true`
* Gleiche Eingaben für Commerce-Anmeldeinformationen

**`demo-dashboard`**
* `web: "yes"`
* `runtime: nodejs:18`
* `require-adobe-auth: false` ← Dashboard ist öffentlich zugänglich (nur durch `DEMO_UI_SECRET` geschützt, falls festgelegt)
* Eingaben: alle Commerce-Anmeldeinformationen + `DEMO_UI_SECRET`, `DEMO_UI_BASE_URL`

**Ereignisregistrierung** (unter `events.registrations`):

```yaml
Split payment — sales order place before:
  description: Invokes payment-orchestrator when an order is about to be placed
  events_of_interest:
    - provider_metadata: dx_commerce_events
      event_codes:
        - com.adobe.commerce.observer.sales_order_place_before
  runtime_action: split_payment_orchestrator/payment-orchestrator
```


### `actions/payment-orchestrator/commerce-client.js`

Freigegebener OAuth 1.0a REST-Client für Adobe Commerce. Implementiert:

**`createCommerceClient(params, logger)`** — gibt `{ request, baseUrl }` zurück

* Liest `COMMERCE_BASE_URL`, `COMMERCE_CONSUMER_KEY`, `COMMERCE_CONSUMER_SECRET`, `COMMERCE_ACCESS_TOKEN`, `COMMERCE_ACCESS_TOKEN_SECRET` aus `params`
* Wird ausgelöst, wenn eine Berechtigung fehlt
* `oauth-1.0a` mit `HMAC-SHA256` (Node.js-`crypto.createHmac`)
* Verwendet `got@11` (nicht `got@12+` - das Projekt verwendet CJS) mit `prefixUrl = ${baseUrl}/rest/V1/`
* Fügt `Authorization` Kopfzeile über `beforeRequest` Hook hinzu
* `request(method, path, options)` - normalisiert den Pfad (Streifen am Anfang `/`), gibt `{ statusCode, body }` zurück
* `throwHttpErrors: false` — gibt nie 4xx/5xx aus; gibt immer den Status-Code zurück


### `actions/payment-orchestrator/threshold.js`

**`evaluateThreshold({ orderTotal, storeCreditAmount, cashAmount, params, logger })`** — gibt `{ pass: boolean, reason: string }` zurück

Logik:
1. `params.PAYMENT_THRESHOLD` lesen; als Gleitkommazahl analysieren; Standardwert ist `100`, wenn fehlt, NaN oder ≤ 0
2. Wenn `orderTotal > threshold`: `{ pass: false, reason: 'PAYMENT_THRESHOLD_EXCEEDED' }` zurückgeben
3. Wenn `Math.abs((storeCreditAmount + cashAmount) - orderTotal) > 0.02`: `{ pass: false, reason: 'SPLIT_AMOUNT_MISMATCH' }` zurückgeben
4. Andernfalls: `{ pass: true, reason: '' }` zurückgeben


### `actions/payment-orchestrator/cash-payment.js`

**`recordCashPending({ commerce, orderId, cashAmount, logger })`** — gibt `{ ok: boolean, error? }` zurück

* Aufrufe `POST orders/${orderId}/comments` mit:

  ```json
  {
    "statusHistory": {
      "comment": "Cash payment of $X.XX pending. Awaiting admin confirmation.",
      "entity_name": "order",
      "parent_id": "<orderId>",
      "is_visible_on_front": true,
      "is_customer_notified": false,
      "status": "pending_payment"
    }
  }
  ```

* Gibt `{ ok: true }` am 2xx zurück; gibt andernfalls `{ ok: false, error: { code, message } }` zurück.
* Schließt in try/catch ein; gibt ein Fehlerobjekt zurück, das nie ausgelöst wird


### `actions/payment-orchestrator/order-update.js`

**`updateOrderAfterOrchestration({ commerce, orderId, success, detail, logger })`** — gibt `{ ok: boolean, error? }` zurück

* If `success`: posts a history comment `"Split payment orchestration completed. Order awaiting cash confirmation."`
* If `!success`: posts `"Payment could not be processed. Please try again or contact support."` — never include `detail` in the customer-visible comment; log `detail` internally only
* Returns `{ ok: boolean, error? }` — never throws


### `actions/payment-orchestrator/store-credit.js`

**`applyStoreCredit({ commerce, cartId, amount, logger })`** — deprecated no-op implementation

Include this file with a JSDoc `@deprecated` notice explaining:
> The orchestrator no longer applies store credit via REST. Store credit is applied at checkout in the Commerce PHP module (`PlaceOrderPlugin`) using `BalanceManagementInterface::apply()`, which requires an active cart. By the time App Builder receives the I/O Event, the cart is inactive. This file is kept for reference or for custom flows where store credit is applied post-order.

Keep a working implementation (same shape as other modules) so developers can study the pattern, but mark it clearly as not used in the current flow.


### `actions/payment-orchestrator/index.js`

I/O Event entry point. Implements `async function main(params)`.

**Payload extraction:**

Adobe Commerce I/O Events may deliver the payload in several shapes. Extract the order value object by checking these paths in order:
1. `params.__ow_body` (parse JSON string if needed) → `.event.data.value`
2. `params.data.value`
3. `params.value`
4. `params.body.event.data.value`
5. Fall back to `params` itself

**Field extraction from value:**
* `orderId = value.entity_id || value.id`
* `orderTotal = parseFloat(value.grand_total ?? value.base_grand_total ?? value.subtotal ?? '0')`
* Split amounts from `value.extension_attributes` (check both `extension_attributes` and `extensionAttributes`):
   * `storeCredit = parseFloat(ext.split_store_credit_amount ?? value.split_store_credit_amount ?? '0')`
   * `cash = parseFloat(ext.split_cash_amount ?? value.split_cash_amount ?? '0')`

**Flow:**
1. Extract value; if `orderId` is missing, log error and return `{ statusCode: 200, body: { ok: false, message: PUBLIC_ERROR } }`
2. Call `evaluateThreshold(...)` — if fails, log and return same 200 response
3. Call `createCommerceClient(params, logger)` — if fails, return 200 error
4. If `storeCredit > 0`, log that store credit was applied at checkout (no REST call needed)
5. Call `recordCashPending(...)` — if fails, call `updateOrderAfterOrchestration(..., success: false)` and return 200 error
6. `updateOrderAfterOrchestration(..., success: true)`
7. `{ statusCode: 200, body: { ok: true, message: 'processed' } }`

**Wichtig:** Immer `statusCode: 200` zurückgeben - I/O Runtime versucht es mit Nicht-200-Antworten erneut, was zu einer doppelten Bestellverarbeitung führen würde. Fehler werden im Hauptteil gemeldet.

**`PUBLIC_ERROR`:** `"Payment could not be processed. Please try again or contact support."` - Wird für alle Fehlermeldungen verwendet, die nach außen gerichtet sind.


### `actions/payment-accept/index.js`

HTTP-Web-Aktion. Ruft `POST /V1/split-payment/orders/:orderId/cash-received` auf.

**Reihenfolge-ID-Auflösung:** Überprüfen Sie `params.orderId`, dann `params.payload.orderId`, dann `params.__ow_body` (geparste JSON). Gibt 400 zurück, wenn fehlt.

**Fluss:**
1. `orderId` auflösen; bei Fehlen 400 zurückgeben
2. Commerce-Client initialisieren; gibt 500 zurück, wenn der Vorgang fehlschlägt
3. `POST split-payment/orders/${orderId}/cash-received` mit leerem JSON-Text aufrufen
4. Wenn 2xx: `{ statusCode: 200, body: { ok: true, orderId, message: 'accepted' } }`
5. Bei Fehler: `{ statusCode: 200, body: { ok: false, message: PUBLIC_ERROR } }` protokollieren und zurückgeben


### `actions/payment-decline/index.js`

HTTP-Web-Aktion. Dasselbe Muster wie `payment-accept`, ruft aber `POST /V1/split-payment/orders/:orderId/cash-decline` auf.

Gibt bei Erfolg `{ ok: true, orderId, message: 'declined' }` zurück.


### `actions/demo-dashboard/index.js`

Eigenständiges Demo-Benutzer-Dashboard. Dient zum Erstellen eines HTML-Dashboards für die Auflistung ausstehender Bargeldbestellungen und das Auslösen von Akzeptieren/Ablehnen von Aktionen. Dies ist eine einzelne Web-Aktion, die sowohl die HTML-Benutzeroberfläche als auch eine JSON-API bereitstellt.

**Sicherheit:**
* Optionale `DEMO_UI_SECRET`: Ist diese Einstellung festgelegt, wird bei allen Anfragen `?secret=<value>` Abfrageparameter oder `x-demo-secret` Kopfzeile benötigt. Gibt 401 zurück, wenn fehlt/falsch.
* Eine Warnung protokollieren, wenn `DEMO_UI_SECRET` nicht festgelegt ist (Dashboard ist ungeschützt)

**Routing (basierend auf HTTP-Methode + Pfad/Hauptteil):**

Die Aktion empfängt alle Anfragen. Absicht ermitteln aus:
* `params.__ow_method` (GET/POST) und `params.__ow_path`- oder Aktionsparameter
* `GET` ohne Aktion → Bereitstellung des HTML-Dashboards
* `GET` mit `action=list` Parameter → JSON-Liste der ausstehenden Bestellungen zurückgeben
* `POST` mit `action=accept` und `orderId` → Aufruf `payment-accept` Logik (oder inline dem Commerce-REST-Aufruf)
* `POST` mit `action=decline` und `orderId` → Aufruf `payment-decline` Logik

**Abrufen ausstehender Bestellungen:**
* `GET orders?searchCriteria[pageSize]=50` von Commerce REST
* Filtern Sie nach Bestellungen, bei denen sich `extension_attributes.split_cash_status === 'pending'` UND-Reihenfolge nicht im Endzustand befindet (`complete`, `closed`, `canceled`, `cancelled`)
* Sortieren der neuesten Priorität im Speicher
* Bis zu 20 zurückgeben (konfigurierbar über `limit` Parameter)

**HTML-Dashboard:**
Das Dashboard ist eine mit `Content-Type: text/html` zurückgegebene HTML-Zeichenfolge. Sie sollte:
* Auflisten ausstehender Bargeldaufträge in einer Tabelle: Bestellnr. (inkrement_id), entity_id, Kundenname, Barbetrag, Speichergutschriftsbetrag, Datum
* Geben Sie **Schaltflächen** Akzeptieren“ und **Ablehnen** für jede Bestellung an, die den eigenen API-Endpunkt der Aktion aufrufen
* Erfolgs-/Fehlerantworten inline anzeigen
* Aktualisierungsschaltfläche einfügen
* So gestaltet sein, dass es verwendbar ist (minimales CSS ist ausreichend; keine externen CDN-Abhängigkeiten, um CORS-Probleme zur Laufzeit zu vermeiden)
* Warnbanner anzeigen, wenn `DEMO_UI_SECRET` nicht festgelegt ist

**Fehler in der Benutzeroberfläche:**
Wenn ein Commerce-REST-Aufruf fehlschlägt, geben Sie den HTTP-Status und eine kurze Beschreibung des Commerce-Fehlertexts an (bereinigen - entfernen Sie HTML-Tags, kürzen Sie auf 500 Zeichen). Geben Sie keine Anmeldeinformationen an.

**Antwort-Helfer:**

```javascript
function jsonResponse(statusCode, obj, extraHeaders = {}) { ... }
function htmlResponse(html) { ... }
```


### `.env.example`

```dotenv
# Commerce REST base URL — no trailing slash
COMMERCE_BASE_URL=

# OAuth 1.0a integration credentials (Admin → System → Integrations)
COMMERCE_CONSUMER_KEY=
COMMERCE_CONSUMER_SECRET=
COMMERCE_ACCESS_TOKEN=
COMMERCE_ACCESS_TOKEN_SECRET=

# PoC threshold — must match split_payment/general/threshold in Commerce (default: 100)
PAYMENT_THRESHOLD=100

LOG_LEVEL=info

# Demo dashboard optional shared secret
DEMO_UI_SECRET=
DEMO_UI_BASE_URL=
```


### Befehl bereitstellen

Nach dem Generieren aller Dateien aus dem `split-payment-orchestrator/`:

```bash
npm install
cp .env.example .env
# Edit .env with your credentials
aio app deploy
```

Notieren Sie sich nach der Bereitstellung die von `aio app deploy` ausgedruckten Aktions-URLs. Über die `demo-dashboard`-URL können Sie auf das Benutzer-Dashboard zugreifen.


### Ende der Eingabeaufforderung


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
