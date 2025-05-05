---
title: Installieren der Adobe I/O Runtime-Befehlszeilenschnittstelle und des API Mesh-Plug-ins
description: Erfahren Sie, wie Sie die Adobe I/O Runtime-Befehlszeilenschnittstelle und das API Mesh-Plug-in installieren
landing-page-description: Erfahren Sie, wie Sie Adobe App Builder verwenden und das Plug-in "Adobe I/O Runtime with API Mesh“ installieren.
short-description: Erfahren Sie, wie Sie Adobe App Builder verwenden und das Plug-in "Adobe I/O Runtime with API Mesh“ installieren.
kt: 11801
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 898a0918-0362-4fa4-9204-d770ff1a7e6f
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Installieren von Adobe I/O Runtime CLI und Mesh-Plug-in

Bevor Sie mit der Verwendung von API Mesh für Adobe Developer App Builder beginnen, müssen Sie die `aio` CLI und das API Mesh-Plug-in installieren.
Installationsanweisungen und Voraussetzungen finden Sie auf der Seite API-Mesh [Erste Schritte](https://developer.adobe.com/graphql-mesh-gateway/gateway/getting-started/){target="_blank"} .

## Für wen ist dieses Video bestimmt?

* Entwicklerinnen und Entwickler, die neu in API Mesh sind, oder [!DNL Adobe Commerce] mit begrenzter Erfahrung mit [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/guides/overview/){target="_blank"} und API Mesh.

## Videoinhalt

* Einführung in API-Mesh
* Installieren der Adobe I/O Runtime-CLI (Befehlszeilenschnittstelle)
* Installieren des API Mesh-Plug-ins

>[!VIDEO](https://video.tv.adobe.com/v/3430771?quality=12&learn=on&captions=ger)

## Installieren der `aio` CLI und des API Mesh-Plug-ins

Führen Sie nach der Installation von `node` und `npm` den folgenden Befehl aus, um die `aio` CLI zu installieren:

```bash
npm install -g @adobe/aio-cli
```

Sobald die Adobe I/O Runtime-CLI installiert ist, verwenden Sie den folgenden Befehl, um das API Mesh-Plug-in zu installieren:

```bash
aio plugins:install @adobe/aio-cli-plugin-api-mesh
```

{{$include /help/_includes/api-mesh-related-links.md}}
