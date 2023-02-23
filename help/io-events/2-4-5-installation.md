---
title: Erfahren Sie, wie Sie IO-Ereignisse für Adobe Commerce 2.4.5 installieren.
description: Erfahren Sie, wie Sie Module installieren, die für IO-Ereignisse in Adobe Commerce 2.4.5 zur Verwendung in Adobe Developer App Builder erforderlich sind
landing-page-description: Erfahren Sie, wie Sie mehrere für Adobe Commerce 2.4.5 erforderliche Module mithilfe von Composer installieren.
kt: 11886
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-22T00:00:00Z
badge: "Adobe Commerce 2.4.5"
source-git-commit: e5fe4d5408b12426f9925c6213bd0cc73b4089b6
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Installation von Adobe Commerce 2.4.5

Erfahren Sie, wie Sie mehrere neue Module in Adobe Commerce mit Composer für Version 2.4.5 installieren. Dadurch werden die erforderlichen Module für die Verwendung in der Adobe Commerce-Anwendung eingerichtet. Weitere Informationen finden Sie unter [Installieren von Adobe I/O-Ereignissen für Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Für wen ist dieses Video?

* Neue Entwickler für Adobe Commerce und Adobe Developer App Builder mit I/O-Ereignissen

## Videoinhalt {#video-content}

* Installation erforderlicher Module mit Composer
* Befehle für On-Premise-Hosting
* Für Adobe Commerce Cloud auszuführende Befehle
* Adobe Commerce Cloud-YAML-Bearbeitung erforderlich

>[!VIDEO](https://video.tv.adobe.com/v/3415794)

## Nützliche Befehle {#useful-commands}

Es gibt verschiedene Befehle, die sich geringfügig unterscheiden, je nachdem, ob Sie sich in einer selbstverwalteten Umgebung befinden oder Adobe Commerce Cloud verwenden.

### Hosting vor Ort {#on-premise}

```bash
composer require magento/commerce-eventing=^1.0 --no-update

composer update

bin/magento events:generate:module

bin/magento module:enable --all

bin/magento setup:upgrade && bin/magento setup:di:compile
```

### Adobe Commerce on Cloud {#adobe-commerce-cloud}

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