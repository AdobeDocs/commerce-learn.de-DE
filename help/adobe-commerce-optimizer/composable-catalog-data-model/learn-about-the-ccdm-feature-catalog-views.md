---
title: Erfahren Sie mehr über Katalogansichten im zusammensetzbaren Katalogdatenmodell
description: Erfahren Sie, wie Katalogansichten im Adobe Composable Catalog Data Model (CCDM) jeder Storefront einen Basiskatalog mit unterschiedlichen Produkten, Preisen und Regeln zuordnen.
feature: Saas, Storefront
topic: Commerce
role: Developer
level: Beginner
doc-type: Tutorial
duration: 297
last-substantial-update: 2026-05-15T00:00:00Z
jira: KT-21132
source-git-commit: e3257f9713b26b0ab8ca2e827aeaac4532ff9dff
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# Katalogansichten im zusammenstellbaren Adobe-Katalogdatenmodell

In Katalogansichten wird erläutert, wie sich die Bereitstellung der einzelnen Zielgruppen in einem zusammenstellbaren Katalog unterscheidet. In diesem Tutorial wird erläutert, was eine Katalogansicht ist, wie Adobe Commerce Optimizer sie für einen Käufer anwendet und warum eine eindeutige Ansichts-ID der Anker für Produkte, Preise und Regeln ist - mithilfe des **Carvelo Automobiles** Demonstrationsszenarios.

## Für wen ist dieses Video bestimmt?

* Commerce-Lösungsarchitekten und -entwickler, die Kataloge mit mehreren Marken oder Händlern in Adobe Commerce Optimizer modellieren

## Videoinhalt

* Das Szenario Carvelo Automobiles (Marken, Händlerverträge und Vereinbarungen)
* Was ist eine Katalogansicht und die „Objektiv“-Metapher über einem einheitlichen Basiskatalog?
* Verwendung einer Katalogansicht durch eine Storefront zum Filtern von Produkten und Preisen (z. B. Celport)
* Katalogansicht - Eindeutige IDs und der Geschäftswert einer einzelnen Datenquelle

>[!VIDEO](https://video.tv.adobe.com/v/3491261?learn=on)

## Szenario: Carvelo Automobile

**Carvelo Automobiles** ist eine fiktive Autoteilefirma, die häufig in Vorführungen, Dokumentationen und Tutorials in Adobe Commerce verwendet wird. Carvelo vertreibt Teile über drei Marken - **Aurora**, **Bolt** und **Cruz** - über drei Händler:

* **Arkbridge** gehört zur West Coast Inc.
* **Kingsbluff** und **Celport** gehören zur East Coast Inc.

Jeder Händler hat seine eigene Vereinbarung darüber, welche Produkte er verkaufen darf. Dadurch entsteht ein wirklich komplexes Setup - und es kann immer noch von **einem einzigen Basiskatalog)** etwa sechs Millionen SKUs ausgeführt werden. Die Funktion, die dies ermöglicht, ist eine **Katalogansicht**.

## Was ist eine Katalogansicht?

Eine **Katalogansicht** ist eine konfigurierte Ansicht Ihres Katalogs für einen bestimmten Geschäftskontext. Betrachten Sie es als eine **Linse**. Ihr einheitlicher Basiskatalog befindet sich in der Mitte und enthält jede SKU für jede Marke. Jeder Händler erhält eine eigene Linse - eine eigene Katalogansicht.

Im Beispiel:

* Das **Arkbridge**-Objektiv kann alle drei Marken zeigen - Aurora-, Bolt- und Cruz-Teile.
* Das **Celport**-Objektiv zeigt nur eine Teilmenge von Bolzen- und Cruz-Teilen.

Jede Katalogansicht kann auch die **Preisfindung** steuern. Die **zugrunde liegenden Katalogdaten ändern sich nicht** nur die sichtbaren Aspekte (Sortiment, Preis und Regeln) ändern sich für diesen Kontext.

## Wie Commerce Optimizer eine Katalogansicht anwendet

Wenn ein Käufer die Storefront **Celport** besucht, verwendet Adobe Commerce Optimizer die **Celport-Katalogansicht** um genau zu bestimmen, welche Produkte, Preise und Regeln gelten. Der Käufer sieht nur, was das Objektiv erlaubt.

Andere Produkte können noch im Katalog vorhanden sein - z. B. Aurora-Reifen, Bolzenmotoren oder Cruz-Batterien - aber **Celports Storefront legt sie nie offen** wenn die Katalogansicht dies nicht zulässt.

## Katalogansicht-ID und Geschäftswert

Jede Katalogansicht hat eine **eindeutige ID**. Diese ID verbindet Ihre Storefront mit ihrer Katalogkonfiguration. Sie legen es einmal in der Storefront-Konfiguration fest, und das nachgelagerte Verhalten folgt - die richtigen Produkte, die richtigen Preise und die richtigen Regeln.

Anstatt für jeden Händler oder jede Marke separate Kataloge zu pflegen - und diese zu synchronisieren - pflegen Sie **einen** zusammenstellbaren Katalog. Katalogansichten sind die Form **vieler verschiedener Storefront-Erlebnisse** aus dieser **einzigen Quelle der Wahrheit**.

## Verwandte Inhalte

* [Handbuch zu [!DNL Adobe Commerce Optimizer]](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview){target="_blank"}
* [Erste Schritte mit der Merchandising-API](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api/#make-your-first-request){target="_blank"}
