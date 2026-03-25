---
title: Checkliste vor der Markteinführung von Adobe Commerce Cloud
description: Erfahren Sie mehr über die Checkliste vor der Markteinführung von Adobe Commerce Cloud und wie Sie sie mit Ihrem Integrator vor der Live-Schaltung abarbeiten können.
feature: Cloud
topic: Commerce, Architecture, Development
role: Admin, Developer, User
level: Intermediate
doc-type: Tutorial
duration: 451
last-substantial-update: 2024-04-17T00:00:00Z
jira: KT-15180
exl-id: c6adb2c2-f194-4a3d-9290-e0837ef062ae
source-git-commit: 8266ad03ec3bd9364bb9093c8876a4dc1507e1a2
workflow-type: tm+mt
source-wordcount: '1674'
ht-degree: 0%

---


# Checkliste vor dem Start

Auf dieser Seite finden Sie eine Zusammenfassung der Adobe Commerce [Site Launch-Dokumentation](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/launch/overview){target="_blank"}.

Diese Checkliste soll Sie bei der Planung und Ausführung eines erfolgreichen Starts der Adobe Commerce Cloud-Site unterstützen. Arbeiten Sie mit Ihrem Systemintegrator für Adobe Commerce Cloud zusammen, um sicherzustellen, dass alle Konfigurationsaufgaben und Checklisten-Elemente abgeschlossen und überprüft wurden. Wenn Sie Probleme mit Checklisten-Elementen haben oder Fragen haben, wenden Sie sich bitte an den zuständigen technischen Kundenberater oder Customer Success Engineer. Wenn Ihrem -Konto kein CTA/CSE zugewiesen ist, können Sie ein Support-Ticket erstellen, um Unterstützung zu erhalten.

Wenn Ihnen ein CTA/CSE zugewiesen wurde, wenden Sie sich mindestens 4 Wochen vor dem Start der neuen Adobe Commerce Cloud-Site an diesen und den Account Manager, um ihn über Ihre **Absicht** zu informieren.

