---
title: Die Datei app.config.yaml
description: Erfahren Sie mehr über die Dateitypen in der Datei app.config.yaml für diese Beispielanwendung.
landing-page-description: Erfahren Sie mehr über Adobe Developer App Builder, das mit Adobe Commerce verwendet wird, und welche Dateitypen in app.config.yaml gespeichert werden.
kt: 12929
doc-type: tutorial
audience: all
last-substantial-update: 2023-3-13
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: ff5f1811-ca93-494e-8e5c-a5e0c7bb673d
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Beschreibung und Verwendung der Datei app.config.yaml {#app-config-yaml}

Diese Datei bestimmt die Konfiguration für das Programm.

## Für wen ist dieses Video bestimmt?

* Entwicklerinnen und Entwickler, die neu in Adobe Commerce sind und nur über eingeschränkte Erfahrung mit Adobe App Builder verfügen und die `app.config.yaml` im Beispielprogramm kennenlernen.

## Videoinhalt

* Die besprochene `app.config.yaml`
* Verknüpfen von Definitionen mit anderen `.js`

>[!VIDEO](https://video.tv.adobe.com/v/3430838?captions=ger&quality=12&learn=on)

## Code-Beispiel

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

Sie können sehen, wie diese statischen Werte im Beispielmodul in der Datei `actions/commerce.index.js` verwendet werden

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
