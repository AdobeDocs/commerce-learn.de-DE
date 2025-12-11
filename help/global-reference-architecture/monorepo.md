---
title: Globale Referenzarchitektur - Monorepo
description: Erfahren Sie, wie Sie mit dem monorepo-Ansatz für eine globale Referenzarchitektur ein skalierbares und widerstandsfähiges Commerce-Erlebnis schaffen
jira: KT-16728
doc-type: tutorial
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
badge: label="Beiträge von Tony Evers, Sr. Technical Architect, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony/" tooltip="Beiträge von Tony Evers"
topic: Architecture, Commerce, Development
old-role: Architect, Developer
role: Developer, User, Leader
level: Experienced
exl-id: ebdc13cf-c452-4728-af00-c3ea1149c2fa
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 0%

---

# Monorepo Global Reference Architecture-Muster

In diesem Handbuch wird erläutert, wie Sie Adobe Commerce mit dem Monorepo Global Reference Architecture (GRA)-Muster einrichten.

Das Monorepo GRA-Muster beinhaltet ein einzelnes Git-Repository, in dem alle gängigen Anpassungen gespeichert werden. Dieses einzelne Git-Repository wird über Composer als separate Composer-Pakete verfügbar gemacht.

![Ein Diagramm, das zeigt, wo Code in einem monorepo-GRA-Muster gespeichert wird](/help/assets/global-reference-architecture/monorepo-gra-pattern-diagram.png){align="center"}

## Vor- und Nachteile dieses Musters

Vorteile:

- Ideal für Funktionstests
- Wiederverwendung von Code durch gemeinsam genutzte Code-Repositorys
- Vollständige Flexibilität bei der Paketinstallation. Jedes GRA-Paket kann einzeln aktualisiert, heruntergestuft oder rückportiert werden
- Vollständige Unterstützung der semantischen Versionierung
- Keine speziellen Tools, keine komplexe Infrastruktur oder spezielle Verzweigungsstrategie erforderlich
- Unterstützung aller von Composer unterstützten Pakettypen
- Ideal für temporäre Umgebungen, die optional sind, aber für Bereitstellungs-Teams mit hohem Volumen sind sie sehr nützlich

Nachteile:

- Mögliche Kombinationen von Paketen bereitzustellen, die nicht in derselben Konfiguration entwickelt wurden, erfordern strenge Testverfahren
- Das monorepo GRA-Muster kann zu Beginn komplex sein. Weisen Sie einen Lead zu, der das Team bei der Arbeit mit dem System unterstützt

## Einrichten von Adobe Commerce mit dem separaten Package GRA-Muster

### Die Verzeichnisstruktur

Die endgültige Verzeichnisstruktur einer vollständigen Adobe Commerce-Installation mit dem separaten Package-GRA-Muster weist diese Verzeichnisstruktur auf:

```text
.
├── app/
│   └── etc/
│       └── config.php
├── packages/
│   └── ...
├── composer.json
└── composer.lock
```

Ein Produktions-Git-Repository weist diese Verzeichnisstruktur auf:

```text
.
├── app/
│   └── etc/
│       └── config.php
├── composer.json
└── composer.lock
```

Der Unterschied besteht darin, dass die Produktionsinstanzen von Composer aus installiert werden, wo das monorepo seine eigene Kopie jedes Pakets im Paketverzeichnis aufbewahrt.

### Produktions-Repository vorbereiten

Erstellen Sie ein Repository für die erste Adobe Commerce-Instanz, die einen Webstore für Brand X darstellt.

```bash
mkdir gra-monorepo-brand-x
cd gra-monorepo-brand-x
composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition .
git init
git remote add origin git@github.com:AntonEvers/gra-monorepo-brand-x.git 
git add composer.json composer.lock
git commit -m 'initialize Brand X repository'
git push -u origin main
```

Installieren von Adobe Commerce mit `bin/magento setup:install`. Übergeben Sie die resultierenden `app/etc/config.php`- und Composer-Dateien. Der Komponist verwaltet alles andere, sodass nichts anderes in Git sein sollte.

### Vorbereiten des Monorepo-Repositorys

Das monorepo-Repository beginnt mit denselben Schritten.

```bash
mkdir gra-monorepo 
cd gra-monorepo
composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition .
```

Installieren Sie Adobe Commerce mit `bin/magento setup:install`, Commit und Push.

```bash
git init
git remote add origin git@github.com:AntonEvers/gra-monorepo.git 
git add composer.json composer.lock app/etc/config.php
git commit -m 'initialize monorepo GRA development repository'
git push -u origin main
```

