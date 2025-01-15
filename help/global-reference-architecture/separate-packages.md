---
title: Separate Packages Globale Referenzarchitektur
description: Optimieren Sie Adobe Commerce mit separaten GRA-Paketen. Informationen zu Setup, Vorteilen und Best Practices für die flexible, versionierte Paketverwaltung.
kt: 16727
doc-type: tutorial
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
topic: Architecture, Commerce, Development
badge: label="Beiträge von Tony Evers, Sr. Technical Architect, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony/" tooltip="Beiträge von Tony Evers"
role: Architect, Developer, User, Leader
level: Beginner, Intermediate
exl-id: cbddc4a3-602f-4208-85cd-b906d2b81f8b
source-git-commit: dacd43ef84dcb2c2633221a90642a469b2ff5a30
workflow-type: tm+mt
source-wordcount: '2101'
ht-degree: 0%

---

# Das Muster der globalen Referenzarchitektur für separate Pakete

In diesem Handbuch wird erläutert, wie Sie Adobe Commerce mit dem GRA-Muster (Separate Packages Global Reference Architecture) einrichten.

Das GRA-Muster für separate Pakete umfasst ein Git-Repository für jedes gemeinsame Paket und ein Git-Repository für jede Adobe Commerce-Instanz. Häufige Pakete werden über Composer mit einem privaten Composer-Repository bereitgestellt.

Dieses globale Referenzarchitekturmuster basiert vollständig auf Composer und wurde entwickelt, um den maximalen Nutzen aus allen Composer-Funktionen zu ziehen.

![Ein Diagramm, das zeigt, wo Code in einem separaten Pakete-GRA-Muster gespeichert wird](/help/assets/global-reference-architecture/separate-packages-gra-pattern-diagram.png){align="center"}

## Vor- und Nachteile dieses Musters

Vorteile:

- Wiederverwendung von Code durch gemeinsam genutzte Code-Repositorys
- Vollständige Flexibilität bei der Paketinstallation. Jedes GRA-Paket kann einzeln aktualisiert, heruntergestuft oder rückportiert werden
- Vollständige Unterstützung der semantischen Versionierung
- Keine speziellen Tools, keine komplexe Infrastruktur oder spezielle Verzweigungsstrategie erforderlich
- Unterstützung aller von Composer unterstützten Pakettypen

Nachteile:

- Die Entwicklung innerhalb dieses GRA-Musters ist am Anfang etwas schwieriger, es gibt eine kleine Lernkurve
- Mögliche Kombinationen von Paketen bereitzustellen, die nicht in derselben Konfiguration entwickelt wurden, erfordern strenge Testverfahren

## Einrichten von Adobe Commerce mit dem separaten Package GRA-Muster

### Die Verzeichnisstruktur

Die endgültige Verzeichnisstruktur einer vollständigen Adobe Commerce-Installation mit dem separaten Package-GRA-Muster sieht wie folgt aus:

```text
.
├── app/
│   └── etc/
│       └── config.php
├── composer.json
└── composer.lock
```

Die `app/code`-, `app/i18n`- und `app/design`-Verzeichnisse werden absichtlich weggelassen. Die separaten Pakete GRAA installiert jedes einzelne Paket von Composer. Auch wenn das Paket nur in einer einzigen Adobe Commerce-Instanz installiert ist.

### Vorbereiten des Speicher-Repositorys

Erstellen Sie ein Repository für die erste Adobe Commerce-Instanz, die einen Webstore für Brand X darstellt.

```bash
mkdir gra-separate-brand-x
cd gra-separate-brand-x
composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition .
git init
git remote add origin git@github.com:AntonEvers/gra-separate-brand-x.git 
git add composer.json composer.lock
git commit -m 'initialize Brand X repository'
git push -u origin main
```

Installieren von Adobe Commerce mit `bin/magento setup:install`. Bestätigen Sie die resultierende `app/etc/config.php`.

### Erstellen von Paket-Repositorys

Jedes Paket in diesem globalen Referenzarchitekturmuster verfügt über ein eigenes Git-Repository. Im Folgenden finden Sie Beispielpakete mit Adobe Commerce-Modulen, die ein GRA-Modul, ein Drittanbietermodul und ein lokales Modul darstellen.

- <https://github.com/AntonEvers/module-example-gra>
- <https://github.com/AntonEvers/module-example-3rdparty>
- <https://github.com/AntonEvers/module-example-local>

Verwenden Sie die Beispiele, um Ihre eigenen Pakete zu erstellen.

### Erstellen von Metapaket-Repositorys

