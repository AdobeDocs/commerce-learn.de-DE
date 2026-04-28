---
title: 'Aufspaltung des Zahlungs-POC: Tutorial-Kurzanleitung'
description: 'Erfahren Sie mehr über die aufgeteilte POC-Dateizuordnung für Zahlungen: Welche Experience League-Seite entspricht jeder KI-Eingabeaufforderung, empfohlener Abschnittsreihenfolge und Autorennotizen für den Luma-Checkout?'
feature: App Builder, Extensibility, Paas, REST, Eventing
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Tutorial
duration: 398
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 1e2c7e0e6d0f2d174b88406ce3fb7c787676ecee
workflow-type: tm+mt
source-wordcount: '1455'
ht-degree: 0%

---

# Aufspaltung des Zahlungs-POC: Tutorial-Kurzanleitung

Auf dieser Seite wird zusammengefasst, wie die Tutorial-Reihe zum Machbarkeitsnachweis für die Aufspaltung von Zahlungen organisiert ist. Es ordnet jede nummerierte Quellaufforderungsdatei ihrer veröffentlichten Experience League-Seite zu, listet eine vorgeschlagene Abschnittsreihenfolge für Leser auf und sammelt Notizen für Autoren und Betreuer.


## Datei-für-Datei-Verweis

### [Erstellen eines aufgeteilten Zahlungs-POC: App Builder- und KI-Tools](create-a-split-payment-poc-app-builder-and-ai-tools.md)

**Source-Bezeichnung:** `00_TUTORIAL_OVERVIEW.md` (Konzeptübersicht; die veröffentlichte Serie wird mit dieser Seite geöffnet.)

**Zweck:** Einführung und Ausrichtung für das Tutorial.

**Warum es benötigt wird:** Gibt Entwicklern das „Warum“ vor dem „Wie“. Erläutert, was sie erstellen werden, wer die Zielgruppe ist und was sie, wenn sich ihre Site von einer sauberen Luma-Installation unterscheidet, anpassen müssen. Dient auch als Inhaltsverzeichnis für den Rest der Serie.

**Tutorial-Nutzung:** Abschnitt wird geöffnet. Legt den Kontext vor allen technischen Schritten fest.


### [Aufspaltung des Zahlungs-POC: Architektur- und Design-Entscheidungen](split-payment-poc-architecture-and-decisions.md)


**Zweck** Detaillierte Erläuterung jeder architektonischen Entscheidung im PoC.

**Warum das nötig ist:** Der häufigste Punkt der Verwirrung bei der Arbeit mit diesem PoC ist das Verständnis *warum* etwas in PHP versus App Builder. Ohne diesen Kontext versuchen Entwickler, Dinge zu verschieben, die nicht verschoben werden können (wie z. B. einen Kreditantrag) und scheitern. In diesem Dokument werden diese Fehler mit einer klaren Begründung vermieden.

**Wichtige behandelte Themen:**

* Die Regel „Was muss in PHP bleiben?“ und warum
* Das Muster der doppelten Durchsetzung von Schwellenwerten
* Warum der Kreditantrag nicht asynchron gespeichert werden kann
* Die fünf Commerce-Edge-Fälle, die von Plug-ins verarbeitet werden
* Der Datenfluss des Erweiterungsattributs von Checkout → Angebot → Bestellung → I/O Event → App Builder

**Tutorial use:** &quot;Architecture&quot; or &quot;How it works&quot; section. Can be skipped by experienced Commerce developers but is essential for App Builder newcomers.


### [Split payment POC: prerequisites and environment setup](split-payment-poc-prerequisites-and-setup.md)


**Purpose:** Complete pre-flight checklist before any code is written or prompts are run.

**Why it&#39;s needed:** The setup phase has the highest failure rate in tutorials. This document ensures Commerce Admin is configured correctly (exact COD title, store credit enabled, test customer has balance, integration created), the App Builder project has I/O Events and the Commerce event provider connected, and the local environment has the right versions.

**Emphasis items:**

* Cash on delivery title must be exactly `Cash` (critical — the JavaScript does string matching)
* Commerce integration must be *activated* (not just saved) for the OAuth credentials to work
* `entity_id` versus `increment_id` explained here to prevent confusion throughout

**Tutorial use:** &quot;Prerequisites&quot; or &quot;Getting started&quot; section. Should be completed interactively — not just read.


### [Split payment POC: environment variables reference](split-payment-poc-env-reference.md)


**Purpose:** All environment variables for all three components in one place.

**Why it&#39;s needed:** The same four OAuth credentials appear in three different files with different variable names (`COMMERCE_*` versus `COMMERCE_INTEGRATION_*`). Having a single reference prevents the &quot;why isn&#39;t this working&quot; debugging where one credential set has a typo.

**Components covered:**

