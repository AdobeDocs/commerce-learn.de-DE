---
title: Konfigurierbares Produkt erstellen
description: Erfahren Sie, wie Sie ein konfigurierbares Produkt mit der REST-API und dem Commerce Admin erstellen.
kt: 14586
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-12-15T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
source-git-commit: 76716d4c9530963f198a855e101c76b6374c6d75
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---


# Konfigurierbares Produkt erstellen

Ein konfigurierbares Produkt ist ein übergeordnetes Produkt aus mehreren einfachen Produkten. Definieren Sie ein konfigurierbares Produkt, damit der Käufer eine oder mehrere Optionen zur Auswahl einer bestimmten Produktvariante auswählen muss. Wenn es sich beispielsweise bei dem Produkt um ein Hemd handelt, muss der Käufer die Größen- und Farboptionen auswählen, um das Hemd auszuwählen.

Obwohl ein konfigurierbares Produkt mehr SKUs verwendet und die Einrichtung zunächst etwas länger dauern kann, kann es am Ende Zeit sparen. Wenn Sie Ihr Unternehmen erweitern möchten, ist der konfigurierbare Produkttyp eine gute Wahl für Produkte mit mehreren Optionen.

Bevor Sie ein konfigurierbares Produkt erstellen, überprüfen Sie, ob alle einfachen Produkte, die in das konfigurierbare Produkt aufgenommen werden sollen, in Adobe Commerce verfügbar sind. Erstellen Sie keine existierenden Elemente.

In diesem Tutorial erfahren Sie, wie Sie ein konfigurierbares Produkt mithilfe der REST-API und des Adobe Commerce-Administrators erstellen.

Verwenden Sie die REST-API, um ein konfigurierbares Produkt zu erstellen:

1. Abrufen der Attribute für eine [Attributset](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-sets.html) , um die ID-Nummern für nachfolgende API-Aufrufe zu verwenden.
1. Erstellen Sie einfache Produkte zur Verwendung im konfigurierbaren Produkt.
1. Erstellen Sie ein leeres konfigurierbares Produkt und verknüpfen Sie die einfachen Produkte.
1. Festlegen der Produktattribute für das konfigurierbare Produkt.
1. Füllen Sie das leere konfigurierbare Produkt mit einfachen Produkten.
1. Rufen Sie das konfigurierbare Produkt und alle Attribute ab.
1. Rufen Sie die zugewiesenen untergeordneten Produkte für das konfigurierbare Produkt ab.
1. Löschen Sie die Verknüpfung von einfachen Produkten mit konfigurierbaren Produkten.

Beim Erstellen konfigurierbarer Produkte mit dem Adobe Commerce-Administrator können Sie entweder zuerst die einfachen Produkte erstellen oder das automatisierte Tool verwenden, das neue einfache Produkte erstellt, die mit dem Assistenten verwendet werden können.

## Für wen ist dieses Video?

- Website-Manager
- eCommerce-Merchandiser
- Neue Adobe Commerce-Entwickler, die erfahren möchten, wie Sie mit der REST-API konfigurierbare Produkte in Adobe Commerce erstellen

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3426381?learn=on)

## Abrufen der Farbattribute mithilfe von cURL

In diesem Beispiel wird der gesamte Attributsatz mit allen einzelnen Attributen für Attributsatz 10 zurückgegeben. Es kann lange dauern, Hunderte von Zeilen sind nicht ungewöhnlich. Bei der Überprüfung der Antwort befindet sich die Attribut-ID für Farbe wahrscheinlich in der Mitte. Beschleunigen Sie die Suche nach diesen Werten, indem Sie grep oder andere Methoden verwenden, um die Ergebnisse zu durchsuchen. Meine Antwort lag nahe Zeile 665 und ist im folgenden Codefragment aus der JSON-Antwort enthalten.

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


Um die Attribut-IDs zum Einrichten Ihres konfigurierbaren Produkts abzurufen, aktualisieren Sie die `attribute-sets/10/attributes` Teil der folgenden cURL-Anfrage zum Ersetzen `10` mit der Attributsatz-ID in Ihrer Umgebung. Diese Anfrage verwendet die GET-Methode.

