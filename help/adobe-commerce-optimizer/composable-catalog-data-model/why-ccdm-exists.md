---
title: Warum das Composable Catalog Data Model (CCDM) vorhanden ist
description: Erfahren Sie, wie CDM einen einheitlichen Katalog speichert, während Storefronts gefilterte Produkte, Preise und Regeln mithilfe von Katalogansichten und Merchandising-Services erhalten.
feature: Saas, Storefront
topic: Commerce
role: Developer
level: Beginner
doc-type: Tutorial
duration: 259
last-substantial-update: 2026-05-15T00:00:00.000Z
jira: KT-18624
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%
---
# Warum das zusammenstellbare Katalogdatenmodell vorhanden ist

Moderne Commerce-Teams verkaufen häufig über **Marken**, **Regionen**, **&#x200B;**&#x200B;und **digitale Kanäle**. Wenn jeder Kanal seine eigene Katalogkopie speichert, verbringen Teams mehr Zeit damit, SKUs, Preise und Verfügbarkeit miteinander in Einklang zu bringen, als das Käufererlebnis zu verbessern. Das **Adobe Composable Catalog Data Model (CCDM)** hinter **Adobe Commerce Optimizer** wurde entwickelt, um dieses Muster umzukehren: **ein einheitlicher Katalog** in einer SaaS-Ebene, mit **Katalogansichten** und **Richtlinien** die Gestaltung dessen, was jede Storefront oder Integration sehen darf.

## Für wen ist dieses Video bestimmt?

* Commerce-Lösungsarchitekten und -entwickler, die noch nicht mit Adobe Commerce Optimizer vertraut sind und den Geschäftskontext benötigen, bevor sie Katalogquellen, Ansichten und Richtlinien konfigurieren

## Videoinhalt

* Warum duplizierte, kanalspezifische Kataloge operationelle Risiken und langsamere Innovationen schaffen
* Wie CDM die Vereinheitlichung von Produktdaten beibehält und gleichzeitig Szenarien mit mehreren Marken und mehreren Regionen unterstützt
* Wie Katalogansichten als „Linse“ zwischen einem freigegebenen Basiskatalog und einer bestimmten Storefront oder Zielgruppe fungieren
* Wie Merchandising Services-APIs diese Ansichten nutzen, damit Headless-Erlebnisse mit dem konfigurierten Katalog übereinstimmen

>[!VIDEO](https://video.tv.adobe.com/v/3491294?captions=ger&learn=on)

## Die Herausforderung mit isolierten Katalogen

Wenn jede Händlerseite, regionale Storefront oder jede Markeneigenschaft eine **eigene Katalogdatenbank** unterhält, treten mehrere Probleme auf:

* **Duplizierung** - Die gleiche SKU, Beschreibung und Medien werden mehrmals eingegeben.
* **Drift** - Preisaktualisierungen, neue Attribute oder auslaufende Artikel landen in einem Kanal, aber nicht in anderen.
* **Langsamere Launches** - Jeder neue Touchpoint wiederholt umfangreiche Datenarbeiten, anstatt einen einzigen Produktdatensatz wiederzuverwenden.

CCDM ist vorhanden, sodass Produktinformationen in einem zusammenstellbaren **einem zusammenstellbaren Katalog** abgelegt werden können, sodass andere Systeme eine Bereicherung darstellen, während Storefronts weiterhin **kanalgerechte** Sortimente und Preise erhalten.

## Änderungen am zusammenstellbaren Katalogdatenmodell

In Adobe Commerce Optimizer werden Produktdaten **aus einer oder mehreren** Katalogquellen“ (z **B. einem Gebietsschema wie `en-US` oder vorgelagerten Systemen wie PIM oder ERP) in einen einheitlichen** aufgenommen. Diese Quelle liefert die Rohattribute und -werte.

**Katalogansichten** definieren dann, wie diese einheitlichen Daten für **Geschäftskontext** organisiert und bereitgestellt) werden: Welche Produkte Ihre **Richtlinien**, welche **Preisbücher** gelten und welche **Katalogquelle** die Ansicht unterstützt. Dieselben zugrunde liegenden Datensätze können daher **viele Projektionen** z. B. separate Ansichten pro Händler, Region oder Marke, unterstützen, ohne den gesamten Katalog für jede Site klonen zu müssen.

Diese Trennung - **woher die Daten stammen** (Katalogquelle) versus **wie sie präsentiert werden** (Katalogansicht) - ist der Hauptgrund dafür, dass Teams CCDM verwenden, anstatt parallele Kataloge pro Kanal zu verwalten.

## Katalogansichten als Storefront-Objektiv

Wie in [Katalogansichten für Merchandising-Services](https://experienceleague.adobe.com/de/docs/commerce/optimizer/setup/catalog-view){target="_blank"} beschrieben, verhält sich eine Katalogansicht wie eine **Linse**: Käufer sehen nur die Produkte, Preise und Regeln, die diese Ansicht zulässt, während der **Basiskatalog** das gemeinsame Aufzeichnungssystem bleibt. Dieses Modell verbindet sich direkt mit **Merchandising Services**, sodass API-Clients die richtige Ansicht (und die zugehörigen Kopfzeilen) übergeben und für jedes Erlebnis eine konsistente, richtliniengesteuerte Antwort erhalten.

Eine genauere Anleitung dazu, wie diese Teile in einen End-to-End-Fluss passen, finden Sie im Abschnitt Anleitung für Entwickler [Erstellen eines zusammensetzbaren Katalogs für Ihre Storefront](https://developer.adobe.com/commerce/services/optimizer/ccdm-use-case){target="_blank"}.

## Verwandte Inhalte

* [Informationen zu Katalogansichten](./learn-about-the-ccdm-feature-catalog-views.md)
* [Katalogansichten für Merchandising-Services](https://experienceleague.adobe.com/de/docs/commerce/optimizer/setup/catalog-view){target="_blank"}
* [Erstellen eines zusammenstellbaren Katalogs für Ihre Storefront](https://developer.adobe.com/commerce/services/optimizer/ccdm-use-case){target="_blank"}
* [Handbuch zu [!DNL Adobe Commerce Optimizer]](https://experienceleague.adobe.com/de/docs/commerce/optimizer/overview){target="_blank"}
* [Erste Schritte mit der Merchandising-API](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#make-your-first-request){target="_blank"}

