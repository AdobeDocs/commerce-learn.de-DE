---
title: Integration der letzten Meile im Commerce-Integrations-Starter-Kit.
description: Integration der letzten Meile in Commerce, wobei Erweiterbarkeitshaken wie Validierung, Umwandlung, Vorverarbeitung, Senden und Nachbearbeitung hervorgehoben werden​
landing-page-description: Erfahren Sie mehr über den Aufbau und die Funktionen von Erweiterbarkeitshaken bei der Integration der letzten Meile für Commerce-Systeme.
kt: 15869
doc-type: video
duration: 465
audience: all
last-substantial-update: 2024-7-30
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
old-role: Architect, Developer
role: Developer
level: Intermediate
exl-id: e86e8c7b-d5d2-484d-90a2-9c5309c7ea1d
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Integration der letzten Meile mit dem Adobe Starter Kit

Erfahren Sie mehr über Elemente, die Sie beim Starten der Last-Mile-Integration mit Adobe Commerce berücksichtigen sollten, wobei Sie sich auf die Verwendung von Erweiterbarkeits-Hooks konzentrieren sollten, um die Konnektivität mit Drittanbietersystemen zu verbessern. In diesem Video wird ein strukturierter Ansatz erläutert, bei dem verschiedene Hooks wie Validierung, Transformation, Vorverarbeitung, Senden und Nachbearbeitung einen nahtlosen Datenfluss und eine nahtlose Systemsynchronisierung sicherstellen. Jeder Hook erfüllt einen bestimmten Zweck, darunter:

* Validieren eingehender Daten anhand von Schemata
* Transformieren von Datenobjekten zwischen Systemen
* Durchführen von Berechnungen vor dem Senden relevanter Informationen
* Senden der Daten an das Zielsystem

Es ist wichtig, separate JavaScript-Dateien für jeden Block zu pflegen, um die Integrität der Geschäftslogik aufrechtzuerhalten und zukünftige Framework-Upgrades zu erleichtern, sodass eine robuste und anpassbare Integrationseinrichtung gewährleistet ist.

Erfahren Sie mehr über die Bedeutung von Nachbearbeitungsaktivitäten über den Nachbearbeitungs-Hook, der es Benutzern ermöglicht, zusätzliche Aktionen nach der Datensynchronisierung auszuführen, z. B. das Hinzufügen von Kommentaren zu Bestellungen oder das Speichern externer IDs. Das Video enthält Best Practices wie das Einkapseln von API-Anfragen in bestimmte Bibliotheken, um Verbindungen mit Drittanbietersystemen zu optimieren. Außerdem erfahren Sie mehr über typische Anwendungsfälle für jeden Hook und erhalten Anleitungen zum Umgang mit verschiedenen Szenarien.

## Zielgruppe

* Entwickler, die die Struktur und Funktionalität von Erweiterbarkeitshaken erlernen möchten und erfahren möchten, wie diese Erweiterungspunkte die Konnektivität mit Drittanbietersystemen verbessern können.
* Entwicklerinnen und Entwickler, die die typischen Anwendungsfälle und Best Practices im Zusammenhang mit den einzelnen Erweiterbarkeitshaken kennenlernen möchten, z. B. Validierung, Umwandlung, Vorverarbeitung, Versand und Nachbearbeitung, um einen nahtlosen Datenfluss, die Systemsynchronisierung und eine effiziente Wartung der Integrationseinrichtung zu ermöglichen. &#x200B;

## Videoinhalt

* Erfahren Sie mehr über die Struktur der aufgerufenen Aktionen in der Last-Mile-Integration.
* Machen Sie sich mit typischen Anwendungsfällen innerhalb des Validierungs-Hooks vertraut, einschließlich der Validierung eingehender Daten anhand von Schemas und dem Überspringen bestimmter Ereignisse auf der Grundlage bestimmter Kriterien. &#x200B;
* Erfahren Sie mehr über die Rolle des Transformations-Hooks beim Transformieren von Datenobjekten zwischen dem Ursprungs- und dem Zielsystem.
* Erfahren Sie mehr über die Bedeutung des Sende-Hooks bei der Erleichterung des tatsächlichen Datenversands an das Zielsystem.

>[!VIDEO](https://video.tv.adobe.com/v/3451936?captions=ger&learn=on)

{{$include /help/_includes/starter-kit-related-links.md}}
