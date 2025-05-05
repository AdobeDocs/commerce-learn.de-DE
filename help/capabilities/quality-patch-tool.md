---
title: Quality Patch-Tool
description: Erfahren Sie, wie Sie das Quality Patch-Tool verwenden, um ein Problem zu diagnostizieren, eine Lösung zu finden und einen Patch anzuwenden, der in der Liste der verfügbaren Patches enthalten ist.
feature: Cloud, Configuration, Logs, System, Tools and External Services
topic: Architecture, Commerce, Development
role: Admin, Architect, User
level: Beginner, Intermediate
doc-type: Technical Video
duration: 771
last-substantial-update: 2024-07-17T00:00:00Z
jira: KT-15836
exl-id: 16710f27-1232-4c6a-aac3-9838308d1267
source-git-commit: e306b2cd26506f6a7ef37c2d416be7172dc3c0d2
workflow-type: tm+mt
source-wordcount: '542'
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

Diese Patches wurden von Adobe-Entwicklern und der Magento Open Source-Community entwickelt, um die Stabilität und Leistung zu verbessern. Beachten Sie, dass dies für die Anwendung einer großen Anzahl von Patches nicht empfohlen wird, da zukünftige Upgrades komplizierter werden können.

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

Das Quality Patches Tool ist zwar für die Anwendung einer begrenzten Anzahl von Patches nützlich, wird aber nicht für die Handhabung einer großen Anzahl von Patches empfohlen. Die Anwendung zu vieler Patches kann zukünftige Upgrades und Wartungsarbeiten erschweren. Wenn Sie viele Patches anwenden müssen, sollten Sie alternative Ansätze in Betracht ziehen oder sich an einen Magento-Spezialisten wenden. 

## Zusammenfassung 

Das Quality Patches Tool ermöglicht E-Commerce-Plattformen, die Stabilität und Sicherheit durch die Anwendung von Patches zu verbessern. Diese Patches beheben Probleme, verbessern die Leistung und optimieren das System. Die Installation auf dem neuesten Stand zu halten, bietet Schutz vor Sicherheitslücken.

Bevor Sie Patches anwenden, müssen Sie diese unbedingt in einer Staging-Umgebung testen. Stellen Sie die Kompatibilität mit Ihrer spezifischen Version von Adobe Commerce oder Magento Open Source sicher. Einige Patches weisen möglicherweise Abhängigkeiten auf. Überprüfen Sie daher die Voraussetzungen sorgfältig.

 Sichern Sie Ihre Installation, bevor Sie Patches anwenden, um Datenverlust zu vermeiden. Wenn Sie Änderungen an benutzerdefiniertem Code vorgenommen haben, beachten Sie, dass Patches Konflikte verursachen können. Befolgen Sie die Best Practices und überwachen Sie die Wirkung jedes Patches.

## Verwandte Artikel und Videos

* [Suche mit Quality Patch Tools](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=de)
* [Versionshinweise](https://experienceleague.adobe.com/de/docs/commerce-operations/tools/quality-patches-tool/release-notes)
* [GitHub für Patches](https://github.com/magento/quality-patches/blob/master/patches/os/)
* [Verwendung des Quality Patch-Tools](https://experienceleague.adobe.com/de/docs/commerce-operations/tools/quality-patches-tool/usage)
* [Technisches Video zu QPT](https://experienceleague.adobe.com/de/docs/commerce-learn/tutorials/tools/quality-patch-tool)
