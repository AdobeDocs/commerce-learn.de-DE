---
title: Installieren der Adobe I/O Runtime-CLI und des API Mesh-Plug-ins
description: Erfahren Sie, wie Sie die Adobe I/O Runtime-Befehlszeilenschnittstelle und das API Mesh-Plug-in installieren, um mit API Mesh für Adobe Developer App Builder zu beginnen.
jira: KT-11801
doc-type: Tutorial
duration: 410
last-substantial-update: 2023-02-08T00:00:00Z
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Developer
level: Beginner
exl-id: 898a0918-0362-4fa4-9204-d770ff1a7e6f
source-git-commit: c73744d503de5023e5c001d0534200522db55b04
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Installieren von Adobe I/O Runtime CLI und Mesh-Plug-in

Bevor Sie mit der Verwendung von API Mesh für Adobe Developer App Builder beginnen, müssen Sie die `aio` CLI und das API Mesh-Plug-in installieren.
Installationsanweisungen und Voraussetzungen finden Sie auf der Seite API-Mesh [Erste Schritte](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/){target="_blank"} .

## Für wen ist dieses Video bestimmt?

* Entwicklerinnen und Entwickler, die neu in API Mesh sind, oder [!DNL Adobe Commerce] mit begrenzter Erfahrung mit [Adobe I/O Runtime](https://developer.adobe.com/app-builder/docs/intro_and_overview/what-is-app-builder){target="_blank"} und API Mesh.

## Videoinhalt

* Einführung in API-Mesh
* Installieren der Adobe I/O Runtime-CLI (Befehlszeilenschnittstelle)
* Installieren des API Mesh-Plug-ins

>[!VIDEO](https://video.tv.adobe.com/v/3430771?captions=ger&learn=on)

## Installieren der `aio` CLI und des API Mesh-Plug-ins

Um die `aio` CLI zu installieren, führen Sie nach der Installation von `node` und `npm` den folgenden Befehl aus:

```bash
npm install -g @adobe/aio-cli
```

Sobald die Adobe I/O Runtime-CLI installiert ist, verwenden Sie den folgenden Befehl, um das API Mesh-Plug-in zu installieren:

```bash
aio plugins:install @adobe/aio-cli-plugin-api-mesh
```

{{$include /help/_includes/api-mesh-related-links.md}}
