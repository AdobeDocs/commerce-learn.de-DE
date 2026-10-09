---
title: Analysieren von MySQL-Abfragen mit Percona Toolkit pt-query-digest
description: Erfahren Sie, wie Sie mit pt-query-digest MySQL-Abfragen aus langsamen, allgemeinen und binären Protokolldateien, SHOW PROCESSLIST und MySQL-Protokolldaten von tcpdump analysieren können.
doc-type: Technical Video
duration: 506
last-substantial-update: 2023-08-28T00:00:00.000Z
feature: Backend Development, Tools and External Services, Logs
topic: Commerce, Development
role: Developer
level: Intermediate
jira: KT-13846
exl-id: 77e91f1b-b3ae-4c6d-bb6d-4fd7ebbb0baf
TQID: 'https://experienceleague.adobe.com/lh-fBjlhZO6W-K08KNb-KaG-N2slLZVpNOSg6LAp0n8'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: b48dbafb-4193-5648-b9d9-bf96e9c9a411
    internal-label: Backend Development
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: 618ab558-d6ad-5352-99d6-d5702c6fdf80
    internal-label: Tools and External Services
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%
---
# Percona Toolkit pt-query-digest

Erfahren Sie, warum Sie pt-query-digest verwenden, und lernen Sie einige praktische Beispiele kennen, um die Analyse zu verbessern.

## Vorgesehene Zielgruppe

* Architekten
* Entwickler
* DevOps

## Videoinhalt

* Erfahren Sie mehr über die Verwendung von pt-query-digest
* Erfahren Sie mehr über die Vorteile und Mängel dieser Funktion des Percona Toolkits
* Machen Sie sich mit den Ergebnissen vertraut und erfahren Sie, welche möglichen Leistungsschritte berücksichtigt werden sollten

>[!VIDEO](https://video.tv.adobe.com/v/3423480?learn=on)

## Code-Verweise

```MYSQL
Be sure to change to match your logs and time frame

$ pt-query-digest mysql-slow.log.7 > mysql-slow.log.7.DIGEST
```

## Nützliche Ressourcen

* [Percona Toolkit](https://docs.percona.com/percona-toolkit/pt-query-digest.html){target="_blank"}
