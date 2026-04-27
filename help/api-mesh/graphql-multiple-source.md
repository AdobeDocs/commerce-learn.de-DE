---
title: Erstellen einer GraphQL mit mehreren Quellen zur Verwendung in API-Mesh
description: Erfahren Sie, wie Sie mehrere Quellen für API Mesh in Adobe Commerce und  [!DNL Adobe App Builder]. Erfahren Sie mehr über einige häufige Fehler und deren Behebung.
jira: KT-11804
doc-type: Tutorial
duration: 409
last-substantial-update: 2023-02-08T00:00:00.000Z
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Developer
level: Beginner, Intermediate
exl-id: d788a068-9d20-4db0-a0eb-fd897873253d
TQID: https://experienceleague.adobe.com/O6ONn4NzMP-VqN0nsCoD-OPkZGMBelLWB-KNP1fZqmA
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 199
ht-degree: 0%

---

# Erstellen eines Netzes mit mehreren Quellen

In diesem Video erfahren Entwicklerinnen und Entwickler, wie sie ein Netz mit mehreren Quellen in API Mesh für Adobe Developer App Builder erstellen. In diesem Video erfahren Sie, wie Sie ein Netz mit mehreren Quellen erstellen und Fehler identifizieren. Weitere Informationen und Codebeispiele finden Sie unter [Erstellen eines Netzes](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1){target="_blank"}.

## Für wen ist dieses Video bestimmt?

* Alle, die neu bei API Mesh sind
* Entwickler, die mehrere API- und GraphQL-Quellen kombinieren möchten

## Videoinhalt

* Verwendung von [Transformationen](https://developer.adobe.com/graphql-mesh-gateway/gateway/transforms/){target="_blank"} zum Ändern des standardmäßigen Quellschemas
* Fehlerbehebung bei Fehlern, z. B. Namenskonflikten, Schemaverfügbarkeit und anderen Problemen mit der Schemasyntax
* Aktualisieren des Netzes mit einer geänderten Konfiguration

>[!VIDEO](https://video.tv.adobe.com/v/3414125?learn=on)

## Erstellen der JSON-Konfigurationsdatei

API Mesh verwendet eine JSON-Konfigurationsdatei, um Ihre Quell-Handler zu definieren. Die JSON-Datei enthält ein `sources`-Array, das die Quellen für Ihr Netz enthält. Im Folgenden finden Sie ein Beispiel für ein Netz mit mehreren Quellen.

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
        "name": "Example",
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
