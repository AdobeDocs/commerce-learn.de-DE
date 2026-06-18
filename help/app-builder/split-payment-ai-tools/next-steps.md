---
title: Aufspaltung des Zahlungs-POC - nächste Schritte nach dem Machbarkeitsnachweis
description: Erfahren Sie, wie Sie den POC für aufgeteilte Zahlungen in die Produktion verschieben können. Experience Cloud-Benutzeroberfläche, ERP-Hooks, API-Mesh, PHP-Umfang, App Builder-Workflows und Bereitstellungs-Checkliste.
feature: App Builder, API Mesh, Extensibility, Paas, REST, Eventing
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, User
level: Intermediate
doc-type: Tutorial
duration: 269
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 63ac13d8c5a97ee81dcdd1f3785a9875aaf2a4db
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# Aufspaltung des Zahlungs-POC: Nächste Schritte nach dem Konzeptnachweis

Das Demo-Dashboard und das Simulationsskript, das Sie in diesem Tutorial erstellt haben, sind absichtlich grob. Sie existieren, um das Muster zu beweisen. Auf dieser Seite wird ein praktischer Weg von der Machbarkeitsstudie zur App Builder-Entwicklung im Produktionsstil beschrieben.


## Schritt 1: Ersetzen des Demo-Dashboards durch eine Experience Cloud-UI-Erweiterung

Die `demo-dashboard` Web-Aktion stellt HTML über eine Zeichenfolge innerhalb einer Node.js-Funktion bereit. Es funktioniert, aber es ist nicht das Produktionsmuster.

Der richtige Ersatz ist die `commerce-backend-ui-1` im `commerce-checkout-starter-kit` - eine React-App, die über die Adobe Admin UI SDK in die Commerce Admin Shell eingebettet ist. Siehe [Aufspaltung des Zahlungs-POC: Eingabeaufforderung zur Erweiterung der Experience Cloud](./experience-cloud-ui-prompt.md)Benutzeroberfläche für die Eingabeaufforderung zur Generierung.

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
2. App Builder validiert den Aufruf (Bearer-Token oder API-Schlüssel — Authentifizierungs-Middleware zu `payment-accept` hinzufügen)
3. App Builder ruft Commerce REST-`cash-received` auf
4. Commerce stellt Rechnungen aus und versendet die Bestellung

Keine PHP-Änderungen erforderlich. Die REST-Oberfläche ist bereits vorhanden. Für die App Builder-Aktion ist nur ein sicherer Aufrufer anstelle einer Dashboard-Schaltfläche erforderlich.

**Authentifizierungsoptionen für ERP-Aufrufer:**
* Adobe I/O Runtime unterstützt `require-adobe-auth: true` für IMS-Token (wenn Ihr ERP ein IMS-Token erhalten kann)
* Für Nicht-Adobe-Systeme: Fügen Sie eine einfache API-Schlüsselprüfung in der `payment-accept` hinzu (überprüfen Sie eine Kopfzeile mit einem Geheimnis, das in der Umgebung der Aktion gespeichert ist)


## Schritt 3 - API-Mesh als Broker-Ebene hinzufügen

Derzeit ruft App Builder Commerce REST direkt mit OAuth 1.0a-Anmeldeinformationen auf. Für größere Bereitstellungen bietet Adobe API Mesh eine verwaltete Gateway-Ebene zwischen App Builder und Commerce.

**Vorteile:**
* Zentralisierte Berechtigungsverwaltung - API Mesh speichert die Commerce-Anmeldeinformationen; App Builder ruft API Mesh auf
* Anforderungstransformation - Ordnen Sie App Builder-Payloads Commerce-REST-Shapes zu, ohne die App Builder-Aktion zu ändern
* Ratenbegrenzung und Caching - Schützen Sie Commerce vor Ereignisdatenverkehr mit hohem Volumen

