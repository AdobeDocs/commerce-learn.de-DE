---
title: Entwicklung und Leistungsaspekte bei Bestandsstatusprüfungen
description: Erfahren Sie mehr über Ideen und Überlegungen zum Durchführen von Bestandsstatusprüfungen für Adobe Commerce.
feature: Best Practices, Inventory
topic: Development, Performance
role: Architect, Developer
level: Intermediate, Experienced
doc-type: Tutorial
duration: 0
last-substantial-update: 2024-05-09T00:00:00Z
jira: KT-15462
source-git-commit: e171d0a0b6272db5e9ca88992a73395af57072ed
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 0%

---


# Entwicklung und Leistungsaspekte bei Bestandsstatusprüfungen

Die Genauigkeit beim Inventar ist eine sehr wichtige Überlegung. Es gibt einige native Funktionen, die dazu beitragen können, dass dieses Risiko so gering wie möglich ist, wie z. B. Rückbestellungen und die Festlegung des Schwellenwerts für &quot;nicht vorrätig&quot;. Beide Themen sind zu lesen unter [Experience League](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/backorders) für weitere Erläuterungen.

Es gibt Projekte und Anwendungsfälle, bei denen Bestandsstatusprüfungen in Echtzeit für einen Adobe Commerce-Store angefordert werden. Dieses Tutorial bietet Einblicke in die Handhabung dieses Gesprächs mit Entwicklungs- und Leistungsaspekten.

## Überprüfen, ob diese Anforderung absolut erforderlich ist

Bereiten Sie sich darauf vor, mit so vielen Informationen wie möglich in das Gespräch einzutreten. Am wichtigsten ist es zu überprüfen, ob native Funktionen für dieses Projekt nicht akzeptabel sind. Finden Sie die Gründe für diese Anfrage, um zu überprüfen, ob die nativen Funktionen von Adobe Commerce diese Anfrage nicht erfüllen.

Ein weiterer Aspekt sind die Kosten für die Entwicklung, den Test und die Pflege dieser Funktion. Nur weil einige Interessenträger dies für notwendig halten, heißt das nicht, dass es eine Anforderung ist. Mit der Bestandsvalidierung außerhalb der Kernfunktionen von Adobe Commerce sind verbundene Kosten verbunden. Diese Kosten gehen auf technische Schulden, mehr Tests und Validierung sowie Nutzungsunterlagen und unterstützende Dokumente für die Architektur zurück.

## Bestimmen, was eine akzeptable Bestandsupdate-Kadenz ist

Versuchen Sie, Bestandsprüfungen in Betracht zu ziehen und wie sie in drei Ansätzen erreicht werden. Jeder hat Vorteile und Einschränkungen. Sie erhöhen auch die Komplexität und erfordern mehr Tests und Überlegungen zur Fehlerbehandlung. Denken Sie daran, wenn Sie sich für eine benutzerdefinierte Route entscheiden, gibt es zusätzliche Verantwortlichkeiten und Überlegungen. Einige Beispiele wären ein Fallback-Prozess, Überwachung, Tests und Fehlerbehebung, der dem Entwicklungsteam überlassen wird. Einige wichtige Elemente sind die neue unterstützende Dokumentation, Schulung und Überwachung, um sicherzustellen, dass das Entwicklungsteam die gesamte Funktion unterstützen kann. Ein weiterer Nebeneffekt besteht darin, dass das Entwicklungsteam vollständig für den Prozess verantwortlich ist und nicht mehr die von der Adobe Commerce-Hauptanwendung bereitgestellten nativen Funktionen nutzt. Die Adobe-Unterstützung kann bei dieser Anpassung nicht helfen.

