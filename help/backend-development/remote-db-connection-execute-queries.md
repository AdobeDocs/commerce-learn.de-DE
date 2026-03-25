---
title: Verbinden und Ausführen von Abfragen mit der Adobe Commerce-Datenbank
description: Stellen Sie eine Verbindung zu einem Adobe Commerce on Cloud-Projekt her, erstellen Sie einen Datenbank-Dump für die Offsite-Verwendung, maskieren oder entfernen Sie personenbezogene Daten und führen Sie SQL mit der Cloud-CLI, einem GUI-Client oder Direktverbindungen aus.
feature: Backend Development,Console,Cloud
topic: Commerce,Development
role: Developer
level: Intermediate, Experienced
doc-type: Technical Video
duration: 1024
last-substantial-update: 2024-06-25T00:00:00Z
jira: KT-14910
exl-id: e740bbd0-5ec7-4272-89cb-0bed776eb149
source-git-commit: d2c01abbc24ec14f6147004bb9a13ebdbfb8b60e
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---

# Verbinden und Ausführen von Abfragen mit der Adobe Commerce-Datenbank

Erfahren Sie, wie Sie eine Verbindung zu einem Adobe Commerce on Cloud-Projekt herstellen, einen Datenbank-Dump für die Offsite-Verwendung erstellen und personenbezogene Daten maskieren oder entfernen können. Greifen Sie auf Daten mit einem lokalen Dump, einer GUI wie MySQL Workbench oder TablePlus oder der `magento-cloud` CLI zu.

## Videoinhalte

* Stellen Sie mit einem GUI-Tool wie MySQL Workbench oder TablePlus eine Verbindung zu einem Remote-Adobe Commerce-Cloud-Projekt her.
* Stellen Sie eine Verbindung mit dem Projekt her und führen Sie SQL über die Befehlszeile aus.

