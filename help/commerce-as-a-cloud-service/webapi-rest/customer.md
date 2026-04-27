---
title: Erkunden neuer Kunden-REST-APIs
description: Erfahren Sie, wie Sie neue Kunden-REST-APIs in Adobe Commerce Cloud Service verwenden. Ideal für Architekten und Entwickler.
feature: REST, Customers, Saas
topic: Development, Integrations
role: Developer
level: Beginner
doc-type: Tutorial
duration: 457
last-substantial-update: 2026-01-27T00:00:00.000Z
jira: KT-20160
exl-id: f40d9b21-1f41-4c76-84a9-161168dbfb1a
TQID: https://experienceleague.adobe.com/DiP21e4T-iLM-IuOVDVkJIvHOJ6y-q4IIdSKVplxcX0
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 505
ht-degree: 0%

---

# Kunden-REST-API

Erfahren Sie, wie Sie neue Kunden-REST-APIs in Adobe Commerce as a Cloud Service verwenden. Dieses Tutorial ist ideal für Architekten und Entwickler, die API-Lösungen effektiv integrieren und optimieren möchten.

## Für wen ist dieses Video bestimmt?

* Backend-Entwickler, die für die Erstellung von Integrationen mit Adobe Commerce verantwortlich sind
* Technische Architekten entwerfen Workflows für das Kundenmanagement für Headless-Commerce-Implementierungen

## Videoinhalt

* Authentifizierung bei Adobe IMS mithilfe von Server-zu-Server-Anmeldedaten, um ein Zugriffstoken für API-Anfragen zu erhalten
* Verwenden des richtigen REST-API-Endpunktformats für Commerce as a Cloud Service
* Programmgesteuertes Erstellen und Aktualisieren von Kundenkonten mithilfe von POST- und PUT-Anfragen mit entsprechenden JSON-Payloads

