---
title: Erstellen einer Preisregel für Warenkorb
description: Erfahren Sie, wie Sie Regeln für den Warenkorbpreis erstellen, die Rabatte im Warenkorb auf der Grundlage einer Reihe von Bedingungen anwenden.
doc-type: feature video
audience: all
activity: use
last-substantial-update: 2022-12-28T00:00:00Z
feature: Configuration, System, Catalogs, Customers, Shopping Cart
topic: Commerce, Administration
role: Admin, Leader, User
level: Beginner, Intermediate
exl-id: ae8cab73-8a8b-4266-8205-b7397633e9bf
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Erstellen einer Preisregel für Warenkorb

Preisregeln für Warenkorb gelten für Artikel im Warenkorb, die auf einer Reihe von Bedingungen basieren. Der Rabatt kann automatisch angewendet werden, wenn die Bedingungen erfüllt sind oder wenn der Kunde einen gültigen Gutscheincode eingibt. Wenn der Rabatt angewendet wird, wird er im Warenkorb unter der Zwischensumme angezeigt. Eine Warenkorbpreisregel kann bei Bedarf für eine Saison oder eine Promotion verwendet werden, indem ihr Status und ihr Datumsbereich geändert werden.

## Für wen ist dieses Video?

- E-Commerce-Marketer
- Website-Manager

## Videoinhalt

>[!VIDEO](https://video.tv.adobe.com/v/343835?quality=12&learn=on)

## Preisanzeigeprobleme

Es gibt einige einzigartige Szenarien, in denen jedes Zeilenelement seinen Rabatt anzeigen muss, aber die Werte stimmen möglicherweise nicht genau überein. Der Grund dafür ist, dass ein Rabatt für Warenkorbpreise auf mehrere Produkte angewendet wird, die Werte jedoch nicht gleichmäßig in zwei Dezimalstellen unterteilt werden.

>[!BEGINSHADEBOX]

Warenkorbpreisregel = 10 % Rabatt, der auf 2 Produkte in der Warenkorbbedingung angewendet wird, damit die Preisregel wirksam wird: Gesamteinträge im Warenkorb sind 2 Aktionen, die den prozentualen Rabatt auf den Produktpreis anwenden und diesen Rabatt auf 10 anwenden

2 Artikel werden dem Warenkorb hinzugefügt, jeder Artikel kostet $19,95

Um den Rabattbetrag zu erhalten, multiplizieren Sie den Produktpreis mit 0,1.

19.95 x 0.1 = 1.995

Das ist das Problem, wir haben 3 Dezimalstellen anstelle von zwei. Die Umwandlung in Dollar ist jetzt ein Problem

>[!ENDSHADEBOX]

### Die Lösung

Wenn wir an den Website-Eigentümer denken, der die einzige Person ist, die von diesem Problem betroffen ist, wurde festgestellt, dass die Anzeige jedes bestellten Artikels mit dem in Dollar bereitgestellten Rabatt am besten geeignet war. Um sicherzustellen, dass der gesamte berechnete Bestellbetrag ordnungsgemäß berechnet wurde, wurde beschlossen, das erste Element zu gruppieren und die anderen die dritte Dezimalstelle abzugeben. Überprüfen Sie dieses Szenario:

>[!BEGINSHADEBOX]

Dieselbe 10-%-Rabatt wie die oben genannte Warenkorbregel. Fügen Sie 2 Produkte zum Warenkorb hinzu, die 19,95 sind

Jedes Produkt sollte 1,995 USD in Rabatten erhalten Produkt 1 - 19,95 x 0,1 = 1,995 2 - 19,95 x 0,1 = 1,995

Als Rabatt wird dem Kunden eine Gesamtsumme von 3,99 gewährt

Beim Anzeigen der Zeileneinträge für den Store-Eigentümer im Admin müssen wir das erste Element anpassen und bis zu 2.000 aufrunden. Das zweite Element, das wir die dritte Dezimalzahl Produkt 1 = 2.00 Produkt 2 = 1.99 ablegen

Der Gesamtrabatt der beiden Produkte entspricht nun, wenn sie zusammengerechnet werden, dem tatsächlichen Rabatt, der einem Kunden gewährt wird.
>[!ENDSHADEBOX]

Im Folgenden finden Sie einen Screenshot, der im Administrator für eine Bestellung mit diesem Szenario angezeigt wird:

![Admin-Ansicht mit geordneten Elementen mit unterschiedlichen Werten](../assets/commerce-admin-cart-price-rule-values-different.png)

### Andere mögliche Lösungen und Grund für ihre Nichtverwendung

>[!BEGINSHADEBOX]

Dieselbe 10-%-Rabatt wie die oben genannte Warenkorbregel. Fügen Sie 2 Produkte zum Warenkorb hinzu, die 19,95 sind

Jedes Produkt sollte 1.995 USD in Rabatten erhalten, aber wenn wir sie einfach aufrunden, wird zu viel Rabatt angezeigt.

Produkt 1 - 19.95 x 0.1 = 1.995 Produkt 2 - 19.95 x 0.1 = 1.995

Konvertieren in Aufrundung aller Elemente Produkt 1 Neuer Wert ist 2,00 Produkt 2 Neuer Wert ist 2,00

Tatsächlich wurde dem Kunden eine Gesamtsumme von 3,99 als Rabatt gewährt. Wenn wir jedoch aufschließen würden, würde dies zeigen, dass 4,00 USD gewährt wurden, und das ist falsch.

2.00 + 2.00 = $4.00

>[!ENDSHADEBOX]

Ähnliches Problem: Wenn die dritte Dezimalstelle für alle Elemente abgelegt wurde, wurde zu wenig Rabatt angezeigt.

>[!BEGINSHADEBOX]

Dieselbe 10-%-Rabatt wie die oben genannte Warenkorbregel. Fügen Sie 2 Produkte zum Warenkorb hinzu, die 19,95 sind

Für jedes Produkt sollten Rabatte in Höhe von 1.995 USD gewährt werden. Wenn wir jedoch nur die dritte Dezimalstelle ablegen, geschieht Folgendes: Produkt 1 - 19.95 x 0.1 = 1.995 Produkt 2 - 19.95 x 0.1 = 1.995

Konvertieren in Ablegen der dritten Dezimalzahl für alle Artikel Produkt 1 Neuer Wert ist 1,99 Produkt 2 Neuer Wert ist 1,99

Tatsächlich wurde dem Kunden eine Gesamtsumme von 3,99 als Rabatt gewährt. Wenn wir jedoch die dritte Dezimalstelle streichen, würde dies zeigen, dass 3,98 USD gegeben wurden, und das ist falsch.

1.99 + 1.99 = $3.98

>[!ENDSHADEBOX]


## Zusätzliche Ressourcen

- [Erstellen einer Warenkorbpreisregel - [!DNL Commerce] Handbuch zu Merchandising und Promotions](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create.html)
- [Couponcodes - [!DNL Commerce] Handbuch zu Merchandising und Promotions](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-coupon.html)
