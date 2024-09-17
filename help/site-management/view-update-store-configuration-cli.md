---
title: Anzeigen und Festlegen von Admin-Konfigurationen mithilfe der Befehlszeile
description: Erfahren Sie, wie Sie Admin-Konfigurationen über die Befehlszeile anzeigen und festlegen.
feature: Configuration,Console,System
topic: Administration,Commerce
role: Developer
level: Beginner
doc-type: Technical Video
duration: 462
last-substantial-update: 2024-01-31T00:00:00Z
jira: KT-14877
exl-id: 6cecba51-8d39-46f5-9864-80126d8ca3da
source-git-commit: d578c066f3e51827694c8bf85aa2324035a8b07b
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# Anzeigen und Festlegen von Admin-Konfigurationen mithilfe der Befehlszeile

Eine Demonstration zum Anzeigen, Festlegen und Suchen von Konfigurationswerten mit der Commerce-CLI. Erfahren Sie, wo die Werte gespeichert werden und wo die Standardwerte herkommen.

## Für wen ist dieses Video?

- Adobe Commerce-Entwickler

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3427123?&learn=on)

## Einige im Tutorial verwendete Befehle

Ändern Sie die Kennwortsicherheitseinstellung in &quot;Empfohlen&quot;:

`$ php bin/magento config:set admin/security/password_is_forced 0`

Anzeigen der E-Mail-Adresse für die Funktion zum automatischen Kopieren von Verkaufsbestellungen

`$ php bin/magento config:show sales_email/order/copy_to`

Leeres Ergebnis für eine Konfiguration anzeigen, die einen Wert in admin hat

`php bin/magento config:show trans_email/ident_sales/email`

## Im Tutorial verwendete MySQL-Abfragen

```
SELECT * FROM core_config_data WHERE path = 'sales_email/order/copy_to';

SELECT * FROM core_config_data WHERE path = 'sales_email/order_comment/copy_to';

SELECT * FROM core_config_data WHERE path = 'trans_email/ident_sales/email';
```

## Auffinden der standardmäßigen Verkaufs-E-Mail

Wie finde ich den Konfigurationswert, der irgendwo in der Codebase definiert ist?
`grep -rnw vendor/magento/ -e 'sales@example.com'`

So zeigen Sie eine Seite im Terminal an und zeigen die Zeilennummern an `cat -n vendor/magento/module-email/etc/config.xml`

## Zusätzliche Ressourcen

- [Befehlszeilenwerkzeug](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/config-cli.html){target="_blank"}
- [Konfigurieren der Administrator-Sicherheit](https://experienceleague.adobe.com/docs/commerce-admin/systems/security/security-admin.html){target="_blank"}
