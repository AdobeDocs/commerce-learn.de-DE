---
title: Erfahren Sie, wie Sie langsame Abfragen in mysql-langsamen Abfragelogs finden und warum die Galera DB-Replikationsdesignmethode der Grund sein kann.
description: Galera DB verfügt über eine Designmethode, die die Replikation von Daten in sekundäre Datenbanken länger dauert als die primäre Datenbank. Erfahren Sie, wie Sie diese Ereignisse im langsamen mysql-Abfrageprotokoll finden, und den Grund, warum Sie Einträge in langsamen Abfragelogs sehen, und wie Sie sie in Zukunft vielleicht verhindern können.
kt: 13635
doc-type: video
activity: use
last-substantial-update: 2023-7-18
feature: Backend Development, Logs, Services
topic: Commerce, Development
role: Architect, Developer
level: Intermediate
source-git-commit: ae85993d98fb8620b763a212e5a2d7e53596870f
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Erfahren Sie mehr über die Galera DB-Replikation und zugehörige langsame MySQL-Abfragen

Galera-Cluster helfen bei Leistung und Skalierbarkeit. Bei der Prüfung sekundärer Datenbanken ist es wichtig zu verstehen, wie die Datenreplikation erfolgt, sich von der primären unterscheidet. Die primäre Datenbank kann Massenvorgänge durchführen. Wenn die Replikation für alle sekundären Datenbanken erfolgt, führen sie Aktionen nacheinander durch. Wenn Sie beispielsweise 67.000.000 Elemente in einem Löschvorgang haben, erfolgt in den sekundären Datenbanken jedes einzelne einzeln. Bei der Überprüfung der langsamen MySQL-Abfrageprotokolle kann diese Aktion viel Zeit in Anspruch nehmen. Da die sekundären Datenbanken Dinge einzeln durchführen, ist dies ein Grund dafür, dass Dinge nicht synchronisiert sind und Leistungsbeeinträchtigungen erkannt werden können.

Wenn möglich, sollten Sie Ihre großen Vorgänge als Lösung stapeln, um die sekundären Datenbanken mit den primären zu synchronisieren. Durch Batch-Vorgänge können die Aktionen zeitnah ausgeführt werden und die Leistungsbeeinträchtigungen auf ein Minimum beschränkt werden.

## Für wen ist dieses Video?

- Architekten
- Entwickler
- DevOps

## Videoinhalt

- Galeriereplikation in sekundäre Datenbank
- Informationen zur Flusssteuerung
- Suchen von Thread-Nummern in langsamen mysql-Abfrageprotokollen
- Massenausführungen erfolgen nur auf der primären Instanz. Replikationen treten jeweils 1 auf
- Batch Ihrer großen Zusagen, damit die Replikation mit der primären

>[!VIDEO](https://video.tv.adobe.com/v/3421688?learn=on)

## Nützliche Ressourcen

- [Galera-Cluster](https://galeracluster.com/)
