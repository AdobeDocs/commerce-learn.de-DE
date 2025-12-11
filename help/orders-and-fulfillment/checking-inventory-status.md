---
title: Bestandsstatusprüfungen und Überlegungen zur Entwicklung und Leistung
description: Erfahren Sie mehr über Ideen und Überlegungen zur Durchführung von Inventarstatusprüfungen für Adobe Commerce.
feature: Best Practices, Inventory
topic: Development, Performance
old-role: Architect, Developer
role: Developer
level: Intermediate, Experienced
doc-type: Tutorial
duration: 0
last-substantial-update: 2024-05-09T00:00:00Z
jira: KT-15462
exl-id: bd2be562-5738-4398-8afb-2faeb0ba6b83
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 0%

---

# Bestandsstatusprüfungen und Überlegungen zur Entwicklung und Leistung

Die Genauigkeit des Inventars ist eine sehr wichtige Überlegung. Es gibt einige native Funktionen, die sicherstellen können, dass dieses Risiko so gering wie möglich ist, wie z. B. Auftragsrückstände und die Festlegung des Schwellenwerts für nicht vorrätige Artikel. Beide Themen finden sich unter [Experience League](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/backorders).

Es gibt Projekte und Anwendungsfälle, in denen für einen Adobe Commerce-Store Inventarstatusprüfungen in Echtzeit angefordert werden. In diesem Tutorial erfahren Sie, wie insight diese Konversation mit Überlegungen zur Entwicklung und Leistung handhabt.

## Überprüfen, ob diese Anfrage unbedingt erforderlich ist

Bereiten Sie sich darauf vor, mit so vielen Informationen wie möglich in das Gespräch zu treten. Das Wichtigste, was Sie tun müssen, ist sicherzustellen, dass die native Funktionalität für dieses Projekt nicht akzeptabel ist. Lesen Sie die Gründe für diese Anfrage, um zu überprüfen, ob die nativen Funktionen von Adobe Commerce diese Anfrage nicht erfüllen.

Eine weitere Überlegung betrifft die Kosten für die Entwicklung, das Testen und die Wartung dieser Funktion. Nur weil einige Stakeholder dies für notwendig halten, bedeutet dies nicht, dass es eine Anforderung ist. Mit der Inventarvalidierung außerhalb der Kernfunktionen von Adobe Commerce sind Kosten verbunden. Diese Kosten entstehen durch technische Nachschuld, weitere Tests und Validierungen sowie Nutzungsdokumentation und unterstützende Dokumente für die Architektur.

## Ermitteln der akzeptablen Kadenz für Inventaraktualisierungen

Versuchen Sie, Inventarprüfungen und deren Durchführung in drei Ansätzen in Betracht zu ziehen. Jede hat ihre Vorteile und Einschränkungen. Sie sind außerdem komplexer und erfordern mehr Tests und Nachdenken bei der Fehlerbehandlung. Denken Sie daran, dass es bei der Entscheidung für eine benutzerdefinierte Route zusätzliche Zuständigkeiten und Überlegungen gibt. Einige Beispiele sind ein Fallback-Prozess, Überwachung, Tests und Fehlerbehebung, die an das Entwicklungs-Team weitergeleitet werden. Einige gute Elemente sind die neue unterstützende Dokumentation, Schulung und Überwachung, um sicherzustellen, dass das Entwicklungs-Team die gesamte Funktion unterstützen kann. Ein zusätzlicher Nebeneffekt besteht darin, dass das Entwicklungs-Team die Verantwortung für den Prozess vollständig trägt und nicht mehr die native Funktionalität nutzt, die vom zentralen Adobe Commerce-Programm bereitgestellt wird. Der Adobe-Support kann bei diesem Anpassungsgrad nicht behilflich sein.