Der erste Ansatz besteht in der Verwendung der nativen Funktionalität. Die Verwendung nativer Funktionen ist das geringste Risiko und hat viele Vorteile. Auf diese Weise können Sie sich auf alle vorhandenen Dokumentationen und Tutorials verlassen, die Adobe Commerce für die Verwendung der Funktion bereitstellt. Das Lagerbestandsmanagement umfasst viele Aspekte. Daher sollte die Verwendung der mit der Anwendung gelieferten Elemente die erste Überlegung sein. Es gibt jedoch Anwendungsfälle, in denen die zum Zeitpunkt der Bestellung im Handel gefundenen Daten möglicherweise nicht vollständig genau sind. Ein Beispiel dafür, wie Dinge nicht mehr synchron sind, ist, dass Verkäufe außerhalb der Adobe Commerce-Anwendung direkt im Bestellverwaltungssystem zulässig sind. Ein Grund dafür ist, dass, um sicherzustellen, dass die korrekten Bestandsgrößen in Adobe Commerce dargestellt werden, eine gewisse Integration erforderlich wäre, damit die Adobe Commerce-Informationen so genau wie möglich gehalten werden. Wenn Überverkäufe nicht akzeptabel sind, ist das Hinzufügen einer Nicht-Lager-Schwelle eine gute Methode, um den Verkauf von Artikeln zu stoppen, bevor Sie auf Null steigen. Die native Synchronisierungsfunktion für Adobe Commerce ist auf maximal 1 Uhr täglich beschränkt. Dies reicht für einige Anwendungsfälle aus, kann jedoch für andere nicht häufig genug sein. Bitte lesen [Geplanter Import und Export](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-scheduled-import-export) für detailliertere Informationen.

Der zweite Ansatz `near real-time`. Nahezu in Echtzeit wird weiterhin die native Funktionalität verwendet. Dies beinhaltet jedoch einige zusätzliche Arbeit, um eine Integration bereitzustellen, die den Handel häufig vorantreibt, um seinen Bestand planmäßig zu aktualisieren. Zum Beispiel jede Stunde. Diese Option muss überlegt werden, wie eine Integration funktionieren kann. Die Verwendung der &quot;Bulk API&quot; und die Verwendung einiger Middleware-Programme zur Datenumwandlung und zum Übertragen auf den Handel sind jedoch ein guter Ansatz. Sehen Sie sich die Verwendung von Adobe App Builder oder ähnlichen Plattformen an, um den Großteil der Arbeit zu erledigen und die Informationen häufiger an Adobe Commerce zu senden.

Der dritte Ansatz und der komplexeste Ansatz mit dem größten Risiko und der größten Verantwortung sind Echtzeit-Live-Bestandsprüfungen an eine externe API oder Datenquelle. Die Durchführung einer Bestandsüberprüfung in Echtzeit an ein externes System ist riskant und hat mehrere andere Elemente, die berücksichtigt werden müssen. Im Folgenden finden Sie eine kleine Auswahl weiterer Dinge, die ausgewertet werden müssen:

* Kann das externe System REST- oder GraphQL-Anforderungen akzeptieren?
* gibt es Einschränkungen für den Endpunkt, z. B. die X-Anzahl von Anfragen pro Minute, die möglicherweise nicht mit dem Website-Traffic übereinstimmen
* Was passiert mit der Antwortzeit unter Last?
* Wenn die Antwortzeiten lang sind, beenden Sie dies automatisch und verwenden eine Ausweichoption wie den nativen Bestand.
* Welche Art von Überwachung ist verfügbar, um sicherzustellen, dass API-Anfragen innerhalb der Toleranzgrenzen liegen?

## Überlegungen zur nicht nativen Lagerbestandsverwaltung

Halten Sie die Anpassungen so komplex wie möglich.
Wie flach kann die Organisation des Bestands sein, ist es nur 1 SKU und die Gesamtmenge des verfügbaren Bestands ODER gibt es andere Attribute, die berücksichtigt werden müssen.

