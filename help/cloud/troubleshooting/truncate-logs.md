---
title: Protokolle kürzen
description: Erfahren Sie, wie Sie eine fehlgeschlagene Bereitstellung aufgrund einer vollen Festplatte durch Abschneiden großer Protokolldateien einteilen können.
feature: Cloud, Site Management
topic: Commerce, Development
role: Architect, Developer
level: Beginner, Intermediate
doc-type: Technical Video
duration: 206
last-substantial-update: 2025-3-25
jira: KT-17595
source-git-commit: b90aa9eb8759391a16dfb29ca25b0d2d271956ed
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Protokolle kürzen

Erfahren Sie, wie Sie eine fehlerhafte Bereitstellung aufgrund einer vollen Festplatte testen und beheben können. Erfahren Sie, wie Sie Befehle finden und ausführen können, um Speicherplatz in Ihrer Adobe Commerce Cloud-Umgebung freizugeben.

Wenn Sie glauben, dass Sie diese Protokolldateien benötigen, können Sie sie `rsync` oder andere Methoden verwenden, um eine Kopie vom Server zur Verfügung zu stellen, bevor Sie sie abschneiden.

## Für wen ist dieses Video gedacht?

- Entwickler und IT-Experten
- Systemadministratoren

## Videoinhalt

- Diagnose und Behebung einer fehlgeschlagenen Bereitstellung
- Wo sich einige häufig vorkommende große Protokolldateien befinden
- Schnellmethode zum Abschneiden einer Protokolldatei

>[!VIDEO](https://video.tv.adobe.com/v/3454572?learn=on)


## Im Video verwendete Befehle

So überprüfen Sie die `df -h` des Festplattenspeichers. Achten Sie auf die Zeile dev/mapper/xxxx

```SHELL
df -h

Filesystem                              Size  Used Avail Use% Mounted on
/dev/loop217                           1016M 1016M     0 100% /
none                                    492K  4.0K  488K   1% /dev
fake-sysfs                              120G     0  120G   0% /sys
tmpfs                                   120G     0  120G   0% /sys/fs/cgroup
tmpfs                                   384M     0  384M   0% /dev/shm
tmpfs                                    50M  460K   50M   1% /run
tmpfs                                   5.0M     0  5.0M   0% /run/lock
/dev/loop236                            144M  144M     0 100% /app
/dev/mapper/hyjh5nlaoabqtxxnh4opgjqzpu  4.9G  4.9G     0 100% /mnt
/dev/loop14                             8.0G  403M  7.6G   5% /tmp
/dev/mapper/platform-lxc                5.0T   69G  4.7T   2% /run/shared
```


Zeigen Sie die Dateien und ihre Größen in menschenlesbarem Format wie KB, MB und GB mithilfe der `ls -lah` an

```SHELL
ls -lah

total 4.7G
drwxr-xr-x 2 web web 4.0K Jul 16  2024 .
drwxr-xr-x 6 web web 4.0K Jan 10  2024 ..
-rw-rw-r-- 1 web web 487K Jul  5  2024 cache.log
-rw-r--r-- 1 web web 1.2K Jul 16  2024 cloud.error.log
-rw-r--r-- 1 web web 328K Mar 25 14:09 cloud.log
-rw-rw-r-- 1 web web 2.4G Jul  5  2024 cron.log
-rw-rw-r-- 1 web web  363 Dec  6  2023 debug.log
-rw-rw-r-- 1 web web  15K Jan 10  2024 indexation.log
-rw-r--r-- 1 web web 229K Jan 10  2024 install_upgrade.log
-rw-r--r-- 1 web web 2.9K Jul 16  2024 patch.log
-rw-rw-r-- 1 web web 2.4G Mar 25 15:36 support_report.log
-rw-rw-r-- 1 web web  516 Dec  6  2023 system.log
```

## Beispiele für das Abschneiden von Protokollen

Nachdem Sie SSH in das richtige Projekt und die richtige Umgebung verschoben haben, wechseln Sie in das Verzeichnis `var/log` . Dann können Sie eine Datei mit etwas Ähnlichem wie `> some-log-file.log` abschneiden

```BASH
> support_report.log 
> cron.log 
```

## Verwandte Dokumentation

- [Konsistenzbenachrichtigungen](https://experienceleague.adobe.com/de/docs/commerce-on-cloud/user-guide/dev-tools/integrations/health-notifications){target="_blank"}
