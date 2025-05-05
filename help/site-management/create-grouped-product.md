---
title: Gruppiertes Produkt erstellen
description: Erfahren Sie, wie Sie mit der REST-API und Commerce Admin ein gruppiertes Produkt erstellen.
kt: 14585
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-11-30T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
exl-id: 3ad7125b-ef6d-4ea0-9fa7-8fc9eb399ec1
source-git-commit: 76a67af957b0d8c1eb64ad42f92412f338650d4b
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Gruppiertes Produkt erstellen

Ein gruppiertes Produkt besteht aus einfachen eigenständigen Produkten, die als Gruppe präsentiert werden. Sie können Varianten eines einzelnen Produkts anbieten oder sie nach Saison oder Thema gruppieren. Bevor Sie ein gruppiertes Produkt erstellen, überprüfen Sie, ob alle in die Gruppe aufzunehmenden einfachen Produkte in Adobe Commerce verfügbar sind, und erstellen Sie alle nicht vorhandenen Produkte.

In diesem Tutorial erfahren Sie, wie Sie ein gruppiertes Produkt mithilfe der REST-API und der Adobe Commerce Admin erstellen.

Verwenden Sie die REST-API, um eine Produktgruppe in der Admin-Liste zu erstellen:

1. Ein leeres gruppiertes Produkt erstellen.
1. Erstellen Sie einfache Produkte zur Verwendung im gruppierten Produkt.
1. Füllen Sie das leere gruppierte Produkt mit einfachen Produkten.
1. Erstellen Sie ein leeres gruppiertes Produkt und verknüpfen Sie die einfachen Produkte.

   Wenn Sie dem gruppierten Produkt einfache Produkte zuordnen, wird das Sortierreihenfolgen-Attribut (`position`) in der Payload vom Frontend verwendet, um die zugehörigen Produkte in einer gewünschten Reihenfolge anzuzeigen. Wenn das Attribut `position` nicht angegeben ist, werden die Produkte in der Reihenfolge angezeigt, in der sie dem gruppierten Produkt hinzugefügt wurden.

Erstellen Sie beim Erstellen von gruppierten Produkten über die Adobe Commerce-Admin zunächst die einfachen Produkte. Wenn Sie bereit sind, das gruppierte Produkt zu erstellen, verknüpfen Sie die einfachen Produkte, indem Sie sie dem gruppierten Produkt in einem Stapel zuweisen.

## Für wen ist dieses Video bestimmt?

- Website-Manager
- E-Commerce-Merchandiser
- Neue Adobe Commerce-Entwicklerinnen und -Entwickler, die lernen möchten, wie Sie mithilfe der REST-API gruppierte Produkte in Adobe Commerce erstellen.

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3454047?learn=on&captions=ger)

## Einrichtung für das gruppierte Produkt

In diesem Beispiel gibt es drei einfache Produkte (zuerst erstellt) und ein gruppiertes Produkt. Dem gruppierten Produkt werden zwei einfache Produkte zugeordnet, und dann wird das dritte einfache Produkt dem gruppierten Produkt hinzugefügt.

## Erstellen des ersten einfachen Produkts mithilfe von cURL

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

## Erstellen des zweiten einfachen Produkts mithilfe von cURL

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

## Erstellen des dritten einfachen Produkts mithilfe von cURL

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

## Leeres gruppiertes Produkt mit cURL erstellen

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

## Hinzufügen des ersten und zweiten einfachen Produkts zum gruppierten Produkt

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

Geben Sie die entsprechende Positionsnummer (alles außer `1` oder `2`) an, die für die ersten beiden Produkte verwendet wird, die ursprünglich mit dem gruppierten Produkt verknüpft waren. Für dieses Beispiel ist die Position `4`.

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

## Löschen eines einfachen Produkts aus einem gruppierten Produkt

Um [einfaches Produkt) aus ](https://developer.adobe.com/commerce/webapi/rest/tutorials/grouped-product/) gruppierten Produkt zu löschen, verwenden Sie: `DELETE /V1/products/{sku}/links/{type}/{linkedProductSku}`.

Um herauszufinden, was als `{type}` verwendet werden soll, verwenden Sie xdebug, um die Anfrage zu erfassen und die $linkTypes zu bewerten: `related`, `crosssell`, `uupsell` und `associated`.
![Gruppierte Produktverknüpfungstypen - Alt-Text](/help/assets/site-management/catalog/grouped-types.png "Gruppierte Produktverknüpfungstypen, die während der xdebug-Sitzung erfasst werden")

Beim Verknüpfen der einfachen Produkte mit dem gruppierten Produkt enthielt die Payload einige ähnliche Abschnitte wie:

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

In der Payload gibt der `link_type` Wert `associated` den in der DELETE-Anfrage erforderlichen `{type}` an. Die Anfrage-URL ähnelt `/V1/products/my-new-grouped-product/links/associated/product-sku-three`.

Siehe die cURL-Anfrage zum Löschen des einfachen Produkts mit der `product-sku-three` SKU aus dem gruppierten Produkt mit der `my-new-grouped-product` SKU:

```bash
curl --location --request DELETE '{{your.url.here}}rest/default/V1/products/my-new-grouped-product/links/associated/product-sku-three' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=9e61396705e9c17423eca2bdf2deefb2'
```

## Abrufen eines gruppierten Produkts mithilfe von cURL

```bash
curl --location '{{your.url.here}}rest/default/V1/products/some-grouped-product-sku' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=3b797a6cc3c5c71f2193109fb9838b12'
```

## Zusätzliche Ressourcen

- [Gruppierte Produkte erstellen und verwalten](https://developer.adobe.com/commerce/webapi/rest/tutorials/grouped-product/){target="_blank"}
- [Gruppiertes Produkt](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-grouped.html?lang=de){target="_blank"}
- [Adobe Developer-REST-Tutorials](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [Adobe Commerce-REST-Überprüfung](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
