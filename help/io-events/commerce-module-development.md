---
title: Erstellen eines Adobe Commerce-Moduls zur Verwendung von I/O-Ereignissen
description: Erfahren Sie, wie Sie ein Commerce-Modul erstellen, um Ereignisse zu verwenden.
jira: KT-11891
doc-type: Tutorial
duration: 314
last-substantial-update: 2023-02-21
feature: App Builder, Eventing, Backend Development
topic: Commerce, Architecture
role: Developer
level: Beginner, Intermediate
exl-id: e8103fe0-116a-499c-ae0a-3ad0511f44d0
TQID: https://experienceleague.adobe.com/bRnOh6fnsyTY-21f81vIXV4-eeitLXQWsAbjg2rx-Is
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: 282072f1e29b836d19dee2e1b6498f75150fe3a5
workflow-type: tm+mt
source-wordcount: 140
ht-degree: 0%

---

# Adobe Commerce-Modulentwicklung

Erfahren Sie, wie Sie Ereignisse registrieren, unterstützte Ereignisse finden und eine neue XML-`io_events.xml` in der Entwicklung benutzerdefinierter Module verwenden. Das Video zeigt Entwicklerinnen und Entwicklern auch, wie sie registrierte Ereignisse finden, die verwendet werden sollen, und wie sie bereits definierte Ereignisse entfernen können. Weitere Dokumentationen finden Sie unter [Installieren von Adobe I/O Events für Adobe Commerce](https://developer.adobe.com/commerce/extensibility/events/installation){target="_blank"}.

## Für wen ist dieses Video bestimmt?

* Entwickler, die noch nicht mit Adobe Commerce und Adobe Developer App Builder vertraut sind und I/O-Ereignisse verwenden.

## Videoinhalt {#video-content}

* Registrieren von Commerce-Ereignissen für Adobe Developer App Builder
* Ereignisse identifizieren, die registriert werden können
* Erfahren Sie, wie Sie Ereignisse in io_events.xml registrieren.
* Erfahren Sie, wie Sie Ereignisse in der Commerce-Instanz registrieren `app/etc/config.php`
* Erfahren Sie, wie Sie sich von einem Ereignis abmelden können

>[!VIDEO](https://video.tv.adobe.com/v/3415802?learn=on)

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


