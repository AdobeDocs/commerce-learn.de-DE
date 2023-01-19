---
title: Out-of-Process-Erweiterbarkeit für Adobe Commerce
description: Erfahren Sie mehr über Adobe App Builder und warum es sich um einen wichtigen Aspekt der Out-of-Process-Erweiterbarkeit handelt.
landing-page-description: Erfahren Sie, was App Builder ist und wie es bei den Entwicklungsstrategien von Adobe Commerce helfen kann.
kt: 11433
doc-type: tutorial
audience: all
last-substantial-update: 2023-01-11T00:00:00Z
source-git-commit: ef0fa95e776b97ddbaf30e0acd1340e30f12738f
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---


# Out-of-Process-Erweiterbarkeit

Die Entwicklung von Adobe Commerce erfolgt historisch mit demselben Repository wie die Hauptanwendung.  Dies wird in der Verarbeitung bezeichnet.  Diese Technik ist sehr gut und bietet dem Entwickler einen erwarteten Mechanismus für die Erweiterung der Anwendung.  Dies ist jedoch preiswert.  Jedes Mal, wenn Sie neuen Code zur Codebase hinzufügen, muss er mit allen Upgrades kompatibel sein.  Sie müssen auch mit der PHP-Version der Server sowie mit vielen anderen Serveranwendungen und -diensten kompatibel sein, die Commerce nutzen wird.  Adobe Developer App Builder erfordert die Erweiterung der Funktionalität, verschiebt sie jedoch von der Site.  Der Code und die Logik sind vollständig extern, und diese Methode wird als Out-of-Process bezeichnet.

## App Builder für Adobe Commerce {#project-firefly}

>[!VIDEO](https://video.tv.adobe.com/v/3412839)

Adobe Developer App Builder bietet ein Erweiterbarkeits-Framework für Entwickler zum Erweitern von [!DNL Adobe Commerce] zur Bereitstellung einer Out-of-Process-Erweiterbarkeit.

App Builder bietet ein einheitliches Erweiterbarkeits-Framework von Drittanbietern für die Integration und Erstellung benutzerdefinierter Anwendungen, die [!DNL Adobe Commerce]. Da dieses Erweiterbarkeits-Framework auf der Infrastruktur der Adobe basiert, können Entwickler benutzerdefinierte Microservices erstellen sowie erweitern und integrieren [!DNL Adobe Commerce] über Adobe-Lösungen und andere Drittanbieterintegrationen.

App Builder bietet Kunden die Möglichkeit, [!DNL Adobe Commerce] in verschiedenen Anwendungsfällen:

* Middleware-Erweiterbarkeit - Schließen Sie externe Systeme mit Adobe-Anwendungen an, indem Sie benutzerdefinierte Connectoren erstellen oder eine Suite vordefinierter Integrationen nutzen.
* Erweiterbarkeit der Hauptdienste - Erweiterung der Kernanwendungsfunktionen durch Erweiterung des Standardverhaltens um benutzerdefinierte Funktionen und Geschäftslogik.
* Erweiterbarkeit des Benutzererlebnisses - Erweitern Sie das Kernerlebnis, um geschäftliche Anforderungen zu unterstützen oder kundenspezifische digitale Eigenschaften, Storefronts und Back-Office-Anwendungen zu erstellen.

App Builder (früher als Project Firefly bekannt) ist eine Cloud-basierte Lösung, d. h. sie wird automatisch skaliert. Dieser Dienst ist auch global verteilt, um unabhängig von Ihrem geografischen Standort die beste Leistung zu erzielen.

## Warum sollten Sie mehr über App Builder erfahren?

Da Adobe Commerce nicht vollständig SAAS ist, kann der Code, den Sie entwickeln oder installieren, Komplexität und Aktualisierungsprobleme hinzufügen. Durch die Verwendung von Out-of-Process-Erweiterbarkeit wie App Builder können Sie Ihrem Adobe Commerce Store benutzerdefinierte, einzigartige Funktionen bereitstellen, ohne dass hierfür In-Process-Methoden erforderlich sind.

Weitere Vorteile sind:

* Entkoppelte Funktionen ermöglichen schnellere Startzeiten.
* Upgrades sind jetzt einfacher. Die benutzerdefinierten Funktionen befinden sich außerhalb der Commerce-Codebasis, wodurch Kompatibilitätsprobleme beim Aktualisieren verhindert werden.
* Durch das Verschieben von Funktionen und Logik außerhalb des Commerce werden Ressourcen freigesetzt, die normalerweise von Entwicklungsmethoden in Prozessen verwendet werden.

## Architektur {#architecture}

Anstelle einer vordefinierten Lösung bietet Adobe Developer App Builder eine gemeinsame, konsistente und standardisierte Entwicklungsplattform für die Erweiterung von Adobe Cloud-Lösungen wie Adobe Commerce, einschließlich:

* Adobe Developer-Konsole, die für benutzerdefinierte Microservice- und Erweiterungsentwicklung verwendet wird. Erstellen und verwalten Sie Projekte und greifen Sie auf alle Tools und APIs zu, die zum Erstellen von Plug-ins und Integrationen erforderlich sind.
* Open-Source-Tools, SDKs und Bibliotheken zum Erstellen benutzerdefinierter Erweiterungen und Integrationen. Verwenden Sie React Spectrum (UI-Toolkit der Adobe), um eine gemeinsame Benutzeroberfläche für alle Adobe Apps zu haben.
* Dienste wie I/O Runtime für das Hosting der Infrastruktur auf der Server-losen Plattform der Adobe und I/O-Ereignisse für ereignisbasierte Integrationen. Adobe bietet außerdem native Unterstützung zum Speichern von Daten und Dateien.
* Adobe Experience Cloud, wo Sie Erweiterungen und Integrationen zur Veröffentlichung in Ihrer Experience Cloud-Organisation senden. Systemadministratoren können diese Erweiterungen überprüfen, verwalten und genehmigen. Nach der Veröffentlichung sind Ihre benutzerdefinierten App Builder-Erweiterungen und -Tools zusammen mit anderen Adobe Experience Cloud-Apps verfügbar.

Die folgende Abbildung zeigt, wie eine auf App Builder aufbauende Standardanwendung diese Funktionen verwendet:

![Architektur](/help/assets/app-builder/firefly-architecture.jpeg)

Weitere Informationen zur App Builder-Architektur finden Sie im Abschnitt [Architekturüberblick](https://developer.adobe.com/app-builder/docs/guides/).

## Erste Schritte mit App Builder {#additional-resources}

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

