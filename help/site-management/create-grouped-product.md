---
title: Erstellen eines gruppierten Produkts
description: Erfahren Sie, wie Sie ein gruppiertes Produkt mit der REST-API und dem Commerce Admin erstellen.
kt: 14585
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-11-30T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
source-git-commit: b44376f9f30e3c02d2c43934046e86faac76f17d
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---


# Erstellen eines gruppierten Produkts

Ein gruppiertes Produkt besteht aus einfachen eigenständigen Produkten, die als Gruppe präsentiert werden. Sie können Varianten eines einzelnen Produkts anbieten oder sie nach Saison oder Thema gruppieren. Bevor Sie ein gruppiertes Produkt erstellen, stellen Sie sicher, dass alle einfachen Produkte, die in die Gruppe aufgenommen werden sollen, in Adobe Commerce verfügbar sind, und erstellen Sie diejenigen, die nicht vorhanden sind.

In diesem Tutorial erfahren Sie, wie Sie ein gruppiertes Produkt mithilfe der REST-API und des Adobe Commerce-Administrators erstellen.

Verwenden Sie die REST-API, um ein Gruppenprodukt in der Admin-Konsole zu erstellen:

1. Erstellen Sie ein leeres gruppiertes Produkt.
1. Erstellen Sie einfache Produkte zur Verwendung im gruppierten Produkt.
1. Füllen Sie das leere gruppierte Produkt mit einfachen Produkten.
1. Erstellen Sie ein leeres gruppiertes Produkt und verknüpfen Sie die einfachen Produkte.

   Wenn Sie einfache Produkte mit dem gruppierten Produkt verknüpfen, wird das Sortierreihenfolgen-Attribut (`position`) in der Payload wird vom Frontend verwendet, um die verknüpften Produkte in der gewünschten Reihenfolge anzuzeigen. Wenn die Variable `position` nicht angegeben ist, werden die Produkte in der Reihenfolge angezeigt, in der sie zum gruppierten Produkt hinzugefügt wurden.

Erstellen Sie beim Erstellen von gruppierten Produkten mit Adobe Commerce Admin zuerst die einfachen Produkte. Wenn Sie bereit sind, das gruppierte Produkt zu erstellen, verknüpfen Sie die einfachen Produkte, indem Sie sie dem gruppierten Produkt in einem Batch zuweisen.

## Für wen ist dieses Video?

- Website-Manager
- eCommerce-Merchandiser
- Neue Adobe Commerce-Entwickler, die erfahren möchten, wie Sie gruppierte Produkte in Adobe Commerce mithilfe der REST-API erstellen.

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3425920?learn=on)

## Einrichtung für das gruppierte Produkt

In diesem Beispiel gibt es drei einfache (zuerst erstellte) Produkte und ein gruppiertes Produkt. Zwei einfache Produkte sind mit dem gruppierten Produkt verknüpft, und dann wird das dritte einfache Produkt zum gruppierten Produkt hinzugefügt.

## Erstellen des ersten einfachen Produkts mit cURL

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=a42da0096288718c9556f77549c6305f; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "product-sku-one",
    "name": "Simple product one",
    "attribute_set_id": 4,
    "price": 1.11,
    "type_id": "simple"
  }
}
```

## Erstellen des zweiten einfachen Produkts mit cURL

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=a42da0096288718c9556f77549c6305f; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "product-sku-two",
    "name": "Simple Product two",
    "attribute_set_id": 4,
    "price": 2.22,
    "type_id": "simple"
  }
}
```

## Drittes einfaches Produkt mithilfe von cURL erstellen

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=a42da0096288718c9556f77549c6305f; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "product-sku-three",
    "name": "Simple product three",
    "attribute_set_id": 4,
    "price": 3.33,
    "type_id": "simple"
  }
}
```

## Erstellen eines leeren gruppierten Produkts mit cURL

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=28a020734488eef2600f8d5c7f302b53; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
    "product":{
        "sku":"my-new-grouped-product",
        "name":"This is my New Grouped Product",
        "attribute_set_id":4,
        "type_id":"grouped",
        "visibility":4
    }
}
'
```

