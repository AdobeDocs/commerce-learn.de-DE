---
title: 'Aufspaltung des Zahlungs-POC: Umgebungsvariablen-Referenz'
description: Erfahren Sie, wie Sie die Einstellungen für Commerce OAuth, Basis-URL, Zahlungsschwellenwert und optionale Demos den Dateien „Orchestrator“, „Benutzeroberflächenerweiterung“ und „Simulationsumgebung“ zuordnen.
feature: App Builder, Configuration, Extensibility, Paas, REST, Security
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Tutorial
duration: 115
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 1e2c7e0e6d0f2d174b88406ce3fb7c787676ecee
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Aufspaltung des Zahlungs-POC: Umgebungsvariablen-Referenz

In jeder Komponente werden dieselben vier Commerce OAuth-Anmeldeinformationen verwendet. Erstellen Sie **[!UICONTROL Commerce Admin]** eine **[!UICONTROL Integration]** und verwenden Sie dann die vier Werte in jeder `.env` unten stehenden Datei erneut. ([&#x200B; Aktivierungsschritte finden Sie unter „Zahlungs-POC aufteilen: Voraussetzungen &#x200B;](split-payment-poc-prerequisites-and-setup.md) Umgebungseinrichtung“.)

## Die vier OAuth-Anmeldeinformationen (überall verwendet)

| Variable | Bezugsquellen |
| --- | --- |
| `COMMERCE_CONSUMER_KEY` | **[!UICONTROL Commerce Admin]** > **[!UICONTROL System]** > **[!UICONTROL Integrations]** > *[Ihre Integration]* |
| `COMMERCE_CONSUMER_SECRET` | Wie oben - Werte werden nur bei Aktivierung angezeigt |
| `COMMERCE_ACCESS_TOKEN` | Wie oben |
| `COMMERCE_ACCESS_TOKEN_SECRET` | Wie oben |


## App Builder Orchestrator

### `split-payment-orchestrator/.env`

Kopieren Sie aus `.env.example` in das Orchestrierungsverzeichnis. Diese Datei nicht übertragen.

```dotenv
# Commerce REST base URL — no trailing slash
COMMERCE_BASE_URL=https://your-store.example.com

# OAuth 1.0a integration credentials
COMMERCE_CONSUMER_KEY=
COMMERCE_CONSUMER_SECRET=
COMMERCE_ACCESS_TOKEN=
COMMERCE_ACCESS_TOKEN_SECRET=

# Must match split_payment/general/threshold in Commerce config (default: 100)
# Both Commerce and App Builder fall back to 100 if this is missing, non-numeric, or ≤ 0
PAYMENT_THRESHOLD=100

LOG_LEVEL=info

# Demo dashboard: if set, requires ?secret=<value> in URL or x-demo-secret header
# Leave empty for private staging only (anyone with the URL can list/accept orders)
DEMO_UI_SECRET=

# Optional: override the base URL used in dashboard action links (useful behind proxies)
DEMO_UI_BASE_URL=
```


## Experience Cloud-Benutzeroberflächenerweiterung (commerce-checkout-starter-kit)

### `commerce-checkout-starter-kit/.env`

Diese Komponente verwendet zwei Berechtigungssätze: IMS für die Auflistung von Bestellungen mit der SDK der **[!UICONTROL Admin]**-Benutzeroberfläche und OAuth 1.0a für Aktionen zum Akzeptieren und Ablehnen.

```dotenv
# IMS — used by CustomMenu/commerce-rest-api to list orders
# The Admin UI SDK provides the IMS token context; these set the Commerce base URL
COMMERCE_BASE_URL=https://your-store.example.com
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRETS=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_SCOPES=
OAUTH_IMS_ORG_ID=
AIO_CLI_ENV=stage

# OAuth 1.0a — same four credentials, COMMERCE_INTEGRATION_ prefix
COMMERCE_INTEGRATION_BASE_URL=https://your-store.example.com
COMMERCE_INTEGRATION_CONSUMER_KEY=
COMMERCE_INTEGRATION_CONSUMER_SECRET=
COMMERCE_INTEGRATION_ACCESS_TOKEN=
COMMERCE_INTEGRATION_ACCESS_TOKEN_SECRET=
```


## Simulationsskript

### `commerce-backend-ui-1/.env.simulation`

Kopieren Sie aus `.env.simulation.example` im selben Verzeichnis.

```dotenv
COMMERCE_BASE_URL=https://your-store.example.com
COMMERCE_CONSUMER_KEY=
COMMERCE_CONSUMER_SECRET=
COMMERCE_ACCESS_TOKEN=
COMMERCE_ACCESS_TOKEN_SECRET=
```


## Notizen

**`PAYMENT_THRESHOLD`** - Muss mit `split_payment/general/threshold` in **[!UICONTROL Commerce]** Systemkonfiguration übereinstimmen. Beide Seiten `100` standardmäßig, wenn der Wert fehlt, nicht numerisch ist oder kleiner oder gleich `0` ist. Wenn Sie den Schwellenwert in **[!UICONTROL Commerce]** ändern, aktualisieren Sie die App Builder-`.env` entsprechend.

**`DEMO_UI_SECRET`** - Optional, aber empfohlen für alle Bereitstellungen, die nicht localhost sind. Jeder Benutzer mit der Dashboard-URL kann Bestellungen auflisten und ausführen, akzeptieren und ablehnen, wenn diese leer ist. Legen Sie für eine echte Staging-Umgebung gemeinsame geheime Daten fest.

**`COMMERCE_BASE_URL`** - Geben Sie nie einen Schrägstrich am Ende an. Der Commerce REST-Client hängt `/rest/V1/` automatisch an.

**`AIO_CLI_ENV`** - Für den **[!UICONTROL Stage]**-Arbeitsbereich auf `stage` festgelegt. Ändern Sie in `prod` , wenn Sie für **[!UICONTROL Production]** bereitstellen.


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
