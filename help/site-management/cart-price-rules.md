---
title: Erstellen von Regeln für Warenkorbpreise
description: Erfahren Sie, wie Sie Regeln für den Warenkorbpreis erstellen, die Rabatte im Warenkorb anwenden, wenn von Ihnen definierte Bedingungen erfüllt sind.
doc-type: Tutorial
last-substantial-update: 2022-12-28T00:00:00Z
feature: Configuration, System, Customers, Shopping Cart
topic: Commerce, Administration
role: User
level: Beginner
duration: 353
jira: KT-17148
exl-id: ae8cab73-8a8b-4266-8205-b7397633e9bf
source-git-commit: 9aa4d70ee6a3825f027aa2a9c6a1ac0f876ed59f
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 0%

---

# Erstellen von Regeln für Warenkorbpreise

Die Regeln für den Warenkorbpreis wenden Rabatte auf Artikel im Warenkorb basierend auf den von Ihnen festgelegten Bedingungen an. Der Rabatt kann automatisch angewendet werden, wenn die Bedingungen erfüllt sind oder wenn der Kunde einen gültigen Gutscheincode eingibt. Der Rabatt wird im Warenkorb unter der Zwischensumme angezeigt. Sie können eine Regel für eine Saison oder eine Promotion aktivieren oder deaktivieren, indem Sie ihren Status und Datumsbereich ändern.

## Für wen ist dieses Video bestimmt?

* E-Commerce-Marketer
* Website-Manager

## Videoinhalt

* Erstellen Sie Regeln für den Warenkorbpreis und optionale Gutscheincodes.
* Erfahren Sie, wie Rabatte im Warenkorb angezeigt werden und welche Werbeaktionen es gibt.

>[!VIDEO](https://video.tv.adobe.com/v/343835?learn=on)

## Probleme mit der Preisanzeige

In einigen Fällen muss jeder Zeileneintrag den angewendeten Rabatt enthalten, aber die angezeigten Werte stimmen möglicherweise nicht genau überein. Dies geschieht, wenn eine Warenkorb-Preisregel einen Rabatt auf mehrere Produkte anwendet und die Aufspaltung nicht gleichmäßig auf zwei Dezimalstellen aufgeteilt wird.

>[!BEGINSHADEBOX]

Warenkorb-Preisregel = 10 % Rabatt auf 2 Produkte im Warenkorb
Bedingung für das Inkrafttreten der Preisregel: Die Gesamtzahl der Artikel im Warenkorb ist 2.
Aktionen wenden den Rabatt in Prozent des Produktpreises an und dieser Rabattbetrag ist 10

2 Artikel werden zum Warenkorb hinzugefügt, jeder kostet $19.95

Um den Rabattbetrag zu erhalten, multiplizieren Sie den Produktpreis mit 0,1

19,95 x 0,1 = 1,995

Dies ist das Problem, wir haben 3 Dezimalstellen statt zwei. Dies in Dollar zu konvertieren ist jetzt ein Problem

>[!ENDSHADEBOX]

### Die Lösung

Für den Händler in der Admin ist der klarste Ansatz, jede bestellte Zeile mit ihrem Rabatt in Dollar anzuzeigen. Um die Reihenfolge insgesamt korrekt zu halten, runden Sie den ersten Zeileneintrag auf und legen Sie die dritte Dezimalstelle auf den verbleibenden Zeileneinträgen ab. Dieses Szenario überprüfen:

>[!BEGINSHADEBOX]

Derselbe Rabatt von 10 % wie über der gültigen Warenkorbregel
Fügen Sie 2 Produkte zu Warenkorb, die 19.95 sind

Jedes Produkt sollte 1.995 US-Dollar Rabatt erhalten
Produkt 1 - 19,95 x 0,1 = 1,995
2 - 19,95 x 0,1 = 1,995

Ein Gesamtbetrag von 3,99 wird dem Kunden als Rabatt zur Verfügung gestellt

Beim Anzeigen der Zeileneinträge für den Geschäftsinhaber im Admin-Bereich
Wir müssen den ersten Punkt anpassen und auf 2.000 aufrunden. Legen Sie für das zweite Element die dritte Dezimalzahl ab.
Produkt 1 = 2,00
Produkt 2 = 1,99

Der jetzt summierte Gesamtrabatt der beiden Produkte entspricht dem tatsächlichen Rabatt, der einem Kunden gewährt wurde.
>[!ENDSHADEBOX]

Im Folgenden finden Sie einen Screenshot, der in der Administrationsoberfläche für eine Bestellung mit diesem Szenario angezeigt würde:

![Admin-Ansicht mit bestellten Artikeln mit unterschiedlichen Werten](../assets/commerce-admin-cart-price-rule-values-different.png)

### Andere mögliche Lösungen und warum sie nicht verwendet wurden

>[!BEGINSHADEBOX]

Derselbe Rabatt von 10 % wie über der gültigen Warenkorbregel
Fügen Sie 2 Produkte zu Warenkorb, die 19.95 sind

Jedes Produkt sollte 1.995 USD Rabatt erhalten,
Aber wenn wir sie aufrunden, gibt es zu viele Rabatte.

Produkt 1 - 19,95 x 0,1 = 1,995
Produkt 2 - 19,95 x 0,1 = 1,995

Zur Aufrundung aller Elemente konvertieren
Produkt 1 Neuer Wert: 2,00
Produkt 2 Neuer Wert: 2,00

Ein Gesamtbetrag von 3,99 wurde dem Kunden tatsächlich als Rabatt gewährt.
Wenn wir jedoch aufschließen, würde es zeigen, dass 4,00 Dollar gegeben wurden, und das ist falsch.

2,00 + 2,00 = 4,00 $

>[!ENDSHADEBOX]

Ähnliches Problem: Wenn die dritte Dezimalzahl für alle Elemente ignoriert wird, wird zu wenig Rabatt angezeigt.

>[!BEGINSHADEBOX]

Derselbe Rabatt von 10 % wie über der gültigen Warenkorbregel
Fügen Sie 2 Produkte zu Warenkorb, die 19.95 sind

Jedes Produkt sollte 1.995 US-Dollar Rabatt erhalten, aber wenn wir nur die dritte Dezimalzahl fallen lassen, passiert dies:
Produkt 1 - 19,95 x 0,1 = 1,995
Produkt 2 - 19,95 x 0,1 = 1,995

Bei Konvertierung wird die dritte Dezimalzahl für alle Elemente ignoriert.
Produkt 1 Neuer Wert: 1,99
Produkt 2 Neuer Wert: 1,99

Ein Gesamtbetrag von 3,99 wurde dem Kunden tatsächlich als Rabatt gewährt.
Wenn wir jedoch die dritte Dezimalzahl fallen lassen, würde dies zeigen, dass $3,98 angegeben wurde, und das ist falsch.

1,99 + 1,99 = 3,98 $

>[!ENDSHADEBOX]

## Zusätzliche Ressourcen

* [Erstellen einer Warenkorb-Preisregel - [!DNL Commerce] Handbuch für Merchandising und Promotions](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create.html){target="_blank"}
* [Gutscheincodes - [!DNL Commerce] Handbuch für Merchandising und Promotions](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-coupon.html){target="_blank"}
