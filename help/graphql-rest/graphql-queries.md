---
title: Abfragen mit GraphQL durchführen
description: Erfahren Sie, wie Sie mit GraphQL in Adobe Commerce eine Abfrage durchführen und [!DNL Magento Open Source]. Dies ist eine Einführung in GraphQL mithilfe von GET- und POST-Aufrufen.
landing-page-description: Erfahren Sie, wie Sie mit GraphQL in Adobe Commerce eine Abfrage durchführen und [!DNL Magento Open Source]. Dies ist eine Einführung in GraphQL mithilfe von GET- und POST-Aufrufen.
short-description: Erfahren Sie, wie Sie mit GraphQL in Adobe Commerce eine Abfrage durchführen und [!DNL Magento Open Source]. Dies ist eine Einführung in GraphQL mithilfe von GET- und POST-Aufrufen.
kt: 11524
doc-type: tutorial
audience: all
last-substantial-update: 2022-12-13T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 443d711d-ec74-4e07-9357-fbbe0f774853
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---

# GraphQL-Abfragen

Machen wir uns mit einem vollständigen Beispiel direkt mit der GraphQL-Abfragesyntax vertraut. (Beachten Sie, dass Sie dies selbst gegen https://venia.magento.com/graphql ausprobieren können.)

Beachten Sie die folgende GraphQL-Abfrage, die Stück für Stück aufgeteilt ist:

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

Eine plausible Antwort von einem GraphQL-Server für die obige Abfrage könnte sein:

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

Das obige Beispiel beruht auf dem vordefinierten GraphQL-Schema für Adobe Commerce, das auf dem Server definiert ist. In dieser Anfrage werden mehrere Datentypen gleichzeitig abgefragt. Die Abfrage gibt genau die Felder aus, die Sie benötigen, und die zurückgegebenen Daten werden ähnlich wie die Abfrage selbst formatiert.

>[!NOTE]
>
>GraphQL-Clients verschleiern die Form der eigentlichen HTTP-Anforderung, die gesendet wird. Dies lässt sich jedoch leicht erkennen. Wenn Sie einen Browser-basierten Client verwenden, beachten Sie die [!UICONTROL Network] -Tab, wenn eine Abfrage gesendet wird. Sie sehen, dass die Anfrage einen rohen Hauptteil enthält, der aus &quot;query:&quot;besteht. `{string}`&quot;, wobei `{string}` ist einfach die unformatierte Zeichenfolge Ihrer gesamten Abfrage. Wenn die Anforderung als GET gesendet wird, kann die Abfrage stattdessen im Abfragezeichenfolgenparameter &quot;query&quot;kodiert werden. Im Gegensatz zu REST spielt der HTTP-Anfragetyp keine Rolle, sondern nur der Inhalt der Abfrage.


## Abfrage zu dem, was Sie möchten

`country` und `categories` im Beispiel stellen zwei verschiedene &quot;Abfragen&quot;für zwei verschiedene Arten von Daten dar. Im Gegensatz zu einem herkömmlichen API-Paradigma wie REST, das separate und explizite Endpunkte für jeden Datentyp definiert. GraphQL bietet Ihnen die Flexibilität, einen einzelnen Endpunkt mit einem Ausdruck abzufragen, der viele Datentypen gleichzeitig abrufen kann.

Gleichermaßen gibt die Abfrage genau die Felder an, die für beide `country` (`id` und `full_name_english`) und `categories` (`items`, das selbst eine Unterauswahl von Feldern aufweist), und die Daten, die Sie erhalten, spiegeln diese Feldspezifikation wider. Für diese Datentypen sind vermutlich viele weitere Felder verfügbar, Sie erhalten jedoch nur das, was Sie angefordert haben.


>[!NOTE]
>
>Sie werden feststellen, dass der Rückgabewert für `items` ist tatsächlich _array_ Werte, aber Sie wählen trotzdem direkt die entsprechenden Unterfelder aus. Wenn der Typ eines Felds eine Liste ist, versteht GraphQL implizit die Unterauswahl, die auf jedes Element in der Liste angewendet werden soll.

## Argumente

Während die Felder, die Sie zurückgeben möchten, in den Klammern jedes Typs angegeben sind, werden benannte Argumente und Werte für sie in Klammern hinter dem Typnamen angegeben. Argumente sind häufig optional und beeinflussen häufig die Art und Weise, wie Abfrageergebnisse gefiltert, formatiert oder anderweitig umgewandelt werden.

Sie übergeben eine `id` -Argument `country`, wobei das Land angegeben wird, das abgefragt werden soll, und eine `filters` Argument für `categories`.

## Felder ganz nach unten

Während Sie neigen könnten, `country` und `categories` als separate Abfragen oder Entitäten, besteht die gesamte in Ihrer Abfrage ausgedrückte Baumstruktur tatsächlich nur aus Feldern. Der Ausdruck von `products` syntaktisch nicht anders ist als `categories`. Beide sind Felder, und es gibt keinen Unterschied zwischen ihrer Konstruktion.

Jedes GraphQL-Datendiagramm hat einen einzigen &quot;Stammtyp&quot;(typischerweise verwiesen) `Query`), um den Baum zu starten, und die häufig als Entitäten betrachteten Typen werden Feldern auf diesem Stammverzeichnis zugewiesen. Die Beispielabfrage führt tatsächlich eine generische Abfrage für den Stammtyp durch und wählt die Felder aus `country` und `categories`. Anschließend werden Unterfelder dieser Felder ausgewählt usw., möglicherweise mehrere Ebenen tief. Wenn der Rückgabetyp eines Felds ein komplexer Typ ist (z. B. ein Feld mit eigenen Feldern und kein Skalartyp), wählen Sie weiterhin die gewünschten Felder aus.

