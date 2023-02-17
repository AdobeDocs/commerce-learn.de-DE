---
title: Erstellen eines GraphQL-Single-Source-Netzwerks in API Mesh
description: Erfahren Sie, wie Sie API-Mesh in Adobe Commerce verwenden und [!DNL Adobe App Builder]. Erfahren Sie mehr über das Erstellen eines Gitters mit einer Quelle.
landing-page-description: Erfahren Sie, wie Sie API-Mesh in Adobe Commerce verwenden und [!DNL Adobe App Builder]. Erfahren Sie mehr über das Erstellen eines Gitters mit einer Quelle.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
source-git-commit: 2cf7eb4d04f874ec42ca5f6d58ec841680376a41
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Erstellen eines Netzwerks mit einer einzigen Quelle

In diesem Video erfahren Entwickler, wie ein Gitter mit einer einzigen Quelle im API-Mesh für Adobe Developer App Builder erstellt wird. Damit dieses grundlegende Beispiel erwartungsgemäß funktioniert, benötigen Sie eine öffentlich zugängliche API oder einen GraphQL-Endpunkt. In diesem Video wird auch erläutert, wie eine einfache `mesh.json` -Datei, die mit Ihrer Commerce-Instanz verwendet werden soll. Weitere Informationen und Codebeispiele finden Sie unter [Erstellen eines Gitters](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1).

## Für wen ist dieses Video?

* Jeder, der neu in API-Mesh ist
* Entwickler, die mehrere GraphQL- und API-Quellen kombinieren möchten
* Jeder, der wissen muss, wie die Registerkarte &quot;Netzwerk&quot;gefiltert und nach GraphQL gefiltert werden soll

## Videoinhalt

* Verwenden des API-Gitters als Reverse-Proxy
* Erstellen eines Gitters aus einer JSON-Konfigurationsdatei
* Zugriff auf den neu erstellten GraphQL-Endpunkt

>[!VIDEO](https://video.tv.adobe.com/v/3414124)

## JSON-Konfigurationsdatei erstellen

API-Mesh verwendet eine JSON-Konfigurationsdatei, um Ihre Quell-Handler zu definieren. Die JSON-Datei enthält eine `sources` -Array, das die Quellen für Ihr Gitter enthält. Im Folgenden finden Sie ein Beispiel für ein Gitter mit einer einzigen Quelle.

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
      }
    ]
  }
}
```

{{$include /help/_includes/api-mesh-related-links.md}}