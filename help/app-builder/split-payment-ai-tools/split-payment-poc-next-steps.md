---
title: 'Aufspaltung des Zahlungs-POC: Nächste Schritte nach dem Konzeptnachweis'
description: 'Erfahren Sie, wie Sie den aufgeteilten Zahlungs-POC in die Produktion verschieben können: Experience Cloud-Benutzeroberfläche, ERP-Hooks, API-Mesh, PHP-Umfang, App Builder-Workflows und Checkliste für die Bereitstellung.'
feature: App Builder, API Mesh, Extensibility, Paas, REST, Eventing
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Tutorial
duration: 269
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 1e2c7e0e6d0f2d174b88406ce3fb7c787676ecee
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# Aufspaltung des Zahlungs-POC: Nächste Schritte nach dem Konzeptnachweis

Das Demo-Dashboard und das Simulationsskript, das Sie in diesem Tutorial erstellt haben, sind absichtlich grob. Sie existieren, um das Muster zu beweisen. Auf dieser Seite wird ein praktischer Weg von der Machbarkeitsstudie zur App Builder-Entwicklung im Produktionsstil beschrieben.


## Schritt 1: Ersetzen des Demo-Dashboards durch eine Experience Cloud-Benutzeroberflächenerweiterung

Die `demo-dashboard` Web-Aktion stellt HTML über eine Zeichenfolge innerhalb einer Node.js-Funktion bereit. Es funktioniert, aber es ist nicht das Produktionsmuster.

Der richtige Ersatz ist die `commerce-backend-ui-1` im `commerce-checkout-starter-kit` - eine React-App, die über die Adobe Admin UI SDK in die Commerce Admin Shell eingebettet ist. Siehe [Aufspaltung des Zahlungs-POC: Experience Cloud UI-Erweiterungs-KI](split-payment-poc-experience-cloud-ui-prompt.md)Eingabeaufforderung für die Erzeugungsaufforderung.

**Änderungen:**
* Benutzende melden sich über die Commerce Admin Shell an (IMS-Authentifizierung statt eines freigegebenen Geheimnisses)
* Die Auftragsliste verwendet den IMS-Token-Kontext - es ist kein Demo-Geheimnis erforderlich
* Akzeptieren/Ablehnen-Aktionen werden auf die IMS-Identität des Benutzers angewendet.
* Die Benutzeroberfläche ist in Commerce Admin unter der URL eingebettet, die Commerce-Administratoren bereits kennen

**Was bleibt gleich:**
* `payment-accept` und `payment-decline` App Builder-Aktionen bleiben unverändert
* Commerce-REST-Endpunkte sind unverändert
* Das PHP-Modul ist unverändert


## Schritt 2: Verbinden eines echten ERP

Der Akzeptier-/Ablehnungsfluss in diesem PoC wird durch das Klicken eines Menschen auf eine Schaltfläche gesteuert. In der Produktion wird dies durch Ihren ERP-, CRM- oder Zahlungsprozessor gesteuert.

**Das Integrationsmuster:**
1. Ihr ERP-System erfasst Bargeld und ruft `POST /payment-accept` (die App Builder Web Action URL) mit `{ orderId: <entity_id> }` auf
2. App Builder validates the call (bearer token or API key — add auth middleware to `payment-accept`)
3. App Builder calls Commerce REST `cash-received`
4. Commerce invoices and ships the order

No PHP changes required. The REST surface is already there. The App Builder action just needs a secure caller instead of a dashboard button.

