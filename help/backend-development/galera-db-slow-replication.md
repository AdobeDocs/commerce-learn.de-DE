---
title: Diagnose der Galera DB-Replikation in langsamen MySQL-Abfrageprotokollen
description: Erfahren Sie, wie das Replikationsdesign von Galera DB die Synchronisation sekundärer Datenbanken verlangsamt, wie Sie diese Ereignisse in langsamen MySQL-Abfrageprotokollen identifizieren und wie Sie die Auswirkungen minimieren können.
doc-type: Technical Video
duration: 452
last-substantial-update: 2023-07-18
feature: Backend Development, Logs, Services
topic: Commerce, Development
role: Developer
level: Intermediate
jira: KT-13635
exl-id: 4a8a2df1-8cac-4bd9-851f-0eaae011b76c
TQID: https://experienceleague.adobe.com/NYapiIjnRv5RAS1glm8do16M4jUPmbgfVCs6ICQwbUc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: add3e29f8841ca4ca99f4c40afc656f00e93ec36
workflow-type: tm+mt
source-wordcount: 262
ht-degree: 0%

---

# Erfahren Sie mehr über die Galera-DB-Replikation und damit zusammenhängende langsame MySQL-Abfragen

Galera-Cluster helfen bei Leistung und Skalierbarkeit. Bei der Betrachtung von Replikatdatenbanken ist es wichtig zu verstehen, dass die Art und Weise, wie die Datenreplikation erfolgt, sich von der primären unterscheidet. Die primäre Datenbank kann Massenvorgänge ausführen. Wenn die Replikation für alle Replikatdatenbanken erfolgt, führen sie die Aktionen nacheinander aus. Wenn beispielsweise 67.000.000 Elemente in einem Löschvorgang enthalten sind, geschieht in den Replikatdatenbanken jedes einzeln. Wenn Sie die MySQL-Protokolle für langsame Abfragen überprüfen, stellen Sie fest, dass diese Aktion lange dauern kann. Die Tatsache, dass die Replikatdatenbanken Vorgänge sequenziell ausführen, ist ein Grund dafür, dass die Dinge nicht synchronisiert sind, und Leistungseinbußen können erkannt werden.

Damit die Replikatdatenbanken mit dem primären Batch synchronisiert bleiben, sollten Sie nach Möglichkeit umfangreiche Vorgänge ausführen. Durch die Batch-Verarbeitung können die Aktionen zeitnah ausgeführt werden und die Leistungsauswirkungen werden auf ein Minimum reduziert.

## Vorgesehene Zielgruppe

* Architekten
* Entwickler
* DevOps

## Videoinhalt

* Galerische Replikation in Replikatdatenbank
* Erfahren Sie mehr über die Flusskontrolle
* Thread-Nummern in langsamen Abfrageprotokollen von MySQL finden
* Massenausführungen finden nur auf der primären Instanz statt. Die Replikationen erfolgen jeweils 1
* Damit die Replikation mit dem primären Batch Schritt halten kann, sollten Sie die großen Commits im Batch speichern.

>[!VIDEO](https://video.tv.adobe.com/v/3421688?learn=on)

## Nützliche Ressourcen

* [Galera-Cluster](https://mariadb.com/products/enterprise/galera-cluster/)