### Vorbereiten der MonoRepo-Entwicklung

Nehmen Sie für die MonoRepo-Entwicklung die folgenden Änderungen an Ihrer Datei „composer.json“ vor:

1. Ändern Sie den Namen und die Beschreibung des Pakets, sodass klar ist, dass dieses Paket Ihr MonoRepo-Paket ist.
1. Löschen Sie das Versionsattribut aus composer.json, da die Version mit Git-Tags für dieses Repository verwaltet wird.
1. Ersetzen Sie den erforderlichen Abschnitt durch ein Metapaket, das später erstellt wird.
1. Ändern Sie die Mindeststabilität in „dev“.
1. Fügen Sie ein Pfadtyp-Repository hinzu, das auf `packages/*/*` verweist, um MonoRepo-Pakete zu hosten, einschließlich Verzweigungs-Aliassen für jedes darin enthaltene Paket
1. Fügen Sie einen Verzweigungsalias für das Projekt selbst hinzu

Der folgende Git-Unterschied zeigt den Unterschied zwischen einer bereinigten Adobe Commerce-Installation und den oben genannten Änderungen:

```diff
@@ -1,6 +1,6 @@
 {
-    "name": "magento/project-enterprise-edition",
-    "description": "eCommerce Platform for Growth (Enterprise Edition)",
+    "name": "antonevers/gra-monorepo",
+    "description": "Monorepo repository for Global Reference Architecture development",
     "type": "project",
     "license": [
         "proprietary"
@@ -15,11 +15,8 @@
         "preferred-install": "dist",
         "sort-packages": true
     },
-    "version": "2.4.7-p3",
     "require": {
-        "magento/product-enterprise-edition": "2.4.7-p3",
-        "magento/composer-dependency-version-audit-plugin": "~0.1",
-        "magento/composer-root-update-plugin": "^2.0.4"
+        "antonevers/gra-meta-brand-x": "self.version"
     },
     "autoload": {
         "exclude-from-classmap": [
@@ -69,16 +66,33 @@
             "Magento\\Tools\\Sanity\\": "dev/build/publication/sanity/Magento/Tools/Sanity/"
         }
     },
-    "minimum-stability": "stable",
+    "minimum-stability": "dev",
     "prefer-stable": true,
     "repositories": [
         {
+            "type": "path",
+            "url": "packages/*/*",
+            "options": {
+                "versions": {
+                    "antonevers/gra-meta-brand-x": "1.4.x-dev",
+                    "antonevers/gra-meta-foundation": "1.4.x-dev",
+                    "antonevers/gra-component-foundation": "1.4.x-dev",
+                    "antonevers/module-gra": "1.4.x-dev",
+                    "antonevers/module-3rdparty": "1.4.x-dev",
+                    "antonevers/module-local": "1.4.x-dev"
+                }
+            }
+        },
+        {
             "type": "composer",
             "url": "https://repo.magento.com/"
         }
     ],
     "extra": {
-        "magento-force": "override"
+        "magento-force": "override",
+        "branch-alias": {
+            "dev-main": "1.4.x-dev"
+        }
     }
 }
```

### Verwenden von Metapaketen

Laden Sie den Beispiel-Code von [AntonEvers/gra-meta-foundation) &#x200B;](https://github.com/AntonEvers/gra-meta-foundation) GitHub herunter, um die Metapakete und die Beispielmodule zu erhalten, die in diesem Beispiel verwendet werden.

Composer-Metapakete bündeln mehrere Composer-Pakete in einem Paket. Wenn ein Metapaket erforderlich ist, werden alle Pakete, die es enthält, automatisch über den Abschnitt Composer erforderlich des Metapakets installiert.

Für dieses Beispiel gibt es zwei Metapakete:

1. **antonevers/gra-meta-brand-x**: Ein Metapaket, das alles enthält, was „Brand X“ ausmacht
1. **antonevers/gra-meta-foundation**: Ein Metapaket, das alles enthält, was immer in einer Marke installiert ist

Für das Brand Metapaket ist das Foundation-Metapaket erforderlich. Wenn ein Brand Metapaket erforderlich ist, wird automatisch auch das Foundation-Metapaket benötigt. Bitte sehen Sie sich die beiden composer.json-Dateien der Metapakete an, um zu sehen, wie sie zusammenhängen:

Antonevers/Gra-Meta-Brand-X:

```json
{
    "name": "antonevers/gra-meta-brand-x",
    "type": "metapackage",
    "license": [
        "OSL-3.0",
        "AFL-3.0"
    ],
    "require": {
        "antonevers/gra-meta-foundation": "^1.4",
        "antonevers/module-local": "^1.4"
    }
}
```

Antonevers/Gra-Meta-Foundation:

```json
{
    "name": "antonevers/gra-meta-foundation",
    "type": "metapackage",
    "license": [
        "OSL-3.0",
        "AFL-3.0"
    ],
    "require": {
        "antonevers/gra-component-foundation": "^1.4",
        "antonevers/module-gra": "^1.4",
        "antonevers/module-3rdparty": "^1.4",
        "magento/composer-dependency-version-audit-plugin": "~0.1",
        "magento/composer-root-update-plugin": "^2.0.4",
        "magento/product-enterprise-edition": "2.4.7-p3"
    }
}
```

Metapakete sind eine gute Möglichkeit, Code zu organisieren, der zusammengehört. Verwenden Sie Metapakete, um Gruppen von Paketen zu definieren, die regional, global, markenspezifisch oder eine für Sie sinnvolle Gruppierung sind. Wenn Sie mehrere Installationen von Adobe Commerce verwalten, bieten matapackages eine sichere und vielseitige Möglichkeit, den Kontext zu definieren, in dem ein Paket erwartet wird.

Metapakete befinden sich im monorepo im `packages`. Dort wird die Verzeichnisstruktur der `vendor` gespiegelt:

```text
.
├── packages/
│   └── antonevers
│       ├── gra-meta-brand-x
│       │   └── composer.json
│       └── gra-meta-foundation
│           └── composer.json
├── composer.json
└── composer.lock
```

### Module hinzufügen und entwickeln

Module im monorepo befinden sich im `packages`. Auf diese Weise kann Composer sie über das Pfadtyp-Repository finden.

Laden Sie den Beispiel-Code von [AntonEvers/gra-meta-foundation) &#x200B;](https://github.com/AntonEvers/gra-meta-foundation) GitHub herunter, um die Metapakete und die Beispielmodule zu erhalten, die in diesem Beispiel verwendet werden.

```text
.
├── packages/
│   └── antonevers
│       ├── gra-meta-brand-x
│       ├── gra-meta-foundation
│       ├── module-3rdparty
│       ├── module-gra
│       └── module-local
├── composer.json
└── composer.lock
```

Sie können bei Bedarf mehrere Namespaces im `packages`-Verzeichnis haben.

Die Entwicklung erfolgt im Paketverzeichnis. Symlinks zu den Paketen im `packages` werden im `vendor` erstellt, sobald Sie `composer update` ausführen. Auf diese Weise wird der Code Teil der Adobe Commerce-Installation.

Führen Sie `bin/magento module:enable --all` oder nur für bestimmte Module aus, um die hinzugefügten Module zu aktivieren.

Mittlerweile sollten Sie über eine funktionierende Adobe Commerce-Installation verfügen, auf der die drei Beispielmodule installiert sind und funktionieren. Sie können überprüfen, ob die Module installiert sind und funktionieren, indem Sie die folgenden Befehle ausführen:

```bash
bin/magento test:gra
bin/magento test:3rdparty
bin/magento test:local
```

### Automatische Paketerstellung

Es gibt mehrere Optionen, um eine automatisierte Paketerstellung zu erreichen. Einige Optionen sind:

