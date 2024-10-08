---
title: Abfragen mit der Datenbank verbinden und ausführen
description: Erfahren Sie mehr über verschiedene Methoden zum Herstellen einer Verbindung zu einem Adobe Commerce-Cloud-Projekt. Erfahren Sie, wie Sie ein Datenbankmodul abrufen, um es außerhalb der Site zu verwenden. Erfahren Sie mehr über einige Methoden zum Maskieren und Entfernen von personenbezogenen Daten.
feature: Backend Development,Console,Cloud
topic: Commerce,Development
role: Developer
level: Intermediate, Experienced
doc-type: Technical Video
duration: 0
last-substantial-update: 2024-06-25T00:00:00Z
jira: KT-14910
exl-id: e740bbd0-5ec7-4272-89cb-0bed776eb149
source-git-commit: 9af981957b5c8722002a5c1cbd09b71e98e0a754
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 0%

---

# Abfragen mit der Adobe Commerce-Datenbank verbinden und ausführen

Erfahren Sie, wie Sie eine Verbindung zu einer Adobe Commerce in einem Cloud-Projekt herstellen, eine Datenbank-Ablage für die Offsite-Verwendung erstellen und personenbezogene Daten (PII) verarbeiten, indem Sie sie maskieren oder entfernen. Erfahren Sie mehr über den Zugriff auf Adobe Commerce-Daten mit verschiedenen Methoden, darunter lokale DB-Dumps, Remote-DB-Verbindungen mit Anwendungen wie MySQL Workbench oder TablesPlus und Direktverbindungen über das Magento Cloud CLI-Tool.

## Videoinhalt

* Erfahren Sie, wie Sie mit einem Tool wie MysqlWorkbench oder TablesPlus schnell eine Verbindung zu einem Remote-Adobe Commerce Cloud-Projekt herstellen können.
* Erfahren Sie, wie Sie über die Befehlszeile schnell eine Verbindung zum Adobe Commerce-Projekt herstellen und SQL ausführen können.

