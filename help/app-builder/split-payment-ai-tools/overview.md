---
title: 'Erstellen eines aufgeteilten Zahlungs-POC: App Builder- und KI-Tools'
description: Erfahren Sie mehr über einen separaten Zahlungsnachweis mit App Builder und Commerce PaaS, einschließlich der Ziele, der Architektur und der Themen, die in dieser ersten Sitzung behandelt werden.
feature: App Builder, Paas, Payments
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Technical Video
duration: 260
jira: KT-20791
source-git-commit: 9add0b4bfa1eba33ec359adaa766b64711df25ba
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# Erstellen eines aufgeteilten Zahlungs-POC: App Builder- und KI-Tools

Dies ist das erste einer Reihe von Tutorials, die Sie mit der Verwendung der KI-unterstützten Entwicklung vertraut machen, um einen Machbarkeitsnachweis für die Aufspaltung der Zahlung zu erstellen. Sie arbeiten mit Adobe App Builder und Adobe Commerce in der Cloud (PaaS) oder lokal und gehen von einer Übersicht in dieser Sitzung zu den praktischen Tutorials, die folgen. Erwarten Sie Ziele, eine allgemeine Architektur und eine Roadmap zu dem, was der Rest der Serie abdeckt.

## Video

>[!VIDEO](https://video.tv.adobe.com/v/3483933?learn=on)

## Wichtige Details


Dieses Tutorial überbrückt die Kluft zwischen dem, wo die meisten Adobe Commerce-Teams heute sind - tief in PHP - und dem, wohin Adobe sie gehen möchte: ereignisgesteuerte, Server-lose Geschäftslogik, die außerhalb von Commerce in Adobe App Builder läuft. Dies geschieht durch eine echte, funktionierende Funktion anstatt durch ein Spielzeugbeispiel.

### Was Sie tatsächlich bauen werden

Split-Zahlungssystem, bei dem Kunden mit einer Kombination aus Nachnahme und Vorratskredit bezahlen. Nachdem die Bestellung aufgegeben wurde, bestätigt oder lehnt ein Benutzer (oder ERP-System) die Barzahlung über ein eigenständiges Dashboard ab - ohne jemals Commerce Admin zu öffnen. Der gesamte Workflow zum Akzeptieren/Ablehnen wird in App Builder ausgeführt.

#### Der Architekturunterricht (Kernunterricht)

Das Tutorial zeigt ein absichtliches und wiederholbares Entscheidungs-Framework:

* **Was in PHP bleiben muss:** alles, was synchron im Commerce-Anfragezyklus läuft oder Commerce-interne APIs ohne saubere externe Oberfläche aufruft
* **Was zu App Builder wechselt:** alles andere - Ereignisverarbeitung, Benutzer-Workflow, externe Integrationen und Tools für die Benutzereingabe

Es geht nicht darum, „alles nach App Builder zu verschieben“. Es ist ein praktischer, ehrlicher Ausgangspunkt für Teams, die die Umstellung ohne Umschreibung beginnen müssen.

### Warum der PHP-Code nicht enthalten ist

Der Ansatz mit der KI-Eingabeaufforderung ist tatsächlich besser als Beispiel-Code für diesen Anwendungsfall, weil die Eingabeaufforderung die Verhaltenskontrakte und die architektonischen Überlegungen erfasst, die Beispiel-Code allein nicht vermitteln kann. Ein Entwickler, der die Eingabeaufforderung ausführt und die Ausgabe liest, versteht, warum der Code so geformt ist, wie er ist, und nicht nur, wie er aussieht.

### Was enthalten ist

* Vollständiger App Builder-Anwendungs-Code (projektübergreifend konsistent - direkt oder als Referenz verwenden)
* Ein kompletter Satz von nummerierten KI-Eingabeaufforderungen, die für Cursor und Claude entwickelt wurden und das Commerce-Modul, den App Builder Orchestrator, das Benutzer-Dashboard, Tests und den Weg zur Produktion abdecken
* Ein Simulationsskript zum Testen des Akzeptanz-/Ablehnungsflusses gegenüber einer Live-Commerce-Site, ohne dass ein echtes ERP erforderlich ist
* Architekturdokumentation zur Erläuterung jeder Entscheidung

### Für wen ist das?

Entwicklerinnen und Entwickler auf Adobe Commerce On-Premise oder Commerce Cloud, die mit der ersten echten App Builder-Integration beginnen. Nicht für die Headless-API-First-Bereitstellung - speziell für Teams, die sich in der Umstellung befinden und eine herkömmliche Storefront betreiben, die sehen möchten, wie sie echte Geschäftslogik auf App Builder abladen können, ohne ihre bestehenden PHP-Investitionen aufzugeben.

### Hinweis zu Voraussetzungen

Adobe Commerce 2.4.5 oder höher, Zugriff auf eine Adobe Developer Console-Organisation mit aktiviertem App Builder-Projekt und I/O-Ereignissen. Für die Checkout-Benutzeroberfläche wird von einem sauberen Luma-Design ausgegangen. Bei benutzerdefinierten Designs muss die Eingabeaufforderung angepasst werden, bevor sie ausgeführt wird.

### Abschließende Gedanken

Dies sollte als Einstiegsdiskussion über die KI-gestützte Entwicklung betrachtet werden. Dieses Tutorial ist eine Demonstration für die Verwendung von KI-Tools in einem Commerce-Entwicklungs-Workflow und nicht nur ein Tutorial zu aufgeteilten Zahlungen.

{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
