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
exl-id: 112bec9a-0f8e-4252-8c52-f486a5e663b5
source-git-commit: 765bf4159892416e02ea1e9b8e4fa69e396d40af
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# Konfigurierbares Produkt erstellen

Ein konfigurierbares Produkt ist ein übergeordnetes Produkt aus mehreren einfachen Produkten. Definieren Sie ein konfigurierbares Produkt, damit der Käufer eine oder mehrere Optionen zur Auswahl einer bestimmten Produktvariante auswählen muss. Wenn es sich beispielsweise bei dem Produkt um ein Hemd handelt, muss der Käufer die Größen- und Farboptionen auswählen, um das Hemd auszuwählen.

Obwohl ein konfigurierbares Produkt mehr SKUs verwendet und die Einrichtung zunächst etwas länger dauern kann, kann es am Ende Zeit sparen. Wenn Sie Ihr Unternehmen erweitern möchten, ist der konfigurierbare Produkttyp eine gute Wahl für Produkte mit mehreren Optionen.

Bevor Sie ein konfigurierbares Produkt erstellen, überprüfen Sie, ob alle einfachen Produkte, die in das konfigurierbare Produkt aufgenommen werden sollen, in Adobe Commerce verfügbar sind. Erstellen Sie keine existierenden Elemente.

In diesem Tutorial erfahren Sie, wie Sie ein konfigurierbares Produkt mithilfe der REST-API und des Adobe Commerce-Administrators erstellen.

Verwenden Sie die REST-API, um ein konfigurierbares Produkt zu erstellen:

1. Rufen Sie die Attribute für einen [Attributsatz](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-sets.html) ab, um die ID-Nummern für nachfolgende API-Aufrufe zu verwenden.
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


Um die Attribut-IDs zum Einrichten Ihres konfigurierbaren Produkts abzurufen, aktualisieren Sie den Abschnitt `attribute-sets/10/attributes` der folgenden cURL-Anfrage, um `10` durch die Attributset-ID in Ihrer Umgebung zu ersetzen. Diese Anfrage verwendet die GET-Methode.

```bash
curl --location '{{your.url.here}}rest/V1/products/attribute-sets/10/attributes' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Erstellen des ersten einfachen Produkts mit cURL

### Umgebungskennungen und Produktdetails anpassen

Erstellen Sie das erste einfache Produkt mithilfe der API, um die folgende POST-Anfrage mit cURL zu senden.

Aktualisieren Sie das Beispiel vor dem Senden der Anfrage mit Werten für Ihre Umgebung.

- Ändern Sie &quot;`"attribute-set": 10`&quot;, um &quot;`10`&quot;durch die Attributset-ID aus Ihrer Umgebung zu ersetzen.
- Ändern Sie `"value": "13"`, um `13` durch den Wert aus Ihrer Umgebung zu ersetzen.

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

- Ändern Sie `"attribute_set_id": 10,` und ersetzen Sie `10` durch die Attributsatz-ID aus in Ihrer Umgebung.
- Ändern Sie `"value": "14"` und ersetzen Sie `14` durch den Wert aus Ihrer Umgebung.

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

Erstellen Sie das dritte einfache Produkt, indem Sie die folgende POST-Anfrage mit cURL senden.

Aktualisieren Sie das Beispiel vor dem Senden der Anfrage mit Werten für Ihre Umgebung.

- Ändern Sie &quot;`"attribute_set_id": 10,`&quot;, um &quot;`10`&quot;durch die Attributset-ID aus Ihrer Umgebung zu ersetzen.
- Ändern Sie `"value": "15"` und ersetzen Sie `15` durch den Wert aus Ihrer Umgebung.

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

Erstellen Sie ein leeres konfigurierbares Produkt, indem Sie die folgende POST-Anfrage mit cURL senden.

Aktualisieren Sie das Beispiel vor dem Senden der Anfrage mit Werten für Ihre Umgebung.

- Ändern Sie `"attribute_set_id": 10,` und ersetzen Sie `10` durch die Attributsatz-ID aus Ihrer Umgebung.
- Ändern Sie `"value": "93"` und ersetzen Sie `93` durch den Wert aus Ihrer Umgebung.

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

Legen Sie die für das konfigurierbare Produkt verfügbaren Optionen fest, indem Sie die folgende POST-Anfrage mit cURL senden.

Ändern Sie vor dem Senden der Anfrage `"attribute_id": 93,` , um `93` durch die Attribut-ID aus Ihrer Umgebung zu ersetzen.

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

Fügen Sie diese einfachen Produkte als untergeordnete Elemente des konfigurierbaren Produkts hinzu, indem Sie die folgende POST anfordern. Senden Sie eine separate Anfrage für jedes Produkt.

Aktualisieren Sie für jede Anfrage den Wert `childSKU` mit dem Wert für das untergeordnete Produkt, das Sie hinzufügen. Im folgenden Beispiel wird das einfache Produkt `kids-Hawaiian-Ukulele-red` dem konfigurierbaren Produkt mit der SKU `Kids-Hawaiian-Ukulele-red` zugewiesen.


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

Nachdem Sie jetzt ein konfigurierbares Produkt mit drei zugewiesenen untergeordneten SKUs erstellt haben. Sie können die verknüpften IDs für die zugewiesenen Produkte anzeigen, indem Sie die folgende GET-Anfrage mit cURL senden. Diese Anfrage gibt detaillierte Informationen zum konfigurierbaren Produkt zurück.

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

Geben Sie nur die dem konfigurierbaren Produkt zugeordneten untergeordneten Elemente zurück, indem Sie die folgende GET-Anfrage senden. Die Antwort enthält alle Attribute für das untergeordnete Produkt, einschließlich SKU und Preis.

Im Folgenden wird die GET-Methode verwendet

```bash
curl --location '{{your.url.here}}/rest/default/V1/configurable-products/kids-hawaiian-ukulele/children' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Löschen oder Entfernen eines untergeordneten Produkts aus dem übergeordneten konfigurierbaren

Sie können ein untergeordnetes DELETE aus einem konfigurierbaren Produkt entfernen, ohne das Produkt aus dem Katalog zu löschen, indem Sie die folgende Produktanforderung mit cURL senden.

```bash
curl --location --request DELETE '{{your.url.here}}/rest/default/V1/configurable-products/Kids-Hawaiian-Ukulele/children/Kids-Hawaiian-Ukulele-Blue' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Zusätzliche Ressourcen

- [Erstellen Sie ein konfigurierbares Produkt-Tutorial](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/){target="_blank"}
- [Konfigurierbares Produkt](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html){target="_blank"}
- [Adobe Developer REST-Tutorials](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [Adobe Commerce REST ReDoc](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
