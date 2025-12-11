---
title: Schemasprache mit GraphQL
description: Erfahren Sie mehr über das mit GraphQL verknüpfte Schema. Lesen Sie eine Beschreibung des Schemas zusammen mit einigen interessanten Mustern und Möglichkeiten, das Schema zu lesen.
landing-page-description: Dies ist eine Einführung in GraphQL. Grundlegendes zum Schema und zur Interpretation einiger Elemente
short-description: Dies ist eine Einführung in GraphQL. Grundlegendes zum Schema und zur Interpretation einiger Elemente
kt: 13939
doc-type: video
audience: all
last-substantial-update: 2023-10-12T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 6b59db07-b99e-47ae-9ccb-d4904afc8251
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Schemasprache

Dies ist Teil 4 der Serie für GraphQL und Adobe Commerce. Die verwendeten Abfragen und Mutationen basieren auf einem bestimmten Datendiagramm, das auf dem Server implementiert wird und das die GraphQL-Laufzeit nutzt, um die Abfrage aufzulösen. Die GraphQL-Spezifikation definiert eine agnostische Sprache zum Ausdrücken der Typen und Beziehungen Ihres Datendiagramms.

>[!VIDEO](https://video.tv.adobe.com/v/3424123?learn=on)

## Verwandte Videos und Tutorials zu GraphQL in dieser Reihe

* [Teil 1: GraphQL - Einführung](../graphql-rest/intro-graphql.md)
* [Teil 2: GraphQL - Abfragen](../graphql-rest/graphql-queries.md)
* [Teil 3 GraphQL - Mutationen](../graphql-rest/graphql-mutations.md)

## Beispielschema

Im Folgenden finden Sie ein abgekürztes Schema, das die bisher betrachteten Abfragen und Mutationen unterstützt:

```graphql
input FilterMatchTypeInput {
  match: String
}

type Money {
  value: Float
}

type Country {
  id: String
  full_name_english: String
}

interface ProductInterface {
  sku: String
  name: String
  related_products: [ProductInterface]
}

type CategoryFilterInput {
  name: FilterMatchTypeInput
}

type CategoryProducts {
  items: [ProductInterface]
}

type CategoryTree {
  name: String
  products(pageSize: Int, currentPage: Int): CategoryProducts
}

type CategoryResult {
  items: [CategoryTree]
}

type Products {
  items: [ProductInterface]
}

type Query {
  country (id: String): Country
  categories (filters: CategoryFilterInput): CategoryResult
  products (search: String): Products
}

input CartItemInput {
  sku: String!
  quantity: Float!
}

type CartPrices {
  grand_total: Money
}

type Cart {
  prices: CartPrices
  total_quantity: Float!
}

type AddProductsToCartOutput {
  cart: Cart!
}

type Mutation {
  addProductsToCart(cartId: String!, cartItems: [CartItemInput!]!): AddProductsToCartOutput
}
```

In der [Dokumentation zu GraphQL](https://graphql.org/learn/schema/){target="_blank"} erfahren Sie mehr über die Einzelheiten des Typsystems, einschließlich der Syntax für einige hier nicht dargestellte Konzepte. Das obige Beispiel ist jedoch selbsterklärend. (Beachten Sie außerdem, wie ähnlich die Syntax der Abfragesyntax ist.) Bei der Definition eines GraphQL-Schemas geht es einfach darum, die verfügbaren Argumente und Felder eines bestimmten Typs zusammen mit den Typen dieser Felder auszudrücken. Jeder komplexe Feldtyp muss selbst über eine Definition verfügen usw., bis Sie einfache Skalartypen wie `String` erhalten.

Die `input`-Deklaration ist in jeder Hinsicht wie eine `type`, definiert jedoch einen Typ, der als Eingabe für ein Argument verwendet werden kann. Beachten Sie auch die `interface`. Dies dient einer Funktion, die mehr oder weniger den Schnittstellen in PHP entspricht. Andere Typen erben von dieser Schnittstelle.

Die Syntax `[CartItemInput!]!` sieht kompliziert aus, ist am Ende aber ziemlich intuitiv. Die `!` _Innen_ der Klammer deklariert, dass jeder Wert im Array ungleich null sein muss, während die Klammer _Außen_ deklariert, dass der Array-Wert selbst ungleich null sein muss (z. B. ein leeres Array).

>[!NOTE]
>
>Die Logik, wie Daten anhand eines Schemas abgerufen und formatiert werden und wie diese Logik bestimmten Typen zugeordnet wird, hängt von der GraphQL-Laufzeitimplementierung ab. Implementierungen sollten jedoch einem konzeptionellen Fluss folgen, der angesichts eines Verständnisses verschachtelter Felder sinnvoll ist: Es wird ein Auflösungsvorgang im Zusammenhang mit dem `Query` oder `Mutation` durchgeführt, bei dem jedes in der Anfrage angegebene Feld geprüft wird. Für jedes Feld, das zu einem komplexen Typ aufgelöst wird, wird eine ähnliche Auflösung für diesen Typ durchgeführt usw., bis alles in Skalarwerte aufgelöst wurde.

{{$include /help/_includes/graphql-rest-related-links.md}}
