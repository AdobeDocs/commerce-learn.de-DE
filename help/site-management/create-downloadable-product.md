---
title: Herunterladbares Produkt erstellen
description: Erfahren Sie, wie Sie mit der REST-API und Adobe Commerce Admin ein herunterladbares Produkt erstellen.
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

# Herunterladbares Produkt erstellen

Erfahren Sie, wie Sie mit der REST-API und Adobe Commerce Admin ein herunterladbares Produkt erstellen.

## Für wen ist dieses Video bestimmt?

- Website-Manager
- E-Commerce-Merchandiser
- Neue Adobe Commerce-Entwickler, die lernen möchten, wie Produkte in Adobe Commerce mithilfe der REST-API erstellt werden

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3453955?learn=on&captions=ger)

## Zulässige herunterladbare Domains

Sie müssen angeben, welche Domains Downloads zulassen dürfen. Domains werden über die Befehlszeile zur `env.php` des Projekts hinzugefügt. Die `env.php`-Datei enthält die Domains, in denen herunterladbare Inhalte enthalten sein dürfen. Ein Fehler tritt auf, wenn ein herunterladbares Produkt mithilfe der REST-API erstellt _vor_ wird die `php.env` aktualisiert:

```bash
{
    "message": "Link URL's domain is not in list of downloadable_domains in env.php."
}
```

Um die Domain festzulegen, stellen Sie eine Verbindung mit dem Server her: `bin/magento downloadable:domains:add www.example.com`

Sobald dies abgeschlossen ist, wird der `env.php` innerhalb des Arrays _downloadable_domains_ geändert.

```php
    'downloadable_domains' => [
        'www.example.com'
    ],
```

Nachdem die Domain der `env.php` hinzugefügt wurde, können Sie ein herunterladbares Produkt in Adobe Commerce Admin oder mithilfe der REST-API erstellen.

Weitere Informationen [&#x200B; Sie unter &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html?lang=de#downloadable_domains)Konfigurationsreferenz“.

>[!IMPORTANT]
>In einigen Versionen von Adobe Commerce wird möglicherweise die folgende Fehlermeldung angezeigt, wenn ein Produkt in der Admin-Abteilung von Adobe Commerce bearbeitet wird. Das Produkt wird mithilfe der REST-API erstellt, aber der verknüpfte Download hat einen `null` Preis.

`Deprecated Functionality: number_format(): Passing null to parameter #1 ($num) of type float is deprecated in /app/vendor/magento/module-downloadable/Ui/DataProvider/Product/Form/Modifier/Data/Links.php on line 228`.

Um diesen Fehler zu beheben, verwenden Sie die Update-Link-API: `POST V1/products/{sku}/downloadable-links.`

Weitere Informationen finden [&#x200B; im Abschnitt „Aktualisieren eines Produkt](#update-downloadable-links)Downloadlinks mit cURL“.

## Erstellen eines herunterladbaren Produkts mithilfe von cURL (Download vom Remote-Server)

Dieses Beispiel zeigt, wie ein herunterladbares Produkt mithilfe von cURL erstellt wird, wenn sich die herunterzuladende Datei nicht auf demselben Server befindet. Dieser Anwendungsfall ist typisch, wenn die Datei in einem S3-Bucket oder einem anderen Digital Asset Manager gespeichert ist.

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

## Erstellen eines herunterladbaren Produkts mithilfe von cURL (Herunterladen vom Commerce-Anwendungsserver)

Dieses Beispiel zeigt, wie Sie mit cURL ein herunterladbares Produkt vom Adobe Commerce Admin erstellen können, wenn die Datei auf demselben Server wie die Adobe Commerce-Anwendung gespeichert wird.

In diesem Anwendungsfall wird die Datei in das `pub/media/downloadable/files/links/`-Verzeichnis übertragen, wenn der Administrator, der den Katalog verwaltet, `upload file` auswählt.  Die Automatisierung erstellt die Dateien und verschiebt sie an ihre jeweiligen Speicherorte anhand des folgenden Musters:

- Jede hochgeladene Datei wird in einem Ordner gespeichert, der auf den ersten beiden Zeichen des Dateinamens basiert.
- Wenn der Upload gestartet wird, erstellt das Commerce-Programm vorhandene Ordner oder verwendet sie, um die Datei zu übertragen.
- Beim Herunterladen der Datei verwendet der `link_file` Abschnitt des Pfads den Teil des Pfads, der an das `pub/media/downloadable/files/links/` angehängt wird.

Wenn die hochgeladene Datei beispielsweise `download-example.zip` heißt:

- Die Datei wird in den Pfad `pub/media/downloadable/files/links/d/o/` hochgeladen.
Die Unterverzeichnisse `/d` und `/d/o` werden erstellt, wenn sie noch nicht vorhanden sind.

- Der endgültige Pfad zur Datei lautet `/pub/media/downloadable/files/links/d/o/download-example.zip`.

- Der `link_url` für dieses Beispiel ist `d/o/download-example.zip`

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

## Abrufen eines Produkts mithilfe von cURL

```bash
curl --location '{{your.url.here}}/rest/default/V1/products/POSTMAN-download-product-1' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=b78cae2338f12d846d233d4e9486607e; private_content_version=564dde2976849891583a9a649073f01e'
```

## Aktualisieren des Produkts mit Postman {#update-downloadable-links}

Verwenden des Endpunkt-`rest/all/V1/products/{sku}/downloadable-links`
Die `SKU` ist die Produkt-ID, die beim Erstellen des Produkts generiert wurde. Im folgenden Codebeispiel ist es beispielsweise die Zahl 39. Stellen Sie jedoch sicher, dass sie aktualisiert wird, um die ID aus Ihrer Website zu verwenden. Dadurch werden die Links für die herunterladbaren Produkte aktualisiert.

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

## Aktualisieren eines Produktdownload-Links mithilfe von CURL

Wenn Sie einen Produkt-Download-Link mit cURL aktualisieren, enthält die URL die SKU für das Produkt, das aktualisiert wird.  Im folgenden Code-Beispiel wird die SKU `abcd12345`. Wenn Sie den Befehl übermitteln, ändern Sie den Wert so, dass er mit der SKU für das Produkt übereinstimmt, das Sie aktualisieren möchten.

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

- [Herunterladbarer Produkttyp](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-downloadable.html?lang=de){target="_blank"}
- [Konfigurationshandbuch für herunterladbare Domains](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html?lang=de#downloadable_domains){target="_blank"}
- [Adobe Developer-REST-Tutorials](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [Adobe Commerce-REST-Überprüfung](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