```bash
curl --location '{{your.url.here}}rest/V1/products/attribute-sets/10/attributes' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Erstellen des ersten einfachen Produkts mit cURL

### Umgebungskennungen und Produktdetails anpassen

Erstellen Sie das erste einfache Produkt mithilfe der API, um die folgende POST-Anfrage mit cURL zu senden.

Aktualisieren Sie das Beispiel vor dem Senden der Anfrage mit Werten für Ihre Umgebung.

- Änderung `"attribute-set": 10` zu ersetzen `10` mit der Attributsatz-ID aus Ihrer Umgebung.
- Änderung `"value": "13"` zu ersetzen `13` mit dem Wert aus Ihrer Umgebung.

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

## Erstellen des zweiten einfachen Produkts mit cURL

Erstellen Sie das zweite einfache Produkt mithilfe der API, um die folgende POST-Anfrage mit cURL zu senden.

Aktualisieren Sie das Beispiel vor dem Senden der Anfrage mit Werten für Ihre Umgebung.

- Änderung `"attribute_set_id": 10,` und ersetzen `10` mit der Attributsatz-ID aus in Ihrer Umgebung.
- Änderung `"value": "14"` und ersetzen `14` mit dem Wert aus Ihrer Umgebung.


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

## Drittes einfaches Produkt mithilfe von cURL erstellen

Erstellen Sie das dritte einfache Produkt mithilfe der API, um die folgende POST-Anfrage mit cURL zu senden.

Aktualisieren Sie das Beispiel vor dem Senden der Anfrage mit Werten für Ihre Umgebung.

- Änderung `"attribute_set_id": 10,` zu ersetzen `10` mit der Attributsatz-ID aus Ihrer Umgebung.
- Änderung `"value": "15"` und ersetzen `15` mit dem Wert aus Ihrer Umgebung.

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

## Erstellen eines leeren konfigurierbaren Produkts mit cURL

Erstellen Sie ein leeres konfigurierbares Produkt, indem Sie die API verwenden, um die folgende POST-Anfrage mit cURL zu senden.

Aktualisieren Sie das Beispiel vor dem Senden der Anfrage mit Werten für Ihre Umgebung.

- Änderung `"attribute_set_id": 10,` und ersetzen `10` mit der Attributsatz-ID aus Ihrer Umgebung.
- Änderung `"value": "93"` und ersetzen `93` mit dem Wert aus Ihrer Umgebung.

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

## Festlegen der für das konfigurierbare Produkt verfügbaren Optionen

Legen Sie die für das konfigurierbare Produkt verfügbaren Optionen fest, indem Sie die API verwenden, um die folgende POST-Anfrage mit cURL zu senden.

Bevor Sie die Anfrage senden, ändern Sie `"attribute_id": 93,` zu ersetzen `93` mit der Attribut-ID aus Ihrer Umgebung.

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

Wenn Sie vergessen haben, die Optionen für das konfigurierbare Produkt (übergeordnetes Produkt) festzulegen, erhalten Sie eine Fehlermeldung, wenn Sie versuchen, ein untergeordnetes Produkt mit dem konfigurierbaren Produkt zu verknüpfen. Die Fehlermeldung ähnelt dem folgenden Beispiel:

`{"message":"The parent product doesn't have configurable product options.","trace":"#0 [internal function]: Magento\\ConfigurableProduct\\Model\\LinkManagement->addChild('Kids-Hawaiian-U...'}`

## Verknüpfen Sie das untergeordnete Produkt mit dem konfigurierbaren

Jetzt haben Sie drei einfache Produkte erstellt:

- `"Kids Hawaiian Ukulele Red"`,
- `"Kids-Hawaiian-Ukulele-Blue"`
- `"Kids-Hawaiian-Ukulele-Green"`

Fügen Sie diese einfachen POST als untergeordnete Elemente des konfigurierbaren Produkts hinzu, indem Sie die API verwenden, um die folgende Produktanfrage für jedes Produkt zu senden. Senden Sie eine separate Anfrage für jedes Produkt.

Aktualisieren Sie für jede Anforderung die `childSKU` -Wert mit dem Wert für das untergeordnete Produkt, das Sie hinzufügen. Im folgenden Beispiel wird das einfache Produkt zugewiesen `kids-Hawaiian-Ukulele-red` zum konfigurierbaren Produkt mit SKU `Kids-Hawaiian-Ukulele-red`.


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

## Konfigurierbares Produkt mit cURL abrufen

Nachdem Sie jetzt ein konfigurierbares Produkt mit drei zugewiesenen untergeordneten SKUs erstellt haben. Sie können die verknüpften IDs für die zugewiesenen Produkte durch die API sehen, um die folgende GET-Anfrage mit cURL zu senden. Diese Anfrage gibt detaillierte Informationen zum konfigurierbaren Produkt zurück.

```json
...
        "configurable_product_links": [
            155,
            157,
            156
        ]
...
```

Im Folgenden wird die GET-Methode verwendet

```bash
curl --location '{{your.url.here}}/rest/default/V1/products/Kids-Hawaiian-Ukulele' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Ermitteln des untergeordneten Produkts, das mit einem konfigurierbaren Produkt verknüpft ist

Diese Anfrage gibt nur die dem konfigurierbaren Produkt zugeordneten untergeordneten Elemente zurück. Diese Antwort enthält alle Attribute für das untergeordnete Produkt, einschließlich SKU und Preis.

Im Folgenden wird die GET-Methode verwendet

```bash
curl --location '{{your.url.here}}/rest/default/V1/configurable-products/kids-hawaiian-ukulele/children' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Löschen oder Entfernen eines untergeordneten Produkts aus dem übergeordneten konfigurierbaren

Sie können ein untergeordnetes DELETE aus einem konfigurierbaren Produkt entfernen, ohne das Produkt aus dem Katalog zu löschen, indem Sie die API verwenden, um die folgende Produktanforderung mit cURL zu senden.

Im Folgenden wird die DELETE-Methode verwendet

```bash
curl --location --request DELETE '{{your.url.here}}/rest/default/V1/configurable-products/Kids-Hawaiian-Ukulele/children/Kids-Hawaiian-Ukulele-Blue' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Zusätzliche Ressourcen

- [Konfigurierbares Produkt-Tutorial erstellen](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/){target="_blank"}
- [Konfigurierbares Produkt](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html){target="_blank"}
- [Adobe Developer REST-Tutorials](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [Adobe Commerce REST ReDoc](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