>[!VIDEO](https://video.tv.adobe.com/v/3479361?learn=on)

## Code-Beispiele

Bevor Sie beginnen, erfassen Sie alle erforderlichen Werte aus [Experience Cloud](https://experience.adobe.com) und der [Adobe Developer Console](https://developer.adobe.com/console). Durch die Bereitstellung dieser Werte ist ein reibungsloser Einrichtungsprozess gewährleistet.

>[!NOTE]
>
>Stellen Sie sicher, dass Sie in der richtigen Organisation arbeiten. Die Auswahl Ihres Unternehmens wirkt sich darauf aus, welche Instanzen und Umgebungen sowohl in Experience Cloud als auch in Developer Console sichtbar sind.

### Details der Instanz - experience.adobe.com

Die Instanzdetails enthalten Dinge wie Ihre Instanz-ID, GraphQL-Endpunkte und Anmeldeinformationen.

### Details für Entwickler - https://developer.adobe.com/console/

In der Developer Console verwalten Sie Ihre API-Anmeldeinformationen, einschließlich Client-IDs, Client-Geheimnissen und Zugriffstoken. Sie können auch neue Berechtigungstypen erstellen, z. B. Server-zu-Server- oder native App-Authentifizierung.

## Voraussetzungen

| Element | Wert | Wo dieser Wert ist |
|--- |--- |--- |
| Instanz-ID | `<instance_id>` | experience.adobe.com |
| REST-Endpunkt | `<rest_endpoint>` | experience.adobe.com |
| Client-ID | `<client_id>` | developer.adobe.com/console |
| Client-Geheimnis | `<client_secret>` | developer.adobe.com/console |


## Schritt 1: Zugriffstoken abrufen (Server-zu-Server-Authentifizierung)

>[!IMPORTANT]
>
> Die in diesem Beispiel angezeigten Variablen sind ungültig. Verwenden Sie die Felder &lt;client_id> und &lt;client_secret> aus Ihren Projektanmeldeinformationen.

```bash
curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'grant_type=client_credentials&client_id=<client_id>&client_secret=<client_secret>&scope=openid,AdobeID,email,additional_info.projectedProductContext,profile,commerce.aco.ingestion,commerce.accs,org.read,additional_info.roles'
```

**Beispielantwort:**

```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIs...",
  "token_type": "bearer",
  "expires_in": 86399
}
```

## Schritt 2: Kunden erstellen

>[!IMPORTANT]
>
> Die in diesem Beispiel angegebene URL ist ungültig. Verwenden Sie Ihre REST-Basis-URL. Austausch von &quot;&lt;rest_endpoint>&quot; mit der URL. Es sieht in etwa so aus wie `https://na1-sandbox.api.commerce.adobe.com/AbCYab34cdEfGHiJ27123`.
>
> Dieser Endpunkt hat /rest/ nicht als Teil der URL. Einschließlich , die zu einem Fehler führt.

**Endpunkt:** `POST /V1/customers`

```bash
curl -X POST \
  "<rest_endpoint>/V1/customers" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <ACCESS_TOKEN>" \
  -d '{
    "customer": {
      "email": "john.doe@example.com",
      "firstname": "John",
      "lastname": "Doe",
      "store_id": 1,
      "website_id": 1
    },
    "password": "TempPa55word!"
  }'
```

**Antwort:**

```json
{
  "id": 5,
  "group_id": 1,
  "created_at": "2026-01-23 20:40:15",
  "updated_at": "2026-01-23 20:40:15",
  "created_in": "Default Store View",
  "email": "john.doe@example.com",
  "firstname": "John",
  "lastname": "Doe",
  "store_id": 1,
  "website_id": 1,
  "addresses": [],
  "disable_auto_group_change": 0
}
```

## Schritt 3: Kunden aktualisieren

>[!IMPORTANT]
>
> Die in diesem Beispiel angegebene URL ist ungültig. Verwenden Sie Ihre REST-Basis-URL. Austausch von &quot;&lt;rest_endpoint>&quot; mit der URL. Es sieht in etwa so aus wie `https://na1-sandbox.api.commerce.adobe.com/AbCYab34cdEfGHiJ27123`.

The number `5` in the following example is the ID from the previously created customer using POST `"id": 5,`. Be sure to change`5` to whatever id was returned in your request.

**Endpunkt:** `PUT /V1/customers/{customerId}`

```bash
curl -X PUT \
  "<rest_endpoint>/V1/customers/5" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <ACCESS_TOKEN>" \
  -d '{
    "customer": {
      "id": 5,
      "email": "john.doe@example.com",
      "firstname": "John",
      "lastname": "Doe-Updated"
    }
  }'
```

**Antwort:**

```json
{
  "id": 5,
  "group_id": 1,
  "created_at": "2026-01-23 20:40:15",
  "updated_at": "2026-01-23 20:40:30",
  "created_in": "Default Store View",
  "email": "john.doe@example.com",
  "firstname": "John",
  "lastname": "Doe-Updated",
  "store_id": 1,
  "website_id": 1,
  "addresses": []
}
```

## Complete script (all-in-one)

>[!IMPORTANT]
>
> Die in diesem Beispiel angezeigten Variablen sind ungültig. Use the client ID and client secret from your project credentials. Verwenden Sie Ihre REST-Basis-URL. Exchange &#39;&lt;rest_endpoint>&#39; with your REST endpoint URL from experience.adobe.com. It looks similar to this  `https://na1-sandbox.api.commerce.adobe.com/AbCDefGHiJ1234567`.

```bash
#!/bin/bash

# Configuration be sure to update these with your projects unique values
CLIENT_ID="<client_id>"
CLIENT_SECRET="<client_secret>"
REST_ENDPOINT="<rest_endpoint>"

# Step 1: Get Access Token
echo "Getting access token..."
ACCESS_TOKEN=$(curl -s -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d "grant_type=client_credentials&client_id=${CLIENT_ID}&client_secret=${CLIENT_SECRET}&scope=openid,AdobeID,email,additional_info.projectedProductContext,profile,commerce.aco.ingestion,commerce.accs,org.read,additional_info.roles" | jq -r '.access_token')

echo "Token obtained: ${ACCESS_TOKEN:0:50}..."

# Step 2: Create Customer
echo ""
echo "Creating customer..."
CREATE_RESPONSE=$(curl -s -X POST \
  "${REST_ENDPOINT}/V1/customers" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${ACCESS_TOKEN}" \
  -d '{
    "customer": {
      "email": "john.doe@example.com",
      "firstname": "John",
      "lastname": "Doe",
      "store_id": 1,
      "website_id": 1
    },
    "password": "TempPa55word!"
  }')

echo "Create Response:"
echo "$CREATE_RESPONSE" | jq .

# Extract customer ID
CUSTOMER_ID=$(echo "$CREATE_RESPONSE" | jq -r '.id')
echo "Customer ID: $CUSTOMER_ID"

# Step 3: Update Customer
echo ""
echo "Updating customer..."
curl -s -X PUT \
  "${REST_ENDPOINT}/V1/customers/${CUSTOMER_ID}" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${ACCESS_TOKEN}" \
  -d "{
    \"customer\": {
      \"id\": ${CUSTOMER_ID},
      \"email\": \"john.doe@example.com\",
      \"firstname\": \"john\",
      \"lastname\": \"Doe-Updated\"
    }
  }" | jq .
```

## Important notes about this tutorial

1. **URL Path**: Use `https://<server>.api.commerce.adobe.com/<tenant-id>/V1/customers` — **NOT** `https://<host>/rest/<store-view-code>/V1/customers`
1. **Authentication**: This tutorial used Server-to-Server (`client_credentials` grant type)
1. **Required Scope**: `commerce.accs`
1. **Token Expiry**: 86400 seconds (24 hours)

## References

* [Adobe Commerce as a Cloud Service Release Notes](https://experienceleague.adobe.com/de/docs/commerce/cloud-service/release-notes)
* [SaaS REST API Reference](https://developer.adobe.com/commerce/webapi/reference/rest/saas/)
* [User Authentication Guide](https://developer.adobe.com/commerce/webapi/rest/authentication/user/)
