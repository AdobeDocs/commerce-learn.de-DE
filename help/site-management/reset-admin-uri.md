---
title: Zurücksetzen des Admin-URI mithilfe der CLI
description: Erfahren Sie, wie Sie den Admin-URI in der Adobe Commerce Cloud-CLI zurücksetzen. Diese Methode ist praktisch, wenn Änderungen an der Admin-URL Zugriffsprobleme verursachen.
feature: Admin Workspace, Console
topic: Administration, Commerce
role: Developer, User
level: Beginner
doc-type: Technical Video
duration: 123
last-substantial-update: 2024-10-14T00:00:00Z
jira: KT-16338
exl-id: dbc155d7-8ce9-4622-abfb-1d8077c3a975
source-git-commit: 25ee35b730cc6265665a87c9c37d24e88c41b60e
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# Admin-URI mithilfe der CLI zurücksetzen

Erfahren Sie, wie Sie den Admin-URI mit dem Adobe Commerce Cloud-CLI-Befehl zurücksetzen. Dies ist nützlich, wenn die Admin-URL vom Administrator geändert wurde, aber ein Fehler aufgetreten ist und Sie nicht mehr auf den Administrator zugreifen können.

>[!VIDEO](https://video.tv.adobe.com/v/3435066/?learn=on)

## Einige im Tutorial verwendete Befehle

Ändern Sie die Konfiguration so, dass eine benutzerdefinierte Admin-Pfad-URL als 0 erwartet wird:

`$ php bin/magento config:set admin/url/use_custom 0`

Ändern Sie die Konfiguration für die benutzerdefinierte Admin Path-URL auf 0

`$ php bin/magento config:set admin/url/use_custom_path 0`
