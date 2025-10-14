---
title: So erstellt Adobe zusammensetzbare Commerce
description: Erfahren Sie mehr über zusammenstellbaren Commerce, Priorisierung eines API-First-Ansatzes und Implementierung einer modularen und Service-orientierten Architektur.
feature: App Builder, Saas
topic: Architecture, Commerce, Development, Headless, Integrations, Performance, Personalization
role: Admin, Architect, User
level: Beginner, Intermediate
doc-type: Tutorial
duration: 0
last-substantial-update: 2024-07-6
jira: KT-15730
exl-id: 4d811a2f-8488-4de7-babd-449aced42e3a
source-git-commit: 57082a851e508653ed9fcafd013a2201c8082873
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 0%

---

# Zusammensetzbarer Handel

Composable Commerce ist ein architektonischer Ansatz im E-Commerce, der die Entkopplung der Frontend-Präsentationsebene von der Backend-Commerce-Funktion beinhaltet. &#x200B; Es ermöglicht Unternehmen, die besten Komponenten oder Module auszuwählen und zu kombinieren, um eine individuelle Lösung zu erstellen. Dieser Ansatz beinhaltet die Aufschlüsselung der herkömmlichen monolithischen E-Commerce-Plattform in kleinere, unabhängige Services oder Microservices, die zusammen zusammengestellt werden können. Composable Commerce bietet Vorteile wie Flexibilität, Skalierbarkeit, Anpassung, Agilität und die Möglichkeit zur einfacheren Integration mit anderen Systemen und Technologien.

Adobe Commerce bietet viele Funktionen und Tools, mit denen Händler zusammenstellbaren Commerce annehmen und implementieren können. Adobe Commerce bietet eine zusammensetzbare Commerce-Methodik und hybride Headless- und Nicht-Headless-Frontend-Erlebnisse. Mit Blick auf die prozessexterne Erweiterbarkeit bietet Adobe API Mesh zur Integration mehrerer Services sowie Adobe App Builder zur Erstellung benutzerdefinierter Microservices.

## Warum ist Composable Commerce wichtig?

Das Verständnis des zusammensetzbaren Handels ist für Unternehmen und Einzelpersonen, die in der E-Commerce-Branche tätig sind, aus verschiedenen Gründen wichtig. Es bietet Flexibilität und Anpassung, Skalierbarkeit und Agilität, Integrationsfunktionen, Zukunftssicherheit und Entwicklerunterstützung. Composable Commerce ermöglicht es Unternehmen, ihre E-Commerce-Plattformen anzupassen und weiterzuentwickeln sowie ihre Geschäftstätigkeit zu skalieren und auszubauen. Zu den weiteren beeindruckenden Vorteilen zählen die Möglichkeit, mit anderen Systemen und Technologien zu integrieren, mit sich verändernden Kundenerwartungen Schritt zu halten und das Know-how von Entwicklern zu nutzen.

Es hilft Unternehmen, durch die sich entwickelnde E-Commerce-Landschaft zu navigieren, fundierte Entscheidungen zu treffen und die Vorteile von Flexibilität, Skalierbarkeit, Anpassung, Agilität und Integrationsfunktionen zu nutzen. Darüber hinaus ist das Wissen über Composable Commerce wichtig für Geschäftswachstum, Anpassung, Agilität und Innovation, Kosteneffizienz, Integration und Flexibilität und Zukunftssicherheit. Es bietet Unternehmen die Möglichkeit, sich schnell an neue Funktionen anzupassen, auf veränderte Marktbedingungen zu reagieren und hochgradig kundenspezifische Lösungen zu erstellen. Zu den weiteren Vorteilen zählen die Fähigkeit, Innovationen schnell umzusetzen, Entwicklungs- und Wartungskosten zu senken und in Services und Systeme von Drittanbietern zu integrieren.

Insgesamt ermöglicht das Verständnis von Composable Commerce Unternehmen, fundierte Entscheidungen zu treffen, ihre E-Commerce-Architektur und -Strategie zu optimieren und Wachstum und Erfolg im digitalen Markt zu fördern.

## Wie können Unternehmen von Composable Commerce profitieren?

Unternehmen können vom zusammenstellbaren Handel auf verschiedene Weise profitieren:

**Flexibilität und Anpassung:** Composable Commerce ermöglicht es Unternehmen, die besten Komponenten oder Microservices auszuwählen und zu kombinieren, um eine maßgeschneiderte E-Commerce-Lösung zu erstellen, die ihren spezifischen Anforderungen entspricht. Es ermöglicht Unternehmen, ihre Plattform so anzupassen, dass sie einzigartige Kundenerlebnisse bereitstellen, spezielle Funktionen implementieren und sich auf dem Markt abheben kann.