Wenn die Bestandsinformationen relativ flach sind, z. B. eine SKU und die gesamte verfügbare Menge, werden die Optionen für nahezu Echtzeit erweitert. Das Konzept von nahezu Echtzeit bedeutet, dass es einen Hintergrundvorgang gibt, der den Bestand aus der Quelle erfasst und dann eine Speicher-Engine füllt, die zur Beantwortung der Anfrage verwendet werden soll. Dazu können Sie Elemente wie Redis, Mongo oder andere nichtrelationale Datenbanken verwenden. Diese Optionen sind schön, da sie sehr schnell sind und für Schlüssel/Wert-Paare gut funktionieren. Wenn die Daten etwas komplexer sind, ist die Verwendung einer Beziehungsdatenbank innerhalb oder außerhalb der Commerce-Anwendung wahrscheinlich erforderlich. Durch Abladen dieser Daten aus der Commerce-Datenbank wird die zentrale Commerce-Anwendung von diesen Transaktionen isoliert. Eine weitere Reihe von Vorteilen sind die Speicherung der E/A aus der Commerce-Anwendung, CPU, RAM und anderen. Statt die Ressourcen der Adobe Commerce-Anwendungsserver zu verwenden, nutzen Sie die neuen APIs, um die Daten aus dem externen Site-Speicher abzurufen.  Dies erfordert wahrscheinlich eine Middleware, um die Umwandlung von Daten zu unterstützen. Stellen Sie dann sicher, dass die aufrufende Anwendung das Ergebnis wie erwartet erhalten kann. Durch die Verwendung von Adobe App Builder mit API-Mesh können die Daten umgewandelt und korrekt formatiert zurückgegeben werden.

Die Verwendung von Adobe App Builder mit API-Gittern ist ebenfalls eine hervorragende Option, wenn mehrere Inventarquellen vorhanden sind.


## Verschieben der Ausführungslogik an einen Out-of-Process-Speicherort

Adobe Developer App Builder bietet ein einheitliches Drittanbieter-Erweiterbarkeits-Framework für die Integration und Erstellung benutzerdefinierter Erlebnisse zur Erweiterung der Adobe-Lösungen. Adobe Commerce kann Adobe Developer App Builder verwenden. Dies wäre ein ausgezeichneter Anwendungsfall für die Erweiterung einiger Funktionen, die normalerweise in der Kernanwendung auftreten und diese von der Site weg verschieben. Durch das Entfernen von Funktionen aus der Commerce-Anwendung wird die Anzahl der Module und die Komplexität der Commerce-Anwendung verringert. Eine geringere Anzahl von Anpassungen in Prozessen verringert die Komplexität der Aktualisierung und Wartung.

