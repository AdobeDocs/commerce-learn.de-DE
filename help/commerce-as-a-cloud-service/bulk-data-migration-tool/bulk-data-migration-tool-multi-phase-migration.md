---
title: Tool für die Massendatenmigration - Mehrphasen-Migration
description: Erfahren Sie, wie Sie mit dem Tool für die Massendatenmigration im Wartungsmodus eine mehrphasige Migration ausführen, wenn Ihre Quelle während der Produktionsumstellung eingefroren bleiben muss.
feature: Data Import/Export
topic: Migration
role: Developer
doc-type: Technical Video
duration: 211
last-substantial-update: 2026-07-27T00:00:00Z
jira: KT-22157
source-git-commit: c3b81a5ffc652bc7ce7640b67fe5529067607251
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Ausführen einer mehrphasigen Migration mit dem Tool für die Massendatenmigration

Führen Sie eine mehrphasige Migration durch, wenn Ihre Quellumgebung während der Extraktion eingefroren werden muss - ideal für Produktionsverlagerungen, bei denen während der Migration keine neuen Aufträge eingehen können. Es verwendet den Wartungsmodus und umfasst fünf Phasen, die nacheinander ausgeführt werden müssen. Wenn Ihre Quelle live bleiben kann, sehen Sie sich stattdessen das einphasige Migrationsvideo in dieser Reihe an.

## Für wen ist dieses Video bestimmt?

* Lösungsarchitekt
* DevOps-Engineer
* Backend-Entwicklerperson

## Videoinhalt

* Ein wichtiger Unterschied vor dem Start: `bin/console` Befehle werden für das Migrations-Tool selbst ausgeführt; `bin/magento maintenance` Befehle werden auf Ihrem Commerce-Quellserver ausgeführt. Das Tool aktiviert oder deaktiviert den Wartungsmodus nicht für Sie - dies ist ein manueller Schritt.
* Phase 1 wird ausgeführt, während die Quelle noch live ist - `bin console migration:before-maintenance` überprüft die Konfiguration, initialisiert die Umgebung, stellt eine Verbindung zu CDMS her, registriert die Migration, führt Funktionstests durch und erstellt synthetische Testdaten. Aktivieren Sie den Wartungsmodus erst nach Abschluss dieser Phase.
* Phase drei besteht in der Extraktion aus einer eingefrorenen Umgebung. `bin/console migration:during-maintenance` öffnet bei Bedarf PaaS-Tunnel neu, extrahiert aus der Quelle, bereinigt Staging-Ansichten, lädt in das ACS-Ziel, führt die Überprüfung durch und bereinigt Testdaten auf dem Ziel.

>[!VIDEO](https://video.tv.adobe.com/v/3496420?captions=ger&learn=on)
