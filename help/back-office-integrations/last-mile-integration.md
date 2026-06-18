---
title: Integration der letzten Meile im Commerce Starter Kit
description: Erfahren Sie mehr über die Integration der letzten Meile in Commerce mithilfe von Erweiterbarkeits-Hooks für die Validierung, Umwandlung, Vorverarbeitung, Übermittlung und Nachbearbeitung.
doc-type: Technical Video
duration: 557
last-substantial-update: 2024-07-30
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Developer
level: Intermediate
jira: KT-15869
exl-id: e86e8c7b-d5d2-484d-90a2-9c5309c7ea1d
TQID: https://experienceleague.adobe.com/TCR23A98L8XrVDEQeqLQoOXKQPBQu-Wb7YnGUkBXgak
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: 9568f37b026d0e659e8092282cb923c7ecde58ac
workflow-type: tm+mt
source-wordcount: 342
ht-degree: 0%

---

# Integration der letzten Meile mit dem Adobe Starter Kit

Erfahren Sie mehr über Elemente, die Sie beim Starten der Last-Mile-Integration mit Adobe Commerce berücksichtigen sollten, und konzentrieren Sie sich auf Erweiterbarkeits-Hooks, um die Konnektivität mit Drittanbietersystemen zu verbessern. In diesem Video wird ein strukturierter Ansatz erläutert, bei dem verschiedene Hooks wie Validierung, Transformation, Vorverarbeitung, Senden und Nachbearbeitung einen nahtlosen Datenfluss und eine nahtlose Systemsynchronisierung sicherstellen. Jeder Hook erfüllt einen bestimmten Zweck, darunter:

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
