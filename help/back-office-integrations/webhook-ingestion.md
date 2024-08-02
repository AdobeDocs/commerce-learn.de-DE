---
title: Konfigurieren, Bereitstellen und Anpassen eines Aufnahme-Webhooks zur Integration von Commerce in ein Drittanbietersystem
description: Erfahren Sie, wie Sie einen Erfassungswebhook einrichten und anpassen, um die Kommunikation zwischen Commerce und einem Backoffice-System von Drittanbietern zu erleichtern.
landing-page-description: Erfahren Sie, wie Sie mit dem Commerce Integration Starter Kit Commerce mithilfe eines Erfassungswebhooks in ein Back-Office-System von Drittanbietern integrieren können.
kt: 15870
doc-type: video
duration: 593
audience: all
last-substantial-update: 2024-7-30
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Architect, Developer
level: Intermediate
source-git-commit: f0c6e9262a2bf2de3144255de1fc78d6972b6d33
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Konfigurieren, Bereitstellen und Anpassen eines Aufnahme-Webhooks

Erfahren Sie mehr über die Einrichtung und Anpassung eines Erfassungswebhooks zur Integration von Commerce in ein Back-Office-System von Drittanbietern. &#x200B; In diesem Video wird erläutert, wie der Webhook Einschränkungen bei der Ereigniskommunikation zwischen Systemen beheben kann, indem er einen öffentlich verfügbaren Endpunkt bereitstellt, um Nachrichten vom Drittanbietersystem an die Adobe IO Eventing-API anzupassen. Der Prozess umfasst die Konfiguration des Webhooks in der Datei `actions.config.yaml`, die Aktivierung in der Datei `app.config.yaml` und die Bereitstellung des Webhooks, um die ordnungsgemäße Funktion sicherzustellen.

In diesem Video werden die Schritte zum Ändern des Webhook-Codes beschrieben, um Ereignisse von Drittanbietern in Formate zu übersetzen, die mit den abonnierten Ereignistypen der Integration kompatibel sind. Es wird das Hinzufügen einer `event-mapping.json` -Datei erläutert, um diese Übersetzung zu erleichtern, und es wird betont, wie wichtig es ist, die Laufzeitaktion nach den Änderungen erneut bereitzustellen. &#x200B; In diesem Video wird auch die Bedeutung der Validierung und Transformation eingehender Ereignis-Payloads in Übereinstimmung mit dem erwarteten Schema hervorgehoben, sodass eine erfolgreiche Verarbeitung und Integration mit der Commerce-API zur Erstellung von Kunden gewährleistet ist.

## Zielgruppe

* Entwickler, die einen Aufnahme-Webhook einrichten möchten
* Jeder, der Code für die Ereignisübersetzung anpassen möchte
* Entwickler und Architekten, die die Bedeutung von Authentifizierung und Nutzlastverwaltung verstehen möchten

## Videoinhalt

* Konfiguration und Bereitstellung: Das Video hebt hervor, wie wichtig es ist, den Aufnahme-Webhook in der Datei `actions.config.yaml` zu konfigurieren und in der Datei `app.config.yaml` zu aktivieren. Außerdem wird hervorgehoben, dass das Projekt nach Änderungen neu bereitgestellt werden muss, um sicherzustellen, dass der Webhook ordnungsgemäß funktioniert.
* Anpassung für Kompatibilität: Es ist wichtig, den Webhook-Code anzupassen, um Drittanbieter-Ereignisse in Formate zu übersetzen, die mit den abonnierten Ereignistypen der Integration übereinstimmen. &#x200B; Diese Anpassung sorgt für eine nahtlose Kommunikation zwischen Systemen und eine erfolgreiche Ereignisverarbeitung.
* Authentifizierungsimplementierung: Unternehmen sind für die Implementierung von Authentifizierungsmechanismen verantwortlich, die für ihre Bedürfnisse geeignet sind, um nicht autorisierte Anfragen bei der Verwendung des Erfassungswebhooks zu verhindern. Dieser Schritt ist für die Aufrechterhaltung der Sicherheit und Integrität der Integration von entscheidender Bedeutung.
* Payload-Validierung und -Umwandlung: Die Validierung und Transformation der eingehenden Ereignis-Payloads entsprechend dem erwarteten Schema ist für eine erfolgreiche Verarbeitung und Integration mit der Commerce-API von entscheidender Bedeutung. &#x200B; Durch das entsprechende Zuschneiden und Zuordnen von Feldern kann die Integration effizient mit den erforderlichen Daten funktionieren.

>[!VIDEO](https://video.tv.adobe.com/v/3431694?learn=on)

{{$include /help/_includes/starter-kit-related-links.md}}

## Codebeispiele

* [Benutzerdefinierter Aufnahme-Webhook](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit/customize-ingestion-webhook)
* [Hinzufügen des Aufnahmeplaners](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit/add-ingestion-scheduler)
