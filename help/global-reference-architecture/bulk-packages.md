---
title: Optimieren von Adobe Commerce mit der globalen Referenzarchitektur für Massenpakete
description: Erfahren Sie, wie Sie Adobe Commerce mithilfe der globalen Referenzarchitektur für Massenpakete einrichten, um die Code-Verwaltung und Versionskontrolle zu optimieren.
kt: 16726
doc-type: tutorial
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
topic: Architecture, Commerce, Development
role: Architect, Developer, User, Leader
level: Beginner, Intermediate
source-git-commit: 916586d3b71b8b74baa04af2ab39abc86ec94f5b
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---


# Das Muster der globalen Referenzarchitektur für Bulk Packages

In diesem Handbuch wird erläutert, wie Sie Adobe Commerce mit dem GRA-Muster (Bulk Packages Global Reference Architecture) einrichten.

Das Massen-Package-GRA-Muster umfasst ein einzelnes Git-Repository, in dem alle gängigen Anpassungen gehostet werden. Dieses einzelne Git-Repository wird über Composer als einzelnes Composer-Paket bereitgestellt, das mehrere Adobe Commerce-Module enthält.

![Ein Diagramm, das zeigt, wo Code in einem Massen-Package-GRA-Muster gespeichert wird](/help/assets/global-reference-architecture/bulk-gra-pattern-diagram.png){align="center"}

## Vor- und Nachteile dieses Musters

Vorteile:

- Wiederverwendung von Code über ein gemeinsam genutztes Code-Repository
- Flexibilität bei der Installation verschiedener historischer Versionen der GRAA auf verschiedenen Instanzen, was schrittweise Versionen ermöglicht
- Flexibilität beim Backport und bei der Pflege mehrerer Hauptversionen der GRA
- Unterstützung der semantischen Versionierung der GRA
- Einfachheit: Entwickler benötigen nicht mehr Fähigkeiten als in regulären Einzelhandelsentwicklungsmustern
- Keine speziellen Tools, keine komplexe Infrastruktur oder spezielle Verzweigungsstrategie erforderlich
- Die Kombination von Paketen in einer Version wird immer gemeinsam entwickelt und getestet

Nachteile:

- Nur möglich, das vollständige GRA einschließlich aller darin enthaltenen Pakete zu aktualisieren.
- Keine Unterstützung im GRA-Bulk-Package für Composer-Pakete außer Adobe Commerce-Modulen, Sprachpaketen und Designs, also keine Metapakete, Magento2-Komponenten-Pakete, Composer-Plug-ins und Patches

## Einrichten von Adobe Commerce mit dem Split Git-GRA-Muster

### Die Verzeichnisstruktur

Das Bulk Packages-GRA installiert den gesamten wiederverwendbaren Code über Composer-Repositorys. Code, der für eine einzelne Instanz spezifisch ist, befindet sich im Git-Repository dieser Instanz. Instanzspezifischer Code wird in anderen Instanzen von Adobe Commerce nicht wiederverwendet.

Die endgültige Verzeichnisstruktur einer vollständigen Adobe Commerce-Installation mit dem Massen-Package-GRA-Muster sieht wie folgt aus:

```text
.
├── app/
│   └── etc/
│       └── config.php
├── composer.json
├── composer.lock
└── packages/
    └── local/
```

Die `app/code`-, `app/i18n`- und `app/design`-Verzeichnisse werden absichtlich weggelassen, da Composer den Code in diesen Verzeichnissen nicht auswertet. Abhängigkeiten, die in den Paketen deklariert sind, werden daher nicht automatisch installiert. Das GRA-Muster für Bulk Packages löst dieses Problem, indem benutzerdefinierter Code in `packages/` installiert und dieses Verzeichnis als Composer-Repository behandelt wird. Composer verknüpft Pakete innerhalb von `packages/` mit `vendor/`.

### Vorbereiten der Git-Repositorys

Erstellen Sie zwei Git-Repositorys für den freigegebenen GRA-Code und für den ersten Store. Beginnen Sie mit dem GRA-Repository, das die folgende Dateistruktur aufweist:

Das Ergebnis ist die folgende Verzeichnisstruktur:

```text
.
├── composer.json
└── src/
    ├── GraOne/
    │   ├── composer.json
    │   └── registration.php
    ├── GraTwo/
    │   ├── composer.json
    │   └── registration.php
    └── registration.php
```

Diese Verzeichnisstruktur erwähnt nur die Datei composer.json und die Datei registration.php der GraOne- und GraTwo-Module. Tatsächlich gibt es mehr Dateien innerhalb dieser Module.

Führen Sie diese Befehle aus, um das Git-Repository zu initiieren:

```bash
mkdir gra-bulk-foundation
cd gra-bulk-foundation
git init
git remote add origin git@github.com:AntonEvers/gra-bulk-foundation.git
vim composer.json # see code snippet below for contents
git add composer.json
git commit -m 'initialize GRA foundation repository'
git push -u origin main
```

Die Inhalte der Datei „composer.json“:

```json
{
    "name": "antonevers/gra-bulk-foundation",
    "description": "Shared code repository",
    "type": "library",
    "license": [
        "OSL-3.0",
        "AFL-3.0"
    ],
    "require": {},
    "autoload": {
        "files": [
            "src/registration.php"
        ],
        "psr-0": {
            "": "src/"
        }
    }
}
```

Ändern Sie den Namespace des composer.json-Pakets in Ihren eigenen Namespace.

Die Inhalte der Datei src/registration.php:

```php
<?php

declare(strict_types=1);

$pathList[] = dirname(__DIR__) . '/src/*/*/registration.php';
foreach ($pathList as $path) {
    $files = glob($path, GLOB_NOSORT | GLOB_ERR);
    if ($files === false) {
        throw new RuntimeException('glob() returned error while searching in \'' . $path . '\'');
    }
    foreach ($files as $file) {
        require_once $file;
    }
}
```

Die Datei registration.php sucht nach anderen registration.php-Dateien innerhalb der Adobe Commerce-Module und führt sie aus.

Erstellen Sie die beiden Beispielmodule mit dem Code in <https://github.com/AntonEvers/gra-bulk-foundation>. Composer wertet die Dateien „composer.json“ in den Beispielmodulen nicht aus. Sie sind dort als Gewohnheit. Wenn Sie sich entscheiden, die Module an einen anderen Ort zu verschieben, werden die Dateien „composer.json“ erneut erforderlich.

### Einrichten des Store-Repositorys

Das Bereitstellungs-Repository enthält die gesamte Adobe Commerce-Installation einschließlich des GRA-Codes. Erstellen Sie das Bereitstellungs-Repository:

```bash
mkdir gra-bulk-brand-x
cd gra-bulk-brand-x
composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition .
git init
git remote add origin git@github.com:AntonEvers/gra-bulk-brand-x.git 
git add composer.json composer.lock
git commit -m 'initialize Brand X repository'
git push -u origin main
```

Installieren von Adobe Commerce mit `bin/magento setup:install`. Installieren Sie die GRA-Beispielmodule im Bereitstellungs-Repository mit Composer:

```bash
composer config repositories.gra-foundation vcs git@github.com:AntonEvers/gra-bulk-foundation.git
composer require antonevers/gra-bulk-foundation:@dev
bin/magento module:enable AntonEvers_GraOne AntonEvers_GraTwo
bin/magento test:gra-one
bin/magento test:gra-two
git add app/etc/config.php composer.json composer.lock
git commit -m 'install GRA foundation'
git push origin main
```

Dieser letzte Befehl sollte zur folgenden Ausgabe führen, um zu überprüfen, ob das Modul installiert ist und funktioniert:

```bash
GRA One module is installed successfully and working!
GRA Two module is installed successfully and working!
```

Sie können mehrere Massenpakete erstellen, um Code zu organisieren. Zum Beispiel ein Massenpaket eines Drittanbieters für Drittanbieter-Code, das nicht über Composer verfügbar ist. Alles, was Sie traditionell in `app/code` installieren würden, sollte sich jetzt im `src/` des Bulk Packages befinden. Eine Ausnahme von dieser Regel ist Code, der nur in einer einzigen Instanz verwendet wird. Diese Pakete werden als lokale Pakete bezeichnet.

### Lokale Pakete installieren

Das Bereitstellungs-Repository hostet lokale Pakete. Sie leben nicht im GRA-Bulk-Paket. Der Speicherort der lokalen Pakete ist nicht `app/code`, sondern `packages/local`. Weisen Sie Composer an, dieses Verzeichnis als Repository zu behandeln:

```bash
composer config repositories.local path 'packages/local/*/*'
git add composer.json
git commit -m 'initialize local composer package storage'
git push origin main
```

Fügen Sie das Beispielmodul hinzu, das unter <https://github.com/AntonEvers/module-example-local> gehostet wird:

```bash
mkdir -p packages/local
cd packages/local
mkdir antonevers
cd antonevers
curl -OL https://github.com/AntonEvers/module-example-local/archive/refs/heads/main.zip
unzip main.zip
rm main.zip
mv module-example-local-main module-local
git add module-local
cd ../../..
composer require antonevers/module-local:@dev
bin/magento module:enable AntonEvers_Local
bin/magento test:local
```

Dieser letzte Befehl sollte zur folgenden Ausgabe führen, um zu überprüfen, ob das Modul installiert ist und funktioniert:

```bash
Local module is installed successfully and working!
```

