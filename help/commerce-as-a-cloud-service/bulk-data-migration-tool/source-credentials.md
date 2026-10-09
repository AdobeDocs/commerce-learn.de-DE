---
title: Tool für die Massendatenmigration - Source-Anmeldeinformationen
description: Erfahren Sie, wie Sie die URL der Quellinstanz und die Authentifizierungsdaten in Ihrer .env-Datei konfigurieren, bevor Sie das Tool für die Massendatenmigration ausführen.
role: Developer
level: Intermediate
doc-type: Technical Video
topic: Migration
feature: Data Import/Export
duration: 238
last-substantial-update: 2026-07-21T00:00:00.000Z
jira: KT-22095
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

>[!VIDEO](https://video.tv.adobe.com/v/3496149?captions=ger&learn=on)
