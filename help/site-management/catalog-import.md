---
title: Erfahren Sie mehr über die nativen Katalogimportoptionen in Adobe Commerce
description: Erfahren Sie, wie Sie mit einigen nativen Optionen zum Importieren Ihres Katalogs in Ihren Adobe Commerce Store vorgehen können.
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
source-git-commit: 47a71d3523d5a894ca4edc458f7e2cf71c283618
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# Optionen zum Importieren eines Katalogs

Es gibt einige native Methoden zum Importieren eines Katalogs in Adobe Commerce. Jede Methode hat ihre eigene Begründung für die Verwendung sowie Vor- und Nachteile, die berücksichtigt werden müssen.

Wählen Sie eine der folgenden Optionen aus, um mehr zu erfahren.

>[!BEGINTABS]

>[!TAB Manuell]

## Manuelles Erstellen der Produkte {#manual-import}

Wenn Sie nur über einen begrenzten Katalog verfügen und nur selten Updates verfügbar sind, ist die manuelle Erstellung der Updates möglicherweise die beste Option. Es erfordert Zeit, um an jedem Produkt teilzunehmen, und einige eingeschränkte Schulungen zur Verwendung des Commerce-Administrators. Die manuelle Katalogverwaltung ist nicht die richtige Option für die meisten Geschäfte, aber in bestimmten Situationen kann es sinnvoll sein. Weitere Informationen zu diesem Prozess finden Sie unter [Produkt erstellen](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html){target="_blank"}. Vergessen Sie nicht, dass Sie mehrere Methoden zur Verwaltung Ihres Katalogs verwenden können. Sobald jedoch die Automatisierung verwendet wird, müssen manuelle Bearbeitungen eingeschränkt sein. Automatisierte Aktualisierungen haben die Möglichkeit, manuell durchgeführte Änderungen zu überschreiben, was zu Verwirrung führt. Sobald die Integration mit Adobe Commerce zur Verwaltung des Katalogs Automatisierung und APIs verwendet, wird empfohlen, die Verwaltung des Katalogs vom Administrator bis [Benutzerrollen und Berechtigungen](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html){target="_blank"}.



### Wann sollten Sie diesen Ansatz berücksichtigen?

- Sehr kleiner Katalog, zum Beispiel weniger als 50 Produkte
- Aktualisierungen sind selten
- Sie verfügen über alle Produktdetails, Bilder, Videos und möchten nicht die Zeit in Anspruch nehmen zu erfahren, wie Sie die Daten in CSV konvertieren
- Sie möchten beim Erstellen der Produkte Bilder und Videos hinzufügen
- Ihr Team ist `not` mit APIs und der Funktionsweise von OAUTH vertraut



>[!TAB Admin CSV]

## Admin-CSV-Import-Tool {#admin-csv}

Mit diesem Tool kann ein Store-Eigentümer einen Katalog mithilfe einer CSV-Berechtigung vom Commerce-Administrator importieren.
[Daten aus Commerce Admin importieren](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/import/data-import.html){target="_blank"}

Vorteile: Das Hochladen einer CSV-Datei vom Administrator ist ein direkter Ansatz für die Katalogverwaltung. Dies ermöglicht schnellere Katalogproduktaktualisierungen in einem mittelgroßen Katalog.

Nachteile:

- Langsam
- Maximale Upload-Datei, die auf dem Server definiert ist und von einem Store-Eigentümer möglicherweise nicht einfach angepasst werden kann.
- Erfordert Administratorzugriff und jemanden zum Ausführen der Aktion. Die Automatisierung ist eingeschränkt
- Zeitplanimporte sind auf das 1-fache der Tagesmax beschränkt.
- Die zugehörigen Bilder und Videos müssen separat hochgeladen werden



### Wann sollten Sie diesen Ansatz berücksichtigen?

- Kataloggröße ist mäßig
- Updates sind nicht mehr als einmal pro Tag
- Sie haben Zugriff auf Serverkonfigurationen, falls Sie die maximale Dateiupload-Größe erhöhen müssen.
- Ihr Team ist `not` mit APIs und der Funktionsweise von OAUTH vertraut



