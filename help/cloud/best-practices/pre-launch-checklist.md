---
title: Checkliste für Adobe Commerce Cloud vor dem Start
description: Erfahren Sie mehr über die Checkliste für die Adobe Commerce Cloud-Vorab-Einführung.
feature: Cloud
topic: Commerce, Architecture, Development
role: Architect, Developer
level: Intermediate
doc-type: Tutorial
duration: 0
last-substantial-update: 2024-04-17T00:00:00Z
jira: KT-15180
kt: 15180
exl-id: c6adb2c2-f194-4a3d-9290-e0837ef062ae
source-git-commit: 191cfb29de7b4fff5ca73dcd1603b51d852aebd1
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 0%

---

# Commerce Cloud Pre-Launch-Checkliste

Im Folgenden finden Sie eine Zusammenfassung der Adobe Commerce [Dokumentation zum Website-Start](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/overview){target="_blank"}.

Diese Checkliste soll bei der Planung und Ausführung eines erfolgreichen Starts der Adobe Commerce Cloud-Website helfen. Arbeiten Sie mit Ihrem Systemintegrator für Adobe Commerce Cloud zusammen, um sicherzustellen, dass alle Konfigurationsaufgaben und Checklisten-Elemente abgeschlossen und überprüft werden. Sollten Sie Schwierigkeiten mit der Checkliste haben oder Fragen haben, wenden Sie sich an den zuständigen technischen Kundenberater oder Customer Success Engineer. Wenn Ihrem Konto kein CTA/CSE zugewiesen wurde, können Sie ein Support-Ticket erstellen.

Wenn Sie dem Konto eine CTA/CSE zugewiesen haben, wenden Sie sich mindestens 4 Wochen vor dem Start der neuen Adobe Commerce Cloud-Site an diese und an den Kundenbetreuer, um sie über Ihre **Absicht** zum Start zu informieren.

- Einige Prüfungen werden mit [!BADGE Blocker] markiert{type=caution tooltip="Potenzieller Blocker"}
- Stellen Sie sicher, dass Sie mit Ihrem Entwickler- oder Systemintegrationspartner zusammenarbeiten, um Ihren Implementierungsansatz zu koordinieren.

>[!IMPORTANT]
> Sie übernehmen [Verantwortung](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility){target="_blank"} für alle schädlichen Auswirkungen und damit verbundenen Risiken für den Produktionsstartplan und die kontinuierliche Site-Stabilität, wenn Sie diese Checkliste nicht verwenden und abschließen.

## 1. Pre-Go Live

1. Lesen Sie die Dokumentation zum Testen und Live-Schaltung [Dokumentation zum Site-Launch](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/overview){target="_blank"}

   >[!NOTE]
   >Stellen Sie sicher, dass ein umfassender _&quot;Live-Bereitschaft-Plan&quot;_ mit Ihrem Partner oder Systemintegrator vollständig vorbereitet ist und alle erforderlichen Aktionselemente enthält. Beachten Sie, dass die Checkliste zwar die Best Practices vor dem Start betont, aber _**nicht**_ die Notwendigkeit Ihres eigenen Go-Live-Bereitstellungsplans ersetzt.

2. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"}[Benutzerhandbuch](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/intro){target="_blank"})
3. Endbenutzer/Händler führten UAT (User Acceptance Testing) durch, einschließlich Backend-Operationen.
4. Das Systemintegratorteam hat durchgängige UAT für Staging und Produktion durchgeführt. Weitere Informationen finden Sie in der [Experience League-Dokumentation](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production){target="_blank"}.
5. Bestätigen Sie die Codebereitstellung und -tests in Staging- und Produktionsumgebungen ([mehr dazu](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production){target="_blank"}).
6. Die Größe des Produktionsclusters wurde dauerhaft auf die vertraglich vereinbarte tägliche Grundlinie erhöht. Wenden Sie sich an den zugewiesenen CTA/CSE, um weitere Informationen zu erhalten, oder heben Sie ein Support-Ticket auf.

## 2. Aktuelle Konfigurationen

