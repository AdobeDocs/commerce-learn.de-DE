---
title: Erstellen eines GraphQL-Single-Source-Netzwerks in API Mesh
description: Erfahren Sie, wie Sie API-Mesh in Adobe Commerce und  [!DNL Adobe App Builder] verwenden. Erfahren Sie mehr über das Erstellen eines Gitters mit einer Quelle.
landing-page-description: Erfahren Sie, wie Sie API-Mesh in Adobe Commerce und  [!DNL Adobe App Builder] verwenden. Erfahren Sie mehr über das Erstellen eines Gitters mit einer Quelle.
short-description: Erfahren Sie, wie Sie API-Mesh in Adobe Commerce und  [!DNL Adobe App Builder] verwenden. Erfahren Sie mehr über das Erstellen eines Gitters mit einer Quelle.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 9a78457a-1539-49c0-ac69-4bbfc6786137
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Erstellen eines Netzwerks mit einer einzigen Quelle

In diesem Video erfahren Entwickler, wie ein Gitter mit einer einzigen Quelle im API-Mesh für Adobe Developer App Builder erstellt wird. Damit dieses grundlegende Beispiel erwartungsgemäß funktioniert, benötigen Sie eine öffentlich zugängliche API oder einen GraphQL-Endpunkt. In diesem Video wird auch erläutert, wie Sie eine einfache `mesh.json` -Datei erstellen, die mit Ihrer Commerce-Instanz verwendet werden kann. Weitere Informationen und Codebeispiele finden Sie unter [Ein Gitter erstellen](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1){target="_blank"}.

## Für wen ist dieses Video?

* Jeder, der neu in API-Mesh ist
* Entwickler, die mehrere GraphQL- und API-Quellen kombinieren möchten
* Jeder, der wissen muss, wie die Registerkarte &quot;Netzwerk&quot;gefiltert und nach GraphQL gefiltert werden soll

## Videoinhalt

* Verwenden des API-Gitters als Reverse-Proxy
* Erstellen eines Gitters aus einer JSON-Konfigurationsdatei
* Zugriff auf den neu erstellten GraphQL-Endpunkt

>[!VIDEO](https://video.tv.adobe.com/v/3414124?quality=12&learn=on)

## JSON-Konfigurationsdatei erstellen

API-Mesh verwendet eine JSON-Konfigurationsdatei, um Ihre Quell-Handler zu definieren. Die JSON-Datei enthält ein `sources` -Array, das die Quellen für Ihr Gitter enthält. Im Folgenden finden Sie ein Beispiel für ein Gitter mit einer einzigen Quelle.

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