1. [Privater Packagist](https://packagist.com/)
1. [Einfacher MonoRepo Builder](https://github.com/symplify/monorepo-builder)
1. Eigene Projektmappe erstellen

[Private Packagist](https://packagist.com/) automatisiert das Erkennen von Paketen im Git-Monorepo und stellt sie über Composer zur Verfügung. Es ist kompatibel mit Adobe Commerce, schnell, wartungsarm und fehleranfällig, weshalb sich dieser Leitfaden auf die Option Private Packagist konzentriert.

Es würde den Rahmen dieses Handbuchs sprengen zu erklären, wie Sie Private Packagist einrichten, siehe die [Dokumente](https://packagist.com/docs).

Es besteht die Möglichkeit, ein Paket in ein MonoRepo umzuwandeln, sobald Sie die Synchronisierung der Organisation eingerichtet haben und Ihre Git-Repositorys automatisch mit Private Packagist synchronisiert werden.

Gehen Sie zunächst zur Registerkarte Pakete und suchen Sie nach dem monorepo:

![Screenshot des privaten Paketierers mit dem im Paketbildschirm sichtbaren monorepo-Paket](/help/assets/global-reference-architecture/packagist-packages-before-multi-package.png){align="center"}

Klicken Sie auf das MonoRepo-Paket und klicken Sie auf „Bearbeiten“ im Detailbildschirm, der Sie zur folgenden Seite führt:

![Screenshot des privaten Paketierers mit der monorepo-Paket-Bearbeitungsseite](/help/assets/global-reference-architecture/packagist-packages-edit.png)

Unter dem ersten Eingabefeld befindet sich ein Link, der besagt: Erstellen Sie ein Repository mit mehreren Paketen. Klicken Sie auf diesen Link.

![Screenshot des privaten Pakisters mit der Multi-Package-Konfiguration](/help/assets/global-reference-architecture/packagist-packages-multi-package.png)

Definieren Sie den Speicherort, an dem sich Composer-Pakete in Ihrem monorepo befinden. Im Beispiel ist der Speicherort `packages/**/composer.json`. Ändern Sie den Speicherort, um zu begrenzen oder zu erweitern, wo der Private-Package-Experte nach zu extrahierenden Paketen sucht.

Die Registerkarte Pakete zeigt alle gefundenen Pakete nach dem Speichern an, und das monorepo selbst ist nicht mehr als Composer-Paket sichtbar:

![Bildschirm „Private Packagist“ mit allen monorepo-Paketen, die im Bildschirm „Packages“ sichtbar sind](/help/assets/global-reference-architecture/packagist-packages-after-multi-package.png)

In Composer wird für jedes Paket innerhalb des monorepo eine Version für jedes Tag oder jede Verzweigung erstellt, das bzw. die in Git im monorepo erstellt wird.

## Installieren der Pakete in der Produktionsumgebung

Befolgen Sie die Anweisungen von Private Packagist, um Private Packagist als Composer-Repository hinzuzufügen. Private Packagist kann und sollte als Spiegel für alle Ihre Composer-Repositorys und Git-Repositorys verwendet werden, einschließlich packagist.org. Auf diese Weise müssen Anmeldeinformationen nicht für Entwickler freigegeben werden, und Sie haben die vollständige Kontrolle über jedes Paket. Dieses Beispiel folgt nicht dieser Best Practice, da es die Adobe Commerce-Codebasis öffentlich verfügbar machen würde.

Laden Sie [GRA Monorepo Brand X](https://github.com/AntonEvers/gra-monorepo-brand-x) von GitHub herunter, um ein Beispiel für einen Produktionsspeicher zu sehen.

Im Produktionsspeicher gibt es kein `packages` Verzeichnis, und alle Pakete werden über Composer installiert. Das einzige erforderliche Paket ist:

```json
    "require": {
        "antonevers/gra-meta-brand-x": "^1.0"
    },
```

Dennoch wird die gesamte Adobe Commerce und das gesamte GRA durch die Anforderungen dieses Metapakets installiert.

## Versionierung

Alle Pakete im monorepo erhalten die gleiche Version wie das monorepo selbst. Stellen Sie sich die Veröffentlichung neuer Versionen des gesamten Programms vor. In der Produktion können Sie jedoch eine Mischung aus Paketen aus verschiedenen monorepo-Versionen installieren.

## Vergängliche Umgebungen

Wenn Sie temporäre Umgebungen verwenden oder planen, diese zu verwenden, ist das monorepo eine hervorragende Wahl. Jede Version und Verzweigung des monorepo enthält alle Adobe Commerce-, Drittanbieter- und benutzerdefinierten Moduldateien. Mit einer kompletten Installation in jeder Verzweigung ist es möglich, jede Art von Test einschließlich Funktionstests durchzuführen. Bei anderen GRA-Setups, wie z. B. den separaten Packages oder Bulk Packages GRA, müssen Sie zunächst eine funktionierende Adobe Commerce-Umgebung erstellen, bevor Sie Funktionstests ausführen können. Aus DevOps-Perspektive macht es monorepo viel einfacher.

## Code-Beispiele

Die Code-Beispiele dieses Artikels wurden in einer Reihe von Git-Repositorys kombiniert, mit denen Sie den Machbarkeitsnachweis umspielen können.

- Ein Beispiel für ein monorepo-Repository: <https://github.com/AntonEvers/gra-monorepo>
- Ein Beispiel für einen Produktionsspeicher: <https://github.com/AntonEvers/gra-monorepo-brand-x>