Der erste Ansatz besteht in der Verwendung der nativen -Funktion. Die Verwendung nativer Funktionen ist mit geringstem Risiko verbunden und bietet viele Vorteile. Dieser Ansatz bedeutet, dass Sie sich bei der Verwendung der Funktion auf die gesamte vorhandene Dokumentation und die von Adobe Commerce bereitgestellten Tutorials verlassen können. Die Bestandsverwaltung umfasst viele Aspekte. Daher sollte zuerst berücksichtigt werden, was im Lieferumfang der Anwendung enthalten ist. Es gibt jedoch Anwendungsfälle, in denen die im Handel zum Zeitpunkt der Bestellung gefundenen Daten möglicherweise nicht vollständig korrekt sind. Ein Beispiel dafür, wie die Dinge aus dem Takt geraten können, ist, dass Verkäufe außerhalb der Adobe Commerce-Anwendung direkt im Auftragsverwaltungssystem erlaubt sind. Ein Grund dafür ist, dass es, um sicherzustellen, dass die korrekten Inventarebenen in Adobe Commerce dargestellt werden, einer gewissen Integration bedarf, damit die Adobe Commerce-Informationen so genau wie möglich sind. Wenn Überverkäufe nicht akzeptabel sind, dann ist das Hinzufügen eines Schwellenwerts für nicht vorrätige Artikel eine gute Methode, den Verkauf von Artikeln zu stoppen, bevor Sie auf null kommen. Die native Synchronisierungsfunktion für Adobe Commerce beträgt maximal 1 Mal pro Tag. Dies ist für einige Anwendungsfälle ausreichend, kann aber für andere nicht häufig genug sein. Weitere Informationen finden [ unter „Geplanter Import ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-scheduled-import-export) Export“.

Der zweite Ansatz wäre `near real-time`. Beinahe in Echtzeit verwendet weiterhin die native Funktionalität. Dazu gehören jedoch einige zusätzliche Arbeiten zur Bereitstellung einer Integration, die Commerce häufig nutzt, um seinen Bestand nach einem Zeitplan zu aktualisieren. Zum Beispiel jede Stunde. Diese Option erfordert einige Überlegungen dazu, wie eine Integration funktionieren könnte, aber die Verwendung der „Bulk-API“ und die Bereitstellung von Middleware zur Umwandlung der Daten und deren Übertragung auf den Handel ist ein großartiger Ansatz. Sehen Sie sich die Verwendung von Adobe App Builder oder ähnlichen Plattformen an, um den Großteil der Arbeit zu erledigen und die Informationen häufiger an Adobe Commerce zu übertragen.

Der dritte Ansatz und der komplexeste mit dem höchsten Risiko und der größten Verantwortung sind Live-Inventarprüfungen in Echtzeit an eine externe API oder Datenquelle. Eine Bestandsprüfung in Echtzeit für ein externes System ist riskant und beinhaltet mehrere andere Elemente, die berücksichtigt werden müssen. Im Folgenden sind nur einige wenige Dinge aufgeführt, die ausgewertet werden müssen:

* Kann das externe System REST- oder GraphQL-Anfragen akzeptieren?
* Gibt es Beschränkungen für den Endpunkt, z. B. die X-Anzahl von Anfragen pro Minute, die nicht mit dem Website-Traffic übereinstimmen
* Was passiert mit der Antwortzeit unter Last?
* Was passiert, wenn die Antwortzeiten lang sind? Beenden Sie dies automatisch und verwenden Sie eine Ausweichoption wie das native Inventar.
* Welche Art der Überwachung ist verfügbar, um sicherzustellen, dass API-Anfragen innerhalb der Toleranzgrenzen liegen?

## Überlegungen zur nicht-nativen Bestandsverwaltung

Halten Sie die Anpassungen so unkompliziert wie möglich.
Wie flach kann die Organisation des Inventars sein, ist es nur 1 SKU und die Gesamtmenge des verfügbaren Lagerbestands ODER gibt es andere Attribute, die berücksichtigt werden müssen.

