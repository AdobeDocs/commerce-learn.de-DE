---
title: Create a configurable product
description: Learn how to create a configurable product using the REST API and the Commerce Admin.
kt: 14586
doc-type: video
duration: 1760
audience: all
activity: use
last-substantial-update: 2023-12-15T00:00:00.000Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
exl-id: 112bec9a-0f8e-4252-8c52-f486a5e663b5
TQID: https://experienceleague.adobe.com/XAvtOnOIycqQ4z-uztWuVzzv0--eVit-I-QDnl67ba8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 994
ht-degree: 0%

---

# Create a configurable product

A configurable product is a parent product of multiple simple products. Define a configurable product to require the buyer to make one or more choices to select a specific product variation. For example, if the product is a shirt, the buyer must choose the size and color options to select the shirt.

Although a configurable product uses more SKUs and may initially take a little longer to set up, it can save you time in the end. If you plan to grow your business, the configurable product type is a good choice for products with multiple options.

Before creating a configurable product, verify that all the simple products to include in the configurable product are available in Adobe Commerce. Create any that do not exist.

In this tutorial, learn how to create a configurable product using the REST API and the Adobe Commerce Admin.

Use the REST API to create a configurable product:

1. Get the attributes for an [attribute set](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-sets.html?lang=de) to use the ID numbers for subsequent API calls.
1. Create simple products for use in the configurable product.
1. Create an empty configurable product and associate the simple products.
1. Set the product attributes for the configurable product.
1. Populate the empty configurable product with simple products.
1. Get the configurable product and all the attributes.
1. Get the assigned children products for the configurable product.
1. Delete the association of simple products to configurable products.

When creating configurable products from the Adobe Commerce Admin, you can either create the simple products first, or use the automated tool that creates new simple products for use using the wizard.

## Für wen ist dieses Video bestimmt?

* Website-Manager
* E-Commerce-Merchandiser
* Neue Adobe Commerce-Entwicklerinnen und -Entwickler, die lernen möchten, wie man mit der REST-API konfigurierbare Produkte in Adobe Commerce erstellt

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3426381?learn=on)

## Abrufen der Farbattribute mithilfe von cURL

In diesem Beispiel wird für Attributsatz 10 der gesamte Attributsatz mit allen einzelnen Attributen zurückgegeben. Es kann lang sein, Hunderte von Zeilen sind nicht ungewöhnlich. Bei der Überprüfung der Antwort wird die Attribut-ID für die Farbe wahrscheinlich in der Mitte angezeigt. Beschleunigen Sie die Suche nach diesen Werten, indem Sie Grep oder andere Methoden verwenden, um die Ergebnisse zu durchsuchen. Meine Antwort war in der Nähe von Zeile 665 und ist im folgenden Ausschnitt aus der JSON-Antwort enthalten.

```json
...
{
        "attribute_id": 93,
        "attribute_code": "color",
        "frontend_input": "select",
        "entity_type_id": "4",
        "is_required": false,
        "options": [
            {
                "label": " ",
                "value": ""
            },
            {
                "label": "Red",
                "value": "13"
            },
            {
                "label": "Blue",
                "value": "14"
            },
            {
                "label": "Green",
                "value": "15"
            }
        ],
...
```


Um die Attribut-IDs abzurufen, um Ihr konfigurierbares Produkt einzurichten, aktualisieren Sie den `attribute-sets/10/attributes` Teil der folgenden cURL-Anfrage, um `10` durch die Attribut-Set-ID in Ihrer Umgebung zu ersetzen. Diese Anfrage verwendet die GET-Methode.

```bash
curl --location '{{your.url.here}}rest/V1/products/attribute-sets/10/attributes' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Erstellen des ersten einfachen Produkts mithilfe von cURL

### Anpassen der Umgebungs-IDs und Produktdetails

Erstellen Sie das erste einfache Produkt, indem Sie die -API verwenden, um die folgende POST-Anfrage mit cURL zu senden.

Bevor Sie die Anfrage senden, aktualisieren Sie das Beispiel mit Werten für Ihre Umgebung.

* Ändern Sie `"attribute-set": 10`, um `10` durch die Attributsatz-ID aus Ihrer Umgebung zu ersetzen.
* Ändern Sie `"value": "13"`, um `13` durch den Wert aus Ihrer Umgebung zu ersetzen.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "product": {
    "sku": "Kids-Hawaiian-Ukulele-red",
    "name": "Kids Hawaiian Ukulele Red",
    "attribute_set_id": 10,
    "price": 12.50,
    "status": 1,
    "visibility": 1,
    "type_id": "simple",
    "weight": "0.5",
    "extension_attributes": {
        "stock_item": {
            "qty": "10",
            "is_in_stock": true
        }
    },
    "custom_attributes": [
        {
            "attribute_code": "color",
            "value": "13"
        }
    ]
  }
}
'
```

## Erstellen des zweiten einfachen Produkts mithilfe von cURL

Erstellen Sie das zweite einfache Produkt, indem Sie die -API verwenden, um die folgende POST-Anfrage mit cURL zu senden.

Bevor Sie die Anfrage senden, aktualisieren Sie das Beispiel mit Werten für Ihre Umgebung.

