---
title: 'Erstellen einer vollständigen Demo zu aufgeteilten Zahlungen - POC: App Builder'
description: In dieser Luma-Demo erfahren Sie, wie Sie Zahlung, REST, App Builder I/O und Benutzende aufteilen, damit sie Arbeit annehmen/ablehnen. Zusätzlich erhalten Sie eine konfigurierbare Summe für Vorbestellungen, die den Warenkorb blockieren kann.
feature: App Builder, Paas, Payments
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Technical Video
duration: 933
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 1e2c7e0e6d0f2d174b88406ce3fb7c787676ecee
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 0%

---

# Erstellen einer vollständigen Demo zu aufgeteilten Zahlungen - POC: App Builder

Dies ist die durchgängige Anleitung zum Machbarkeitsnachweis für die Aufspaltung von Zahlungen, der auf Adobe Commerce und Adobe App Builder basiert. In der Demo wird davon ausgegangen, dass Sie bereits KI-Tools verwendet haben, und eine Eingabeaufforderung angezeigt, um die im Prozess befindliche Commerce-Erweiterung und die App Builder-App zu erstellen. In diesem Video wird gezeigt, was passiert, nachdem dieser Code zusammengeführt, auf einer Adobe Commerce Cloud-Website unter Verwendung des nativen Luma-Designs bereitgestellt und das App Builder-Projekt live ist.

Ein Käufer zahlt mit Teil-Bargeld und Teil-**[!UICONTROL Store Credit]**. Commerce verfügt über das synchrone Auschecken und die APIs, die die Storefront benötigt. App Builder übernimmt die Orchestrierung, Benutzer-Workflows und I/O-Ereignisnutzer. Die Referenzimplementierung verwendet ein Commerce-Projekt (PaaS) und die native Kasse von Luma anstelle einer Edge Delivery Services-Storefront, die immer noch ein häufiger Pfad für viele Händler ist. Wenn Sie **Adobe Commerce as a Cloud Service** in einer anderen Topologie verwenden, bleibt der App Builder-Code ähnlich, aber Storefront und laufende Arbeit würden anders aussehen. Für On-Premise, Self-Hosting und Commerce in der Cloud auf Luma zeigt dieses Video eine praktische Aufteilung zwischen Prozesscode und App Builder für neue Funktionen.

## Video

