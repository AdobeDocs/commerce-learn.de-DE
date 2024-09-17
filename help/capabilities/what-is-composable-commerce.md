---
title: Wie Adobe Composable Commerce erstellt
description: Erfahren Sie mehr über Composable Commerce, die Priorisierung eines API-First-Ansatzes und die Implementierung einer modularen und dienstorientierten Architektur.
feature: App Builder, Saas
topic: Architecture, Commerce, Development, Headless, Integrations, Performance, Personalization
role: Admin, Architect, User
level: Beginner, Intermediate
doc-type: Tutorial
duration: 0
last-substantial-update: 2024-06-27T00:00:00Z
jira: KT-15730
exl-id: 4d811a2f-8488-4de7-babd-449aced42e3a
source-git-commit: d578c066f3e51827694c8bf85aa2324035a8b07b
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 0%

---

# Kompossiver Handel

Composable Commerce ist ein architektonischer Ansatz im E-Commerce, der die Entkopplung der Front-End-Präsentationsschicht von der Back-End-Commerce-Funktion umfasst. &#x200B; So können Unternehmen die besten Komponenten oder Module auswählen und kombinieren, um eine angepasste Lösung zu erstellen. Dieser Ansatz beinhaltet die Unterteilung der traditionellen monolithischen E-Commerce-Plattform in kleinere, unabhängige Dienste oder Microservices, die zusammengestellt werden können. Composable Commerce bietet Vorteile wie Flexibilität, Skalierbarkeit, Anpassung, Agilität und die Möglichkeit einer einfacheren Integration in andere Systeme und Technologien.

Adobe Commerce bietet zahlreiche Funktionen und Werkzeuge zur Unterstützung von Händlern bei der Übernahme und Implementierung von Composable Commerce. Adobe Commerce bietet eine kombinierbare Commerce-Methodik und hybride Headless- und Nicht-Headless-Frontend-Erlebnisse. Mit Blick auf die Out-of-Process-Erweiterbarkeit bietet Adobe API-Mesh zur Integration mehrerer Dienste und Adobe App Builder zur Erstellung benutzerdefinierter Microservices.

## Warum ist der kombinierte Handel wichtig?

Das Verständnis des kombinierbaren Handels ist für Unternehmen und Einzelpersonen, die in der E-Commerce-Industrie tätig sind, aus verschiedenen Gründen wichtig. Es bietet Flexibilität und Anpassung, Skalierbarkeit und Agilität, Integrationsfunktionen, Zukunftssicherung und Entwicklerunterstützung. Der kombinierte Handel ermöglicht es Unternehmen, ihre E-Commerce-Plattformen anzupassen und weiterzuentwickeln, ihre Geschäftstätigkeit zu skalieren und zu erweitern. Zu den beeindruckenderen Vorteilen zählen die Möglichkeit, sich in andere Systeme und Technologien zu integrieren, mit den sich entwickelnden Kundenerwartungen Schritt zu halten und das Know-how der Entwickler zu nutzen.

Es hilft Unternehmen, in der sich entwickelnden E-Commerce-Landschaft zu navigieren, fundierte Entscheidungen zu treffen und die Vorteile von Flexibilität, Skalierbarkeit, Anpassung, Agilität und Integrationsfunktionen zu nutzen. Darüber hinaus ist das Wissen über den kombinierbaren Handel für Unternehmenswachstum, Anpassung, Agilität und Innovation, Kosteneffizienz, Integration und Flexibilität sowie Zukunftssicherung wichtig. Es ermöglicht Unternehmen die Möglichkeit, sich schnell an neue Funktionen anzupassen und auf sich ändernde Marktbedingungen zu reagieren und hochgradig angepasste Lösungen zu entwickeln. Zu den weiteren Vorteilen zählen die Fähigkeit, schnell zu innovieren, Entwicklungs- und Wartungskosten zu senken und in Dienste und Systeme von Drittanbietern zu integrieren.

Insgesamt ermöglicht das Verständnis des kombinierbaren Handels Unternehmen, fundierte Entscheidungen zu treffen, ihre E-Commerce-Architektur und -Strategie zu optimieren und Wachstum und Erfolg auf dem digitalen Markt zu fördern.

## Wie können Unternehmen von dem kombinierten Handel profitieren?

Unternehmen können vom kombinierbaren Handel auf verschiedene Weise profitieren:

**Flexibilität und Anpassung:** Der kombinierbare Handel ermöglicht es Unternehmen, die besten Komponenten oder Microservices auszuwählen und zu kombinieren, um eine angepasste E-Commerce-Lösung zu erstellen, die ihren spezifischen Anforderungen entspricht. Sie ermöglicht es Unternehmen, ihre Plattform so anzupassen, dass sie einzigartige Kundenerlebnisse bieten, spezialisierte Funktionen implementieren und sich auf dem Markt differenzieren können.

**Skalierbarkeit und Flexibilität:** Mit einer zusammenstellbaren Architektur können Unternehmen verschiedene Komponenten ihrer E-Commerce-Plattform unabhängig skalieren. Dadurch können sie Ressourcen zuweisen und spezifische Funktionen bedarfsorientiert skalieren, um eine optimale Leistung und Kosteneffizienz zu gewährleisten. Der kombinierbare Handel ermöglicht auch agile Entwicklungspraktiken, sodass Teams gleichzeitig an verschiedenen Komponenten arbeiten und Änderungen unabhängig voneinander bereitstellen können, was zu einer schnelleren Time-to-Market führt.

**Integrationsfunktionen:** Der zusammengesetzte Handel ermöglicht die nahtlose Integration mit Drittanbietersystemen, -diensten und -technologien. Unternehmen können ihre E-Commerce-Plattform einfach mit verschiedenen Tools wie ZahlungsGateways, ERP-Systemen, CRM-Systemen, Marketing-Automatisierungsplattformen und mehr verbinden. Diese Integrationsfunktion ermöglicht es Unternehmen, die besten Lösungen zu nutzen und ein einheitliches Ökosystem zu schaffen, das die betriebliche Effizienz und das Kundenerlebnis verbessert.

**Zukunftssicherung:** Der Composable Commerce bietet Unternehmen die Flexibilität, ihre E-Commerce-Plattform anzupassen und weiterzuentwickeln, wenn sich Technologie- und Markttrends ändern. Unternehmen können damit problemlos Komponenten hinzufügen oder ersetzen, neue Technologien integrieren und dem Wettbewerb voraus bleiben. Diese zukunftssichere Funktion stellt sicher, dass Unternehmen kontinuierlich innovativ sind und sich wandelnde Kundenerwartungen erfüllen können.

**Entwicklerbefähigung:** Kompositioneller Commerce ermöglicht Entwicklern die Flexibilität, mit verschiedenen Technologien, Sprachen und Frameworks zu arbeiten. Dadurch können sich Entwickler auf bestimmte Komponenten oder Microservices konzentrieren und so Spezialisierung und Fachwissen ermöglichen. Diese Ermächtigung führt zu erhöhter Entwicklerproduktivität, schnelleren Entwicklungszyklen und der Fähigkeit, die neuesten Tools und Technologien zu nutzen.

Insgesamt ermöglicht der kombinierbare Handel Unternehmen die Erstellung einer hochflexiblen, skalierbaren und anpassbaren E-Commerce-Plattform, die sich an die sich ändernden Geschäftsanforderungen anpassen, außergewöhnliche Kundenerlebnisse bereitstellen und Wachstum und Erfolg im digitalen Markt fördern kann.

## Welche Funktionen hat Adobe Commerce für den kombinierten Handel?

Adobe Commerce bietet verschiedene Funktionen zur Unterstützung von Händlern bei der Übernahme und Implementierung von Composable Commerce:

**Composable Commerce Methodology:** Adobe Commerce bietet eine zusammenstellbare Commerce-Methode, die Händlern beim Verständnis und bei der Umsetzung der Prinzipien der Komponentenarchitektur hilft. Diese Methode hilft Unternehmen dabei, die Vorteile von Flexibilität, Skalierbarkeit und Anpassung zu nutzen und dabei Faktoren wie Komplexität, technische Reife und Projektgröße zu berücksichtigen.

**Funktionen mit hohem Funktionsumfang:** Adobe Commerce bietet einen umfassenden Funktionsumfang, auf den über seine GraphQLAPI zugegriffen werden kann. Diese funktionsreiche Funktion ermöglicht es Händlern, die Anzahl der Anbieter zu minimieren, die in ihrem Commerce-Stack erforderlich sind, und so die Zeit bis zur Markteinführung zu verkürzen. Sie ermöglicht es Unternehmen, schneller zu starten und gleichzeitig die Flexibilität zu erhalten, zusätzliche Drittanbieterdienste oder -funktionen zu erstellen und zu integrieren, während sich ihr Commerce-Stack entwickelt.

