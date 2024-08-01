---
title: Integration der letzten Meile in das Commerce Integration Starter Kit.
description: Integration der letzten Meile in Commerce, Hervorhebung von Erweiterbarkeits-Hooks wie Validierung, Transformation, Vorverarbeitung, Versand und Nachbearbeitung. ​
landing-page-description: Erfahren Sie mehr über die Struktur und Funktionen von Erweiterungshaken bei der Integration von Letztmeilen für Commerce-Systeme.
kt: 15869
doc-type: video
duration: 465
audience: all
last-substantial-update: 2024-7-30
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Architect, Developer
level: Intermediate
source-git-commit: aed143b96f13a413f85fc461e11f358b4c657015
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Letztmeilenintegration mit dem Adobe Starter Kit

Erfahren Sie mehr über die Elemente, die Sie beim Start der Integration der letzten Meile mit Adobe Commerce berücksichtigen sollten, wobei der Schwerpunkt auf der Verwendung von Erweiterbarkeitshaken liegt, um die Konnektivität mit Drittanbietersystemen zu verbessern. In diesem Video wird ein strukturierter Ansatz beschrieben, bei dem verschiedene Hooks wie Validierung, Transformation, Vorverarbeitung, Versand und Nachbearbeitung einen nahtlosen Datenfluss und eine Systemsynchronisierung gewährleisten. Jeder Haken erfüllt einen bestimmten Zweck, darunter:

* Validieren eingehender Daten mit Schemata
* Transformieren von Datenobjekten zwischen Systemen
* Berechnungen vor dem Senden relevanter Informationen durchführen
* Senden der Daten an das Zielsystem

Es ist wichtig, für jeden Baustein separate JavaScript-Dateien zu verwalten, um die Integrität der Geschäftslogik zu wahren und zukünftige Framework-Upgrades zu erleichtern und so eine robuste und anpassbare Integrationseinrichtung zu gewährleisten.

Erfahren Sie mehr über die Bedeutung von Nachbearbeitungs-Aktivitäten über den Nachbearbeitungs-Hook, mit dem Benutzer nach der Datensynchronisation zusätzliche Aktionen ausführen können, z. B. Kommentare zu Bestellungen hinzufügen oder externe IDs speichern können. Das Video enthält Best Practices wie das Einkapseln von API-Anfragen in bestimmte Bibliotheken, um Verbindungen mit Drittanbietersystemen zu optimieren. Außerdem lernen Sie typische Anwendungsfälle für jeden Erweiterungspunkt und Anleitungen zum Umgang mit verschiedenen Szenarien kennen.

## Zielgruppe

* Entwickler, die die Struktur und Funktionalität von Erweiterbarkeits-Hooks lernen möchten und wie diese Hooks die Verbindung mit Drittanbietersystemen verbessern können.
* Entwickler, die typische Anwendungsfälle und Best Practices im Zusammenhang mit den einzelnen Erweiterbarkeits-Hooks lernen möchten, wie z. B. Validierung, Transformation, Vorverarbeitung, Versand und Nachbearbeitung, um einen nahtlosen Datenfluss, eine Systemsynchronisierung und eine effiziente Wartung der Integrationseinrichtung zu erleichtern. &#x200B;

## Videoinhalt

* Erfahren Sie mehr über die Struktur der aufgerufenen Aktionen in der Letztmeilenintegration.
* Machen Sie sich mit typischen Anwendungsfällen im Validierungs-Hook vertraut, einschließlich der Validierung eingehender Daten anhand von Schemas und des Überspringens bestimmter Ereignisse basierend auf bestimmten Kriterien. &#x200B;
* Erfahren Sie, welche Rolle der Transformationshaken beim Transformieren von Datenobjekten zwischen dem Ursprungs- und dem Zielsystem spielt.
* Erfahren Sie mehr über die Bedeutung des Sende-Hooks für die Erleichterung des tatsächlichen Versands von Daten an das Zielsystem.

>[!VIDEO](https://video.tv.adobe.com/v/3431692?learn=on)

{{$include /help/_includes/starter-kit-related-links.md}}