Metapakete steuern den Umfang der gemeinsamen GRA-Codebasis in diesem GRA-Muster. Sie definieren, was in der Foundation enthalten ist: welche Kombination von Paketversionen werden immer zusammen installiert. Ein Beispiel:

```json
{
    "name": "antonevers/gra-meta-foundation",
    "type": "metapackage",
    "require": {
        "antonevers/gra-component-foundation": "~1.0",
        "antonevers/module-gra": "~1.0",
        "antonevers/module-3rdparty": "~1.0",
        "magento/composer-dependency-version-audit-plugin": "~0.1",
        "magento/composer-root-update-plugin": "~2.0",
        "magento/product-enterprise-edition": "2.4.6-p3"
    }
}
```

Das obige Snippet ist composer.json eines Metapakets. Da Metapakete nur eine composer.json-Datei und keinen anderen Code enthalten. Der obige Code ist auch das vollständige Metapaket. Hosten Sie sie in einem Git-Repository und Sie verfügen über ein installierbares Metapaket-Composer-Repository. Dazu sind ein Beispiel-GRA-Modul und ein Drittanbietermodul sowie das Adobe Commerce-Kernmodul erforderlich. Dazu ist auch die gra-component-foundation erforderlich, die im nächsten Kapitel erläutert wird.

Metapakete sind eine Möglichkeit, Pakete zu bündeln, ohne Abhängigkeiten zwischen den Paketen zu erstellen. Selbst wenn keine technische Abhängigkeit zwischen Paketen besteht, können Sie mit einem Metapaket bewirken, dass diese zusammen installiert werden. Wenn Sie dieses Metapaket in Ihrem Projekt benötigen, werden alle Pakete oder Metapakete installiert, die für das Metapaket erforderlich sind. Wenn Sie also ein leeres Composer-Projekt erstellen und nur dieses Paket benötigen, installiert Composer Adobe Commerce und das GRA- und Drittanbietermodul.

Auf diese Weise können Sie sicherstellen, dass jeder Store denselben Satz von grundlegenden Paketen enthält.

Sie können auf ähnliche Weise ein Metapaket definieren, das Store x definiert. Dazu wird das Foundation-Metapaket, die vollständige GRA-Foundation sowie ein lokales Modul benötigt:

```json
{
    "name": "antonevers/gra-meta-brand-x",
    "type": "metapackage",
    "require": {
        "antonevers/gra-meta-foundation": "~1.0",
        "antonevers/module-local": "~1.0"
    }
}
```

Das Brand-X-Metapaket ist optional. Sie können auch das Brand Metapaket überspringen und diese Abhängigkeiten direkt in Ihrem Store Composer-Projekt benötigen. Der Vorteil eines Metapakets für lokale Module besteht darin, dass Sie keine Funktionsverzweigungen und Funktions-Pull-Anforderungen im Git-Repository des Speichers haben, nur in den Paket-Repositorys. Es handelt sich um eine Sicherheitsmaßnahme. Darüber hinaus können Sie semantische Versionen auf die Paket-Repositorys anwenden und verschiedene Git-Tags auf Ihrem Hauptprojekt verwenden, z. B. um benannte Versionen zu verfolgen. Es liegt an dir.

### GRA Foundation-Dateien außerhalb des Anbieterverzeichnisses

Manchmal müssen Dateien außerhalb des Anbieterverzeichnisses gespeichert werden. Dateien, die sich im `dev/`-Verzeichnis befinden, oder Domain-Überprüfungsdateien, z. B. `.gitignore`. Der Pakettyp „magento2-component“ ist für diesen Zweck konzipiert. Schauen Sie sich <https://github.com/AntonEvers/gra-component-foundation> an.

```json
{
    "name": "antonevers/gra-component-foundation",
    "type": "magento2-component",
    "require": {
        "magento/magento-composer-installer": "*"
    },
    "extra": {
        "map": [
            [
                "src/gitignore",
                ".gitignore"
            ]
        ]
    }
}
```

Dieses Paket hat den Typ magento2-component und es enthält einen src-Ordner, der Dateien hostet, die in den Adobe Commerce-Stammordner kopiert werden. Die Zuordnung in dieser Datei kopiert `/src/gitignore` nach `/.gitignore` im Hauptprojekt von Composer.

Auf diese Weise können Sie Dateien außerhalb des Anbieterverzeichnisses auch zu einem Teil Ihrer GRA-Foundation machen.

### Entwickeln eines GRA Foundation-Moduls

Die Entwicklung erfolgt innerhalb des Anbieterverzeichnisses. Bitten Sie Composer, Ihre Foundation-Pakete aus der Quelle zu installieren. Checkt dabei Pakete aus Git aus, anstatt sie aus einem heruntergeladenen Archiv zu installieren.

