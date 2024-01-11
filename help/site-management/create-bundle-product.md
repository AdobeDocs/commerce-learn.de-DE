---
title: Erstellen eines Bundle-Produkts
description: Erfahren Sie, wie Sie ein Bundle-Produkt mit der REST-API und dem Commerce Admin erstellen.
kt: 14589
doc-type: video
audience: all
activity: use
last-substantial-update: 2024-1-8
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
source-git-commit: e02540438df1cc85e6be7440351a72e77cfc1bf2
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---


# Erstellen eines Bundle-Produkts

Ein Bundle-Produkt ist eine Möglichkeit, mehrere Produkte unter einem übergeordneten Produkt zu gruppieren. Diese untergeordneten Produkte können ein festgelegter Satz von Produkten sein oder einige Varianten bieten, die flexible Konfigurationsoptionen für Kunden bieten. Die Einrichtung von Bundle-Produktarten dauert etwas länger, und Sie müssen diese planen, bevor Sie sie konfigurieren. Das Angebot von Bundle-Produkten verbessert jedoch das Einkaufserlebnis, indem es Kunden erleichtert, ihre Produktauswahl anzupassen.

Sie können beispielsweise ein Produktpaket mit dem Namen `Learning to surf` in Ihrem Webstore. Das Bundle ist das übergeordnete Produkt, das als Container für die zugewiesenen untergeordneten Produkte dient, die verfügbare Optionen angeben:

- Standard-Surfbrett
- Eine typische Surfbrett-Leine
- Rote Surfbrett-Finnen

Wenn zusätzliche Flexibilität gewünscht wird, wird empfohlen, mehrere Optionen für untergeordnete Produkte zu ermöglichen. Dies erfordert eine komplexere Verwendung von Optionen und untergeordneten Produkten. Die letzten Optionen zum Erweitern des vorherigen Beispiels sind:

- Standard-Surfbrett
- Eine typische Surfbrett-Leine
- Auswahl der Flossenfarbe:
   - Rot
   - Blau
   - Gelb

Unabhängig davon, ob es sich bei dem Bundle um eine statische Gruppe einfacher Produkte oder um mehrere Produkte mit Varianten handelt, machen die flexiblen Konfigurationsoptionen Bundle-Produktarten zu einem einzigartigen und leistungsstarken Merchandising-Tool für den Adobe Commerce Store.

Stellen Sie vor dem Erstellen eines Bundle-Produkts sicher, dass alle einfachen Produkte, die in das Bundle-Produkt aufgenommen werden sollen, in Adobe Commerce verfügbar sind. Erstellen Sie keine existierenden Elemente.

In diesem Tutorial erfahren Sie, wie Sie ein Bundle-Produkt mithilfe der REST-API und des Adobe Commerce-Administrators erstellen.

Verwenden Sie die REST-API, um ein Bundle-Produkt zu definieren:

1. Erstellen Sie einfache Produkte zur Verwendung im Bundle-Produkt.
1. Erstellen Sie ein Bundle-Produkt und verknüpfen Sie die einfachen Produkte.
1. Laden Sie das Paket-Produkt und alle zugehörigen Optionen herunter.
1. Löschen Sie eine Option aus einem Abschnitt der Bundle-Produkte.
1. Wiederherstellen der Optionen für ein Paket-Produkt.

Beim Erstellen von Bundle-Produkten über den Adobe Commerce-Administrator können Sie entweder zuerst die einfachen Produkte erstellen oder das automatisierte Tool verwenden, um einfache Produkte mithilfe eines Assistenten zu erstellen.

## Für wen ist dieses Video?

- Website-Manager
- eCommerce-Merchandiser
- Neue Adobe Commerce-Entwickler, die lernen möchten, wie Bundle-Produkte in Adobe Commerce mithilfe der REST-API erstellt werden

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3426797?learn=on)

## Produkte mit REST erstellen

Mit den folgenden Befehlen werden alle Produkte erstellt, die zum Definieren des Bundle-Produkts in diesem Beispiel erforderlich sind: fünf einfache Produkte und ein Bundle-Produkt mit drei Optionen.