## Hinzufügen der ersten und zweiten einfachen Produkte zum gruppierten Produkt

```bash
curl --location '{{your.url.here}}/rest/default/V1/products/my-new-grouped-product/links' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=28a020734488eef2600f8d5c7f302b53; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
    "items":[
        {
            "sku":"my-new-grouped-product",
            "link_type":"associated",
            "linked_product_sku":"product-sku-one",
            "linked_product_type":"simple",
            "position":1,
            "extension_attributes":{
            "qty":1
            }
        },
        {
            "sku":"my-new-grouped-product",
            "link_type":"associated",
            "linked_product_sku":"product-sku-two",
            "linked_product_type":"simple",
            "position":2,
            "extension_attributes":{
            "qty":1
            }
        }
    ]
}
'
```

## Hinzufügen des dritten einfachen Produkts zum vorhandenen gruppierten Produkt

Fügen Sie die entsprechende Positionsnummer hinzu (alles außer `1` oder `2`), die für die ersten beiden Produkte verwendet werden, die ursprünglich dem gruppierten Produkt zugeordnet waren. In diesem Beispiel lautet die Position `4`.

```bash
curl --location --request PUT '{{your.url.here}}/rest/default/V1/products/my-new-grouped-product/links' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=9e61396705e9c17423eca2bdf2deefb2' \
--data '{
    "entity":{
        "sku":"my-new-grouped-product",
        "link_type":"associated",
        "linked_product_sku":"product-sku-three",
        "linked_product_type":"simple",
        "position":4,
        "extension_attributes":{
            "qty":1
        }
    }
}

'
```

## Ein einfaches Produkt aus einem gruppierten Produkt löschen

nach [Löschen eines einfachen Produkts](https://developer.adobe.com/commerce/webapi/rest/tutorials/grouped-product/) aus einem gruppierten Produkt verwenden: `DELETE /V1/products/{sku}/links/{type}/{linkedProductSku}`.

So entdecken Sie, was als `{type}`verwenden Sie xdebug, um die Anfrage zu erfassen und die $linkTypes auszuwerten: `related`, `crosssell`, `uupsell`, und `associated`.
![Gruppierte Produktverknüpfungstypen - Alternativtext](/help/assets/site-management/catalog/grouped-types.png "Gruppierte Produktverknüpfungstypen, die während der Xdebug-Sitzung erfasst werden")

Beim Verknüpfen der einfachen Produkte mit dem gruppierten Produkt enthielt die Payload einige Abschnitte ähnlich den folgenden:

```bash
        {
            "sku":"my-new-grouped-product",
            "link_type":"associated",
            "linked_product_sku":"product-sku-two",
            "linked_product_type":"simple",
            "position":2,
            "extension_attributes":{
            "qty":1
            }
        }
```

In der Payload wird die `link_type` value `associated` stellt die `{type}` -Wert, der in der DELETE-Anfrage erforderlich ist. Die Anforderungs-URL ähnelt dem `/V1/products/my-new-grouped-product/links/associated/product-sku-three`.

Siehe cURL-Anfrage zum Löschen des einfachen Produkts mit der `product-sku-three` SKU aus dem gruppierten Produkt mit der `my-new-grouped-product` SKU:

```bash
curl --location --request DELETE '{{your.url.here}}rest/default/V1/products/my-new-grouped-product/links/associated/product-sku-three' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=9e61396705e9c17423eca2bdf2deefb2'
```

## Abrufen eines gruppierten Produkts mit cURL

```bash
curl --location '{{your.url.here}}rest/default/V1/products/some-grouped-product-sku' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=3b797a6cc3c5c71f2193109fb9838b12'
```

## Zusätzliche Ressourcen

- [Erstellen und Verwalten von gruppierten Produkten](https://developer.adobe.com/commerce/webapi/rest/tutorials/grouped-product/){target="_blank"}
- [Gruppierungsprodukt](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-grouped.html){target="_blank"}
- [Adobe Developer REST-Tutorials](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [Adobe Commerce REST ReDoc](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
