---
title: Out-of-Process-Erweiterbarkeit für Adobe Commerce
description: Erfahren Sie mehr über Adobe App Builder und warum er ein wichtiger Aspekt der prozessexternen Erweiterbarkeit ist.
landing-page-description: Erfahren Sie, was App Builder ist und wie er bei den Entwicklungsstrategien von Adobe Commerce helfen kann.
short-description: Erfahren Sie, was App Builder ist und wie er bei den Entwicklungsstrategien von Adobe Commerce helfen kann.
kt: 11433
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-16
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 94f8d82a-4a95-46ea-8eed-edf9bed5760c
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 6%

---

# Einführung in App Builder

Bisher wurde bei der Adobe Commerce-Entwicklung die prozessinterne Erweiterbarkeit verwendet. Das In-Process-Modell erfordert, dass jeder neue Code mit Upgrades, der PHP-Version des Servers und vielen anderen wichtigen Serveranwendungen und -diensten, die Commerce verwendet, kompatibel ist. Adobe Developer App Builder verwendet prozessexterne Erweiterbarkeit, um diese Kompatibilitätsprobleme zu vermeiden.

## App Builder für Adobe Commerce {#app-builder}

>[!VIDEO](https://video.tv.adobe.com/v/3412839?quality=12&learn=on)

Adobe Developer App Builder ist eine Server-lose Erweiterungsplattform für die Integration und Erstellung benutzerdefinierter Erlebnisse zur Erweiterung von Adobe-Lösungen. Sie ist jetzt für Adobe Commerce verfügbar. Mit App Builder können Sie sichere und skalierbare Apps erstellen, die Commerce-native Funktionen erweitern und mit Lösungen von Drittanbietern integrieren. Als Entwickler können Sie jetzt die Vorteile der prozessexternen Erweiterbarkeit mit Adobe Commerce nutzen, was sofortige und langfristige Vorteile bietet.

App Builder bietet ein einheitliches Erweiterungs-Framework für Drittanbieter zur Integration und Erstellung benutzerdefinierter Anwendungen, die [!DNL Adobe Commerce] erweitern. Da dieses Erweiterbarkeits-Framework auf der Infrastruktur von Adobe basiert, können Entwicklerinnen und Entwickler benutzerdefinierte Microservices erstellen und [!DNL Adobe Commerce] über andere Adobe-Lösungen und Drittanbieterintegrationen erweitern und integrieren.

App Builder bietet Kunden die Möglichkeit, [!DNL Adobe Commerce] in verschiedenen Anwendungsfällen zu erweitern:

* Middleware-Erweiterbarkeit: Verbinden Sie externe Systeme mit Adobe-Anwendungen, indem Sie benutzerdefinierte Connectoren erstellen oder eine Suite vordefinierter Integrationen nutzen.
* Erweiterbarkeit der Hauptdienste - Erweiterung der Kernanwendungsfunktionen durch Erweiterung des Standardverhaltens um benutzerdefinierte Funktionen und Geschäftslogik.
* Erweiterbarkeit des Benutzererlebnisses - Erweitern Sie das Kernerlebnis, um Geschäftsanforderungen zu unterstützen oder kundenspezifische digitale Eigenschaften, Storefronts und Back-Office-Anwendungen zu erstellen.

Adobe Developer App Builder ist eine Cloud-basierte Lösung, die automatisch skaliert wird. Dieser Service ist auch global verteilt, um die beste Leistung unabhängig von Ihrem geografischen Standort zu ermöglichen.

## Warum sollten Sie mehr über App Builder erfahren?

Da Adobe Commerce kein vollständiges SAAS-Produkt ist, kann der von Ihnen entwickelte Code zu komplexeren Problemen und Upgrades führen. Durch die Verwendung von prozessexternen Erweiterbarkeiten wie App Builder können Sie Ihrem Adobe Commerce-Store benutzerdefinierte, eindeutige Funktionen bereitstellen, ohne dass hierfür prozessinterne Methoden erforderlich sind.

Weitere Vorteile:

* Entkoppelte Funktionen ermöglichen einen schnelleren Start.
* Upgrades sind jetzt einfacher. Die benutzerdefinierten Funktionen befinden sich außerhalb der Commerce-Codebasis, wodurch Kompatibilitätsprobleme beim Upgrade vermieden werden.
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
* [Videos zu App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o){target="_blank"}

## Testen einer der Beispielanwendungen {#appbuilder-codesamples}

Sind Sie bereit, mit der Entwicklung zu beginnen? Der folgende Link enthält Beispielanwendungen, die Ihnen bei den ersten Schritten helfen:

* [App Builder Code Labs auf der Adobe Developer-Website](https://developer.adobe.com/app-builder/docs/resources/){target="_blank"}

## Support {#support}

Für Anfragen zum Entwickler-Support verwenden Sie das [Experience League-Forum](https://experienceleaguecommunities.adobe.com/t5/app-builder/ct-p/project-firefly?profile.language=de){target="_blank"} um Hilfe zu erhalten.

{{$include /help/_includes/app-builder-related-links.md}}
