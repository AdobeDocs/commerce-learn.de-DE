---
title: 'Bestandsstatusprüfungen: Entwicklung und Leistung'
description: Erfahren Sie, wie Sie bewerten können, ob in Adobe Commerce Inventarprüfungen in Echtzeit erforderlich sind, und lesen Sie Überlegungen zur Entwicklung und Leistung für Ihren Store.
feature: Best Practices, Inventory
topic: Development, Performance
role: Developer
level: Intermediate, Experienced
doc-type: Tutorial
duration: 496
last-substantial-update: 2024-05-09
jira: KT-15462
exl-id: bd2be562-5738-4398-8afb-2faeb0ba6b83
TQID: https://experienceleague.adobe.com/IfBm4JSpLXViUNTHo7amAL6GIYJsC4O-rdITtbqJV24
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
subfeature_v2:
  - id: b01a71b7-d17a-42b2-a9ac-af4b8d9d2ef5
    internal-label: 2FA
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
    internal-label: B2B
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
source-git-commit: fcf0f5116ba75bd618f4ed80591ecc96132cdb45
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 0%
---
# Bestandsstatusprüfungen und Überlegungen zur Entwicklung und Leistung

Die Genauigkeit des Inventars ist eine wichtige Überlegung. Es gibt einige native Funktionen, die sicherstellen können, dass dieses Risiko so gering wie möglich ist, wie z. B. Auftragsrückstände und die Festlegung des Schwellenwerts für nicht vorrätige Artikel. Beide Themen finden sich unter [Adobe Experience League](https://experienceleague.adobe.com/de/docs/commerce-admin/inventory/configuration/backorders) für weitere Erläuterungen.

Es gibt Projekte und Anwendungsfälle, in denen für einen Adobe Commerce-Store Inventarstatusprüfungen in Echtzeit angefordert werden. In diesem Tutorial erfahren Sie, wie insight diese Konversation mit Überlegungen zur Entwicklung und Leistung handhabt.

## Überprüfen, ob diese Anfrage erforderlich ist

Bereiten Sie sich darauf vor, die Anfrage mit so vielen Informationen wie möglich zu besprechen. Das Wichtigste, was Sie tun müssen, ist sicherzustellen, dass die native Funktionalität für dieses Projekt nicht akzeptabel ist. Lesen Sie die Gründe für diese Anfrage, um zu überprüfen, ob die nativen Funktionen von Adobe Commerce diese Anfrage nicht erfüllen.

Eine weitere Überlegung betrifft die Kosten für die Entwicklung, das Testen und die Wartung dieser Funktion. Die Meinung eines Stakeholders macht etwas nicht unbedingt zu einer Anforderung. Mit der Inventarvalidierung außerhalb der Kernfunktionen von Adobe Commerce sind Kosten verbunden. Diese Kosten entstehen in Form von technischem Schuldendienst, mehr Tests und Validierungen sowie Nutzungsdokumenten und Begleitdokumenten für die Architektur.

## Ermitteln der akzeptablen Kadenz für Inventaraktualisierungen

Versuchen Sie, Inventarprüfungen und deren Durchführung in drei Ansätzen in Betracht zu ziehen. Jede hat ihre Vorteile und Einschränkungen. Sie sind außerdem komplexer und erfordern mehr Tests und Nachdenken bei der Fehlerbehandlung. Denken Sie daran, dass es bei der Entscheidung, eine benutzerdefinierte Lösung zu implementieren, zusätzliche Zuständigkeiten und Überlegungen gibt. Beispiele sind ein Fallback-Prozess, Überwachung, Tests und Fehlerbehebung, die dem Entwicklungs-Team obliegen. Einige gute Elemente sind die neue unterstützende Dokumentation, Schulung und Überwachung, um sicherzustellen, dass das Entwicklungs-Team die gesamte Funktion unterstützen kann. Ein Nebeneffekt besteht darin, dass das Entwicklungs-Team für den Prozess verantwortlich ist und nicht mehr die native Funktionalität nutzt, die von der zentralen Adobe Commerce-Anwendung bereitgestellt wird. Der Adobe-Support kann bei diesem Anpassungsgrad nicht behilflich sein.

Der erste Ansatz besteht in der Verwendung der nativen -Funktion. Die Verwendung nativer Funktionen ist mit geringstem Risiko verbunden und bietet viele Vorteile. Dieser Ansatz bedeutet, dass Sie sich bei der Verwendung der Funktion auf die gesamte vorhandene Dokumentation und die von Adobe Commerce bereitgestellten Tutorials verlassen können. Die Bestandsverwaltung hat viele Aspekte. Verwenden Sie daher zuerst, was im Lieferumfang der Anwendung enthalten ist. Es gibt jedoch Anwendungsfälle, in denen die im Handel zum Zeitpunkt der Bestellung gefundenen Daten nicht korrekt sind. Ein Beispiel für die Synchronisierung von Daten ist, dass Verkäufe außerhalb der Adobe Commerce-Anwendung direkt im Order Management-System zulässig sind. Ein Grund dafür ist, dass um sicherzustellen, dass die korrekten Inventarebenen in Adobe Commerce dargestellt werden, eine Art Integration erforderlich ist, damit die Adobe Commerce-Informationen so genau wie möglich sind. Wenn Überverkäufe nicht akzeptabel sind, dann ist das Hinzufügen eines Schwellenwerts für nicht vorrätige Artikel eine gute Methode, den Verkauf von Artikeln zu stoppen, bevor Sie auf null kommen. Die native Synchronisierungsfunktion für Adobe Commerce beträgt maximal 1 Mal pro Tag. Diese Häufigkeit ist für einige Anwendungsfälle ausreichend, für andere jedoch nicht häufig genug. Bitte lesen Sie [Geplanter Import und Export](https://experienceleague.adobe.com/de/docs/commerce-admin/systems/data-transfer/data-scheduled-import-export) für detaillierte Informationen.

Der zweite Ansatz ist `near real-time`. Beinahe in Echtzeit verwendet weiterhin die native Funktionalität. Dazu gehören jedoch einige zusätzliche Arbeiten zur Bereitstellung einer Integration, die Commerce häufig nutzt, um seinen Bestand nach einem Zeitplan zu aktualisieren. Zum Beispiel jede Stunde. Diese Option erfordert Überlegungen zur Funktionsweise einer Integration, aber die Verwendung der „Bulk-API“ und die Verwendung einer Middleware zur Umwandlung der Daten und zur Übertragung auf den Handel ist ein großartiger Ansatz. Sehen Sie sich die Verwendung von Adobe App Builder oder ähnlichen Plattformen an, um den Großteil der Arbeit zu erledigen und die Informationen häufiger an Adobe Commerce zu übertragen.

Der dritte Ansatz und der komplexeste mit dem höchsten Risiko und der größten Verantwortung sind Live-Inventarprüfungen in Echtzeit an eine externe API oder Datenquelle. Eine Bestandsprüfung in Echtzeit für ein externes System ist riskant und beinhaltet mehrere andere Elemente, die berücksichtigt werden müssen. Im Folgenden finden Sie einige weitere Aspekte, die ausgewertet werden müssen:

* Kann das externe System REST- oder GraphQL-Anfragen akzeptieren?
* Gibt es Einschränkungen für den Endpunkt, z. B. die X-Anzahl von Anfragen pro Minute, die nicht mit dem Website-Traffic übereinstimmen?
* Was passiert mit der Antwortzeit unter Last?
* Was passiert, wenn die Antwortzeiten lang sind? Beenden Sie dies automatisch und verwenden Sie eine Ausweichoption wie das native Inventar.
* Welche Art der Überwachung ist verfügbar, um sicherzustellen, dass API-Anfragen innerhalb der Toleranzgrenzen liegen?

## Überlegungen zur nicht nativen Bestandsverwaltung

Halten Sie die Anpassungen so unkompliziert wie möglich.
Wie flach kann die Organisation des Inventars sein, ist es 1 SKU und der Gesamtbetrag des verfügbaren Lagerbestands ODER gibt es andere Attribute, die berücksichtigt werden müssen.

Wenn die Inventarinformationen relativ flach sind, z. B. eine SKU und die insgesamt verfügbare Menge, werden die Optionen für nahezu Echtzeit erweitert. Das Konzept der nahezu in Echtzeit bedeutet, dass ein Hintergrundvorgang stattfindet, bei dem der Bestand aus der Quelle erfasst und dann eine Speicher-Engine gefüllt wird, die als Antwort auf die Anfrage verwendet werden soll. Hierfür können Sie Elemente wie Redis, Mongo oder andere nicht-relationale Datenbanken verwenden. Diese Optionen sind schnell und eignen sich hervorragend für Schlüssel/Wert-Paare. Wenn die Daten etwas komplexer sind, ist die Verwendung einer Beziehungsdatenbank entweder innerhalb oder außerhalb der Commerce-Anwendung erforderlich. Durch die Auslagerung aus der Commerce-Datenbank bleibt die zentrale Commerce-Anwendung von diesen Transaktionen isoliert. Weitere Vorteile sind das Speichern der E/A-Vorgänge aus der Commerce-Anwendung, CPU, RAM und anderen. Um Ressourcen von den Adobe Commerce-Anwendungs-Servern zu sparen, nutzen Sie die neuen APIs, um die Daten aus dem Offsite-Speicher abzurufen. Für diesen Prozess ist eine Middleware erforderlich, die bei der Umwandlung von Daten hilft. Stellen Sie dann sicher, dass die aufrufende Anwendung das Ergebnis erwartungsgemäß abrufen kann. Durch die Verwendung von Adobe App Builder mit API Mesh können die Daten transformiert und ordnungsgemäß formatiert zurückgegeben werden.

Die Verwendung von Adobe App Builder mit API Mesh ist auch eine gute Option, wenn mehrere Bestandsquellen vorhanden sind.


## Verschiebt die Ausführungslogik aus dem Prozess

Adobe Developer App Builder bietet ein einheitliches Erweiterungs-Framework für Drittanbieter zur Integration und Erstellung benutzerdefinierter Erlebnisse, um Adobe-Lösungen zu erweitern. Adobe Commerce kann Adobe Developer App Builder verwenden. Dieser Ansatz ist ein hervorragender Anwendungsfall für die Erweiterung einiger Funktionen, die normalerweise in der Kernanwendung auftreten, und verschiebt sie von einem Standort in einen anderen. Durch das Entfernen von Funktionen aus dem Commerce-Programm wird die Anzahl der Module und die Komplexität des Commerce-Programms reduziert. Weniger Anpassungen während des Prozesses reduzieren wiederum die Komplexität von Upgrades und Wartungsarbeiten.

Als Anregung für die Umsetzung dieser Aufgabe hat das Team von Adobe eine Dokumentation erstellt, die eine großartige Inspirationsquelle darstellt und funktionierende Code-Beispiele bereitstellt. Wenn ein Käufer ein Produkt in den Warenkorb legt, prüft ein Inventarverwaltungssystem eines Drittanbieters, ob der Artikel auf Lager ist. Wenn dies der Fall ist, lassen Sie das Produkt hinzufügen. Andernfalls wird eine Fehlermeldung angezeigt. Code-Beispiele und weitere Informationen finden Sie unter [Webhook-Anwendungsfälle](https://developer.adobe.com/commerce/extensibility/webhooks/use-cases/#add-product-to-cart).

## Wann Bestandsprüfungen durchzuführen sind

Wann überprüft werden muss, ob noch Inventar verfügbar ist, hängt von den geschäftlichen Stakeholdern ab. Der Software-Architekt erhält dabei einige Informationen von anderen wichtigen Stakeholdern. Zu einigen geeigneten Zeiten gehören das Hinzufügen eines Artikels zum Warenkorb und der Eintritt in den Checkout-Workflow. Alle anderen Ereignisse fügen den Backend-Systemen Last hinzu, wenn dies nicht erforderlich ist. Das Ziel besteht darin, ein Inventarproblem nur dann zu erfassen, wenn es von höchster Bedeutung ist. Berücksichtigen Sie sorgfältig andere Prüfungen, die sich auf das Gesamtziel für Bestandsstatusprüfungen auswirken, und lassen Sie diese nur zu, wenn sich die Beteiligten des potenziellen Risikos einer zusätzlichen Belastung bewusst sind.

## Ermitteln der Inventarquelle

Eine umfassende Untersuchung der externen Bestandsquelle ist erforderlich. Auszuwerten sind die verfügbaren API-Optionen, die Unterstützung für GraphQL und die erwarteten Antwortzeiten. Wenn die Inventarquelle eine begrenzte Verbindungsbandbreite hat oder nie in einer Echtzeitanfrage verwendet werden sollte, ist die Möglichkeit zur Verwendung ausgeschlossen und der Architekt muss stattdessen Fast-Echtzeit in Betracht ziehen. Wenn die API-Anfragezeiten die definierten Parameter überschreiten, ist dies keine praktikable Option. Ein Beispiel für dieses Verhalten ist, dass die API-Antworten bei einmaligen Anfragen 200 ms betragen, bei moderater Last jedoch auf 500 bis 900 ms ansteigen. Diese Situation verschlimmert sich mit zunehmender Auslastung und schließt Live-Inventaranrufe aus.

Testen Sie die API-Antwortzeiten unbedingt mit einfachen Anfragen sowie mit einem hohen Volumen, das dem erwarteten Traffic auf der Live-Website ähnelt. Denken Sie daran, alle Bereiche von Commerce gleichzeitig zu testen, um reale Szenarien zu simulieren. Wenn Live-Inventaranrufe auf Produktseiten, im Warenkorb und während des Checkouts erfolgen, müssen Lasttests alle diese gleichzeitig simulieren, um das tatsächliche Kundenverhalten zu imitieren.

## Fallback-Optionen

Wenn die Bestandsquelle heruntergefahren ist und die Überwachung verfügbar ist, wird die Verwendung der nativen Funktion von Adobe Commerce empfohlen. Mit einer ordnungsgemäßen Überwachung kann sich das Kundenerlebnis jedoch dynamisch ändern, um den Verlust von Inventarprüfungen in Echtzeit widerzuspiegeln. Dies bedeutet, dass ein Verkauf oder eine Veranstaltung vorzeitig abgebrochen oder von der Anzeige entfernt wird, um einen Überverkauf zu vermeiden. Besprechen Sie den Fallback-Plan mit dem Store-Eigentümer, damit jeder den automatischen Prozess versteht, der übernommen wird, wenn die Bestandsquelle ausfällt.

## Schlussfolgerung

Die Entscheidung, Inventarprüfungen in Echtzeit durchzuführen, ist von großer Bedeutung. Der Entwickler oder Architekt muss sicherstellen, dass Website-Verantwortlicher, Entwicklungsteam und andere vollständig geschult sind und alle Vorteile und potenziellen Fallstricke kennen. Durch die Bereitstellung eines durchdachten Plans, der die Gründe abdeckt, und eines Fallback-Prozesses ist der Schlüssel zum Erfolg.

Live-Inventarprüfungen können durchgeführt werden, erfordern jedoch Recherchen und Überlegungen zu Tests und Validierungen während des QA-Zyklus. Sicherstellen, dass Belastungstests und automatisierte End-to-End-Tests sicherstellen, dass alle potenziellen Probleme erfasst und getriggert werden.

Wenn bei der Überwachung fehlgeschlagene Aufrufe oder langsame Antwortzeiten erkannt werden, führen Sie Aktionen durch, um die Website online zu halten und die Kundenreizung zu minimieren. Die Fallback-Optionen reichen von der Verwendung nativer Funktionen bis zur Deaktivierung von Promotions, der Benachrichtigung des Entwicklungs-Teams oder der Umleitung von Anfragen an ein sekundäres Backend-System. Die Implementierung des Ausweichmechanismus sollte ebenso sorgfältig geplant werden wie die tatsächliche Integration, da bei jedem System irgendwann Probleme auftreten. Alles, was automatisiert ist oder manuelles Handeln erfordert, sollte klar dokumentiert werden.
