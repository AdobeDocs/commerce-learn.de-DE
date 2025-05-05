---
title: Erkennen von IP-Adressen
description: Erfahren Sie, wie Sie IP-Adressen für Adobe Commerce Cloud-Umgebungen erkennen, um die Sicherheit zu erhöhen und die Server-Kommunikation zu optimieren
feature: Cloud, Configuration
topic: Commerce, Development, Integrations
role: Developer
level: Beginner
doc-type: Technical Video
duration: 0
last-substantial-update: 2025-04-07T00:00:00Z
jira: KT-17553
exl-id: beb0a6e1-e6b1-4ec0-976c-77a22a27e8a2
source-git-commit: 3acec65129773a8ba94eb52c53d15d7633440717
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 0%

---

# Erkennen von IP-Adressen für verschiedene Umgebungen

Erfahren Sie, wie Sie IP-Adressen für verschiedene Umgebungen in einem Adobe Commerce Cloud-Projekt erkennen. Mithilfe einer Reihe von Befehlen wie Adobe Commerce CLI, sed, xargs, dig, grep und sort -u können Benutzer IP-Adressen für Entwicklungs-, Staging- und Produktionsumgebungen identifizieren.

## Für wen ist dieses Video bestimmt?

* Entwickler: Sie möchten verstehen, wie Sie die IP-Adressen für das Adobe Commerce Cloud-Projekt erfassen.
* Entwicklungs- und Sicherheits-Teams, die den Zugriff auf Drittanbieter- oder Backend-Systeme einschränken müssen

## Videoinhalt {#video-content}

* Erfahren Sie, wie Sie die IP-Adresse für eine beliebige Umgebung in Adobe Commerce Cloud ermitteln.

