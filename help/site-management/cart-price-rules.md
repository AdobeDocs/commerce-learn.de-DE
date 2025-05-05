---
title: Erstellen einer Warenkorb-Preisregel
description: Erfahren Sie, wie Sie Regeln für den Warenkorbpreis erstellen, die Rabatte im Warenkorb auf der Grundlage einer Reihe von Bedingungen anwenden.
doc-type: feature video
audience: all
activity: use
last-substantial-update: 2022-12-28T00:00:00Z
feature: Configuration, System, Customers, Shopping Cart
topic: Commerce, Administration
role: Admin, Leader, User
level: Beginner
duration: 171
jira: KT-17148
exl-id: ae8cab73-8a8b-4266-8205-b7397633e9bf
source-git-commit: d290ba1d9c8892b4322aeb19d3c65d9d8087a309
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---

# Erstellen einer Warenkorb-Preisregel

Die Regeln für den Warenkorbpreis wenden Rabatte auf Artikel im Warenkorb an, die auf einer Reihe von Bedingungen basieren. Der Rabatt kann automatisch angewendet werden, wenn die Bedingungen erfüllt sind oder wenn der Kunde einen gültigen Gutscheincode eingibt. Wenn angewendet, wird der Rabatt im Warenkorb unter der Zwischensumme angezeigt. Eine Warenkorb-Preisregel kann bei Bedarf für eine Saison oder Promotion verwendet werden, indem ihr Status und ihr Datumsbereich geändert werden.

## Für wen ist dieses Video bestimmt?

- E-Commerce-Marketer
- Website-Manager

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/3411359?quality=12&learn=on&captions=ger)

## Probleme mit der Preisanzeige

Es gibt einige eindeutige Szenarien, in denen jeder Zeileneintrag seinen Rabatt anzeigen muss, aber die Werte stimmen möglicherweise nicht genau überein. Der Grund dafür ist, dass ein Rabatt aufgrund einer Warenkorbpreisregel auf mehrere Produkte angewendet wird, die Werte sich jedoch nicht gleichmäßig auf zwei Dezimalstellen teilen.

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

Wenn man an den Besitzer der Website denkt, der die einzige Person ist, die von diesem Problem betroffen ist, wurde festgestellt, dass die Anzeige jedes bestellten Artikels mit dem Rabatt in Dollar am besten geeignet war. Um sicherzustellen, dass der gesamte Bestellbetrag ordnungsgemäß berechnet wurde, wurde beschlossen, den ersten Posten aufzurunden und die anderen die dritte Dezimalstelle abzulegen. Dieses Szenario überprüfen:

>[!BEGINSHADEBOX]

Derselbe Rabatt von 10 % wie über der gültigen Warenkorbregel
Fügen Sie 2 Produkte zu Warenkorb, die 19.95 sind

Jedes Produkt sollte 1.995 US-Dollar Rabatt erhalten
Produkt 1 - 19,95 x 0,1 = 1,995
2 - 19,95 x 0,1 = 1,995

Ein Gesamtbetrag von 3,99 wird dem Kunden als Rabatt zur Verfügung gestellt

Beim Anzeigen der Zeileneinträge für den Geschäftsinhaber im Admin-Bereich
Der erste Eintrag muss angepasst und auf 2.000 aufgerundet werden. Beim zweiten Eintrag wird die dritte Dezimalstelle abgelegt
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

- [Erstellen einer Warenkorb-Preisregel - [!DNL Commerce] Handbuch für Merchandising und Promotions](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create.html?lang=de)
- [Gutscheincodes - [!DNL Commerce] Handbuch für Merchandising und Promotions](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-coupon.html?lang=de)
