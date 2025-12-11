---
title: Die .env-Datei
description: Erfahren Sie mehr über die Dateitypen in der .env-Datei für diese Beispielanwendung
landing-page-description: Erfahren Sie mehr über die mit Adobe Commerce verwendete Adobe Developer App Builder und welche Inhaltstypen in der .env-Datei verwendet werden
kt: 12423
doc-type: tutorial
audience: all
last-substantial-update: 2023-3-13
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 934fcdd1-ee61-4914-89ce-f6f04b1bc763
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# Generieren und Konfigurieren der .env-Datei {#env-file}

Der `.env` ist eine spezielle Datei, die nicht Teil des Beispielmoduls ist, aber für die Verwendung in Ihrer Adobe Developer App Builder-Anwendung wichtig ist. Diese Datei enthält Geheimnisse und andere Informationen. Vermeiden Sie es, diese Datei in ein Code-Repository zu übertragen.

## Für wen ist dieses Video bestimmt?

* Entwicklerinnen und Entwickler, die neu in Adobe Commerce sind und nur über eingeschränkte Erfahrung mit Adobe App Builder verfügen und mehr über die `.env` erfahren möchten.

## Videoinhalt

* Einführung in die .env-Datei und ihren Zweck
* Generieren der .env-Datei
* Anhängen der Datei zum Hinzufügen neuer geheimer Daten
* Übertragung dieser Datei vermeiden, da sie vertrauliche Informationen enthält

>[!VIDEO](https://video.tv.adobe.com/v/3416593?quality=12&learn=on)

## Code-Beispiel

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

Sie können sehen, wie diese statischen Werte im Beispielmodul in der Datei `actions/commerce.index.js` verwendet werden.

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
