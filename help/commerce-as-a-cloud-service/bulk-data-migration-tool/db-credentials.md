---
title: Tool für die Massendatenmigration - DB-Anmeldeinformationen
description: Erfahren Sie, wie Sie die Quelldatenbankverbindung in Ihrer .my.cnf-Datei mithilfe der Magento Cloud-CLI oder einer Projekt-ID konfigurieren, bevor Sie das Migrations-Tool ausführen.
role: Developer
level: Intermediate
doc-type: Technical Video
topic: Migration
feature: Data Import/Export
duration: 161
last-substantial-update: 2026-07-21T00:00:00Z
jira: KT-22105
source-git-commit: 0dcb41e9138a36528f10333b0b5a9a9b2a39ed40
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
* Verwenden Sie die Magento Cloud-CLI-Tunnelbefehle, um Host-, Benutzer-, Kennwort-, Port- und Datenbankwerte abzurufen.
* Überprüfen Sie die Host- und Port-Konnektivität, bevor Sie das Tool ausführen, wenn Ihre Quelle lokal ist.

>[!VIDEO](https://video.tv.adobe.com/v/3496152?learn=on)
