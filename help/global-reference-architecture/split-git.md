---
title: Einrichten von Adobe Commerce mit der globalen Split-Git-Referenzarchitektur
description: Erfahren Sie, wie Sie Adobe Commerce mithilfe der globalen Split-Git-Referenzarchitektur einrichten, um die Code-Verwaltung zu optimieren und die Bereitstellung zu optimieren. ​
kt: 16725
doc-type: tutorial
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
badge: label="Beiträge von Tony Evers, Sr. Technical Architect, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony/" tooltip="Beiträge von Tony Evers"
topic: Architecture, Commerce, Development
role: Architect, Developer, User, Leader
level: Beginner, Intermediate
exl-id: ac544f77-8f5f-4ad1-92b2-bdf323100c13
source-git-commit: dacd43ef84dcb2c2633221a90642a469b2ff5a30
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 0%

---

# Das aufgeteilte globale Git-Referenzarchitekturmuster

In diesem Handbuch wird erläutert, wie Sie Adobe Commerce mit dem Split Git Global Reference Architecture (GRA)-Muster einrichten.

Das aufgeteilte Git-GRA-Muster umfasst zwei Git-Repositorys für die Entwicklung und ein Git-Repository pro Adobe Commerce-Instanz. In den Beispielen wird davon ausgegangen, dass jede Instanz eine eindeutige Marke darstellt.

![Ein Diagramm, das zeigt, wo Code in einem aufgeteilten GRA-Muster gespeichert ist](/help/assets/global-reference-architecture/split-git-gra-pattern-diagram.png){align="center"}

## Vor- und Nachteile dieses Musters

Vorteile:

- Wiederverwendung von Code über ein gemeinsam genutztes Code-Repository
- Einfaches GRA-Muster, auch für Teams mit begrenztem Komponistenwissen geeignet
- Zusätzlich zu Adobe Commerce-Modulen, Themen und Sprachpaketen ist es möglich, jede Art von Composer-Paket über dieses Modell zu installieren, einschließlich Composer-Plug-in, Composer-Metapaket, Magento2-Komponente und Patches
- Freigabe in Phasen möglich, Freigabe in Regionen in eigenen Wartungsfenstern planen
- Unterstützung für Git-Tags zu Administrationszwecken, nicht zur Bereitstellungssteuerung
- Sicherstellen, dass die Kombination von Paketen in einer Produktionsbereitstellung in genau dieser Konfiguration entwickelt und getestet wird

Nachteile:

- Keine zusätzliche Flexibilität im Vergleich zu anderen GRA-Mustern
- Es ist nicht möglich, einzelne Module pro Instanz zu aktualisieren oder herunterzustufen. Führen Sie immer ein Upgrade oder ein Downgrade für die gesamte GRA durch.
- In den meisten Fällen ist das Muster für Massenpakete besser geeignet, da es ebenso einfach, aber konventioneller ist

## Einrichten von Adobe Commerce mit dem Split Git-GRA-Muster

### Die Verzeichnisstruktur

Das aufgeteilte Git-Graph-Muster weist zwei Arten von Repositorys auf: Entwicklungs-Repositorys und Installations-Repositorys. Die Entwicklungs-Repositorys enthalten nur einen Teil einer vollständigen Adobe Commerce-Installation. Die Installations-Repositorys enthalten die vollständige Adobe Commerce-Installation und werden für die Bereitstellung verwendet, jedoch nicht für die Entwicklung.

Die endgültige Verzeichnisstruktur einer vollständigen Adobe Commerce-Installation mit dem aufgeteilten Git-GRA-Muster sieht wie folgt aus:

```text
.
├── .gitignore
├── app/
│   └── etc/
│       └── config.php
├── composer.json
├── composer.lock
└── packages/
    ├── 3rdparty/
    ├── gra/
    └── local/
```

