---
title: Create Cart Price Rules
description: Learn how to create cart price rules that apply discounts in the shopping cart when conditions you define are met.
doc-type: Tutorial
last-substantial-update: 2022-12-28T00:00:00.000Z
feature: Configuration, System, Customers, Shopping Cart
topic: Commerce, Administration
role: User
level: Beginner
duration: 353
jira: KT-17148
exl-id: ae8cab73-8a8b-4266-8205-b7397633e9bf
TQID: https://experienceleague.adobe.com/2gmoGQBVz2foQwnGJRlXzWF-OkNGZtiJkQWy0F-0utg
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 701
ht-degree: 0%

---

# Create Cart Price Rules

Cart price rules apply discounts to items in the shopping cart based on conditions you set. The discount can apply automatically when conditions are met, or when the customer enters a valid coupon code. The discount appears in the cart under the subtotal. You can turn a rule on or off for a season or promotion by changing its status and date range.

## Für wen ist dieses Video bestimmt?

* E-Commerce-Marketer
* Website-Manager

## Videoinhalt

* Create cart price rules and optional coupon codes.
* See how discounts appear in the cart and for promotions.

>[!VIDEO](https://video.tv.adobe.com/v/343835?learn=on)

## Pricing display issues

In some cases, each line item must show the discount applied, but displayed values may not match exactly. This happens when a cart price rule applies one discount across multiple products and the split does not divide evenly to two decimal places.

>[!BEGINSHADEBOX]

Cart Price Rule = 10% discount applied to 2 products in the cart
Condition for price rule to take effect: total items in cart is 2
Actions apply percent of product price discount and that discount amount is 10

2 items are added to the cart, each are $19.95

To get the discount amount multiply the product price times 0.1

19.95 x 0.1 = 1.995

This is the issue, we have 3 decimal places, instead of two. Converting this to dollars is now a problem

>[!ENDSHADEBOX]

### The solution

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

2.00 + 2.00 = $4.00

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

1.99 + 1.99 = $3.98

>[!ENDSHADEBOX]

## Zusätzliche Ressourcen

* [Erstellen einer Warenkorb-Preisregel - Handbuch  [!DNL Commerce] Merchandising und Promotions“](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create.html){target="_blank"}
* [Gutscheincodes - Handbuch  [!DNL Commerce] Merchandising und Promotions“](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-coupon.html){target="_blank"}
