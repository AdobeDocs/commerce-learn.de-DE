---
title: Out-of-Process-Erweiterbarkeit für Adobe Commerce
description: Erfahren Sie mehr über Adobe App Builder und warum es sich um einen wichtigen Aspekt der Out-of-Process-Erweiterbarkeit handelt.
landing-page-description: Erfahren Sie, was App Builder ist und wie es bei den Entwicklungsstrategien von Adobe Commerce helfen kann.
kt: 11433
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-16T00:00:00Z
source-git-commit: 8726d58abbf6ac0fb1e403a0ece335978d4d7eac
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---


# Einführung in App Builder

In der Vergangenheit wurde bei der Adobe Commerce-Entwicklung eine Erweiterung der Prozesse verwendet. Das In-Process-Modell erfordert, dass jeder neue Code mit Upgrades, der PHP-Version des Servers und vielen anderen wichtigen Server-Anwendungen und -Services kompatibel ist, die Commerce verwendet. Adobe Developer App Builder verwendet Out-of-Process-Erweiterbarkeit, um diese Kompatibilitätsprobleme zu vermeiden.

## App Builder für Adobe Commerce {#project-firefly}

>[!VIDEO](https://video.tv.adobe.com/v/3412839)

Adobe Developer App Builder ist eine Server-lose Erweiterungsplattform zur Integration und Erstellung benutzerdefinierter Erlebnisse, um Adobe-Lösungen zu erweitern. Jetzt ist er für Adobe Commerce verfügbar. Mit App Builder können Sie sichere und skalierbare Apps erstellen, die Commerce-native Funktionen erweitern und in Lösungen von Drittanbietern integrieren. Als Entwickler können Sie jetzt die Out-of-Process-Erweiterbarkeit mit Adobe Commerce nutzen, was wiederum sofortige und langfristige Vorteile bietet.

App Builder bietet ein einheitliches Erweiterbarkeits-Framework von Drittanbietern für die Integration und Erstellung benutzerdefinierter Anwendungen, die [!DNL Adobe Commerce]. Da dieses Erweiterbarkeits-Framework auf der Infrastruktur der Adobe basiert, können Entwickler benutzerdefinierte Microservices erstellen sowie erweitern und integrieren [!DNL Adobe Commerce] über andere Adobe-Lösungen und Drittanbieterintegrationen.

App Builder bietet Kunden die Möglichkeit, [!DNL Adobe Commerce] in verschiedenen Anwendungsfällen:

* Middleware-Erweiterbarkeit - Schließen Sie externe Systeme mit Adobe-Anwendungen an, indem Sie benutzerdefinierte Connectoren erstellen oder eine Suite vordefinierter Integrationen nutzen.
* Erweiterbarkeit der Hauptdienste - Erweiterung der Kernanwendungsfunktionen durch Erweiterung des Standardverhaltens um benutzerdefinierte Funktionen und Geschäftslogik.
* Erweiterbarkeit des Benutzererlebnisses - Erweitern Sie das Kernerlebnis, um geschäftliche Anforderungen zu unterstützen oder kundenspezifische digitale Eigenschaften, Storefronts und Back-Office-Anwendungen zu erstellen.

App Builder (früher als Project Firefly bekannt) ist eine Cloud-basierte Lösung, d. h. sie wird automatisch skaliert. Dieser Dienst ist auch global verteilt, um unabhängig von Ihrem geografischen Standort die beste Leistung zu erzielen.

## Warum sollten Sie mehr über App Builder erfahren?

Da Adobe Commerce kein vollwertiges SAAS-Produkt ist, kann der von Ihnen entwickelte Code Komplexität und Aktualisierungsprobleme hinzufügen. Durch die Verwendung von Out-of-Process-Erweiterbarkeit wie App Builder können Sie Ihrem Adobe Commerce Store benutzerdefinierte, einzigartige Funktionen bereitstellen, ohne dass hierfür In-Process-Methoden erforderlich sind.

Weitere Vorteile sind:

* Entkoppelte Funktionen ermöglichen schnellere Startzeiten.
* Upgrades sind jetzt einfacher. Die benutzerdefinierten Funktionen befinden sich außerhalb der Commerce-Codebase, wodurch Kompatibilitätsprobleme beim Upgrade verhindert werden.
* Durch das Verschieben von Funktionen und Logik außerhalb von Commerce werden Ressourcen freigesetzt, die normalerweise von Entwicklungsmethoden in Prozessen verwendet werden.

## Architektur {#architecture}

Anstelle einer vordefinierten Lösung bietet Adobe Developer App Builder eine gemeinsame, konsistente und standardisierte Entwicklungsplattform für die Erweiterung von Adobe Cloud-Lösungen wie Adobe Commerce, einschließlich:

* Adobe Developer-Konsole, die für benutzerdefinierte Microservice- und Erweiterungsentwicklung verwendet wird. Erstellen und verwalten Sie Projekte und greifen Sie auf alle Tools und APIs zu, die zum Erstellen von Plug-ins und Integrationen erforderlich sind.
* Open-Source-Tools, SDKs und Bibliotheken zum Erstellen benutzerdefinierter Erweiterungen und Integrationen. Verwenden Sie React Spectrum (UI-Toolkit der Adobe), um eine gemeinsame Benutzeroberfläche für alle Adobe Apps zu haben.
* Dienste wie I/O Runtime für das Hosting der Infrastruktur auf der Server-losen Plattform der Adobe und I/O-Ereignisse für ereignisbasierte Integrationen. Adobe bietet außerdem native Unterstützung zum Speichern von Daten und Dateien.
* Adobe Experience Cloud, wo Sie Erweiterungen und Integrationen zur Veröffentlichung in Ihrer Experience Cloud-Organisation senden. Systemadministratoren können diese Erweiterungen überprüfen, verwalten und genehmigen. Nach der Veröffentlichung sind Ihre benutzerdefinierten App Builder-Erweiterungen und -Tools zusammen mit anderen Adobe Experience Cloud-Apps verfügbar.

Die folgende Abbildung zeigt, wie eine auf App Builder aufbauende Standardanwendung diese Funktionen verwendet:

![Architektur](/help/assets/app-builder/firefly-architecture.jpeg)

Weitere Informationen zur App Builder-Architektur finden Sie im Abschnitt [Architekturüberblick](https://developer.adobe.com/app-builder/docs/guides/).

## Amazon Sales Channel-Erweiterung {#amazon-sales-channel-extension}

>[!IMPORTANT]
>
>Die Amazon-Sales Channel-Erweiterung befindet sich noch in der Entwicklung und wurde nicht offiziell veröffentlicht.  Diese Videos und Tutorials zeigen Ihnen, wie Sie Adobe Developer App Builder für einen praktischen Anwendungsfall verwenden können.

Die folgenden Tutorials zeigen, wie Sie mit einer App Builder-Erweiterung eine Verbindung zwischen Adobe Commerce und Amazon Sales Channel herstellen.

* [Technische Übersicht App Builder](../app-builder/app-builder-technical-overview.md)
* [Erweiterungs-Framework](../app-builder/extensibility-framework-commerce-eventing.md)
* [Funktionale Demonstration App Builder](../app-builder/app-builder-functional-demonstration.md)

## Erste Schritte mit App Builder {#additional-resources}

Eine Übersicht über die Strategie für den kombinierbaren Handel, einschließlich der ersten Einrichtung, finden Sie in folgendem Blogpost:

[Wie App Builder die geschäftliche Agilität Ihrer Commerce-Plattform fördert](https://business.adobe.com/blog/how-to/how-app-builder-helps-you-implement-a-composable-commerce-strategy)

Für die ersten Schritte mit App Builder hat Adobe die folgende Dokumentation erstellt:

* [App Builder - Erste Schritte](https://developer.adobe.com/app-builder/docs/getting_started/)

## Weiteres Lernen mit Dokumentation {#appbuilder-documentation}

App Builder stellt Videos und Dokumentationen für Entwickler bereit, einschließlich Handbüchern und Referenzdokumenten, mit denen Sie Ihre eigenen benutzerdefinierten Anwendungen entwickeln können:

* [App Builder-Dokumentation](https://developer.adobe.com/app-builder/docs/overview/)
* [App Builder-Videos](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Testen einer der Beispielanwendungen {#appbuilder-codesamples}

Bereit zur Entwicklung? Der folgende Link enthält Beispielanwendungen, die Ihnen beim Einstieg helfen:

* [App Builder-Code-Labs auf der Adobe Developer-Website](https://developer.adobe.com/app-builder/docs/resources/)

## Support {#support}

Verwenden Sie für Support-Anfragen für Entwickler den [Experience League](https://experienceleaguecommunities.adobe.com/t5/app-builder/ct-p/project-firefly) Hilfe.

{{$include /help/_includes/app-builder-related-links.md}}
