---
title: Quality Patch-Tool
description: Erfahren Sie, wie Sie das Quality Patch-Tool verwenden, um ein Problem zu diagnostizieren, eine Lösung zu finden und einen Patch anzuwenden, der in der Liste der verfügbaren Patches enthalten ist.
feature: Cloud, Configuration, Logs, System, Tools and External Services
topic: Architecture, Commerce, Development
role: Admin, Developer, User
level: Beginner, Intermediate
doc-type: Technical Video
duration: 903
last-substantial-update: 2024-07-17T00:00:00.000Z
jira: KT-15836
exl-id: 16710f27-1232-4c6a-aac3-9838308d1267
TQID: 'https://experienceleague.adobe.com/GpcJqSCn3XqLZtm-QdQ-ka9c-RdkG-C6Hd3FpXrh8-I'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
subfeature_v2:
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
  - id: 618ab558-d6ad-5352-99d6-d5702c6fdf80
    internal-label: Tools and External Services
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%
---
# Quality Patch-Tool

Erfahren Sie, wie Sie das Quality Patch-Tool verwenden, um ein Problem zu diagnostizieren, eine Lösung zu finden und einen Patch anzuwenden, der in der Liste der verfügbaren Patches enthalten ist.

## Was Sie lernen werden

Erfahren Sie, wie Sie ein Problem testen, und verwenden Sie dann einige grundlegende Techniken, um einen Qualitäts-Patch zu finden, um eine Korrektur anzuwenden.

## Zielgruppe

* Entwickler, die lernen, wie Probleme gefunden und dieses Tool zum Anwenden von GIT-Patches für bekannte Probleme genutzt werden

## Videoinhalt

Das Quality Patches Tool ist ein Befehlszeilenprogramm für Adobe Commerce und Magento Open Source. Folgendes ermöglicht es Ihnen zu tun:

* Allgemeine Informationen zu den neuesten Qualitäts-Patches anzeigen.
* Wenden Sie Qualitäts-Patches auf Ihre Installation an.
* Angewendete Patches bei Bedarf zurücksetzen

Diese Patches wurden von Adobe Developers und der Magento Open Source-Community entwickelt, um die Stabilität und Leistung zu verbessern. Beachten Sie, dass dies für die Anwendung einer großen Anzahl von Patches nicht empfohlen wird, da zukünftige Upgrades komplizierter werden können.

>[!VIDEO](https://video.tv.adobe.com/v/3431436?learn=on)

## Wozu dient das Quality Patch-Tool?

Sie sollten das Quality Patches Tool für Adobe Commerce oder Magento Open Source verwenden, wenn Sie Folgendes tun möchten:

Stabilität und Leistung verbessern: Qualitäts-Patches beheben Probleme, verbessern die Sicherheit und optimieren die Installation.
Bleiben Sie auf dem neuesten Stand: Durch das Anwenden von Patches wird sichergestellt, dass Ihr System aktuell und geschützt ist.
Änderungen rückgängig machen: Wenn ein Patch unerwartete Probleme verursacht, können Sie ihn mithilfe des Tools rückgängig machen. Denken Sie daran, dass es sich am besten für die Anwendung einer begrenzten Anzahl von Patches eignet, um zukünftige Upgrades zu vermeiden.  

## Einschränkungen oder Bedenken bei der Verwendung des Quality Patch-Tools

Das Quality Patches Tool bietet zwar Vorteile, es sind jedoch einige Überlegungen zu beachten:

* Kompatibilität: Stellen Sie sicher, dass die Patches mit Ihrer spezifischen Version von Adobe Commerce oder Magento Open Source kompatibel sind.
* Testen: Testen Sie Patches immer in einer Staging-Umgebung, bevor Sie sie auf die Produktion anwenden. Es können unerwartete Probleme auftreten.
* Patch-Abhängigkeiten: Einige Patches können von anderen abhängig sein. Beachten Sie alle Voraussetzungen.
* Anpassungen: Wenn Sie Änderungen an benutzerdefiniertem Code vorgenommen haben, können Patches zu Konflikten führen. Überprüfen Sie die Änderungen sorgfältig.
* Sichern: Sichern Sie Ihre Installation, bevor Sie Patches anwenden, um Datenverlust zu vermeiden.

Das Quality Patches Tool ist zwar für die Anwendung einer begrenzten Anzahl von Patches nützlich, wird aber nicht für die Handhabung einer großen Anzahl von Patches empfohlen. Die Anwendung zu vieler Patches kann zukünftige Upgrades und Wartungsarbeiten erschweren. Wenn Sie zahlreiche Patches anwenden müssen, sollten Sie alternative Ansätze in Betracht ziehen oder sich an einen Magento-Spezialisten wenden. 

## Zusammenfassung

Das Quality Patches Tool ermöglicht E-Commerce-Plattformen, die Stabilität und Sicherheit durch die Anwendung von Patches zu verbessern. Diese Patches beheben Probleme, verbessern die Leistung und optimieren das System. Die Installation auf dem neuesten Stand zu halten, bietet Schutz vor Sicherheitslücken.

Bevor Sie Patches anwenden, müssen Sie diese unbedingt in einer Staging-Umgebung testen. Gewährleisten Sie die Kompatibilität mit Ihrer spezifischen Version von Adobe Commerce oder Magento Open Source. Einige Patches weisen möglicherweise Abhängigkeiten auf. Überprüfen Sie daher die Voraussetzungen sorgfältig.

 Sichern Sie Ihre Installation, bevor Sie Patches anwenden, um Datenverlust zu vermeiden. Wenn Sie Änderungen an benutzerdefiniertem Code vorgenommen haben, beachten Sie, dass Patches Konflikte verursachen können. Befolgen Sie die Best Practices und überwachen Sie die Wirkung jedes Patches.

## Verwandte Artikel und Videos

* [Quality Patch-Tools suchen](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html)
* [Versionshinweise](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/release-notes)
* [GitHub für Patches](https://github.com/magento/quality-patches/blob/master/patches/os/)
* [Verwendung des Quality Patch-Tools](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/usage)
* [Technisches Video zu QPT](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/tools/quality-patch-tool)
