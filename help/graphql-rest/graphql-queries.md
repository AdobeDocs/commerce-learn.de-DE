---
title: Ausführen einer Abfrage mit GraphQL
description: Erfahren Sie, wie Sie eine Abfrage mit GraphQL auf Adobe Commerce und  [!DNL Magento Open Source]. Dies ist eine Einführung in GraphQL mithilfe von GET- und POST-Aufrufen.
landing-page-description: Erfahren Sie, wie Sie eine Abfrage mit GraphQL auf Adobe Commerce und  [!DNL Magento Open Source]. Dies ist eine Einführung in GraphQL mithilfe von GET- und POST-Aufrufen.
short-description: Erfahren Sie, wie Sie eine Abfrage mit GraphQL auf Adobe Commerce und  [!DNL Magento Open Source]. Dies ist eine Einführung in GraphQL mithilfe von GET- und POST-Aufrufen.
kt: 13937
doc-type: video
audience: all
last-substantial-update: 2023-10-12T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 443d711d-ec74-4e07-9357-fbbe0f774853
source-git-commit: 2041bbf1a2783975091b9806c12fc3c34c34582f
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# GraphQL-Abfragen

Dies ist Teil 2 der Serie für GraphQL und Adobe Commerce. In diesem Tutorial und Video erfahren Sie mehr über GraphQL-Abfragen und wie Sie diese mit Adobe Commerce durchführen.

