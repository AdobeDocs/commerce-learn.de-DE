---
title: Einführung in GraphQL
description: Erfahren Sie, wie Sie GraphQL in Adobe Commerce und  [!DNL Magento Open Source] verwenden. Verwenden Sie GraphQL-GET- und POST-Aufrufe für Adobe Commerce und  [!DNL Magento Open Source].
short-description: Erfahren Sie, wie Sie GraphQL-GET- und POST-Aufrufe für Adobe Commerce und  [!DNL Magento Open Source] verwenden.
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

Dies ist Teil 1 der Reihe für GraphQL und Adobe Commerce. GraphQL ist schnell zum Branchenstandard geworden, der zeigt, wie leistungsstarke clientseitige Anwendungen mit einem Backend kommunizieren. Es ist ein zunehmend relevantes Thema für Adobe Commerce-Entwickler, da die Plattform ihre Funktionen im Bereich Headless-Implementierungen weiter ausbaut.

Wenn Sie mit GraphQL noch nicht vertraut sind, werden Sie in diesem Abschnitt auf die grundlegenden Konzepte und Verwendungsmöglichkeiten hingewiesen.

>[!VIDEO](https://video.tv.adobe.com/v/3424117?learn=on)

## Verwandte Videos und Tutorials zu GraphQL in dieser Reihe

* [Teil 2 GraphQL - Abfragen](../graphql-rest/graphql-queries.md)
* [Teil 3 GraphQL - Mutationen](../graphql-rest/graphql-mutations.md)
* [Teil 4 GraphQL - Schema](../graphql-rest/graphql-schema.md)

## Was ist GraphQL?

GraphQL ist eine Spezifikation für eine eindeutige API-Abfragesprache und die Laufzeitumgebung, die Daten als Reaktion auf diese Abfragesprache bereitstellt.

Herkömmliche Web-APIs wie REST haben bei unterschiedlichen Systemen, die Daten hin und her weiterleiten, zwar gute Dienste geleistet, aber für moderne App-Link-Erlebnisse wie Progressive Webs Application weniger als Spitzenleistungen erbracht. In solchen Anwendungen kommunizieren die Frontend- und Backend-Ebenen der Anwendung _Dasselbe_ über die Web-API. Der reglementierte Ansatz von Schemas wie REST bietet in diesem Zusammenhang, wo viele Arten von Daten schnell abgerufen werden müssen, oft nicht die passende Flexibilität.

Mit GraphQL kann ein Client _genau_ die benötigten Daten ausdrücken. Anstatt mehrere Netzwerkanforderungen zum Abrufen mehrerer Datentypen zu erfordern, kann eine einzelne Anfrage für viele Typen abgefragt werden. Außerdem werden Antworten schlank gehalten, indem nur die Typen und Felder aufgenommen werden, die angefordert werden (in einem Format, das die Abfrage intuitiv spiegelt).

Die Laufzeitumgebung, die die GraphQL-Spezifikation implementiert, kann in jeder beliebigen Sprache erstellt werden. Adobe Commerce und [!DNL Magento Open Source] verwenden die
[graphql-php](https://webonyx.github.io/graphql-php/){target="_blank"} PHP-Implementierung und erstellt eigene Ebenen darauf.

[ Vollständige GraphQL-Dokumentation anzeigen](https://graphql.org/learn){target="_blank"}

## Verwenden eines GraphQL-Clients

Sie benötigen einen GUI GraphQL-Client, um Codebeispiele und -Tutorials zu testen. Es gibt mehrere Optionen:

* [Altair](https://altairgraphql.dev/){target="_blank"} ist ein hervorragender Client mit vollem Funktionsumfang, der speziell für GraphQL entwickelt wurde. Adobe verwendet Altair in Video-Clips.
* Wenn Sie das Desktop-Programm nicht installieren möchten, gibt es auch Altair-Erweiterungen, die direkt in Ihrer
  Der Browser [Chrome](https://chromewebstore.google.com/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja){target="_blank"}, Firefox oder [Edge](https://microsoftedge.microsoft.com/addons/detail/altair-graphql-client/kpggioiimijgcalmnfnalgglgooonopa){target="_blank"}.
* [GraphiQL](https://github.com/graphql/graphiql/tree/main/packages/graphiql){target="_blank"} ist eine Implementierung der GraphQL IDE von der GraphQL Foundation. Dies ist kein installierbares Tool, sondern ein Paket, mit dem Sie die Oberfläche selbst erstellen können.
* Wenn Sie bereits mit [Postman](https://www.postman.com/){target="_blank"} vertraut sind, werden GraphQL-Abfragen zwar angemessen unterstützt, aber nicht so vollständig wie ein dedizierter GraphQL-Client.

In Ihrem GraphQL-Client sollten Sie Ihre Anforderungen an den URL-Pfad `/graphql` in Ihrer Adobe Commerce- oder [!DNL Magento Open Source]-Instanz senden. Wenn Sie es vorziehen, eine vorhandene Instanz für Ihre Tests zu verwenden, können Sie die Demo des Venia-Designs (die Beispielimplementierung des PWA Studios) verwenden: `https://venia.magento.com/graphql`

{{$include /help/_includes/graphql-rest-related-links.md}}
