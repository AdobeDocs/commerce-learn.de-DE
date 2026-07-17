---
title: Aufspaltung des Zahlungs-POC — Tutorial-Schnellübersicht
description: Erfahren Sie mehr über die aufgeteilte POC-Dateizuordnung für Zahlungen. Welche Experience League-Seite für jede KI-Eingabeaufforderung, vorgeschlagene Abschnittsreihenfolge und Autorenhinweise für den Luma-Checkout geeignet ist.
feature: App Builder, Extensibility, Paas, REST, Eventing
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, User
level: Intermediate
doc-type: Tutorial
duration: 398
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: a9472912c20d157e310abfece16519156b10945f
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 0%

---

# Aufspaltung des Zahlungs-POC: Tutorial-Kurzanleitung

Auf dieser Seite wird zusammengefasst, wie die Tutorial-Reihe zum Machbarkeitsnachweis für die Aufspaltung von Zahlungen organisiert ist. Es ordnet jede nummerierte Quellaufforderungsdatei ihrer veröffentlichten Experience League-Seite zu, listet eine vorgeschlagene Abschnittsreihenfolge für Leser auf und sammelt Notizen für Autoren und Betreuer.


## Datei-für-Datei-Verweis

### Erstellen eines aufgeteilten Zahlungs-POC: App Builder- und KI-Tools

[Erstellen eines aufgeteilten Zahlungs-POC: App Builder- und KI-Tools](./overview.md)

**Zweck:** Einführung und Ausrichtung für das Tutorial.

**Warum es benötigt wird:** Gibt Entwicklern das „Warum“ vor dem „Wie“. Erläutert, was sie erstellen werden, wer die Zielgruppe ist und was sie, wenn sich ihre Site von einer sauberen Luma-Installation unterscheidet, anpassen müssen. Dient auch als Inhaltsverzeichnis für den Rest der Serie.

**Tutorial-Nutzung:** Abschnitt wird geöffnet. Legt den Kontext vor allen technischen Schritten fest.


### Aufspaltung des Zahlungs-POC: Architektur- und Design-Entscheidungen

[Aufspaltung des Zahlungs-POC: Architektur- und Design-Entscheidungen](./architecture-and-decisions.md)

**Zweck** Detaillierte Erläuterung jeder architektonischen Entscheidung im PoC.

**Warum das nötig ist:** Der häufigste Punkt der Verwirrung bei der Arbeit mit diesem PoC ist das Verständnis *warum* etwas in PHP versus App Builder. Ohne diesen Kontext versuchen Entwickler, Dinge zu verschieben, die nicht verschoben werden können (wie z. B. einen Kreditantrag) und scheitern. In diesem Dokument werden diese Fehler mit einer klaren Begründung vermieden.

**Wichtige behandelte Themen:**

* Die Regel „Was muss in PHP bleiben?“ und warum
* Das Muster der doppelten Durchsetzung von Schwellenwerten
* Warum der Kreditantrag nicht asynchron gespeichert werden kann
* Die fünf Commerce-Edge-Fälle, die von Plug-ins verarbeitet werden
* Der Datenfluss des Erweiterungsattributs von Checkout → Angebot → Bestellung → I/O Event → App Builder

**Tutorial-Nutzung** Abschnitt „Architektur“ oder „Funktionsweise“. Kann von erfahrenen Commerce-Entwicklerinnen und -Entwicklern übersprungen werden, ist aber für App Builder-Neulinge unverzichtbar.


### Aufspaltung des Zahlungs-POC: Voraussetzungen und Einrichtung der Umgebung

[Aufspaltung des Zahlungs-POC: Voraussetzungen und Einrichtung der Umgebung](./prerequisites-and-setup.md)

**Zweck:** Vervollständigen Sie die Checkliste vor dem Flug, bevor Code geschrieben oder Eingabeaufforderungen ausgeführt werden.