Wenn die Inventarinformationen relativ flach sind, z. B. eine SKU und die insgesamt verfügbare Menge, werden die Optionen für nahezu Echtzeit erweitert. Das Konzept der nahezu in Echtzeit bedeutet, dass ein Hintergrundvorgang stattfindet, bei dem der Bestand aus der Quelle erfasst und dann eine Speicher-Engine gefüllt wird, die als Antwort auf die Anfrage verwendet werden soll. Hierfür können Sie Elemente wie Redis, Mongo oder andere nicht-relationale Datenbanken verwenden. Diese Optionen sind schön, da sie sehr schnell sind und hervorragend für Schlüssel/Wert-Paare funktionieren. Wenn die Daten etwas komplexer sind, ist wahrscheinlich die Verwendung einer Beziehungsdatenbank innerhalb oder außerhalb der Commerce-Anwendung erforderlich. Durch die Auslagerung aus der Commerce-Datenbank bleibt die zentrale Commerce-Anwendung von diesen Transaktionen isoliert. Weitere Vorteile sind das Speichern der E/A-Vorgänge aus der Commerce-Anwendung, CPU, RAM und anderen. Anstatt die Ressourcen der Adobe Commerce-Anwendungs-Server zu verwenden, nutzen Sie die neuen APIs, um die Daten aus dem Offsite-Speicher abzurufen.  Dazu wird wahrscheinlich eine Middleware benötigt, die bei der Umwandlung von Daten hilft. Stellen Sie dann sicher, dass die aufrufende Anwendung das Ergebnis erwartungsgemäß abrufen kann. Durch die Verwendung von Adobe App Builder mit API Mesh können die Daten transformiert und ordnungsgemäß formatiert zurückgegeben werden.

Die Verwendung von Adobe App Builder mit API Mesh ist auch eine gute Option, wenn mehrere Bestandsquellen vorhanden sind.


## Verschieben der Ausführungslogik an einen prozessexternen Speicherort

Adobe Developer App Builder bietet ein einheitliches Erweiterungs-Framework für Drittanbieter zur Integration und Erstellung benutzerdefinierter Erlebnisse, um Adobe-Lösungen zu erweitern. Adobe Commerce kann Adobe Developer App Builder verwenden. Dies wäre ein hervorragender Anwendungsfall für die Erweiterung einiger Funktionen, die normalerweise in der Hauptanwendung auftreten, und für die Verschiebung von außerhalb. Durch das Entfernen von Funktionen aus dem Commerce-Programm wird die Anzahl der Module und die Komplexität des Commerce-Programms reduziert. Weniger Anpassungen während des Prozesses reduzieren wiederum die Komplexität von Upgrades und Wartungsarbeiten.