>[!VIDEO](https://video.tv.adobe.com/v/3430507?learn=on)

Erfahren Sie, wie Sie eine Verbindung zu einer Adobe Commerce in einem Cloud-Projekt herstellen, eine Datenbank für die Verwendung außerhalb der Site ablegen, PII maskieren und entfernen können.

Sie können mit einer der folgenden Methoden auf Adobe Commerce-Daten aus Ihrem Cloud-Projekt zugreifen:

* Verwenden eines lokalen DB-Dump
* Eine DB-Verbindung zu Ihrer Remote-Cloud-Umgebung mit einer Anwendung wie MySQL Workbench oder Tables Plus
* Stellen Sie eine direkte Verbindung zur Cloud-Umgebung her, indem Sie das &quot;magento-cloud&quot;-CLI-Tool verwenden und Befehle auf dem Remote-Server ausführen

Die bevorzugte Methode besteht darin, einen Datenbank-Dump durchzuführen und ihn zu scrubben, um Kundeninformationen zu entfernen. Entfernen Sie die Kundendaten vollständig, wenn die Daten nicht benötigt werden.

## Verwenden des Adobe Commerce Cloud CLI-Tools

Zum Erstellen eines Datenbank-Dump muss die [Adobe Commerce Cloud CLI](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli/cloud-cli-overview.html) installiert sein. Wechseln Sie auf Ihrem lokalen Laptop zu einem Ordner und führen Sie den folgenden Befehl aus. Ersetzen Sie unbedingt `your-project-id` durch die Projekt-ID, die `asasdasd45q` ähnelt. Sie müssen auch `your-environment-name` durch den Namen Ihrer Umgebung ersetzen, z. B. `master` oder `staging`.

`magento-cloud db:dump -p your-project-id -e your-environment-name`

Wenn Sie sich nicht sicher sind, ob die Projekt-ID oder die Umgebung vorliegt, können Sie diese im -Befehl auslassen:

`magento-cloud db:dump`

In der CLI werden Sie aufgefordert, das richtige Projekt und die richtige Umgebung anzugeben. Im folgenden Beispiel wird dieses Dialogfeld angezeigt. Dieses Beispiel zeigt mehrere Projekte, die Ihrem Konto zugewiesen sind, aber wahrscheinlich steht nur ein Projekt zur Verfügung.

Ordnerwechsel

```bash
cd ~/Downloads/db-tutorial 
```

Führen Sie nun den Befehl aus, um den Datenbank-Dump zu erstellen

```bash
magento-cloud db:dump
```

Da wir kein Projekt oder keine Umgebung angegeben haben, stellt die Adobe Commerce-CLI einige Fragen: Hier finden Sie ein Beispiel für einen Dialog

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

## Verwenden der ECE-Tools von Adobe Commerce

Wenn Sie nicht über das CLI-Tool für Adobe Commerce verfügen, können Sie `ssh` in Ihr Projekt eingeben und den Befehl `ece` `vendor/bin/ece-tools db-dump` ausführen:
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

Im folgenden Beispiel wird `rsync` verwendet, um die Datei in den Ordner `~/Downloads/db-tutorial` zu ziehen.

```bash
rsync -avrp -e ssh abasrpikfw4123-remote-db-ecpefky--mymagento@ssh.us-4.magento.cloud:/app/var/dump-main-1707850906.sql.gz ~/Downloads/db-tutorial
```

Das Terminal-Fenster gibt einige Informationen aus, hier einige Beispielausgabe

```bash
rsync -avrp -e ssh abasrpikfw4123-remote-db-ecpefky--mymagento@ssh.us-4.magento.cloud:/app/var/dump-main-1707850906.sql.gz ~/Downloads/db-tutorial
receiving file list ... done
dump-main-1707850906.sql.gz

sent 38 bytes  received 2691041 bytes  358810.53 bytes/sec
total size is 2690241  speedup is 1.00
```

Zeigen Sie den Inhalt der Datei an, um zu überprüfen, ob sie erfolgreich heruntergeladen wurde.

```bash
ls -lah
total 29840
drwxr-xr-x    4 <ussername>  staff   128B Feb 13 13:02 .
drwx------@ 103 <ussername>   staff   3.2K Feb 13 12:52 ..
-rw-r--r--    1 <ussername>   staff    11M Feb 13 12:53 abasrpikfw4123--remote-db-ecpefky--mysql--main--dump.sql
-rw-r--r--    1 <ussername>   staff   2.6M Feb 13 13:01 dump-main-1707850906.sql.gz
```

Nachdem Sie über die Daten verfügen, sollten Sie sie bereinigen, indem Sie die Kundendaten entfernen oder maskieren. Das folgende Beispielskript hilft Ihnen bei den ersten Schritten.

In diesem Beispiel werden Kundendaten in zufällige Zeichenfolgen umgewandelt, aber alle Elemente werden beibehalten. Dieses Beispiel enthält einige zusätzliche Tabellen, die zeigen, dass Kunden-PII in Tabellen von Drittanbietern sowie in Kerntabellen zu finden sind. Prüfen Sie die Daten in jeder Tabelle sorgfältig und maskieren oder entfernen Sie alle Kundendaten.

In der Regel ist der Architekt oder Lead-Entwickler die einzige Person, die für die Maskierung und Bereinigung von Datenbank-Dumps verantwortlich ist. Ein dedizierter Bereiniger senkt die Exposition der Rohdaten, wodurch sich die Möglichkeit verringert, Verstöße gegen Compliance-Regeln und -Vorschriften zu ahnden.

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

Alternativ können Sie die Datensätze löschen, anstatt die Informationen zu maskieren, wodurch auch die neue DB kleiner wird. Sobald PII maskiert oder entfernt wurde, können die Daten für ein Team sicher bereitgestellt werden, damit es sie in seiner Umgebung verwenden kann.

## Remote-DB-Verbindung zu einem Adobe Commerce Cloud-Projekt

Diese Methode ermöglicht das versehentliche Bearbeiten und Löschen von echten Daten. Dieser Ansatz sollte mit Vorsicht angewandt werden. Die Verwendung einer Datenbanksicherung und die Offline-Überprüfung der Daten ist der bevorzugte Ansatz. Es gibt Fälle, in denen ein direkter Zugriff auf die Daten in der Adobe Commerce Cloud erforderlich ist, was jedoch mit Risiken verbunden ist. Es gibt kein &quot;Bist du dir sicher&quot;? Fragen gestellt werden, sodass es möglich ist, Daten versehentlich zu ändern oder zu entfernen.

Super wichtig! Eine Remote-DB-Verbindung ist praktisch und nutzt echte Live-Daten, birgt jedoch Risiken. Ich persönlich und als technischer Hauptarchitekte für Adobe Commerce empfehle es nicht. Es ist zu einfach zu vergessen, dass Sie sich auf der Remote-DB befinden und Daten versehentlich löschen oder ändern. Es gibt eine Option, um eine Verbindung mit der schreibgeschützten Replikation herzustellen, die jedoch je nach der Schwere der SQL-Aktivitäten gewisse Auswirkungen auf die Site hat. Da dies jedoch möglich ist, sind dies die Schritte, um dies zu erreichen.

Errichtung eines SSH-Tunnels:

```bash
magento-cloud tunnel:open
```

Nachdem das Projekt ausgewählt und die Umgebung ausgewählt wurde, wird die Ausgabe aus dem Befehl ausgegeben, der in den Einstellungen für die grafische Oberfläche von mysql verwendet wird.

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

Stellen Sie mithilfe der Befehlsoption `SSH tunnel opened to database at` eine Verbindung mithilfe einer grafischen MySQL-Schnittstelle her.

```bash
SSH tunnel opened to database at: mysql://user:@127.0.0.1:30000/main
```

Nachdem Sie über die richtigen Informationen verfügen, können Sie diese Werte weiterhin in die Cloud Console einfügen.

Sie finden den SSH-Hostnamen und den Benutzernamen aus den Cloud-Anmeldedaten in der Cloud Console.

![logo - Adobe Commerce Cloud Console](./assets/cloud-ui-screenshot.png "Adobe Commerce Cloud Console")

Hier ist ein Beispiel: `ssh abasrpikfw4123-remote-db-ecpefky--mymagento@ssh.us-4.magento.cloud`
Der SSH-Hostname ist alles nach dem @-Zeichen: `ssh.us-4.magento.cloud` in diesem Beispiel.
Der SSH-Benutzername ist alles vor dem @-Zeichen: `abasrpikfw4123-remote-db-ecpefky—mymagento`

## Suchen von Werten für die Verbindung zur Datenbank

Zum direkten Zugriff auf die MariaDB-Datenbank muss SSH verwendet werden, um sich bei der Remote-Cloud-Umgebung anzumelden und eine Verbindung zur Datenbank herzustellen.

1. Verwenden Sie SSH, um sich bei der Remote-Umgebung anzumelden.

   ```bash
   magento-cloud ssh
   ```

1. Rufen Sie die Anmeldedaten für MySQL aus den Eigenschaften `database` und `type` in der Variablen [$MAGENTO_CLOUD_RELATIONSHIPS](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/properties/properties.html?lang=en#relationships) ab.

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

Verwenden Sie dann die Konfigurationswerte in Ihrer MySQL-GUI. Im folgenden Beispiel wird MySQL Workbench verwendet, aber jede App, die MySQL-Verbindungen unterstützt, verfügt über ähnliche Felder.

![logo - MySQL GUI example using MySQL Workbench](./assets/mysql-workbench-after-connecting.png " MySQL GUI example using MySQL Workbench")

![logo - MySQL GUI example using TablesPlus](./assets/tablesPlus-db-connection.png " MySQL GUI example using TablesPlus")

Nach der Einrichtung ist es möglich, eine MySQL-GUI zu verwenden, um Abfragen auf einem Remote-Adobe Commerce Cloud-Projekt auszuführen.

## Direkte Verbindung zur Cloud-Projektdatenbank zur Ausführung von SQL

Die folgende Methode verwendet die &quot;`magento-cloud`&quot;-CLI, um direkt eine Verbindung zur mysql-Datenbank herzustellen und SQL auszuführen, was eine schnellere Datenbankabfrage ermöglicht. Wenn Sie diese Datenbank kopieren müssen, lesen Sie eine der alternativen Methoden, um [einen Datenbank-Dump zu erstellen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud.html).

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

Sie können beispielsweise alle Datensätze aus der Tabelle `core_config_data` finden, die das Wort `secure` als Teil der Spalte `path` enthalten:

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

[Adobe Commerce Cloud CLI](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/dev-tools/cloud-cli/cloud-cli-overview.html)
[MySQL-Dienst einrichten](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/mysql.html)
[Richten Sie eine Remote-MySQL-Datenbankverbindung ein](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/database-server/mysql-remote.html)
[Erstellen eines Datenbank-Dump auf Adobe Commerce in der Cloud-Infrastruktur](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud.html)
