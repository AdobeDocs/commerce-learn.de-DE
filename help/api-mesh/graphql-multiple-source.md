---
title: Erstellen einer GraphQL mit mehreren Quellen zur Verwendung im API-Mesh
description: Erfahren Sie, wie Sie mehrere Quellen für das API-Mesh in Adobe Commerce verwenden und [!DNL Adobe App Builder]. Erfahren Sie mehr über einige häufige Fehler und wie Sie diese beheben können.
landing-page-description: Erfahren Sie, wie Sie API-Mesh in Adobe Commerce verwenden und [!DNL Adobe App Builder]. Erfahren Sie mehr über das Erstellen einer Anfrage mit mehreren Quellen und wie Sie einige häufige Fehler beheben können.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
source-git-commit: b6d501c5c852e1cc2cf1f05f91b5a9d96ac7d036
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Mehrere Quell-GraphQL-API-Maschen erstellen

Das Video hilft Entwicklern dabei, zu verstehen, wie ein Reverse-Proxy mit mehreren Quellen für GraphQL erstellt wird. In diesem Video wird gezeigt, wie verschiedene Quellen zugeordnet, Fehler erkannt und Änderungen an Git gespeichert werden. Grundlegende Codebeispiele, die im Video verwendet wurden, finden Sie unter [Erstellen eines Gitters](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1).

## Für wen ist dieses Video?

* Jeder, der neu für das API-Gitter ist
* Entwickler, die mehrere grafische Quellen verwenden möchten
* Jeder, der wissen muss, wie die Registerkarte &quot;Netzwerk&quot;gefiltert und nach Grafik gefiltert werden soll

## Videoinhalt

* Wie das API-Schema für komplexe benutzerdefinierte Attribute aus einer zweiten Quelle das standardmäßige Quellschema überschreiben kann
* Ändern der API-Gitterkonfiguration, um das zweite überschreibende Schema zu berücksichtigen
* Beheben von Fehlern, die im Prozess auftreten können, z. B. Namenskonflikte, Schemaverfügbarkeit und andere SDL-Syntax
* Beispiel für häufige Fehler nach Versuchen, Schemas zuzuordnen
* Erstellen des API-Gitters nach Bearbeitung neu
* Speichern von Änderungen an Git nach Änderung der API-Message-Konfiguration

>[!VIDEO](https://video.tv.adobe.com/v/3414125)

## JSON-Konfigurationsdatei erstellen

Damit Adobe App Builder von all Ihren Quellen erfahren kann, definieren Sie sie in einer JSON-Konfiguration. Jede Quelle ist ein Element in einem Array und Sie können eine oder mehrere haben. Im Folgenden finden Sie ein Beispiel für eine Mehrfachquellenanforderung, die miteinander verknüpft sind, um eine einzelne Antwort zu bilden.

```json
{
"meshConfig": {
    "sources": [
      {
        "name": "Commerce",
        "handler": {
          "graphql": {
            "endpoint": "https://venia.magento.com/graphql/"
          }
        }
      },
      {
        "name": "ERP",
        "handler": {
          "graphql": {
            "endpoint": "https://www.example.com/graphql/"
          }
        }
      }
    ]
  }
}
```

{{$include /help/_includes/api-mesh-related-links.md}}
