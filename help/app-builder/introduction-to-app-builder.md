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
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 94f8d82a-4a95-46ea-8eed-edf9bed5760c
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 5%

---

# Einführung in App Builder

In der Vergangenheit wurde bei der Adobe Commerce-Entwicklung eine Erweiterung der Prozesse verwendet. Das In-Process-Modell erfordert, dass jeder neue Code mit Upgrades, der PHP-Version des Servers und vielen anderen wichtigen Serveranwendungen und -diensten kompatibel ist, die Commerce verwendet. Adobe Developer App Builder verwendet Out-of-Process-Erweiterbarkeit, um diese Kompatibilitätsprobleme zu vermeiden.

## App Builder für Adobe Commerce {#app-builder}

>[!VIDEO](https://video.tv.adobe.com/v/3412839?quality=12&learn=on)

Adobe Developer App Builder ist eine Server-lose Erweiterbarkeitsplattform zur Integration und Erstellung benutzerdefinierter Erlebnisse, um Adobe-Lösungen zu erweitern. Jetzt ist es für Adobe Commerce verfügbar. Mit App Builder können Sie sichere und skalierbare Apps erstellen, die Commerce-native Funktionen erweitern und in Lösungen von Drittanbietern integrieren. Als Entwickler können Sie jetzt die Out-of-Process-Erweiterbarkeit mit Adobe Commerce nutzen, was wiederum sofortige und langfristige Vorteile bietet.

App Builder bietet ein einheitliches Erweiterbarkeits-Framework von Drittanbietern für die Integration und Erstellung benutzerdefinierter Anwendungen, die [!DNL Adobe Commerce] erweitern. Da dieses Erweiterbarkeits-Framework auf der Adobe-Infrastruktur basiert, können Entwickler benutzerdefinierte Microservices erstellen und [!DNL Adobe Commerce] über andere Adobe-Lösungen und Drittanbieterintegrationen hinweg erweitern und integrieren.

App Builder bietet Kunden eine Möglichkeit, [!DNL Adobe Commerce] in verschiedenen Anwendungsfällen zu erweitern:

* Middleware-Erweiterbarkeit - Schließen Sie externe Systeme mit Adobe-Anwendungen an, indem Sie benutzerdefinierte Connectoren erstellen oder eine Suite vordefinierter Integrationen nutzen.
* Erweiterbarkeit der Hauptdienste - Erweiterung der Kernanwendungsfunktionen durch Erweiterung des Standardverhaltens um benutzerdefinierte Funktionen und Geschäftslogik.
* Erweiterbarkeit des Benutzererlebnisses - Erweitern Sie das Kernerlebnis, um geschäftliche Anforderungen zu unterstützen oder kundenspezifische digitale Eigenschaften, Storefronts und Back-Office-Anwendungen zu erstellen.

Adobe Developer App Builder ist eine Cloud-basierte Lösung, d. h. sie wird automatisch skaliert. Dieser Dienst ist auch global verteilt, um unabhängig von Ihrem geografischen Standort die beste Leistung zu erzielen.

## Warum sollten Sie mehr über App Builder erfahren?

Da Adobe Commerce kein vollwertiges SAAS-Produkt ist, kann der von Ihnen entwickelte Code Komplexität und Aktualisierungsprobleme hinzufügen. Durch die Verwendung von Out-of-Process-Erweiterbarkeit wie App Builder können Sie benutzerdefinierte, einzigartige Funktionen für Ihren Adobe Commerce-Store bereitstellen, ohne dass hierfür In-Process-Methoden erforderlich sind.

Weitere Vorteile sind:

* Entkoppelte Funktionen ermöglichen schnellere Startzeiten.
* Upgrades sind jetzt einfacher. Die benutzerdefinierten Funktionen befinden sich außerhalb der Commerce-Codebasis, wodurch Kompatibilitätsprobleme beim Aktualisieren verhindert werden.
* Durch das Verschieben von Funktionen und Logik außerhalb von Commerce werden Ressourcen freigesetzt, die normalerweise von Entwicklungsmethoden in Prozessen verwendet werden.

## Architektur {#architecture}

Anstelle einer vordefinierten Lösung bietet Adobe Developer App Builder eine gemeinsame, konsistente und standardisierte Entwicklungsplattform für die Erweiterung von Adobe Cloud-Lösungen wie Adobe Commerce, einschließlich:

* Adobe Developer Console wird für benutzerdefinierte Microservice- und Erweiterungsentwicklung verwendet. Erstellen und verwalten Sie Projekte und greifen Sie auf alle Tools und APIs zu, die zum Erstellen von Plug-ins und Integrationen erforderlich sind.
* Open-Source-Tools, SDKs und Bibliotheken zum Erstellen benutzerdefinierter Erweiterungen und Integrationen. Verwenden Sie React Spectrum (Adobe UI Toolkit), um eine gemeinsame Benutzeroberfläche für alle Adobe-Apps zu haben.
* Dienste wie I/O Runtime für das Hosting der Infrastruktur auf der Server-losen Adobe-Plattform und I/O-Ereignisse für ereignisbasierte Integrationen. Adobe bietet außerdem native Unterstützung zum Speichern von Daten und Dateien.
* Adobe Experience Cloud, wo Sie Erweiterungen und Integrationen zur Veröffentlichung in Ihrer Experience Cloud-Organisation senden. Systemadministratoren können diese Erweiterungen überprüfen, verwalten und genehmigen. Nach der Veröffentlichung sind Ihre benutzerdefinierten App Builder-Erweiterungen und -Tools zusammen mit anderen Adobe Experience Cloud-Apps verfügbar.

Die folgende Abbildung zeigt, wie eine auf App Builder aufbauende Standardanwendung diese Funktionen verwendet:

![Architektur](/help/assets/app-builder/app-builder-architecture.jpeg)

Weitere Informationen zur App Builder-Architektur finden Sie unter [Architekturübersicht](https://developer.adobe.com/app-builder/docs/guides/){target="_blank"}.

## Amazon Sales Channel-Erweiterung {#amazon-sales-channel-extension}

>[!IMPORTANT]
>
>Die Amazon-Sales Channel-Erweiterung befindet sich noch in der Entwicklung und wurde nicht offiziell veröffentlicht.  In diesen Videos und Tutorials erfahren Sie, wie Sie Adobe Developer App Builder für einen praktischen Anwendungsfall verwenden.

Die folgenden Tutorials zeigen, wie Sie mit einer App Builder-Erweiterung eine Verbindung zwischen Adobe Commerce und Amazon Sales Channel herstellen.

* [Technischer Überblick App Builder](../app-builder/app-builder-technical-overview.md)
* [Erweiterungs-Framework](../app-builder/extensibility-framework-commerce-eventing.md)
* [Funktionsvorführung App Builder](../app-builder/app-builder-functional-demonstration.md)

## Erste Schritte mit App Builder {#additional-resources}

Eine Übersicht über die Strategie für den kombinierbaren Handel, einschließlich der ersten Einrichtung, finden Sie in folgendem Blogpost:

[Wie App Builder die geschäftliche Agilität Ihrer Commerce-Plattform fördert](https://business.adobe.com/blog/how-to/how-app-builder-helps-you-implement-a-composable-commerce-strategy){target="_blank"}

Für die ersten Schritte mit App Builder hat Adobe die folgende Dokumentation erstellt:

* [Erste Schritte mit App Builder](https://developer.adobe.com/app-builder/docs/getting_started/){target="_blank"}

## Weiteres Lernen mit Dokumentation {#appbuilder-documentation}

App Builder stellt Videos und Dokumentationen für Entwickler bereit, einschließlich Handbüchern und Referenzdokumenten, die bei der Entwicklung Ihrer eigenen benutzerdefinierten Anwendungen helfen:

* [App Builder-Dokumentation](https://developer.adobe.com/app-builder/docs/overview/){target="_blank"}
* [App Builder-Videos](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o){target="_blank"}

## Testen einer der Beispielanwendungen {#appbuilder-codesamples}

Bereit zur Entwicklung? Der folgende Link enthält Beispielanwendungen, die Ihnen beim Einstieg helfen:

* [App Builder-Code-Labs auf der Adobe Developer-Website](https://developer.adobe.com/app-builder/docs/resources/){target="_blank"}

## Support {#support}

Verwenden Sie für Support-Anfragen für Entwickler das [Experience League-Forum](https://experienceleaguecommunities.adobe.com/t5/app-builder/ct-p/project-firefly){target="_blank"}, um Hilfe zu erhalten.

{{$include /help/_includes/app-builder-related-links.md}}
