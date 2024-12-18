---
title: Erfahren Sie, wie Sie ein Modul in Adobe Commerce erstellen, um Ereignisse zu verwenden.
description: Erfahren Sie, wie Sie ein Commerce-Modul erstellen, um Ereignisse zu verwenden.
landing-page-description: Erfahren Sie, wie Sie ein Adobe Commerce-Modul erstellen, um Ereignisse zu verwenden.
short-description: Erfahren Sie, wie Sie ein Adobe Commerce-Modul erstellen, um Ereignisse zu verwenden.
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

# Adobe Commerce-Modulentwicklung

Erfahren Sie, wie Sie Ereignisse registrieren, unterstützte Ereignisse finden und eine neue XML-`io_events.xml` in der Entwicklung benutzerdefinierter Module verwenden. In diesem Video erfahren Entwicklerinnen und Entwickler auch, wie sie registrierte Ereignisse finden, die verwendet werden können, und alle bereits definierten Ereignisse abmelden können. Weitere Dokumentationen finden Sie unter [Installieren von Adobe I/O-Ereignissen für Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Für wen ist dieses Video bestimmt?

* Entwickler, die noch nicht mit Adobe Commerce und Adobe Developer App Builder vertraut sind und I/O-Ereignisse verwenden.

## Videoinhalt {#video-content}

* Registrieren von Ereignissen in Commerce zur Verwendung in Adobe Developer App Builder
* Ereignisse identifizieren, die registriert werden können
* Erfahren Sie, wie Sie Ereignisse in io_events.xml registrieren.
* Erfahren Sie, wie Sie Ereignisse in der Commerce-Instanz registrieren `app/etc/config.php`
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
