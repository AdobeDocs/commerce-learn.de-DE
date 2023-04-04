---
title: Erfahren Sie, wie Sie IO-Ereignisse für Adobe Commerce 2.4.6 installieren.
description: Erfahren Sie, wie Sie Module installieren, die für IO-Ereignisse in Adobe Commerce 2.4.6 zur Verwendung in Adobe Developer App Builder erforderlich sind
landing-page-description: Erfahren Sie, wie Sie mehrere Module installieren, die für Adobe Commerce 2.4.6 erforderlich sind.
short-description: Learn how to install several modules needed for Adobe Commerce 2.4.6.
kt: 11887
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-22T00:00:00Z
badge: "Adobe Commerce 2.4.6"
source-git-commit: d85426bcf3ae0412a433414d70c874964905dda0
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Installation von Adobe Commerce 2.4.6

Erfahren Sie, wie Sie mehrere neue Module in Adobe Commerce mithilfe von Composer für Version 2.4.6 installieren. Weitere Dokumentationen finden Sie unter [Installieren von Adobe I/O-Ereignissen für Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Für wen ist dieses Video?

* Entwickler, die mit Adobe Commerce und Adobe Developer App Builder über I/O-Ereignisse neu sind.

## Videoinhalt {#video-content}

* Befehle für On-Premise-Hosting
* Für Adobe Commerce Cloud auszuführende Befehle
* Adobe Commerce Cloud-YAML-Bearbeitung erforderlich

>[!VIDEO](https://video.tv.adobe.com/v/3415795?quality=12&learn=on)

## Nützliche Befehle {#useful-commands}

Es gibt verschiedene Befehle, die sich geringfügig unterscheiden, je nachdem, ob Sie sich in einer selbstverwalteten Umgebung befinden oder Adobe Commerce Cloud verwenden.

### Hosting vor Ort {#on-premise}

```bash
bin/magento events:generate:module

bin/magento module:enable --all

bin/magento setup:upgrade && bin/magento setup:di:compile
```

### Adobe Commerce on Cloud {#adobe-commerce-cloud}

```bash
composer info magento/ece-tools
```

Commerce Cloud `.magento.env.yaml`:

```yaml
stage:
  global:
    ENABLE_EVENTING: true
```

{{$include /help/_includes/io-events-related-links.md}}
