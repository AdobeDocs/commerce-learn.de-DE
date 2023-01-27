---
title: Hinzufügen einer Tabelle zu einer Datenbank
description: "[!DNL Commerce] verfügt über einen speziellen Mechanismus, mit dem Sie Datenbanktabellen erstellen, vorhandene ändern und sogar Daten hinzufügen können."
topic: Development
kt: 5613
doc-type: video
activity: use
exl-id: fb222752-5689-4f87-94cf-a61ed7005e6b
source-git-commit: e8d2631b31319701beb327f42fdf1372d9dad9b7
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Hinzufügen einer Tabelle zu einer Datenbank

>[!IMPORTANT]
>
>Dies wird nicht mehr empfohlen, siehe https://developer.adobe.com/commerce/php/development/components/declarative-schema/


[!DNL Commerce] verfügt über einen speziellen Mechanismus, mit dem Sie Datenbanktabellen erstellen, vorhandene ändern und sogar Daten hinzufügen können - wie Setup-Daten, die hinzugefügt werden müssen, wenn ein Modul installiert wird. Dieser Mechanismus ermöglicht es, diese Änderungen zwischen verschiedenen Installationen zu übertragen.

Statt bei der Neuinstallation des Systems wiederholt manuelle SQL-Vorgänge auszuführen, erstellen Entwickler ein Installations- (oder Upgrade-) Skript, das die Daten enthält. Das Skript wird jedes Mal ausgeführt, wenn ein Modul installiert wird.

## Für wen ist dieses Video?

- Entwickler

## Videoinhalt

- Modul erstellen
- InstallSchema-Skript erstellen
- Create InstallData Script
- Neues Modul hinzufügen und sicherstellen, dass eine Tabelle mit Daten erstellt wurde
- UpgradeSchema-Skript erstellen
- UpgradeData-Skript erstellen
- Führen Sie Aktualisierungsskripte aus und überprüfen Sie, ob die Tabelle geändert wurde.

>[!VIDEO](https://video.tv.adobe.com/v/35791?quality=12&learn=on)

## Nützliche Ressourcen

- [Migrieren von Installations-/Upgrade-Skripten in ein deklaratives Schema](https://developer.adobe.com/commerce/php/development/components/declarative-schema/migration-scripts/)