Für Anregungen, wie dies erreicht werden kann, hat das Team von Adobe eine Dokumentation erstellt, die eine großartige Inspirationsquelle sein und Arbeitscode-Beispiele bereitstellen kann. Wenn ein Käufer ein Produkt zum Warenkorb hinzufügt, überprüft ein Lagerbestandsverwaltungssystem eines Drittanbieters, ob der Artikel vorrätig ist. Ist dies der Fall, lassen Sie zu, dass das Produkt hinzugefügt wird. Zeigen Sie andernfalls eine Fehlermeldung an.  Codebeispiele und weitere Informationen finden Sie unter [Anwendungsfälle für Webhook](https://developer.adobe.com/commerce/extensibility/webhooks/use-cases/#add-product-to-cart).

## Wann werden Bestandskontrollen durchgeführt?

Wann überprüft werden soll, ob noch Inventar verfügbar ist, wird schließlich dem Geschäftsinhaber überlassen, der Softwarearchitekte mit einigen Beiträgen von anderen wichtigen Interessengruppen. Einige passende Zeiten wären beim Hinzufügen eines Artikels zum Warenkorb und beim Einstieg in den Checkout-Workflow enthalten. Alle anderen Ereignisse fügen einfach den Backend-Systemen Lasten hinzu, wenn dies nicht erforderlich ist. Beachten Sie, dass das Ziel darin besteht, ein Inventarproblem nur dann zu lösen, wenn es von größter Bedeutung ist. Andere Prüfungen sind zwar nett zu haben, sollten aber, wenn sie sich auf das Gesamtziel der Bestandsstatusprüfungen auswirken könnten, sorgfältig geprüft und nur dann zugelassen werden, wenn die Beteiligten der Wirtschaft oder andere über das potenzielle Risiko einer zusätzlichen Belastung der Backend-Systeme informiert sind.

## Erforschung der Inventarquelle

Eine umfassende Untersuchung der externen Inventarquelle ist erforderlich. Zu bewertende Elemente sind verfügbare API-Optionen, Unterstützung für GraphQL und erwartete Reaktionszeiten. Wenn die Inventarquelle über eine begrenzte Verbindungsbandbreite verfügt oder nie für die Verwendung in einer Echtzeitanforderung vorgesehen war, wird die Nutzungsmöglichkeit ausgeschlossen und der Architekt muss stattdessen nahezu Echtzeit in Betracht ziehen.  Wenn die API-Anforderungszeiten die definierten Parameter überschreiten, wird dies auch von der praktikablen Option ausgeschlossen.  Ein Beispiel dafür wären API-Antworten, die für eine Zeitanforderung 200MS® sind, aber unter moderater Belastung auf 500 bis 900MS® ansteigen.  Dies würde sich wahrscheinlich nur verschlechtern, wenn mehr ausgelastet würde und keine Live-Inventaraufrufe verfügbar wären.

Testen Sie die API-Antwortzeiten mit einfachen Anforderungen sowie mit einem hohen Volumen, das dem erwarteten Traffic auf der Live-Website ähnlich ist. Denken Sie daran, alle Bereiche aus dem Handel gleichzeitig zu testen, um reale Szenarien zu simulieren. Wenn es sich bei der Erwartung um einen Live-Inventaraufruf auf Produktseiten handelt, müssen beim Anzeigen und Bearbeiten eines Warenkorbs und während des Checkouts die Lasttests all diese gleichzeitig simulieren, um das reale Kundenverhalten und die Erwartung für einen Store nachzuahmen.

## Fallback-Optionen

Wenn die Inventarquelle ausfällt und eine Überwachung verfügbar ist, wird empfohlen, die native Funktion von Adobe Commerce zu verwenden. Bei ordnungsgemäßer Überwachung kann sich das Kundenerlebnis jedoch dynamisch ändern, um den Verlust von Bestandsprüfungen in Echtzeit widerzuspiegeln. Dies kann bedeuten, dass ein Verkauf oder Ereignis frühzeitig abgebrochen oder aus der Anzeige entfernt wird, um Überverkäufe zu vermeiden. Die Erwartung, was zu tun ist, wenn die Inventarquelle aus irgendeinem Grund ausfällt, muss berücksichtigt und mit dem Eigentümer des Stores besprochen werden, damit jeder über jeden automatischen Prozess informiert ist, der in diesem unglücklichen Fall übernommen wird.

## Schlussfolgerung

Die Entscheidung, Bestandskontrollen in Echtzeit durchzuführen, ist von großer Bedeutung. Die Sicherstellung, dass der Website-Eigentümer, das Entwicklungsteam und andere vollständig ausgebildet sind und sich über alle Gewinne und potenziellen Fallstricke im Klaren sind, obliegt dem Projektleiter oder Architekten. Ein umsichtiger Plan, der die Gründe abdeckt, und ein Ausweichprozess sind der Schlüssel zum Erfolg.

Live-Inventarprüfungen können durchgeführt werden, erfordern jedoch während des QA-Zyklus Untersuchungen und Überlegungen zu Tests und Validierungen. Durch die Sicherstellung, dass Belastungstests durchgeführt und automatisierte Tests beendet werden, wird sichergestellt, dass alle potenziellen Probleme erkannt und getestet werden.

Indem Sie überlegen, welche Aktionen durchzuführen sind, wenn die Überwachung einen Trend von fehlgeschlagenen Aufrufen an das externe System erkennt oder wenn die Antwortzeiten über den akzeptablen Schwellenwerten liegen, kann die Site online bleiben und den Kunden die geringste Verärgerung bieten. Fallback-Optionen können so einfach sein wie das Deaktivieren der externen Inventarprüfungen und die Verwendung der nativen Funktionalität oder so fortschrittlich wie das Deaktivieren einer Promotion, das Benachrichtigen des Entwicklungsteams über die eskalierenden Probleme oder vielleicht sogar das Umleiten von Anforderungen an ein zweites oder drittes Backend-System, falls verfügbar. Wie der Ausweichmechanismus angewendet wird, sollte nur als Implementierung durchdacht werden, da jede Integration irgendwann Probleme hat. Alles, was automatisiert ist oder manuelles Handeln erfordert, sollte klar dokumentiert sein.
