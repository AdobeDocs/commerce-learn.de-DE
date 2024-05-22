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
source-git-commit: 00a8d6883473de796abc79ef2e9be34f56429a17
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 0%

---

# Commerce Cloud Pre-Launch-Checkliste

Im Folgenden finden Sie eine Zusammenfassung der Adobe Commerce [Dokumentation zum Site-Launch](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/overview){target="_blank"}.

Diese Checkliste soll bei der Planung und Ausführung eines erfolgreichen Starts der Adobe Commerce Cloud-Website helfen. Arbeiten Sie mit Ihrem Systemintegrator für Adobe Commerce Cloud zusammen, um sicherzustellen, dass alle Konfigurationsaufgaben und Checklisten-Elemente abgeschlossen und überprüft werden. Sollten Sie Schwierigkeiten mit der Checkliste haben oder Fragen haben, wenden Sie sich an den zuständigen technischen Kundenberater oder Customer Success Engineer. Wenn Ihrem Konto keine CTA/CSE zugewiesen ist, können Sie ein Support-Ticket für Unterstützung erstellen.

Wenn Sie dem Konto eine CTA/CSE zugewiesen haben, wenden Sie sich mindestens 4 Wochen vor dem Start der neuen Adobe Commerce Cloud-Website an diese und an den Kundenbetreuer, um sie über Ihre **Absicht** , um zu starten.