**Warum dies erforderlich ist:** Die Einrichtungsphase weist in den Tutorials die höchste Fehlerrate auf. Dieses Dokument stellt sicher, dass Commerce Admin korrekt konfiguriert ist (exakter CODE-Titel, Store-Guthaben aktiviert, Kundensaldo getestet, Integration erstellt), das App Builder-Projekt über I/O-Ereignisse verfügt und der Commerce-Ereignisanbieter angeschlossen ist und die lokale Umgebung über die richtigen Versionen verfügt.

**Elemente hervorheben:**

* Der Cash-on-Delivery-Titel muss exakt `Cash` sein (wichtig - der JavaScript verwendet Zeichenfolgenabgleich)
* Die Commerce-Integration muss *aktiviert* (nicht nur gespeichert) sein, damit die OAuth-Anmeldeinformationen funktionieren
* `entity_id` versus `increment_id` hier erläutert, um Verwirrung während des gesamten

**Tutorial-Verwendung** Abschnitt „Voraussetzungen“ oder „Erste Schritte“. Sollte interaktiv abgeschlossen werden - nicht nur gelesen.


### Aufspaltung des Zahlungs-POC: Umgebungsvariablen-Referenz

[Aufspaltung des Zahlungs-POC: Umgebungsvariablen-Referenz](./env-reference.md)

**Zweck** Alle Umgebungsvariablen für alle drei Komponenten an einem Ort.

**Warum dies erforderlich ist** Dieselben vier OAuth-Anmeldeinformationen werden in drei verschiedenen Dateien mit unterschiedlichen Variablennamen angezeigt (`COMMERCE_*` im Vergleich zu `COMMERCE_INTEGRATION_*`). Eine einzelne Referenz verhindert das Debugging von „Warum funktioniert das nicht?“, wenn ein Berechtigungssatz einen Tippfehler enthält.

**Betroffene Komponenten:**

* `split-payment-orchestrator/.env`
* `commerce-checkout-starter-kit/.env` (IMS + OAuth)
* `commerce-backend-ui-1/.env.simulation`

**Tutorial-Verwendung** Verweis-Seitenleiste oder Abschnitt „Konfiguration“. Wird auch als Ergänzung zu den Build-Eingabeaufforderungen verwendet.


### Aufspaltung des Zahlungs-POC: Commerce-Modul-KI-Eingabeaufforderung

[Aufspaltung des Zahlungs-POC: Commerce-Modul-KI-Eingabeaufforderung](./commerce-module-prompt.md)

**Zweck:** Vollständige, eigenständige AI-Eingabeaufforderung, um das gesamte `Client_SplitPayment` PHP-Modul zu generieren.

**Warum es benötigt wird:** Dies ist das primäre AI-Build-Artefakt für die PHP-Seite. Es ist so geschrieben, dass ein Entwickler ohne PHP-Erfahrung es an Cursor (mit Claude) übergeben kann und ein funktionierendes Modul erhält. Jede Datei wird angegeben, jeder Verhaltensvertrag wird definiert, wichtige Implementierungshinweise sind enthalten und die Befehle zum Aktivieren des Moduls werden anschließend bereitgestellt.

**Abdeckung:**

* Vollständige Dateistruktur (mehr als 30 Dateien)
* Datenbankschema, Erweiterungsattribute, REST-Endpunkte, E/A-Ereigniskonfiguration
* Alle PHP-Klassen mit vollständigen Verhaltensspezifikationen (nicht nur Signaturen)
* KnockoutJS-Checkout-Komponentenspezifikationen
* Die fünf Edge-Gehäuse-Plug-ins mit Erklärungen, warum jedes vorhanden ist
* Anpassungsbeschriftungen für Nicht-Luma-Designs

**Tutorial-Verwendung** Abschnitt „Erstellen des Commerce-Moduls“. Die Eingabeaufforderung selbst ist ein Artefakt - Entwickler kopieren sie in ihr KI-Tool und führen es aus.


### Aufspaltung des Zahlungs-POC: App Builder Orchestrator-KI-Eingabeaufforderung

[Aufspaltung des Zahlungs-POC: App Builder Orchestrator-KI-Eingabeaufforderung](./orchestrator-prompt.md)

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


