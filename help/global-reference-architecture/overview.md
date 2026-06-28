---
title: Optimieren der Wiederverwendung von Code mit Adobe Commerce
description: Erfahren Sie, wie Sie die Wiederverwendung von Code in Adobe Commerce mit Mustern der globalen Referenzarchitektur optimieren und so die Leistung und Compliance über mehrere Instanzen hinweg verbessern können.
jira: KT-15773
doc-type: Tutorial
duration: 284
last-substantial-update: 2025-01-06
feature: Best Practices, Configuration, Install
badge: label="Beiträge von Tony Evers, Sr. Technical Architect, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony" tooltip="Beiträge von Tony Evers"
topic: Architecture, Commerce, Development
role: Developer, User, Leader
level: Beginner, Intermediate
exl-id: 5475ade8-028c-4b24-a563-60dcda5ba93a
TQID: https://experienceleague.adobe.com/1-cE8TS4syjsMuX3VmhQu5zhFX-z3yxV-GlwxVl7eqM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 776428136218d5d3cf5b1720832798822039aee2
workflow-type: tm+mt
source-wordcount: 1116
ht-degree: 0%

---

# Implementierungstechniken der globalen Referenzarchitektur

{{only-for-on-prem-commerce-cloud}}

Es gibt mehrere Möglichkeiten, die Wiederverwendung von Code mit Adobe Commerce zu optimieren. Diese vier Implementierungstechniken haben jeweils ihre eigenen Vorteile. Die Beispiele in diesem Artikel sind von einfach bis komplexer sortiert. Wählen Sie die Strategie aus, die am besten zu Ihrem Projekt und Ihrer künftigen Roadmap passt. Die Migration von einer Strategie zur anderen kann zeitaufwendig sein.

## Verwendung der globalen Referenzarchitektur

Die globale Referenzarchitektur kann je nach der Anzahl der Instanzen, deren Inhaber Sie sind, von Nutzen sein. Eine Instanz ist eine eigenständige Installation von Adobe Commerce unter Verwendung einer eigenen Datenbank. Um zu erfahren, wie viele Instanzen Sie besitzen, zählen Sie die Anzahl der Produktionsdatenbanken. Wenn Sie mehr als eine Instanz verwalten oder dieses Szenario für die Zukunft vorhersehen, können Sie von der globalen Referenzarchitektur profitieren. Je mehr Funktionen die Instanzen gemeinsam nutzen, desto mehr Wert bietet eine globale Referenzarchitektur.

In jedem dieser Szenarien ist es ratsam, die Verwendung mehrerer Instanzen von Adobe Commerce zu untersuchen.

1. **Verschiedene Store-**: Wenn Sie Code für mehrere Store-Operatoren mit jeweils einem eigenen Store verwalten, sind separate Instanzen erforderlich, um die individuellen Anforderungen effektiv zu erfüllen.
2. **Einhaltung nationaler Vorschriften**: Bestimmte Vorschriften verlangen, dass Kundendaten in bestimmten Regionen gespeichert werden müssen. In solchen Fällen sind gesonderte Instanzen unerlässlich, um die Einhaltung dieser Vorschriften zu gewährleisten.
3. **Betriebliche Unterschiede zwischen geografischen Regionen**: Betrieb in mehreren Regionen bedeutet unterschiedliche Wartungspläne und -anforderungen. Die Verwendung separater Instanzen ermöglicht eine flexible und effiziente Verwaltung dieser Varianten.
4. **Flash-Verkäufe mit hoher Intensität**: Geschäfte, die Flash-Verkäufe in großem Umfang durchführen, benötigen oft eine optimierte Server-Leistung. Dedizierte Infrastruktur, die von separaten Instanzen bereitgestellt wird, sorgt für eine optimale Leistung in solchen Zeiten hoher Nachfrage.
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

Dieses Muster besteht aus Git-Repositorys für die Entwicklung und einem Git-Repository pro Instanz. Jede Datei in der Instanz wird in einem Entwicklungs-Repository gepflegt. Sie werden zu der gesamten GRA zusammengefasst. Jede Codezeile ist nur in einem einzigen Entwicklungs-Repository vorhanden und wird mithilfe der Fleding-Technik auf den Instanzen installiert, was zu einer Wiederverwendung von Code führt.

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

Bewerten Sie die Projektkomplexität, den Bedarf an Flexibilität und die Fähigkeit des Entwicklungsteams, sich an die Auswahl eines GRA-Musters anzupassen.

Teams mit wenig Adobe Commerce-Erfahrung beginnen am besten einfach. Wenn das Projekt jedoch aufgrund seiner Eigenschaften ein komplexeres GRA-Muster erfordert, gehen Sie keine Kompromisse ein.

Allgemeine Projektmerkmale in Bezug auf jedes Muster:

1. **Kein GRA-Muster**: Einzelne Instanz von Adobe Commerce ohne Erweiterungspläne. Mehrere Instanzen von Adobe Commerce mit minimaler Gemeinsamkeit zwischen ihnen.

2. **Git-GRA-Muster aufteilen**: Teams, die Composer wegen ihrer Anpassungen vermeiden möchten. In den meisten Fällen ist das Muster für Massenpakete ein bevorzugtes Muster für Git-Aufspaltungen.

3. **Massen-Paket-GRA-Muster**: Anpassungs-Code-Basis mit hoher Interdependenz. Instanzen haben sehr ähnliche Kombinationen benutzerdefinierter Pakete. Keine häufige Promotion oder Herabstufung einzelner Pakete. Teams mit wenig Erfahrung im Code-Management und einem Bedürfnis nach Einfachheit.

4. **Separate packages GRA pattern**: Flexible Verwaltung des Veröffentlichungsumfangs erforderlich. In den nächsten fünf Jahren werden 50 oder weniger individuelle Pakete erwartet. Potenziell globale und regionale Ebenen des gemeinsamen Codes. Keine Pläne für die Migration zu einem Monorepo-Muster. Das Team ist technisch versiert und hält sich strikt an den Prozess.

5. **Monorepo GRA Muster**: Alle Eigenschaften der separaten Pakete GRA Muster. In den nächsten 5 Jahren werden mehr als 50 Pakete erwartet. Notwendigkeit umfassender automatisierter Tests. Unterstützung für temporäre Umgebungen. Komplexe Code-Basis für Unternehmen, die skaliert werden muss, ohne die Wartungskosten zu gleichen Kosten zu skalieren.

### Die Kosten einer falschen Wahl

Die Migration von einem Muster zum anderen ist möglich. Das folgende Diagramm zeigt die Auswirkungen des Wechsels von einem Muster zum anderen. Grüne Linien zeigen geringe Auswirkungen, gelbe und bernsteinfarbene Linien zeigen mäßig komplexe bis komplexe Migrationen.

![Ein Diagramm mit farbigen Pfeilen zwischen allen 4 GRA-Mustern, die den Schwierigkeitsgrad des Wechselns von einem zum anderen anzeigen.](/help/assets/global-reference-architecture/wrong-choice.png){align="center"}
