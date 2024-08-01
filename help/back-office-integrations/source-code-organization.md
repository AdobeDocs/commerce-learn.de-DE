---
title: Erfahren Sie mehr über das Commerce Integration Starter Kit mit wichtigen Ordnern und Automatisierungsskripten - erklärt
description: Erfahren Sie mehr über die Organisation des Quellcodes im Commerce Integration Starter Kit. ​
landing-page-description: Source Code-Organisation in einem Commerce Integration Starter Kit
kt: 15868
doc-type: video
duration: 420
audience: all
last-substantial-update: 2024-7-30
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Architect, Developer
level: Intermediate
source-git-commit: 11daa4b29dafe5fcecf6b75cf2269b87f65c4612
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Source-Code-Organisation für das Adobe Starter Kit

Erfahren Sie mehr über die Organisation des Quellcodes im Adobe Commerce Integration-Starter-Kit. &#x200B; Durchsuchen Sie die Struktur des Projekts und markieren Sie wichtige Ordner wie `actions` und `scripts` sowie deren jeweiligen Inhalt. &#x200B; Der Ordner &quot;Aktionen&quot;enthält Unterordner wie `ingestion` und `webhook`, die für die Ereignisverarbeitung und -verfolgung erforderlichen Code enthalten. Außerdem erfahren Sie mehr über die Ordner `starter-kit-info` und `scripts`. Der Ordner `scripts` konzentriert sich auf Automatisierungsskripte wie `commerce-event-subscribe` und `onboarding`, die die Ereigniskonfiguration und die Einrichtung des Anbieters innerhalb des Projekts optimieren.
&#x200B;
Erkunden Sie die Logik hinter der Quellcodestruktur und legen Sie im Einzelnen dar, wie die Ordner `commerce` und `external` unter jedem Entitätsordner Ereignisse aus verschiedenen Systemen verarbeiten. In diesem Video wird die Rolle des Ordners `consumer` beim Versenden von Ereignissen an die entsprechende Ereignis-Handler-Laufzeitaktion erläutert, um eine nahtlose Verarbeitung sicherzustellen. Das Video behandelt auch den Wiederholungsmechanismus, der in den Laufzeitaktionen implementiert ist, um fehlerhafte Ereignisse effektiv zu verarbeiten. &#x200B;Machen Sie sich mit der Organisation und Funktionalität des Quellcodes im Adobe Commerce Integration-Starter-Kit vertraut und bieten Sie wertvolle Einblicke in die Ereignisverarbeitung, Automatisierungsskripte und Konfigurationssatzungen.

## Zielgruppe

* Entwickler, die verstehen möchten, wie der Quellcode in Schlüsselordner wie `actions` und `scripts` unterteilt ist.
* Erfahren Sie mehr über den Ordner &quot;`actions`&quot;, der Unterordner wie `ingestion` und ` webhook` enthält, die für die Verarbeitung von Ereignissen und das Tracking von Bereitstellungen erforderlichen Code enthalten.
* Entwickler, die mehr über den Ordner `actions` erfahren möchten, der Ordner für Entitäten wie `customer`, `order`, `product` und `stock` enthält.

## Videoinhalt

* Beachten Sie, dass die vier Hauptordner `actions`, `scripts`, `test` und `utils` sind, wobei der Fokus auf den Ordnern `actions` und `scripts` während der Sitzung liegt. &#x200B;
* Erfahren Sie mehr über den Ordner `actions` und wie er wichtige Unterordner wie `ingestion` und `webhook` enthält.
* Durchsuchen Sie den Ordner &quot;`actions`&quot;, und warum es bestimmte Ordner für Entitäten wie `customer`, `order`, `product` und `stock` gibt, die jeweils Laufzeitaktionen enthalten, die in die Ordner `commerce` und `external` strukturiert sind, um Ereignisse aus Commerce und Drittanbietersystemen effektiv zu verwalten. &#x200B;
* Erfahren Sie, wie wichtig es ist, den Code im Ordner &quot;`starter-kit-info`&quot;nicht zu ändern, da dieser eine Laufzeitaktion enthält, die von Adobe verwendet wird, um Projektbereitstellungen basierend auf dem Starter Kit zu verfolgen. &#x200B;
* Machen Sie sich mit dem Ordner `scripts` vertraut, der Automatisierungsskripte wie `commerce-event-subscribe` und `onboarding` enthält, die die Ereigniskonfiguration, die Einrichtung des Anbieters und die Konfiguration des Adobe I/O Events-Moduls in Commerce automatisieren. &#x200B;

  >[!VIDEO](https://video.tv.adobe.com/v/3431691?learn=on)

  {{$include /help/_includes/starter-kit-related-links.md}}