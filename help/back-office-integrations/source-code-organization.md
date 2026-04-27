---
title: Erfahren Sie mehr über das Commerce Integration Starter Kit mit Schlüsselordnern und Automatisierungsskripten
description: Erfahren Sie mehr über die Organisation des Quell-Codes im Commerce Integration Starter Kit. ​
landing-page-description: Erkunden der Source Code-Organisation in einem Commerce Integration Starter Kit
kt: 15868
doc-type: video
duration: 534
audience: all
last-substantial-update: 2024-7-30
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
old-role: Architect, Developer
role: Developer
level: Intermediate
exl-id: 678f4d2b-c57e-4afb-a535-1048a88bc3b1
TQID: https://experienceleague.adobe.com/P6-sK18TcpC91YXJcXohIvzmii3N66ZKh3nZha-RYQY
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 371
ht-degree: 0%

---

# Source Code-Organisation für das Adobe Starter Kit

Erfahren Sie mehr über die Organisation des Quell-Codes im Adobe Commerce Integration Starter Kit. &#x200B; Sie die Struktur des Projekts durch Hervorheben wichtiger Ordner wie `actions` und `scripts` und ihrer jeweiligen Inhalte. &#x200B; Der Ordner „actions“ enthält Unterordner wie `ingestion` und `webhook`, die wesentlichen Code für die Ereignisverarbeitung und -verfolgung enthalten. Außerdem erfahren Sie mehr über die `starter-kit-info` und `scripts` Ordner. Der Ordner `scripts` konzentriert sich auf Automatisierungsskripte wie `commerce-event-subscribe` und `onboarding`, die die Ereigniskonfiguration und die Anbietereinrichtung innerhalb des Projekts optimieren.
&#x200B;
Erkunden Sie die Logik hinter der Quell-Code-Struktur und beschreiben Sie, wie die `commerce`- und `external`-Ordner unter den einzelnen Entitätsordnern Ereignisse verarbeiten, die von verschiedenen Systemen stammen. In diesem Video wird die Rolle des `consumer`-Ordners beim Senden von Ereignissen an die entsprechende Ereignishandler-Laufzeitaktion erläutert, um eine nahtlose Verarbeitung sicherzustellen. In diesem Video wird auch der in den Laufzeitaktionen implementierte Wiederholungsmechanismus behandelt, um fehlschlagende Ereignisse effektiv zu behandeln. &#x200B;Machen Sie sich mit der Organisation und Funktionalität des Quell-Codes im Adobe Commerce Integration Starter Kit vertraut und erhalten Sie wertvolle Einblicke in die Ereignisverarbeitung, Automatisierungsskripte und Konfigurationseinstellungen.

## Zielgruppe

* Entwickler, die verstehen möchten, wie der Quell-Code in wichtigen Ordnern wie `actions` und `scripts` organisiert ist.
* Erfahren Sie, dass der Ordner `actions` Unterordner wie `ingestion` und enthält` webhook` die wichtigen Code für die Verarbeitung von Ereignissen und das Tracking von Bereitstellungen enthalten.
* Entwickler, die mehr über den `actions` erfahren möchten, der Ordner für Entitäten wie `customer`, `order`, `product` und `stock` enthält.

## Videoinhalt

* Verstehen Sie, dass die vier Hauptordner `actions`, `scripts`, `test` und `utils` sind, wobei der Schwerpunkt auf den `actions` und `scripts` Ordnern während der Sitzung liegt. &#x200B;
* Erfahren Sie mehr über den `actions` Ordner und darüber, wie er wichtige Unterordner wie `ingestion` und `webhook` enthält.
* Erfahren Sie mehr über den `actions` Ordner und darüber, warum es bestimmte Ordner für Entitäten wie `customer`, `order`, `product` und `stock` gibt, die jeweils Laufzeitaktionen enthalten, die in `commerce` und `external` Ordner strukturiert sind, um Ereignisse aus Commerce und Drittanbietersystemen effektiv zu verwalten. &#x200B;
* Erfahren Sie, wie wichtig es ist, den Code im `starter-kit-info`-Ordner nicht zu ändern, der eine Laufzeitaktion enthält, die von Adobe verwendet wird, um Projektbereitstellungen basierend auf dem Starter Kit zu verfolgen. &#x200B;
* Machen Sie sich mit dem `scripts`-Ordner vertraut, der Automatisierungsskripte wie `commerce-event-subscribe` und `onboarding` enthält, die die Ereigniskonfiguration, die Anbietereinrichtung und die Konfiguration des Adobe I/O Events-Moduls in Commerce automatisieren. &#x200B;

>[!VIDEO](https://video.tv.adobe.com/v/3431691?learn=on)

{{$include /help/_includes/starter-kit-related-links.md}}
