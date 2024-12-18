---
title: Erfahren Sie, wie Sie langsame Abfragen in MySQL-Protokollen für langsame Abfragen finden und warum die Design-Methode für die Galera-DB-Replikation der Grund sein könnte
description: Galera DB verfügt über eine Design-Methode, die die Replikation von Daten in sekundäre Datenbanken länger als die primäre Datenbank dauert. Erfahren Sie, wie Sie diese Ereignisse im MySQL-Protokoll für langsame Abfragen finden, und erfahren Sie, warum Einträge in den Protokollen für langsame Abfragen angezeigt werden und wie Sie sie möglicherweise in Zukunft verhindern können.
kt: 13635
doc-type: video
activity: use
last-substantial-update: 2023-7-18
feature: Backend Development, Logs, Services
topic: Commerce, Development
role: Architect, Developer
level: Intermediate
exl-id: 4a8a2df1-8cac-4bd9-851f-0eaae011b76c
source-git-commit: 598bff1fd2cefdc449d5ae3431401aec1e796313
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Erfahren Sie mehr über die Galera-DB-Replikation und damit zusammenhängende langsame MySQL-Abfragen

Galera-Cluster helfen bei Leistung und Skalierbarkeit. Wenn Sie sekundäre Datenbanken berücksichtigen, müssen Sie wissen, dass sich die Datenreplikation von der primären unterscheidet. Die primäre Datenbank kann Massenvorgänge ausführen. Wenn die Replikation für alle sekundären Datenbanken erfolgt, führen sie die Aktionen nacheinander aus. Wenn beispielsweise 67.000.000 Elemente in einem Löschvorgang enthalten sind, geschieht in den sekundären Datenbanken jeweils eines nach dem anderen. Wenn Sie die langsamen Abfrageprotokolle von MySQL durchgehen, stellen Sie fest, dass diese Aktion lange dauern kann. Da die sekundären Datenbanken jeweils nur eine Leistung erbringen, ist ein Grund dafür, dass die Dinge nicht synchronisiert sind und Leistungseinbußen erkannt werden können.

Zur Lösung sollten Sie Ihre umfangreichen Vorgänge so stapelweise ausführen, dass die sekundären Datenbanken mit der primären Datenbank synchronisiert bleiben. Durch die Batch-Verarbeitung können die Aktionen zeitnah ausgeführt werden und die Leistungsauswirkungen werden auf ein Minimum reduziert.

## Für wen ist dieses Video bestimmt?

- Architekten
- Entwickler
- DevOps

## Videoinhalt

- Galerische Replikation in sekundäre Datenbank
- Erfahren Sie mehr über die Flusskontrolle
- Thread-Nummern in langsamen Abfrageprotokollen von MySQL finden
- Massenausführungen finden nur auf der primären Instanz statt. Die Replikationen erfolgen jeweils 1
- Bündeln Sie Ihre umfangreichen Commits, damit die Replikation mit der primären Instanz Schritt halten kann

>[!VIDEO](https://video.tv.adobe.com/v/3421688?learn=on)

## Nützliche Ressourcen

- [Galera-Cluster](https://galeracluster.com/)
