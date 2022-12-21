---
title: Einführung in GraphQL
description: Erfahren Sie, wie Sie GraphQL in Adobe Commerce verwenden und [!DNL Magento Open Source]. Verwenden von GraphQL-GET- und POST-Aufrufen für Adobe Commerce und [!DNL Magento Open Source].
landing-page-description: Erfahren Sie, wie Sie GraphQL in Adobe Commerce verwenden und [!DNL Magento Open Source]. Verwenden von GraphQL-GET- und POST-Aufrufen für Adobe Commerce und [!DNL Magento Open Source].
kt: 11524
doc-type: tutorial
audience: all
last-substantial-update: 2022-12-13T00:00:00Z
source-git-commit: 9dc530107470617f88992d8eb2ed9feb017a6530
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Einführung in GraphQL

GraphQL ist schnell zum Branchenstandard geworden, der zeigt, wie leistungsstarke clientseitige Anwendungen mit einem Backend kommunizieren. Es ist ein zunehmend relevantes Thema für Adobe Commerce-Entwickler, da die Plattform ihre Funktionen im Bereich Headless-Implementierungen weiter ausbaut.

Wenn Sie mit GraphQL noch nicht vertraut sind, werden Sie in diesem Abschnitt auf die grundlegenden Konzepte und Verwendungsmöglichkeiten hingewiesen.

## Was ist GraphQL?

GraphQL ist eine Spezifikation für eine eindeutige API-Abfragesprache und die Laufzeitumgebung, die Daten als Reaktion auf diese Abfragesprache bereitstellt.

Herkömmliche Web-APIs wie REST haben bei unterschiedlichen Systemen, die Daten hin und her weiterleiten, zwar gute Dienste geleistet, aber für moderne App-Link-Erlebnisse wie Progressive Web Application weniger als Spitzenleistungen erbracht. In solchen Anwendungen sind die Front-End- und Back-End-Ebenen der _same_ Anwendungs-Kommunikation über Web-API. Der reglementierte Ansatz von Systemen wie REST bietet in diesem Zusammenhang, wo viele Arten von Daten schnell abgerufen werden müssen, oft nicht die passende Flexibilität.

GraphQL ermöglicht es einem Client, _just_ die benötigten Daten. Anstatt mehrere Netzwerkanforderungen zum Abrufen mehrerer Datentypen zu erfordern, kann eine einzelne Anfrage für viele Typen abgefragt werden. Außerdem werden Antworten schlank gehalten, indem nur die Typen und Felder aufgenommen werden, die angefordert werden (in einem Format, das die Abfrage intuitiv spiegelt).

Die Laufzeitumgebung, die die GraphQL-Spezifikation implementiert, kann in jeder beliebigen Sprache erstellt werden. Adobe Commerce und [!DNL Magento Open Source] die
[graphql-php](https://webonyx.github.io/graphql-php/) PHP-Implementierung und erstellt eigene Ebenen darauf.

[Vollständige Dokumentation zu GraphQL anzeigen](https://graphql.org/learn)

## Verwenden eines GraphQL-Clients

Sie benötigen einen GUI GraphQL-Client, um Codebeispiele und -Tutorials zu testen. Es gibt mehrere Optionen:

* [Altair](https://altairgraphql.dev/) ist ein hervorragender Client mit vollem Funktionsumfang, der speziell für GraphQL entwickelt wurde. Adobe verwendet Altair in Videos.
* Wenn Sie das Desktop-Programm nicht installieren möchten, gibt es auch Altair-Erweiterungen, die direkt in Ihrer
   [Chrome](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja), Firefox oder [Edge](https://microsoftedge.microsoft.com/addons/detail/altair-graphql-client/kpggioiimijgcalmnfnalgglgooonopa) Browser.
* [GraphiQL](https://github.com/graphql/graphiql/tree/main/packages/graphiql) ist eine Implementierung der GraphQL IDE von der GraphQL Foundation. Dies ist kein installierbares Tool, sondern ein Paket, mit dem Sie die Oberfläche selbst erstellen können.
* Wenn Sie bereits mit [Postman](https://www.postman.com/), bietet sie eine angemessene Unterstützung für GraphQL-Abfragen, obwohl sie nicht so umfassend wie ein dedizierter GraphQL-Client unterstützt wird.

In Ihrem GraphQL-Client sollten Sie Ihre Anforderungen an den URL-Pfad senden `/graphql` auf Ihrer Adobe Commerce oder [!DNL Magento Open Source] -Instanz. Wenn Sie es vorziehen, eine vorhandene Instanz für Ihre Tests zu verwenden, können Sie die Demo des Venia-Designs (die Beispielimplementierung von PWA Studio) verwenden: `https://venia.magento.com/graphql`