**Das Muster:**
* Ersetzen `createCommerceClient(params, logger)` Aufrufe durch Aufrufe an Ihren API-Mesh-Endpunkt
* API-Mesh handhabt das OAuth-Signieren für Commerce


## Schritt 4: Reduzierung des PHP-Platzbedarfs

Das aktuelle PHP-Modul behandelt fünf Dinge, die im Prozess bleiben müssen (siehe [Split Payment POC: Architektur- und Design-Entscheidungen](./architecture-and-decisions.md)). Mit zunehmender Reife der API-Oberfläche von Adobe Commerce können einige dieser Funktionen verschoben werden:

**In Zukunft potenziell beweglich:**
* Die Store-Credit-REST-API entwickelt sich weiter - zukünftige Versionen können die Anwendung von Guthaben nach der Bestellung oder auf inaktive Warenkörbe unterstützen
* Da immer mehr Commerce-Vorgänge asynchron sind, kann der Schwellenwert-Guard auf einen vorkonfigurierten API-Mesh-Resolver verschoben werden

**Nicht beweglich (architektonische Einschränkungen):**
* Die Zitatbearbeitung vor dem `placeOrder()` erfordert immer prozessinternen Code, es sei denn, Commerce stellt über einen API-First-Erweiterungspunkt einen fehlerfreien Hook zur Verfügung
* Die REST-Endpunkte (`/V1/split-payment/*`) sind für diese Funktion spezifisch. Sie befinden sich in Commerce, weil sie Commerce-interne Services aufrufen


## Schritt 5: Hinzufügen eines weiteren Workflows zu App Builder

Der aktuelle PoC tut eine Sache: die Auftragserteilung überwachen und dann Akzeptieren/Ablehnen aktivieren. Natürliche Erweiterungen:

**Betrugs-Scoring vor der Annahme:**
Rufen Sie in `payment-orchestrator` nach der Aufzeichnung ausstehender Barmittel eine Betrugs-Scoring-API auf, bevor das Orchestrierungsergebnis als endgültig betrachtet wird. Wenn der Score über einem Schwellenwert liegt, wird automatisch abgelehnt, anstatt auf eine Benutzeraktion zu warten.

**Benachrichtigungs-E-Mails:**
Wenn `payment-accept` erfolgreich ist, senden Sie eine E-Mail (über Adobe Campaign, SendGrid oder eine beliebige HTTPS-API), die den Kunden darüber informiert, dass seine Barzahlung bestätigt wurde.

**Treuepunktpreise:**
Nachdem die Barzahlung bestätigt wurde, rufen Sie eine Treue-API auf, um Punkte zu vergeben. Dies ist reine App Builder - kein PHP erforderlich.

**Verarbeitung der Zeitüberschreitung:**
Fügen Sie eine geplante App Builder-Aktion (unter Verwendung von `cron` in `app.config.yaml`) hinzu, die Bestellungen mit `split_cash_status = 'pending'` älter als X Tage sucht und automatisch ablehnt.


## Schritt 6: Bereitstellung für Produktion

Der POC ist für `Stage` Arbeitsbereich konfiguriert. Wechseln zur Produktion:

```bash
# Switch to production workspace
aio app use
# Select Production workspace

# Update .env for production
# (same credentials, but production Commerce base URL)

# Deploy
aio app deploy
```

**Checkliste für die Produktionsbereitschaft:**
* [ ] `DEMO_UI_SECRET` festgelegt (oder das Demo-Dashboard durch die Experience Cloud-Benutzeroberfläche ersetzt)
* [ ] `LOG_LEVEL=warn` oder `error` in Produktion (nicht `debug`)
* [ ] `PAYMENT_THRESHOLD` entspricht der Commerce-Produktionskonfiguration
* [ ] Anmeldedaten für die Commerce-Integration in `.env` für eine dedizierte Produktionsintegration (nicht für Staging)
* [ ] Fastly IP-Zulassungsliste mit App Builder Production Egress-IPs (Commerce Cloud) aktualisiert
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