* Ändern Sie `"attribute_set_id": 10,` und ersetzen Sie `10` durch die Attributsatz-ID aus in Ihrer Umgebung.
* Ändern Sie `"value": "14"` und ersetzen Sie `14` durch den Wert aus Ihrer Umgebung.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "product": {
    "sku": "Kids-Hawaiian-Ukulele-Blue",
    "name": "Kids Hawaiian Ukulele Blue",
    "attribute_set_id": 10,
    "price": 15,
    "status": 1,
    "visibility": 1,
    "type_id": "simple",
    "weight": "0.5",
    "extension_attributes": {
        "stock_item": {
            "qty": "20",
            "is_in_stock": true
        }
    },
    "custom_attributes": [
        {
            "attribute_code": "color",
            "value": "14"
        }
    ]
  }
}
'
```

## Erstellen des dritten einfachen Produkts mithilfe von cURL

Erstellen Sie das dritte einfache Produkt, indem Sie die folgende POST-Anfrage mit cURL senden.

Bevor Sie die Anfrage senden, aktualisieren Sie das Beispiel mit Werten für Ihre Umgebung.

* Ändern Sie `"attribute_set_id": 10,`, um `10` durch die Attributsatz-ID aus Ihrer Umgebung zu ersetzen.
* Ändern Sie `"value": "15"` und ersetzen Sie `15` durch den Wert aus Ihrer Umgebung.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "product": {
    "sku": "Kids-Hawaiian-Ukulele-Green",
    "name": "Kids Hawaiian Ukulele Green",
    "attribute_set_id": 10,
    "price": 25,
    "status": 1,
    "visibility": 1,
    "type_id": "simple",
    "weight": "0.5",
    "extension_attributes": {
        "stock_item": {
            "qty": "30",
            "is_in_stock": true
        }
    },
    "custom_attributes": [
        {
            "attribute_code": "color",
            "value": "15"
        }
    ]
  }
}
'
```

## Create an empty configurable product using cURL

Create an empty configurable product by sending the following POST request using cURL.

Bevor Sie die Anfrage senden, aktualisieren Sie das Beispiel mit Werten für Ihre Umgebung.

* Change `"attribute_set_id": 10,` and replace `10` with the attribute set id from your environment.
* Ändern Sie `"value": "93"` und ersetzen Sie `93` durch den Wert aus Ihrer Umgebung.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "product": {
    "sku": "Kids-Hawaiian-Ukulele",
    "name": "Kids Hawaiian Ukulele",
    "attribute_set_id": 10,
    "status": 1,
    "visibility": 4,
    "type_id": "configurable",
    "weight": "0.5",
    "custom_attributes": [
        {
            "attribute_code": "color",
            "value": "93"
        }
    ]
  }
}'
```

## Set the options available for the configurable product

Set the options available for the configurable product by sending the following POST request using cURL.

Before submitting the request, change `"attribute_id": 93,` to replace `93` with the attribute id from your environment.

```bash
curl --location '{{your.url.here}}/rest/default/V1/configurable-products/Kids-Hawaiian-Ukulele/options' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "option": {
    "attribute_id": "93",
    "label": "Color",
    "position": 0,
    "is_use_default": true,
    "values": [
      {
        "value_index": 9
      }
    ]
  }
}'
```

If you forget to set the options for the configurable product (parent), you get an error when you try to associate a child product to the configurable product. The error message is similar to the following example:

`{"message":"The parent product doesn't have configurable product options.","trace":"#0 [internal function]: Magento\\ConfigurableProduct\\Model\\LinkManagement->addChild('Kids-Hawaiian-U...'}`

## Link the child product to the configurable

Now, you have created three simple products:

* `"Kids Hawaiian Ukulele Red"`,
* `"Kids-Hawaiian-Ukulele-Blue"`
* `"Kids-Hawaiian-Ukulele-Green"`

Add these simple products as children of the configurable product by sending the following POST request. Submit a separate request for each product.

For each request, update the `childSKU` value with the value for the child product you are adding. The following example assigns the simple product `kids-Hawaiian-Ukulele-red` to the configurable product with the SKU `Kids-Hawaiian-Ukulele-red`.


```bash
curl --location '{{your.url.here}}rest/default/V1/configurable-products/Kids-Hawaiian-Ukulele/child' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "childSku": "Kids-Hawaiian-Ukulele-red"
}
'
```

## Get a configurable product using cURL

Now that you have created a configurable product with three assigned child SKUs. You can see the linked IDs for the assigned products by sending the following GET request using cURL. This request returns detailed information about the configurable product.

```json
...
        "configurable_product_links": [
            155,
            157,
            156
        ]
...
```

The following uses the GET method

```bash
curl --location '{{your.url.here}}/rest/default/V1/products/Kids-Hawaiian-Ukulele' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Get the children product associated to a configurable product

Return only the children associated with the configurable product by sending the following GET request. The response will include all the attributes for the child product including SKU and price.

Im Folgenden wird die GET-Methode verwendet

```bash
curl --location '{{your.url.here}}/rest/default/V1/configurable-products/kids-hawaiian-ukulele/children' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Löschen oder Entfernen eines untergeordneten Produkts aus der übergeordneten konfigurierbaren Komponente

Sie können ein untergeordnetes Produkt aus einem konfigurierbaren Produkt entfernen, ohne das Produkt aus dem Katalog zu löschen, indem Sie die folgende DELETE-Anfrage mit cURL senden.

```bash
curl --location --request DELETE '{{your.url.here}}/rest/default/V1/configurable-products/Kids-Hawaiian-Ukulele/children/Kids-Hawaiian-Ukulele-Blue' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Zusätzliche Ressourcen

* [Erstellen eines konfigurierbaren Produkt-Tutorials](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/){target="_blank"}
* [Konfigurierbares Produkt](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html?lang=de){target="_blank"}
* [Adobe Developer-REST-Tutorials](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
* [Adobe Commerce REST-Dokumentation](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
