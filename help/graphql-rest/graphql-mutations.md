---
title: Durchführen einer Mutation mit GraphQL
description: Hier erhalten Sie eine Einführung in die Durchführung einer Mutation mit GraphQL in Adobe Commerce und [!DNL Magento Open Source]. Führen Sie Ihre erste Mutation mithilfe von POST-Aufrufen durch.
landing-page-description: Hier erhalten Sie eine Einführung in die Durchführung einer Mutation mit GraphQL in Adobe Commerce und [!DNL Magento Open Source]. Führen Sie Ihre erste Mutation mithilfe von POST-Aufrufen durch.
short-description: Hier erhalten Sie eine Einführung in die Durchführung einer Mutation mit GraphQL in Adobe Commerce und [!DNL Magento Open Source]. Führen Sie Ihre erste Mutation mithilfe von POST-Aufrufen durch.
kt: 11524
doc-type: tutorial
audience: all
last-substantial-update: 2022-12-13T00:00:00Z
exl-id: 6b82ffda-925f-4a81-8ca5-49a2b8ab4929
source-git-commit: 67d21ca23cdccc87cdeed4a08a3ebb48e5bd1030
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Mutationen

Jede vollständige API-Spezifikation muss die Möglichkeit bieten, Daten nicht nur abzufragen, sondern auch zu erstellen und zu aktualisieren.

REST unterscheidet zwischen Anforderungen, die Daten ändern, und Anforderungen, die nicht mit dem Anfragetyp oder &quot;Verb&quot;(GET vs. POST oder PUT) übereinstimmen.
Bei Verwendung von GraphQL werden datenmodifizierte Abfragen durch die `mutation` -Keyword, das einem anderen Stammtyp im Schema entspricht, das auf dem Server definiert ist.

Sehen Sie sich diese Beispiel-Mutation an, um einem Benutzer ein Produkt zum Warenkorb hinzuzufügen. (Hierfür ist eine Warenkorb-ID erforderlich, die für die Sitzung des angemeldeten Kunden oder unter Verwendung der Variablen `createEmptyCart` Mutation.)

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

Sie können sich vorstellen, dass die oben genannte Mutation in einer Anfrage zusammen mit dem folgenden Variablenwörterbuch gesendet wird:

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

Und schließlich könnten Sie eine Antwort wie die folgende erhalten:

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

Beachten Sie vor allem, dass im oben genannten Beispiel neben der Verwendung des `mutation` anstelle von `query`, ist die Syntax mit einer Abfrage identisch. Wie bei Abfragen umfasst die Mutation:

* Ein beliebiger Vorgangsname (`doAddToCart`)
* Eine Liste von Variablen (z. B. `$cartId`)
* Ein anfängliches Feld (`addProductsToCart`) mit Argumenten (z. B. `cartId`, auf den Wert von `$cartId`) in Klammern
* Eine Unterauswahl von Feldern in geschweiften Klammern

Die Teilauswahl der Felder ermöglicht es, die Felder, die Sie zurückgeben möchten, flexibel zu definieren (aus dem Typ, der als Rückgabewert von `addProductsToCart` - `AddProductsToCartOutput`), nachdem die Mutation abgeschlossen ist.

Wie bereits erläutert, beginnen in einem GraphQL-Schema definierte Felder bei Abfragen mit einem Stammtyp (in der Regel als `Query`). Ähnlich gibt es auch einen anderen Stammtyp für Mutationen (in der Regel als `Mutation`). `addProductsToCart` ist ein Feld dieses Stammtyps.

Einige weitere Hinweise zum obigen Beispiel:

* Die `!` Zeichensuffic `String` und `CartItemInput` gibt an, dass die Variable erforderlich ist.
* Die eckigen Klammern (`[]`) um die `CartItemInput` Typ, der für `$cartItems` eine Liste dieses Typs anstelle eines einzelnen Werts angeben.

{{$include /help/_includes/graphql-rest-related-links.md}}
