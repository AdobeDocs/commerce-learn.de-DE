---
title: Erfahren Sie, wie Sie ein Modul in Adobe Commerce zur Verwendung von Ereignissen erstellen.
description: Erfahren Sie, wie Sie das Commerce-Modul zur Verwendung von Ereignissen erstellen.
landing-page-description: Erfahren Sie, wie Sie ein Adobe Commerce-Modul zur Verwendung von Ereignissen erstellen.
short-description: Erfahren Sie, wie Sie ein Adobe Commerce-Modul zur Verwendung von Ereignissen erstellen.
kt: 11891
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-21T00:00:00Z
feature: App Builder, Eventing, Backend Development
topic: Commerce, Architecture
role: Architect, Developer
level: Beginner, Intermediate
exl-id: e8103fe0-116a-499c-ae0a-3ad0511f44d0
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Entwicklung von Adobe Commerce-Modulen

Erfahren Sie, wie Sie Ereignisse registrieren, unterstützte Ereignisse finden und wie Sie eine neue XML-Datei `io_events.xml` in der Entwicklung benutzerdefinierter Module verwenden. Das Video zeigt Entwicklern außerdem, wie sie registrierte Ereignisse finden, die verwendet werden können, und alle möglicherweise bereits definierten Ereignisse abmelden können. Weitere Informationen finden Sie unter [Installieren von Adobe I/O-Ereignissen für Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Für wen ist dieses Video?

* Entwickler, die neu bei Adobe Commerce und Adobe Developer App Builder mit I/O-Ereignissen sind.

## Videoinhalt {#video-content}

* Registrieren von Ereignissen in Commerce zur Verwendung in Adobe Developer App Builder
* Identifizieren von Ereignissen, die registriert werden können
* Erfahren Sie, wie Sie Ereignisse in io_events.xml registrieren.
* Erfahren Sie, wie Sie Ereignisse in den Commerce-Instanzen registrieren `app/etc/config.php`
* Erfahren Sie, wie Sie sich von einem Ereignis abmelden

>[!VIDEO](https://video.tv.adobe.com/v/3415802?quality=12&learn=on)

## Nützliche Befehle {#useful-commands}

```bash
bin/magento events:list:all Magento_Catalog

bin/magento events:info plugin.magento.catalog.api.category_repository.save

bin/magento events:subscribe observer.catalog_category_save_after --fields=entity_id --fields=parent_id

cat app/etc/config.php

bin/magento events:unsubscribe observer.catalog_category_save_after

bin/magento events:list
```

{{$include /help/_includes/io-events-related-links.md}}