>[!VIDEO](https://video.tv.adobe.com/v/3450067?learn=on&captions=ger)

## Verwandte Videos und Tutorials zu GraphQL in dieser Reihe

* [Teil 1: GraphQL - Einführung](../graphql-rest/intro-graphql.md)
* [Teil 3 GraphQL - Mutationen](../graphql-rest/graphql-mutations.md)
* [Teil 4: GraphQL - Schema](../graphql-rest/graphql-schema.md)

## Beispiel für eine GraphQL-Syntax

Lassen Sie uns mit einem vollständigen Beispiel direkt in die GraphQL-Abfragesyntax eintauchen. (Denken Sie daran, dass Sie dies selbst gegen https://venia.magento.com/graphql versuchen können.)

Beachten Sie die folgende GraphQL-Abfrage, die Stück für Stück aufgeschlüsselt ist:

```graphql
{
    country (
        id: "US"
    ) {
        id
        full_name_english
    }

    categories(
        filters: {
            name: {
                match: "Tops"
            }
        }
    ) {
        items {
            name
            products(
                pageSize: 10,
                currentPage: 2
            ) {
                items {
                    sku
                }
            }
        }
    }
}
```

Eine plausible Antwort eines GraphQL-Servers für die obige Abfrage könnte sein:

```json
{
  "data": {
    "country": {
      "id": "US",
      "full_name_english": "United States"
    },
    "categories": {
      "items": [
        {
          "name": "Tops",
          "products": {
            "items": [
              {
                "sku": "VSW06"
              },
              {
                "sku": "VT06"
              },
              {
                "sku": "VSW07"
              },
              {
                "sku": "VT07"
              },
              {
                "sku": "VSW08"
              },
              {
                "sku": "VT08"
              },
              {
                "sku": "VSW09"
              },
              {
                "sku": "VT09"
              },
              {
                "sku": "VSW10"
              },
              {
                "sku": "VT10"
              }
            ]
          }
        }
      ]
    }
  }
}
```

Das obige Beispiel stützt sich auf das vorkonfigurierte GraphQL-Schema für Adobe Commerce, das auf dem -Server definiert ist. In dieser Anfrage gilt Folgendes:
Gleichzeitiges Abfragen mehrerer Datentypen. Die Abfrage gibt genau die gewünschten Felder aus, und die zurückgegebenen Daten sind formatiert
Ähnlich wie die Abfrage selbst.

>[!NOTE]
>
>GraphQL-Clients verschleiern das Format der tatsächlich gesendeten HTTP-Anfrage, aber dies ist leicht zu entdecken. Wenn Sie einen Browser-basierten Client verwenden, sehen Sie sich die Registerkarte [!UICONTROL Network] an, wenn eine Abfrage gesendet wird. Sie sehen, dass die Anfrage einen Rohtext enthält, der aus „Abfrage: `{string}`&quot; besteht, wobei `{string}` einfach die Rohzeichenfolge der gesamten Abfrage ist. Wenn die Anfrage als GET gesendet wird, kann die Abfrage stattdessen im Abfragezeichenfolgen-Parameter „query“ codiert werden. Im Gegensatz zu REST spielt der HTTP-Anfragetyp keine Rolle, sondern nur der Inhalt der Abfrage.


## Fragen nach dem, was Sie möchten

`country` und `categories` im Beispiel stellen zwei verschiedene „Abfragen“ für zwei verschiedene Arten von Daten dar. Im Gegensatz zu einem herkömmlichen API-Paradigma wie REST, mit dem separate und explizite Endpunkte für jeden Datentyp definiert werden. GraphQL bietet Ihnen die Flexibilität, einen einzelnen Endpunkt mit einem Ausdruck abzufragen, der viele Datentypen gleichzeitig abrufen kann.

Ebenso gibt die Abfrage genau die Felder an, die sowohl für `country` (`id` und `full_name_english`) als auch für `categories` (`items`, das selbst eine Unterauswahl von Feldern aufweist) gewünscht sind, und die empfangenen Daten spiegeln diese Feldspezifikation wider. Für diese Datentypen stehen vermutlich noch viel mehr Felder zur Verfügung, Sie erhalten jedoch nur das zurückgegeben, was Sie angefordert haben.


>[!NOTE]
>
>Sie werden feststellen, dass der Rückgabewert für `items` tatsächlich ein _Array_ von Werten ist, aber Sie wählen trotzdem direkt Unterfelder dafür aus. Wenn der Typ eines Felds eine Liste ist, versteht GraphQL implizit Unterauswahlen, die auf jedes Element in der Liste angewendet werden sollen.

## Argumente

Während die Felder, die zurückgegeben werden sollen, in den geschweiften Klammern jedes Typs angegeben werden, werden benannte Argumente und Werte für sie in Klammern nach dem Typnamen angegeben. Argumente sind häufig optional und beeinflussen oft die Art und Weise, wie Abfrageergebnisse gefiltert, formatiert oder anderweitig transformiert werden.

Sie übergeben ein `id` Argument an `country`, das das jeweilige Land angibt, das abgefragt werden soll, und ein `filters` Argument für `categories`.

## Felder ganz nach unten

Während Sie dazu neigen, `country` und `categories` als separate Abfragen oder Entitäten zu betrachten, besteht die gesamte in Ihrer Abfrage ausgedrückte Baumstruktur tatsächlich nur aus Feldern. Der Ausdruck von `products` unterscheidet sich syntaktisch nicht von dem von `categories`. Beide sind Felder, und es gibt keinen Unterschied zwischen ihrer Konstruktion.

Jedes GraphQL-Datendiagramm hat einen einzigen „Stamm“-Typ (in der Regel als &quot;`Query`&quot; bezeichnet), um die Baumstruktur zu starten, und die Typen, die häufig als Entitäten betrachtet werden, werden den Feldern auf diesem Stamm zugewiesen. Die Beispielabfrage erstellt tatsächlich eine generische Abfrage für den Stammentyp und wählt die Felder `country` und `categories` aus. Anschließend werden Unterfelder dieser Felder ausgewählt usw., die möglicherweise mehrere Ebenen tief sind. Wenn der Rückgabetyp eines Felds ein komplexer Typ ist (z. B. eines mit eigenen Feldern statt eines Skalartyps), wählen Sie weiterhin die gewünschten Felder aus.

Dieses Konzept verschachtelter Felder ist auch der Grund, warum Sie Argumente für `products` (`pageSize` und `currentPage`) auf die gleiche Weise übergeben können wie für das `categories` der obersten Ebene.

![GraphQL-Feldstruktur](../assets/graphql-field-tree.png)

## Variablen

Versuchen Sie eine andere Abfrage:

```graphql
query getProducts(
    $search: String
) {
    products(
        search: $search
    ) {
        items {
            ...productDetails
            related_products {
                ...productDetails
            }
        }
    }
}

fragment productDetails on ProductInterface {
    sku
    name
}
```

Zunächst ist zu beachten, dass der vor der öffnenden Klammer der Abfrage hinzugefügte `query` das Keyword ist, zusammen mit einem Vorgangsnamen (`getProducts`). Dieser Vorgangsname ist beliebig und entspricht keinem Element im Server-Schema. Diese Syntax wurde hinzugefügt, um die Einführung von Variablen zu unterstützen.

In der vorherigen Abfrage haben Sie die Werte für die Argumente Ihrer Felder direkt als Zeichenfolgen oder Ganzzahlen hartcodiert. Die GraphQL-Spezifikation bietet jedoch erstklassige Unterstützung für die Trennung der Benutzereingabe von der Hauptabfrage mithilfe von Variablen.

In der neuen Abfrage verwenden Sie Klammern vor der öffnenden Klammer der gesamten Abfrage, um eine `$search` Variable zu definieren (Variablen verwenden immer die Dollarzeichen-Präfixsyntax). Diese Variable wird dem `search`-Argument für `products` bereitgestellt.

Wenn eine Abfrage Variablen enthält, wird erwartet, dass die GraphQL-Anfrage neben der Abfrage selbst ein separates JSON-kodiertes Wertewörterbuch enthält. Für die obige Abfrage können Sie zusätzlich zum Abfragetext die folgende JSON-Datei mit Variablenwerten senden:

```json
{
    "search": "VT01"
}
```

>[!NOTE]
>
>Wenn Sie diese Abfragen für die Venia-Beispiel-Site und nicht für Ihre eigene Adobe Commerce-Instanz ausprobieren, sind die zurückgegebenen Ergebnisse für `related_products` wahrscheinlich leer.

In jedem GraphQL-fähigen Client, den Sie zum Testen verwenden (z. B. Altair und GraphiQL), unterstützt die Benutzeroberfläche die Eingabe der JSON-Variablen getrennt von der Abfrage.

Wie Sie gesehen haben, dass die eigentliche HTTP-Anfrage für eine GraphQL-Abfrage „query: `{string}`&quot; in ihrem Hauptteil enthält, enthält jede Anfrage mit einem Variablenwörterbuch einfach ein zusätzliches „variables: `{json}`&quot; in demselben Hauptteil, wobei `{json}` die JSON-Zeichenfolge mit den Variablenwerten ist.

Die neue Abfrage verwendet auch ein _Fragment_ (`productDetails`), um dieselbe Feldauswahl an mehreren Stellen wiederzuverwenden. [Weitere Informationen über Fragmente finden ](https://graphql.org/learn/queries/#fragments){target="_blank"} in der Dokumentation zu GraphQL.

{{$include /help/_includes/graphql-rest-related-links.md}}