```bash
rm -r vendor/antonevers/*
composer install --prefer-source
```

Mit diesem Befehl wurden Pakete im Namespace „antonevers“ mit Git ausgecheckt. Wenn Sie den Ordner Vendor/Antonevers/module-gra aufrufen, gelangen Sie auch in das Git-Repository „module-gra“. Sie können jetzt Verzweigungen direkt aus dem Anbieterverzeichnis erstellen, auschecken und zusammenführen und auf diese Weise entwickeln.

### Einbinden von Drittanbietermodulen in die GRA Foundation

Fügen Sie dem GRA-Metapaket Pakete von Drittanbietern hinzu. Wenn kein Drittanbieter-Code verfügbar ist, um ihn aus einem Composer-Repository zu installieren, erstellen Sie ein Paket dafür. Erstellen Sie ein Git-Repository, fügen Sie die Paketinhalte hinzu (alles, was in app/code/vender/package enthalten sein würde) und stellen Sie sicher, dass sich eine gültige Datei „composer.json“ im Stammverzeichnis des Repositorys befindet. Sie können dieses Paket jetzt über Composer installieren.

## Einrichten eines privaten Composer-Repositorys

Ein privates Repository ist in der globalen Referenzarchitektur nicht obligatorisch. Dadurch werden Bereitstellungen und Installationen beschleunigt, die Repository-Konfiguration in composer.json wird reduziert und die Sicherheit erhöht. Anmeldeinformationen für andere Composer-Repositorys und den Adobe Commerce-Marketplace werden in Ihrem privaten Repository gespeichert. Keine sensiblen Anmeldeinformationen mehr im Paket mit dem Code oder auf den Computern der Entwickler.

Darüber hinaus bieten einige private Repositorys zusätzliche Funktionen wie E-Mail-Benachrichtigungen, wenn einer Ihrer Stores eine Sicherheitslücke in einer seiner Abhängigkeiten aufweist.

Das Problem der Langsamkeit tritt auf, wenn mehrere VCS-Repositorys in composer.json vorhanden sind. Jedes Composer-Repository muss bei Upgrades gelesen werden und mit 50 Repositorys für 50 Pakete mindestens den 50-fachen Mehraufwand für nur ein einzelnes Composer-Repository aufweisen.

![Ein Diagramm, das zeigt, wo eine Langsamkeit auftritt, wenn ein Composer-Repository fehlt](/help/assets/global-reference-architecture/separate-packages-without-mirror-diagram.png){align="center"}

Schließen Sie einen Composer-Mirror in Form eines privaten Composer-Repositorys ein. Die Spiegelung enthält eine Kopie aller Pakete aus anderen Composer-Repositorys sowie aller gehosteten Git-Pakete. Mit einem privaten Composer-Repository erhalten Sie zusätzlich eine differenzierte Zugriffskontrolle.

Bei der Git-Synchronisierung erkennt ein privates Composer-Repository automatisch neue Pakete in Ihren Git-Repositorys sowie neue Versionen vorhandener Pakete.

Mit Satis: <https://composer.github.io/satis/> können Sie Ihr eigenes privates Repository hosten. Ein Beispiel für ein öffentliches Repository finden Sie unter <https://antonevers.github.io/gra-composer-repository/>. Dieses Repository wird in den Code-Beispielen als Composer-Repository verwendet. Es sind zusätzliche Maßnahmen erforderlich, um ein Satis-Repository privat zu machen.

Es gibt Lösungen, die man konfigurieren und vergessen kann: Private Packagist <https://packagist.com/>, die von den gleichen Leuten gemacht wird, die Composer oder JFrog Artifactory <https://jfrog.com/artifactory/> geschrieben haben.

## Versandcode

Bei Metapaketen gibt es 3 Schritte, um Code bereitzustellen.

1. Änderungen in Pakete zusammenführen und die geänderten Pakete versionieren.
2. (Optional, nur wenn neue Pakete hinzugefügt werden) Erfordert die neuen Pakete in den Metapaketen und Version der Metapakete.
3. (Optional, nur wenn neue Pakete hinzugefügt werden) Die neuen Metapakete in Adobe Commerce erfordern und bereitstellen.

Der Bereitstellungsumfang wird mit Paketversionen gesteuert. Die Erstellung einer stabilen Version eines Pakets bedeutet, dass dieses Paket für die Produktionsbereitstellung bereit ist.

Um eine neue Version zu erstellen, führen Sie das Composer-Update im Haupt-Composer-Projekt aus, das die vollständige Store-Installation enthält. Alle aktuellen Versionen von Paketen werden installiert.

