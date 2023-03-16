---
title: Konfigurieren von Adobe Commerce
description: Erfahren Sie, wie Sie Adobe Commerce so konfigurieren, dass Ereignisse in Adobe Developer App Builder verwendet werden können.
landing-page-description: Erfahren Sie, wie Sie Adobe Commerce so konfigurieren, dass der Ereignismechanismus für die Verwendung durch Adobe Developer App Builder verwendet wird.
short-description: Learn how to configure Adobe Commerce to use the event mechanism for consumption by Adobe Developer App Builder.
kt: 11889
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-21T00:00:00Z
source-git-commit: 67d21ca23cdccc87cdeed4a08a3ebb48e5bd1030
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Konfigurieren von Adobe Commerce

Erfahren Sie, wie Sie Adobe Commerce so konfigurieren, dass die Ereignisse verfügbar gemacht werden. Weitere Informationen finden Sie unter [Installieren von Adobe I/O-Ereignissen für Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Für wen ist dieses Video?

* Entwickler, die mit Adobe Commerce und Adobe Developer App Builder über I/O-Ereignisse neu sind, müssen ein Adobe App Builder-Projekt erstellen.

## Videoinhalt {#video-content}

* Konfiguration der Adobe I/O-Ereignisse in der Commerce-Admin-Instanz
* Speichern eines privaten Schlüssels in der Commerce-Administration
* Speichern der eindeutigen Kennung im Commerce-Administrator
* Erstellen eines Ereignisanbieters

>[!VIDEO](https://video.tv.adobe.com/v/3415799)

## Nützliche Befehle {#useful-commands}

```bash
bin/magento events:create-event-provider --label "my_provider" --description "Provides out-of-process extensibility for Adobe Commerce"

bin/magento events:subscribe observer.catalog_product_save_after --fields=name --fields=price
```

{{$include /help/_includes/io-events-related-links.md}}
