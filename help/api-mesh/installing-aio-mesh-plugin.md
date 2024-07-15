---
title: Installieren der Befehlszeilenschnittstelle von Adobe I/O Runtime und des API-Mesh-Plug-ins
description: Erfahren Sie, wie Sie die Befehlszeilenschnittstelle von Adobe I/O Runtime und das API-Mesh-Plug-in installieren.
landing-page-description: Erfahren Sie, wie Sie Adobe App Builder verwenden und Adobe I/O Runtime mit API-Mesh-Plug-in installieren.
short-description: Erfahren Sie, wie Sie Adobe App Builder verwenden und Adobe I/O Runtime mit API-Mesh-Plug-in installieren.
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

# Installieren des Adobe I/O Runtime-CLI- und Mesh-Plug-ins

Bevor Sie mit der Verwendung von API Measurement für Adobe Developer App Builder beginnen, müssen Sie die `aio`-CLI und das API-Mesh-Plug-in installieren.
Installationsanweisungen und -voraussetzungen finden Sie auf der Seite API-Mesh [Erste Schritte](https://developer.adobe.com/graphql-mesh-gateway/gateway/getting-started/){target="_blank"} .

## Für wen ist dieses Video?

* Entwickler, die neu im API-Mesh sind oder [!DNL Adobe Commerce] mit eingeschränktem Erlebnis mit [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/guides/overview/){target="_blank"} und API-Mesh arbeiten.

## Videoinhalt

* Einführung in das API-Mesh
* Installieren der Adobe I/O Runtime-CLI (Befehlszeilenschnittstelle)
* Installieren des API-Mesh-Plug-ins

>[!VIDEO](https://video.tv.adobe.com/v/3414122?quality=12&learn=on)

## Installieren des Plug-ins `aio` CLI und API-Mesh

Führen Sie nach der Installation von `node` und `npm` den folgenden Befehl aus, um die `aio`-CLI zu installieren:

```bash
npm install -g @adobe/aio-cli
```

Nachdem die Adobe I/O Runtime-CLI installiert wurde, verwenden Sie den folgenden Befehl, um das API-Mesh-Plug-in zu installieren:

```bash
aio plugins:install @adobe/aio-cli-plugin-api-mesh
```

{{$include /help/_includes/api-mesh-related-links.md}}