* `split-payment-orchestrator/.env`
* `commerce-checkout-starter-kit/.env` (IMS + OAuth)
* `commerce-backend-ui-1/.env.simulation`

**Tutorial use:** Reference sidebar or &quot;Configuration&quot; section. Also used as a companion to the build prompts.


### [Split payment POC: Commerce module AI prompt](split-payment-poc-commerce-module-prompt.md)


**Purpose:** Complete, self-contained AI prompt to generate the entire `Client_SplitPayment` PHP module.

**Why it&#39;s needed:** This is the primary AI build artifact for the PHP side. It is written so that a developer with no PHP experience can hand it to Cursor (with Claude) and get a working module. Every file is specified, every behavioral contract is defined, critical implementation notes are included, and the commands to enable the module afterward are provided.

**Abdeckung:**

* Vollständige Dateistruktur (mehr als 30 Dateien)
* Datenbankschema, Erweiterungsattribute, REST-Endpunkte, E/A-Ereigniskonfiguration
* Alle PHP-Klassen mit vollständigen Verhaltensspezifikationen (nicht nur Signaturen)
* KnockoutJS-Checkout-Komponentenspezifikationen
* Die fünf Edge-Gehäuse-Plug-ins mit Erklärungen, warum jedes vorhanden ist
* Anpassungsbeschriftungen für Nicht-Luma-Designs

**Tutorial-Verwendung** Abschnitt „Erstellen des Commerce-Moduls“. Die Eingabeaufforderung selbst ist ein Artefakt - Entwickler kopieren sie in ihr KI-Tool und führen es aus.


### [Zahlungs-POC aufteilen: App Builder Orchestrator-KI-Eingabeaufforderung](split-payment-poc-app-builder-orchestrator-prompt.md)


**Zweck:** Vollständige, in sich abgeschlossene KI-Eingabeaufforderung zum Generieren der `split-payment-orchestrator` App Builder-Anwendung.

**Warum es benötigt wird:** Die vier App Builder-Aktionen (`payment-orchestrator`, `payment-accept`, `payment-decline`, `demo-dashboard`) sind der Kern der „Was aus PHP herauskam“-Story. Diese Eingabeaufforderung generiert alle mit vollständigen Verhaltensspezifikationen, einer korrekten `app.config.yaml` und der Konfiguration der Ereignisregistrierung.

**Abdeckung:**

* `app.config.yaml` mit allen vier Aktionen und der E/A-Ereignisregistrierung
* Freigegebener Client für OAuth 1.0a `commerce-client.js`
* Alle vier Aktionen mit vollständigen logischen Spezifikationen
* Der `store-credit.js` veraltete Stub (mit Erläuterung *warum* wird nicht verwendet - dies ist pädagogisch wichtig)
* Das Demo-Dashboard mit HTML-Rendering, Bestellfilterung und Sicherheit
* Mit allen Variablen `.env.example`

**Tutorial-Verwendung** Abschnitt „Erstellen des App Builder-Programms“. Begleiter der Commerce-Modulaufforderung.


### [Zahlungs-POC aufteilen: Experience Cloud UI-Erweiterung - KI-Eingabeaufforderung](split-payment-poc-experience-cloud-ui-prompt.md)


**Zweck:** KI-Aufforderung, die optionale SDK-Erweiterung für die Experience Cloud Admin-Benutzeroberfläche zu generieren.

**Warum dies erforderlich ist:** Das Demo-Dashboard in der Orchestrierungs-Eingabeaufforderung ist absichtlich grob - es ist ein Machbarkeitsnachweis, keine Produktion. This section shows developers the next step: embedding the split payment dashboard into the Commerce Admin Shell using the Admin UI SDK. It was missing entirely from the original prompts.

**Abdeckung:**

* `ext.config.yaml` for the Admin UI SDK extension
* React components for the order dashboard and order detail
* Backend actions using IMS auth for listing and OAuth for accept/decline
* The simulation script (also used for testing)

**Tutorial use:** Optional &quot;Going further&quot; or &quot;Production path&quot; section. Can be skipped if the tutorial focuses only on the PoC.


### [Split payment POC: testing and verification guide](split-payment-poc-testing-and-verification.md)


**Purpose:** Step-by-step testing guide covering every component in the correct verification order.

**Why it&#39;s needed:** Building the components is half the work. Developers need a clear verification path that starts from the lowest level (database columns, REST endpoints) and builds to the full end-to-end flow. The original prompts had a setup checklist but no explicit testing flow.

**Abdeckung:**

* Commerce module installation verification
* Admin configuration verification
* REST endpoint smoke tests (curl commands)
* Checkout UI walkthrough (including validation cases)
* Threshold guard test
* Full order placement test
* Simulation script usage for accept and decline
* Demo dashboard usage
* App Builder action log inspection
* Ten common failure modes with specific fixes

