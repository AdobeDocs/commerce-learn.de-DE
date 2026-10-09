---
title: Abfragen von Daten
description: Erfahren Sie, wie Sie Adobe Commerce Optimizer-Produktdaten mit GraphQL abfragen, einschließlich der Formatierung von JSON-Antworten mit JQ und der Struktursuche nach Abfragevariablen.
feature: Saas, Storefront
topic: Commerce
role: Developer
level: Beginner
doc-type: Tutorial
duration: 204
last-substantial-update: 2025-08-13T00:00:00.000Z
jira: KT-18548
exl-id: bad3d926-2952-4bac-b685-adb16f009f8d
autotag-review: '2026-08-11T18:59:22.151Z'
TQID: 'https://experienceleague.adobe.com/IxrS6rwleWgU0-jtwu4hUavQuZesbQ6h5z7zVZR2xCo'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%
---
# Abfragen von Daten in Adobe Commerce Optimizer

Erfahren Sie, wie Sie Daten mit GraphQL in einer Adobe Commerce Optimizer-Instanz abfragen.

## Für wen ist dieses Video bestimmt?

* Commerce-Lösungsarchitekt und -entwickler

## Videoinhalt

* Abfragen von Daten mit GraphQL
* Verwenden von JQ, um das Lesen von JSON zu vereinfachen

>[!VIDEO](https://video.tv.adobe.com/v/3470809?captions=ger&learn=on)

## Code-Beispiele

Tauschen Sie unbedingt Werte wie `{{insert-your-graphql-endpoint-url}}`, `{{insert-your-ac-view-id}}` und `{{your-search-query-string}}` mit den Werten aus, die für Ihre Abfrage benötigt werden.

Einfache Beispielabfrage

```bash
curl '{{insert-your-graphql-endpoint-url}}' \
-H 'Content-Type: application/json' \
-H 'AC-View-ID: {{insert-your-ac-view-id}}' \
-d '{"query": "query ProductSearch($search: String!) { productSearch( phrase: $search, page_size: 10, current_page: 2) { items { productView { sku name description shortDescription images { url } ... on SimpleProductView { attributes { label name value } price { regular { amount { value currency } } roles } } } } } }", "variables": { "search": "{{your-search-query-string}}"}}'
```

Einfache Beispielabfrage mit `jq` zum hübschen Drucken der Ausgabe

```bash
curl '{{insert-your-graphql-endpoint-url}}' \
-H 'Content-Type: application/json' \
-H 'AC-View-ID: {{insert-your-ac-view-id}}' \
-d '{"query": "query ProductSearch($search: String!) { productSearch( phrase: $search, page_size: 10, current_page: 2) { items { productView { sku name description shortDescription images { url } ... on SimpleProductView { attributes { label name value } price { regular { amount { value currency } } roles } } } } } }", "variables": { "search": "{{your-search-query-string}}"}}' | jq .
```

## Verwandte Inhalte

* [Erste Schritte mit der Merchandising-API](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#make-your-first-request){target="_blank"}
* [Handbuch zu [!DNL Adobe Commerce Optimizer]](https://experienceleague.adobe.com/de/docs/commerce/optimizer/overview){target="_blank"}

