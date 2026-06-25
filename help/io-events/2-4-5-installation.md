---
title: Erfahren Sie, wie Sie IO-Ereignisse für Adobe Commerce 2.4.5 installieren
description: Erfahren Sie, wie Sie Module installieren, die für E/A-Ereignisse in Adobe Commerce 2.4.5 zur Verwendung in Adobe Developer App Builder erforderlich sind
landing-page-description: Erfahren Sie, wie Sie mit Composer mehrere für Adobe Commerce 2.4.5 erforderliche Module installieren.
short-description: Erfahren Sie, wie Sie mit Composer mehrere für Adobe Commerce 2.4.5 erforderliche Module installieren.
kt: 11886
doc-type: tutorial
duration: 214
audience: all
last-substantial-update: 2023-02-22T00:00:00.000Z
badge: Adobe Commerce 2.4.5
feature: App Builder, Eventing
topic: Commerce, Architecture
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: e0adfd85-5a3d-44ba-aab5-ecd7c61715cf
TQID: https://experienceleague.adobe.com/vb-q-JXeM4KvkxzfDui1MaTOSBFXDVBwmpTeolUtKGw
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: 456f3cae8c45d137a195456692c2d11204126bb7
workflow-type: tm+mt
source-wordcount: 190
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

>[!VIDEO](https://video.tv.adobe.com/v/3415794?learn=on)

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

