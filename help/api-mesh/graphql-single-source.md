---
title: Erstellen eines GraphQL-Mesh aus einer Quelle in API-Mesh
description: Erfahren Sie, wie Sie API Mesh in Adobe Commerce und Adobe App Builder verwenden. Erfahren Sie, wie Sie ein Netz mit einer einzigen GraphQL-Quelle erstellen und auf den neuen Endpunkt zugreifen.
jira: KT-11804
doc-type: Tutorial
duration: 485
last-substantial-update: 2023-02-08T00:00:00.000Z
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Developer
level: Beginner
exl-id: 9a78457a-1539-49c0-ac69-4bbfc6786137
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: b48dbafb-4193-5648-b9d9-bf96e9c9a411
    internal-label: Backend Development
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
subfeature_v2:
  - id: ce84ce08-883f-4337-ae83-6bb1855ca732
    internal-label: API Mesh
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
  - id: 618ab558-d6ad-5352-99d6-d5702c6fdf80
    internal-label: Tools and External Services
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
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

>[!VIDEO](https://video.tv.adobe.com/v/3414124?learn=on)

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
