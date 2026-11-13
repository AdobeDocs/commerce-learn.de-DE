---
title: Zusammensetzbare Commerce mit Adobe
description: Erfahren Sie mehr über zusammensetzbaren Commerce mit Adobe-Plattformoptionen, Edge Delivery Services-Storefronts, API Mesh, App Builder und MCP-Entwicklungs-Tools für Commerce.
feature: API Mesh, App Builder, Saas
topic: Architecture, Commerce, Development, Headless, Integrations, Performance, Personalization
role: Admin, Developer, User
level: Intermediate
doc-type: Tutorial
duration: 307
last-substantial-update: 2026-11-13
jira: KT-15730
exl-id: 4d811a2f-8488-4de7-babd-449aced42e3a
TQID: 'https://experienceleague.adobe.com/NG-US7zLBgzV425mheo3oQ9Z6gnzAr6aRCLNjHVU0aM'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
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
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
autotag-review: '2026-11-13T20:04:10.194Z'
source-git-commit: 3a52f4de8c63f08418f4fa44833a7bf7eb90175b
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 0%
---
# Zusammensetzbarer Handel

Composable Commerce ist ein architektonischer Ansatz, der Commerce-Funktionen über APIs kombiniert. Sie können Komponenten für Storefront-Erlebnisse, Katalogverwaltung, Produktsuche, Checkout und andere Geschäftsanforderungen auswählen und integrieren, anstatt jede Funktion aus einer eng verbundenen Anwendung zu beziehen.

Headless-Commerce trennt die Präsentationsebene der Storefront vom Commerce-Backend. Composable Commerce baut auf dieser Trennung auf, indem es Teams die Wahl lässt, welche Funktionen zusammengehalten und welche unabhängig integriert werden sollen. Eine Headless-Storefront macht nicht von Natur aus jede Backend-Komponente unabhängig austauschbar.

Adobe unterstützt diesen Ansatz durch Commerce-Plattformoptionen, Storefront-Technologie sowie Integrations- und Entwicklungs-Tools. Entwicklungs-MCPs für Adobe Commerce as a Cloud Service (ACCS), Adobe Commerce Optimizer (ACO), Edge Delivery Services, API Mesh, App Builder und Commerce dienen verschiedenen Zwecken. Sie sind keine austauschbaren Produkte oder ein erforderlicher kombinierter Stapel.

## Vorteile und Kompromisse

Ein zusammenstellbarer Ansatz kann Ihnen dabei helfen:

* **Anpassen des Kundenerlebnisses:** Wählen Sie Storefront-Komponenten und integrieren Sie Services, die Ihren Geschäftsanforderungen entsprechen.
* **Inkrementell modernisieren:** Ersetzen Sie ausgewählte Funktionen und behalten Sie gleichzeitig andere Systeme und deren Daten bei.
* **Unabhängig skalieren und weiterentwickeln:** Entwerfen Sie Integrationen und Erweiterungen so, dass ihre Änderungen keine Veröffentlichung der gesamten Commerce-Anwendung erfordern.
* **Wiederverwenden von Commerce-Funktionen:** Verwenden Sie unterstützte Plattformfunktionen und APIs, anstatt jede Geschäftsfunktion neu zu erstellen.

Diese Vorteile hängen von der Implementierung ab. Bewertung der technischen Reife, der Versandkosten, der Lizenzierung, der Sicherheit und des Datenschutzes. Definieren Sie die Eigentümerschaft für API-Verträge, Datensynchronisierung, Authentifizierung, Leistung und Fehler in allen Services. Eine modularere Architektur kann auch die Integration und die betriebliche Komplexität erhöhen.

## Adobe Commerce-Architekturoptionen

Entscheiden Sie zunächst, ob Sie eine verwaltete Commerce-Plattform benötigen oder die Kundenerlebnisse rund um ein vorhandenes Transaktions-Backend modernisieren möchten.

Einen Videovergleich finden Sie unter [Verfügbare Commerce-Optionen von Adobe](./adobes-available-commerce-options.md).

### Adobe Commerce as a Cloud Service

Adobe Commerce as a Cloud Service ist eine verwaltete SaaS-Commerce-Plattform. Adobe verwaltet die Kernanwendung, die Infrastruktur und Updates. Seine Architektur umfasst Commerce Foundation, Headless-Storefront-Funktionen, Merchandising-Services und Entwickler-Tools.

Verwenden Sie diese Option, wenn Sie eine verwaltete Commerce-Foundation mit unterstützten Erweiterungspunkten bewerten. Planen Sie für benutzerdefinierte Geschäftslogik eine unterstützte prozessexterne Erweiterbarkeit ein, anstatt davon auszugehen, dass vorhandene PHP-Erweiterungen unverändert bereitgestellt werden können. ACS unterstützt keine Luma-Storefronts. Nehmen Sie Storefront-Migration in Ihren Implementierungsplan auf, falls zutreffend.

