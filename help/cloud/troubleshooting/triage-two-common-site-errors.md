---
title: Diagnose und Behebung einiger häufiger Commerce Cloud-Fehler
description: Beheben Sie zwei häufige Adobe Cloud-Projektfehler, die verhindern, dass die Site geladen wird.
feature: Cloud, Site Management
topic: Commerce, Development
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
doc-type: Technical Video
duration: 260
last-substantial-update: 2024-10-30T00:00:00Z
jira: KT-16419
exl-id: 4c21b6a6-783a-422f-9071-3534ed68e8be
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Diagnose- und Fehlerbehebungsdienst nicht verfügbar und Fehler aufgetreten

Erfahren Sie, wie Sie zwei häufige Fehler in Adobe Commerce Cloud-Projekten triagieren und beheben.  Erfahren Sie, wie und warum diese Fehler auftreten und welche Schritte zur Behebung empfohlen werden.

## Für wen ist dieses Video gedacht?

- Entwickler und IT-Experten
- Systemadministratoren

## Videoinhalt

- Diagnose und Behebung von Speicherproblemen:
- Wartungsmodus verwalten
- Effiziente Tipps zur Fehlerbehebung

>[!VIDEO](https://video.tv.adobe.com/v/3447702?captions=ger&learn=on)


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