>[!VIDEO](https://video.tv.adobe.com/v/3430507?learn=on)

Sie können mit einer der folgenden Methoden auf Adobe Commerce-Daten aus Ihrem Cloud-Projekt zugreifen:

* Verwenden Sie einen lokalen DB-Dump.
* Öffnen Sie mit einer Anwendung wie MySQL Workbench oder TablePlus eine DB-Verbindung zu Ihrer Remote-Cloud-Umgebung.
* Stellen Sie mit der `magento-cloud` CLI eine direkte Verbindung zur Cloud-Umgebung her und führen Sie Befehle auf dem Remote-Server aus.

Es wird empfohlen, einen Datenbank-Dump zu löschen, um Kundeninformationen zu entfernen. Entfernen Sie Kundendaten vollständig, wenn Sie sie nicht benötigen.

## Verwenden des Adobe Commerce Cloud CLI-Tools

Zum Erstellen eines Datenbank[Dump muss die &#x200B;](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli/cloud-cli-overview.html)Adobe Commerce Cloud CLI) installiert sein. Öffnen Sie auf dem lokalen Computer ein Verzeichnis und führen Sie den folgenden Befehl aus. Ersetzen Sie `your-project-id` durch Ihre Projekt-ID (ähnlich wie `asasdasd45q`). Ersetzen Sie `your-environment-name` durch den Namen Ihrer Umgebung, z. B. `master` oder `staging`.

`magento-cloud db:dump -p your-project-id -e your-environment-name`

Wenn Sie sich bezüglich der Projekt-ID oder der Umgebung nicht sicher sind, können Sie diese im Befehl weglassen:

`magento-cloud db:dump`

Die CLI fordert Sie auf, das richtige Projekt und die richtige Umgebung anzugeben. Im folgenden Beispiel wird dieses Dialogfeld angezeigt. Dieses Beispiel zeigt mehrere Projekte, die Ihrem Konto zugewiesen sind, aber Sie haben wahrscheinlich nur ein Projekt zur Verfügung.

In Verzeichnis ändern

```bash
cd ~/Downloads/db-tutorial 
```

Führen Sie nun den Befehl aus, um den Datenbank-Dump zu erstellen

```bash
magento-cloud db:dump
```

Da Sie kein Projekt oder keine Umgebung angegeben haben, stellt die Adobe Commerce Cloud-CLI einige Fragen. Das folgende Beispiel zeigt ein Beispieldialogfeld.

```bash
Enter a number to choose a project:
  [0] demo-ralbin (ral32nryq4123)
  [1] adobe-commerce-demo (abc123zzkipexnqo)
  [2] DX Tutorials - Commerce (abasrpikfw4123)
 > 2

Enter a number to choose an environment:
Default: master
  [0] master (type: production)
  [1] remote-db (type: development)
 > 1

Creating SQL dump file: /Users/<username>/Downloads/db-tutorial/abasrpikfw4123--remote-db-ecpefky--mysql--main--dump.sql
```

## Verwenden der Adobe Commerce ECE-Tools

Wenn Sie nicht über das Adobe Commerce-CLI-Tool verfügen, können Sie in Ihr Projekt `ssh` und den `ece`-`vendor/bin/ece-tools db-dump` ausführen:
Beispielantwort:

```bash
ssh abasrpikfw4123-remote-db-ecpefky--mymagento@ssh.us-4.magento.cloud

 __  __                   _          ___ _             _ 
|  \/  |__ _ __ _ ___ _ _| |_ ___   / __| |___ _  _ __| |
| |\/| / _` / _` / -_) ' \  _/ _ \ | (__| / _ \ || / _` |
|_|  |_\__,_\__, \___|_||_\__\___/  \___|_\___/\_,_\__,_|
            |___/                                        

 Welcome to Magento Cloud.

 This is environment remote-db-ecpefky
 of project abasrpikfw4123.

web@mymagento.0:~$ vendor/bin/ece-tools db-dump
The db-dump operation switches the site to maintenance mode, stops all active cron jobs and consumer queue processes, and disables cron jobs before starting the dump process.
Your site will not receive any traffic until the operation completes.
Do you wish to proceed with this process? (y/N)?y
[2024-02-13T19:01:45.130999+00:00] INFO: Starting backup.
[2024-02-13T19:01:45.155039+00:00] NOTICE: Enabling Maintenance mode
[2024-02-13T19:01:46.404427+00:00] INFO: Trying to kill running cron jobs and consumers processes
[2024-02-13T19:01:46.420149+00:00] INFO: Running Magento cron and consumers processes were not found.
[2024-02-13T19:01:46.420434+00:00] INFO: Waiting for lock on db dump.
[2024-02-13T19:01:46.420499+00:00] INFO: Start creation DB dump for main database...
[2024-02-13T19:01:50.697886+00:00] INFO: Finished DB dump for main database, it can be found here: /app/var/dump-main-1707850906.sql.gz
[2024-02-13T19:01:51.628328+00:00] NOTICE: Maintenance mode is disabled.
[2024-02-13T19:01:51.628419+00:00] INFO: Backup completed.
web@mymagento.0:~$ exit
logout
Connection to ssh.us-4.magento.cloud closed.
```

Verwenden Sie `SFTP` oder `rsync`, um den Datenbank-Dump in Ihre lokale Umgebung zu ziehen.

Im folgenden Beispiel wird `rsync` verwendet, um die Datei in den `~/Downloads/db-tutorial` Ordner zu ziehen.

```bash
rsync -avrp -e ssh abasrpikfw4123-remote-db-ecpefky--mymagento@ssh.us-4.magento.cloud:/app/var/dump-main-1707850906.sql.gz ~/Downloads/db-tutorial
```

Das Terminal-Fenster gibt einige Informationen aus. Hier ist ein Beispiel für die Ausgabe

```bash
rsync -avrp -e ssh abasrpikfw4123-remote-db-ecpefky--mymagento@ssh.us-4.magento.cloud:/app/var/dump-main-1707850906.sql.gz ~/Downloads/db-tutorial
receiving file list ... done
dump-main-1707850906.sql.gz

sent 38 bytes  received 2691041 bytes  358810.53 bytes/sec
total size is 2690241  speedup is 1.00
```

Zeigen Sie den Inhalt der Datei an, um sicherzustellen, dass sie erfolgreich heruntergeladen wurde.

```bash
ls -lah
total 29840
drwxr-xr-x    4 <username>  staff   128B Feb 13 13:02 .
drwx------@ 103 <username>   staff   3.2K Feb 13 12:52 ..
-rw-r--r--    1 <username>   staff    11M Feb 13 12:53 abasrpikfw4123--remote-db-ecpefky--mysql--main--dump.sql
-rw-r--r--    1 <username>   staff   2.6M Feb 13 13:01 dump-main-1707850906.sql.gz
```

Nachdem Sie die Daten haben, stellen Sie sicher, dass Sie sie bereinigen, indem Sie die Kundendaten entfernen oder maskieren. Das folgende Beispielskript hilft Ihnen bei den ersten Schritten.

Dieses Beispiel wandelt Kundendaten in zufällige Zeichenfolgen um, behält jedoch alle Elemente bei. Dieses Beispiel enthält einige zusätzliche Tabellen, um zu demonstrieren, dass Kunden-PII sowohl in Drittanbietertabellen als auch in Kerntabellen zu finden sind. Überprüfen Sie die Daten in jeder Tabelle sorgfältig und maskieren oder entfernen Sie alle Kundendaten.

Normalerweise ist der Architekt oder der leitende Entwickler die einzige Person, die für das Maskieren und Bereinigen von Datenbank-Dumps verantwortlich ist. Ein dediziertes Sanitizer verringert die Exposition der Rohdaten, was die Möglichkeit von Verstößen gegen Compliance-Regeln und -Vorschriften verringert.

```sql
SET FOREIGN_KEY_CHECKS=0;
UPDATE customer_entity SET email = REPLACE(email, SUBSTRING(email, LOCATE('@', email) +1), CONCAT(UUID(), '.com'));
UPDATE email_contact SET email = REPLACE(email, SUBSTRING(email, LOCATE('@', email) +1), CONCAT(UUID(), '.com'));
UPDATE sales_invoice_grid SET customer_email = 'customer@example.com', customer_name  = 'Jack Smith';
UPDATE sales_order SET customer_email = 'customer@example.com', customer_firstname = 'Sally', customer_lastname = 'Smith', remote_ip = '127.0.0.1';
UPDATE sales_order_address SET region = 'Ohio', postcode = '12345-1234', lastname = 'Smith', street = '123 Main street', region_id = 44, city = 'Phoenix', telephone = NULL, firstname = 'Jane', company = NULL;
UPDATE sales_order_grid SET customer_email = 'customer@example.com', shipping_name = 'Jack', billing_name = 'Jack Smith', billing_address = '123 Main Street', shipping_address = '321 Pine Street', customer_name = 'Jane Smith';
UPDATE sales_shipment_grid SET customer_email = 'customer@example.com', customer_name = 'Jane Smith', billing_address = '123 Main street', billing_name = 'Jack Doe', shipping_name = 'Susie Smith';
UPDATE quote SET customer_email = 'customer@example.com', customer_firstname = 'Sally', customer_lastname = 'Jones', customer_dob = NULL, remote_ip = '127.0.0.1';
UPDATE quote_address SET email = 'customer@example.com', firstname = 'Jack', lastname = 'Smith', company = NULL, street = '123 Main st', city = 'AnyCity', region = 'Some State', region_id = 44, postcode = '12345-1234', telephone = NULL;
UPDATE magento_rma SET customer_custom_email = 'customer@example.com' WHERE customer_custom_email IS NOT NULL;
UPDATE customer_address_entity SET firstname = 'Jack', lastname = 'Smith', telephone = '909-555-1212', postcode = NULL,  region = NULL, street = '123 Main street', city = 'Anycity', company = NULL;
UPDATE customer_grid_flat SET name = 'Jane Doe', email = 'customer@example.com', dob = NULL, gender = NULL, taxvat = NULL, shipping_full = '', billing_full = '', billing_firstname = 'Jack', billing_lastname = 'Smith', billing_telephone = NULL, billing_postcode = NULL, billing_country_id = NULL, billing_region = NULL, billing_street = '123 Main street', billing_city = 'Anycity', billing_fax = NULL, billing_vat_id = NULL, billing_company = NULL;
UPDATE sales_creditmemo_grid SET billing_name = 'Sally', billing_address = '123 Main Street', customer_name = 'Jack Smith', customer_email = 'customer@example.com';
UPDATE magento_rma_grid SET customer_name = 'Jack Smith';
UPDATE newsletter_subscriber SET subscriber_email = 'customer@example.com';
UPDATE core_config_data SET value = '' WHERE path = 'orderexport/general/serial';
UPDATE core_config_data SET value = '' WHERE path = 'productexport/general/serial';
UPDATE core_config_data SET value = '' WHERE path = 'trackingimport/general/serial';
UPDATE core_config_data SET value = '' WHERE path = 'stockimport/general/serial';
UPDATE core_config_data SET value = '' WHERE path = 'remarketing/onescript/merchant_id';
UPDATE core_config_data SET value = '' WHERE path = 'remarketing/onescript/merchant_id';
UPDATE core_config_data SET value = '' WHERE path = 'algoliasearch_credentials/credentials/application_id';
UPDATE core_config_data SET value = '' WHERE path = 'algoliasearch_credentials/credentials/search_only_api_key';
UPDATE core_config_data SET value = '' WHERE path = 'tax/avatax/production_account_number';
UPDATE core_config_data SET value = '' WHERE path = 'tax/avatax/production_license_key';
UPDATE core_config_data SET value = '' WHERE path = 'design/head/includes';
UPDATE core_config_data SET value = '' WHERE path = 'payment/braintree/merchant_id';
UPDATE core_config_data SET value = '' WHERE path = 'payment/braintree/public_key';     
UPDATE core_config_data SET value = '' WHERE path = 'payment/braintree/private_key';
UPDATE core_config_data SET value = '' WHERE path = 'system/full_page_cache/fastly/fastly_service_id';
UPDATE core_config_data SET value = '' WHERE path = 'system/full_page_cache/fastly/fastly_api_key';
UPDATE core_config_data SET value = '' WHERE path = 'google/analytics/container_id';  
UPDATE core_config_data SET value = '' WHERE path = 'analytics/general/token';
UPDATE vault_payment_token SET public_hash = UUID(), details = '{"type":"VI","maskedCC":"1111","expirationDate":"01\/2019"}';
TRUNCATE customer_log; 
TRUNCATE customer_visitor; 
TRUNCATE magento_logging_event;
TRUNCATE oauth_consumer;
TRUNCATE oauth_nonce;
TRUNCATE oauth_token;
TRUNCATE password_reset_request_event;
TRUNCATE acknowledgement;
TRUNCATE acknowledgement_report;
TRUNCATE avatax_log;
TRUNCATE avatax_queue;
TRUNCATE cron_schedule;
SET FOREIGN_KEY_CHECKS=1;
```

Alternativ können Sie die Datensätze löschen, anstatt die Informationen zu maskieren, was die neue DB ebenfalls verkleinert. Sobald personenbezogene Daten maskiert oder entfernt wurden, können die Daten sicher einem Teamkollegen zur Verwendung in seiner lokalen Umgebung bereitgestellt werden.

## Remote-DB-Verbindung zu einem Adobe Commerce Cloud-Projekt

Diese Methode ermöglicht die versehentliche Bearbeitung und Löschung von Live-Daten. Verwenden Sie es mit Vorsicht. Datenbank-Backup und Offline-Überprüfung bevorzugen, wenn möglich. Manchmal müssen Sie direkt auf Daten in Adobe Commerce Cloud zugreifen. Dieser Workflow ist weiterhin mit Risiken verbunden. GUIs fügen keine Bestätigungsaufforderungen hinzu, sodass Sie versehentlich Daten ändern oder entfernen können.

Eine Remote-Datenbankverbindung ist praktisch, aber riskant. Sie können leicht vergessen, dass Sie mit der Produktion verbunden sind und Daten löschen oder ändern. Sie können eine Verbindung zu einem schreibgeschützten Replikat herstellen, doch die hohe SQL-Anzahl wirkt sich weiterhin auf die Site aus. Adobe empfiehlt keine routinemäßigen Remote-Verbindungen zu beschreibbaren Datenbanken. Führen Sie die folgenden Schritte nur aus, wenn Sie die Risiken verstehen.

SSH-Tunnel einrichten:

```bash
magento-cloud tunnel:open
```

Nachdem das Projekt ausgewählt und die Umgebung ausgewählt wurde, gibt es eine Ausgabe des Befehls , der in den Einstellungen für die grafische Benutzeroberfläche von MySQL verwendet wird.

```bash
magento-cloud tunnel:open

Enter a number to choose a project:
  [0] demo-ralbin (ral32nryq4123)
  [1] adobe-commerce-demo (abc123zzkipexnqo)
  [2] DX Tutorials - Commerce (abasrpikfw4123)
 > 2

Enter a number to choose an environment:
Default: master
  [0] master (type: production)
  [1] remote-db (type: development)
 > 1

SSH tunnel opened to database at: mysql://user:@127.0.0.1:30000/main
SSH tunnel opened to redis at: redis://127.0.0.1:30001
SSH tunnel opened to opensearch at: http://127.0.0.1:30002
SSH tunnel opened to rabbitmq at: amqp://guest:guest@127.0.0.1:30003

Logs are written to: /Users/<user>/.magento-cloud/tunnels.log

List tunnels with: magento-cloud tunnels
View tunnel details with: magento-cloud tunnel:info
Close tunnels with: magento-cloud tunnel:close

Save encoded tunnel details to the MAGENTO_CLOUD_RELATIONSHIPS variable using:
  export MAGENTO_CLOUD_RELATIONSHIPS="$(magento-cloud tunnel:info --encode)"
```

Stellen Sie mithilfe der `SSH tunnel opened to database at`-Befehlsoption eine Verbindung über eine grafische MySQL-Schnittstelle her.

```bash
SSH tunnel opened to database at: mysql://user:@127.0.0.1:30000/main
```

Nachdem Sie nun über die richtigen Informationen verfügen, geben Sie diese Werte in die Cloud-Konsole ein.

Den SSH-Hostnamen und Benutzernamen finden Sie in den Cloud-Anmeldedaten in der Cloud-Konsole.

![Adobe Commerce Cloud-Konsole](./assets/cloud-ui-screenshot.png "Adobe Commerce Cloud-Konsole")

Im Folgenden finden Sie ein Beispiel: `ssh abasrpikfw4123-remote-db-ecpefky--mymagento@ssh.us-4.magento.cloud`
Der SSH-Hostname ist in diesem Beispiel alles nach dem @-Zeichen: `ssh.us-4.magento.cloud`.
Der SSH-Benutzername liegt vor dem @-Zeichen: `abasrpikfw4123-remote-db-ecpefky--mymagento`

## Suchen von Werten für die Verbindung zur Datenbank

Um direkt auf die MariaDB-Datenbank zuzugreifen, verwenden Sie SSH, um sich bei der Remote-Cloud-Umgebung anzumelden und eine Verbindung zur Datenbank herzustellen.

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

2. Abrufen der MySQL-Anmeldeinformationen aus den `database`- und `type`-Eigenschaften in der Variablen [$MAGENTO_CLOUD_RELATIONSHIPS](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/properties/properties.html?lang=en#relationships).

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   oder

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   Suchen Sie in der Antwort die MySQL-Informationen. Beispiel:

   ```json
   "database" : [
      {
         "password" : "",
         "rel" : "mysql",
         "hostname" : "nnnnnnnn.mysql.service._.magentosite.cloud",
         "service" : "mysql",
         "host" : "database.internal",
         "ip" : "###.###.###.###",
         "port" : 3306,
         "path" : "main",
         "cluster" : "projectid-integration-id",
         "query" : {
            "is_master" : true
         },
         "type" : "mysql:10.3",
         "username" : "user",
         "scheme" : "mysql"
      }
   ],
   ```

Verwenden Sie dann die Konfigurationswerte in Ihrer MySQL-GUI. Im folgenden Beispiel wird MySQL Workbench verwendet, aber jede App, die MySQL-Verbindungen unterstützt, hat ähnliche Felder.

![MySQL Workbench-Verbindungsbeispiel](./assets/mysql-workbench-after-connecting.png "MySQL Workbench-Verbindungsbeispiel")

![TablePlus-Verbindungsbeispiel](./assets/tablesPlus-db-connection.png "TablePlus-Verbindungsbeispiel")

Nachdem Sie die Verbindung konfiguriert haben, können Sie eine MySQL-GUI verwenden, um Abfragen in einem Remote-Adobe Commerce-Cloud-Projekt auszuführen.

## Direkte Verbindung zur Cloud-Projektdatenbank herstellen, um SQL auszuführen

Die folgende Methode verwendet die `magento-cloud` CLI, um eine direkte Verbindung zur MySQL-Datenbank herzustellen und SQL für eine schnellere Abfrage auszuführen. Wenn Sie eine Kopie dieser Datenbank benötigen, verwenden Sie eine der alternativen Methoden zum [Erstellen eines Datenbank-Dump](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud.html).

```bash
magento-cloud db:sql    

Enter a number to choose a project:
  [0] demo-ralbin (ral32nryq4123)
  [1] adobe-commerce-demo (abc123zzkipexnqo)
  [2] DX Tutorials - Commerce (abasrpikfw4123)
 > 2

Enter a number to choose an environment:
Default: master
  [0] master (type: production)
  [1] remote-db (type: development)
 > 1

Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 273454
Server version: 10.6.15-MariaDB-1:10.6.15+maria~deb10-log mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

Sie können beispielsweise alle Datensätze aus der `core_config_data`-Tabelle finden, die das Wort `secure` als Teil der `path` enthalten:

```sql
MariaDB [main]> SELECT * FROM core_config_data WHERE path LIKE '%secure%' \G;
*************************** 1. row ***************************
 config_id: 5
     scope: default
  scope_id: 0
      path: web/unsecure/base_url
     value: http://remote-db-ecpefky-abasrpikfw4123.us-4.magentosite.cloud/
updated_at: 2024-02-02 18:03:17
*************************** 2. row ***************************
 config_id: 6
     scope: default
  scope_id: 0
      path: web/secure/base_url
     value: https://remote-db-ecpefky-abasrpikfw4123.us-4.magentosite.cloud/
updated_at: 2024-02-02 18:03:17
*************************** 3. row ***************************
 config_id: 8
     scope: default
  scope_id: 0
      path: web/secure/use_in_adminhtml
     value: 1
updated_at: 2023-04-26 19:43:58
3 rows in set (0.001 sec)

ERROR: No query specified

MariaDB [main]> 
```

## Zusätzliche Ressourcen

* [Adobe Commerce Cloud-CLI](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli/cloud-cli-overview.html)
* [Einrichten des MySQL-Service](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/mysql.html)
* [Einrichten einer Remote-MySQL-Datenbankverbindung](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/database-server/mysql-remote.html)
* [Erstellen eines Datenbank-Dump auf Adobe Commerce in der Cloud-Infrastruktur](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud.html)
