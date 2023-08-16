---
title: Erfahren Sie, wie Sie bedingte Ereignisse in Adobe Commerce verwenden.
description: Erfahren Sie, wie Sie bedingte Ereignisse zur Verwendung in Adobe Developer App Builder verwenden.
landing-page-description: Erfahren Sie, wie Sie bedingte Adobe Commerce-Ereignisse verwenden.
short-description: Erfahren Sie, wie Sie bedingte Adobe Commerce-Ereignisse verwenden.
kt: 11890
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-21T00:00:00Z
feature: App Builder, Eventing, Backend Development
topic: Commerce, Architecture
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 03787aa3-051b-4a35-b2e8-ecf6762b5eb4
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Bedingte Ereignisse für Adobe Commerce

Erfahren Sie mehr über bedingte Ereignisse in Adobe Commerce, die in Adobe Developer App Builder verwendet werden können. Weitere Informationen finden Sie unter [Installieren von Adobe I/O-Ereignissen für Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/conditional-events/){target="_blank"}.

## Für wen ist dieses Video?

* Entwickler, die mit Adobe Commerce und Adobe Developer App Builder über I/O-Ereignisse neu sind, müssen ein Adobe App Builder-Projekt erstellen.

## Videoinhalt {#video-content}

* Erfahren Sie mehr über bedingte Ereignisse
* Erfahren Sie mehr über die ordnungsgemäße Verwendung der neuen XML-Datei io_events.xml
* Erfahren Sie, wie Sie bedingte Ereignisse konfigurieren
* Definieren von Regeln für die Verwendung in bedingten Ereignissen
* Erfahren Sie, wie Sie Ereignisse in den Commerce-Instanzen registrieren. `app/etc/config.php`

>[!VIDEO](https://video.tv.adobe.com/v/3415806?quality=12&learn=on)

## Nützliche Befehle {#useful-commands}

```bash
bin/magento events:subscribe plugin.magento.catalog.model.resource_model.product.save --fields=sku --fields=qty --fields=category_id

bin/magento events:subscribe plugin.magento.catalog.model.resource_model.product.save_low_stock --parent=plugin.magento.catalog.model.resource_model.product.save --fields=sku --fields=qty --fields=category_id --rules="qty|lessThan|20" --rules="category_id|in|3,4,5"

cat app/etc/config.php

bin/magento events:list

bin/magento events:list -v
```

{{$include /help/_includes/io-events-related-links.md}}
