---
title: Erfahren Sie, wie Sie IO-Ereignisse für Adobe Commerce 2.4.5 installieren
description: Erfahren Sie, wie Sie Module installieren, die für E/A-Ereignisse in Adobe Commerce 2.4.5 zur Verwendung in Adobe Developer App Builder erforderlich sind
landing-page-description: Erfahren Sie, wie Sie mit Composer mehrere für Adobe Commerce 2.4.5 erforderliche Module installieren.
short-description: Erfahren Sie, wie Sie mit Composer mehrere für Adobe Commerce 2.4.5 erforderliche Module installieren.
kt: 11886
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-22T00:00:00Z
badge: Adobe Commerce 2.4.5
feature: App Builder, Eventing
topic: Commerce, Architecture
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: e0adfd85-5a3d-44ba-aab5-ecd7c61715cf
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Installation von Adobe Commerce 2.4.5

Erfahren Sie, wie Sie mit Composer für Version 2.4.5 mehrere neue Module in Adobe Commerce installieren. Dadurch werden die erforderlichen Module für die Verwendung in der Adobe Commerce-Anwendung eingerichtet. Weitere Dokumentationen finden Sie unter [Installieren von Adobe I/O Events für Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Für wen ist dieses Video bestimmt?

* Entwickler, die noch nicht mit Adobe Commerce und Adobe Developer App Builder vertraut sind und I/O Events verwenden

## Videoinhalt {#video-content}

* Installation erforderlicher Module mit dem Composer
* Befehle, die für das On-Premise-Hosting ausgeführt werden
* Für Adobe Commerce Cloud auszuführende Befehle
* Adobe Commerce Cloud-YAML - erforderliche Bearbeitung

>[!VIDEO](https://video.tv.adobe.com/v/3415794?quality=12&learn=on)

## Nützliche Befehle {#useful-commands}

Es gibt verschiedene Befehle, die sich geringfügig unterscheiden, je nachdem, ob Sie sich in einer selbst gehosteten Umgebung befinden oder Adobe Commerce Cloud verwenden.

### On-Premise Hosting {#on-premise}

```bash
composer require magento/commerce-eventing=^1.0 --no-update

composer update

bin/magento events:generate:module

bin/magento module:enable --all

bin/magento setup:upgrade && bin/magento setup:di:compile
```

### Adobe Commerce in Cloud Manager {#adobe-commerce-cloud}

```bash
composer require magento/commerce-eventing=^1.0 --no-update

composer update

composer info magento/ece-tools
```

Commerce Cloud `.magento.env.yaml`:

```yaml
stage:
  global:
    ENABLE_EVENTING: true
```

{{$include /help/_includes/io-events-related-links.md}}
