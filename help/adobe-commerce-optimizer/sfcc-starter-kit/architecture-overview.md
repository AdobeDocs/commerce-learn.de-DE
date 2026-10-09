---
title: Salesforce Commerce Cloud Connector-Architektur
description: Erfahren Sie, wie das Salesforce Commerce Cloud Connector Starter Kit App Builder-Laufzeitaktionen und Delta-Exporte verwendet, um Kataloge mit Adobe Commerce Optimizer zu synchronisieren.
feature: App Builder,Saas
topic: Administration,Commerce,Integrations
role: Developer
level: Beginner
doc-type: Technical Video
duration: 288
last-substantial-update: 2025-10-20T00:00:00.000Z
jira: KT-19014
exl-id: 1e0edcbb-5619-45c2-b06d-9133f23a634f
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%
---
# Architektur des Salesforce Commerce Cloud Starter Kits

Erfahren Sie mehr über die Architektur und Funktionalität des Commerce Optimizer Connector-Starter-Kits, das Salesforce Commerce Cloud (SFCC) und Adobe App Builder integriert. Das Starter Kit wird von Adobe Commerce Optimizer zur Optimierung der Katalogsynchronisierung für Edge Delivery-Storefronts verwendet. Es wird erläutert, wie eine benutzerdefinierte Patrone in SFCC Katalogänderungen über Delta-Exportdateien erkennt und über benutzerdefinierte APIs verfügbar macht. Diese Änderungen werden von synchronen und asynchronen App Builder-Laufzeitaktionen genutzt, um vollständige und Delta-Synchronisierungen, Metadatenaktualisierungen und produktspezifische Synchronisierungen durchzuführen. Das System umfasst auch Validierungstools, um die Genauigkeit der Storefront sicherzustellen, und verwendet die Statusverwaltung von App Builder, um den Synchronisierungsstatus zu verfolgen und Konflikte zu verhindern.

## Für wen ist dieses Video bestimmt?

* Commerce-Lösungsarchitekt
* Technische Marketing-Ingenieure
* E-Commerce-Plattform-Administratoren

## Videoinhalt

* Benutzerdefinierte SFCC-Cartridge und -APIs erkennen Katalogänderungen über Delta-Exporte und ermöglichen so eine effiziente Datensynchronisation mit Adobe App Builder.
* App Builder Runtime-Aktionen verwalten vollständige und Delta-Synchronisationen, Validierungen und das Status-Tracking, um genaue und konfliktfreie Aktualisierungen der Commerce Optimizer sicherzustellen.

>[!VIDEO](https://video.tv.adobe.com/v/3476046?learn=on)

