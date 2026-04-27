---
title: Optimizing Code Reuse with Adobe Commerce
description: Learn how to optimize code reuse in Adobe Commerce with Global Reference Architecture patterns, enhancing performance and compliance across multiple instances.
kt: 15773
doc-type: tutorial
duration: 287
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
badge: label="Contributed by Tony Evers, Sr. Technical Architect, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony/" tooltip="Contributed by Tony Evers"
topic: Architecture, Commerce, Development
old-role: Architect, Developer
role: Developer, User, Leader
level: Beginner, Intermediate
exl-id: 5475ade8-028c-4b24-a563-60dcda5ba93a
TQID: https://experienceleague.adobe.com/1-cE8TS4syjsMuX3VmhQu5zhFX-z3yxV-GlwxVl7eqM
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b5f00040-57a0-4a6d-a39e-383b1936c2c9id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 1127
ht-degree: 0%

---

# Global Reference Architecture Implementation Techniques

{{only-for-on-prem-commerce-cloud}}

There are several ways to optimize code reuse with Adobe Commerce. These four implementation techniques each have their own advantages. The examples in this article are ordered from simple to more complex. Pick the strategy that best fits your project and future roadmap. A migration from one strategy to another can be time consuming.

## When to use Global Reference Architecture

Global reference architecture can be valuable, depending on the number of instances you own. An instance is a standalone installation of Adobe Commerce using its own database. Count the number of production databases to know how many instances you own. If you maintain more than one instance, or if you foresee this scenario in the future, you can benefit from global reference architecture. The more functionality the instances share, the more value a global reference architecture adds.

In any of these scenarios, it is advisable to explore using multiple instances of Adobe Commerce.

1. **Different Store Owners**: If you maintain code for multiple store owners, each with their own distinct store, separate instances may be needed to maintain their individual requirements effectively.
2. **Compliance with National Regulations**: Certain regulations mandate that customer data must be stored within specific regions. In such cases, separate instances are essential to ensure compliance with these regulations.
3. **Operational Variances Across Geographical Regions**: Operating in multiple regions may mean differing maintenance schedules and requirements. Using separate instances allows for flexibility in managing these variations efficiently.
4. **High-Intensity Flash Sales**: Stores conducting large-scale flash sales often require optimized server performance. Dedicated infrastructure provided by separate instances ensures optimal performance during such high-demand periods.
5. **Wesentliche Unterschiede zwischen Marken oder Ländern**: Wenn der Unterschied zwischen Marken oder Ländern groß ist, führt die Verwendung einer einzigen Instanz zu Code, der nur für einige Marken oder Länder verwendet wird. Separate Instanzen können die Leistung und Stabilität verbessern, indem unnötiger Code für Marken und Länder, die ihn nicht benötigen, entfernt wird.

## Globale Referenzarchitekturmuster

Neben „Kein GRA-Muster“ gibt es vier Arten von GRA-Mustern.

![5 Icons von GRA-Mustern: keine GRA, Split, Bulk, Separate und Monorepo.](/help/assets/global-reference-architecture/gra-patterns-horizontal.png){align="center"}

### Kein GRA-Muster

![Ein Symbol, das „kein GRA“ darstellt](/help/assets/global-reference-architecture/no-gra.png){align="center"}

Wenn kein GRA-Muster verwendet wird, ist jede Adobe Commerce-Instanz eine eindeutige Anwendung. Es gibt keine Wiederverwendung von Code, es sei denn, Code wird manuell von einer Instanz in eine andere verschoben. Diese Kopien weichen immer voneinander ab. Der Aufwand um sicherzustellen, dass jede Instanz dieselben Änderungen hat, aber dennoch wie erwartet funktioniert, kann überwältigend werden. In diesem Szenario benötigen drei Instanzen den dreifachen Wartungsaufwand einer Instanz.

![Ein Diagramm mit 3 Geschäften, wobei jeder eine Kopie des ersten ist, wobei eine einzigartige Entwicklung in allen 3 Kopien stattfindet.](/help/assets/global-reference-architecture/no-gra-pattern-diagram.png){align="center"}

### Das aufgeteilte Git-GRA-Muster

![Ein Symbol, das das „geteilte“ GRAA-Muster darstellt](/help/assets/global-reference-architecture/split-git.png){align="center"}

Dieses Muster besteht aus Git-Repositorys für die Entwicklung und einem Git-Repository pro Instanz. Jede Datei in der Instanz wird in einem der Entwicklungs-Repositorys verwaltet. Sie kommen als Zopf zusammen und bilden die ganze GRA. Jede Codezeile ist nur in einem einzigen Entwicklungs-Repository vorhanden und wird mithilfe der Fleding-Technik auf den Instanzen installiert, was zu einer Wiederverwendung von Code führt.

![Ein Diagramm, das zeigt, wo Code in einem aufgeteilten GRA-Muster gespeichert ist](/help/assets/global-reference-architecture/split-git-gra-pattern-diagram.png){align="center"}

### Das GRA-Muster für Massenpakete

![Ein Symbol für das „Massen“-GRA-Muster](/help/assets/global-reference-architecture/bulk-packages.png){align="center"}

