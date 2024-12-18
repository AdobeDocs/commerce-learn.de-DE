---
title: Durchführen einer Mutation mit GraphQL
description: Erhalten Sie eine Einführung in die Durchführung einer Mutation mit GraphQL in Adobe Commerce und  [!DNL Magento Open Source]. Führen Sie Ihre erste Mutation mithilfe von POST-Aufrufen durch.
landing-page-description: Erhalten Sie eine Einführung in die Durchführung einer Mutation mit GraphQL in Adobe Commerce und  [!DNL Magento Open Source]. Führen Sie Ihre erste Mutation mithilfe von POST-Aufrufen durch.
short-description: Erhalten Sie eine Einführung in die Durchführung einer Mutation mit GraphQL in Adobe Commerce und  [!DNL Magento Open Source]. Führen Sie Ihre erste Mutation mithilfe von POST-Aufrufen durch.
kt: 13938
doc-type: video
audience: all
last-substantial-update: 2023-10-12T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 6b82ffda-925f-4a81-8ca5-49a2b8ab4929
source-git-commit: 2041bbf1a2783975091b9806c12fc3c34c34582f
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Mutationen

Dies ist Teil 3 der Serie für GraphQL und Adobe Commerce. Mutationen sind die Möglichkeit, Werte mithilfe von GraphQL zu speichern, zu aktualisieren und zurückzugeben.


>[!VIDEO](https://video.tv.adobe.com/v/3424121?learn=on)

## Verwandte Videos und Tutorials zu GraphQL in dieser Reihe

* [Teil 1: GraphQL - Einführung](../graphql-rest/intro-graphql.md)
* [Teil 2: GraphQL - Abfragen](../graphql-rest/graphql-queries.md)
* [Teil 4: GraphQL - Schema](../graphql-rest/graphql-schema.md)

## Beispielmutation

Jede vollständige API-Spezifikation muss die Möglichkeit bieten, Daten nicht nur abzufragen, sondern auch zu erstellen und zu aktualisieren.

REST unterscheidet zwischen Anfragen, die Daten ändern, und solchen, die nicht mit dem Anfragetyp oder „Verb“ (GET vs. POST oder PUT) übereinstimmen.
Bei Verwendung von GraphQL werden datenmodifizierende Abfragen durch das `mutation`-Schlüsselwort unterschieden, das einem anderen entspricht
Stammentyp im auf dem Server definierten Schema.

Sehen Sie sich diese Beispielmutation für das Hinzufügen eines Produkts zum Warenkorb eines Benutzers an. (Dies erfordert eine generierte Warenkorb-ID
für die Sitzung des angemeldeten Kunden oder unter Verwendung der `createEmptyCart` Mutation)

```graphql
mutation doAddToCart(
    $cartId: String!,
    $cartItems: [CartItemInput!]!
) {
    addProductsToCart(
        cartId: $cartId
        cartItems: $cartItems
    ) {
        cart {
            total_quantity
            prices {
                grand_total {
                    value
                }
            }
        }
    }
}
```

Sie können sich vorstellen, dass die obige Mutation in einer Anfrage zusammen mit den folgenden Wörterbuchvariablen gesendet wird:

```json
{
  "cartId": "{cart-id}",
  "cartItems": [
    {
      "quantity": 1,
      "sku": "VT01-RN-XS"
    }
  ]
}
```

Und schließlich erhalten Sie möglicherweise eine Antwort wie die folgende:

```json
{
  "data": {
    "addProductsToCart": {
      "cart": {
        "total_quantity": 1,
        "prices": {
          "grand_total": {
            "value": 35.2
          }
        }
      }
    }
  }
}
```

Im Hinblick auf das obige Beispiel ist Folgendes am wichtigsten: Abgesehen von der Verwendung des `mutation`-Schlüsselworts anstelle von `query`
Die Syntax ist identisch mit der einer Abfrage. Wie Abfragen umfasst die Mutation:

* Ein beliebiger Vorgangsname (`doAddToCart`)
* Eine Liste von Variablen (z. B. `$cartId`)
* Ein anfängliches Feld (`addProductsToCart`) mit Argumenten (z. B. `cartId`, die auf den Wert von `$cartId` gesetzt sind) in Klammern
* Eine Unterauswahl von Feldern in geschweiften Klammern

Mit der Unterauswahl „Felder“ können Sie flexibel die Felder definieren, die Sie zurückgeben möchten (vom Typ , der als zugewiesen wurde).
Rückgabewert von `addProductsToCart` - `AddProductsToCartOutput`), nachdem die Mutation abgeschlossen ist.

Wie bereits erläutert, beginnen in einem GraphQL-Schema definierte Felder in einem Stammtyp für Abfragen (in der Regel als `Query` bezeichnet). Ähnlich gilt
Für Mutationen gibt es einen anderen Stammentyp (in der Regel als `Mutation` bezeichnet). `addProductsToCart` ist ein Feld
über diesen Stammentyp.

Einige weitere Hinweise zum obigen Beispiel:

* Das `!` Zeichen, das `String` und `CartItemInput` Suffix angibt, dass die Variable erforderlich ist.
* Die eckigen Klammern (`[]`) um den für `$cartItems` angegebenen `CartItemInput` geben eine Liste an
von diesem Typ statt eines einzelnen Werts.

{{$include /help/_includes/graphql-rest-related-links.md}}