**Skalierbarkeit und Agilität:** Mit einer zusammensetzbaren Architektur können Unternehmen verschiedene Komponenten ihrer E-Commerce-Plattform unabhängig skalieren. Dies bedeutet, dass sie Ressourcen zuweisen und spezifische Funktionen auf der Grundlage der Nachfrage skalieren können, um eine optimale Leistung und Kosteneffizienz zu gewährleisten. Composable Commerce ermöglicht auch agile Entwicklungspraktiken, sodass Teams gleichzeitig an verschiedenen Komponenten arbeiten und Änderungen unabhängig bereitstellen können, was zu einer schnelleren Markteinführung führt.

**Integrationsfunktionen:** Composable Commerce ermöglicht die nahtlose Integration mit Systemen, Services und Technologien von Drittanbietern. Unternehmen können ihre E-Commerce-Plattform einfach mit verschiedenen Tools wie Zahlungs-Gateways, ERP-Systemen, CRM-Systemen, Marketing-Automatisierungsplattformen und mehr verbinden. Diese Integrationsfunktion ermöglicht es Unternehmen, die besten Lösungen zu nutzen und ein einheitliches Ökosystem zu schaffen, das die betriebliche Effizienz und das Kundenerlebnis verbessert.

**Zukunftssicher:** Composable Commerce bietet Unternehmen die Flexibilität, ihre E-Commerce-Plattform an sich verändernde Technologien und Markttrends anzupassen und weiterzuentwickeln. Es ermöglicht Unternehmen, Komponenten einfach hinzuzufügen oder zu ersetzen, neue Technologien zu integrieren und der Konkurrenz einen Schritt voraus zu sein. Diese Zukunftssicherheit stellt sicher, dass Unternehmen kontinuierlich innovativ sind und die sich verändernden Kundenerwartungen erfüllen können.

**Entwicklerbefähigung:** Composable Commerce bietet Entwicklern die Flexibilität, mit verschiedenen Technologien, Sprachen und Frameworks zu arbeiten. Es ermöglicht Entwicklern, sich auf bestimmte Komponenten oder Microservices zu konzentrieren, was eine Spezialisierung und Fachwissen ermöglicht. Diese Befähigung führt zu einer höheren Entwicklerproduktivität, schnelleren Entwicklungszyklen und der Möglichkeit, die neuesten Tools und Technologien zu nutzen.

Insgesamt ermöglicht Composable Commerce Unternehmen die Erstellung einer hochgradig flexiblen, skalierbaren und anpassbaren E-Commerce-Plattform, die sich an sich ändernde Geschäftsanforderungen anpassen kann, außergewöhnliche Kundenerlebnisse bereitstellt und Wachstum und Erfolg im digitalen Markt steigert.

## Welche Funktionen hat Adobe Commerce für zusammenstellbaren Commerce?

Adobe Commerce bietet verschiedene Funktionen, um Händler bei der Einführung und Implementierung von Composable Commerce zu unterstützen:

**Zusammensetzbare Commerce-Methode:** Adobe Commerce bietet eine zusammensetzbare Commerce-Methode, die Händlern beim Verständnis und der Implementierung der Prinzipien der zusammensetzbaren Architektur hilft. Diese Methode hilft Unternehmen, die Vorteile von Flexibilität, Skalierbarkeit und Anpassung zu nutzen und dabei Faktoren wie Komplexität, technische Reife und Projektgröße zu berücksichtigen.

**Funktionsumfang mit umfassenden Funktionen:** Adobe Commerce bietet über seine GraphQLAPI eine umfassende Reihe von Funktionen, auf die Sie zugreifen können. Mit dieser funktionsreichen Funktion können Händler die Anzahl der für ihren Commerce-Stack erforderlichen Anbieter minimieren und so die Time-to-Market-Herausforderungen reduzieren. Es ermöglicht Unternehmen eine schnellere Markteinführung und bietet gleichzeitig die Flexibilität, zusätzliche Services oder Funktionen von Drittanbietern zu erstellen und zu integrieren, während sich ihr Commerce-Stack weiterentwickelt.

**Hybride Frontend-Erlebnisse:** Adobe Commerce unterstützt sowohl Headless- als auch Nicht-Headless-Frontend-Erlebnisse innerhalb desselben Ökosystems. Diese Flexibilität ermöglicht es Händlern, den am besten geeigneten architektonischen Ansatz für jeden spezifischen Frontend-Anwendungsfall auszuwählen. Es ermöglicht einen schrittweisen Übergang zu einer Headless- und zusammensetzbaren Architektur, ohne dass das gesamte System gleichzeitig migriert werden muss.

