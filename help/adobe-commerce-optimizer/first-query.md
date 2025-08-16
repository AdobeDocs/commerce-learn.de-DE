---
title: Abfragen von Daten
description: Erfahren Sie, wie Sie Daten für eine Adobe Commerce Optimizer-Instanz abfragen.
feature: Saas, Storefront
topic: Commerce
role: Developer
level: Beginner
doc-type: Tutorial
duration: 182
last-substantial-update: 2025-08-13T00:00:00Z
jira: KT-18548
source-git-commit: c598e46f7119ebdb1575e41c65d6285109fd9af9
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Abfragen von Daten in Adobe Commerce Optimizer

Erfahren Sie, wie Sie Daten mit GraphQL in einer Adobe Commerce Optimizer-Instanz abfragen.

## Für wen ist dieses Video bestimmt?

* Commerce-Lösungsarchitekt und -entwickler

## Videoinhalt

* Abfragen von Daten mit GraphQL
* Verwenden von JQ, um das Lesen von JSON zu vereinfachen

>[!VIDEO](https://video.tv.adobe.com/v/3470809?learn=on&enablevpops&captions=ger)

## Code-Beispiele

Tauschen Sie unbedingt Werte wie `{{insert-your-graphql-endpoint-url}}`, `{{insert-your-ac-source-locale}}` und `{{your-search-query-string}}` mit den Werten aus, die für Ihre Abfrage benötigt werden.

Einfache Beispielabfrage

```bash
curl '{{insert-your-graphql-endpoint-url}}' \
-H 'Content-Type: application/json' \
-H 'AC-Source-Locale: {{insert-your-ac-source-locale}}' \
-d '{"query": "query ProductSearch($search: String!) { productSearch( phrase: $search, page_size: 10, current_page: 2) { items { productView { sku name description shortDescription images { url } ... on SimpleProductView { attributes { label name value } price { regular { amount { value currency } } roles } } } } } }", "variables": { "search": "{{your-search-query-string}}"}}'
```

Einfache Beispielabfrage mit `jq` zum hübschen Drucken der Ausgabe

```bash
curl '{{insert-your-graphql-endpoint-url}}' \
-H 'Content-Type: application/json' \
-H 'AC-Source-Locale: {{insert-your-ac-source-locale}}' \
-d '{"query": "query ProductSearch($search: String!) { productSearch( phrase: $search, page_size: 10, current_page: 2) { items { productView { sku name description shortDescription images { url } ... on SimpleProductView { attributes { label name value } price { regular { amount { value currency } } roles } } } } } }", "variables": { "search": "{{your-search-query-string}}"}}' | jq .
```

## Verwandte Inhalte

* [Erste Schritte mit der Merchandising-API](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api/#make-your-first-request){target="_blank"}
* [[!DNL Adobe Commerce Optimizer] Anleitung](https://experienceleague.adobe.com/de/docs/commerce/optimizer/overview){target="_blank"}
