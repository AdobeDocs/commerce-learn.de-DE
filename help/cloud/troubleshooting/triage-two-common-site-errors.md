---
title: Einige häufige Commerce Cloud-Fehler diagnostizieren und beheben
description: Beheben Sie zwei häufige Adobe Cloud-Projektfehler, die das Laden der Site verhindern.
feature: Cloud, Site Management
topic: Commerce, Development
role: Architect, Developer
level: Beginner, Intermediate
doc-type: Technical Video
duration: 260
last-substantial-update: 2024-10-30T00:00:00Z
jira: KT-16419
source-git-commit: 27c1715dd42853013181d9c729549a5a32bc2af0
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Diagnose und Fehlerbehebung für nicht verfügbaren Dienst und aufgetretenen Fehler

Erfahren Sie, wie Sie zwei häufige Fehler in Adobe Commerce Cloud-Projekten testen und beheben können.  Erfahren Sie, wie und warum diese Fehler auftreten und welche Schritte zur Behebung dieser Fehler empfohlen werden.

## Für wen ist dieses Video vorgesehen?

- Entwickler und IT-Fachkräfte
- Systemadministratoren

## Videoinhalt

- Speicherprobleme diagnostizieren und beheben:
- Wartungsmodus verwalten
- Tipps zur effizienten Fehlerbehebung

>[!VIDEO](https://video.tv.adobe.com/v/3435766?learn=on)


## Im Video verwendete Befehle

Suchen Sie die letzten fünf Zeilen des Ausnahmeprotokolls, die in der Antwortmeldung erwähnt werden.

```SHELL
 tail -n 5 ~/var/log/exception.log
```

Überprüfen des Festplattenspeicherplatzes. Beachten Sie die Zeile dev/mapper/xxxx .

```SHELL
df -h
```

Hier werden die 15 größten Dateien vorgestellt

```SHELL
find -type f -exec du -Sh {} + | sort -rh | head -n 15
```

Status des Wartungsmodus anzeigen

```SHELL
php bin/magento maintenance:status
```

Wartungsmodus deaktivieren

```SHELL
php bin/magento maintenance:disable 
```
