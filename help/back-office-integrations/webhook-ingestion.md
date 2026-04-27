---
title: Konfigurieren, Bereitstellen und Anpassen eines Aufnahme-Webhooks
description: Erfahren Sie, wie Sie einen Aufnahme-Webhook einrichten und anpassen, um die Kommunikation zwischen Commerce und einem Back-Office-System eines Drittanbieters zu erleichtern.
landing-page-description: Erfahren Sie, wie Sie mit dem Commerce Integration Starter Kit Commerce mithilfe eines Aufnahme-Webhooks in ein Back-Office-System eines Drittanbieters integrieren können.
kt: 15870
doc-type: video
duration: 697
audience: all
last-substantial-update: 2024-7-30
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
old-role: Architect, Developer
role: Developer
level: Intermediate
exl-id: f2654873-256e-4c1b-abed-8bfbc4db3fbb
TQID: https://experienceleague.adobe.com/nUXdrsjzeD939jOjZS8ywPV3OeOaxpZCmeuveACtYrY
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 432
ht-degree: 0%

---

# Konfigurieren, Bereitstellen und Anpassen eines Aufnahme-Webhooks

Erfahren Sie mehr über die Einrichtung und Anpassung eines Aufnahme-Webhooks zur Integration von Commerce mit einem Back-Office-System eines Drittanbieters. &#x200B; diesem Video wird erläutert, wie der Webhook Einschränkungen bei der Ereigniskommunikation zwischen Systemen beheben kann, indem er einen öffentlich verfügbaren Endpunkt bereitstellt, um Nachrichten vom Drittanbietersystem an die Adobe IO Eventing-API anzupassen. Der Prozess umfasst das Konfigurieren des Webhooks in der `actions.config.yaml`-Datei, dessen Aktivierung in der `app.config.yaml`-Datei und dessen Bereitstellung, um eine ordnungsgemäße Funktionalität sicherzustellen.

In diesem Video werden die Schritte zum Ändern des Webhook-Codes beschrieben, um Ereignisse von Drittanbietern in Formate zu übersetzen, die mit den abonnierten Ereignistypen der Integration kompatibel sind. Es wird das Hinzufügen einer `event-mapping.json`-Datei erläutert, um diese Übersetzung zu erleichtern, und es wird betont, wie wichtig es ist, die Laufzeitaktion erneut bereitzustellen, nachdem Änderungen vorgenommen wurden. &#x200B; Video zeigt auch, wie wichtig es ist, eingehende Ereignis-Payloads zu validieren und so zu transformieren, dass sie dem erwarteten Schema entsprechen und eine erfolgreiche Verarbeitung und Integration mit der Commerce-API zum Erstellen von Kunden sicherstellen.

## Zielgruppe

* Entwickler, die einen Aufnahme-Webhook einrichten möchten
* Jeder, der Code für die Ereignisübersetzung anpassen möchte
* Entwickler und Architekten, die die Bedeutung von Authentifizierung und Payload-Management verstehen möchten

## Videoinhalt

* Konfiguration und Bereitstellung: Im Video wird hervorgehoben, wie wichtig es ist, den Aufnahme-Webhook in der `actions.config.yaml`-Datei zu konfigurieren und in der `app.config.yaml`-Datei zu aktivieren. Außerdem wird die Notwendigkeit hervorgehoben, das Projekt erneut bereitzustellen, nachdem Änderungen vorgenommen wurden, um sicherzustellen, dass der Webhook ordnungsgemäß funktioniert.
* Anpassung aus Kompatibilitätsgründen: Es ist wichtig, den Webhook-Code anzupassen, um Drittanbieterereignisse in Formate zu übersetzen, die den abonnierten Ereignistypen der Integration entsprechen. &#x200B; Diese Anpassung sorgt für eine nahtlose Kommunikation zwischen Systemen und eine erfolgreiche Ereignisverarbeitung.
* Authentifizierungsimplementierung: Unternehmen sind dafür verantwortlich, Authentifizierungsmechanismen zu implementieren, die für ihre Anforderungen geeignet sind, um nicht autorisierte Anforderungen bei der Verwendung des Aufnahme-Webhooks zu verhindern. Dieser Schritt ist für die Wahrung der Sicherheit und Integrität der Integration von wesentlicher Bedeutung.
* Payload-Validierung und -Transformation: Die Validierung und Transformation eingehender Ereignis-Payloads entsprechend dem erwarteten Schema ist für eine erfolgreiche Verarbeitung und Integration mit der Commerce-API von entscheidender Bedeutung. &#x200B; durch entsprechendes Zuschneiden und Zuordnen von Feldern kann die Integration mit den erforderlichen Daten effizient arbeiten.

>[!VIDEO](https://video.tv.adobe.com/v/3431694?learn=on)

{{$include /help/_includes/starter-kit-related-links.md}}

## Code-Beispiele

* [Webhook für benutzerdefinierte Aufnahme](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit/customize-ingestion-webhook)
* [Aufnahme-Scheduler hinzufügen](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit/add-ingestion-scheduler)
