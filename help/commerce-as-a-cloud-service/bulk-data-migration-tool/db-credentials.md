---
title: Tool für die Massendatenmigration - DB-Anmeldeinformationen
description: Erfahren Sie, wie Sie die Quelldatenbankverbindung in Ihrer .my.cnf-Datei mithilfe der Magento Cloud-CLI oder einer Projekt-ID konfigurieren, bevor Sie das Migrations-Tool ausführen.
role: Developer
level: Intermediate
doc-type: Technical Video
topic: Migration
feature: Data Import/Export
duration: 161
last-substantial-update: 2026-07-21T00:00:00.000Z
jira: KT-22105
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%
---
# Konfigurieren der Datenbankanmeldeinformationen für das Tool für die Massendatenmigration

Richten Sie die Quelldatenbankverbindung in Ihrer `.my.cnf` ein, bevor Sie das Tool für die Massendatenmigration ausführen. Die Schritte unterscheiden sich je nachdem, ob es sich bei Ihrer Quellumgebung um eine lokale Umgebung oder Adobe Commerce as a Cloud Service (PaaS) handelt.

## Für wen ist dieses Video bestimmt?

* Lösungsarchitekt
* DevOps-Engineer
* Backend-Entwicklerperson

## Videoinhalt

* Kopieren Sie `.my.cnf.example` nach `.my.cnf` und erstellen Sie einen neuen Abschnitt mit dem Namen für Ihre Quellverbindung.
* Legen Sie die Projekt-ID in `.my.cnf` fest, wenn Ihre Quelle Adobe Commerce as a Cloud Service (PaaS) ist.
* Verwenden Sie die Befehle des Magento Cloud CLI-Tunnels, um Host-, Benutzer-, Passwort-, Port- und Datenbankwerte abzurufen.
* Überprüfen Sie die Host- und Port-Konnektivität, bevor Sie das Tool ausführen, wenn Ihre Quelle lokal ist.

>[!VIDEO](https://video.tv.adobe.com/v/3496164?captions=ger&learn=on)
