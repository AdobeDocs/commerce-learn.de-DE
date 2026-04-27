---
title: Learn about catalog import options that come native with Adobe Commerce
description: Learn how a few of the native options for importing your catalog to your Adobe Commerce store.
kt: 13634
doc-type: tutorial
duration: 211
audience: all
activity: use
last-substantial-update: 2023-8-15
feature: Backend Development, Data Import/Export, REST
topic: Commerce, Administration, Content Management
role: Admin, User
level: Beginner, Intermediate
exl-id: 18713a44-df39-4b94-91ce-c7efeb4ce2b3
TQID: https://experienceleague.adobe.com/-JG7blrxImSXjA2DP9soZfsicISW0hkP2zJeWdMpVBU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 898
ht-degree: 0%

---

# Options for importing a catalog

There are a few native methods for importing a catalog into Adobe Commerce. Each method has its own reasoning for usage along with pros and cons that must be considered.

Choose from one of the options below to learn more.

>[!BEGINTABS]

>[!TAB Manual]

## Creating the products manually {#manual-import}

If you have a limited catalog and updates are infrequent, creating them manually might be the best option. It requires time to enter each product and some limited training to how to use the Commerce Admin. Manual catalog management is not the right option for most stores, but in certain situations, it may make sense. To see additional documentation for this process, visit [Create a product](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=de){target="_blank"}. Do not forget, you can use more than one method to manage your catalog, however once automation is used, manual edits must be limited. Automated updates have the opportunity to overwrite any changes performed manually, and therefore cause confusion. Once the integration with Adobe Commerce to manage the catalog is using automation and APIs, it is advised to restrict management of the catalog from the admin through [user roles and permissions](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html?lang=de){target="_blank"}.

### When to consider this approach

* Very small catalog, for example fewer than 50 products
* Updates are infrequent
* You have all the product details, images, videos, and you do not want to take the time to learn how to convert the data to CSV
* Sie möchten beim Erstellen der Produkte das Hinzufügen von Bildern und Videos einbeziehen
* Ihr Team ist `not` mit APIs und der Funktionsweise von OAUTH vertraut

>[!TAB Admin-CSV]

## Admin CSV Import Tool {#admin-csv}

Mit diesem Tool kann ein Store-Inhaber einen Katalog mithilfe einer CSV-Datei direkt vom Commerce-Administrator importieren.
[Daten von Commerce Admin importieren](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/import/data-import.html?lang=de){target="_blank"}

Vorteile:
Das Hochladen einer CSV-Datei von der Administratorin bzw. dem Administrator ist ein unkomplizierter Ansatz für die Katalogverwaltung. Dies ermöglicht schnellere Katalogproduktaktualisierungen auf einen Katalog mittlerer Größe.

Nachteile:

* Langsam
* Die maximale Größe der Upload-Datei ist auf dem Server definiert und kann von einem Store-Inhaber möglicherweise nicht einfach angepasst werden.
* Erfordert Administratorzugriff und jemanden, der die Aktion ausführt, ist die Automatisierung eingeschränkt
* Geplante Importe sind auf maximal 1 x täglich beschränkt
* Die zugehörigen Bilder und Videos müssen separat hochgeladen werden

### Wann dieser Ansatz in Betracht zu ziehen ist

* Kataloggröße ist moderat
* Aktualisierungen werden nicht öfter als einmal täglich durchgeführt
* Sie haben einige Zugriffsrechte auf Server-Konfigurationen, falls Sie die maximale Größe des Datei-Uploads erhöhen müssen
* Ihr Team ist `not` mit APIs und der Funktionsweise von OAUTH vertraut

>[!TAB Massen-REST-API]

## Massen-REST-API {#bulk-rest-api}

Die Massen-REST-API ermöglicht eine Automatisierung und häufigere Aktualisierungen. Diese API ist schneller als der Admin-Upload von CSV.
[Dokumentation zu Massenendpunkten](https://developer.adobe.com/commerce/webapi/rest/use-rest/bulk-endpoints/){target="_blank"}

Vorteile:
The ability to import large data sets that are not in CSV format.

Nachteile:

* Die zugehörigen Bilder und Videos müssen separat hochgeladen werden
* Can be limited by bandwidth constraints on the hosting provider

### Wann dieser Ansatz in Betracht zu ziehen ist

* Catalog is any size
* Updates are frequent, more than 1x a day is acceptable
* Time to import is important but not critical and a short delay in processing the import data is acceptable
* The data is not structured in CSV format and you are not capable of transforming it using automation

>[!TAB ASYNC REST API]

## ASYNC REST API {#async-rest-api}

An asynchronous web endpoint intercepts messages to a Web API and writes them to the message queue. Each time the system accepts such an API request, it generates a UUID identifier. Adobe Commerce includes this UUID when it adds the message to the queue. Then, a consumer reads the messages from the queue and executes them one-by-one.
[Asynchronous web endpoints documentation](https://developer.adobe.com/commerce/webapi/rest/use-rest/asynchronous-web-endpoints/){target="_blank"}

Vorteile:

* Fast to import data
* Store scope is supported or you can specify `all` to perform operation on all existing stores

Nachteile:

* GET request are not supported

### Wann dieser Ansatz in Betracht zu ziehen ist

* Imports are frequent
* No issue with a small delay from the time they are submitted via API and then processed from the message queue.


>[!TAB CSV-REST-API]

## CSV-REST-API {#csv-rest-api}

Diese API-Option ermöglicht im Vergleich zu allen anderen nativen Optionen extrem schnelle Importe.

[Daten-REST-CSV-API importieren](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"}
Vorteile:

* Schnellste Methode zur Verarbeitung der eingehenden Daten
* Kann mehrmals täglich ausgeführt werden
* Daten können mit gzip für große Anfragen komprimiert werden, um Größenbeschränkungen für HTTP-Anfragen zu vermeiden.

Nachteile:

* Die zugehörigen Bilder und Videos müssen separat hochgeladen werden
* Die Daten müssen im CSV-Format vorliegen.

### Wann dieser Ansatz in Betracht zu ziehen ist

* Katalog ist eine beliebige Größe
* Updates werden häufig durchgeführt, mehr als 1x täglich ist akzeptabel
* Wichtig ist die Gesamtzeit für den Import
* Die Daten liegen bereits im CSV-Format vor oder können einfach durch Automatisierung transformiert werden

>[!ENDTABS]

## Zusätzliche Ressourcen

* [Daten mit der neuen REST-CSV importieren](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"}
* [Hauptdokumentation zum Datenimport](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/import/data-import.html?lang=de){target="_blank"}
* [Versionshinweise zu Adobe Commerce Version 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/adobe-commerce/2-4-6.html?lang=de){target="_blank"}
* [Benutzer, Rollen und Berechtigungen](../site-management/users-roles-permissions.md){target="_blank"}
