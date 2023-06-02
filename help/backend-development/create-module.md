---
title: Modul erstellen
description: Erstellen Sie eine Seite, die json mit einem Parameter zurückgibt.
topic: Development
kt: 5602
doc-type: video
activity: use
exl-id: 941c04ee-54b8-4b81-b77d-fff5875927f0
source-git-commit: 32d1366758fa6453a48570cfd08d10a93559a974
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Modul erstellen

Das Modul ist ein strukturelles Element von [!DNL Commerce] - das ganze System basiert auf Modulen. In der Regel besteht der erste Schritt beim Erstellen einer Anpassung darin, ein Modul zu erstellen.

## Für wen ist dieses Video?

- Entwickler

## Schritte zum Hinzufügen eines Moduls

- Erstellen Sie den Modulordner.
- Erstellen Sie die Datei etc/module.xml .
- Erstellen Sie die Datei registration.php .
- Führen Sie das Setup von bin/magento aus.
- Aktualisierungsskript zur Installation des neuen Moduls.
- Überprüfen Sie, ob das Modul funktioniert.

>[!VIDEO](https://video.tv.adobe.com/v/35792?learn=on)

### module.xml

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Training_Sales">
        <sequence>
            <module name="Magento_Sales"/>
        </sequence>
    </module>
</config>
```

### registration.php

```PHP
<?php

use Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'Training_Sales',
    __DIR__);
```

## Nützliche Ressourcen

- [Handbuch zur Modulreferenz](https://developer.adobe.com/commerce/php/module-reference/)
