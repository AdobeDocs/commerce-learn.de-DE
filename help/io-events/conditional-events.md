---
title: Erfahren Sie, wie Sie bedingte Ereignisse in Adobe Commerce verwenden
description: Erfahren Sie, wie Sie bedingte Ereignisse zur Verwendung in Adobe Developer App Builder verwenden.
landing-page-description: Erfahren Sie, wie Sie bedingte Adobe Commerce-Ereignisse verwenden.
short-description: Erfahren Sie, wie Sie bedingte Adobe Commerce-Ereignisse verwenden.
kt: 11890
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-21T00:00:00Z
feature: App Builder, Eventing, Backend Development
topic: Commerce, Architecture
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 03787aa3-051b-4a35-b2e8-ecf6762b5eb4
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Bedingte Adobe Commerce-Ereignisse

Erfahren Sie mehr über bedingte Ereignisse in Adobe Commerce, die in Adobe Developer App Builder verwendet werden können. Weitere Dokumentationen finden Sie unter [Installieren von Adobe I/O Events für Adobe Commerce](https://developer.adobe.com/commerce/extensibility/events/conditional-events/){target="_blank"}.

## Für wen ist dieses Video bestimmt?

* Entwickler, die noch nicht mit Adobe Commerce und Adobe Developer App Builder vertraut sind und I/O-Ereignisse verwenden, müssen ein Adobe App Builder-Projekt erstellen.

## Videoinhalt {#video-content}

* Informationen zu bedingten Ereignissen
* Erfahren Sie, wie Sie die neue XML-Datei „io_events.xml“ ordnungsgemäß verwenden.
* Erfahren Sie, wie Sie bedingte Ereignisse konfigurieren
* Definieren von Regeln zur Verwendung in bedingten Ereignissen
* Erfahren Sie, wie Sie Ereignisse in der Commerce-Instanz registrieren `app/etc/config.php`

>[!VIDEO](https://video.tv.adobe.com/v/3430657?captions=ger&quality=12&learn=on)

## Nützliche Befehle {#useful-commands}

```bash
bin/magento events:subscribe plugin.magento.catalog.model.resource_model.product.save --fields=sku --fields=qty --fields=category_id

bin/magento events:subscribe plugin.magento.catalog.model.resource_model.product.save_low_stock --parent=plugin.magento.catalog.model.resource_model.product.save --fields=sku --fields=qty --fields=category_id --rules="qty|lessThan|20" --rules="category_id|in|3,4,5"

cat app/etc/config.php

bin/magento events:list

bin/magento events:list -v
```

{{$include /help/_includes/io-events-related-links.md}}
