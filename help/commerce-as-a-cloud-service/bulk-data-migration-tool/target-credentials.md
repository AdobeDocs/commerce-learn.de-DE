---
title: Tool für die Massendatenmigration - Target-Anmeldedaten
description: Erfahren Sie, wie Sie die URLs der Zielinstanz, die Adobe IMS-Anmeldeinformationen und die CDMS-Einstellungen in Ihrer .env-Datei konfigurieren, bevor Sie das Tool für die Massendatenmigration ausführen.
role: Developer
level: Intermediate
doc-type: Technical Video
topic: Migration
feature: Data Import/Export
duration: 226
last-substantial-update: 2026-07-21T00:00:00Z
jira: KT-22107
source-git-commit: b3c029f7c1080550900cbc5838478cd7a4137a20
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