**Hybride Frontend-Erlebnisse:** Adobe Commerce unterstützt sowohl Headless- als auch Nicht-Headless-Frontend-Erlebnisse innerhalb desselben Ökosystems. Diese Flexibilität ermöglicht es Händlern, für jeden Frontend-Anwendungsfall den am besten geeigneten architektonischen Ansatz zu wählen. Sie ermöglicht einen schrittweisen Übergang zu einer Headless- und Composable-Architektur ohne gleichzeitige Migration des gesamten Systems.

**API-Mesh:** Adobe Commerces API-Mesh vereinfacht die Integration mehrerer Microservices, Drittanbieter-Tools und Anwendungen in einen einheitlichen API-Endpunkt für Frontend-Entwickler. Dadurch können Entwickler mehrere Datenquellen zu einem einzigen GraphQL-Endpunkt kombinieren, was die Komplexität reduziert und die Entwicklung und Pflege neuer Funktionen und Erlebnisse optimiert.

**Adobe App Builder:** Adobe App Builder ist eine Server-lose Erweiterbarkeitsplattform, mit der Händler benutzerdefinierte Microservices erstellen, benutzerdefinierte Erlebnisse erstellen und Adobe-Lösungen erweitern können. Mit App Builder können Händler sichere und skalierbare Apps erstellen, die die native Funktionalität von Adobe Commerce erweitern und in Lösungen von Drittanbietern integrieren. Dadurch entfällt die Notwendigkeit, dass Händler ihre eigene Infrastruktur für Anpassungen und Microservices aufbauen und pflegen, wodurch die Komplexität verringert und die Gesamtbetriebskosten gesenkt werden.

Diese von Adobe Commerce bereitgestellten Funktionen vereinfachen die Übernahme und Implementierung von Composable Commerce. So können Händler die Vorteile von Flexibilität, Skalierbarkeit, Anpassung und Integrationsfunktionen nutzen und gleichzeitig die Komplexität und den Entwicklungsaufwand reduzieren.

## Abschließende Gedanken

Composable Commerce ist ein architektonischer Ansatz im E-Commerce, der die Entkopplung der Front-End-Präsentationsschicht von der Back-End-Commerce-Funktion umfasst. Hier finden Sie die wichtigsten Erkenntnisse zum kombinierbaren Handel:

**Architektur:** Der Composable Commerce folgt einer modularen und entkoppelten Architektur, die es Unternehmen ermöglicht, die besten Komponenten oder Microservices auszuwählen und zu kombinieren, um eine angepasste Lösung zu erstellen. Diese Architektur bietet Flexibilität, Skalierbarkeit und Agilität.

**Vorteile:** Composable Commerce bietet verschiedene Vorteile, darunter Flexibilität und Anpassung, Skalierbarkeit und Agilität, Integrationsfunktionen, Zukunftssicherung und Entwicklerunterstützung. Sie ermöglicht Unternehmen die Anpassung, Skalierung, Integration, Innovation und Nutzung von Entwicklerwissen.

**Überlegungen:** Bei der Erwägung von Composable Commerce sollten Faktoren wie Komplexität, interner technischer Reifegrad, Projektgröße und -struktur, Anpassung vs. Standardisierung, Gesamtbetriebskosten sowie Sicherheit und Datenschutz sorgfältig bewertet werden.

**Adobe Commerce:** Adobe Commerce bietet Funktionen und Werkzeuge zur Unterstützung von Händlern bei der Übernahme und Implementierung von Composable Commerce. Dazu gehören eine zusammenstellbare Commerce-Methode, funktionsreiche Funktionalität, hybride Frontend-Erlebnisse, API-Mesh für die Integration und Adobe App Builder für benutzerdefinierte Microservices.

**Geschäftliche Auswirkungen:** Der kombinierbare Handel ermöglicht es Unternehmen, eine hochgradig flexible, skalierbare und anpassbare E-Commerce-Plattform zu erstellen. Sie ermöglicht es ihnen, einzigartige Kundenerlebnisse bereitzustellen, bedarfsgerecht zu skalieren, in andere Systeme zu integrieren, ihre Vorgänge zukunftssicher zu gestalten und Entwickler-Know-how zu nutzen.

Das Verständnis des kombinierbaren Handels ist für Unternehmen in der E-Commerce-Branche von entscheidender Bedeutung, um wettbewerbsfähig zu bleiben, sich an sich ändernde Marktbedingungen anzupassen und außergewöhnliche Kundenerlebnisse zu bieten. Durch die Nutzung von Composable Commerce können Unternehmen die Vorteile von Flexibilität, Skalierbarkeit, Anpassung, Agilität und Integrationsfunktionen nutzen und so Wachstum und Erfolg auf dem digitalen Markt fördern.