Siehe [Übersicht über Adobe Commerce as a Cloud Service](https://experienceleague.adobe.com/de/docs/commerce/cloud-service/overview).

### Adobe Commerce Optimizer

Adobe Commerce Optimizer unterstützt Katalogverwaltung, Produkterkennung, Suche, Empfehlungen und Storefront-Erlebnisse und ermöglicht Ihnen gleichzeitig die Beibehaltung eines bestehenden Commerce-Backends. Katalogdaten können aus externen Quellen stammen und ein Drittanbietersystem kann für den Warenkorb- und Checkout-Lebenszyklus verantwortlich bleiben.

Verwenden Sie diese Option, wenn eine kundenorientierte Modernisierung das Ziel ist und kein Ersatz für das Transaktions-Backend erforderlich ist. Planen Sie explizit die Katalogaufnahme und Warenkorb- und Checkout-Integrationen. ACS und ACO sind separate Architekturoptionen, kein erforderlicher kombinierter Stack. Überprüfen Sie die aktuelle Integrationsunterstützung, bevor Sie Services für Ihre Implementierung auswählen.

Siehe [Übersicht über Adobe Commerce Optimizer](https://experienceleague.adobe.com/de/docs/commerce/optimizer/overview).

### Bestehende Adobe Commerce-Bereitstellungen

Adobe Commerce auf Cloud-Infrastrukturen und lokale Bereitstellungen können auch schrittweise Headless-Storefronts und unterstützte API-basierte Integrationen übernehmen. Je nach Bereitstellung können Sie eine vorhandene Storefront beibehalten oder eine unterstützte Headless-Storefront übernehmen. Die Beibehaltung vorhandener Commerce-Funktionen kann die Integrationsarbeit reduzieren und gleichzeitig die separate Weiterentwicklung ausgewählter Services ermöglichen.

Funktionsverfügbarkeit, Erweiterungskompatibilität, Lizenzierung und Setup-Anforderungen variieren je nach Angebot und Version. Vergleichen Sie die [Adobe Commerce-Plattformen und -Services](https://experienceleague.adobe.com/de/docs/commerce/information-center/explore-platforms-and-services/platform-and-services) bevor Sie eine Architektur auswählen.

## Commerce Storefront powered by Edge Delivery Services

Die von Edge Delivery Services unterstützte Commerce-Storefront bietet die Ebene für das Storefront-Erlebnis und die Bereitstellung von Inhalten. Dank der Headless-Architektur können Teams das Frontend unabhängig von der Commerce Foundation entwickeln. Die dokumentbasierte Erstellung und visuelle Bearbeitung unterstützen Inhaltsaktualisierungen, während Storefront-Komponenten Commerce-APIs für Shopping-Funktionen verwenden.

Unterscheiden Sie die Storefront-Oberfläche von den Systemen, die für Katalogdaten, Preise, Warenkorbvorgänge, Checkout und Bestellungen verantwortlich sind. Edge Delivery Services ersetzt nicht das Transaktions-Commerce-Backend. Identifizieren Sie die unterstützten Services und den Integrationspfad für Ihr ausgewähltes Backend, bevor Sie die Storefront implementieren.

Siehe die Dokumentation zur Commerce-Storefront [&#128279;](https://experienceleague.adobe.com/en/tools/commerce-storefront/).

## Integration und Erweiterbarkeit

API Mesh und App Builder helfen beim Verbinden und Erweitern von Commerce-Funktionen, ohne dass jede Anpassung in die Commerce-Kernanwendung eingebettet werden muss.

### API-Mesh

API Mesh für Adobe Developer App Builder kombiniert mehrere Adobe-, private und Drittanbieter-API-Quellen zu einem abfragbaren GraphQL-Endpunkt. Verwenden Sie sie, um Daten für Frontend-Erlebnisse zu erstellen und den Zugriff auf vorhandene Services zu koordinieren.

Die API-Komposition macht die Definition von API-Verträgen, Authentifizierung, Fehlerbehandlung oder Eigentümerschaft von transaktionaler Geschäftslogik nicht überflüssig. Halten Sie diese Verantwortlichkeiten im Integrationsentwurf explizit fest.

Siehe [API-Mesh-Übersicht](https://developer.adobe.com/graphql-mesh-gateway/).

### Adobe App Builder

Adobe App Builder bietet eine Plattform für Programme, die Adobe-Lösungen erweitern und auf Adobe-Infrastrukturen, einschließlich Adobe I/O Runtime, ausgeführt werden. Sie können ihn für prozessexterne Anpassungen und Integrationen mit Systemen wie CRM-Systemen, ERP-Systemen und PIMs verwenden.

Wählen Sie unterstützte Erweiterungspunkte, Ereignisse und Webhooks für das von Ihnen verwendete Commerce-Angebot aus. Entwerfen und testen Sie die Anwendung getrennt vom Core Commerce-Veröffentlichungslebenszyklus.

Siehe [Übersicht über App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/).

## Commerce-Entwicklungs-MCPs und -Kenntnisse

Commerce-Entwicklungs-MCPs und -Kenntnisse unterstützen die KI-unterstützte Entwicklung von App Builder-Anwendungen und Storefront-Anpassungen. Sie können auch dabei helfen, bestehende Adobe Commerce PHP-Erweiterungen beim Wechsel zu ACCS zu App Builder-Anwendungen zu migrieren.

MCP-Server (Model Context Protocol) verbinden kompatible KI-Codierungs-Clients mit Entwicklungs-Tools. Die Tools von Adobe umfassen die Tools Commerce Developer MCP Server, App Builder MCP Server und Dropins AI sowie Commerce-spezifische Fähigkeiten.

Commerce-Entwicklungs-MCPs sind Entwicklungs-Tools und keine Storefront-Versand-, Warenkorb-, Checkout- oder Auftragsverarbeitungs-Services. Sie machen eine Anwendung nicht automatisch mit jedem Commerce-Angebot kompatibel. Überprüfen Sie die generierten Änderungen und testen Sie sie mit der Zielumgebung.

Siehe [MCPs und Kenntnisse für die Entwicklung in Commerce](https://developer.adobe.com/commerce/extensibility/developer-agent/coding-tools).

## Planen einer zusammensetzbaren Implementierung

1. Definieren Sie Geschäftsziele, Kundenerlebnisse, Sicherheitsanforderungen und die für Ihr Team verfügbaren Fähigkeiten.
2. Wählen Sie die Commerce-Plattform aus und ermitteln Sie, welche vorhandenen Systeme beibehalten oder ersetzt werden sollen.
3. Wählen Sie eine unterstützte Storefront aus und definieren Sie die Grenzen zwischen Präsentation, Merchandising und Transaktions-Services.
4. Legen Sie Dateneigentum- und API-Verträge für Kataloginformationen, Preise, Inventar, Kunden, Warenkörbe, Checkout und Bestellungen fest.
5. Planen Sie Authentifizierung, Datensynchronisierung, Caching, Überwachung und Fehlerbehandlung über Integrationen hinweg.
6. Inkrementelle Implementierung und Validierung von Funktionalität, Leistung und Sicherheit vor jeder Version.

Eine zusammensetzbare Implementierung ist erfolgreich, wenn ihre Komponenten geschäftlichen Anforderungen entsprechen und zuverlässig zusammenarbeiten. Wählen Sie die benötigten Funktionen aus, anstatt Services hinzuzufügen, um die Architektur modularer zu gestalten.

## Verwandte Ressourcen

Sehen Sie sich diese Tutorials, Videos, Implementierungshandbücher und die Wiedergabeliste an, um Ihre Architektur zu planen und Commerce-Integrationen zu erstellen.

### Commerce-Plattformen und Storefronts

* [Architektur von Adobe Commerce as a Cloud Service](../commerce-as-a-cloud-service/architecture.md)
* [Zusammensetzbare Storefronts und modulare Architektur](../commerce-as-a-cloud-service/product-overview/composable-storefront-and-modular-architecture.md)
* [Übersicht über Adobe Commerce Optimizer](../adobe-commerce-optimizer/overview.md)
* [Warum das zusammenstellbare Katalogdatenmodell vorhanden ist](../adobe-commerce-optimizer/composable-catalog-data-model/why-ccdm-exists.md)
* [Kundenerlebnisse mit Edge Delivery Services](../edge-delivery-services/shopper-experience.md)

### Integration und Entwicklung

* [Out-of-Process-Erweiterbarkeit mit App Builder](../app-builder/foundations/introduction-to-app-builder.md)
* [Erste Schritte mit API-Mesh](../api-mesh/getting-started-api-mesh.md)
* [Erstellen eines API-Netzes mit mehreren Quellen](../api-mesh/graphql-multiple-source.md)
* [Erstellen benutzerdefinierter Versandraten mit KI- und MCP-Tools](../app-builder/custom-shipping-rates-ai-tools/ai-tools-starter-kit.md)

### Dokumentation zu Architektur und Entwicklung

* [Migrieren zu Adobe Commerce as a Cloud Service](https://experienceleague.adobe.com/de/docs/commerce/cloud-service/migration/overview)
* [Adobe Commerce Optimizer-Integrationen](https://experienceleague.adobe.com/de/docs/commerce/optimizer/integrations-overview)
* [Erste Schritte bei der Entwicklung einer Commerce-Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/)
* [Best Practices für MCPs und Kompetenzen in der Commerce-Entwicklung](https://developer.adobe.com/commerce/extensibility/developer-agent/best-practices)

### Wiedergabeliste

* [Erste Schritte mit API Mesh unter Verwendung von Adobe App Builder und Adobe Commerce](https://experienceleague.adobe.com/de/playlists/commerce-get-started-app-builder-and-api-mesh)