### Aufspaltung des Zahlungs-POC: API-Eingabeaufforderung für Experience Cloud-UI-Erweiterung

[Aufspaltung des Zahlungs-POC: API-Eingabeaufforderung für Experience Cloud-UI-Erweiterung](./experience-cloud-ui-prompt.md)

**Zweck:** KI-Aufforderung, die optionale SDK-Erweiterung für die Experience Cloud Admin-Benutzeroberfläche zu generieren.

**Warum dies erforderlich ist:** Das Demo-Dashboard in der Orchestrierungs-Eingabeaufforderung ist absichtlich grob - es ist ein Machbarkeitsnachweis, keine Produktion. In diesem Abschnitt wird der nächste Schritt für Entwickler gezeigt: Einbetten des Dashboards für die Aufspaltung von Zahlungen in die Commerce Admin Shell mithilfe der Admin-Benutzeroberfläche von SDK. Es fehlte völlig in den ursprünglichen Eingabeaufforderungen.

**Abdeckung:**

* `ext.config.yaml` für die SDK-Erweiterung der Admin-Benutzeroberfläche
* React-Komponenten für das Bestell-Dashboard und die Bestelldetails
* Backend-Aktionen, die die IMS-Authentifizierung für die Auflistung und OAuth für das Akzeptieren/Ablehnen verwenden
* Das Simulationsskript (wird auch für Tests verwendet)

**Tutorial-Verwendung** Optionaler Abschnitt „Weiter gehen“ oder „Produktionspfad“. Kann übersprungen werden, wenn sich das Tutorial nur auf den PoC konzentriert.


### Split Payment POC: Test- und Verifizierungshandbuch

[Split Payment POC: Test- und Verifizierungshandbuch](./testing-and-verification.md)

**Zweck** Eine schrittweise Anleitung zum Testen aller Komponenten in der richtigen Überprüfungsreihenfolge.

**Warum das nötig ist** Die Komponenten zu bauen ist die halbe Arbeit. Entwickler benötigen einen klaren Verifizierungspfad, der von der niedrigsten Ebene (Datenbankspalten, REST-Endpunkte) beginnt und Builds zum vollständigen End-to-End-Fluss umfasst. Die ursprünglichen Eingabeaufforderungen enthielten eine Setup-Checkliste, aber keinen expliziten Testfluss.

**Abdeckung:**

* Commerce-Modulinstallationsüberprüfung
* Administrator-Konfigurationsüberprüfung
* REST-Endpunkt-Feuerprobe (curl-Befehle)
* Anleitung zur Checkout-Benutzeroberfläche (einschließlich Validierungsfällen)
* Schwellenwertprüfung
* Vollständiger Bestell-Platzierungstest
* Verwendung des Simulationsskripts zum Akzeptieren und Ablehnen
* Verwendung des Demo-Dashboards
* Prüfung des App Builder-Aktionsprotokolls
* Zehn gängige Fehlermodi mit spezifischen Fehlerbehebungen

**Tutorial-Verwendung** Abschnitt „Testen“ oder „Verifizierung“. Auch als Referenz zur Fehlerbehebung nützlich.


### Aufspaltung des Zahlungs-POC: Nächste Schritte nach dem Konzeptnachweis

[Aufspaltung des Zahlungs-POC: Nächste Schritte nach dem Konzeptnachweis](./next-steps.md)

**Zweck:** Roadmap für die Weiterentwicklung des POC zu produktionsbereiten Mustern.

**Warum es erforderlich ist:** Ein PoC-Tutorial birgt die Gefahr, dass Entwickler ein „Was jetzt?“ Gefühl. In diesem Dokument werden die natürlichen Fortschritte von der Demo- zur Produktionsumgebung dargestellt: Ersetzen des Demo-Dashboards durch eine Experience Cloud-Erweiterung, Verbinden eines echten ERP, Hinzufügen von API-Mesh, Erweitern des App Builder-Workflows und Checkliste für die Produktionsbereitstellung.

**Wichtiger Inhalt:**

