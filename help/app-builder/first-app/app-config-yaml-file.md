---
title: Die Datei "app.config.yaml"
description: Erfahren Sie mehr über die Dateitypen in der Datei "app.config.yaml"für diese Beispielanwendung.
landing-page-description: Erfahren Sie mehr über den mit Adobe Commerce verwendeten Adobe Developer App Builder und welche Dateitypen in der Datei app.config.yaml verwendet werden.
kt: 12426
doc-type: tutorial
audience: all
last-substantial-update: 2023-03-13T00:00:00Z
source-git-commit: 037a7571c87f328dde0f39dd830c7379bd2230b6
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---


# Die `app.config.yaml` file {#app-config-yaml}

Diese Datei bestimmt die Konfiguration für die Anwendung.

## Für wen ist dieses Video?

* Entwickler, die mit Adobe Commerce neu sind und nur über eingeschränkte Erfahrung mit Adobe App Builder verfügen und über die `app.config.yaml` in der Probenanwendung.

## Videoinhalt

* Die `app.config.yaml` diskutierte Datei
* Verknüpfung von Definitionen mit anderen `.js` files

>[!VIDEO](https://video.tv.adobe.com/v/3416592)

## Codebeispiel

```bash
# Specify your secrets here
# This file must not be committed to source control
## Adobe I/O Runtime credentials
AIO_runtime_auth=abcd1234-aaa-bbb-ccc-12345:Abcdd12345asdfadsfadsfee2323232323232
AIO_runtime_namespace=12345-someworkspace-stage
AIO_runtime_apihost=https://adobeioruntime.net
## Adobe I/O Console service account credentials (JWT) Api Key
SERVICE_API_KEY=

# You can also include commerce OAuth credentials, our sample module will use the following example credentials:
#COMMERCE_BASE_URL=https://somecommercewebsite.com/
#COMMERCE_CONSUMER_KEY=abcebdme5bvafnemk0mdeeiyfq123
#COMMERCE_CONSUMER_SECRET=ffff86sqws3pss5hhuofiqgq4t04rrr11
#COMMERCE_ACCESS_TOKEN=gdddfccronj098r4m04zyq773s5o64
#COMMERCE_ACCESS_TOKEN_SECRET=ggg7nb19jhr5gi9jzfan9ggzipe8yrus
```

Sie können sehen, dass diese statischen Werte im Beispielmodul in der Datei verwendet werden `actions/commerce.index.js`

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
