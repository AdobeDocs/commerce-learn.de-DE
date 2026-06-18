---
title: Verwenden der nativen Funktionalität eines Wiederholungsmechanismus
description: Erfahren Sie, wie Sie mit dem Wiederholungsmechanismus von Adobe I/O Events widerstandsfähige Programme erstellen können, die Wiederholungsbedingungen, Back-off-Strategien und visuelle Indikatoren abdecken.
doc-type: Technical Video
duration: 402
last-substantial-update: 2024-07-31
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Developer
level: Intermediate
jira: KT-15872
exl-id: 412060b3-76ae-4c27-bf96-8eb2a0f0d0e8
TQID: https://experienceleague.adobe.com/hrzcmSY8cAke4LBLRtqfkP8-t6jP4KMoMc7iL3WPRng
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: 9568f37b026d0e659e8092282cb923c7ecde58ac
workflow-type: tm+mt
source-wordcount: 382
ht-degree: 0%

---

# Verwenden des Adobe I/O Events-Wiederholungsmechanismus für eine robuste Anwendung

In diesem Video wird eine umfassende Anleitung zur Nutzung des integrierten Wiederholungsmechanismus von Adobe I/O Events zur Verbesserung der Ausfallsicherheit von Programmen beschrieben. Erfahren Sie, wie bestimmte HTTP-Antwortstatus-Trigger weitere Zustellversuche codieren. Adobe I/O Events verwendet exponentielle und feste Back-off-Strategien für weitere Zustellversuche, wobei die Intervalle von einer Minute auf 15 Minuten zunehmen. In der Dokumentation wird auch beschrieben, wie Wiederholungsindikatoren in der Entwicklerkonsole angezeigt werden. Visuelle Hinweise wie Warnsymbole und Kreispfeile zeigen fehlgeschlagene bzw. wiederholte Ereignisse an.

Erfahren Sie, wie der Wiederholungsmechanismus im Kontext der Laufzeitaktionen des „Verbrauchers“ funktioniert, und stellen Sie fest, ob ein Ereignis erneut versucht wird. Erfolgreiche Antworten werden mit dem Status-Code 200 angezeigt, während Fehlerantworten ein Fehlerobjekt mit dem Attribut „statusCode“ enthalten. Die Laufzeitaktion „Verbraucher“ bestimmt den HTTP-Antwort-Code, der basierend auf nachgelagerten Verarbeitungsergebnissen zurückgegeben werden soll, und stellt so eine effiziente Ereignisbehandlung und letztendlich erfolgreiche Aktivierungen sicher.

## Zielgruppe

* Entwickler, die die spezifischen HTTP-Antwort-Status-Codes verstehen möchten, die von einem Trigger-Ereignis erneut versucht werden.
* Teams, die mehr über die exponentiellen und festen Back-off-Strategien von Adobe I/O Events für weitere Zustellversuche erfahren möchten.
* Entwicklerinnen und Entwickler, die verstehen möchten, wie visuelle Indikatoren in der Entwicklerkonsole Ereignisse mit Fehlern und erneuten Zustellversuchen darstellen.

## Videoinhalt

* Adobe I/O Events verfügt über einen nativen Wiederholungsmechanismus, der Ereignisaktivierungen basierend auf bestimmten HTTP-Antwort-Status-Codes automatisch wiederholt.
* Der von Adobe I/O Events implementierte Wiederholungsmechanismus umfasst exponentielle und feste Back-off-Strategien.
* Visuelle Indikatoren in der Entwicklerkonsole, z. B. Warnsymbole für fehlgeschlagene Ereignisse und Zirkularpfeilsymbole für erneut versuchte Ereignisse.
* Die Laufzeitaktionen „Consumer“ spielen eine entscheidende Rolle bei der Bestimmung der geeigneten HTTP-Antwort-Status-Codes für die Ereignisbehandlung.

>[!VIDEO](https://video.tv.adobe.com/v/3431695?learn=on)

{{$include /help/_includes/starter-kit-related-links.md}}

## Verwandte Dokumentation

* [Webhook kann ein Ereignis nicht verarbeiten](https://developer.adobe.com/events/docs/support/faq/#what-happens-if-my-webhook-is-unable-to-handle-a-specific-event-but-handles-all-other-events-gracefully)
* [Webhook heruntergefahren und als instabil markiert](https://developer.adobe.com/events/docs/support/faq/#what-happens-if-my-webhook-is-down-why-is-my-event-registration-marked-as-unstable)