>[!VIDEO](https://video.tv.adobe.com/v/3457493/?learn=on)

## Befehl zum Abrufen der IP-Adresse

Beachten Sie, dass Sie Ihre Projekt-ID und den Umgebungsnamen anstelle der Platzhalterinformationen verwenden müssen.  Möglicherweise muss auch der `{1..3}` geändert werden, damit er der Anzahl der Knoten in Ihrem Adobe Commerce Cloud-Cluster entspricht. Am häufigsten ist jedoch der Wert 3.

```bash
magento-cloud environment:url -p InsertYourProjectID -e UseYourEnvironmentName --pipe -1 | sed 's/.\.c\.(.)/\1/;s/.$//' | xargs -I% dig +short {1..3}."%" | grep '^\d' | sort -u
```

## Adobe Commerce Cloud-CLI

```bash
magento-cloud environment:url -p InsertYourProjectID -e UseYourEnvironmentName --pipe -1
```

Das Magento-Cloud-CLI-Tool unterstützt Entwickler und Systemadministratoren bei der effizienten Verwaltung von Adobe Commerce Cloud-Projekten und -Umgebungen. Sie erweitert die Funktionalität der Cloud-Konsole und ermöglicht es Benutzern, Routineaufgaben auszuführen und die Automatisierung lokal auszuführen. Zu den wichtigsten Funktionen gehören die Verwaltung von Integrationsumgebungen, das Auschecken und Zusammenführen von Umgebungen, das Auflisten von Variablen und die Verwendung von SSH zur Verbindung mit Remote-Umgebungen. Das Tool vereinfacht Workflows, indem es die Ausführung von Befehlen direkt von der lokalen Workstation aus ermöglicht und so den gesamten Entwicklungs- und Bereitstellungsprozess verbessert.

In diesem ersten Abschnitt des Beispiel-Codes fordert `magento-cloud environment:url -p InsertYourProjectID -e UseYourEnvironmentName --pipe -1` die URL für die Umgebung an. Der zurückgegebene Wert sieht in etwa wie `http://integration-1ajmyuq-mk7xr7zmslfg.us-4.magentosite.cloud/` aus. Ab und zu sieht es mehr so aus wie dieses `http://mcprod.russell.dummycachetest.com.c.abcikdxbg789.ent.magento.cloud/`.  Dieser erste Befehl ist recht einfach, und jetzt ist es an der Zeit, mit dem nächsten Befehl fortzufahren.

Weitere Informationen finden Sie unter [Cloud-CLI - Übersicht](https://experienceleague.adobe.com/de/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview){target="_blank"}

## Verwenden von `sed` für Suchen und Ersetzen

```bash
sed 's/.\.c\.(.)/\1/;s/.$//'
```

Der Befehl `sed` in UNIX®Linux® steht für Stream-Editor. Sie wird verwendet, um grundlegende Texttransformationen für einen Eingabestream (eine Datei oder eine Eingabe aus einer Pipeline) durchzuführen. Häufige Verwendungszwecke sind das Suchen, Suchen und Ersetzen, Einfügen und Löschen von Text. Der Befehl verarbeitet Text `sed` Zeile und wendet bestimmte Vorgänge an, wodurch er zu einem leistungsstarken Tool für Textbearbeitung und Skripterstellung wird.

Wie bereits erwähnt, gibt es in der Regel zwei Arten von URLs, die von der `magento-cloud` CLI zurückgegeben werden. Es gibt eine Variante, die `.com.c.c` in der Mitte enthält. Diese Variante ist diejenige, die manipuliert werden muss. Wenn diese Struktur erkannt wird, muss alles vom Anfang der URL bis zum `.com.c.c` entfernt werden.  Dann bleibt nur noch der letzte Teil der URL. Eine Beispiel-URL sieht wie `http://mcprod.russell.dummycachetest.com.c.abcikdxbg789.ent.magento.cloud/` aus.  Wenn dieses Muster erkannt wird, besteht das Ziel darin, alles nach dem `.c.` zu behalten.  In diesem bereitgestellten Beispiel-Code wird `sed 's/.\.c\.(.)/\1/'` verwendet, um dieses Teil zu erfassen und den Rest des ursprünglich zurückgegebenen Werts zu ignorieren. Der verbleibende Teil der URL ähnelt `abcikdxbg789.ent.magento.cloud/`.\
In `sed` werden zwei Befehle ausgeführt. Sie sind durch ein Semikolon getrennt. Der zweite Teil meiner `sed`-`;s/.$//'` besteht darin, alle nachfolgenden Schrägstriche zu entfernen, sofern sie vorhanden sind, um diese URL zu bereinigen, sodass sie wie `abcikdxbg789.ent.magento.cloud` aussieht.  Zu diesem Zeitpunkt wurde die URL bereinigt und ist für den nächsten Befehl bereit.

## Xargs mit Ausgrabung

```bash
xargs -I% dig +short {1..3}."%"
```

Der `xargs`Befehl in UNIX®Linux® wird verwendet, um Befehlszeilen aus der Standardeingabe zu erstellen und auszuführen. Es nimmt Eingaben aus einer Pipe oder einer Datei und konvertiert sie in Argumente für einen anderen Befehl. Dies ist besonders nützlich für die Verarbeitung einer großen Anzahl von Argumenten, die die Grenze der Shell überschreiten. Mit dem `xargs` können Vorgänge wie das Verschieben, Kopieren oder Löschen von Dateien durchgeführt werden. Dies ermöglicht eine effiziente Batch-Verarbeitung, indem mehrere Argumente in einer einzigen Ausführung an Befehle übergeben werden.

Der `dig`-Befehl, kurz für Domain Information Groper, ist ein Tool zur Netzwerkverwaltung, mit dem DNS-Server (Domain Name System) abgefragt werden können. Es hilft beim Abrufen von Informationen über DNS-Einträge, wie A-, AAAA-, MX- und CNAME-Einträge. Der Befehl `dig` wird häufig verwendet, um DNS-Probleme zu beheben, DNS-Konfigurationen zu überprüfen und detaillierte Informationen über Domain-Namen und die zugehörigen IP-Adressen zu sammeln. Durch Verwendung verschiedener Optionen und Flags können Benutzende die Ausgabe anpassen, um bestimmte Details oder eine knappe Zusammenfassung anzuzeigen.

Die Verwendung von `xargs` mit `dig` macht es kompliziert, aber es ist notwendig. Ziel ist es, die bereinigte URL zu speichern.  Nachdem die URL als Variable gespeichert wurde, wird sie in den `dig`-Befehl eingefügt.

Der Befehl `dig` wurde erstellt, um DNS-Informationen zu erfassen. Um die Menge der zurückgegebenen Daten zu reduzieren, wird das Argument `+short` verwendet. Bei Verwendung von `dig` in Kombination mit `+short` werden IP-Adressen und manchmal Zeichenfolgen zurückgegeben.

In diesem Teil des Befehls speichert `xargs` diese URL-`abcikdxbg789.ent.magento.cloud` und fügt sie in die nächste `dig` ein. Das Verfahren zum Speichern der URL in Kombination mit der Iteration erleichtert die Verwendung des Befehls `dig` . Denken Sie daran, dass mein Beispiel-Code eine Möglichkeit ist, das Ziel zu erreichen, und Sie können die Dinge ändern, um Ihre Anforderungen und Erwartungen zu erfüllen.

An dieser Stelle ist die URL bereit. Als Nächstes sehen wir, wie es möglich ist, jeden Server im Cluster zu überprüfen. Für Adobe Commerce Cloud hat jeder Server im Cluster eine Nummer. Die Server-Kennung ist ein Präfix für die URL, die gerade bereinigt und einsatzbereit gemacht wurde. Eine schnelle und einfache Möglichkeit, die Server zu deaktivieren, ist die Verwendung von `{1..3}`. Durch Verwendung von `{1..3}`, das den `dig`-Befehl dreimal ausführt. Im Folgenden sehen Sie, was passiert, wenn Sie die Ausführung in Echtzeit beobachten.

```bash
dig +short 1.<projectid>.ent.magento.cloud
dig +short 2.<projectid>.ent.magento.cloud
dig +short 3.<projectid>.ent.magento.cloud
```

Zu besseren Veranschaulichungszwecken würde diese von `dig` verwendete Beispiel-URL wie folgt aussehen:

```bash
dig +short 1.aabcikdxbg789.ent.magento.cloud
dig +short 2.abcikdxbg789.ent.magento.cloud
dig +short 3.abcikdxbg789.ent.magento.cloud
```

Wenn `{1..3}` geändert wurde, um `{1..6}` zu werden, würde es wie folgt aussehen:

```bash
dig +short 1.aabcikdxbg789.ent.magento.cloud
dig +short 2.abcikdxbg789.ent.magento.cloud
dig +short 3.abcikdxbg789.ent.magento.cloud
dig +short 4.aabcikdxbg789.ent.magento.cloud
dig +short 5.abcikdxbg789.ent.magento.cloud
dig +short 6.abcikdxbg789.ent.magento.cloud
```

## Der `grep`

Es gibt Fälle, in denen eine Zeichenfolge als Teil des Ergebnisses von `dig` zurückgegeben wird. Zu diesem Zweck werden nur IP-Adressen verwendet, die aus Zahlen mit Punkten bestehen. Um sicherzustellen, dass die endgültige Ausgabe nur Zahlen enthält, können Sie den Befehl anpassen. Nach Abschluss wird die endgültige Syntax ` grep '^\d'`.  Durch Hinzufügen von `'^\d'` behält der Befehl `grep` nur Zahlen bei und ignoriert alles andere.

## Der `sort`

Durch die Verwendung von `sort -u` werden alle Duplikate aus der Liste der IPs entfernt. Duplikate treten nur bei der Suche nach Entwicklungsstufen auf.

Diese Umgebungen auf niedrigerer Ebene sind mandantenfähig und teilen die zugrunde liegenden Server mit vielen anderen Projekten. Entwicklungsumgebungen sind Einzelserver und nie ein Cluster. Wenn der dig-Befehl daher über jede Iteration schleift, gibt er dieselbe IP mehrmals zurück. Mithilfe der `sort -u` werden also alle doppelten IPs entfernt, und es bleiben nur eindeutige IP-Adressen übrig.



## Verwandte Dokumentation

* [Regionale IP-Adressen](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/regional-ip-addresses|https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/regional-ip-addresses){target="_blank"}
