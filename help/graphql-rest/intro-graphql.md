---
title: Einführung in GraphQL
description: Erfahren Sie, wie Sie GraphQL in Adobe Commerce und  [!DNL Magento Open Source]. Verwenden Sie GET- und POST-Aufrufe von GraphQL für Adobe Commerce und  [!DNL Magento Open Source].
short-description: Erfahren Sie, wie Sie GraphQL-GET- und -POST-Aufrufe für Adobe Commerce und  [!DNL Magento Open Source].
kt: 11524
doc-type: video
audience: all
last-substantial-update: 2023-10-12T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 8ea823da-24a3-4627-885c-4b3279b9142c
source-git-commit: b8b1e40a2f4d38954f0d21bc6f1a91b7ec0bd8c9
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# Einführung in GraphQL

Dies ist Teil 1 der Serie für GraphQL und Adobe Commerce. GraphQL hat sich schnell zum Branchenstandard dafür entwickelt, wie leistungsstarke Client-seitige Anwendungen mit einem Backend kommunizieren. Es ist ein zunehmend relevantes Thema für Adobe Commerce-Entwicklerinnen und -Entwickler, da die Plattform ihre Funktionen im Bereich der Headless-Implementierungen weiter erweitert.

Wenn Sie GraphQL noch nicht kennen, finden Sie in diesem Abschnitt grundlegende Konzepte und Verwendungsmöglichkeiten.

>[!VIDEO](https://video.tv.adobe.com/v/3443951?learn=on&captions=ger)

## Verwandte Videos und Tutorials zu GraphQL in dieser Reihe

* [Teil 2: GraphQL - Abfragen](../graphql-rest/graphql-queries.md)
* [Teil 3 GraphQL - Mutationen](../graphql-rest/graphql-mutations.md)
* [Teil 4: GraphQL - Schema](../graphql-rest/graphql-schema.md)

## Was ist GraphQL?

GraphQL ist eine Spezifikation für eine eindeutige API-Abfragesprache und die Laufzeitumgebung, die Daten als Antwort auf diese Abfragesprache bereitstellt.

Herkömmliche Web-APIs wie REST eignen sich gut für die Weitergabe von Daten zwischen unterschiedlichen Systemen, bieten jedoch weniger als eine Spitzenleistung für moderne App-Link-Erlebnisse wie Progressive Webs Application. In Anwendungen wie diesem kommunizieren die Frontend- und Backend-Ebenen _derselben_-Anwendung über die Web-API. Der regulierte Ansatz von Systemen wie REST bietet in diesem Zusammenhang, in dem viele Arten von Daten schnell abgerufen werden müssen, häufig nicht die angemessene Flexibilität.

GraphQL ermöglicht es einem Client, die benötigten Daten _genau_ zu beschreiben. Anstatt mehrere Netzwerkanfragen zum Abrufen mehrerer Datentypen zu erfordern, kann eine einzelne Anfrage nach vielen Typen abfragen. Zudem werden die Antworten schlank gehalten, indem nur die angeforderten Typen und Felder in das Format aufgenommen werden, das die Abfrage intuitiv widerspiegelt.

Die Laufzeit, die die GraphQL-Spezifikation implementiert, kann in jeder Sprache erstellt werden. Adobe Commerce und [!DNL Magento Open Source] verwenden
[graphql-php](https://webonyx.github.io/graphql-php/){target="_blank"} PHP-Implementierung und baut darauf eigene Ebenen auf.

[Vollständige Dokumentation zu GraphQL anzeigen](https://graphql.org/learn){target="_blank"}

## Verwenden eines GraphQL-Clients

Sie benötigen einen GUI GraphQL-Client, um Code-Beispiele und -Tutorials zu testen. Es gibt mehrere Optionen:

* [Altair](https://altairgraphql.dev/){target="_blank"} ist ein exzellenter und voll ausgestatteter Client, der speziell für GraphQL entwickelt wurde. Adobe verwendet Altair in Videoanleitungen.
* Wenn Sie das Desktop-Programm nicht installieren möchten, gibt es auch Altair-Erweiterungen, die direkt in Ihrem Programm ausgeführt werden
  [Chrome](https://chromewebstore.google.com/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja){target="_blank"}, Firefox oder [Edge](https://microsoftedge.microsoft.com/addons/detail/altair-graphql-client/kpggioiimijgcalmnfnalgglgooonopa){target="_blank"}Browser.
* [GraphiQL](https://github.com/graphql/graphiql/tree/main/packages/graphiql){target="_blank"} ist eine Implementierung der GraphQL-IDE von GraphQL Foundation. Dies ist kein installierbares Tool, sondern ein Paket, mit dem Sie die Schnittstelle selbst erstellen können.
* Wenn Sie bereits mit [Postman](https://www.postman.com/){target="_blank"} vertraut sind, bietet diese Funktion anständige Unterstützung für GraphQL-Abfragen, auch wenn sie nicht so umfassend ist wie ein dedizierter GraphQL-Client.

In Ihrem GraphQL-Client sollten Sie Ihre Anfragen an den URL-Pfad senden, der auf Ihrer Adobe Commerce- oder [!DNL Magento Open Source]-Instanz `/graphql` ist. Wenn Sie lieber eine vorhandene Instanz für Ihre Tests verwenden möchten, können Sie die Demo des Venia-Designs verwenden (die Beispielimplementierung von PWA Studio): `https://venia.magento.com/graphql`

{{$include /help/_includes/graphql-rest-related-links.md}}