Die Adobe Commerce-Kern- und Drittanbietermodule werden direkt über Composer-Repositorys installiert. Git-Repositorys können als Composer-Repositorys verwendet werden. Bei diesem Muster wird die gesamte gemeinsam genutzte GRA-Codebasis in einem oder mehreren Git-Repositorys gehostet und über Composer installiert. Das Hauptmerkmal ist, dass mehrere Module, Sprachpakete oder Themen in einem einzigen Composer-Paket gehostet werden, was die Entwicklung vereinfacht.

![Ein Diagramm, das zeigt, wo Code in einem Massen-Package-GRA-Muster gespeichert wird](/help/assets/global-reference-architecture/bulk-gra-pattern-diagram.png){align="center"}

### Die separaten Pakete GRAD-Muster

![Ein Symbol, das das GRA-Muster „Separate Packages“ darstellt](/help/assets/global-reference-architecture/separate-packages.png){align="center"}

Jedes Adobe Commerce-Modul, Sprachpaket oder Design wird als separates Composer-Paket installiert. Jede Anpassung verfügt über ein eigenes Git-Repository. Dies bedeutet ultimative Flexibilität bei der Komposition der Instanzen und verfügt über eine zuverlässige Composer-Abhängigkeitsverwaltung. Zur Leistungsoptimierung werden alle Pakete in einem einzigen privaten Composer-Repository gespiegelt.

![Ein Diagramm, das zeigt, wo Code in einem separaten Paket-GRA-Muster gespeichert wird](/help/assets/global-reference-architecture/separate-packages-gra-pattern-diagram.png){align="center"}

### Das monorepo GRA-Muster

![Ein Symbol für das „monorepo“-GRA-Muster](/help/assets/global-reference-architecture/monorepo.png){align="center"}

Die gesamte Entwicklung erfolgt in einem einzigen Code-Repository. Durch die Automatisierung werden Pakete für neue Versionen generiert und in einem Composer-Repository veröffentlicht. Das Muster kombiniert den geringen Entwicklungs-Overhead des Massenpaketansatzes mit der Flexibilität des separaten Paketansatzes. Das monorepo-Muster ist auch ideal für automatisierte Funktionstests.

![Ein Diagramm, das zeigt, wo Code in einem monorepo-GRA-Muster gespeichert wird](/help/assets/global-reference-architecture/monorepo-gra-pattern-diagram.png){align="center"}

## Auswählen eines GRA-Musters

Die Wahl für ein GRA-Muster wird getroffen, indem die Projektkomplexität, der Bedarf an Flexibilität und die Anpassungsfähigkeit des Entwicklungsteams bewertet werden.

Teams mit wenig Adobe Commerce-Erfahrung beginnen am besten einfach. Wenn das Projekt jedoch aufgrund seiner Eigenschaften ein komplexeres GRA-Muster erfordert, gehen Sie keine Kompromisse ein.

Allgemeine Projektmerkmale in Bezug auf jedes Muster:

1. **Kein GRA-Muster**: Einzelne Instanz von Adobe Commerce ohne Erweiterungspläne. Mehrere Instanzen von Adobe Commerce mit minimaler Gemeinsamkeit zwischen ihnen.

2. **Git-GRA-Muster aufteilen**: Teams, die Composer wegen ihrer Anpassungen vermeiden möchten, in den meisten Fällen ist das Muster für Massenpakete ein bevorzugtes Muster für Git-Aufspaltung.

3. **Massen-Paket-GRA-Muster**: Anpassungs-Code-Basis mit hoher Interdependenz. Instanzen haben alle sehr ähnliche Kombinationen benutzerdefinierter Pakete. Keine häufige Promotion oder Herabstufung einzelner Pakete. Teams mit wenig Erfahrung im Code-Management und Bedarf an Einfachheit.

4. **Separate packages GRA pattern**: Flexible Verwaltung des Veröffentlichungsumfangs erforderlich. In den nächsten fünf Jahren werden 50 oder weniger individuelle Pakete erwartet. Potenziell globale und regionale Ebenen des gemeinsamen Codes. Keine Pläne für die Migration zu einem Monorepo-Muster. Das Team ist technisch versiert und hält sich strikt an den Prozess.

5. **Monorepo GRA Muster**: Alle Eigenschaften der separaten Pakete GRA Muster. In den nächsten 5 Jahren werden mehr als 50 Pakete erwartet. Notwendigkeit umfassender automatisierter Tests. Unterstützung für temporäre Umgebungen. Komplexe Code-Basis für Unternehmen, die skaliert werden muss, ohne die Wartungskosten zu gleichen Kosten zu skalieren.

### Die Kosten einer falschen Wahl

Die Migration von einem Muster zum anderen ist möglich. Das folgende Diagramm zeigt die Auswirkungen des Wechsels von einem Muster zum anderen. Grüne Linien zeigen geringe Auswirkungen, gelbe und bernsteinfarbene Linien zeigen mäßig komplexe bis komplexe Migrationen.

![Ein Diagramm mit farbigen Pfeilen zwischen allen 4 GRA-Mustern, die den Schwierigkeitsgrad des Wechselns von einem zum anderen anzeigen.](/help/assets/global-reference-architecture/wrong-choice.png){align="center"}
