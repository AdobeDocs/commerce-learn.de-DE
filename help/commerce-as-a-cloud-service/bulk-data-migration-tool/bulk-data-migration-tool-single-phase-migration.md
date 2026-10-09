---
title: Tool für die Massendatenmigration - Einphasige Migration
description: Erfahren Sie, wie Sie mit dem Tool für die Massendatenmigration eine einphasige Migration für Probeläufe und Umgebungen ausführen, in denen die Quelle während der Extraktion live bleiben kann.
role: Developer
level: Intermediate
doc-type: Technical Video
topic: Migration
feature: Data Import/Export
duration: 737
last-substantial-update: 2026-07-24T00:00:00.000Z
jira: KT-22139
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%
---
# Ausführen einer einphasigen Migration mit dem Tool für die Massendatenmigration

Führen Sie eine einphasige Migration durch, wenn Ihre Quellumgebung während der Extraktion live bleiben kann - ideal für Trockenläufe sowie Entwicklungs- oder Sandbox-Umgebungen. Wenn Sie eine eingefrorene Quelle benötigen, z. B. eine Produktionsumstellung, bei der während der Migration keine neuen Bestellungen eingehen können, sehen Sie sich stattdessen das Video zur schrittweisen Migration in dieser Reihe an.

## Für wen ist dieses Video bestimmt?

* Lösungsarchitekt
* DevOps-Engineer
* Backend-Entwicklerperson

## Videoinhalt

* Erstellen Sie das Docker-Image mit `bin console build` - führen Sie dies nur erneut aus, wenn sich die Docker-Datei ändert.
* Um den CDMS-CLI-Container-Manager zu starten, führen Sie `bin console start` aus und öffnen Sie dann eine Shell im Container, um die Abhängigkeiten herunterzuladen.
* Um die vollständige zehn-Schritte-Pipeline auszuführen, führen Sie `bin console migration` aus: Überprüfen Sie die Konfiguration, initialisieren Sie die Umgebung, öffnen Sie PaaS-Tunnel, führen Sie Integrationstests aus, registrieren Sie sich beim CDMS, analysieren Sie das Zielschema, generieren Sie Testdaten, extrahieren Sie Quelldaten, laden Sie in ACS, überprüfen Sie Prüfsummen, bereinigen Sie und fassen Sie zusammen.
* Überprüfen Sie den Migrationszusammenfassungsbericht - Schritt 8 (Datenintegritätsprüfung) protokolliert Fehler, ohne die Pipeline anzuhalten, sodass ein abgeschlossener Durchlauf keine saubere Überprüfung garantiert.
* Dieser einphasige Befehl ist eine vollständige, in sich abgeschlossene Pipeline. Verwenden Sie ihn nicht als Schritt innerhalb des Workflows für den Wartungsmodus (stufenweise Migration), der über eigene dedizierte Befehle verfügt.

>[!VIDEO](https://video.tv.adobe.com/v/3496316?learn=on)
