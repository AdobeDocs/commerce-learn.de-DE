---
title: Erstellen einer GraphQL mit mehreren Quellen zur Verwendung in API-Mesh
description: Erfahren Sie, wie Sie mehrere Quellen für API Mesh in Adobe Commerce und  [!DNL Adobe App Builder]. Erfahren Sie mehr über einige häufige Fehler und deren Behebung.
landing-page-description: Erfahren Sie, wie Sie API Mesh in Adobe Commerce und  [!DNL Adobe App Builder]. Erfahren Sie, wie Sie ein Netz mit mehreren Quellen erstellen und einige häufige Fehler beheben.
short-description: Erfahren Sie, wie Sie API Mesh in Adobe Commerce und  [!DNL Adobe App Builder]. Erfahren Sie, wie Sie ein Netz mit mehreren Quellen erstellen und einige häufige Fehler beheben.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Architect, Developer
level: Beginner, Intermediate
exl-id: d788a068-9d20-4db0-a0eb-fd897873253d
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '234'
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

>[!VIDEO](https://video.tv.adobe.com/v/3414125?quality=12&learn=on)

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
