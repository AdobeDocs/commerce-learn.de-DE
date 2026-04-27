---
title: Zurücksetzen des Admin-URI mithilfe der CLI
description: Erfahren Sie, wie Sie den Admin-URI in der Adobe Commerce Cloud-CLI zurücksetzen. Diese Methode ist praktisch, wenn Änderungen an der Admin-URL Zugriffsprobleme verursachen.
feature: Admin Workspace, Console
topic: Administration, Commerce
role: Developer, User
level: Beginner
doc-type: Technical Video
duration: 144
last-substantial-update: 2024-10-14T00:00:00.000Z
jira: KT-16338
exl-id: dbc155d7-8ce9-4622-abfb-1d8077c3a975
TQID: https://experienceleague.adobe.com/OgyaTHVhQSRFApJPYwkzodSyAJcBjwk8kIrw4VBXltQ
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 107
ht-degree: 0%

---

# Admin-URI mithilfe der CLI zurücksetzen

Erfahren Sie, wie Sie den Admin-URI mit dem Adobe Commerce Cloud-CLI-Befehl zurücksetzen. Dies ist nützlich, wenn die Admin-URL vom Administrator geändert wurde, aber ein Fehler aufgetreten ist und Sie nicht mehr auf den Administrator zugreifen können.

>[!VIDEO](https://video.tv.adobe.com/v/3435066?learn=on)

## Einige im Tutorial verwendete Befehle

Ändern Sie die Konfiguration so, dass eine benutzerdefinierte Admin-Pfad-URL als 0 erwartet wird:

`$ php bin/magento config:set admin/url/use_custom 0`

Ändern Sie die Konfiguration für die benutzerdefinierte Admin Path-URL auf 0

`$ php bin/magento config:set admin/url/use_custom_path 0`