**Authentication options for the ERP caller:**
* Adobe I/O Runtime supports `require-adobe-auth: true` for IMS tokens (if your ERP can get an IMS token)
* For non-Adobe systems: add a simple API key check in the `payment-accept` action (check a header against a secret stored in the action&#39;s env)


## Step 3 — Add API Mesh as a Broker Layer

Currently, App Builder calls Commerce REST directly with OAuth 1.0a credentials. For larger deployments, Adobe API Mesh provides a managed gateway layer between App Builder and Commerce.

**Benefits:**
* Centralized credential management — API Mesh holds the Commerce credentials; App Builder calls API Mesh
* Request transformation — map App Builder payloads to Commerce REST shapes without changing the App Builder action
* Rate limiting and caching — protect Commerce from high-volume event traffic

**The pattern:**
* Replace `createCommerceClient(params, logger)` calls with calls to your API Mesh endpoint
* API Mesh handles OAuth signing toward Commerce


## Step 4 — Reduce the PHP Footprint

The current PHP module handles five things that must stay in-process (see [Split payment POC: architecture and design decisions](split-payment-poc-architecture-and-decisions.md)). As Adobe Commerce&#39;s API surface matures, some of these may become movable:

**Potentially movable in the future:**
* The store credit REST API is evolving — future versions may support applying credit post-order or to inactive carts
* As more Commerce operations become async-safe, the threshold guard may be movable to a pre-order API Mesh resolver

**Not movable (architectural constraints):**
* Quote manipulation before `placeOrder()` will always require in-process code unless Commerce exposes a clean hook via an API-first extension point
* The REST endpoints (`/V1/split-payment/*`) are specific to this feature; they live in Commerce because they call Commerce-internal services


## Step 5 — Add More Workflow to App Builder

The current PoC does one thing: listen for order placement, then enable accept/decline. Natural extensions:

**Fraud scoring before accept:**
In `payment-orchestrator`, after recording cash pending, call a fraud scoring API before the orchestration result is considered final. If the score is above a threshold, auto-decline instead of waiting for operator action.

**Notification emails:**
When `payment-accept` succeeds, trigger an email (via Adobe Campaign, SendGrid, or any HTTPS API) notifying the customer that their cash payment was confirmed.

**Loyalty point awards:**
After cash is confirmed, call a loyalty API to award points. This is pure App Builder — no PHP required.

**Timeout handling:**
Add a scheduled App Builder action (using `cron` in `app.config.yaml`) that scans for orders with `split_cash_status = 'pending'` older than X days and auto-declines them.


## Step 6 — Deploy to Production

The PoC is configured for `Stage` workspace. Moving to production:

```bash
# Switch to production workspace
aio app use
# Select Production workspace

# Update .env for production
# (same credentials, but production Commerce base URL)

# Deploy
aio app deploy
```

**Checklist for production readiness:**
* [ ] `DEMO_UI_SECRET` set (or demo dashboard replaced with Experience Cloud UI)
* [ ] `LOG_LEVEL=warn` or `error` in production (not `debug`)
* [ ] `PAYMENT_THRESHOLD` matches Commerce production config
* [ ] Commerce Integration credentials in `.env` are for a dedicated production integration (not staging)
* [ ] Fastly IP allowlist updated with App Builder production egress IPs (Commerce Cloud)
* [ ] E/A-Ereignisregistrierung in Produktionsarbeitsbereich bestätigt


## Architekturübersicht

```
PoC (this tutorial)
┌─────────────────────────────────────────────────┐
│  Commerce                 App Builder            │
│  ┌─────────────┐         ┌──────────────────┐   │
│  │  PHP Module │◄────────│ payment-orchestr │   │
│  │  REST API   │────────►│ payment-accept   │   │
│  │  Checkout UI│         │ payment-decline  │   │
│  └─────────────┘         │ demo-dashboard   │   │
└─────────────────────────────────────────────────┘

Phase 2: Experience Cloud UI
┌─────────────────────────────────────────────────┐
│  Commerce                 App Builder            │
│  ┌─────────────┐         ┌──────────────────┐   │
│  │  PHP Module │◄────────│ payment-orchestr │   │
│  │  REST API   │────────►│ payment-accept   │   │
│  │  Checkout UI│         │ payment-decline  │   │
│  │             │         │ Admin UI ext.    │   │
│  └─────────────┘         └──────────────────┘   │
└─────────────────────────────────────────────────┘

Phase 3: Real ERP + API Mesh
┌──────────────────────────────────────────────────────────┐
│  ERP  ──►  App Builder  ──►  API Mesh  ──►  Commerce     │
│            (orchestrator)   (gateway)    (PHP module      │
│            (accept)                      REST surface)    │
└──────────────────────────────────────────────────────────┘
```


## Wichtige Referenzen

* [Dokumentation zu Adobe App Builder](https://developer.adobe.com/app-builder/docs/overview/){target="_blank"}
* [Adobe I/O Events für Commerce](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"}
* [Commerce Checkout-Starterkit](https://github.com/adobe/commerce-checkout-starter-kit){target="_blank"}
* [Adobe Admin-Benutzeroberfläche SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}
* [Adobe-API-Mesh](https://developer.adobe.com/graphql-mesh-gateway/){target="_blank"}
* [Adobe I/O Runtime (OpenWhisk)](https://developer.adobe.com/runtime/docs/){target="_blank"}



{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
