---
title: Durchführen einer Mutation mit GraphQL
description: Hier erhalten Sie eine Einführung in die Durchführung einer Mutation mit GraphQL unter Adobe Commerce und  [!DNL Magento Open Source]. Führen Sie Ihre erste Mutation mithilfe von POST-Aufrufen durch.
landing-page-description: Hier erhalten Sie eine Einführung in die Durchführung einer Mutation mit GraphQL unter Adobe Commerce und  [!DNL Magento Open Source]. Führen Sie Ihre erste Mutation mithilfe von POST-Aufrufen durch.
short-description: Hier erhalten Sie eine Einführung in die Durchführung einer Mutation mit GraphQL unter Adobe Commerce und  [!DNL Magento Open Source]. Führen Sie Ihre erste Mutation mithilfe von POST-Aufrufen durch.
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

Dies ist Teil 3 der Reihe für GraphQL und Adobe Commerce. Mutationen ermöglichen das Speichern, Aktualisieren und Zurückgeben von Werten mithilfe von GraphQL.


>[!VIDEO](https://video.tv.adobe.com/v/3424121?learn=on)

## Verwandte Videos und Tutorials zu GraphQL in dieser Reihe

* [Teil 1 GraphQL - Einführung](../graphql-rest/intro-graphql.md)
* [Teil 2 GraphQL - Abfragen](../graphql-rest/graphql-queries.md)
* [Teil 4 GraphQL - Schema](../graphql-rest/graphql-schema.md)

## Beispiel-Mutation

Jede vollständige API-Spezifikation muss die Möglichkeit bieten, Daten nicht nur abzufragen, sondern auch zu erstellen und zu aktualisieren.

REST unterscheidet zwischen Anforderungen, die Daten ändern, und Anforderungen, die nicht mit dem Anfragetyp oder &quot;Verb&quot;(GET vs. POST oder PUT) übereinstimmen.
Bei Verwendung von GraphQL werden datenmodifizierte Abfragen durch das Schlüsselwort `mutation` gekennzeichnet, das einem anderen
Stammtyp im Schema, das auf dem Server definiert ist.

Sehen Sie sich diese Beispiel-Mutation an, um einem Benutzer ein Produkt zum Warenkorb hinzuzufügen. (Dies erfordert eine generierte Warenkorb-ID.
für die Sitzung des angemeldeten Kunden oder die Verwendung der `createEmptyCart` -Mutation.)

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

Beachten Sie vor allem, dass im oben gezeigten Beispiel abgesehen von der Verwendung des Schlüsselworts `mutation` anstelle von `query`,
die Syntax mit einer Abfrage identisch ist. Wie bei Abfragen umfasst die Mutation:

* Ein beliebiger Vorgangsname (`doAddToCart`)
* Eine Liste von Variablen (z. B. `$cartId`)
* Ein anfängliches Feld (`addProductsToCart`) mit Argumenten (z. B. `cartId`, festgelegt auf den Wert von `$cartId`) in Klammern
* Eine Unterauswahl von Feldern in geschweiften Klammern

Die Teilauswahl der Felder ermöglicht es, die Felder, die Sie zurückgeben möchten, flexibel zu definieren (ausgehend vom Typ, der als
Rückgabewert von `addProductsToCart` - `AddProductsToCartOutput`) nach Abschluss der Mutation.

Wie bereits erläutert, beginnen in einem GraphQL-Schema definierte Felder bei Abfragen mit einem Stammtyp (normalerweise als `Query` bezeichnet). Ebenso
Ein anderer Stammtyp ist für Mutationen vorhanden (normalerweise als `Mutation` bezeichnet). `addProductsToCart` ist ein Feld
auf diesem Stammtyp.

Einige weitere Hinweise zum obigen Beispiel:

* Das Suffix `!` -Zeichen `String` und `CartItemInput` zeigt an, dass die Variable erforderlich ist.
* Die eckigen Klammern (`[]`) um den für `$cartItems` angegebenen `CartItemInput`-Typ geben eine Liste an
diesen Typ anstelle eines einzelnen Werts verwenden.

{{$include /help/_includes/graphql-rest-related-links.md}}
