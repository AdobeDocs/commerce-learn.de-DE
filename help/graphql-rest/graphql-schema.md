---
title: Schemasprache mit GraphQL
description: Erfahren Sie mehr über das mit GraphQL verbundene Schema. Lesen Sie eine Beschreibung des Schemas sowie einige interessante Muster und Möglichkeiten, das Schema zu lesen.
landing-page-description: Dies ist eine Einführung in GraphQL. Grundlegendes zum Schema und zur Interpretation einiger Elemente
short-description: Dies ist eine Einführung in GraphQL. Grundlegendes zum Schema und zur Interpretation einiger Elemente
kt: 11524
doc-type: tutorial
audience: all
last-substantial-update: 2022-12-13T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 6b59db07-b99e-47ae-9ccb-d4904afc8251
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Schemasprache

Die verwendeten Abfragen und Mutationen basieren auf einem bestimmten Datendiagramm, das auf dem Server implementiert wird, den die GraphQL-Laufzeitumgebung zur Auflösung der Abfrage nutzt. Die GraphQL-Spezifikation definiert eine agnostische Sprache zum Ausdrücken der Typen und Beziehungen Ihres Datendiagramms.

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

Sie können sich näher mit [die Dokumentation zu GraphQL](https://graphql.org/learn/schema/){target="_blank"} , um mehr über die Details des Typsystems zu erfahren, einschließlich der Syntax für einige Konzepte, die hier nicht dargestellt werden. Das obige Beispiel ist jedoch selbsterklärend. (Beachten Sie außerdem, wie ähnlich die Syntax der Abfragesyntax ist.) Die Definition eines GraphQL-Schemas dient lediglich dazu, die verfügbaren Argumente und Felder eines bestimmten Typs sowie die Typen dieser Felder auszudrücken. Jeder komplexe Feldtyp muss selbst eine Definition haben usw. durch die Struktur, bis Sie zu einfachen Skalartypen wie `String`.

Die `input` Erklärung gleicht in jeder Hinsicht einer `type` definiert jedoch einen Typ, der als Eingabe für ein Argument verwendet werden kann. Beachten Sie auch die `interface` Erklärung. Dies dient mehr oder weniger der gleichen Funktion wie Schnittstellen in PHP. Andere Typen erben von dieser Schnittstelle.

Die Syntax `[CartItemInput!]!` schaut schwierig aus, ist aber am Ende ziemlich intuitiv. Die `!` _inside_ Die Klammer deklariert, dass jeder Wert im Array ungleich null sein muss, während der Wert _outside_ gibt an, dass der Array-Wert selbst nicht null sein muss (z. B. ein leeres Array).

>[!NOTE]
>
>Die Logik, wie Daten gemäß einem Schema abgerufen und formatiert werden und wie diese Logik bestimmten Typen zugeordnet wird, liegt bei der GraphQL-Laufzeitimplementierung. Implementierungen sollten jedoch einem konzeptionellen Ablauf folgen, der im Hinblick auf ein Verständnis um verschachtelte Felder sinnvoll ist: einem Auflösungsvorgang, der mit der Stamm-Node verknüpft ist `Query` oder `Mutation` -Typ durchgeführt wird, der jedes in der Anfrage angegebene Feld prüft. Für jedes Feld, das zu einem komplexen Typ aufgelöst wird, wird eine ähnliche Auflösung für diesen Typ durchgeführt usw., bis alles in skalare Werte aufgelöst wurde.

{{$include /help/_includes/graphql-rest-related-links.md}}
