---
title: Konfigurieren, Bereitstellen und Anpassen eines Aufnahme-Webhooks
description: Erfahren Sie, wie Sie einen Aufnahme-Webhook einrichten und anpassen, um die Kommunikation zwischen Commerce und einem Back-Office-System eines Drittanbieters zu erleichtern.
landing-page-description: Erfahren Sie, wie Sie mit dem Commerce Integration Starter Kit Commerce mithilfe eines Aufnahme-Webhooks in ein Back-Office-System eines Drittanbieters integrieren können.
kt: 15870
doc-type: video
duration: 593
audience: all
last-substantial-update: 2024-7-30
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
old-role: Architect, Developer
role: Developer
level: Intermediate
exl-id: f2654873-256e-4c1b-abed-8bfbc4db3fbb
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Konfigurieren, Bereitstellen und Anpassen eines Aufnahme-Webhooks

Erfahren Sie mehr über die Einrichtung und Anpassung eines Aufnahme-Webhooks zur Integration von Commerce mit einem Back-Office-System eines Drittanbieters&#x200B; In diesem Video wird erläutert, wie der Webhook Einschränkungen bei der Ereigniskommunikation zwischen Systemen beheben kann, indem ein öffentlich verfügbarer Endpunkt bereitgestellt wird, um Nachrichten vom Drittanbietersystem an die Adobe IO Eventing-API anzupassen. Der Prozess umfasst das Konfigurieren des Webhooks in der `actions.config.yaml`-Datei, dessen Aktivierung in der `app.config.yaml`-Datei und dessen Bereitstellung, um eine ordnungsgemäße Funktionalität sicherzustellen.

In diesem Video werden die Schritte zum Ändern des Webhook-Codes beschrieben, um Ereignisse von Drittanbietern in Formate zu übersetzen, die mit den abonnierten Ereignistypen der Integration kompatibel sind. Es wird das Hinzufügen einer `event-mapping.json`-Datei erläutert, um diese Übersetzung zu erleichtern, und es wird betont, wie wichtig es ist, die Laufzeitaktion erneut bereitzustellen, nachdem Änderungen vorgenommen wurden&#x200B; In diesem Video wird auch die Bedeutung der Validierung und Umwandlung eingehender Ereignis-Payloads entsprechend dem erwarteten Schema hervorgehoben, um eine erfolgreiche Verarbeitung und Integration mit der Commerce-API für die Erstellung von Kunden sicherzustellen.

## Zielgruppe

* Entwickler, die einen Aufnahme-Webhook einrichten möchten
* Jeder, der Code für die Ereignisübersetzung anpassen möchte
* Entwickler und Architekten, die die Bedeutung von Authentifizierung und Payload-Management verstehen möchten

## Videoinhalt

* Konfiguration und Bereitstellung: Im Video wird hervorgehoben, wie wichtig es ist, den Aufnahme-Webhook in der `actions.config.yaml`-Datei zu konfigurieren und in der `app.config.yaml`-Datei zu aktivieren. Außerdem wird die Notwendigkeit hervorgehoben, das Projekt erneut bereitzustellen, nachdem Änderungen vorgenommen wurden, um sicherzustellen, dass der Webhook ordnungsgemäß funktioniert.
* Anpassung aus Kompatibilitätsgründen: Es ist wichtig, den Webhook-Code anzupassen, um Drittanbieterereignisse in Formate zu übersetzen, die den abonnierten Ereignistypen der Integration entsprechen. &#x200B; Diese Anpassung sorgt für eine nahtlose Kommunikation zwischen Systemen und eine erfolgreiche Ereignisverarbeitung.
* Authentifizierungsimplementierung: Unternehmen sind dafür verantwortlich, Authentifizierungsmechanismen zu implementieren, die für ihre Anforderungen geeignet sind, um nicht autorisierte Anforderungen bei der Verwendung des Aufnahme-Webhooks zu verhindern. Dieser Schritt ist für die Wahrung der Sicherheit und Integrität der Integration von wesentlicher Bedeutung.
* Payload-Validierung und -Transformation: Die Validierung und Transformation eingehender Ereignis-Payloads entsprechend dem erwarteten Schema ist für eine erfolgreiche Verarbeitung und Integration mit der Commerce-API von entscheidender Bedeutung. &#x200B; Durch entsprechendes Zuschneiden und Zuordnen von Feldern kann die Integration mit den erforderlichen Daten effizient arbeiten.

>[!VIDEO](https://video.tv.adobe.com/v/3431694?learn=on)

{{$include /help/_includes/starter-kit-related-links.md}}

## Code-Beispiele

* [Webhook für die benutzerdefinierte Aufnahme](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit/customize-ingestion-webhook)
* [Aufnahme-Scheduler hinzufügen](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit/add-ingestion-scheduler)
