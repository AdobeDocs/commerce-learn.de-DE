---
title: Erstellen eines herunterladbaren Produkts
description: Erfahren Sie, wie Sie mit der REST-API und dem Adobe Commerce Admin ein herunterladbares Produkt erstellen.
kt: 14464
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-11-16T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
exl-id: 90753b8d-eca0-4868-b40e-9563d2b0e1e8
source-git-commit: eba043cd4169cd762653557bf9283b8d6a208ef0
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---

# Erstellen eines herunterladbaren Produkts

Erfahren Sie, wie Sie mit der REST-API und dem Adobe Commerce Admin ein herunterladbares Produkt erstellen.

## Für wen ist dieses Video?

- Website-Manager
- eCommerce-Merchandiser
- Neue Adobe Commerce-Entwickler, die lernen möchten, wie Produkte in Adobe Commerce mithilfe der REST-API erstellt werden

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3425753?learn=on)

## Zulässige herunterladbare Domänen

Sie müssen angeben, welche Domänen Downloads zulassen dürfen. Domänen werden über die Befehlszeile zur Datei &quot;`env.php`&quot;des Projekts hinzugefügt. Die Datei `env.php` enthält Details zu den Domänen, die herunterladbaren Inhalt enthalten dürfen. Ein Fehler tritt auf, wenn ein herunterladbares Produkt mithilfe der REST-API _erstellt wurde, bevor_ die Datei `php.env` aktualisiert wird:

```bash
{
    "message": "Link URL's domain is not in list of downloadable_domains in env.php."
}
```

Um die Domäne festzulegen, verbinden Sie sich mit dem Server: `bin/magento downloadable:domains:add www.example.com`

Sobald dies abgeschlossen ist, wird der `env.php` im Array _downloadable_domains_ geändert.

```php
    'downloadable_domains' => [
        'www.example.com'
    ],
```

Nachdem die Domäne zum `env.php` hinzugefügt wurde, können Sie ein herunterladbares Produkt in der Adobe Commerce Admin oder mithilfe der REST-API erstellen.

