---
title: Erfahren Sie, wie Sie IO-Ereignisse für Adobe Commerce 2.4.6 installieren
description: Erfahren Sie, wie Sie Module installieren, die für E/A-Ereignisse in Adobe Commerce 2.4.6 zur Verwendung in Adobe Developer App Builder erforderlich sind
jira: KT-11887
doc-type: Tutorial
duration: 136
last-substantial-update: 2023-02-22
badge: Adobe Commerce 2.4.6
feature: App Builder, Eventing
topic: Commerce, Architecture
role: Developer
level: Beginner, Intermediate
exl-id: 41b31ed8-04c5-4d50-aaff-abc3718b5957
TQID: https://experienceleague.adobe.com/19IVX54xo-RAJAOuXNIABdy11ExmBRAbWugi4eZ0cF0
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: 282072f1e29b836d19dee2e1b6498f75150fe3a5
workflow-type: tm+mt
source-wordcount: 141
ht-degree: 0%

---

# Installation von Adobe Commerce 2.4.6

Erfahren Sie, wie Sie mit Composer für Version 2.4.6 mehrere neue Module in Adobe Commerce installieren. Weitere Dokumentationen finden Sie unter [Installieren von Adobe I/O Events für Adobe Commerce](https://developer.adobe.com/commerce/extensibility/events/installation){target="_blank"}.

## Vorgesehene Zielgruppe

* Entwickler, die noch nicht mit Adobe Commerce und Adobe Developer App Builder vertraut sind und I/O Events verwenden.

## Videoinhalt {#video-content}

* Befehle, die für das On-Premise-Hosting ausgeführt werden
* Für Adobe Commerce Cloud auszuführende Befehle
* Adobe Commerce Cloud-YAML - erforderliche Bearbeitung

>[!VIDEO](https://video.tv.adobe.com/v/3430643?captions=ger&learn=on)

## Nützliche Befehle {#useful-commands}

Es gibt verschiedene Befehle, die sich je nachdem, ob Sie sich in einer selbst gehosteten Umgebung befinden oder Adobe Commerce Cloud verwenden, leicht unterscheiden.

### On-Premise Hosting {#on-premise}

```bash
bin/magento events:generate:module

bin/magento module:enable --all

bin/magento setup:upgrade && bin/magento setup:di:compile
```

### Adobe Commerce in Cloud Manager {#adobe-commerce-cloud}

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