>[!TAB Massen-REST-API]

## Massen-REST-API {#bulk-rest-api}

Die Massen-REST-API ermöglicht Automatisierung und häufigere Aktualisierungen. Diese API ist schneller als der Administrator-Upload von CSV.
[Dokumentation zu Massen-Endpunkten](https://developer.adobe.com/commerce/webapi/rest/use-rest/bulk-endpoints/){target="_blank"}

Vorteile: Die Möglichkeit, große Datensätze zu importieren, die nicht im CSV-Format vorliegen.

Nachteile:

- Die zugehörigen Bilder und Videos müssen separat hochgeladen werden
- Kann durch Bandbreiteneinschränkungen für den Hosting-Provider begrenzt werden
- Sie müssen Optionsattribut-IDs verwenden, nicht die Beschriftungen



### Wann sollten Sie diesen Ansatz berücksichtigen?

- Katalog ist beliebig groß
- Aktualisierungen sind häufig, es ist mehr als 1x am Tag zulässig
- Die Zeit für den Import ist wichtig, aber nicht wichtig, und eine kurze Verzögerung bei der Verarbeitung der Einfuhrdaten ist akzeptabel.
- Die Daten sind nicht im CSV-Format strukturiert und können nicht mithilfe der Automatisierung transformiert werden



>[!TAB ASYNC REST API]

## ASYNC REST API {#async-rest-api}

Ein asynchroner Web-Endpunkt fängt Nachrichten an eine Web-API ab und schreibt sie in die Nachrichtenwarteschlange. Jedes Mal, wenn das System eine solche API-Anfrage akzeptiert, generiert es eine UUID-Kennung. Adobe Commerce fügt diese UUID hinzu, wenn die Nachricht der Warteschlange hinzugefügt wird. Anschließend liest ein Verbraucher die Nachrichten aus der Warteschlange und führt sie einzeln aus.
[Dokumentation zu asynchronen Web-Endpunkten](https://developer.adobe.com/commerce/webapi/rest/use-rest/asynchronous-web-endpoints/){target="_blank"}

Vorteile:

- Schnelles Importieren von Daten
- Der Speicherbereich wird unterstützt oder Sie können `all` zum Ausführen des Vorgangs für alle vorhandenen Speicher

Nachteile:

- GET-Anfrage wird nicht unterstützt

### Wann sollten Sie diesen Ansatz berücksichtigen?

- Häufig werden Einfuhren getätigt
- Kein Problem mit geringer Verzögerung ab dem Zeitpunkt, zu dem sie per API gesendet und dann aus der Nachrichtenwarteschlange verarbeitet werden.



>[!TAB CSV REST API]

## CSV REST API {#csv-rest-api}

Diese API-Option ermöglicht im Vergleich zu allen anderen nativen Optionen extrem schnelle Importe.

[Importieren von Daten REST CSV-API](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"}
Vorteile:

- Schnellste Methode zur Verarbeitung der eingehenden Daten
- Kann mehrmals pro Tag ausgeführt werden
- Daten können mit gzip für große Anforderungen komprimiert werden, um HTTP-Anforderungsgrößenbeschränkungen zu vermeiden.

Nachteile:

- Die zugehörigen Bilder und Videos müssen separat hochgeladen werden
- Die Daten müssen im CSV-Format vorliegen

### Wann sollten Sie diesen Ansatz berücksichtigen?

- Katalog ist beliebig groß
- Aktualisierungen sind häufig, es ist mehr als 1x am Tag zulässig
- Allgemeine Zeit für die Einfuhr ist wichtig
- Die Daten liegen bereits im CSV-Format vor oder können einfach mithilfe der Automatisierung transformiert werden



>[!ENDTABS]

## Zusätzliche Ressourcen

- [Importieren von Daten mit dem neuen REST CSV](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"}
- [Hauptdokumentation zum Importieren von Daten](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/import/data-import.html){target="_blank"}
- [Versionshinweise zur Adobe Commerce-Version 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/adobe-commerce/2-4-6.html){target="_blank"}
- [Benutzer, Rollen und Berechtigungen](../site-management/users-roles-permissions.md){target="_blank"}