>[!VIDEO](https://video.tv.adobe.com/v/3484087?learn=on)

## Für wen ist dieses Video bestimmt?

* Technische Architekten planen die Erweiterbarkeit von Commerce
* Entwickelnde, die Checkout- und Integrationen implementieren
* Implementierungsteams, die eine realistische Aufteilung zwischen PHP und App Builder benötigen

## Einrichten des Szenarios in der Storefront

Das Demo-Konto ist **[!UICONTROL Store Credit]** und Sie sehen dieses Guthaben an der Kasse. Fügen Sie Produkte hinzu, bis die Bestellsumme etwa 80 $ beträgt. Diese Größe bietet Ihnen Raum, sowohl den erfolgreichen Akzeptierungspfad als auch den Ablehnungspfad anzuzeigen, ähnlich wie bei einer Kartenverschlechterung, ohne dass die Mathematik Sie bekämpft.

**[!UICONTROL Split payment]** wird nur angemeldeten Kundinnen und Kunden angeboten, da die Sitzung Storeguthaben offenlegen muss. Beim Auschecken eines Gastes wird die Aufspaltungsoption nicht angezeigt.

1. Wählen Sie im **[!UICONTROL Payment]** Schritt die Bargeldmethode aus (in der Demo wird **[!UICONTROL Cash on delivery]** in &quot;**Cash“**).
1. Unter der Zahlungsmethode wird ein aufgeteilter Zahlungsbereich angezeigt. Das Feld Bargeld wird auf die Bestellsumme vorausgefüllt und die Komponente liest **[!UICONTROL Store Credit]** aus der Sitzung.
1. Für einen ~$80 Warenkorb legen Sie **$50** Cash und **$30** Store-Guthaben fest, sodass die Komponente $50 + $30 = $80 anzeigt.
1. Wenn die Beträge gültig sind, geben Sie die Bestellung auf.

Die Benutzeroberfläche führt einen Aufruf an eine neue **[!UICONTROL Commerce]**-REST-API für die Aufspaltung durch. Das Auschecken bleibt synchron: Commerce wendet das Store-Guthaben an, speichert aufgeteilte Zeilen für die Bestellung und gibt ein I/O-Ereignis aus, das App Builder später verbraucht. Die Erfolgsseite wird sofort vom Kunden angezeigt.

## Überprüfen Sie die Bestellung im Commerce Admin.

Öffnen Sie in **[!UICONTROL Sales]** > **[!UICONTROL Orders]** die neue Bestellung. Der **[!UICONTROL Payment information]** Bereich zeigt die Aufspaltung, zum Beispiel **$ 50** Bargeld und **$ 30** Warenkorb. Der Status ist **Ausstehend** wenn Bargeld noch nicht eingezogen wurde. Die Speichergutschrift wird bereits bei der Auftragserstellung übernommen.

**[!UICONTROL Comments]** können von App Builder hinzugefügten Text enthalten. Der **[!UICONTROL Payment orchestrator action]** in App Builder hat das E/A-Ereignis erhalten, die Aufspaltungsbeträge überprüft und authentifizierten REST verwendet, um Kommentare anzuhängen. **[!UICONTROL Commerce]** behandelt dies wie jeden anderen REST-Aufruf und muss den Autor nicht kennen.

## Verwenden des App Builder-Benutzer-Dashboards (ERP oder Back Office)

Ein einfaches HTML-Erlebnis wird als **[!UICONTROL App Builder]** Web-Aktion ausgeführt (keine **[!UICONTROL Admin]** für diese Ansicht). Das Dashboard ruft die **[!UICONTROL Commerce Order]** REST-API auf und filtert auf **Ausstehend** sodass Sie die 50-Dollar-Bareinlage finden können.

Normalerweise integrieren Sie dieses Muster in ein ERP- oder Betrug-Tool. Es werden zwei Aktionen demonstriert:

* **Akzeptieren** - Bestätigt, dass Bargeld empfangen wurde (in der Produktion häufig eine automatisierte Post von einer Kassenlade oder einem Ladensystem).
* **Ablehnen** - simuliert Betrug oder einen fehlgeschlagenen Erfassungsschritt (in der Produktion, in der Regel von Ihrem Risiko-Service aus automatisiert).

**Akzeptieren und Abschließen der Bestellung**

1. Verwenden Sie in der **[!UICONTROL App Builder]**-App **Akzeptieren**, um Bargeld zu bestätigen.
1. Die App ruft einen neuen **[!UICONTROL Commerce]**-Endpunkt auf, der die Geldlinie abschließt. Der grundlegende Auftragsfluss (Rechnungsstellung und in diesem Build eine automatisierte Lieferung) wird mit nativem **[!UICONTROL Commerce]** ausgeführt. Keiner dieser Pfade erfordert einen Menschen in **[!UICONTROL Admin]**. Orchestrierung und der Endpunkt sind in App Builder verfügbar.

Aktualisieren Sie dieselbe Bestellung in **[!UICONTROL Admin]**: der Status wechselt zu **Abgeschlossen** wenn das Bargeld akzeptiert wird, mit Rechnung und, wenn das Produkt versandfähig ist, einer Lieferung, um den gesamten Lebenszyklus der Demo zu verkürzen.

**Ablehnen und abbrechen**

1. Öffnen Sie eine vordefinierte Bestellung, die sich noch im Ablehnungsszenario befindet.
1. Verwenden Sie in der **[!UICONTROL App Builder]**-App **Ablehnen**, um einen Betrug oder einen Sammlungsfehler zu simulieren.
1. In **[!UICONTROL Admin]** lautet die Bestellung **Storniert**. Die Historie zeigt den Status „Bargeld abgelehnt“, Kommentare erläutern das Ergebnis, der Käufer wurde nicht mit der Ladenkreditlinie belastet, als wäre es ein endgültiger Verkauf, und die Ladenkreditrechnung wird mit der Stornierung ungültig gemacht. Ein Produktionssystem würde den Kunden auch benachrichtigen und alle Lagerbestände oder Serviceleistungen freigeben.

## Schwellenwert für die Bestellsumme (Validierung vor der Erstellung der Bestellung)

App Builder- oder **[!UICONTROL Commerce]**-Konfiguration kann Validierungsregeln unterstützen. Dieser Build blockiert Bestellungen über **$ 100** im Warenkorbwert (eine Demo-Begrenzung, die Sie ändern können). Eine Werteprüfung ist nicht die gängigste Geschäftsregel - Bestands- oder Verfügbarkeitsprüfungen sind eher typisch. Sie zeigt jedoch, dass die Validierung **[!UICONTROL Payment]** in **[!UICONTROL Commerce]** ausgeführt werden kann, bevor eine Bestellung erstellt wird, während App Builder weiterhin die Folgeautomatisierung handhabt.

1. Fügen Sie Produkte hinzu, bis die Gesamtsumme über **$100** liegt.
1. Die Aufspaltung **[!UICONTROL UI]** weiterhin angezeigt. Das Ergebnis „Überschreibung“ wird nur in **Reihenfolge“**.
1. Der Käufer sieht einen allgemeinen Fehler wie **Zahlung konnte nicht verarbeitet werden. Bitte erneut versuchen oder den Support kontaktieren.**
1. Der **[!UICONTROL cart]** bleibt unverändert, sodass der Kunde die Gesamtsumme senken, eine andere Methode auswählen oder sich an den Support wenden kann.

Hier kann eine Risikobewertung, eine Regionsregel oder Ähnliches eingefügt werden. **[!UICONTROL Commerce]** blockiert die Reihenfolge, und **[!UICONTROL App Builder]** können Benachrichtigungen und Fallarbeiten im Nachhinein besitzen.

## Commerce On-Premise, Commerce in der Cloud und **Adobe Commerce as a Cloud Service**

In dieser exemplarischen Vorgehensweise werden **[!UICONTROL Adobe Commerce]** auf einer von Ihnen verwalteten Infrastruktur oder **[!UICONTROL Commerce in the cloud]** (PaaS) mit einer herkömmlichen Storefront abgeglichen. Für **[!UICONTROL Adobe Commerce as a Cloud service]** (SaaS) mit einem anderen Frontend und ohne In-Process-Modul in dieser Form sind die App Builder-Teile weitgehend gleich, während Storefront- und Erweiterungsarbeiten unterschiedlich wären. In allen Fällen gilt das gleiche Prinzip: Lassen Sie **[!UICONTROL Commerce]** tun, was innerhalb der **[!UICONTROL Commerce]**-Anfrage geschehen muss, und verwenden Sie **[!UICONTROL App Builder]** für den Rest des Erlebnisses.

{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
