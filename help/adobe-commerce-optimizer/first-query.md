---
title: Abfragen von Daten
description: Erfahren Sie, wie Sie Daten für eine Adobe Commerce Optimizer-Instanz abfragen.
feature: Saas, Storefront
topic: Commerce
role: Developer
level: Beginner
doc-type: Tutorial
duration: 243
last-substantial-update: 2025-08-13T00:00:00.000Z
jira: KT-18548
exl-id: bad3d926-2952-4bac-b685-adb16f009f8d
TQID: https://experienceleague.adobe.com/IxrS6rwleWgU0-jtwu4hUavQuZesbQ6h5z7zVZR2xCo
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 114
ht-degree: 0%

---

# Abfragen von Daten in Adobe Commerce Optimizer

Erfahren Sie, wie Sie Daten mit GraphQL in einer Adobe Commerce Optimizer-Instanz abfragen.

## Für wen ist dieses Video bestimmt?

* Commerce-Lösungsarchitekt und -entwickler

## Videoinhalt

* Abfragen von Daten mit GraphQL
* Verwenden von JQ, um das Lesen von JSON zu vereinfachen

>[!VIDEO](https://video.tv.adobe.com/v/3470800?learn=on)

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

* [Erste Schritte mit der Merchandising-API](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api/#make-your-first-request){target="_blank"}
* [Handbuch zu [!DNL Adobe Commerce Optimizer]](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview){target="_blank"}