**Tutorial use:** &quot;Testing&quot; or &quot;Verification&quot; section. Also valuable as a troubleshooting reference.


### [Split payment POC: next steps after the proof of concept](split-payment-poc-next-steps.md)


**Purpose:** Roadmap for evolving the PoC into production-ready patterns.

**Why it&#39;s needed:** A PoC tutorial risks leaving developers with a &quot;what now?&quot; feeling. This document maps the natural progressions from demo to production: replacing the demo dashboard with an Experience Cloud extension, connecting a real ERP, adding API Mesh, expanding App Builder workflow, and production deployment checklist.

**Key content:**

* Architecture evolution diagram (PoC → Phase 2 → Phase 3)
* ERP integration pattern (what changes, what stays the same)
* API Mesh broker pattern
* Production deployment checklist
* Key reference links

**Tutorial use:** &quot;Next steps&quot; closing section. Also useful as a conversation starter for scoping a real project.


## Suggested tutorial sections

Based on these files, a typical structure for readers is:

| Tutorial section | Experience League page |
| --- | --- |
| Introduction and learning objectives | [Erstellen eines aufgeteilten Zahlungs-POC: App Builder- und KI-Tools](create-a-split-payment-poc-app-builder-and-ai-tools.md) |
| End-to-end demo (video) | [Create a split payment POC: App Builder full demo](create-a-split-payment-poc-app-builder-and-ai-tools-full-demo.md) |
| Architecture: what lives where | [Aufspaltung des Zahlungs-POC: Architektur- und Design-Entscheidungen](split-payment-poc-architecture-and-decisions.md) |
| Voraussetzungen und Einrichtung | [Aufspaltung des Zahlungs-POC: Voraussetzungen und Einrichtung der Umgebung](split-payment-poc-prerequisites-and-setup.md) |
| Umgebungsvariablen | [Aufspaltung des Zahlungs-POC: Umgebungsvariablen-Referenz](split-payment-poc-env-reference.md) |
| Schritt 1: Commerce-Modul erstellen | [Zahlungs-POC aufteilen: Commerce-Modul-KI-Eingabeaufforderung](split-payment-poc-commerce-module-prompt.md) |
| Schritt 2: App Builder Orchestrator erstellen | [Zahlungs-POC aufteilen: App Builder Orchestrator-KI-Eingabeaufforderung](split-payment-poc-app-builder-orchestrator-prompt.md) |
| Schritt 3: Testen des End-to-End-Flusses | [Aufspaltung des Zahlungs-POC: Test- und Verifizierungshandbuch](split-payment-poc-testing-and-verification.md) |
| Schritt 4 (optional): Erweiterung der Admin-Benutzeroberfläche | [Zahlungs-POC aufteilen: Experience Cloud UI-Erweiterung - KI-Eingabeaufforderung](split-payment-poc-experience-cloud-ui-prompt.md) |
| Nächste Schritte und Produktionspfad | [Aufspaltung des Zahlungs-POC: Nächste Schritte nach dem Machbarkeitsnachweis](split-payment-poc-next-steps.md) |


## Wichtige Hinweise für Autoren von Tutorials

**Bei der Annahme des Luma-Designs:** Jede Build-Eingabeaufforderung generiert Code für eine saubere Luma-Installation. Im Tutorial sollte dies ganz oben klar angegeben werden. Entwicklerinnen und Entwickler mit benutzerdefinierten Checkouts müssen die `LayoutProcessorPlugin`-Injections-Pfade und möglicherweise die RequireJS-Konfiguration anpassen. Die Eingabeaufforderungen zur Serieneinführung und zum Build enthalten Hinweise zur Anpassung.

**Zum PHP-Modul:** Das Tutorial stellt den PHP-Code nicht explizit als Copy-Paste-Download bereit. Die KI-Eingabeaufforderung *generiert* sie. Dies ist beabsichtigt - es lehrt das Muster der Verwendung von KI zum Erstellen von Commerce-Erweiterungen, nicht nur das Kopieren und Einfügen von Textbausteinen. Der generierte Code sollte jedoch, wenn er in einer sauberen Umgebung aufgefordert wird, genau mit dem funktionierenden Code in `app/code/Client/SplitPayment/` übereinstimmen.

**Zum Schwellenwert von 100 $:** Dies ist ein hartcodierter PoC-Wert. Das Tutorial sollte beachten, dass Real Stores dies über die Commerce-Admin-Konfiguration und nicht über eine Kompilierungszeitkonstante konfigurieren sollten.

**Abhängigkeit bei Filialguthaben:** Der aufgeteilte Zahlungsfluss erfordert `Magento_CustomerBalance` (das native Filialguthaben-Modul).


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
