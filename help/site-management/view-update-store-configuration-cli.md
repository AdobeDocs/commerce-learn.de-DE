---
title: Anzeigen und Festlegen von Admin-Konfigurationen über die Befehlszeile
description: Erfahren Sie, wie Sie Admin-Konfigurationen über die Befehlszeile anzeigen und festlegen können.
feature: Configuration,Console,System
topic: Administration,Commerce
role: Developer
level: Beginner
doc-type: Technical Video
duration: 510
last-substantial-update: 2024-01-31T00:00:00.000Z
jira: KT-14877
exl-id: 6cecba51-8d39-46f5-9864-80126d8ca3da
TQID: https://experienceleague.adobe.com/W0kaFd-DJAPA1kFO0hWaBZXsSarojbt5Hnv3QkW85hA
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 168
ht-degree: 0%

---

# Anzeigen und Festlegen von Admin-Konfigurationen über die Befehlszeile

Eine Demonstration zum Anzeigen, Festlegen und Suchen von Konfigurationswerten mit der Commerce-CLI. Verstehen, wo die Werte gespeichert werden und wo die Standardwerte herkommen

## Für wen ist dieses Video bestimmt?

* Adobe Commerce-Entwickler

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3439979?captions=ger&learn=on)

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

* [Befehlszeilen-Tool](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/config-cli.html?lang=de){target="_blank"}
* [Konfigurieren der Admin-Sicherheit](https://experienceleague.adobe.com/docs/commerce-admin/systems/security/security-admin.html?lang=de){target="_blank"}