**API Mesh:** API Mesh von Adobe Commerce vereinfacht die Integration mehrerer Microservices, Drittanbieter-Tools und Anwendungen in einen einheitlichen API-Endpunkt für Frontend-Entwickler. Damit können Entwicklerinnen und Entwickler mehrere Datenquellen zu einem einzigen GraphQL-Endpunkt kombinieren, was die Komplexität reduziert und die Entwicklung und Pflege neuer Funktionen und Erlebnisse optimiert.

**Adobe App Builder:** Adobe App Builder ist eine Server-lose Erweiterungsplattform, mit der Händler benutzerdefinierte Microservices erstellen, benutzerdefinierte Erlebnisse erstellen und Adobe-Lösungen erweitern können. Mit App Builder können Händler sichere und skalierbare Apps erstellen, die die native Funktionalität von Adobe Commerce erweitern und mit Lösungen von Drittanbietern integrieren. Dadurch entfällt die Notwendigkeit für Händler, eine eigene Infrastruktur für Anpassungen und Microservices zu erstellen und zu pflegen, wodurch die Komplexität reduziert und die Gesamtbetriebskosten gesenkt werden.

Diese von Adobe Commerce bereitgestellten Funktionen vereinfachen die Einführung und Implementierung von Composable Commerce und ermöglichen es Händlern, die Vorteile von Flexibilität, Skalierbarkeit, Anpassung und Integrationsfunktionen zu nutzen und gleichzeitig die Komplexität und den Entwicklungsaufwand zu reduzieren.

## Abschließende Gedanken

Composable Commerce ist ein architektonischer Ansatz im E-Commerce, der die Entkopplung der Frontend-Präsentationsebene von der Backend-Commerce-Funktion beinhaltet. Im Folgenden finden Sie die wichtigsten Erkenntnisse zum zusammensetzbaren Commerce:

**Architektur:** Composable Commerce folgt einer modularen und entkoppelten Architektur, die es Unternehmen ermöglicht, die besten Komponenten oder Microservices auszuwählen und zu kombinieren, um eine individuelle Lösung zu erstellen. Diese Architektur bietet Flexibilität, Skalierbarkeit und Flexibilität.

**Vorteile:** Composable Commerce bietet mehrere Vorteile, darunter Flexibilität und Anpassung, Skalierbarkeit und Agilität, Integrationsfunktionen, Zukunftssicherheit und Entwicklerunterstützung. Es ermöglicht Unternehmen, sich anzupassen, zu skalieren, zu integrieren, Innovationen zu entwickeln und Entwicklerwissen zu nutzen.

**Überlegungen:** Bei der Betrachtung von zusammensetzbarem Commerce sollten Faktoren wie Komplexität, interne technische Reife, Projektgröße und -struktur, Anpassung vs. Standardisierung, Gesamtbetriebskosten sowie Sicherheit und Datenschutz sorgfältig bewertet werden.

**Adobe Commerce:** Adobe Commerce bietet Funktionen und Tools, mit denen Händler zusammensetzbaren Commerce annehmen und implementieren können. Dazu gehören eine zusammenstellbare Commerce-Methodik, umfangreiche Funktionen, hybride Frontend-Erlebnisse, API Mesh für die Integration und Adobe App Builder für benutzerdefinierte Microservices.

**Geschäftsauswirkungen:** Composable Commerce ermöglicht Unternehmen die Erstellung einer hochgradig flexiblen, skalierbaren und anpassbaren E-Commerce-Plattform. Sie ermöglicht es ihnen, einzigartige Kundenerlebnisse bereitzustellen, auf der Grundlage der Nachfrage zu skalieren, in andere Systeme zu integrieren, ihren Betrieb zukunftssicher zu gestalten und Entwickler-Know-how zu nutzen.

Das Verständnis von Composable Commerce ist für Unternehmen in der E-Commerce-Branche von entscheidender Bedeutung, um wettbewerbsfähig zu bleiben, sich an sich ändernde Marktbedingungen anzupassen und außergewöhnliche Kundenerlebnisse bereitzustellen. Durch die Nutzung von Composable Commerce können Unternehmen die Vorteile von Flexibilität, Skalierbarkeit, Anpassung, Agilität und Integrationsfunktionen nutzen und so Wachstum und Erfolg im digitalen Markt steigern.
