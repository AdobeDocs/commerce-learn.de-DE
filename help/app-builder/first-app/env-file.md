---
title: Die .env-Datei
description: Erfahren Sie mehr über die Dateitypen in der .env-Datei für diese Beispielanwendung.
landing-page-description: Erfahren Sie mehr über den mit Adobe Commerce verwendeten Adobe Developer App Builder und darüber, welche Inhaltstypen in der .env-Datei verwendet werden
kt: 12423
doc-type: tutorial
audience: all
last-substantial-update: 2023-03-13T00:00:00Z
source-git-commit: d85426bcf3ae0412a433414d70c874964905dda0
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---


# .env-Datei generieren und konfigurieren {#env-file}

Die `.env` ist eine spezielle Datei, die nicht Teil des Beispielmoduls ist, aber für die Verwendung in Ihrer Adobe Developer App Builder-Anwendung wichtig ist. Diese Datei enthält Geheimnisse und andere Informationen. Vermeiden Sie es, diese Datei an ein Code-Repository zu übergeben.

## Für wen ist dieses Video?

* Entwickler, die mit Adobe Commerce neu sind und nur über eingeschränkte Erfahrung mit Adobe App Builder verfügen, die mehr über die `.env` -Datei.

## Videoinhalt

* Einführung in die .env-Datei und ihren Zweck
* Generieren der .env-Datei
* Anfügen der Datei zum Hinzufügen neuer Geheimnisse
* Vermeiden Sie die Verwendung dieser Datei, da sie sensible Informationen enthält

>[!VIDEO](https://video.tv.adobe.com/v/3416593?quality=12&learn=on)

## Codebeispiel

```bash
# Specify your secrets here
# The .env file must not be committed to source control
## Adobe I/O Runtime credentials
AIO_runtime_auth=abcd1234-aaa-bbb-ccc-12345:Abcdd12345asdfadsfadsfee2323232323232
AIO_runtime_namespace=12345-someworkspace-stage
AIO_runtime_apihost=https://adobeioruntime.net
## Adobe I/O Console service account credentials (JWT) Api Key
SERVICE_API_KEY=

# You can include some commerce OAUTH credentials too, our sample module will use this
#COMMERCE_BASE_URL=https://somecommercewebsite.com/
#COMMERCE_CONSUMER_KEY=abcebdme5bvafnemk0mdeeiyfq123
#COMMERCE_CONSUMER_SECRET=ffff86sqws3pss5hhuofiqgq4t04rrr11
#COMMERCE_ACCESS_TOKEN=gdddfccronj098r4m04zyq773s5o64
#COMMERCE_ACCESS_TOKEN_SECRET=ggg7nb19jhr5gi9jzfan9ggzipe8yrus
```

Sie können sehen, dass diese statischen Werte im Beispielmodul in der Datei verwendet werden `actions/commerce.index.js`.

```javascript
        const oauth = getCommerceOauthClient(
            {
                url: params.COMMERCE_BASE_URL,
                consumerKey: params.COMMERCE_CONSUMER_KEY,
                consumerSecret: params.COMMERCE_CONSUMER_SECRET,
                accessToken: params.COMMERCE_ACCESS_TOKEN,
                accessTokenSecret: params.COMMERCE_ACCESS_TOKEN_SECRET
            },
            logger
        )
```

{{$include /help/_includes/app-builder-first-app-related-links.md}}
