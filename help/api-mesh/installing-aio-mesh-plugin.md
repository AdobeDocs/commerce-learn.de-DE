---
title: Installieren der Befehlszeilenschnittstelle von Adobe I/O Runtime und des API-Mesh-Plug-ins
description: Erfahren Sie, wie Sie die Befehlszeilenschnittstelle von Adobe I/O Runtime und das API-Mesh-Plug-in installieren.
landing-page-description: Erfahren Sie, wie Sie Adobe App Builder verwenden und Adobe I/O Runtime mit API-Mesh-Plug-in installieren.
short-description: Erfahren Sie, wie Sie Adobe App Builder verwenden und Adobe I/O Runtime mit API-Mesh-Plug-in installieren.
kt: 11801
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
exl-id: 898a0918-0362-4fa4-9204-d770ff1a7e6f
source-git-commit: edb98cf6544954d741c43beb39f4056326c7d26b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Installieren des Adobe I/O Runtime-CLI- und Mesh-Plug-ins

Bevor Sie mit der Verwendung von API Measurement für Adobe Developer App Builder beginnen, müssen Sie die `aio` CLI und das API-Mesh-Plug-in.
Installationsanweisungen und -voraussetzungen finden Sie im API-Handbuch [Erste Schritte](https://developer.adobe.com/graphql-mesh-gateway/gateway/getting-started/){target="_blank"} Seite.

## Für wen ist dieses Video?

* Entwickler, die neu im API-Mesh sind oder [!DNL Adobe Commerce] eingeschränkte Erfahrung mit [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/guides/overview/){target="_blank"} und API-Mesh.

## Videoinhalt

* Einführung in das API-Mesh
* Installieren der Adobe I/O Runtime-CLI (Befehlszeilenschnittstelle)
* Installieren des API-Mesh-Plug-ins

>[!VIDEO](https://video.tv.adobe.com/v/3414122?quality=12&learn=on)

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
