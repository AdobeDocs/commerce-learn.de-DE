---
title: Bundle-Produkt erstellen
description: Erfahren Sie, wie Sie mit der REST-API und Commerce Admin ein Produktpaket erstellen.
kt: 14589
doc-type: video
audience: all
activity: use
last-substantial-update: 2024-1-8
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
exl-id: 5d688e6a-ae8c-4a55-b16c-5d3ae2d1bfd5
source-git-commit: 765bf4159892416e02ea1e9b8e4fa69e396d40af
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# Bundle-Produkt erstellen

Ein Produktpaket ist eine Möglichkeit, mehrere Produkte unter einem übergeordneten Produkt zu gruppieren. Bei diesen untergeordneten Produkten kann es sich um einen definierten Satz von Produkten handeln oder um einige Varianten, die Kunden flexible Konfigurationsoptionen bieten. Die Einrichtung von Bundle-Produkttypen dauert etwas länger und Sie müssen einige Planungen durchführen, bevor Sie sie konfigurieren können. Das Angebot von Bundle-Produkten verbessert jedoch das Einkaufserlebnis, da Kunden ihre Produktauswahl leichter anpassen können.

Beispielsweise können Sie in Ihrem Webstore ein Produktpaket mit dem Namen `Learning to surf` anbieten. Das Bundle ist das übergeordnete Produkt, das als Container für die zugewiesenen untergeordneten Produkte dient, die die verfügbaren Optionen angeben:

- Ein Standard-Surfbrett
- Eine typische Surfbrett-Leine
- Rote Surfbrett-Flossen

Wenn zusätzliche Flexibilität erwünscht ist, wird empfohlen, verschiedene Optionen für untergeordnete Produkte zuzulassen. Dies erfordert eine komplexere Verwendung von Optionen und untergeordneten Produkten. Um das vorherige Beispiel zu erweitern, lauten die endgültigen Optionen:

- Ein Standard-Surfbrett
- Eine typische Surfbrett-Leine
- Auswahl der Flossenfarbe:
   - Rot
   - Blau
   - Gelb

Unabhängig davon, ob es sich bei dem Bundle um eine statische Gruppe einfacher Produkte oder um mehrere Produkte mit Varianten handelt, machen die flexiblen Konfigurationsoptionen Bundle-Produkttypen zu einem einzigartigen und leistungsstarken Merchandising-Tool für den Adobe Commerce Store.

Bevor Sie ein Produktpaket erstellen, überprüfen Sie, ob alle einfachen Produkte, die im Produktpaket enthalten sein sollen, in Adobe Commerce verfügbar sind. Erstellen Sie alle , die nicht vorhanden sind.

In diesem Tutorial erfahren Sie, wie Sie ein Produktpaket mithilfe der REST-API und der Adobe Commerce Admin erstellen.

Verwenden der REST-API zum Definieren eines Produktpakets:

1. Erstellen Sie einfache Produkte zur Verwendung im Produktpaket.
1. Erstellen Sie ein Produkt-Bundle und verknüpfen Sie die einfachen Produkte.
1. Rufen Sie das Produktpaket und alle zugehörigen Optionen ab.
1. Löschen einer Option aus einem Abschnitt der Produktpakete.
1. Stellen Sie die Optionen für ein Produktpaket wieder her.

Beim Erstellen von Bundle-Produkten über den Adobe Commerce-Administrator können Sie entweder zuerst die einfachen Produkte erstellen oder das automatisierte Tool verwenden, um mithilfe eines Assistenten einfache Produkte zu erstellen.

## Für wen ist dieses Video bestimmt?

- Website-Manager
- E-Commerce-Merchandiser
- Neue Adobe Commerce-Entwicklerinnen und -Entwickler, die lernen möchten, wie Sie mit der REST-API Bundle-Produkte in Adobe Commerce erstellen

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3426797?learn=on)

## Erstellen von Produkten mit REST

Mit den folgenden Befehlen werden alle Produkte erstellt, die zum Definieren des Bundle-Produkts in diesem Beispiel erforderlich sind: fünf einfache Produkte und ein Bundle-Produkt mit drei Optionen.

Bevor Sie die Anfrage senden, aktualisieren Sie das Beispiel mit Werten für Ihre Umgebung.

- Ändern Sie `"attribute-set": 4`, um `4` durch die Attributsatz-ID aus Ihrer Umgebung zu ersetzen.

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

## Bundle-Produkt erstellen und die einfachen Produkte als Optionen zuweisen

Erstellen Sie ein Produktpaket, indem Sie die folgende POST-Anfrage senden.

Bevor Sie die Anfrage senden, aktualisieren Sie das Beispiel mit Werten für Ihre Umgebung.

- Ändern Sie `"attribute_set_id": 4,` und ersetzen Sie `4` durch die Attributsatz-ID aus Ihrer Umgebung.

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

## Löschen einer Option aus einem Produktpaket

Entfernen Sie ein untergeordnetes Produkt aus einem Produktpaket, ohne das Produkt aus dem Katalog zu löschen, indem Sie die folgende DELETE-Anfrage mit cURL senden.

```bash
curl --location --request DELETE '{{your.url.here}}/rest/default/V1/bundle-products/beginner-surfboard/options/35/children/blue-fins-and-fin-plugs' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3'
```

## Produktoptionen wiederherstellen

Stellen Sie beim Aktualisieren der Bundle-Produktoptionen sicher, dass Sie alle Optionen einbeziehen, die Sie mit diesem Produkt verknüpfen möchten. Wenn Ihr ursprünglicher Satz von Optionen drei Produkte enthielt und eines entfernt wurde, schließen Sie alle drei Optionen in die POST-Anfrage ein, um sicherzustellen, dass das Produktpaket alle Optionen angibt. Wenn Sie nur die Option einbezogen haben, die Sie entfernt haben, enthält das aktualisierte Produktpaket nur diese Option.

Suchen Sie die Option-ID, indem Sie die Antwort aus der Erstellung für das Produkt-Bundle überprüfen. In dieser Antwort wird die `option_id` `35`.

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

Aktualisieren Sie das Produktpaket, um die von Ihnen entfernte Option hinzuzufügen, indem Sie die folgende POST-Anfrage senden.

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

- [Erstellen eines Bundle-Produkt-Tutorials](https://developer.adobe.com/commerce/webapi/rest/tutorials/bundle-product/){target="_blank"}
- [Bundle-Produkt](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-bundle.html?lang=de){target="_blank"}
- [Adobe Developer-REST-Tutorials](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [Adobe Commerce-REST-Überprüfung](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