Die `app/code`-, `app/i18n`- und `app/design`-Verzeichnisse werden absichtlich weggelassen, da Composer den Code in diesen Verzeichnissen nicht auswertet. Abhängigkeiten, die in den Paketen deklariert sind, werden daher nicht automatisch installiert. Das aufgeteilte Git-GRA-Muster behebt dieses Problem, indem der gesamte benutzerdefinierte Code in `packages/` installiert und dieses Verzeichnis als Composer-Repository behandelt wird. Composer verknüpft Pakete innerhalb von `packages/` mit `vendor/`.

### Vorbereiten der Git-Repositorys

Erstellen Sie 3 Git-Repositorys für:

1. Eine Adobe Commerce-Instanz
2. Drittanbieter-Code, der nicht über Composer installiert wird
3. Ihre Anpassungen in Form von Modulen, Designs, Sprachpaketen usw.; Ihre GRA

In diesem Handbuch werden die folgenden Namen für diese Repositorys verwendet:

1. gra-split-brand-x
2. gra-split-3rdParty
3. gra-split-gra

Alle Repositorys im aufgeteilten Git-GRAD-Muster werden in einem zusammengeführt. Damit Git das Zusammenführen mehrerer Repositorys ermöglicht, benötigen alle drei Repositorys einen gemeinsamen Verlauf. Erstellen Sie ein Git-Projekt mit einem einzigen Commit und übertragen Sie es auf alle Remote-Standorte.

```bash
mkdir gra-split-brand-x
cd gra-split-brand-x
git init
git remote add origin git@github.com:AntonEvers/gra-split-brand-x.git
git remote add 3rdparty git@github.com:AntonEvers/gra-split-3rdparty.git
git remote add gra git@github.com:AntonEvers/gra-split-gra.git
touch .gitkeep
git add .gitkeep
git commit -m 'initialize repository'
git push -u origin main
git push 3rdparty main
git push gra main
```

Wenn Sie die temporäre Datei `.gitkeep` an alle Remote-Standorte senden, wird derselbe anfängliche Commit mit demselben Commit-Hash erstellt, wodurch ein gemeinsamer Verlauf erstellt wird. Jede Änderung, die in einer Remote-Instanz erstellt wird, kann mit der anderen zusammengeführt werden.

Von hier aus weichen die Repositorys voneinander ab. Das Repository gra-split-brand-x enthält markenspezifischen Code. Das Repository von gra-split-3rd-party enthält nur Code von Drittanbietern. Das Repository gra-split-gra enthält nur Ihre globale Referenzarchitektur, die aus dem gesamten benutzerdefinierten Code besteht.

Installieren Sie Adobe Commerce im Repository „gra-split-brand-x“.

```bash
composer create-project --no-install --repository-url=https://repo.magento.com/ magento/project-enterprise-edition temp
mv temp/composer.json ./
rmdir temp
git add composer.json
git commit -m 'install Adobe Commerce'
git push origin main
```

Erstellen Sie erste Commits in den Repositorys „gra-split-3rdparty“ und „gra-split-gra“. Am einfachsten ist es, diese Repositorys in separaten Ordnern auszuchecken.

```bash
cd ..
git clone git@github.com:AntonEvers/gra-split-3rdparty.git
git clone git@github.com:AntonEvers/gra-split-gra.git
cd gra-split-3rdparty
mkdir -p packages/3rdparty
touch packages/3rdparty/.gitkeep
git add packages/3rdparty/.gitkeep
git commit -m 'initialize 3rd party package storage'
git push origin main
cd ../gra-split-gra
mkdir -p packages/gra
touch packages/gra/.gitkeep
git add packages/gra/.gitkeep
git commit -m 'initialize GRA package storage'
git push origin main
```

Diese beiden Repositorys speichern Pakete von Drittanbietern und GRA-Pakete. Es kann Code geben, der ausschließlich für jede Instanz von Adobe Commerce gilt. Erstellen Sie einen Speicherort für diese lokalen Pakete im Repository „gra-split-brand-x“.

```bash
cd ../gra-split-brand-x
mkdir -p packages/local
touch packages/local/.gitkeep
git add packages/local/.gitkeep
git commit -m 'initialize local package storage'
git push origin main
```