Weitere Informationen finden Sie unter [Konfigurationsreferenz](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html#downloadable_domains) .

>[!IMPORTANT]
>Bei einigen Versionen von Adobe Commerce tritt möglicherweise der folgende Fehler auf, wenn ein Produkt in der Adobe Commerce-Admin-Konsole bearbeitet wird. Das Produkt wird mit der REST-API erstellt, der verknüpfte Download hat jedoch einen `null` -Preis.

`Deprecated Functionality: number_format(): Passing null to parameter #1 ($num) of type float is deprecated in /app/vendor/magento/module-downloadable/Ui/DataProvider/Product/Form/Modifier/Data/Links.php on line 228`.

Um diesen Fehler zu beheben, verwenden Sie die Update Link-API: `POST V1/products/{sku}/downloadable-links.`

Weitere Informationen finden Sie im Abschnitt [Aktualisieren eines Produkt-Downloadlinks mit cURL](#update-downloadable-links) .

## Erstellen eines herunterladbaren Produkts mit cURL (Download vom Remote-Server)

In diesem Beispiel wird gezeigt, wie ein herunterladbares Produkt mithilfe von cURL erstellt wird, wenn sich die herunterzuladende Datei nicht auf demselben Server befindet. Dieser Anwendungsfall ist typisch, wenn die Datei in einem S3-Bucket oder einem anderen digitalen Asset-Manager gespeichert wird.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=b78cae2338f12d846d233d4e9486607e; private_content_version=564dde2976849891583a9a649073f01' \
--data '{
  "product": {
    "sku": "POSTMAN-download-product-1",
    "name": "POSTMAN download product-1",
    "attribute_set_id": 4,
    "price": 9.9,
    "status": 1,
    "visibility": 4,
    "type_id": "downloadable",
    "extension_attributes": {
        "website_ids": [
            1
        ],
        
        "downloadable_product_links": [
            {
                "title": "My url link",
                "sort_order": 1,
                "is_shareable": 1,
                "price": 0,
                "number_of_downloads": 0,
                "link_type": "url",
                "link_url": "{{location.url.where.file.exists}}/some-file.zip",
                "sample_type": "url",
                "sample_url": "{{location.url.where.file.exists}}/sample-file.zip"
            }
        ],
        "downloadable_product_samples": []
    },
    "product_links": [],
    "options": [],
    "media_gallery_entries": [],
    "tier_prices": []
  }
}
'
```

## Erstellen eines herunterladbaren Produkts mit cURL (Download vom Commerce-Anwendungsserver)

In diesem Beispiel wird gezeigt, wie mithilfe von cURL ein herunterladbares Produkt aus dem Adobe Commerce-Administrator erstellt wird, wenn die Datei auf demselben Server wie die Adobe Commerce-Anwendung gespeichert wird.

In diesem Anwendungsfall wird die Datei in das Verzeichnis `pub/media/downloadable/files/links/` übertragen, wenn der Administrator, der den Katalog verwaltet, &quot;`upload file`&quot;auswählt.  Durch die Automatisierung werden die Dateien anhand des folgenden Musters erstellt und an ihre jeweiligen Speicherorte verschoben:

- Jede hochgeladene Datei wird in einem Ordner gespeichert, der auf den ersten beiden Zeichen des Dateinamens basiert.
- Wenn der Upload initiiert wird, erstellt oder verwendet das Commerce-Programm vorhandene Ordner, um die Datei zu übertragen.
- Beim Herunterladen der Datei verwendet der Abschnitt `link_file` des Pfads den Teil des Pfads, der an das Verzeichnis `pub/media/downloadable/files/links/` angehängt ist.

Wenn die hochgeladene Datei beispielsweise `download-example.zip` heißt:

- Die Datei wird in den Pfad `pub/media/downloadable/files/links/d/o/` hochgeladen.
Die Unterverzeichnisse `/d` und `/d/o` werden erstellt, wenn sie nicht vorhanden sind.

- Der endgültige Pfad zur Datei ist `/pub/media/downloadable/files/links/d/o/download-example.zip`.

- Der `link_url` -Wert für dieses Beispiel ist `d/o/download-example.zip`

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=571f5ebe48857569cd56bde5d65f83a2; private_content_version=9f3286b427812be6aec0b04cae33ba35' \
--data '{
  "product": {
    "sku": "sample-local-download-file",
    "name": "A downloadable product with locally hosted download file",
    "attribute_set_id": 4,
    "price": 33,
    "status": 1,
    "visibility": 4,
    "type_id": "downloadable",
    "extension_attributes": {
        "website_ids": [
            1
        ],
        "downloadable_product_links": [
            {
                "title": "an api version of already upload file",
                "sort_order": 1,
                "is_shareable": 1,
                "price": 0,
                "number_of_downloads": 0,
                "link_type": "file",
                "link_file": "/d/o/downloadable-file-demo-file-upload.zip",
                "sample_type": null
            }
        ],
        "downloadable_product_samples": []
    },
    "product_links": [],
    "options": [],
    "media_gallery_entries": [],
    "tier_prices": []
  }
}'
```

## Produkt mit curl abrufen

```bash
curl --location '{{your.url.here}}/rest/default/V1/products/POSTMAN-download-product-1' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=b78cae2338f12d846d233d4e9486607e; private_content_version=564dde2976849891583a9a649073f01e'
```

## Produkt mit Postman aktualisieren {#update-downloadable-links}

Endpunkt `rest/all/V1/products/{sku}/downloadable-links` verwenden
Die `SKU` ist die Produkt-ID, die beim Erstellen des Produkts generiert wurde. Im folgenden Codebeispiel ist es die Nummer 39, aber stellen Sie sicher, dass sie aktualisiert wird, um die ID von Ihrer Website zu verwenden. Dadurch werden die Links für die herunterladbaren Produkte aktualisiert.

```json
{
  "link": {
    "id": 39,
    "title": "My swagger update",
    "sort_order": 0,
    "is_shareable": 0,
    "price": 0,
    "number_of_downloads": 0,
    "link_type": "url",
    "link_file": "{{your.url.here}}/some-file.zip",
    "link_url": "{{your.url.here}}/some-file.zip",
    "link_file_content": {
      "file_data": "{{your.url.here}}/some-file.zip",
      "extension_attributes": {}
    }
  },
  "isGlobalScopeContent": true
}
```

## Aktualisieren eines Produkt-Downloadlinks mithilfe von CURL

Wenn Sie einen Produkt-Download-Link mit cURL aktualisieren, enthält die URL die SKU für das Produkt, das aktualisiert wird.  Im folgenden Codebeispiel lautet die SKU `abcd12345`. Wenn Sie den Befehl senden, ändern Sie den Wert so, dass er mit der SKU für das Produkt übereinstimmt, das Sie aktualisieren möchten.

```bash
curl --location '{{your.url.here}}/rest/all/V1/products/abcd12345/downloadable-links' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=fa5d76f4568982adf369f758e8cb9544; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "link": {
    "id": {{The ID of the download link for example 39}},
    "title": "My update",
    "sort_order": 0,
    "is_shareable": 0,
    "price": 0,
    "number_of_downloads": 0,
    "link_type": "url",
    "link_file": "{{your.url.here}}/some-file.zip",
    "link_url": "{{your.url.here}}/some-file.zip",
    "link_file_content": {
      "file_data": "{{your.url.here}}/some-file.zip",
      "extension_attributes": {}
    }
  },
  "isGlobalScopeContent": true
}'
```

## Zusätzliche Ressourcen

- [herunterladbarer Produkttyp](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-downloadable.html){target="_blank"}
- [ Konfigurationshandbuch für herunterladbare Domänen](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html#downloadable_domains){target="_blank"}
- [Adobe Developer REST-Tutorials](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [Adobe Commerce REST ReDoc](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
