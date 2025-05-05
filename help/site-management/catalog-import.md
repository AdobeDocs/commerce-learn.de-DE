---
title: Erfahren Sie mehr über die Katalogimportoptionen in Adobe Commerce
description: Erfahren Sie mehr über einige der nativen Optionen zum Importieren Ihres Katalogs in Ihren Adobe Commerce-Store.
kt: 13634
doc-type: tutorial
audience: all
activity: use
last-substantial-update: 2023-8-15
feature: Backend Development, Data Import/Export, REST
topic: Commerce, Administration, Content Management
role: Admin, User
level: Beginner, Intermediate
exl-id: 18713a44-df39-4b94-91ce-c7efeb4ce2b3
source-git-commit: b0fe49352b00a68554e662327cd66983c30d8285
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# Optionen zum Importieren eines Katalogs

Es gibt einige native Methoden zum Importieren eines Katalogs in Adobe Commerce. Jede Methode hat ihre eigenen Gründe für die Verwendung zusammen mit den Vor- und Nachteilen, die berücksichtigt werden müssen.

Wählen Sie eine der folgenden Optionen aus, um mehr zu erfahren.

>[!BEGINTABS]

>[!TAB Manuell]

## Manuelles Erstellen der Produkte {#manual-import}

Wenn Sie nur über einen begrenzten Katalog verfügen und Aktualisierungen selten auftreten, ist es möglicherweise am besten, sie manuell zu erstellen. Die Eingabe der einzelnen Produkte dauert einige Zeit, und für die Verwendung von Commerce Admin sind einige begrenzte Schulungen erforderlich. Die manuelle Katalogverwaltung ist für die meisten Geschäfte nicht die richtige Option, kann aber in bestimmten Situationen sinnvoll sein. Weitere Dokumentationen zu diesem Prozess finden Sie unter [Produkt erstellen](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=de){target="_blank"}. Vergessen Sie nicht, dass Sie mehr als eine Methode zur Verwaltung Ihres Katalogs verwenden können. Sobald jedoch eine Automatisierung verwendet wird, müssen manuelle Bearbeitungen eingeschränkt werden. Automatisierte Aktualisierungen bieten die Möglichkeit, manuell durchgeführte Änderungen zu überschreiben und dadurch Verwirrung zu stiften. Sobald die Integration mit Adobe Commerce zum Verwalten des Katalogs mithilfe von Automatisierung und APIs erfolgt, wird empfohlen, die Katalogverwaltung vom Administrator durch [Benutzerrollen und -berechtigungen](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html?lang=de){target="_blank"} einzuschränken.

### Wann dieser Ansatz in Betracht zu ziehen ist

- Sehr kleiner Katalog, zum Beispiel weniger als 50 Produkte
- Aktualisierungen treten selten auf
- Sie verfügen über alle Produktdetails, Bilder und Videos und möchten sich nicht die Zeit nehmen, um zu erfahren, wie die Daten in CSV konvertiert werden
- Sie möchten beim Erstellen der Produkte das Hinzufügen von Bildern und Videos einbeziehen
- Ihr Team ist `not` mit APIs und der Funktionsweise von OAUTH vertraut

>[!TAB Admin-CSV]

## Admin CSV Import Tool {#admin-csv}

Mit diesem Tool kann ein Store-Inhaber einen Katalog mithilfe einer CSV-Datei direkt vom Commerce-Administrator importieren.
[Daten von Commerce Admin importieren](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/import/data-import.html?lang=de){target="_blank"}

Vorteile:
Das Hochladen einer CSV-Datei von der Administratorin bzw. dem Administrator ist ein unkomplizierter Ansatz für die Katalogverwaltung. Dies ermöglicht schnellere Katalogproduktaktualisierungen auf einen Katalog mittlerer Größe.

Nachteile:

- Langsam
- Die maximale Größe der Upload-Datei ist auf dem Server definiert und kann von einem Store-Inhaber möglicherweise nicht einfach angepasst werden.
- Erfordert Administratorzugriff und jemanden, der die Aktion ausführt, ist die Automatisierung eingeschränkt
- Geplante Importe sind auf maximal 1 x täglich beschränkt
- Die zugehörigen Bilder und Videos müssen separat hochgeladen werden

### Wann dieser Ansatz in Betracht zu ziehen ist

