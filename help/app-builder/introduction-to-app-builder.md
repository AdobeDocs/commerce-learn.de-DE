---
title: Out-of-process extensibility for Adobe Commerce
description: Erfahren Sie mehr über Adobe App Builder und warum er ein wichtiger Aspekt der prozessexternen Erweiterbarkeit ist.
jira: KT-11433
doc-type: Tutorial
duration: 322
last-substantial-update: 2023-02-16T00:00:00.000Z
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Developer
level: Beginner, Intermediate
exl-id: 94f8d82a-4a95-46ea-8eed-edf9bed5760c
TQID: https://experienceleague.adobe.com/c3dl6gZ7Jtje5rZCB9HrwmCbFrcu8bllL0z0B9cl5Jg
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 777
ht-degree: 2%

---

# Einführung in App Builder

Historically, Adobe Commerce development has used in-process extensibility. The in-process model requires any new code to be compatible with upgrades, the server&#39;s PHP version, and many other essential server applications and services that Commerce uses. Adobe Developer App Builder uses out-of-process extensibility to avoid these compatibility issues.

## App Builder for Adobe Commerce {#app-builder}

>[!VIDEO](https://video.tv.adobe.com/v/3412839?learn=on)

Adobe Developer App Builder is a serverless extensibility platform for integrating and creating custom experiences to extend Adobe solutions, and it&#39;s now available for Adobe Commerce. With App Builder, you can build secure and scalable apps that extend Commerce-native functionality and integrate with third-party solutions. As a developer, you can now take advantage of out-of-process extensibility with Adobe Commerce and that in turn provides immediate and long-term benefits.

App Builder provides a unified third-party extensibility framework for integrating and creating custom applications that extend [!DNL Adobe Commerce]. Since this extensibility framework is built on Adobe&#39;s infrastructure, developers can build custom microservices, and extend and integrate [!DNL Adobe Commerce] across other Adobe solutions and third-party integrations.

App Builder provides a way for customers to extend [!DNL Adobe Commerce] in various use cases:

* middleware extensibility - Connect external systems with Adobe applications by building custom connectors or take advantage of a suite of pre-built integrations.
* core services extensibility - Extend core application capabilities by extending the default behavior with custom features and business logic.
* user experience extensibility - Extend core experience to support business requirements or build customer-specific digital properties, storefronts, and back-office applications.

Adobe Developer App Builder is a cloud-based solution, which means that it automatically scales. This service is also globally distributed to allow the best performance regardless of your geographic location.

## Why should you learn more about App Builder

Since Adobe Commerce is not a fully SAAS product, the code you develop can add complexity and upgrade issues. By using out-of-process extensibility, such as App Builder, you can provide custom, unique functionality to your Adobe Commerce store without requiring in-process methods.

Other benefits include:

* Decoupled features allow for faster time to launch.
* Upgrades are now easier. Die benutzerdefinierten Funktionen befinden sich außerhalb der Commerce-Codebasis, wodurch Kompatibilitätsprobleme beim Upgrade vermieden werden.
* Wenn Funktionen und Logik außerhalb von Commerce verschoben werden, werden Ressourcen freigegeben, die normalerweise von prozessinternen Entwicklungsmethoden verwendet werden.

## Architektur {#architecture}

Anstelle einer vordefinierten Lösung bietet Adobe Developer App Builder eine gemeinsame, konsistente und standardisierte Entwicklungsplattform für die Erweiterung von Adobe Cloud-Lösungen wie Adobe Commerce, einschließlich:

* Adobe Developer Console wird für die Entwicklung benutzerdefinierter Microservices und Erweiterungen verwendet. Erstellen und verwalten Sie Projekte, während Sie auf alle Tools und APIs zugreifen, die zum Erstellen von Plug-ins und Integrationen erforderlich sind.
* Open-Source-Tools, SDKs und Bibliotheken zum Erstellen benutzerdefinierter Erweiterungen und Integrationen. Verwenden Sie React Spectrum (UI-Toolkit von Adobe), um eine gemeinsame Benutzeroberfläche für alle Adobe-Apps zu haben.
* Services wie I/O Runtime für das Hosting der Infrastruktur auf der Server-losen Adobe-Plattform und I/O Events für ereignisbasierte Integrationen. Adobe bietet außerdem vordefinierte Unterstützung für das Speichern von Daten und Dateien.
* Adobe Experience Cloud, bei dem Sie Erweiterungen und Integrationen zur Veröffentlichung in Ihrer Experience Cloud-Organisation einreichen. Systemadministratoren können diese Erweiterungen überprüfen, verwalten und genehmigen. Nach der Veröffentlichung sind Ihre benutzerdefinierten App Builder-Erweiterungen und -Tools zusammen mit anderen Adobe Experience Cloud-Apps verfügbar.

Die folgende Abbildung zeigt, wie eine auf App Builder aufbauende Standardanwendung diese Funktionen nutzt:

![Architektur](/help/assets/app-builder/app-builder-architecture.jpeg)

Weitere Informationen zur App Builder-Architektur finden Sie unter [Architekturübersicht](https://developer.adobe.com/app-builder/docs/guides/){target="_blank"}.

## Erste Schritte mit App Builder {#additional-resources}

Einen Überblick über die zusammenstellbare Commerce-Strategie, die die Ersteinrichtung umfasst, finden Sie im folgenden Blogpost:

[Wie App Builder die Agilität Ihrer Geschäftsplattform steigert](https://business.adobe.com/blog/how-to/how-app-builder-helps-you-implement-a-composable-commerce-strategy){target="_blank"}

Um Ihnen die ersten Schritte mit App Builder zu erleichtern, hat Adobe die folgende Dokumentation erstellt:

* [Erste Schritte mit App Builder](https://developer.adobe.com/app-builder/docs/getting_started/){target="_blank"}

## Weiter lernen mit Dokumentation {#appbuilder-documentation}

App Builder bietet Videos und Dokumentation für Entwicklerinnen und Entwickler, einschließlich Handbüchern und Referenzdokumentation, die Sie bei der Entwicklung Ihrer eigenen benutzerdefinierten Programme unterstützen:

* [Dokumentation zu App Builder](https://developer.adobe.com/app-builder/docs/overview/){target="_blank"}
* [App Builder videos](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o){target="_blank"}

## Try Out One of the Sample Applications {#appbuilder-codesamples}

Ready to start developing? The following link contains sample applications to help get you started:

* [App Builder Code Labs on Adobe Developer Website](https://developer.adobe.com/app-builder/docs/resources/){target="_blank"}

## Support {#support}

For developer support requests, use the [Experience League forum](https://experienceleaguecommunities.adobe.com/t5/app-builder/ct-p/project-firefly?profile.language=de){target="_blank"} for assistance.

{{$include /help/_includes/app-builder-related-links.md}}
