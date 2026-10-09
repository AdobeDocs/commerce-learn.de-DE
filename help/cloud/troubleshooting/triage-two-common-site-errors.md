---
title: Diagnose und Behebung einiger häufiger Commerce Cloud-Fehler
description: Beheben Sie zwei häufige Adobe Cloud-Projektfehler, die verhindern, dass die Site geladen wird.
feature: Cloud, Site Management
topic: Commerce, Development
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
doc-type: Technical Video
duration: 297
last-substantial-update: 2024-10-30T00:00:00.000Z
jira: KT-16419
exl-id: 4c21b6a6-783a-422f-9071-3534ed68e8be
TQID: 'https://experienceleague.adobe.com/-mN2UoNU6uKjUoHmZT59LgT4o7p4d4O2Zl1BR3x8y-8'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 938d2364-5176-55ec-80f1-9415253e5e51
    internal-label: Site Management
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%
---
# Diagnose- und Fehlerbehebungsdienst nicht verfügbar und Fehler aufgetreten

Erfahren Sie, wie Sie zwei häufige Fehler in Adobe Commerce Cloud-Projekten triagieren und beheben.  Erfahren Sie, wie und warum diese Fehler auftreten und welche Schritte zur Behebung empfohlen werden.

## Für wen ist dieses Video gedacht?

* Entwickler und IT-Experten
* Systemadministratoren

## Videoinhalt

* Diagnose und Behebung von Speicherproblemen:
* Wartungsmodus verwalten
* Effiziente Tipps zur Fehlerbehebung

>[!VIDEO](https://video.tv.adobe.com/v/3435766?learn=on)


## Im Video verwendete Befehle

Suchen Sie die letzten 5 Zeilen des Ausnahmeprotokolls, die in der Antwortnachricht erwähnt werden.

```SHELL
 tail -n 5 ~/var/log/exception.log
```

So überprüfen Sie den Festplattenspeicher. Achten Sie auf die Zeile dev/mapper/xxxx

```SHELL
df -h
```

Suchen wir die 15 größten Dateien

```SHELL
find -type f -exec du -Sh {} + | sort -rh | head -n 15
```

Anzeigen des Status des Wartungsmodus

```SHELL
php bin/magento maintenance:status
```

Deaktivieren des Wartungsmodus

```SHELL
php bin/magento maintenance:disable 
```
