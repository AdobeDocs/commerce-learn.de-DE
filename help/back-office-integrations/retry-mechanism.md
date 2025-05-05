---
title: Verwenden der nativen Funktionalität eines Wiederholungsmechanismus
description: Nutzen Sie den Wiederholungsmechanismus von Adobe I/O Events für robuste Anwendungen, einschließlich Wiederholungsbedingungen und visueller Indikatoren.
landing-page-description: Machen Sie sich mit dem integrierten Wiederholungsmechanismus von Adobe I/O Events vertraut und nutzen Sie ihn, um die Anwendungsresilienz zu verbessern und Ereignisaktivierungen effektiv zu verwalten.
kt: 15872
doc-type: video
duration: 314
audience: all
last-substantial-update: 2024-7-31
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Architect, Developer
level: Intermediate
exl-id: 412060b3-76ae-4c27-bf96-8eb2a0f0d0e8
source-git-commit: c2a6ea2267f8ce8efebcbda06d6e55cb93afcf84
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# Nutzung des Wiederholungsmechanismus für Adobe I/O-Ereignisse zur Verbesserung der Anwendungsresilienz

In diesem Video wird eine umfassende Anleitung zur Nutzung des integrierten Wiederholungsmechanismus von Adobe I/O-Ereignissen zur Verbesserung der Anwendungsresilienz beschrieben. Erfahren Sie, wie bestimmte HTTP-Antwortstatus-Trigger weitere Zustellversuche codieren. Adobe I/O Events nutzt exponentielle und feste Back-off-Strategien für weitere Zustellversuche, wobei die Intervalle von einer Minute auf 15 Minuten zunehmen. In der Dokumentation wird auch beschrieben, wie Wiederholungsindikatoren in der Entwicklerkonsole angezeigt werden. Visuelle Hinweise wie Warnsymbole und Kreispfeile zeigen fehlgeschlagene bzw. wiederholte Ereignisse an.

Erfahren Sie, wie der Wiederholungsmechanismus im Kontext der Laufzeitaktionen des „Verbrauchers“ funktioniert, und stellen Sie fest, ob ein Ereignis erneut versucht wird. Erfolgreiche Antworten werden mit dem Status-Code 200 angezeigt, während Fehlerantworten ein Fehlerobjekt mit dem Attribut „statusCode“ enthalten. Die Laufzeitaktion „Verbraucher“ bestimmt den HTTP-Antwort-Code, der basierend auf nachgelagerten Verarbeitungsergebnissen zurückgegeben werden soll, und stellt so eine effiziente Ereignisbehandlung und letztendlich erfolgreiche Aktivierungen sicher.

## Zielgruppe

* Entwickler, die die spezifischen HTTP-Antwort-Status-Codes verstehen möchten, die von einem Trigger-Ereignis erneut versucht werden.
* Teams, die mehr über die exponentiellen und festen Back-off-Strategien von Adobe I/O Events für weitere Zustellversuche erfahren möchten.
* Entwicklerinnen und Entwickler, die verstehen möchten, wie visuelle Indikatoren in der Entwicklerkonsole Ereignisse mit Fehlern und erneuten Zustellversuchen darstellen.

## Videoinhalt

* Adobe I/O-Ereignisse verfügen über einen nativen Wiederholungsmechanismus, der Ereignisaktivierungen basierend auf bestimmten HTTP-Antwort-Status-Codes automatisch wiederholt.
* Der von Adobe I/O Events implementierte Wiederholungsmechanismus umfasst exponentielle und feste Back-off-Strategien.
* Visuelle Indikatoren in der Entwicklerkonsole, z. B. Warnsymbole für fehlgeschlagene Ereignisse und Zirkularpfeilsymbole für erneut versuchte Ereignisse.
* Die Laufzeitaktionen „Consumer“ spielen eine entscheidende Rolle bei der Bestimmung der geeigneten HTTP-Antwort-Status-Codes für die Ereignisbehandlung.

>[!VIDEO](https://video.tv.adobe.com/v/3449082?learn=on&captions=ger)

{{$include /help/_includes/starter-kit-related-links.md}}

## Verwandte Dokumentation

* [Webhook kann ein Ereignis nicht verarbeiten](https://developer.adobe.com/events/docs/support/faq/#what-happens-if-my-webhook-is-unable-to-handle-a-specific-event-but-handles-all-other-events-gracefully)
* [Webhook heruntergefahren und als instabil markiert](https://developer.adobe.com/events/docs/support/faq/#what-happens-if-my-webhook-is-down-why-is-my-event-registration-marked-as-unstable)
