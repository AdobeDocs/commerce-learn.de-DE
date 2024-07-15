---
title: Schemasprache mit GraphQL
description: Erfahren Sie mehr über das mit GraphQL verbundene Schema. Lesen Sie eine Beschreibung des Schemas sowie einige interessante Muster und Möglichkeiten, das Schema zu lesen.
landing-page-description: Dies ist eine Einführung in GraphQL. Grundlegendes zum Schema und zur Interpretation einiger Elemente
short-description: Dies ist eine Einführung in GraphQL. Grundlegendes zum Schema und zur Interpretation einiger Elemente
kt: 13939
doc-type: video
audience: all
last-substantial-update: 2023-10-12T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 6b59db07-b99e-47ae-9ccb-d4904afc8251
source-git-commit: 2041bbf1a2783975091b9806c12fc3c34c34582f
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Schemasprache

Dies ist Teil 4 der Reihe für GraphQL und Adobe Commerce. Die verwendeten Abfragen und Mutationen basieren auf einem bestimmten Datendiagramm, das auf dem Server implementiert wird, den die GraphQL-Laufzeitumgebung zur Auflösung der Abfrage nutzt. Die GraphQL-Spezifikation definiert eine agnostische Sprache zum Ausdrücken der Typen und Beziehungen Ihres Datendiagramms.

>[!VIDEO](https://video.tv.adobe.com/v/3424123?learn=on)

## Verwandte Videos und Tutorials zu GraphQL in dieser Reihe

* [Teil 1 GraphQL - Einführung](../graphql-rest/intro-graphql.md)
* [Teil 2 GraphQL - Abfragen](../graphql-rest/graphql-queries.md)
* [Teil 3 GraphQL - Mutationen](../graphql-rest/graphql-mutations.md)

## Beispielschema

Im Folgenden finden Sie ein abgekürztes Typschema, das die Abfragen und Mutationen unterstützt, die Sie bisher betrachtet haben:

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

Sie können sich [die GraphQL-Dokumentation](https://graphql.org/learn/schema/){target="_blank"} ansehen, um mehr über die Details des Typsystems zu erfahren, einschließlich der Syntax für einige Konzepte, die hier nicht dargestellt werden. Das obige Beispiel ist jedoch selbsterklärend. (Beachten Sie außerdem, wie ähnlich die Syntax der Abfragesyntax ist.) Die Definition eines GraphQL-Schemas dient lediglich dazu, die verfügbaren Argumente und Felder eines bestimmten Typs sowie die Typen dieser Felder auszudrücken. Jeder komplexe Feldtyp muss selbst über eine Definition usw. verfügen, bis Sie zu einfachen Skalartypen wie `String` gelangen.

Die `input` -Deklaration ist in jeder Hinsicht wie ein `type`, definiert jedoch einen Typ, der als Eingabe für ein Argument verwendet werden kann. Beachten Sie auch die Deklaration `interface` . Dies dient mehr oder weniger der gleichen Funktion wie Schnittstellen in PHP. Andere Typen erben von dieser Schnittstelle.

Die Syntax `[CartItemInput!]!` sieht schwierig aus, ist aber am Ende ziemlich intuitiv. Die Klammer &quot;`!` _inside_&quot;deklariert, dass jeder Wert im Array nicht null sein muss, während die Klammer &quot;_outside_&quot;angibt, dass der Array-Wert selbst nicht null sein muss (z. B. ein leeres Array).

>[!NOTE]
>
>Die Logik, wie Daten gemäß einem Schema abgerufen und formatiert werden und wie diese Logik bestimmten Typen zugeordnet wird, liegt bei der GraphQL-Laufzeitimplementierung. Implementierungen sollten jedoch einem konzeptionellen Ablauf folgen, der im Hinblick auf ein Verständnis der verschachtelten Felder sinnvoll ist: Es wird ein Auflösungsvorgang ausgeführt, der mit dem Stamm-Typ `Query` oder `Mutation` verknüpft ist und die einzelnen in der Anfrage angegebenen Felder überprüft. Für jedes Feld, das zu einem komplexen Typ aufgelöst wird, wird eine ähnliche Auflösung für diesen Typ durchgeführt usw., bis alles in skalare Werte aufgelöst wurde.

{{$include /help/_includes/graphql-rest-related-links.md}}
