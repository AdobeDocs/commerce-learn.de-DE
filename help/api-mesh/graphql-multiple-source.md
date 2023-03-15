---
title: Erstellen einer GraphQL mit mehreren Quellen zur Verwendung im API-Mesh
description: Erfahren Sie, wie Sie mehrere Quellen für das API-Mesh in Adobe Commerce verwenden und [!DNL Adobe App Builder]. Erfahren Sie mehr über einige häufige Fehler und wie Sie diese beheben können.
landing-page-description: Erfahren Sie, wie Sie API-Mesh in Adobe Commerce verwenden und [!DNL Adobe App Builder]. Erfahren Sie, wie Sie ein Gitter mit mehreren Quellen erstellen und einige häufige Fehler beheben können.
short-description: Discover how to use API Mesh on Adobe Commerce and [!DNL Adobe App Builder]. Learn about creating a mesh that has multiple sources and how to resolve some common errors.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
source-git-commit: 67d21ca23cdccc87cdeed4a08a3ebb48e5bd1030
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Erstellen eines Netzwerks mit mehreren Quellen

In diesem Video erfahren Entwickler, wie ein Gitter mit mehreren Quellen im API-Mesh für Adobe Developer App Builder erstellt wird. In diesem Video erfahren Sie, wie Sie ein Gitter mit mehreren Quellen erstellen und Fehler identifizieren. Weitere Informationen und Codebeispiele finden Sie unter [Erstellen eines Gitters](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1){target="_blank"}.

## Für wen ist dieses Video?

* Jeder, der neu für das API-Gitter ist
* Entwickler, die mehrere API- und GraphQL-Quellen kombinieren möchten

## Videoinhalt

* Verwendung [Transformationen](https://developer.adobe.com/graphql-mesh-gateway/gateway/transforms/){target="_blank"} Ändern des Standardquellschemas
* Beheben von Fehlern, wie Namenskonflikten, Schemaverfügbarkeit und andere Probleme mit der Schemasyntax
* Aktualisieren Ihres Netzwerks mit einer geänderten Konfiguration

>[!VIDEO](https://video.tv.adobe.com/v/3414125)

## JSON-Konfigurationsdatei erstellen

API-Mesh verwendet eine JSON-Konfigurationsdatei, um Ihre Quell-Handler zu definieren. Die JSON-Datei enthält eine `sources` -Array, das die Quellen für Ihr Gitter enthält. Im Folgenden finden Sie ein Beispiel für ein Gitter mit mehreren Quellen.

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
