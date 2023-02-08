---
title: Installieren der Adobe Developer I/O-Befehlszeilenschnittstelle und des API-Mesh-Plug-ins
description: Erfahren Sie, wie Sie die Befehlszeilenschnittstelle von Adobe Developer IO und das API-Mesh-Plug-in installieren.
landing-page-description: Erfahren Sie, wie Sie Adobe App Builder verwenden und das Adobe Developer I/O mit API-Mesh-Plug-in installieren.
kt: 11801
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
source-git-commit: b6d501c5c852e1cc2cf1f05f91b5a9d96ac7d036
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Installieren des Adobe Developer IO- und Mesh-Plug-ins

Bevor Sie beginnen, müssen einige Dinge eingerichtet werden. Zunächst die Einrichtung der Adobe Developer I/O-Befehlszeilenschnittstelle. Stellen Sie als Nächstes sicher, dass das API-Mesh-Plug-in in jeder Umgebung konfiguriert ist.
Anweisungen zum Einrichten Ihrer lokalen Umgebung für die Ausführung von Knoten, nvm und zum Installieren der Adobe Developer I/O finden Sie unter [GraphQL Messaging - Erste Schritte](https://developer.adobe.com/graphql-mesh-gateway/gateway/getting-started/).

## Für wen ist dieses Video?

* Entwickler, die mit Adobe App Builder oder [!DNL Magento Open Source] mit eingeschränkter Erfahrung mit Adobe Developer I/O und API-Mesh.

## Videoinhalt

* Einführung in das API-Mesh
* Installieren der Befehlszeilenschnittstelle von Adobe Developer IO
* Hinzufügen des API-Mesh-Plug-ins zur AIO-Befehlszeile

>[!VIDEO](https://video.tv.adobe.com/v/3414122/)

## Beispielbefehle mit NPM und AIO

Die Installation der Befehlszeilenschnittstelle von Adobe Developer ist recht einfach. Führen Sie nach der Installation von Node diesen Befehl aus `npm install -g @adobe/aio-cli`
Nachdem die Adobe Developer-CLI installiert wurde, kann das Mesh-Plugin installiert werden. Führen Sie dazu diesen Befehl aus `aio plugins:install @adobe/aio-cli-plugin-api-mesh`

{{$include /help/_includes/api-mesh-related-links.md}}