## Versionierung

Die Versionierung in einem separaten Paket-GRA ist ein Synonym für Tagging-Module in Git. Git-Tags erstellen nummerierte Versionen Ihrer Pakete, die Composer installiert.
Mit dem richtigen Versionierungsansatz können Ihre Pakete automatisch fließen, ohne dass die Sicherheit beeinträchtigt wird.

Zwei Beispiele:

```json
{
    "name": "antonevers/gra-meta-foundation",
    "type": "metapackage",
    "require": {
        "antonevers/gra-component-foundation": "1.1.4",
        "antonevers/module-gra": "1.0.0",
        "antonevers/module-3rdparty": "1.3.89"
    }
}
```

Dieses Beispiel zeigt eine strenge Definition von Abhängigkeiten. 3 Pakete sind in exakten Versionen erforderlich. Composer-Update mit diesem Metapaket in Ihrer Installation tut nichts. Es installiert diese 3 Pakete immer genau in diesen Versionen, auch wenn eine neuere Version verfügbar ist.

```json
{
    "name": "antonevers/gra-meta-foundation",
    "type": "metapackage",
    "require": {
        "antonevers/gra-component-foundation": "~1.0",
        "antonevers/module-gra": "~1.0",
        "antonevers/module-3rdparty": "~1.0"
    }
}
```

Dieses Beispiel zeigt eine lockere Definition von Abhängigkeiten. Mit `~1.0` kann jede Version dieser Pakete installiert werden, wenn sie größer oder gleich `1.0.0` und kleiner als `2.0.0` sind, mit einer Präferenz für die höchste verfügbare Version. Weitere Informationen zum Definieren von Versionsabhängigkeiten finden Sie unter <https://getcomposer.org/doc/articles/versions.md>:

> Der Operator ~ lässt sich am besten anhand eines Beispiels erklären: `~1.2` entspricht `>=1.2 <2.0.0`, während `~1.2.3` gleich `>=1.2.3 <1.3.0` ist.

Sobald Sie eine neue Version eines der genannten Pakete veröffentlichen, wird diese automatisch mit dem Composer-Update installiert.

Anwenden der semantischen Versionierung. Alles über die semantische Versionierung erfahren Sie auf <https://semver.org/>. Vor allem die FAQ ist ein Muss zu lesen. Bei semantischer Versionierung werden die Zahlen in „1.0.0“ MAJOR.MINOR.PATCH genannt. Nebenversionen und Patch-Versionen eines Pakets sollten sicher eingeführt werden, ohne die Anwendung zu beschädigen.
Sie können automatisch Patches einbeziehen und kleinere Upgrades manuell auswählen. Beachten Sie, dass dies zusätzlichen Aufwand verursacht, wenn Sie jede kleinere Änderung manuell auswählen:

```json
{
    "name": "antonevers/gra-meta-foundation",
    "type": "metapackage",
    "require": {
        "antonevers/gra-component-foundation": "~1.1.0",
        "antonevers/module-gra": "~1.0.0",
        "antonevers/module-3rdparty": "~1.3.0"
    }
}
```

All dies funktioniert natürlich nur, wenn Sie die semantische Versionierung immer konsequent anwenden. Und nicht nur in Metapaketen, sondern die Anforderungen Ihrer regulären Pakete sollten Abhängigkeiten auch lose definieren. Wenn Sie eine strikte Abhängigkeit in Ihrem System haben, ist dieses Paket auf die strikte Definition beschränkt.

Suchen Sie diese strikten Abhängigkeiten, indem Sie „composer depends \&lt;Paketname\>&quot; eingeben. Weitere Informationen finden Sie unter <https://getcomposer.org/doc/03-cli.md#depends-why> .

## Verzweigungsstrategie

Sie können verschiedene Verzweigungsstrategien verwenden, um dieses globale Referenzstrategiemuster zu unterstützen, sofern die Hauptverzweigung die einzige Verzweigung ist, in der Sie Ihre Pakete versionieren. Wenn Sie eine Version über mehrere Verzweigungen hinweg erstellen, besteht die Gefahr, dass die Funktionalität zwischen den Versionen nach dem Zufallsprinzip verloren geht. Erstellen Sie nur stabile Versionen auf dem Hauptzweig.

Erstellen Sie nur Funktionsverzweigungen in Ihren Paket-Repositorys. Nicht in Ihren Store-Installations-Repositorys. Bleiben Sie in der Lage, Änderungen an Ihrem Store nur mit Composer einzuführen. Vermeidung der Notwendigkeit von Git-Zusammenführungen im Bereitstellungs-Repository.

