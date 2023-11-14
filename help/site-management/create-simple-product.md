---
title: Einfaches Produkt erstellen
description: Erfahren Sie, wie Sie ein einfaches Produkt mit der REST-API und dem Commerce-Administrator erstellen.
kt: 14446
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-11-13T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
source-git-commit: 9f5d0e83995d12b5884c53fc8bcb0e9d1913768e
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Einfaches Produkt erstellen

Erfahren Sie, wie Sie ein einfaches Produkt mit der REST-API und dem Commerce-Administrator erstellen.

## Für wen ist dieses Video?

- Website-Manager
- eCommerce-Merchandiser
- Neue Entwickler für Adobe Commerce, die lernen müssen, wie REST zum Erstellen eines Produkts in Adobe Commerce verwendet wird

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3425650?learn=on)

## Curl-Codebeispiel zum Erstellen eines Produkts

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

## Beispiel für einen Curl-Code zum Abrufen eines Produkts

```bash
curl --location '{{your.url.here}}rest/default/V1/products/some-product-sku' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=3b797a6cc3c5c71f2193109fb9838b12'
```

## Zusätzliche Ressourcen

- [Adobe Developer REST-Tutorials](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [Adobe Commerce REST ReDoc](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
