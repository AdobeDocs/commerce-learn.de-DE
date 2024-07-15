---
title: Erfahren Sie, wie das Percona Toolkit pt-query-digest funktioniert und warum es verwendet wird.
description: Analysieren Sie MySQL-Abfragen aus langsamen, allgemeinen und binären Protokolldateien. Es kann auch Abfragen aus "SHOW PROCESSLIST"und MySQL-Protokolldaten aus tcpdump analysieren.
kt: 13846
doc-type: video
activity: use
last-substantial-update: 2023-8-28
feature: Backend Development, Tools and External Services, Logs
topic: Commerce, Development
role: Architect, Developer
level: Intermediate
exl-id: 77e91f1b-b3ae-4c6d-bb6d-4fd7ebbb0baf
source-git-commit: 598bff1fd2cefdc449d5ae3431401aec1e796313
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Percona Toolkit pt-query-digest

Erfahren Sie, warum Sie den pt-query-digest und einige Beispiele aus der realen Welt verwenden, um die Argumentation zu vertiefen.

## Für wen ist dieses Video?

- Architekten
- Entwickler
- DevOps

## Videoinhalt

- Informationen zur Verwendung von pt-query-digest
- Erfahren Sie mehr über die Vorteile und Mängel dieser Funktion des Percona Toolkit
- Machen Sie sich mit den Ergebnissen vertraut und erfahren Sie, welche möglichen Leistungsschritte berücksichtigt werden sollten.

>[!VIDEO](https://video.tv.adobe.com/v/3423480?learn=on)

## Codeverweise

```MYSQL
Be sure to change to match your logs and time frame

$ pt-query-digest mysql-slow.log.7 > mysql-slow.log.7.DIGEST
```

## Nützliche Ressourcen

- [Percona Toolkit](https://docs.percona.com/percona-toolkit/pt-query-digest.html){target="_blank"}
- [Deadlocks in MySQL](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/database/deadlocks-in-mysql.html){target="_blank"}
