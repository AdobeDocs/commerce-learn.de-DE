---
title: Anzeigen und Festlegen von Admin-Konfigurationen über die Befehlszeile
description: Erfahren Sie, wie Sie Admin-Konfigurationen über die Befehlszeile anzeigen und festlegen können.
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

# Anzeigen und Festlegen von Admin-Konfigurationen über die Befehlszeile

Eine Demonstration zum Anzeigen, Festlegen und Suchen von Konfigurationswerten mit der Commerce-CLI. Verstehen, wo die Werte gespeichert werden und wo die Standardwerte herkommen

## Für wen ist dieses Video bestimmt?

- Adobe Commerce-Entwickler

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3439979?&learn=on&captions=ger)

## Einige im Tutorial verwendete Befehle

Ändern Sie die Sicherheitseinstellung des Kennworts in Empfohlen:

`$ php bin/magento config:set admin/security/password_is_forced 0`

E-Mail-Adresse für die Funktion zum automatischen Kopieren von Kundenaufträgen anzeigen

`$ php bin/magento config:show sales_email/order/copy_to`

Leeres Ergebnis für eine Konfiguration anzeigen, die einen Wert in Admin hat

`php bin/magento config:show trans_email/ident_sales/email`

## Im Tutorial verwendete MySQL-Abfragen

```
SELECT * FROM core_config_data WHERE path = 'sales_email/order/copy_to';

SELECT * FROM core_config_data WHERE path = 'sales_email/order_comment/copy_to';

SELECT * FROM core_config_data WHERE path = 'trans_email/ident_sales/email';
```

## Wo finde ich die Standard-Verkaufs-E-Mail?

Wie finde ich den Konfigurationswert, der irgendwo in der Code-Basis definiert ist?
`grep -rnw vendor/magento/ -e 'sales@example.com'`

So zeigen Sie eine Seite im Terminal und Zeilennummern `cat -n vendor/magento/module-email/etc/config.xml` an

## Zusätzliche Ressourcen

- [Befehlszeilen-Tool](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/config-cli.html?lang=de){target="_blank"}
- [Konfigurieren der Admin-Sicherheit](https://experienceleague.adobe.com/docs/commerce-admin/systems/security/security-admin.html?lang=de){target="_blank"}
