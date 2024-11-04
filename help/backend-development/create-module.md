---
title: Modul erstellen
description: Erfahren Sie, wie Sie ein Modul in Adobe Commerce erstellen, das Informationen an den PSR-Logger sendet. Dadurch wird Ihrem ersten Modul in Adobe Commerce eine Funktion hinzugefügt.
kt: 5614
doc-type: video
activity: use
last-substantial-update: 2023-6-2
feature: Configuration, System, Backend Development
topic: Commerce, Development
role: Admin, Developer
level: Beginner, Intermediate
exl-id: 941c04ee-54b8-4b81-b77d-fff5875927f0
source-git-commit: 4f6c8abec90663f80233b94456ad1e58edb86d51
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Modul erstellen

Das Modul ist ein Strukturelement von [!DNL Commerce] - das gesamte System basiert auf Modulen. In der Regel besteht der erste Schritt beim Erstellen einer Anpassung darin, ein Modul zu erstellen.

## Für wen ist dieses Video?

- Entwickler

## Schritte zum Hinzufügen eines Moduls

- Erstellen Sie den Ordner &quot;module&quot;.
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

```php
<?php

use Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'Training_Sales',
    __DIR__);
```

### Hinzufügen eines Plug-ins und Bereitstellen einiger Funktionen

Der nächste Schritt besteht darin, unserem grundlegenden Modul einige Funktionen hinzuzufügen. Ein Plug-in ist ein wichtiges Tool, das alle Adobe Commerce-Entwickler verwenden. In diesem Video und Tutorial können Sie ein Plug-in erstellen.

>[!VIDEO](https://video.tv.adobe.com/v/3420255?learn=on)

### Was Sie für Plug-ins beachten sollten

- Alle Plug-ins werden in `di.xml` deklariert.
- Das Plug-in benötigt einen eindeutigen Namen
- disabled und sortOrder sind optional
- Der Umfang des Plug-ins wird durch den Ordner festgelegt, in dem es sich befindet
- Plug-ins können vor, nach oder beide (um) ausgeführt werden, wobei die Methode aufgerufen wird
- Vermeiden Sie die Verwendung von `around` -Plug-ins. Sie sind versucht zu verwenden, sind aber oft die falsche Wahl und führen zu Leistungsproblemen.

### Beispiele für Plug-in-Code

Hier finden Sie die XML- und PHP-Klassen, die im Tutorial zum Hinzufügen eines Plug-ins zum ersten Modul verwendet werden

### app/code/Training/Sales/etc/adminhtml/di.xml

```xml
<?xml version="1.0" ?>
<!--
/**
 * Copyright &copy; Magento, Inc. All rights reserved.
 * See COPYING.txt for license details.
 */
-->
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <!-- A Plugin that executes when the admin user places an order -->
    <type name="Magento\Sales\Model\Order">
        <plugin name="admin-training-sales-add-logging" type="Training\Sales\Plugin\AdminAddLoggingAfterOrderPlacePlugin" disabled="false" sortOrder="0"/>
    </type>
</config>
```

### app/code/Training/Sales/etc/frontend/di.xml

```xml
<?xml version="1.0" ?>
<!--
/**
 * Copyright &copy; Magento, Inc. All rights reserved.
 * See COPYING.txt for license details.
 */
-->
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <!-- A plugin that executes when a customer uses the LoginPost controller from the Luma frontend -->
    <type name="Magento\Customer\Controller\Account\LoginPost">
        <plugin name="training-customer-loginpost-plugin"
                type="Training\Sales\Plugin\CustomerLoginPostPlugin" sortOrder="20"/>
    </type>
</config>
```

### app/code/Training/Sales/etc/webapi_rest/di.xml

```xml
<?xml version="1.0" ?>
<!--
/**
 * Copyright &copy; Magento, Inc. All rights reserved.
 * See COPYING.txt for license details.
 */
-->
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <!-- A plugin that executes when the REST API is used OR when the Luma frontend places an order -->
    <type name="Magento\Sales\Model\Order">
        <plugin name="rest-training-sales-add-logging" type="Training\Sales\Plugin\RestAddLoggingAfterOrderPlacePlugin"/>
    </type>
</config>
```

### app/code/Training/Sales/Plugin/AdminAddLoggingAfterOrderPlacePlugin.php

```php
<?php

declare(strict_types=1);

namespace Training\Sales\Plugin;

use Magento\Sales\Model\Order;
use Psr\Log\LoggerInterface;

/**
 *
 */
class AdminAddLoggingAfterOrderPlacePlugin
{

    /**
     * @var LoggerInterface
     */
    private LoggerInterface $logger;

    /**
     * @param LoggerInterface $logger
     */
    public function __construct(
        LoggerInterface $logger
    ) {
        $this->logger = $logger;
    }

    /**
     * Add log after an order is placed
     *
     * @param Order $subject
     * @param Order $result
     * @return Order
     */
    public function afterPlace(Order $subject, Order $result): Order
    {
        // Log this admin area order
        $this->logger->notice('An ADMIN User placed an Order - $' . $subject->getBaseTotalDue());
        return $result;
    }
}
```

### app/code/Training/Sales/Plugin/CustomerLoginPostPlugin.php

```php
<?php

declare(strict_types=1);

namespace Training\Sales\Plugin;

use Psr\Log\LoggerInterface;
use Magento\Framework\App\RequestInterface;

/**
 * Introduces Context information for ActionInterface of Customer Action
 */
class CustomerLoginPostPlugin
{

    /**
     * @var LoggerInterface
     */
    private LoggerInterface $logger;

    /**
     * @var RequestInterface
     */
    private RequestInterface $request;

    /**
     * @param LoggerInterface $logger
     * @param RequestInterface $request
     */
    public function __construct(LoggerInterface $logger, RequestInterface $request)
    {
        $this->logger = $logger;
        $this->request = $request;
    }

    /**
     * Simple example of a before Plugin on a public method in a Controller
     */
    public function beforeExecute()
    {
        $login = $this->request->getParam('login');
        $username = $login['username'];
        $this->logger->notice( "Login Post controller was used for " . $username );
    }
}
```

### app/code/Training/Sales/Plugin/RestAddLoggingAfterOrderPlacePlugin.php

```php
<?php

declare(strict_types=1);

namespace Training\Sales\Plugin;

use Magento\Sales\Model\Order;
use Psr\Log\LoggerInterface;

/**
 *
 */
class RestAddLoggingAfterOrderPlacePlugin
{

    /**
     * @var LoggerInterface
     */
    private LoggerInterface $logger;

    /**
     * @param LoggerInterface $logger
     */
    public function __construct(
        LoggerInterface $logger
    ) {
        $this->logger = $logger;
    }

    /**
     * Add log after an order is placed
     *
     * @param Order $subject
     * @param Order $result
     * @return Order
     */
    public function afterPlace(Order $subject, Order $result): Order
    {
        // Log this customer driven order
        $this->logger->notice('A Customer placed an Order for $' . $subject->getBaseTotalDue());
        return $result;
    }
}
```

## Nützliche Ressourcen

- [Modul-Referenzhandbuch](https://developer.adobe.com/commerce/php/module-reference/){target="_blank"}
- [Plugins](https://developer.adobe.com/commerce/php/development/components/plugins/){target="_blank"}
