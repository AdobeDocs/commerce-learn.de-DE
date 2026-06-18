---
title: Erstellen eines GraphQL-Mesh aus einer Quelle in API-Mesh
description: Erfahren Sie, wie Sie API Mesh in Adobe Commerce und Adobe App Builder verwenden. Erfahren Sie, wie Sie ein Netz mit einer einzigen GraphQL-Quelle erstellen und auf den neuen Endpunkt zugreifen.
jira: KT-11804
doc-type: Tutorial
duration: 485
last-substantial-update: 2023-02-08T00:00:00Z
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Developer
level: Beginner
exl-id: 9a78457a-1539-49c0-ac69-4bbfc6786137
source-git-commit: c73744d503de5023e5c001d0534200522db55b04
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Erstellen eines Netzes mit einer einzigen Quelle

In diesem Video erfahren Entwicklerinnen und Entwickler, wie sie ein Netz mit einer einzigen Quelle in API Mesh für Adobe Developer App Builder erstellen. Damit dieses einfache Beispiel funktioniert, benötigen Sie eine öffentlich zugängliche API oder einen GraphQL-Endpunkt. In diesem Video wird auch erläutert, wie Sie eine einfache `mesh.json` erstellen, die mit Ihrer Commerce-Instanz verwendet werden kann. Weitere Informationen und Codebeispiele finden Sie unter [Erstellen eines Netzes](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh){target="_blank"}.

## Für wen ist dieses Video bestimmt?

* Jeder, der mit API Mesh noch nicht vertraut ist
* Entwickler, die mehrere GraphQL- und API-Quellen kombinieren möchten
* Alle, die wissen müssen, wie man die Registerkarte Netzwerk filtert und nach GraphQL filtert

## Videoinhalt

* Verwenden von API Mesh als Reverse-Proxy
* Erstellen eines Netzes aus einer JSON-Konfigurationsdatei
* Zugreifen auf den neu erstellten GraphQL-Endpunkt

>[!VIDEO](https://video.tv.adobe.com/v/3430825?captions=ger&learn=on)

## Erstellen der JSON-Konfigurationsdatei

API Mesh verwendet eine JSON-Konfigurationsdatei, um Ihre Quell-Handler zu definieren. Die JSON-Datei enthält ein `sources`-Array, das die Quellen für Ihr Netz enthält. Im Folgenden finden Sie ein Beispiel für ein Netz mit einer einzigen Quelle.

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
