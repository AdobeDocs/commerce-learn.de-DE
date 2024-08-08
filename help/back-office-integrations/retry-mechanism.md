---
title: Verwenden der nativen Funktionalität eines Wiederholungsmechanismus
description: Nutzen Sie den Wiederholungsmechanismus von Adobe I/O-Ereignissen für widerstandsfähige Anwendungen, einschließlich Wiederholungsbedingungen und visueller Indikatoren.
landing-page-description: Verstehen und nutzen Sie den integrierten Wiederholungsmechanismus von Adobe I/O-Ereignissen, um die Anwendungswiderstandsfähigkeit zu erhöhen und Ereignisaktivierungen effektiv zu verwalten.
kt: 15872
doc-type: video
duration: 314
audience: all
last-substantial-update: 2024-7-31
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Architect, Developer
level: Intermediate
source-git-commit: eb548dd83e3bab7a4a1486cd2cbd88efcc060121
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# Verwenden des Wiederholungsmechanismus von Adobe I/O-Ereignissen für die Anwendungswiderstandsfähigkeit

In diesem Video wird ein umfassender Leitfaden zur Nutzung des integrierten Wiederholungsmechanismus von Adobe I/O-Ereignissen zur Stärkung der Anwendungs-Ausfallsicherheit vorgestellt. Erfahren Sie, wie es bei bestimmten HTTP-Antwortstatus-Codes erneut zu Trigger-Ereignissen kommt. Adobe I/O Events setzt exponentielle und feste Backoff-Strategien für Neuversuche ein, wobei die Intervalle von einer Minute auf 15 Minuten steigen. In der Dokumentation wird auch beschrieben, wie Wiederholungsindikatoren in der Entwicklerkonsole angezeigt werden, wobei visuelle Hinweise wie Warnsymbole bzw. kreisförmige Pfeile die fehlgeschlagenen bzw. erneut versucht-Ereignisse angeben.

Erfahren Sie, wie der Wiederholungsmechanismus im Kontext der &quot;consumer&quot;-Laufzeitaktionen funktioniert, und bestimmen Sie, ob ein Ereignis erneut versucht wird. Erfolgreiche Antworten werden mit einem Statuscode 200 angezeigt, während Fehlerantworten ein Fehlerobjekt mit dem Attribut &quot;statusCode&quot;enthalten. Die &quot;consumer&quot;-Laufzeitaktion bestimmt den HTTP-Antwort-Code, der basierend auf den nachgelagerten Verarbeitungsergebnissen zurückgegeben wird, wodurch eine effiziente Ereignisverarbeitung und schließlich erfolgreiche Aktivierungen sichergestellt werden.

## Zielgruppe

* Entwickler, die die spezifischen HTTP-Antwortstatus-Codes verstehen möchten, die das Trigger-Ereignis erneut versucht.
* Teams, die über die exponentiellen und fixen Backoff-Strategien erfahren möchten, die von Adobe I/O Events für weitere Versuche eingesetzt werden.
* Entwickler, die verstehen möchten, wie visuelle Indikatoren in der Entwicklerkonsole fehlgeschlagene und wiederholt ausgeführte Ereignisse darstellen.

## Video-Download

* Adobe I/O-Ereignisse verfügen über einen nativen Wiederholungsmechanismus, mit dem Ereignisaktivierungen basierend auf bestimmten HTTP-Antwortstatus-Codes automatisch wiederholt werden.
* Der von Adobe I/O Events implementierte Wiederholungsmechanismus umfasst exponentielle und feste Back-off-Strategien.
* Visuelle Indikatoren in der Entwicklerkonsole, z. B. Warnsymbole für fehlgeschlagene Ereignisse und kreisförmige Pfeilsymbole für Wiederholungsereignisse.
* Die &quot;consumer&quot;-Laufzeitaktionen spielen eine entscheidende Rolle bei der Bestimmung der geeigneten HTTP-Antwortstatus-Codes für die Ereignisverarbeitung.

>[!VIDEO](https://video.tv.adobe.com/v/3431695?learn=on)

{{$include /help/_includes/starter-kit-related-links.md}}

## Verwandte Dokumentation

* [Webhook cannot handle an event](https://developer.adobe.com/events/docs/support/faq/#what-happens-if-my-webhook-is-unable-to-handle-a-specific-event-but-handles-all-other-events-gracefully)
* [Webhook down und markiert als instabil](https://developer.adobe.com/events/docs/support/faq/#what-happens-if-my-webhook-is-down-why-is-my-event-registration-marked-as-unstable)
