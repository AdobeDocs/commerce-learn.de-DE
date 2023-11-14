---
title: Einfaches Produkt erstellen
description: Erfahren Sie, wie Sie ein einfaches Produkt mit der REST-API und dem Commerce Admin erstellen.
kt: 14446
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-11-14T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
source-git-commit: 89dc3b7f456c9434921ed870369712a721895d02
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# Einfaches Produkt erstellen

Erfahren Sie, wie Sie ein einfaches Produkt mit der REST-API und dem Adobe Commerce-Administrator erstellen.

## Für wen ist dieses Video?

- Website-Manager
- eCommerce-Merchandiser
- Neue Adobe Commerce-Entwickler, die lernen möchten, wie Produkte in Adobe Commerce mithilfe der REST-API erstellt werden.

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3425650?learn=on)

## Produkt mit curl erstellen

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=a42da0096288718c9556f77549c6305f; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "some-product-sku",
    "name": "My curl created product test",
    "attribute_set_id": 4,
    "price": 222,
    "type_id": "simple"
  }
}
```

## Produkt mit curl abrufen

```bash
curl --location '{{your.url.here}}rest/default/V1/products/some-product-sku' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=3b797a6cc3c5c71f2193109fb9838b12'
```

## Zusätzliche Ressourcen

- [Adobe Developer REST-Tutorials](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [Adobe Commerce REST ReDoc](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
