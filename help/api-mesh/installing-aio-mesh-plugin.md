---
title: Installieren der Befehlszeilenschnittstelle von Adobe I/O Runtime und des API-Mesh-Plug-ins
description: Erfahren Sie, wie Sie die Befehlszeilenschnittstelle von Adobe I/O Runtime und das API-Mesh-Plug-in installieren.
landing-page-description: Erfahren Sie, wie Sie Adobe App Builder verwenden und Adobe I/O Runtime mit API-Mesh-Plug-in installieren.
kt: 11801
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
source-git-commit: a6fb3810f34246df73ae5557240eaaa0f4407eb1
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---


# Installieren des Adobe I/O Runtime-CLI- und Mesh-Plug-ins

Bevor Sie mit der Verwendung von API Measurement für Adobe Developer App Builder beginnen, müssen Sie die `aio` CLI und das API-Mesh-Plug-in.
Installationsanweisungen und -voraussetzungen finden Sie im API-Handbuch [Erste Schritte](https://developer.adobe.com/graphql-mesh-gateway/gateway/getting-started/) Seite.

## Für wen ist dieses Video?

* Entwickler, die neu im API-Mesh sind oder [!DNL Adobe Commerce] eingeschränkte Erfahrung mit [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/guides/overview/) und API-Mesh.

## Videoinhalt

* Einführung in das API-Mesh
* Installieren der Adobe I/O Runtime-CLI (Befehlszeilenschnittstelle)
* Installieren des API-Mesh-Plug-ins

>[!VIDEO](https://video.tv.adobe.com/v/3414122/)

## Installieren der `aio` CLI und API-Mesh-Plug-in

Nach der Installation `node` und `npm`Führen Sie den folgenden Befehl aus, um den `aio` CLI:

```bash
npm install -g @adobe/aio-cli
```

Nachdem die Adobe I/O Runtime-CLI installiert wurde, verwenden Sie den folgenden Befehl, um das API-Mesh-Plug-in zu installieren:

```bash
aio plugins:install @adobe/aio-cli-plugin-api-mesh
```

{{$include /help/_includes/api-mesh-related-links.md}}