Aktualisieren Sie das Beispiel vor dem Senden der Anfrage mit Werten für Ihre Umgebung.

- Änderung `"attribute-set": 4` zu ersetzen `4` mit der Attributsatz-ID aus Ihrer Umgebung.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "10-ft-beginner-surfboard",
    "name": "10 Foot Beginner surfboard",
    "attribute_set_id": 4,
    "price": 100,
    "type_id": "simple",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      }
    }
  }
}
'
```

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "8-ft-surboard-leash",
    "name": "8 Foot surboard leash",
    "attribute_set_id": 4,
    "price": 50,
    "type_id": "simple",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      }
    }
  }
}
'
```

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "red-fins-and-fin-plugs",
    "name": "Red fins and fin plugs",
    "attribute_set_id": 4,
    "price": 15,
    "type_id": "simple",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      }
    }
  }
}
'
```

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "blue-fins-and-fin-plugs",
    "name": "Blue fins and fin plugs",
    "attribute_set_id": 4,
    "price": 15,
    "type_id": "simple",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      }
    }
  }
}
'
```

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "yellow-fins-and-fin-plugs",
    "name": "Yellow fins and fin plugs",
    "attribute_set_id": 4,
    "price": 15,
    "type_id": "simple",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      }
    }
  }
}
'
```

## Erstellen eines Bundle-Produkts und Zuweisen einfacher Produkte als Optionen

Erstellen Sie ein Bundle-Produkt, indem Sie die folgende POST anfordern.

Aktualisieren Sie das Beispiel vor dem Senden der Anfrage mit Werten für Ihre Umgebung.

- Änderung `"attribute_set_id": 4,` und ersetzen `4` mit der Attributsatz-ID aus Ihrer Umgebung.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "beginner-surfboard",
    "name": "Beginner Surfboard",
    "attribute_set_id": 4,
    "status": 1,
    "visibility": 4,
    "type_id": "bundle",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      },
      "bundle_product_options": [
        {
          "option_id": 0,
          "position": 1,
          "sku": "surfboard-essentials",
          "title": "Beginners 10ft Surfboard",
          "type": "checkbox",
          "required": true,
          "product_links": [
            {
              "sku": "10-ft-beginner-surfboard",
              "option_id": 1,
              "qty": 1,
              "position": 1,
              "is_default": false,
              "price": 100,
              "price_type": 0,
              "can_change_quantity": 0
            }
          ]
        },
        {
          "option_id": 1,
          "position": 2,
          "sku": "surboard-leash",
          "title": "Surfboard leash",
          "type": "checkbox",
          "required": true,
          "product_links": [
            {
              "sku": "8-ft-surboard-leash",
              "option_id": 2,
              "qty": 1,
              "position": 1,
              "is_default": false,
              "price": 50,
              "price_type": 0,
              "can_change_quantity": 0
            }
          ]
        },
        {
          "option_id": 3,
          "position": 2,
          "sku": "surfboard-color",
          "title": "Choose a color for the fins and fin plugs",
          "type": "radio",
          "required": true,
          "product_links": [
            {
              "sku": "red-fins-and-fin-plugs",
              "option_id": 2,
              "qty": 1,
              "position": 1,
              "is_default": false,
              "price": 0,
              "price_type": 0,
              "can_change_quantity": 0
            },
            {
              "sku": "blue-fins-and-fin-plugs",
              "option_id": 2,
              "qty": 1,
              "position": 2,
              "is_default": false,
              "price": 0,
              "price_type": 0,
              "can_change_quantity": 0
            },
            {
              "sku": "yellow-fins-and-fin-plugs",
              "option_id": 3,
              "qty": 1,
              "position": 3,
              "is_default": false,
              "price": 0,
              "price_type": 0,
              "can_change_quantity": 0
            }
          ]
        }
      ]
    },
    "custom_attributes": [
      {
        "attribute_code": "price_view",
        "value": "0"
      }
    ]
  },
  "saveOptions": true
}
'
```