* Architekturentwicklung (PoC → Phase 2 → Phase 3)
* ERP-Integrationsmuster (was ändert sich, was bleibt gleich)
* API-Mesh-Brokermuster
* Checkliste für die Produktionsbereitstellung
* Wichtige Referenzlinks

**Tutorial-Verwendung** Abschlussabschnitt „Nächste Schritte“. Dies ist auch als Gesprächsstarter für die Berechnung des Umfangs eines echten Projekts nützlich.


## Empfohlene Tutorial-Abschnitte

Basierend auf diesen Dateien ist eine typische Struktur für Leser:

| Tutorial-Abschnitt | Experience League-Seite |
| --- | --- |
| Einführung und Lernziele | [Erstellen eines aufgeteilten Zahlungs-POC: App Builder- und KI-Tools](./overview.md) |
| End-to-End-Demo (Video) | [Erstellen eines aufgeteilten Zahlungs-POC: Vollständige Demo zu App Builder](./full-demo.md) |
| Architektur: Was lebt wo? | [Aufspaltung des Zahlungs-POC: Architektur- und Design-Entscheidungen](./architecture-and-decisions.md) |
| Voraussetzungen und Einrichtung | [Aufspaltung des Zahlungs-POC: Voraussetzungen und Einrichtung der Umgebung](./prerequisites-and-setup.md) |
| Umgebungsvariablen | [Aufspaltung des Zahlungs-POC: Umgebungsvariablen-Referenz](./env-reference.md) |
| Schritt 1: Commerce-Modul erstellen | [Zahlungs-POC aufteilen: Commerce-Modul-KI-Eingabeaufforderung](./commerce-module-prompt.md) |
| Schritt 2: App Builder Orchestrator erstellen | [Zahlungs-POC aufteilen: App Builder Orchestrator-KI-Eingabeaufforderung](./orchestrator-prompt.md) |
| Schritt 3: Testen des End-to-End-Flusses | [Aufspaltung des Zahlungs-POC: Test- und Verifizierungshandbuch](./testing-and-verification.md) |
| Schritt 4 (optional): Erweiterung der Admin-Benutzeroberfläche | [Zahlungs-POC aufteilen: Eingabeaufforderung für die Erweiterung der Experience Cloud-Benutzeroberfläche](./experience-cloud-ui-prompt.md) |
| Nächste Schritte und Produktionspfad | [Aufspaltung des Zahlungs-POC: Nächste Schritte nach dem Machbarkeitsnachweis](./next-steps.md) |


## Wichtige Hinweise für Autoren von Tutorials

**Bei der Annahme des Luma-Designs:** Jede Build-Eingabeaufforderung generiert Code für eine saubere Luma-Installation. Im Tutorial sollte dies ganz oben klar angegeben werden. Entwicklerinnen und Entwickler mit benutzerdefinierten Checkouts müssen die `LayoutProcessorPlugin`-Injections-Pfade und möglicherweise die RequireJS-Konfiguration anpassen. Die Eingabeaufforderungen zur Serieneinführung und zum Build enthalten Hinweise zur Anpassung.

**Zum PHP-Modul:** Das Tutorial stellt den PHP-Code nicht explizit als Copy-Paste-Download bereit. Die KI-Eingabeaufforderung *generiert* sie. Dies ist beabsichtigt - es lehrt das Muster der Verwendung von KI zum Erstellen von Commerce-Erweiterungen, nicht nur das Kopieren und Einfügen von Textbausteinen. Der generierte Code sollte jedoch, wenn er in einer sauberen Umgebung aufgefordert wird, genau mit dem funktionierenden Code in `app/code/Client/SplitPayment/` übereinstimmen.

**Zum Schwellenwert von 100 $:** Dies ist ein hartcodierter PoC-Wert. Das Tutorial sollte beachten, dass Real Stores dies über die Commerce-Admin-Konfiguration und nicht über eine Kompilierungszeitkonstante konfigurieren sollten.

**Abhängigkeit bei Filialguthaben:** Der aufgeteilte Zahlungsfluss erfordert `Magento_CustomerBalance` (das native Filialguthaben-Modul).


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