### Wo verschiedene Arten von Code gespeichert werden

Adobe Commerce ist ein Composer-Programm. Die bevorzugte Methode zur Installation ist immer die Installation über Composer-Repositorys. Nur wenn ein Modulanbieter keine Installation über ein Composer-Repository anbietet, können Sie Module von Drittanbietern im Repository von Drittanbietern speichern. Der bevorzugte Ort für benutzerdefinierten Code ist im GRA-Repository. Wenn ein Modul nur von einer bestimmten Instanz verwendet wird, wird es zu lokalem Code.

Zusammenfassung:

- **Adobe Commerce**: in einem Composer-Repository gespeichert.
- **Module von Drittanbietern**: in einem Composer-Repository gespeichert.
- **Fallback-Option für Drittanbietermodule**: im Git-Repository von gra-split-3rd-party gespeichert.
- **GRA Foundation Code**: im gra-split-gra Git-Repository gespeichert.
- **Lokaler Code**: im Git-Repository „gra-split-brand-x“ gespeichert.

### Package-Speicher mit Composer verbinden

Composer kann das Paketverzeichnis als Composer-Repository behandeln. Informieren Sie Composer über den Speicherort von Paketen im Paketverzeichnis.

```json
"repositories": [
  {"type": "path", "url": "packages/local/*/*"},
  {"type": "path", "url": "packages/gra/*/*"},
  {"type": "path", "url": "packages/3rdparty/*/*"},
  {"type": "composer", "url": "https://repo.magento.com"}
]
```

Composer sucht zwei Ebenen tief nach „composer.json“-Dateien in den drei Speicherverzeichnissen. Erstellen Sie Unterverzeichnisse innerhalb der drei Code-Speicherverzeichnisse genau so, wie sie im `vendor/` Verzeichnis erscheinen würden.

Beispiel: Wenn ein Paket normalerweise in `vendor/example-corp/module-example/` installiert ist, wird es in `packages/3rdparty/example-corp/module-example/` gespeichert. Composer verknüpft das Paket mit &quot;`vendor/example-corp/module-example/`&quot;, wenn Sie es benötigen.

Verwenden Sie den Namespace und den Namen des Composer-Pakets als Ordnerstruktur. Beispiel: Ein Modul, das traditionell in `app/code/MyCorp/MyCustomization/` vorhanden ist, hat den Namen `my-corp/module-my-customization` in composer.json. Bewahren Sie dieses Paket in `packages/gra/my-corp/module-my-customization` auf.

### Neue Pakete in die Instanz-Repositorys einschließen

Zusammenführen von Paketen aus den Remote-Standorten von Drittanbietern und GRA in das Repository „gra-split-brand-x“.

```bash
cd gra-split-brand-x
git fetch - all
git merge gra/main 3rdparty/main
git push origin main
```

Das Ergebnis ist die folgende Verzeichnisstruktur:

```text
.
├── composer.json
└── packages/
    ├── 3rdparty/
    ├── gra/
    └── local/
```

Änderungen im Repository von Drittanbietern und im GRA Foundation Repository werden in den Marken-Repositorys zusammengeführt. Auf diese Weise werden Drittanbieter- und GRA-Code nur an einem Ort gepflegt. Verschieben Sie die Änderungen mit einer Git-Zusammenführung in die Marken.

Adobe Commerce erkennt neue Module nicht automatisch. Composer ausführen erfordert, dass nach einer Zusammenführung ein neues Paket hinzugefügt wird. Führen Sie Composer-Updates jedes Mal aus, wenn Sie eines Ihrer Pakete nach einer Zusammenführung aktualisieren.

### Installieren von Beispielmodulen

Installieren Sie als Konzeptnachweis Beispielmodule, um zu sehen, wie das GRA-Muster funktioniert.

Führen Sie `composer install` und `bin/magento install` aus, bevor Sie fortfahren.

Es gibt 3 Testmodule für auf GitHub:

1. [module-example-local](https://github.com/AntonEvers/module-example-local)
2. [module-example-gra](https://github.com/AntonEvers/module-example-gra)
3. [module-example-3rdParty](https://github.com/AntonEvers/module-example-3rdparty)

### Installieren eines lokalen Moduls

Das Hinzufügen eines Moduls zum lokalen Code-Pool ist einfach. Laden Sie das Modul herunter und extrahieren Sie es. Mit Composer verlangen. Aktivieren Sie sie mit `bin/magento` und übertragen Sie die Dateien im Brand-Repository.

```bash
cd gra-split-brand-x
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

Wenn die Ausgabe oben angezeigt wird, können Sie sie sicher in das Marken-Repository übertragen.

```bash
git add packages/local/antonevers/module-local app/etc/config.php composer.json composer.lock 
git commit -m 'add local module'
git push origin main
```

### Installieren und Entwickeln eines GRA Foundation-Moduls

Das Hinzufügen eines Moduls zum GRA-Repository unterscheidet sich von der Installation lokaler Module. Standardmäßig werden Commits zu „origin/main“ hinzugefügt, dem Repository von „gra-split-brand-x“. Änderungen an GRA-Modulen sollten in das gra-split-gra-Repository übertragen und anschließend in das gra-split-brand-x-Repository zusammengeführt werden.

### Erstellen einer Entwicklungsumgebung

Erstellen Sie eine Entwicklungsumgebung mit einer Kombination aller Code-Pools an einem Ort. Sie können Code einzeln über Symlinks an das lokale, allgemeine und Drittanbieter-Repository senden. Erstellen Sie zunächst ein neues Entwicklungsverzeichnis neben Ihren Marken-, GRA- und Repository-Verzeichnissen von Drittanbietern.

```text
.
├── gra-development    # <---
├── gra-split-3rdparty
├── gra-split-brand-x
└── gra-split-gra
```

```bash
cd ..
mkdir gra-development
cd gra-development
cp ../gra-split-brand-x/composer.json ../gra-split-brand-x/composer.lock .
mkdir packages
ln -s ../../gra-split-brand-x/packages/local/ packages/
ln -s ../../gra-split-3rdparty/packages/3rdparty/ packages/
ln -s ../../gra-split-gra/packages/gra/ packages/
```

Das Ergebnis ist die folgende Verzeichnisstruktur:

```text
.
├── packages/
│ ├── 3rdparty -> ../../gra-split-3rdparty/packages/3rdparty/
│ ├── gra -> ../../gra-split-gra/packages/gra/
│ └── local -> ../../gra-split-brand-x/packages/local/
├── composer.lock
└── composer.json
```

Führen Sie `composer install` und `bin/magento install` im Verzeichnis „gra-development“ aus.

Es ist jetzt möglich, Änderungen direkt aus den `packages/3rdparty`-, `packages/gra`- und `package/local`-Verzeichnissen zu übernehmen. Git übergibt die Änderungen an das Git-Repository, mit dem die Verzeichnisse verknüpft sind. Es ist wichtig, dass der Git-Commit-Befehl im `packages/3rdparty`-, `packages/gra`- oder `package/local`-Verzeichnis ausgegeben wird. Führen Sie keinen Git-Commit im Projektstamm aus.

### Installieren von Beispielmodulen

Installieren Sie die Beispielmodule von Drittanbietern und GRAs in den Paketverzeichnissen.

```bash
cd packages/gra
mkdir antonevers
cd antonevers
curl -OL https://github.com/AntonEvers/module-example-gra/archive/refs/heads/main.zip
unzip main.zip
rm main.zip
mv module-example-gra-main module-gra
git add module-gra
 
cd ../../3rdparty
mkdir antonevers
cd antonevers
curl -OL https://github.com/AntonEvers/module-example-3rdparty/archive/refs/heads/main.zip
unzip main.zip
rm main.zip
mv module-example-3rdparty-main module-3rdparty
git add module-3rdparty
 
cd ../../..
composer require antonevers/module-gra:@dev antonevers/module-3rdparty:@dev
bin/magento module:enable AntonEvers_Gra AntonEvers_ThirdParty
bin/magento test:gra
bin/magento test:3rdparty
```

Dieser letzte Befehl sollte zur folgenden Ausgabe führen, um zu überprüfen, ob das Modul installiert ist und funktioniert:

```bash
GRA module is installed successfully and working!
3rd party module is installed successfully and working!
```

Wenn die Ausgabe oben angezeigt wird, können Sie sie sicher in das Marken-Repository übertragen. Führen Sie `git remote -v` aus, um zu überprüfen, ob Sie sich für die richtige Remote-Konfiguration entscheiden.

```bash
cd packages/gra
git remote -v 
origin git@github.com:AntonEvers/gra-split-gra.git (fetch)
origin git@github.com:AntonEvers/gra-split-gra.git (push)
git add antonevers/module-gra
git commit -m 'add GRA module'
git push origin main
 
cd ../3rdparty
git remote -v 
origin git@github.com:AntonEvers/gra-split-3rdparty.git (fetch)
origin git@github.com:AntonEvers/gra-split-3rdparty.git (push)
git add antonevers/module-3rdparty
git commit -m 'add third-party module'
git push origin main
```

### Code an die Instanzen senden

Führen Sie die Repositorys von GRA und Drittanbietern mit dem Repository „gra-split-brand-x“ zusammen, um den Code an eine Adobe Commerce-Instanz zu senden. Führen Sie `composer require` aus, `bin/magento module:enable` und übertragen Sie das Ergebnis.

```bash
cd gra-split-brand-x
git fetch - all
git merge gra/main 3rdparty/main
composer require antonevers/module-gra:@dev antonevers/module-3rdparty:@dev
bin/magento module:enable AntonEvers_Gra AntonEvers_ThirdParty
git add app/etc/config.php composer.lock composer.json
git commit -m 'install GRA and third-party modules'
git push origin main
```

## Verzweigungsstrategie

Dieses GRA-Muster funktioniert mit allen Verzweigungsstrategien, wenn Sie die Verzweigungsstrategie der Store-Repositorys in den Repositorys von Drittanbietern und GRAs spiegeln. Erstellen Sie für -Versionen eine Versionsverzweigung mit demselben Namen in allen drei Repositorys. Zusammenführen der Versionsverzweigungen im Speicher-Repository während der Vorbereitung der Veröffentlichung.

Manchmal gibt es eine Ticketverzweigung, in der sowohl lokaler Code als auch Drittanbieter-Code oder GRA-Code geändert werden müssen. In diesem Fall müssen die Ticket-Verzweigungen in allen zugehörigen Repositorys erstellt werden.

Zusammenführen von Drittanbieter- und GRA-Commits niemals im Marken-Repository innerhalb von Ticket-Verzweigungen. Checken Sie stattdessen für jeden Code-Pool die richtigen Verzweigungen in Ihrer Entwicklungsumgebung aus. Die Zusammenführung mit dem Marken-Repository erfolgt nur beim Erstellen der Version oder beim Erstellen einer QA-Verzweigung.

## Code-Beispiele

Die Code-Beispiele für diesen Artikel sind als eine Reihe von Git-Repositorys verfügbar, mit denen Sie den Machbarkeitsnachweis testen können.

- Ein Beispiel für einen Produktionsspeicher: <https://github.com/AntonEvers/gra-split-brand-x>
- Das Drittanbieter-Code-Repository: <https://github.com/AntonEvers/gra-split-3rdparty>
- Das GRA-Code-Repository: <https://github.com/AntonEvers/gra-split-gra>
- Ein Beispiel für ein lokales Modul: <https://github.com/AntonEvers/module-example-local>
- Ein Beispiel für ein GRA-Modul: <https://github.com/AntonEvers/module-example-gra>
- Ein Beispiel für ein Modul eines Drittanbieters: <https://github.com/AntonEvers/module-example-3rdparty>