Um zu erfahren, wie dies erreicht werden kann, hat das Team von Adobe eine Dokumentation erstellt, die eine großartige Inspirationsquelle sein und funktionierende Code-Beispiele bieten kann. Wenn ein Käufer ein Produkt in den Warenkorb legt, prüft ein Inventarverwaltungssystem eines Drittanbieters, ob der Artikel auf Lager ist. Wenn dies der Fall ist, lassen Sie das Produkt hinzufügen. Andernfalls wird eine Fehlermeldung angezeigt.  Code-Beispiele und weitere Informationen finden Sie unter [Webhook-Anwendungsfälle](https://developer.adobe.com/commerce/extensibility/webhooks/use-cases/#add-product-to-cart).

## Wann Bestandsprüfungen durchzuführen sind

Wann überprüft werden muss, ob noch Inventar verfügbar ist, wird letztendlich der Geschäftsinhaber entscheiden, der Softwarearchitekt mit einigen Beiträgen von anderen wichtigen Stakeholdern. Einige geeignete Zeiten umfassen das Hinzufügen eines Artikels zum Warenkorb und den Eintritt in den Checkout-Workflow. Alle anderen Ereignisse fügen den Backend-Systemen einfach Last hinzu, wenn dies möglicherweise nicht erforderlich ist. Das Ziel besteht darin, ein Inventarproblem nur dann zu erfassen, wenn es von höchster Bedeutung ist. Andere Prüfungen sind vielleicht wünschenswert, aber wenn sie sich auf das Gesamtziel für Bestandsstatusprüfungen auswirken können, sollten sie sorgfältig abgewogen und nur zulässig sein, wenn die geschäftlichen Stakeholder oder andere das potenzielle Risiko einer zusätzlichen Belastung der Backend-Systeme kennen.

## Ermitteln der Inventarquelle

Eine umfassende Untersuchung der externen Bestandsquelle ist erforderlich. Auszuwerten sind die verfügbaren API-Optionen, die Unterstützung für GraphQL und die erwarteten Antwortzeiten. Wenn die Inventarquelle eine begrenzte Verbindungsbandbreite hat oder nie in einer Echtzeitanfrage verwendet werden sollte, ist die Möglichkeit zur Verwendung ausgeschlossen und der Architekt muss stattdessen Fast-Echtzeit in Betracht ziehen.  Wenn die API-Anfragezeiten die definierten Parameter überschreiten, wird dies auch als praktikable Option ausgeschlossen.  Ein Beispiel hierfür wären API-Antworten mit einer Größe von 200 MS® für einmalige Anfragen, die jedoch bei moderater Last auf 500 bis 900 MS® ansteigen.  Dies würde sich wahrscheinlich noch verschlimmern, wenn mehr Daten geladen würden und keine Live-Inventaranrufe mehr verfügbar wären.

Testen Sie die API-Antwortzeiten unbedingt mit einfachen Anfragen sowie mit einem hohen Volumen, das dem erwarteten Traffic auf der Live-Website ähnelt. Denken Sie daran, alle Bereiche von Commerce gleichzeitig zu testen, um reale Szenarien zu simulieren. Wenn ein Live-Inventaranruf auf Produktseiten erfolgen soll, muss beim Anzeigen und Bearbeiten eines Warenkorbs und während des Checkouts beim Auslastungstest alles gleichzeitig simuliert werden, um das tatsächliche Kundenverhalten und die Erwartungen an einen Store zu imitieren.

## Fallback-Optionen

Wenn die Bestandsquelle ausgefallen ist und die Überwachung verfügbar ist, wird die Verwendung der nativen Funktion von Adobe Commerce empfohlen. Mit einer ordnungsgemäßen Überwachung kann sich das Kundenerlebnis jedoch dynamisch ändern, um den Verlust von Inventarprüfungen in Echtzeit widerzuspiegeln. Dies kann bedeuten, dass ein Verkauf oder eine Veranstaltung vorzeitig storniert oder von der Anzeige entfernt wird, um einen Überverkauf zu vermeiden. Die Erwartung, was zu tun ist, wenn die Bestandsquelle aus irgendeinem Grund ausfällt, muss mit dem Ladenbesitzer überlegt und besprochen werden, damit jeder über jeden automatischen Prozess informiert ist, der unter diesen unglücklichen Umständen die Führung übernimmt.

## Schlussfolgerung

Die Entscheidung, Inventarprüfungen in Echtzeit durchzuführen, ist von großer Bedeutung. Der Entwickler oder Architekt muss sicherstellen, dass Website-Verantwortlicher, Entwicklungsteam und andere vollständig geschult sind und alle Vorteile und potenziellen Fallstricke kennen. Durch die Bereitstellung eines durchdachten Plans, der die Gründe abdeckt, und eines Fallback-Prozesses ist der Schlüssel zum Erfolg.

Live-Inventarprüfungen können durchgeführt werden, erfordern jedoch Recherchen und Überlegungen zu Tests und Validierungen während des QA-Zyklus. Sicherstellen, dass Belastungstests und automatisierte End-to-End-Tests sicherstellen, dass alle potenziellen Probleme erfasst und getriggert werden.

Indem Sie überlegen, welche Aktionen ausgeführt werden sollen, wenn bei der Überwachung ein Trend fehlgeschlagener Aufrufe an das externe System erkannt wird oder die Antwortzeiten oberhalb akzeptabler Schwellenwerte liegen, können Sie die Website online bleiben und den Kunden so wenig wie möglich Ärger bereiten. Fallback-Optionen können so einfach sein wie das Deaktivieren der externen Inventarprüfungen und die Verwendung der nativen Funktion. Sie können aber auch so weit entwickelt sein wie das Deaktivieren einer Promotion, das Benachrichtigen des Entwicklungs-Teams über eskalierende Probleme oder sogar das Umleiten von Anfragen an ein zweites oder drittes Backend-System, falls verfügbar. Wie der Ausweichmechanismus angewendet wird, sollte nur als tatsächliche Implementierung betrachtet werden, da jede Integration irgendwann Probleme aufweist. Alles, was automatisiert ist oder manuelles Handeln erfordert, sollte klar dokumentiert werden.