Übertragen Sie das lokale Modul in das Marken-Repository:

```bash
git add packages/local/antonevers/module-local app/etc/config.php composer.json composer.lock 
git commit -m 'add local module'
git push origin main
```

## Übersicht über Code-Speicherorte

Nur wenn der Drittanbieter die Installation nicht über ein Composer-Repository anbietet, können Sie Module von Drittanbietern im `src/` Ihres Foundation-Repositorys oder in einem dedizierten Massenpaket von Drittanbietern speichern.

- **Adobe Commerce Core**: verfügbar über repo.magento.com.
- **Module von Drittanbietern**: verfügbar über den Marketplace oder das eigene Composer-Repository eines Anbieters.
- **Fallback-Option für Drittanbietermodule**: Wird `src/` eines Massenpakets gespeichert.
- **GRA-Foundation**: Wird in `src/` des Foundation-Bulk-Pakets gespeichert.
- **Lokaler Code**: im `packages/local` des Bereitstellungs-Repositorys gespeichert.

## Entwickeln eines GRA-Moduls

Installieren Sie das Bulk Package aus der Quelle, um Git im Bulk Package Directory zu aktivieren:

```bash
rm -r vendor/antonevers/gra-bulk-foundation
composer install --prefer-source
```

Das Massenpaket wurde mit Git ausgecheckt. Wenn Sie das `vendor/antonevers/gra-bulk-foundation`-Verzeichnis eingeben, gelangen Sie auch in das Git-Repository, das auf der Massenbasis basiert. Sie können Verzweigungen in diesem Verzeichnis erstellen, auschecken und zusammenführen.

Fügen Sie Composer-Abhängigkeiten zur Datei „composer.json“ im Stammverzeichnis des GRA-Bulk-Pakets hinzu, bei dem es sich um die einzige Datei im Bulk-Paket handelt, die Composer auswertet.

## Einbeziehen von Drittanbietermodulen in das GRA-Bulk-Package

Fügen Sie Pakete von Drittanbietern im erforderlichen Abschnitt von composer.json im Stammverzeichnis der GRA Foundation hinzu, um sie Ihrer GRA hinzuzufügen. Auf diese Weise werden die Pakete immer über den Composer in allen Ihren Instanzen installiert.

## Code bereitstellen

Um Code an die Hauptverzweigung zu senden, gibt es zwei Pfade. Zuerst die lokalen Module, die mit der Hauptverzweigung zusammengeführt werden. Führen Sie ein Composer-Update für diese Module aus. Erlauben Sie Entwicklern nicht, composer.lock in ihren Ticket-Verzweigungen zu aktualisieren, um Konflikte zu reduzieren. Aktualisieren Sie die Datei composer.lock nur in Staging- und Produktionszweigen, wodurch das Risiko von Konflikten reduziert wird.

Zweitens die GRA-Bulk-Pakete, die in die Hauptverzweigung des GRA-Bulk-Repositorys zusammengeführt werden. Anschließend können Sie ein Git-Tag zur Hauptverzweigung hinzufügen und so das Composer-Paket versionieren. Sie benötigen Ihre neue Version des GRA-Bulk-Pakets in der Datei „composer.json“ des Bereitstellungs-Repositorys, um es zu installieren.

## Verzweigungsstrategie

Dieses GRA-Muster funktioniert mit allen Verzweigungsstrategien, solange Sie die Verzweigungsstrategie der Bereitstellungs-Repositorys in Ihrem GRA-Massen-Repository spiegeln. Erstellen Sie für -Versionen eine Versionsverzweigung mit demselben Namen in beiden Repositorys. Erstellen Sie zur Entwicklung eine Ticket-Verzweigung in beiden Repositorys.

In Ticket-Verzweigungen sollten Sie fast nie die Datei composer.lock aktualisieren müssen. Sehen Sie sich mit Git einfach die richtigen Verzweigungen in Ihrer Entwicklungsumgebung für den Store und das GRA Foundation-Repository an. Die Ausnahme besteht, wenn Sie Anforderungen in der GRA Foundation composer.json-Datei aktualisieren. Das Upgrade der GRA Foundation im Bereitstellungs-Repository erfolgt nur beim Erstellen der Version oder beim Erstellen einer QA-Verzweigung.

## Code-Beispiele

Die Code-Beispiele für diesen Artikel sind als eine Reihe von Git-Repositorys verfügbar, mit denen Sie den Machbarkeitsnachweis testen können.

- Ein Beispiel für einen Produktionsspeicher: <https://github.com/AntonEvers/gra-bulk-brand-x>
- Das GRA-Code-Repository: <https://github.com/AntonEvers/gra-bulk-foundation>
- Ein Beispiel für ein lokales Modul: <https://github.com/AntonEvers/module-example-local>