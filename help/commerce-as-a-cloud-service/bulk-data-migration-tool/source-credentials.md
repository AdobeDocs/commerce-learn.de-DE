---
title: Tool für die Massendatenmigration - Source-Anmeldeinformationen
description: Erfahren Sie, wie Sie die URL der Quellinstanz und die Authentifizierungsdaten in Ihrer .env-Datei konfigurieren, bevor Sie das Tool für die Massendatenmigration ausführen.
role: Developer
level: Intermediate
doc-type: Technical Video
topic: Migration
feature: Data Import/Export
duration: 238
last-substantial-update: 2026-07-21T00:00:00Z
jira: KT-22095
source-git-commit: a785518a36cda9d2bfb82951c26f2e197ee3d43e
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# Konfigurieren von Quellberechtigungen für das Tool für die Massendatenmigration

Legen Sie die URL der Quellinstanz und die Authentifizierungsdaten in Ihrer `.env` fest, bevor Sie das Tool für die Massendatenmigration ausführen. Die Authentifizierungsschritte unterscheiden sich geringfügig je nachdem, ob Ihre Quellumgebung lokal oder Adobe Commerce as a Cloud Service (PaaS) ist.

## Für wen ist dieses Video bestimmt?

* Lösungsarchitekt
* DevOps-Engineer
* Backend-Entwicklerperson

## Videoinhalt

* Legen Sie die Quellinstanz-URL sowie die REST- und GraphQL-URLs in der `.env` fest.
* Rufen Sie Integrationsschlüssel unter **System** > **Erweiterungen** > **Integrationen** in Adobe Commerce Admin ab oder erstellen Sie sie.
* Um die vier erforderlichen Token zu generieren, aktivieren Sie die Integration.
* Rufen Sie das Magento-CLI-Token von account.magento.cloud ab, wenn Ihre Quelle Adobe Commerce as a Cloud Service (PaaS) ist.

>[!VIDEO](https://video.tv.adobe.com/v/3496142?learn=on)