## Löschen einer Option aus einem Bundle-Produkt

Entfernen Sie ein untergeordnetes DELETE aus einem Bundle-Produkt, ohne das Produkt aus dem Katalog zu löschen, indem Sie die folgende Produktanforderung mit cURL senden.

```bash
curl --location --request DELETE '{{your.url.here}}/rest/default/V1/bundle-products/beginner-surfboard/options/35/children/blue-fins-and-fin-plugs' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3'
```

## Produktoptionen wiederherstellen

Stellen Sie beim Aktualisieren der Bundle-Produktoptionen sicher, dass Sie alle Optionen einschließen, die Sie mit diesem Produkt verknüpfen möchten. Wenn Ihr ursprünglicher Optionssatz drei Produkte enthielt und eines entfernt wurde, schließen Sie alle drei Optionen in die POST-Anfrage ein, um sicherzustellen, dass das Produktpaket alle Optionen angibt. Wenn Sie nur die entfernte Option eingeschlossen haben, enthält das aktualisierte Produktpaket nur diese Option.

Suchen Sie die Optionskennung, indem Sie die Antwort aus der Erstellung für das Bundle-Produkt überprüfen. In dieser Antwort wird die `option_id` is `35`.

```json
...
,
            {
                "option_id": 35,
                "title": "added back color options for fins and fin plugs",
                "required": true,
                "type": "radio",
                "position": 2,
                "sku": "beginner-surfboard",
                "product_links": [
                    {
                        "id": "77",
                        "sku": "red-fins-and-fin-plugs",
                        "option_id": 35,
                        "qty": 1,
                        "position": 1,
                        "is_default": false,
                        "price": 15,
                        "price_type": null,
                        "can_change_quantity": 0
                    },
                    {
                        "id": "78",
                        "sku": "blue-fins-and-fin-plugs",
                        "option_id": 35,
                        "qty": 1,
                        "position": 2,
                        "is_default": false,
                        "price": 15,
                        "price_type": null,
                        "can_change_quantity": 0
                    },
                    {
                        "id": "79",
                        "sku": "yellow-fins-and-fin-plugs",
                        "option_id": 35,
                        "qty": 1,
                        "position": 3,
                        "is_default": false,
                        "price": 15,
                        "price_type": null,
                        "can_change_quantity": 0
                    }
                ]
            }
...
```

Aktualisieren Sie das Produktpaket, um die entfernte Option hinzuzufügen, indem Sie die folgende POST-Anfrage senden.

```bash
curl --location '{{your.url.here}}/rest/default/V1/bundle-products/options/add' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "option": {
    "option_id": 35,
    "title": "Choose a color for the fins and fin plugs",
    "required": true,
    "type": "radio",
    "position": 2,
    "sku": "beginner-surfboard",
    "product_links": [
      {
        "sku": "red-fins-and-fin-plugs",
        "option_id": 35,
        "qty": 1,
        "position": 1,
        "is_default": false,
        "price": 0,
        "price_type": null,
        "can_change_quantity": 0,
        "extension_attributes": {}
      },
      {
        "sku": "blue-fins-and-fin-plugs",
        "option_id": 35,
        "qty": 1,
        "position": 2,
        "is_default": false,
        "price": 0,
        "price_type": null,
        "can_change_quantity": 0,
        "extension_attributes": {}
      },
      {
        "sku": "yellow-fins-and-fin-plugs",
        "option_id": 35,
        "qty": 1,
        "position": 3,
        "is_default": false,
        "price": 0,
        "price_type": null,
        "can_change_quantity": 0,
        "extension_attributes": {}
      }
    ],
    "extension_attributes": {}
  }
}'
```

## Zusätzliche Ressourcen

- [Bundle-Produkt-Tutorial erstellen](https://developer.adobe.com/commerce/webapi/rest/tutorials/bundle-product/){target="_blank"}
- [Paket-Produkt](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-bundle.html){target="_blank"}
- [Adobe Developer REST-Tutorials](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [Adobe Commerce REST ReDoc](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