Verzweigungstypen, die in Verzweigungsstrategien und Repositorys häufig sind, in denen sie vorhanden sein sollten:

**Funktionsverzweigungen**: sind nirgendwo sonst in Ihren Paket-Repositorys vorhanden.

**Versionsverzweigungen** werden in jedem Repository erstellt: Pakete, Metapakete, Speicherinstallations-Repositorys. Wenn Sie eine Version planen, gruppieren Sie Änderungen in Versionszweigen von Paketen, bevor Sie sie versionieren. Angenommen, Sie bereiten eine Version mit dem Codenamen „Unicorn“ vor. Sie können in Paketen mit Änderungen eine Verzweigung „Release-Unicorn“ erstellen. Mische alles darin zusammen und benötige dann „dev-release-unicorn as 1.4.0“ in deinem Metapaket. Erfahren Sie mehr über Aliase, um zu sehen, was dort passiert: <https://getcomposer.org/doc/articles/aliases.md>.

**QA/Dev-Verzweigungen**: Ähnlich wie Versionsverzweigungen.

**Hauptverzweigung**: Muss in jedem Repository vorhanden sein und sollte immer die Verzweigung sein, die die Produktion oder einen produktionsbereiten Status darstellt. Der Hauptzweig ist der Ort, an dem Sie Code taggen, um Versionen zu veröffentlichen.
Stellen Sie sicher, dass Sie eine Verzweigungsstrategie mit geringem Wartungsaufwand wählen. Beispielsweise ist das Zusammenführen der Hauptverzweigung wieder in QA-, UAT-, Release- oder Dev-Verzweigungen nach einer Hotfix-Veröffentlichung eine allgemeine Wartungsaufgabe. Je mehr Pakete, desto mehr Repositorys und desto mehr sich wiederholende Overhead-Aufgaben.

Verwenden Sie ein Tool wie mixu/gr, um Routinevorgänge für mehrere Git-Repositorys in einem Batch durchzuführen: <https://github.com/mixu/gr>

## Benennungskonventionen

Mit dem GRA-Muster Separate Packages sind Pakete Teil der GRA-Foundation, wenn das Foundation-Metapaket sie erfordert. Fügen Sie Pakete zum Metapaket hinzu oder entfernen Sie es, um sie in die Foundation und wieder heraus zu verschieben.

Metapakete bieten Flexibilität beim Installationsumfang von Paketen. Es ist besonders wichtig, dass die Namen von Paketen keine Wörter enthalten, die sich auf den vorgesehenen Zweck des Pakets beziehen. Der Name antonevers/module-gra-store-locator kann verwirrend werden, wenn Sie sich entscheiden, dieses Paket aus der GRA Foundation zu nehmen. Vermeiden Sie den Umfang (GRA, Foundation, lokal). Vermeiden Sie Regionen (EMEA, Spanien, Global). Vermeiden Sie auf jeden Fall den Namen des Speichers, für den ein Paket erstellt wurde. Wählen Sie Namen aus, die sich nur auf die Funktion beziehen, die dem Paket hinzugefügt wird. Auf diese Weise können Sie sie überall dort wiederverwenden, wo Sie möchten, auch in unvorhergesehenen zukünftigen Szenarien. Der Name antonevers/module-store-locator wäre ausgezeichnet.

Stellen Sie sicher, dass verwandte Pakete in Übersichten zusammen angezeigt werden. Erstellen Sie Namen von generisch zu spezifisch. Also: antonevers/module-b2b-tax-free anstelle von antonevers/tax-free-module-b2b.

## Code-Beispiele

Die Code-Beispiele für diesen Blogpost wurden in einer Reihe von Git-Repositorys kombiniert, mit denen Sie mit dem Machbarkeitsnachweis spielen können.

- Ein Beispiel für einen Produktionsspeicher: <https://github.com/AntonEvers/gra-separate-brand-x>
- Ein Beispiel für ein Foundation-Modul: <https://github.com/AntonEvers/module-example-gra>
- Ein Beispiel für ein Modul eines Drittanbieters: <https://github.com/AntonEvers/module-example-3rdparty>
- Ein Beispiel für ein lokales Modul: <https://github.com/AntonEvers/module-example-local>
- Ein Beispiel für ein Foundation-Metapaket: <https://github.com/AntonEvers/gra-meta-foundation>
- Ein Beispiel für ein lokales Metapaket (optional): <https://github.com/AntonEvers/gra-meta-brand-x>
- Ein Beispiel für ein Composer-Repository: <https://github.com/AntonEvers/gra-composer-repository>
