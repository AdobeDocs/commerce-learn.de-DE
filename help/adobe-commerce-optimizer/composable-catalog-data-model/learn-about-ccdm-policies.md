---
title: Erfahren Sie mehr über CCDM-Richtlinien im zusammensetzbaren Katalogdatenmodell
description: Erfahren Sie, wie Richtlinien im Adobe Composable Catalog Data Model Produkte mit STATIC-Regeln und TRIGGER-Headern in jeder Katalogansicht filtern.
feature: Saas, Storefront
topic: Commerce
role: Developer
level: Beginner
doc-type: Tutorial
duration: 378
last-substantial-update: 2026-05-21T00:00:00Z
jira: KT-21258
source-git-commit: 84a3cb5868dd7c6f4adb0d46d53ed718133a6895
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Richtlinien im Adobe Composable Catalog Data Model

Wenn eine **Katalogansicht** die Linse ist, die das formt, was Kunden von einem einheitlichen Basiskatalog sehen, **Richtlinien** ist das, woraus diese Linse besteht. In diesem Tutorial wird erläutert, was eine Richtlinie ist, wie **STATIC**- und **TRIGGER**-Richtlinien im Demonstrationsszenario **Carvelo Automobiles** zusammenarbeiten und warum die Aktualisierung einer Richtlinie sofort wirksam wird - ohne den Katalog neu zu erstellen.

## Für wen ist dieses Video bestimmt?

* Commerce-Lösungsarchitekten und -entwickler, die Katalogansichten und Merchandising-Regeln in Adobe Commerce Optimizer konfigurieren

## Videoinhalt

* Richtlinien als Datenzugriffsfilter für Produktattribute
* Kombinieren mehrerer Richtlinien in der Celport-Katalogansicht (Marken und Teilekategorien)
* STATISCHE Richtlinien für dauerhafte Geschäftsregeln
* Durch API-Anfrage-Header aktivierte Trigger-Richtlinien (z. B. `AC-Policy-Brand`)
* Aktualisieren von Richtlinien in täglichen Vorgängen ohne Katalogneuaufbau

>[!VIDEO](https://video.tv.adobe.com/v/3491433?captions=ger&learn=on)

Eine **Richtlinie** ist ein **Datenzugriffsfilter**. Sie prüft Produktattribute und wendet Regeln an, die bestimmen, welche Produkte eine Katalogansicht verfügbar machen kann. Richtlinien befinden sich oberhalb des freigegebenen zusammensetzbaren Katalogs und duplizieren keine Katalogdaten.

## STATISCHE Richtlinien

Eine **STATIC**-Richtlinie ist **immer aktiviert**. Es erzwingt dauerhafte Geschäftsregeln unabhängig vom Käuferverhalten oder Sitzungsstatus.

Im Celport-Szenario umfassen die STATISCHEN Regeln Folgendes:

* Celport wird nur die Marken **Bolt** und **Cruz** verkaufen.
* Celport zeigt nur **Bremsen** und **Aufhängung** Teile.

Diese Regeln werden nie abgeschaltet. STATISCHE Richtlinien sind der Ort **an dem** Lizenzvereinbarungen **„territoriale**&quot; und **Markenberechtigungen**. Wenn Sie sie einmal festlegen, erzwingt Adobe Commerce Optimizer sie automatisch bei jeder Anfrage.

## TRIGGER-Richtlinien

Richtlinien mit einer Wertquelle von **TRIGGER** werden manchmal als **exklusive Richtlinien** bezeichnet. Die Katalogansicht führt diese Richtlinie **nur bei Angabe des Triggers** in der Kopfzeile des API-Aufrufs aus.

Beispielsweise kann eine Experience Delivery Services (EDS)-Storefront ein Dropdown-Menü mit **Alle Marken**, **Aurora**, **Bolt** und **Cruz**:

* In der ersten Seitenansicht ist nichts ausgewählt, sodass keine zusätzliche Markenkopfzeile gesendet wird.
* Wenn der Käufer &quot;**&quot; auswählt** setzt die zugrunde liegende API die `AC-Policy-Brand` auf `Bolt`.
* Wenn der Käufer &quot;**&quot;**, wird dieselbe Kopfzeile auf &quot;`Cruz`&quot; festgelegt.

Die Katalogansicht wendet die TRIGGER-Richtlinie nur an, wenn diese Kopfzeile vorhanden ist. Diese unterstützt interaktive Filterung, ohne die permanenten STATIC-Regeln zu ändern.

## GEMEINSAM MIT STATIC UND TRIGGER

**STATIC**-Richtlinien verarbeiten dauerhafte Regeln. **TRIGGER** Richtlinien verarbeiten interaktive Richtlinien. Zusammen in einer einzigen Katalogansicht bieten sie sowohl **Compliance** als auch **Flexibilität** - feste Sortimentgrenzen sowie kundengesteuerte Verfeinerung.

## Richtlinien aktualisieren, ohne den Katalog neu zu erstellen

Für den täglichen Betrieb müssen die Richtlinien sofort geändert werden. Nehmen wir an, die Lizenzvereinbarung von Celport erlaubt **Reifen** sowie Bremsen und Federung:

1. Öffnen Sie die entsprechende Richtlinie.
1. Fügen Sie **Reifen** zur Werteliste hinzu.
1. Speichern.

Diese Änderung ist **sofort verfügbar**. Es gibt keine Katalogneuerstellung, Neubereitstellung oder Wartezeit. Die nächste Anfrage an die Celport-Storefront spiegelt die Aktualisierung wider.

Richtlinien sind einfache Filter in einem **freigegebenen Katalog**, keine Regeln, die in separate Katalogkopien eingebettet sind. **Ändern Sie die Regel, nicht die Daten.**

## Verwandte Inhalte

* [Warum das zusammenstellbare Katalogdatenmodell vorhanden ist](./why-ccdm-exists.md)
* [Informationen zu Katalogansichten](./learn-about-the-ccdm-feature-catalog-views.md)
* [Katalogansichten für Merchandising-Services](https://experienceleague.adobe.com/de/docs/commerce/optimizer/setup/catalog-view){target="_blank"}
* [Handbuch zu [!DNL Adobe Commerce Optimizer]](https://experienceleague.adobe.com/de/docs/commerce/optimizer/overview){target="_blank"}
* [Erste Schritte mit der Merchandising-API](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api/#make-your-first-request){target="_blank"}
