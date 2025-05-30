---
title: Einfaches Produkt erstellen
description: Erfahren Sie, wie Sie mit der REST-API und Commerce Admin ein einfaches Produkt erstellen können.
kt: 14446
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-11-14T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
exl-id: 62ba8e71-dcff-4c72-8850-029be2c42620
source-git-commit: a9712c4354967e8e53c421878be8b83bb6056e6d
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Einfaches Produkt erstellen

Erfahren Sie, wie Sie mit der REST-API und Adobe Commerce Admin ein einfaches Produkt erstellen können.

## Für wen ist dieses Video bestimmt?

- Website-Manager
- E-Commerce-Merchandiser
- Neue Adobe Commerce-Entwicklerinnen und -Entwickler, die lernen möchten, wie Produkte in Adobe Commerce mithilfe der REST-API erstellt werden.

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3443911?learn=on&captions=ger)

## Erstellen eines Produkts mithilfe von cURL

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

## Abrufen eines Produkts mithilfe von cURL

```bash
curl --location '{{your.url.here}}rest/default/V1/products/some-product-sku' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=3b797a6cc3c5c71f2193109fb9838b12'
```

## Zusätzliche Ressourcen

- [Adobe Developer-REST-Tutorials](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [Adobe Commerce-REST-Überprüfung](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
