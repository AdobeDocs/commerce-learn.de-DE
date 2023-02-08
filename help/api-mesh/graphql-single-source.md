---
title: Erstellen einer GraphQL-Einzelquellenanforderung zur Verwendung im API-Mesh
description: Erfahren Sie, wie Sie API-Mesh in Adobe Commerce verwenden und [!DNL Adobe App Builder]. Erfahren Sie mehr über das Erstellen einer Anfrage mit einer Quelle.
landing-page-description: Erfahren Sie, wie Sie API-Mesh in Adobe Commerce verwenden und [!DNL Adobe App Builder]. Erfahren Sie mehr über das Erstellen einer Anfrage mit einer Quelle.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
source-git-commit: b6d501c5c852e1cc2cf1f05f91b5a9d96ac7d036
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# GraphQL API-Gitter für eine Quelle erstellen

Das Video hilft Entwicklern dabei, zu verstehen, wie ein Reverse-Proxy von GraphQL erstellt wird und über eine einzige Quelle verfügt. Beachten Sie, dass eine öffentlich zugängliche URL mit einem gültigen GraphQL-Schema erforderlich ist, damit GraphQL Mesh erwartungsgemäß funktioniert. In diesem Video wird auch erläutert, wie Sie Ihre erste JSON-Datei für die Verwendung mit Ihrer Commerce-Website einrichten. Grundlegende Codebeispiele, die im Video verwendet wurden, finden Sie unter [Erstellen eines Gitters](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1).

## Für wen ist dieses Video?

* Jeder, der neu für das API-Gitter ist
* Entwickler, die mehrere grafische Quellen verwenden möchten
* Jeder, der wissen muss, wie die Registerkarte &quot;Netzwerk&quot;gefiltert und nach Grafik gefiltert werden soll

## Videoinhalt

* Verwenden der API als Reverse-Proxy
* JSON-Konfiguration mit der Befehlszeilenschnittstelle von Adobe Developer
* Zugriff auf den neu erstellten GraphQL-Endpunkt

>[!VIDEO](https://video.tv.adobe.com/v/3414124)

## JSON-Konfigurationsdatei erstellen

Damit Adobe App Builder von all Ihren Quellen erfahren kann, definieren Sie sie in einer JSON-Konfiguration. Jede Quelle ist ein Element in einem Array und Sie können eine oder mehrere haben. Im Folgenden finden Sie ein Beispiel für eine einzelne Quelle

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