* Einige Prüfungen werden mit [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"} hervorgehoben, da sie möglicherweise Ihre Live-Schaltung blockieren, wenn sie nicht sorgfältig überprüft wird.
* Arbeiten Sie mit Ihrem Entwickler oder Systemintegrationspartner zusammen, damit Ihr Implementierungsansatz aufeinander abgestimmt bleibt.

>[!IMPORTANT]
> Sie übernehmen [Verantwortung](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility){target="_blank"} für alle nachteiligen Auswirkungen und damit verbundenen Risiken für den Produktions-Launch-Zeitplan und die fortlaufende Site-Stabilität, wenn Sie diese Checkliste nicht verwenden und ausfüllen.

## &#x200B;1. Live-Schaltung

1. Lesen Sie die Dokumentation zum Testen und zur Live[Schaltung (Dokumentation zum Site-Launch](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/launch/overview){target="_blank"}

   >[!NOTE]
   >Stellen Sie sicher, dass mit Ihrem Partner oder Systemintegrator ein umfassender _-&quot;_-Plan“ vollständig vorbereitet ist, der alle erforderlichen Aktionselemente enthält. Denken Sie daran, dass die Checkliste vor der Markteinführung zwar den Schwerpunkt auf die Best Practices von Adobe legt _&#x200B;**jedoch**&#x200B;_ ersetzt (nicht), dass Sie einen eigenen Plan für die Live-Schaltung benötigen.

2. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"} Lesen Sie die Empfehlungen und Informationen zu Support Insights (SWAT[&#x200B; (Benutzerhandbuch](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/intro){target="_blank"})
3. Bestätigen, dass Endbenutzer und Händler UAT (User Acceptance Testing) abgeschlossen haben, einschließlich Backend-Vorgänge.
4. Bestätigen Sie, dass das Systemintegrator-Team End-to-End-UAT für Staging und Produktion durchgeführt hat. Weitere Informationen finden Sie in der Dokumentation zu [Experience League](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/test/staging-and-production){target="_blank"}.
5. Bestätigen der Bereitstellung und des Testens von Code in Staging- und Produktionsumgebungen ([mehr dazu](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/test/staging-and-production){target="_blank"})
6. Vergewissern Sie sich, dass der Produktions-Cluster dauerhaft auf die vertraglich festgelegte tägliche Grundlinie vergrößert wurde. Wenden Sie sich an den zugewiesenen CTA/CSE, um weitere Informationen zu erhalten, oder erstellen Sie ein Support-Ticket.

## &#x200B;2. Aktuelle Konfigurationen

1. Aktualisieren von Adobe Commerce und zugehörigen Paketen/Services auf die [neueste Version](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview){target="_blank"}
2. Überprüfen Sie die aktuellen Konfigurationen und Services mit Ihrem SI/Partner und [&#x200B; Sie die Best Practices](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/catalog-management){target="_blank"}.
3. Überprüfen Sie MySQL/Shared-Files [Festplattenauslastung](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/storage/manage-disk-space){target="_blank"}

## &#x200B;3. Fastly-Konfigurationen

1. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"} Stellen Sie sicher, dass die Zwischenspeicherung funktioniert ([Vollseitencache](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management){target="_blank"} oder [GraphQL-](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/){target="_blank"}). Lesen Sie das [Handbuch zur schnellen Einrichtung](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/cdn/fastly){target="_blank"}.
2. Verwenden Sie gegebenenfalls die GET-Methode für GraphQL-Abfragen auf PWA-/Headless-Websites.

   >[!NOTE]
   > Nur die mit einem HTTP-GET-Vorgang gesendeten Abfragen können zwischengespeichert werden (falls zutreffend). [POST-Abfragen können nicht zwischengespeichert &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/){target="_blank"}.

3. Stellen Sie sicher, dass Fastly Image Optimization aktiviert ist [siehe Fastly Image Optimization](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/cdn/fastly-image-optimization){target="_blank"})
4. Stellen Sie sicher, dass der richtige Shield-Speicherort konfiguriert ist ([Konfigurieren des Cache, der Backends und der Ursprungsabschirmung](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration){target="_blank"}).
5. Bestätigen Sie, dass die Web Application Firewall (**WAF**) funktioniert. (Siehe [Fehlerbehebung bei blockierten &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/cdn/fastly-waf-service){target="_blank"}, falls vorhanden, und Einschränkungen.)
6. Aktualisieren Sie die Liste „Ignorierte URL[Parameter“ von Fastly &#x200B;](https://github.com/iancassidyweb/magento2/commit/68fdecfcd26c957382b8d68b64887e0a83298524){target="_blank"} im Admin-Bedienfeld, um die Cache-Leistung zu verbessern.

   >[!NOTE]
   > In der Fastly-Konfiguration unter _Admin > Stores > Konfigurationen > System > Vollständiger Seiten-Cache > Fastly-Konfiguration > Erweiterte Konfiguration > Ignorierte URL-Parameter (global)_ finden Sie eine kommagetrennte Liste von Parametern, die Fastly bei der Suche nach zwischengespeicherten Seiten ignorieren sollte. Laden Sie die VCL erneut hoch, nachdem Sie diese Liste geändert haben.

## &#x200B;4. DNS und SSL

1. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"} Bestätigen Sie, dass alle erforderlichen Domain-Namen angefordert werden. _(Senden Sie im Voraus ein Support-Ticket für hinzugefügte oder geänderte Domains.)_
2. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"} SSL-Zertifikat (TLS) wurde auf die Domain(s) angewendet. Lesen Sie [diesen Artikel](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/ssl-tls-certificates-for-magento-commerce-cloud-faq){target="_blank"}, um weitere Informationen zu erhalten.
3. Aktualisieren Sie den DNS[TTL-Wert (Time to Live](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/launch/checklist){target="_blank"} auf das Minimum für die Live-Schaltung.
4. Aktivieren von SendGrid SPF und DKIM.

   >[!NOTE]
   > Fügen Sie die SendGrid-CNAME-Einträge für jede Domain zur DNS-Konfiguration hinzu. Lesen Sie [SendGrid-E-Mail](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/sendgrid){target="_blank"}Service, um zu sehen, wie Sie die Absender-Domains ändern können, und vieles mehr.

## &#x200B;5. Datenbankkonfigurationen

Adobe Commerce Cloud verwendet einen MariaDB Galera-Cluster als Datenbank für die Staging- und die Produktionsumgebung. Galera-Cluster sind entscheidend für die Verbesserung der Leistung und Skalierbarkeit. Informationen zu optimalen Verfahren und Einschränkungen für Galera-Cluster-Replikationen finden Sie in den folgenden Artikeln.

* [Best Practices für MySQL-Konfigurationen](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration){target="_blank"}
* Verwaltete Warnhinweise in Adobe Commerce: [MariaDB-Warnhinweise](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/managed-alerts-for-adobe-commerce/managed-alerts-on-magento-commerce-mariadb-alerts){target="_blank"}
* Best Practices für [Datenbankkonfiguration](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud){target="_blank"}
* [Galera-Clusterreplikation und Flusskontrolle](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/backend-development/galera-db-slow-replication){target="_blank"} (tiefer gehende Analyse)

1. [MySQL-Slave-Verbindung](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration#slave-connections){target="_blank"} wird empfohlen, um die Leistung bei hohen Datenbanklasten zu verbessern.
2. Stellen Sie sicher, dass das Zeilenformat für alle Datenbanktabellen auf &quot;[&quot; anstelle von „COMPACT“ &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/maintenance/mariadb-upgrade#convert-database-table-storage-format){target="_blank"} ist (dies gilt insbesondere für On-Premise- zu Cloud-Migrationen).
3. Ändern Sie die Datenbank-Speicher-Engine von [MyISAM zu InnoDB](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud#convert-all-myisam-tables-to-innodb){target="_blank"} für alle Tabellen.
4. Überprüfen und optimieren Sie Datenbanktabellen mit einer Größe von mehr als 1 GB rechtzeitig im Voraus.
5. Die Informationen zum Datenbankschema sind aktuell und aktuell. (Siehe [dieses Handbuch](https://mariadb.com/docs/server/ha-and-performance/optimization-and-tuning/query-optimizations/statistics-for-optimizing-queries/engine-independent-table-statistics#collecting-statistics-with-the-analyze-table-statement){target="_blank"}).

## &#x200B;6. Bereitstellungen

1. Überprüfen Sie den idealen Status der statischen Inhaltsbereitstellung (SCD), um die Wartungszeit während Bereitstellungen in der Produktionsumgebung zu reduzieren. Lesen Sie [SCD-Strategien (Static Content Deployment](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/deploy/static-content){target="_blank"} und [Store-](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/store-settings){target="_blank"}).
2. Überprüfen Sie die Minimierungseinstellungen für HTML, JavaScript und CSS. (Dies gilt nicht für PWA-/Headless-Websites).
3. Vergewissern Sie sich, dass die Verwendung der folgenden Cloud-Variablen ihren Verwendungszwecken entspricht. ([SCD_MATRIX](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/env/stage/variables-build#scd_matrix){target="_blank"}, [SCD_ON_DEMAND](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/env/stage/variables-global#scd_on_demand){target="_blank"} und [SKIP_SCD](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/env/stage/variables-deploy#skip_scd){target="_blank"})

## &#x200B;7. Tests und Fehlerbehebung

1. Testen Sie die ausgehenden Transaktions-E-Mails. Lesen Sie mehr über [Adobe Commerce Cloud - SendGrid-E-Mail-Funktion](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/sendgrid){target="_blank"}.
2. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"} Vergewissern Sie sich, dass keine Adobe-bezogenen Blocker zum Starten vorhanden sind.
3. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"} Führen Sie vor der Live-Schaltung Belastungs- und Belastungstests auf der Produktionsinstanz durch und teilen Sie die Ergebnisse mit dem zugewiesenen CTA/CSE.

   >[!NOTE]
   > Ein [Belastungs- und Belastungstest dient dem Zweck](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/test/guidance#:~:text=A%20load%20test%20can%20help,Scan%20Tool%20for%20your%20sites.){target="_blank"} Engpässe zu identifizieren und Leistungsprobleme innerhalb der Anwendung aufzudecken. Sie spielt eine entscheidende Rolle bei der Verwaltung der Erwartungen hinsichtlich der Cluster-Größe und der Bestimmung der erforderlichen Skalierungsanpassungen, um die Geschäftsanforderungen effektiv zu erfüllen.

   >[!IMPORTANT]
   > **_WARNING:_** Senden Sie beim Vorbereiten eines Auslastungstests **keine** Live-Transaktions-E-Mails (auch an Platzhalteradressen). Das Senden von E-Mails während des Tests kann dazu führen, dass das Projekt vor dem Start das für SendGrid konfigurierte Standard-Versandlimit (12 KB) erreicht.
   > 
   > * Deaktivieren der E-Mail-Kommunikation:
   >   Navigieren Sie _Store > Konfiguration > Erweitert > System > E-Mail-Sendeeinstellungen_.

4. Führen Sie Sicherheitstests auf der Produktionsinstanz im Rahmen des Sicherheitsmodells [gemeinsame Verantwortung“ &#x200B;](https://business.adobe.com/products/commerce.html){target="_blank"}. Für die Einhaltung der PCI-Richtlinien (Payment Card Industry) erfordert die angepasste Site Penetrationstests.

## &#x200B;8. Andere Konfigurationen

1. Wechseln Sie für die Indizierung auf _Aktualisierung planmäßig_, mit Ausnahme des **_customer_grid_**, das auf „SAVE“ bleibt (siehe [Indizierungsmodi](https://developer.adobe.com/commerce/php/development/components/indexing/#indexing-modes){target="_blank"}).
2. Dokumentieren Sie alle verwendeten Suchmaschinen oder Erweiterungen von Drittanbietern.
3. Überprüfen Sie, ob [SEO-Konfigurationen (Suchmaschinenoptimierung) ordnungsgemäß eingerichtet sind](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/seo-overview){target="_blank"} damit Indexer/Crawler die Website ggf. scannen können.
4. Hinzufügen von Weiterleitungen und Routen (siehe [Konfigurieren von Routen](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/routes/routes-yaml){target="_blank"})

   >[!NOTE]
   > Fügen Sie in der Integrationsumgebung Umleitungen und Routen zur Datei „routes.yaml“ hinzu und überprüfen Sie die Konfiguration in dieser Umgebung, bevor Sie sie in der Staging- und Produktionsumgebung bereitstellen.

   Beispiel `routes.yaml` Fragment:

   ```yaml
           "http://{all}/":
               type: upstream
               upstream: "mymagento:http"
   
           "http://{all}/":
               type: upstream
               upstream: "mymagento:http"
   ```

5. Stellen Sie sicher, dass Xdebug deaktiviert ist, wenn es während der Entwicklung aktiviert wurde (siehe [Konfigurieren von Xdebug für Commerce in Cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/test/debug){target="_blank"}).
6. Überprüfen Sie, ob OPcache und andere Konfigurationen in der Datei php.ini korrekt aktualisiert wurden ([siehe Beispiel](https://github.com/magento/magento-cloud/blob/master/php.ini#L41){target="_blank"}).
7. Abonnieren Sie die [**Adobe Commerce-Statusseite**](https://status.adobe.com/cloud/experience_cloud#/){target="_blank"}.
8. Abonnieren Sie die New Relic[Benachrichtigungskanäle „Verwaltete Warnhinweise für Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce){target="_blank"}, um die angegebenen Leistungsmetriken zu überwachen ([mehr dazu](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/monitor/new-relic/new-relic-service){target="_blank"}).

## &#x200B;9. Sicherheit

1. Richten Sie die Adobe Commerce-Sicherheitsprüfung ein.

   >[!NOTE]
   > [Die Adobe Commerce-Sicherheitsprüfung ist ein hilfreiches Tool](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-scan){target="_blank"} mit dem Sie veraltete Softwareversionen, fehlerhafte Konfigurationen und potenzielle Malware auf der Website entdecken können. Melden Sie sich an, planen Sie die Ausführung häufig und stellen Sie sicher, dass E-Mails an den richtigen technischen Sicherheitskontakt gesendet werden.
   > 
   > Führen Sie diese Aufgabe während der UAT aus. Wenn Sie die Option „Periodische Scans“ verwenden, sollten Sie die Scans zu Zeiten geringer Auslastung planen. Öffnen Sie nach der Anmeldung bei Ihrem Adobe Commerce-Konto das Sicherheits-Scan-Tool von Ihrem Konto aus (siehe [Sicherheitsprüfung](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-scan){target="_blank"} für Zugriff und Verwendung).

2. Ändern Sie die Standardeinstellungen für den Adobe Commerce Admin.
3. Ändern Sie das Administratorkennwort (siehe [Konfigurieren der Admin-Sicherheit](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-admin){target="_blank"}).
4. Admin-URL ändern (siehe [Verwenden einer benutzerdefinierten Admin-URL](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#use-a-custom-admin-url){target="_blank"}).
5. Entfernen Sie alle Benutzer, die nicht mehr im Projekt vorhanden sind (siehe [Erstellen und Verwalten von Benutzern](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access){target="_blank"}).
6. Bestätigen Sie, dass die Administratorkennwörter den Anforderungen entsprechen (siehe [Administratorkennwörter](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-admin){target="_blank"}).
7. Konfigurieren Sie die Zwei-Faktor-Authentifizierung (siehe [Zwei-Faktor-Authentifizierung (Admin)](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-admin#two-factor-authentication){target="_blank"}.

## &#x200B;10. Live-Schaltung

Wenn die Umstellung abgeschlossen ist, führen Sie die folgenden Schritte aus (weitere Informationen finden Sie unter [DNS-Konfigurationen](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/launch/checklist){target="_blank"}):

1. Greifen Sie auf Ihren DNS-Service zu und aktualisieren Sie A- und CNAME-Einträge für jede Ihrer Domains und Hostnamen:
   1. Fügen Sie einen CNAME-Eintrag für _&lt;&lt;www.yourdomain.com>>_ hinzu, der auf **prod.magentocloud.map.fastly.net** verweist.
   2. Legen Sie vier A-Einträge für _&lt;meinedomäne.com“_ fest, die auf Folgendes verweisen:\
      151.101.1.124\
      151.101.65.124\
      151.101.129.124\
      151.101.193.124
2. Ändern Sie die Adobe Commerce-Basis-URL in _&lt;&lt;www.yourdomain.com>>_
3. Warten Sie, bis die TTL-Zeit verstrichen ist, und starten Sie dann den Webbrowser neu.
4. Testen Sie die Website.

### Wenn Sie ein Problem bei der Blockierung der Live-Schaltung haben:

Wenn während der Umstellung Probleme auftreten, die Sie daran hindern, den Service zu starten, verwenden Sie am schnellsten den Helpdesk und öffnen Sie ein Ticket mit dem Grund „Mein Geschäft kann nicht gestartet werden“ und rufen Sie eine Hotline-Support-Nummer an (aktuelle Nummern und Verfahren finden Sie unter [Adobe Commerce P1](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-p1-notification-hotline){target="_blank"}Benachrichtigungs-Hotline):

* Gebührenfrei in den USA: (+1) 877 282 7436 (direkt über die Adobe Commerce P1-Hotline)
* Gebührenfrei in den USA: (+1) 800 685 3620 (Beim ersten Menü drücken Sie 7 für die Adobe Commerce P1-Hotline)
* US Local: (+1) 408 537 8777

## &#x200B;11. Nach der Live-Schaltung

Sobald die Site live ist, senden Sie eine E-Mail an die zugewiesene CTA (technischer Kundenberater), CSE (Customer Success Engineer) und AM (Account Manager). Wenn Sie jedoch keinen Account Manager für das Projekt zugewiesen haben, können Sie ein Support-Ticket erstellen, in dem Sie darum bitten, die Überwachung mit hoher SLA zu aktivieren, sobald die Site live gegangen ist. Der CTA/CSE führt die folgenden Aufgaben aus, sobald die Website für den Start mit Fastly-Aktivierung und Caching verifiziert wurde:

* Markieren Sie den Cluster als live und erstellen Sie ein Support-Ticket, um die Überwachung mit hohen SLA-Werten (Service Level Agreements) zu aktivieren.
* Aktivieren Sie New Relic Synthetics für die Überwachung der Betriebszeit.

>[!MORELIKETHIS]
> 
> * [Übersicht über die Launch-Bereitschaft - Implementierungs-Playbook](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/launch/overview){target="_blank"}
> * [Launch-Checkliste - Benutzerhandbuch](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/launch/checklist){target="_blank"}
> * [Checkliste vor dem Start - Site-Manager/Commerce-Administratorhandbuch](https://experienceleague.adobe.com/en/docs/commerce-admin/start/setup/prelaunch-checklist){target="_blank"}
> * [Sicherheitsmodell mit gemeinsamer Verantwortung](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility){target="_blank"}
