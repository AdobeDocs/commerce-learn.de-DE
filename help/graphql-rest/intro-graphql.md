---
title: Einführung in GraphQL
description: Erfahren Sie, wie Sie GraphQL in Adobe Commerce und [!DNL Magento Open Source] verwenden können. Verwenden von GraphQL GET- und POST-Aufrufen für Adobe Commerce und [!DNL Magento Open Source].
short-description: Erfahren Sie, wie Sie GraphQL GET- und POST-Aufrufe für Adobe Commerce und [!DNL Magento Open Source] verwenden können.
kt: 11524
doc-type: video
duration: 286
audience: all
last-substantial-update: 2023-10-12T00:00:00.000Z
feature: GraphQL
topic: Commerce, Architecture, Headless
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 8ea823da-24a3-4627-885c-4b3279b9142c
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 6%
---
# Einführung in GraphQL

Dies ist Teil 1 der Serie für GraphQL und Adobe Commerce. GraphQL hat sich schnell zum Branchenstandard dafür entwickelt, wie leistungsstarke Client-seitige Anwendungen mit einem Backend kommunizieren. Es ist ein zunehmend relevantes Thema für Adobe Commerce-Entwicklerinnen und -Entwickler, da die Plattform ihre Funktionen im Bereich der Headless-Implementierungen weiter erweitert.

Wenn Sie GraphQL noch nicht kennen, finden Sie in diesem Abschnitt grundlegende Konzepte und Verwendungsmöglichkeiten.

>[!VIDEO](https://video.tv.adobe.com/v/3443951?captions=ger&learn=on)

## Verwandte Videos und Tutorials zu GraphQL in dieser Reihe

* [Teil 2: GraphQL - Abfragen](../graphql-rest/graphql-queries.md)
* [Teil 3 GraphQL - Mutationen](../graphql-rest/graphql-mutations.md)
* [Teil 4: GraphQL - Schema](../graphql-rest/graphql-schema.md)

## Was ist GraphQL?

GraphQL ist eine Spezifikation für eine eindeutige API-Abfragesprache und die Laufzeitumgebung, die Daten als Antwort auf diese Abfragesprache bereitstellt.

Herkömmliche Web-APIs wie REST eignen sich gut für die Weitergabe von Daten zwischen unterschiedlichen Systemen, bieten jedoch weniger als eine Spitzenleistung für moderne App-Link-Erlebnisse wie progressive Web-Anwendungen. In Anwendungen wie diesem kommunizieren die Frontend- und Backend-Ebenen _derselben_-Anwendung über die Web-API. Der regulierte Ansatz von Systemen wie REST bietet in diesem Zusammenhang, in dem viele Arten von Daten schnell abgerufen werden müssen, häufig nicht die angemessene Flexibilität.

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