- Einige Prüfungen werden hervorgehoben mit [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"}
- Stellen Sie sicher, dass Sie mit Ihrem Entwickler- oder Systemintegrationspartner zusammenarbeiten, um Ihren Implementierungsansatz zu koordinieren.

>[!IMPORTANT]
> Sie akzeptieren [Verantwortung](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility){target="_blank"} für alle schädlichen Auswirkungen und damit verbundenen Risiken auf den Zeitplan für den Produktionsstart und die kontinuierliche Stabilität des Standorts, wenn Sie diese Checkliste nicht verwenden und abschließen.

## 1. Pre-Go Live

1. Lesen Sie die Dokumentation zu Testen und Live-Schaltung . [Dokumentation zum Site-Launch](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/overview){target="_blank"}

   >[!NOTE]
   >Sicherstellen einer umfassenden _&quot;Go live readiness Plan&quot;_ ist vollständig mit Ihrem Partner oder Systemintegrator vorbereitet und beinhaltet alle notwendigen Aktionselemente. Beachten Sie, dass die Checkliste zwar die Best Practices vor dem Start hervorhebt, sie aber auch bewährte Verfahren vor dem Start berücksichtigt. _**nicht**_ die Notwendigkeit Ihres eigenen Go-Live-Bereitstellungsplans ersetzen.

2. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"}[Benutzerhandbuch](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/intro){target="_blank"})
3. Endbenutzer/Händler führten UAT (User Acceptance Testing) durch, einschließlich Backend-Operationen.
4. Das Systemintegratorteam hat durchgängige UAT für Staging und Produktion durchgeführt. Siehe Abschnitt [Experience League-Dokumentation](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production){target="_blank"}.
5. Bestätigen Sie die Codebereitstellung und -tests in Staging- und Produktionsumgebungen ([Mehr dazu](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production){target="_blank"}).
6. Die Größe des Produktionsclusters wurde dauerhaft auf die vertraglich vereinbarte tägliche Grundlinie erhöht. Wenden Sie sich an den zugewiesenen CTA/CSE, um weitere Informationen zu erhalten, oder heben Sie ein Support-Ticket auf.

## 2. Aktuelle Konfigurationen

1. Aktualisieren Sie Adobe Commerce und die zugehörigen Pakete/Dienste auf die [neueste Version](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview){target="_blank"}
2. Überprüfen Sie die aktuellen Konfigurationen und Dienste mit Ihrem SI/Partner und [Best Practices befolgen](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/catalog-management){target="_blank"}.
3. Überprüfen Sie MySQL/Shared-Files [Festplattenauslastung](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space){target="_blank"}

## 3. Schnelle Konfigurationen

1. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"}[Vollseitencache](https://developer.adobe.com/commerce/frontend-core/guide/caching/){target="_blank"} oder [Zwischenspeicherung in GraphQL](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/){target="_blank"}). Lesen Sie die [Schnelles Setup-Handbuch](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly){target="_blank"}.
2. Verwenden Sie gegebenenfalls die GET-Methode für GraphQL-Abfragen auf PWA/Headless-Websites.

   >[!NOTE]
   > Nur Abfragen, die mit einem HTTP-GET-Vorgang gesendet wurden, können zwischengespeichert werden (falls zutreffend). [POST-Abfragen können nicht zwischengespeichert werden](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/){target="_blank"}.

3. Stellen Sie sicher, dass die schnelle Bildoptimierung aktiviert ist ([Siehe Fastly Image Optimization .](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly-image-optimization){target="_blank"})
4. Überprüfen Sie, ob die richtige Schildposition konfiguriert ist ([Cache-, Backends- und Ursprungs-Shirding konfigurieren](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration){target="_blank"}).
5. Web Application Firewall (**WAF**) funktioniert. (Siehe [Fehlerbehebung bei blockierten Anfragen](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly-waf-service){target="_blank"}, sofern vorhanden, und Einschränkungen)
6. Schnelles Aktualisieren [&quot;Ignorierte URL-Parameter&quot;](https://github.com/iancassidyweb/magento2/commit/68fdecfcd26c957382b8d68b64887e0a83298524){target="_blank"} im Admin-Bereich, um die Cache-Leistung zu verbessern.

   >[!NOTE]
   > In der Fastly-Konfiguration unter _Admin > Stores > Konfigurationen > System > Vollständiger Seiten-Cache > Schnelle Konfiguration > Erweiterte Konfiguration > Ignorierte URL-Parameter (Global)_, finden Sie eine kommagetrennte Liste von Parametern, die bei der Suche nach zwischengespeicherten Seiten von Fastly ignoriert werden sollten. Stellen Sie sicher, dass Sie den VCL erneut hochladen, nachdem Sie diese Liste geändert haben.

## 4. DNS und SSL

1. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"}_(Senden Sie ein Support-Ticket im Voraus für hinzugefügte oder geänderte Domänen)_
2. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"}[diesem Artikel](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/ssl-tls-certificates-for-magento-commerce-cloud-faq){target="_blank"} für weitere Informationen.
3. DNS aktualisieren [TTL (Time to Live)](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist#to-update-dns-configuration-for-site-launch){target="_blank"} -Wert auf das Mindestmaß, für das Liveschluss.
4. Aktivieren von Sendgrid SPF und DKIM

   >[!NOTE]
   > Fügen Sie der DNS-Konfiguration die SendGrid-CNAME-Einträge für jede Domäne hinzu. Lesen [SendGrid-E-Mail-Dienst](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/sendgrid){target="_blank"} um zu sehen, wie Sie die Absenderdomänen ändern können und vieles mehr.

## 5. Datenbankkonfigurationen

Adobe Commerce Cloud verwendet einen MariaDB Galera-Cluster als Datenbank für die Staging- und Produktionsumgebung. Galera-Cluster sind maßgeblich für die Verbesserung der Leistung und Skalierbarkeit. In den folgenden Artikeln erhalten Sie Einblicke in die optimalen Vorgehensweisen und Einschränkungen von Galera-Cluster-Replikationen.

- [Best Practices für MySQL-Konfigurationen](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration){target="_blank"}
- Verwaltete Warnhinweise in Adobe Commerce: [MariaDB-Warnhinweise](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-mariadb-alerts){target="_blank"}
- Best Practices für [Datenbankkonfiguration](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud){target="_blank"}
- Detaillierte Analyse zu [Galera Cluster-Replikationen und Flusssteuerung.](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/backend-development/galera-db-slow-replication){target="_blank"}

1. [MYSQL-Slave-Verbindung](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration#slave-connections){target="_blank"} wird empfohlen, um die Leistung bei hohen Datenbanklasten zu verbessern.
2. Stellen Sie sicher, dass das Zeilenformat für alle Datenbanktabellen auf [DYNAMIC anstelle von COMPACT](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/maintenance/mariadb-upgrade#convert-database-table-storage-format){target="_blank"} (Dies gilt insbesondere für On-Premise- zu Cloud-Migrationen.)
3. Datenbank-Speicher-Engine ändern von [MyISAM to InnoDB](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud#convert-all-myisam-tables-to-innodb){target="_blank"} für alle Tabellen.
4. Überprüfen und optimieren Sie Datenbanktabellen mit einer Größe von mehr als 1 GB im Voraus.
5. Die Datenbankschemadaten sind aktuell und aktuell. (siehe [diesem Handbuch](https://mariadb.com/kb/en/engine-independent-table-statistics/#collecting-statistics-with-the-analyze-table-statement){target="_blank"}).

## 6. Dienstbezüge

1. Überprüfen Sie den idealen Status der statischen Inhaltsbereitstellung (SCD), um die Wartungszeit während Bereitstellungen in der Produktionsumgebung zu reduzieren. Überprüfen [Strategien zur statischen Inhaltsbereitstellung (SCD)](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/static-content){target="_blank"} und [Speicherkonfigurationsverwaltung](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/store-settings){target="_blank"} Handbuch.
2. Überprüfen Sie die Minimierungseinstellungen für HTML, JavaScript und CSS. (Dies gilt nicht für PWA/Headless-Websites).
3. Vergewissern Sie sich, dass die Verwendung der folgenden Cloud-Variablen mit den beabsichtigten Zwecken übereinstimmt. ([SCD_MATRIX](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-build#scd_matrix){target="_blank"}, [SCD_ON_DEMAND](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global#scd_on_demand){target="_blank"} und [SKIP_SCD](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy#skip_scd){target="_blank"})

## 7. Tests und Fehlerbehebung

1. Testen Sie die ausgehenden Transaktions-E-Mails. Mehr dazu [Adobe Commerce Cloud - SendGrid Mail-Funktion](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/sendgrid){target="_blank"}.
2. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"}
3. [!BADGE Blocker]{type=caution tooltip="Potenzieller Blocker"}

   >[!NOTE]
   > A [Belastungs- und Belastungstest dient dem Zweck](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/guidance#:~:text=A%20load%20test%20can%20help,Scan%20Tool%20for%20your%20sites.){target="_blank"} Ermittlung von Engpässen und Aufdeckung von Leistungsproblemen innerhalb der Anwendung. Es spielt eine entscheidende Rolle bei der Verwaltung der Erwartungen in Bezug auf die Clustergröße und bei der Festlegung der erforderlichen Skalierungsanpassungen, um die geschäftlichen Anforderungen effektiv zu erfüllen.

   >[!IMPORTANT]
   > **_WARNUNG:_** Bei der Vorbereitung des Belastungstests: **_nicht_** Live-Transaktions-E-Mails versenden (auch an Platzhalter-Adressen). Das Senden von E-Mails während des Tests kann dazu führen, dass das Projekt vor dem Start das für SendGrid konfigurierte standardmäßige Versandlimit (12k) erreicht.
   > 
   > - Deaktivieren der E-Mail-Kommunikation:
   >   Navigieren Sie zu _Store > Konfiguration > Erweitert > System > E-Mail-Versandeinstellungen_.

4. Durchführung von Sicherheitstests auf der Produktionsinstanz im Rahmen der [Sicherheitsmodell für gemeinsame Verantwortung](https://business.adobe.com/products/magento/secure-ecommerce.html){target="_blank"}. Für die PCI-Compliance (Payment Card Industry) erfordert die angepasste Website Penetrationstests.

## 8. Sonstige Konfigurationen

1. Indizierung wechseln zu _&quot;planmäßig aktualisieren_&quot;, mit Ausnahme der **_customer_grid_** , die weiterhin &quot;SAVE&quot;ist (siehe [Indizierungsmodi](https://developer.adobe.com/commerce/php/development/components/indexing/#indexing-modes){target="_blank"}).
2. Verwenden Sie Suchmaschinen oder -erweiterungen von Drittanbietern?
3. Bestätigen Sie, dass [SEO-Konfigurationen (Suchmaschinenoptimierung) sind ordnungsgemäß eingerichtet](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/seo-overview){target="_blank"} , damit Indexer/Crawler die Website gegebenenfalls scannen können.
4. Hinzufügen von Umleitungen und Routen (siehe [Routen konfigurieren](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/routes/routes-yaml){target="_blank"})

   >[!NOTE]
   >Fügen Sie Weiterleitungen und Routen zur Datei routes.yaml in der Integrationsumgebung hinzu und überprüfen Sie die Konfiguration in dieser Umgebung, bevor Sie sie in Staging und Produktion bereitstellen.

       &quot;http://{all}/&quot;:
       Typ: Upstream
       Upstream: &quot;mymagento:http&quot;
       
       &quot;http://{all}/&quot;:
       Typ: Upstream
       Upstream: &quot;mymagento:http&quot;
   
5. Stellen Sie sicher, dass XDebug deaktiviert ist, wenn es während der Entwicklung aktiviert ist (siehe [Xdebug konfigurieren](https://developer.adobe.com/commerce/cloud-tools/docker/test/configure-xdebug/){target="_blank"}).
6. Überprüfen Sie, ob der Op-Cache und andere Konfigurationen in der Datei php.ini ([siehe dieses Beispiel](https://github.com/magento/magento-cloud/blob/master/php.ini#L41){target="_blank"}).
7. Abonnieren Sie die [**Adobe Commerce-Statusseite**](https://status.adobe.com/cloud/experience_cloud#/){target="_blank"}.
8. Abonnieren von New Relic &quot;[Verwaltete Warnhinweise für Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce){target="_blank"}&quot;Benachrichtigungskanäle zur Überwachung der jeweiligen Leistungsmetriken ([mehr dazu](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/monitor/new-relic/new-relic-service){target="_blank"}).

## 9. Sicherheit

1. Einrichten des Adobe Commerce-Sicherheitsscan

   >[!NOTE]
   > [Adobe Commerce Security Scan ist ein nützliches Tool](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-scan){target="_blank"} , die Ihnen dabei hilft, veraltete Softwareversionen, falsche Konfigurationen und potenzielle Malware auf der Site zu entdecken. Melden Sie sich an, planen Sie die Ausführung oft und stellen Sie sicher, dass E-Mails an den richtigen technischen Sicherheitskontakt gesendet werden.
   > 
   > Führen Sie diese Aufgabe während der UAT aus. Wenn Sie die Option Periodische Scans verwenden, stellen Sie sicher, dass Sie Scans zu Zeiten geringer Nachfrage planen. Siehe [Sicherheitsscan](https://account.magento.com/scanner/index/dashboard/){target="_blank"} im Adobe Commerce-Konto. Sie müssen sich bei einem Adobe Commerce-Konto anmelden, um auf die Sicherheitsprüfung zugreifen zu können.

2. Ändern Sie die Standardeinstellungen für den Adobe Commerce-Administrator.
3. Ändern Sie das Administratorkennwort (siehe [Konfigurieren der Admin Security](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-admin){target="_blank"}).
4. Ändern der Admin-URL (siehe [Verwenden einer benutzerdefinierten Admin-URL](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#use-a-custom-admin-url){target="_blank"}).
5. Entfernen Sie alle Benutzer, die nicht mehr im Projekt enthalten sind (siehe [Benutzer erstellen und verwalten](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/user-access){target="_blank"}).
6. Kennwörter für Administratoren werden konfiguriert (siehe [Admin-Passwortanforderungen](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-admin){target="_blank"}).
7. Zwei-Faktor-Authentifizierung konfigurieren (siehe [Zweifaktorauthentifizierung](https://developer.adobe.com/commerce/testing/functional-testing-framework/two-factor-authentication/){target="_blank"}).

## 10. Live-Schaltung

Führen Sie die folgenden Schritte aus, um weitere Informationen zu erhalten (siehe [DNS-Konfigurationen](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist){target="_blank"}):

1. Greifen Sie auf Ihren DNS-Dienst zu und aktualisieren Sie A- und CNAME-Einträge für jede Ihrer Domänen und Hostnamen:
   1. Hinzufügen eines CNAME-Eintrags für _&lt;&lt;www.yourdomain.com>>_, unter Hinweis auf **prod.magentocloud.map.fastly.net**
   2. Legen Sie vier A-Datensätze für _&lt;&lt;yourdomain.com>>_, der auf Folgendes verweist:\
      151 101 1 124\
      151 101 65 124\
      151 101 129 124\
      151 101 193 124
2. Ändern Sie die Adobe Commerce-Basis-URL in _&lt;&lt;www.yourdomain.com>>_
3. Warten Sie, bis die TTL-Zeit vergangen ist, und starten Sie dann den Webbrowser neu.
4. Testen Sie die Website.

### Wenn Sie ein Problem haben, das die Live-Schaltung blockiert:

Wenn Sie auf Probleme stoßen, die Sie daran hindern, während der Umstellung gestartet zu werden, besteht die schnellste Methode, um eine angemessene Unterstützung zu erhalten, darin, den Helpdesk zu verwenden und ein Ticket mit dem Grund &quot;Mein Geschäft kann nicht gestartet werden&quot;zu öffnen, und eine Hotline-Supportnummer aufzurufen (siehe [die Liste der Hotline-Nummern der Adobe Commerce P1 (Priorität 1)](https://support.magento.com/hc/en-us/articles/360042536151){target="_blank"}):

- Gebührenfrei in den USA: (+1) 877 282 7436 (direkt zur Adobe Commerce P1-Hotline)
- Gebührenfrei in den USA: (+1) 800 685 3620 (drücken Sie im ersten Menü die Taste 7 für Adobe Commerce P1-Hotline)
- US Local: (+1) 408 537 8777

## 11. Nach der Live-Schaltung

Sobald die Site live ist, senden Sie eine E-Mail an den zugewiesenen CTA (Customer Technical Advisory), CSE (Customer Success Engineer) und AEM (Account Manager). Wenn Sie dem Projekt jedoch keinen Kundenbetreuer zugewiesen haben, können Sie ein Support-Ticket erstellen, in dem Sie die Aktivierung der High SLA-Überwachung beantragen, sobald die Site live geschaltet wurde. Der CTA/CSE führt die folgenden Aufgaben aus, sobald geprüft wird, dass die Site mit Fastly-Aktivierung und Caching gestartet wird:

- Taggen Sie den Cluster als live und erstellen Sie ein Support-Ticket, um die Überwachung von High SLA (Service Level Agreements) zu aktivieren.
- Aktivieren Sie New Relic Synthetics für die Überwachung der Betriebszeit.

>[!MORELIKETHIS]
> 
> - [Launch-Bereitschaftsübersicht - Implementierungs-Playbook](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/launch/overview){target="_blank"}
> - [Checkliste für Launch - Benutzerhandbuch](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist){target="_blank"}
> - [Checkliste vor dem Start - Site Manager/Commerce Admin-Handbuch](https://experienceleague.adobe.com/en/docs/commerce-admin/start/setup/prelaunch-checklist){target="_blank"}
> - [Sicherheitsmodell für gemeinsame Verantwortung](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility){target="_blank"}
