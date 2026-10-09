---
title: Tool für die Massendatenmigration - Target-Anmeldedaten
description: Erfahren Sie, wie Sie die URLs der Zielinstanz, die Adobe IMS-Anmeldeinformationen und die CDMS-Einstellungen in Ihrer .env-Datei konfigurieren, bevor Sie das Tool für die Massendatenmigration ausführen.
role: Developer
level: Intermediate
doc-type: Technical Video
topic: Migration
feature: Data Import/Export
duration: 226
last-substantial-update: 2026-07-21T00:00:00.000Z
jira: KT-22107
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
source-wordcount: '173'
ht-degree: 0%
---
# Konfigurieren der Target-Anmeldeinformationen für das Tool für die Massendatenmigration

Legen Sie die URLs der Zielinstanz, die Adobe IMS-Anmeldeinformationen und die CDMS-Einstellungen in Ihrer `.env`-Datei fest, bevor Sie das Tool für die Massendatenmigration ausführen. Stellen Sie sicher, dass Ihre Adobe IMS-URL, Ziel-URL und der CDMS-Host alle derselben Umgebungsstufe entsprechen - Staging- oder Produktionsumgebung.

## Für wen ist dieses Video bestimmt?

* Lösungsarchitekt
* DevOps-Engineer
* Backend-Entwicklerperson

## Videoinhalt

* Legen Sie die Zielinstanz-REST- und GraphQL-URLs sowie die Ziel-Mandanten-ID in der `.env` fest. Verwenden Sie dazu Werte aus dem Instanzinformationsbereich auf experience.adobe.com.
* Legen Sie die Adobe IMS-URL so fest, dass sie zu Ihrer Umgebungsebene (Staging- oder Produktionsebene) und Region passt.
* Rufen Sie die Adobe IMS-Client-ID und das Client-Geheimnis aus **Projekt** > **OAuth Server-zu-Server** in der Adobe Developer Console ab.
* Kopieren Sie die Zielgruppen-Organisations-ID und konfigurieren Sie den CDMS-Host, den Port und die lokalen Server-Einstellungen so, dass sie zu Ihrer Umgebung passen.

>[!VIDEO](https://video.tv.adobe.com/v/3496174?captions=ger&learn=on)