1. Aktualisieren Sie Adobe Commerce und die zugehörigen Pakete/Dienste auf die [neueste Version](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview){target="_blank"}
2. Überprüfen Sie die aktuellen Konfigurationen und Dienste mit Ihrem SI/Partner und befolgen Sie [die Best Practices](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/catalog-management){target="_blank"}.
3. Überprüfen Sie die Verwendung von MySQL/Shared-Files [Disk Usage](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space){target="_blank"}

## 3. Schnelle Konfigurationen

1. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"}[Vollseitencache](https://developer.adobe.com/commerce/frontend-core/guide/caching/){target="_blank"} oder [GraphQL-Caching](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/){target="_blank"}). Lesen Sie den Leitfaden [ Schnell einrichten](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly){target="_blank"}.
2. Verwenden Sie gegebenenfalls die GET-Methode für GraphQL-Abfragen auf PWA/Headless-Websites.

   >[!NOTE]
   > Nur Abfragen, die mit einem HTTP-GET-Vorgang gesendet wurden, können zwischengespeichert werden (falls zutreffend). [POST-Abfragen können nicht zwischengespeichert werden](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/){target="_blank"}.

3. Stellen Sie sicher, dass die Fastly-Bildoptimierung aktiviert ist ([Siehe Fastly Image Optimization](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly-image-optimization){target="_blank"}).
4. Stellen Sie sicher, dass der richtige Schildspeicherort konfiguriert ist ([Cache-, Backends- und Ursprungsabschirmung konfigurieren](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration){target="_blank"}).
5. Die Webanwendungs-Firewall (**WAF**) funktioniert. (Siehe [Fehlerbehebung bei blockierten Anfragen](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly-waf-service){target="_blank"}, falls vorhanden und Einschränkungen).
6. Aktualisieren Sie die Liste Fastly [&quot;Ignorierte URL-Parameter&quot;](https://github.com/iancassidyweb/magento2/commit/68fdecfcd26c957382b8d68b64887e0a83298524){target="_blank"} im Admin-Bereich, um die Cache-Leistung zu verbessern.

   >[!NOTE]
   > In der Schnellkonfiguration unter &quot;_Admin > Stores > Konfigurationen > System > Vollständiger Seiten-Cache > Schnelle Konfiguration > Erweiterte Konfiguration > Ignorierte URL-Parameter (Global)&quot;_ finden Sie eine kommagetrennte Liste von Parametern, die bei der Suche nach zwischengespeicherten Seiten schnell außer Acht gelassen werden sollten. Stellen Sie sicher, dass Sie den VCL erneut hochladen, nachdem Sie diese Liste geändert haben.

## 4. DNS und SSL

1. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"}_(Senden Sie ein Support-Ticket im Voraus für hinzugefügte oder geänderte Domänen)_
2. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"}[dieser Artikel](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/ssl-tls-certificates-for-magento-commerce-cloud-faq){target="_blank"} für weitere Informationen.
3. Aktualisieren Sie den DNS [TTL (Time to Live)](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist#to-update-dns-configuration-for-site-launch){target="_blank"} -Wert auf das Minimum, das für die Live-Schaltung verfügbar ist.
4. Aktivieren von Sendgrid SPF und DKIM

   >[!NOTE]
   > Fügen Sie der DNS-Konfiguration die SendGrid-CNAME-Einträge für jede Domäne hinzu. Lesen Sie [SendGrid email service](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/sendgrid){target="_blank"} , um zu erfahren, wie Sie die Absenderdomänen ändern und mehr.

## 5. Datenbankkonfigurationen

Adobe Commerce Cloud verwendet einen MariaDB Galera-Cluster als Datenbank für die Staging- und Produktionsumgebung. Galera-Cluster sind maßgeblich für die Verbesserung der Leistung und Skalierbarkeit. In den folgenden Artikeln erhalten Sie Einblicke in die optimalen Vorgehensweisen und Einschränkungen von Galera-Cluster-Replikationen.

- [Best Practices für MySQL-Konfigurationen](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration){target="_blank"}
- Verwaltete Warnhinweise in Adobe Commerce: [MariaDB-Warnhinweise](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-mariadb-alerts){target="_blank"}
- Best Practices für die [Datenbankkonfiguration](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud){target="_blank"}
- Tiefe Analyse für [Galera-Cluster-Replikationen und Flusssteuerung.](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/backend-development/galera-db-slow-replication){target="_blank"}

1. [MYSQL Slave-Verbindung](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration#slave-connections){target="_blank"} wird empfohlen, um die Leistung bei hohem Laden der Datenbank zu verbessern.
2. Stellen Sie sicher, dass das Zeilenformat für alle Datenbanktabellen auf &quot;[DYNAMIC&quot;anstelle von &quot;COMPACT](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/maintenance/mariadb-upgrade#convert-database-table-storage-format){target="_blank"}&quot;festgelegt ist (dies gilt insbesondere für On-Premise- zu Cloud-Migrationen).
3. Ändern Sie die Datenbank-Speicher-Engine für alle Tabellen von [MyISAM in InnoDB](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud#convert-all-myisam-tables-to-innodb){target="_blank"} .
4. Überprüfen und optimieren Sie Datenbanktabellen mit einer Größe von mehr als 1 GB im Voraus.
5. Die Datenbankschemadaten sind aktuell und aktuell. (Siehe [dieses Handbuch](https://mariadb.com/kb/en/engine-independent-table-statistics/#collecting-statistics-with-the-analyze-table-statement){target="_blank"}).

## 6. Dienstbezüge

1. Überprüfen Sie den idealen Status der statischen Inhaltsbereitstellung (SCD), um die Wartungszeit während Bereitstellungen in der Produktionsumgebung zu reduzieren. Lesen Sie die Anleitung zur Bereitstellung statischer Inhalte (SCD) ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/static-content){target="_blank"} und zur Verwaltung der Speicherkonfiguration [4}{target="_blank"}.[](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/store-settings)
2. Überprüfen Sie die Minimierungseinstellungen für HTML, JavaScript und CSS. (Dies gilt nicht für PWA/Headless-Websites).
3. Vergewissern Sie sich, dass die Verwendung der folgenden Cloud-Variablen mit den beabsichtigten Zwecken übereinstimmt. ([SCD_MATRIX](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-build#scd_matrix){target="_blank"}, [SCD_ON_DEMAND](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global#scd_on_demand){target="_blank"} und [SKIP_SCD](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy#skip_scd){target="_blank"})

## 7. Tests und Fehlerbehebung

1. Testen Sie die ausgehenden Transaktions-E-Mails. Weitere Informationen zur Funktion [Adobe Commerce Cloud - SendGrid Mail](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/sendgrid){target="_blank"}.
2. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"}
3. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"}

   >[!NOTE]
   > Ein [Last- und Belastungstest dient dem Zweck](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/guidance#:~:text=A%20load%20test%20can%20help,Scan%20Tool%20for%20your%20sites.){target="_blank"}, Engpässe zu identifizieren und Leistungsprobleme innerhalb der Anwendung zu ermitteln. Es spielt eine entscheidende Rolle bei der Verwaltung der Erwartungen in Bezug auf die Clustergröße und bei der Festlegung der erforderlichen Skalierungsanpassungen, um die geschäftlichen Anforderungen effektiv zu erfüllen.

   >[!IMPORTANT]
   > **_WARNUNG:_** Bitte senden Sie bei der Vorbereitung eines Belastungstests **_keine Live-Transaktions-E-Mails (auch nicht an Platzhalter-Adressen)._** Das Senden von E-Mails während des Tests kann dazu führen, dass das Projekt vor dem Start das für SendGrid konfigurierte standardmäßige Versandlimit (12k) erreicht.
   > 
   > - Deaktivieren der E-Mail-Kommunikation:
   >   Navigieren Sie zu _Store > Konfiguration > Erweitert > System > E-Mail-Versandeinstellungen_.

4. Führen Sie im Rahmen des Sicherheitsmodells [Geteilte Verantwortung](https://business.adobe.com/products/magento/secure-ecommerce.html){target="_blank"} Sicherheitstests auf der Produktionsinstanz durch. Für die PCI-Compliance (Payment Card Industry) erfordert die angepasste Website Penetrationstests.

## 8. Sonstige Konfigurationen

1. Wechseln Sie zur Indizierung zu _&quot;Update nach Zeitplan_&quot;, mit Ausnahme von **_customer_grid_** , das auf &quot;SAVE&quot;verbleibt (siehe [Indizierungsmodi](https://developer.adobe.com/commerce/php/development/components/indexing/#indexing-modes){target="_blank"}).
2. Verwenden Sie Suchmaschinen oder -erweiterungen von Drittanbietern?
3. Vergewissern Sie sich, dass die Konfigurationen für [SEO (Suchmaschinenoptimierung) ordnungsgemäß eingerichtet sind](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/seo-overview){target="_blank"}, damit Indexer/Crawler die Website gegebenenfalls scannen können.
4. Hinzufügen von Umleitungen und Routen (siehe [Routen konfigurieren](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/routes/routes-yaml){target="_blank"})

   >[!NOTE]
   >Fügen Sie Weiterleitungen und Routen zur Datei routes.yaml in der Integrationsumgebung hinzu und überprüfen Sie die Konfiguration in dieser Umgebung, bevor Sie sie in Staging und Produktion bereitstellen.

       &quot;http://{all}/&quot;:
       type: Upstream
       Upstream: &quot;mymagento:http&quot;
       
       &quot;http://{all}/&quot;:
       type: Upstream
       Upstream: &quot;mymagento:http&quot;
   
5. Stellen Sie sicher, dass XDebug deaktiviert ist, wenn es während der Entwicklung aktiviert ist (siehe [Xdebug konfigurieren](https://developer.adobe.com/commerce/cloud-tools/docker/test/configure-xdebug/){target="_blank"}).
6. Überprüfen Sie, ob der op-Cache und andere Konfigurationen in der php.ini-Datei korrekt aktualisiert wurden ([siehe dieses Beispiel](https://github.com/magento/magento-cloud/blob/master/php.ini#L41){target="_blank"}).
7. Abonnieren Sie die [**Adobe Commerce-Statusseite**](https://status.adobe.com/cloud/experience_cloud#/){target="_blank"}.
8. Abonnieren Sie die New Relic-Benachrichtigungskanäle &quot;[Verwaltete Warnhinweise für Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce){target="_blank"}&quot;, um die jeweiligen Leistungsmetriken zu überwachen ([lesen Sie mehr](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/monitor/new-relic/new-relic-service){target="_blank"}).

## 9. Sicherheit

1. Einrichten des Adobe Commerce-Sicherheitsscan

   >[!NOTE]
   > [Adobe Commerce Security Scan ist ein nützliches Tool](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-scan){target="_blank"}, mit dem Sie veraltete Softwareversionen, falsche Konfigurationen und potenzielle Malware auf der Site erkennen können. Melden Sie sich an, planen Sie die Ausführung oft und stellen Sie sicher, dass E-Mails an den richtigen technischen Sicherheitskontakt gesendet werden.
   > 
   > Führen Sie diese Aufgabe während der UAT aus. Wenn Sie die Option Periodische Scans verwenden, stellen Sie sicher, dass Sie Scans zu Zeiten geringer Nachfrage planen. Weitere Informationen finden Sie auf der Seite [Sicherheitsscan](https://account.magento.com/scanner/index/dashboard/){target="_blank"} im Adobe Commerce-Konto. Sie müssen sich bei einem Adobe Commerce-Konto anmelden, um auf die Sicherheitsprüfung zugreifen zu können.

2. Ändern Sie die Standardeinstellungen für den Adobe Commerce-Administrator.
3. Ändern Sie das Administratorkennwort (siehe [Konfigurieren von Admin Security](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-admin){target="_blank"}).
4. Ändern Sie die Admin-URL (siehe [Verwenden einer benutzerdefinierten Admin-URL](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#use-a-custom-admin-url){target="_blank"}).
5. Entfernen Sie alle Benutzer, die nicht mehr im Projekt enthalten sind (siehe [Benutzer erstellen und verwalten](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/user-access){target="_blank"}).
6. Passwörter für Administratoren sind konfiguriert (siehe [Anforderungen an das Admin-Passwort](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-admin){target="_blank"}).
7. Konfigurieren Sie die Authentifizierung mit zwei Faktoren (siehe [Zweifaktorauthentifizierung](https://developer.adobe.com/commerce/testing/functional-testing-framework/two-factor-authentication/){target="_blank"}).

## 10. Live-Schaltung

Wenn es Zeit ist, den Code zu überarbeiten, führen Sie die folgenden Schritte aus (weitere Informationen finden Sie unter [DNS-Konfigurationen](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist){target="_blank"}):

1. Greifen Sie auf Ihren DNS-Dienst zu und aktualisieren Sie A- und CNAME-Einträge für jede Ihrer Domänen und Hostnamen:
   1. Fügen Sie einen CNAME-Eintrag für _&lt;&lt;www.yourdomain.com>>_ hinzu, der auf **prod.magentocloud.map.fastly.net** verweist.
   2. Legen Sie vier A-Einträge für _&lt;&lt;yourdomain.com>>_ fest, die auf Folgendes verweisen:\
      151 101 1 124\
      151 101 65 124\
      151 101 129 124\
      151 101 193 124
2. Ändern Sie die Adobe Commerce-Basis-URL in &quot;_&lt;&lt;www.yourdomain.com>_&quot;
3. Warten Sie, bis die TTL-Zeit vergangen ist, und starten Sie dann den Webbrowser neu.
4. Testen Sie die Website.

### Wenn Sie ein Problem haben, das die Live-Schaltung blockiert:

Wenn Sie bei Problemen auf Probleme stoßen, die Sie am Start während der Umstellung hindern, können Sie am schnellsten rechtzeitig Unterstützung erhalten, indem Sie den Helpdesk verwenden und ein Ticket mit dem Grund &quot;Mein Geschäft kann nicht gestartet werden&quot;öffnen und eine Hotline-Support-Nummer aufrufen (siehe [die Liste der Hotline-Nummern von Adobe Commerce P1 (Priorität 1)](https://support.magento.com/hc/en-us/articles/360042536151){target="_blank"}):

- Gebührenfrei in den USA: (+1) 877 282 7436 (direkt zur Adobe Commerce P1-Hotline)
- Gebührenfrei in den USA: (+1) 800 685 3620 (drücken Sie im ersten Menü die Taste 7 für Adobe Commerce P1-Hotline)
- US Local: (+1) 408 537 8777

## 11. Nach der Live-Schaltung

Sobald die Site live ist, senden Sie eine E-Mail an den zugewiesenen CTA (Customer Technical Advisory), CSE (Customer Success Engineer) und AEM (Account Manager). Wenn Sie dem Projekt jedoch keinen Kundenbetreuer zugewiesen haben, können Sie ein Support-Ticket erstellen, in dem Sie darum bitten, die Überwachung mit hoher SLA zu aktivieren, sobald die Site live geschaltet wurde. Der CTA/CSE führt die folgenden Aufgaben aus, sobald geprüft wird, dass die Site mit Fastly-Aktivierung und Caching gestartet wurde:

- Taggen Sie den Cluster als live und erstellen Sie ein Support-Ticket, um die Überwachung für High SLA (Service Level Agreements) zu aktivieren.
- Aktivieren Sie New Relic Synthetics für die Überwachung der Betriebszeit.

>[!MORELIKETHIS]
> 
> - [Launch-Bereitschaftsübersicht - Implementierungs-Playbook](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/launch/overview){target="_blank"}
> - [Checkliste starten - Benutzerhandbuch](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist){target="_blank"}
> - [Checkliste für den Vorabstart - Site-Manager/Commerce-Administratorhandbuch](https://experienceleague.adobe.com/en/docs/commerce-admin/start/setup/prelaunch-checklist){target="_blank"}
> - [Sicherheitsmodell für gemeinsame Verantwortung](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility){target="_blank"}