- Kataloggröße ist moderat
- Aktualisierungen werden nicht öfter als einmal täglich durchgeführt
- Sie haben einige Zugriffsrechte auf Server-Konfigurationen, falls Sie die maximale Größe des Datei-Uploads erhöhen müssen
- Ihr Team ist `not` mit APIs und der Funktionsweise von OAUTH vertraut

>[!TAB Massen-REST-API]

## Massen-REST-API {#bulk-rest-api}

Die Massen-REST-API ermöglicht eine Automatisierung und häufigere Aktualisierungen. Diese API ist schneller als der Admin-Upload von CSV.
[Dokumentation zu Massenendpunkten](https://developer.adobe.com/commerce/webapi/rest/use-rest/bulk-endpoints/){target="_blank"}

Vorteile:
Die Möglichkeit, große Datensätze zu importieren, die nicht im CSV-Format vorliegen.

Nachteile:

- Die zugehörigen Bilder und Videos müssen separat hochgeladen werden
- Kann durch Bandbreitenbeschränkungen auf den Hosting-Provider beschränkt werden

### Wann dieser Ansatz in Betracht zu ziehen ist

- Katalog ist eine beliebige Größe
- Updates werden häufig durchgeführt, mehr als 1x täglich ist akzeptabel
- Die Importzeit ist wichtig, aber nicht kritisch, und eine kurze Verzögerung bei der Verarbeitung der Importdaten ist akzeptabel
- Die Daten sind nicht im CSV-Format strukturiert und können nicht mithilfe der Automatisierung umgewandelt werden

>[!TAB ASYNC-REST-API]

## ASYNC REST-API {#async-rest-api}

Ein asynchroner Web-Endpunkt fängt Nachrichten an eine Web-API ab und schreibt sie in die Nachrichtenwarteschlange. Jedes Mal, wenn das System eine solche API-Anfrage akzeptiert, generiert es eine UUID-Kennung. Adobe Commerce fügt diese UUID hinzu, wenn es die Nachricht zur Warteschlange hinzufügt. Anschließend liest ein Verbraucher die Nachrichten aus der Warteschlange und führt sie einzeln aus.
[Dokumentation zu asynchronen Web-Endpunkten](https://developer.adobe.com/commerce/webapi/rest/use-rest/asynchronous-web-endpoints/){target="_blank"}

Vorteile:

- Schneller Datenimport
- Der Store-Bereich wird unterstützt oder Sie können angeben, `all` Vorgänge für alle vorhandenen Stores ausgeführt werden sollen

Nachteile:

- GET-Anfragen werden nicht unterstützt

### Wann dieser Ansatz in Betracht zu ziehen ist

- Importe sind häufig
- Kein Problem mit einer kleinen Verzögerung ab dem Zeitpunkt, zu dem sie über die API gesendet und dann aus der Nachrichtenwarteschlange verarbeitet werden.


>[!TAB CSV-REST-API]

## CSV-REST-API {#csv-rest-api}

Diese API-Option ermöglicht im Vergleich zu allen anderen nativen Optionen extrem schnelle Importe.

[Daten-REST-CSV-API importieren](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"}
Vorteile:

- Schnellste Methode zur Verarbeitung der eingehenden Daten
- Kann mehrmals täglich ausgeführt werden
- Daten können mit gzip für große Anfragen komprimiert werden, um Größenbeschränkungen für HTTP-Anfragen zu vermeiden.

Nachteile:

- Die zugehörigen Bilder und Videos müssen separat hochgeladen werden
- Die Daten müssen im CSV-Format vorliegen.

### Wann dieser Ansatz in Betracht zu ziehen ist

- Katalog ist eine beliebige Größe
- Updates werden häufig durchgeführt, mehr als 1x täglich ist akzeptabel
- Wichtig ist die Gesamtzeit für den Import
- Die Daten liegen bereits im CSV-Format vor oder können einfach durch Automatisierung transformiert werden

>[!ENDTABS]

## Zusätzliche Ressourcen

- [Importieren von Daten mit der neuen REST-CSV](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"}
- [Hauptdokumentation zum Datenimport](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/import/data-import.html?lang=de){target="_blank"}
- Versionshinweise zu [Adobe Commerce Version 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/adobe-commerce/2-4-6.html?lang=de){target="_blank"}
- [Benutzer, Rollen und Berechtigungen](../site-management/users-roles-permissions.md){target="_blank"}
