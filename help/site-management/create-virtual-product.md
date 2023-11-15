---
title: Erstellen eines virtuellen Produkts
description: Erfahren Sie, wie Sie ein virtuelles Produkt mit der REST-API und dem Commerce Admin erstellen.
kt: 14464
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-11-15T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
source-git-commit: 225faceffefc31a6205f689933210510dba235d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Erstellen eines virtuellen Produkts

Erfahren Sie, wie Sie ein virtuelles Produkt mit der REST-API und dem Adobe Commerce Admin erstellen.

## Für wen ist dieses Video?

- Website-Manager
- eCommerce-Merchandiser
- Neue Adobe Commerce-Entwickler, die lernen möchten, wie Produkte in Adobe Commerce mithilfe der REST-API erstellt werden.

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3425723?learn=on)

## Erstellen eines virtuellen Produkts mit curl

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=2cd97649bcf4ee5b45b23f8eb940e3a0; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "postman-rest-virtual-product-test",
    "name": "POSTMAN virtual product test",
    "attribute_set_id": 4,
    "price": 44,
    "type_id": "virtual"
  }
}
'
```

## Produkt mit curl abrufen

```bash
curl --location '{{your.url.here}}/rest/default/V1/products/Admin-created-virtual-product' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=2cd97649bcf4ee5b45b23f8eb940e3a0; private_content_version=564dde2976849891583a9a649073f01e'
```

## Zusätzliche Ressourcen

- [Adobe Developer REST-Tutorials](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [Adobe Commerce REST ReDoc](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