Aus diesem Konzept verschachtelter Felder können Sie auch Argumente für `products` (`pageSize` und `currentPage`) auf die gleiche Weise wie für die oberste Ebene `categories` -Feld.

![GraphQL-Feldstruktur](../assets/graphql-field-tree.png)

## Variablen

Versuchen wir es mit einer anderen Abfrage:

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

Zunächst ist zu beachten, dass das Keyword hinzugefügt wird. `query` vor der öffnenden Klammer der Abfrage, zusammen mit einem Vorgangsnamen (`getProducts`). Dieser Vorgangsname ist willkürlich. Es entspricht nichts im Serverschema. Diese Syntax wurde hinzugefügt, um die Einführung von Variablen zu unterstützen.

In der vorherigen Abfrage haben Sie Werte für die Argumente Ihrer Felder direkt als Zeichenfolgen oder Ganzzahlen hartcodiert. Die GraphQL-Spezifikation unterstützt jedoch die Trennung der Benutzereingabe von der Hauptabfrage mithilfe von Variablen.

In der neuen Abfrage verwenden Sie Klammern vor der ersten Klammer der gesamten Abfrage, um eine `$search` (Variablen verwenden immer die Dollarzeichen-Präfixsyntax). Diese Variable wird der Variablen `search` Argument für `products`.

Wenn eine Abfrage Variablen enthält, wird erwartet, dass die GraphQL-Anforderung ein separates JSON-kodiertes Wertewörterbuch neben der Abfrage selbst enthält. Für die obige Abfrage können Sie zusätzlich zum Abfragetext die folgende JSON-Datei mit Variablenwerten senden:

```json
{
    "search": "VT01"
}
```

>[!NOTE]
>
>Wenn Sie diese Abfragen für die Venia-Beispielsite und nicht für Ihre eigene Adobe Commerce-Instanz ausprobieren, sind die zurückgegebenen Ergebnisse wahrscheinlich leer für `related_products`.

In jedem GraphQL-fähigen Client, den Sie zum Testen verwenden (z. B. Altair und GraphiQL), unterstützt die Benutzeroberfläche die Eingabe der Variablen JSON separat von der Abfrage.

Genau wie Sie gesehen haben, dass die eigentliche HTTP-Anforderung für eine GraphQL-Abfrage &quot;Abfrage&quot;enthält: `{string}`&quot;, enthält jede Anfrage, die ein Variablenwörterbuch enthält, einfach eine zusätzliche &quot;Variablen: `{json}`&quot;in derselben Stelle, wobei `{json}` ist die JSON-Zeichenfolge mit den Variablenwerten.

Die neue Abfrage verwendet auch eine _fragment_ (`productDetails`), um dieselbe Feldauswahl an mehreren Stellen wiederzuverwenden. [Weitere Informationen zu Fragmenten](https://graphql.org/learn/queries/#fragments){target="_blank"} in der GraphQL-Dokumentation.

{{$include /help/_includes/graphql-rest-related-links.md}}
