---
title: Erstellen einer effektiven Support-Anfrage
description: Erfahren Sie, wie Sie ein Support-Ticket erstellen, um die Effizienz der Anfrage zu maximieren.
feature: Best Practices, Customer Service, Support
topic: Commerce
role: Admin, Developer, User
level: Beginner, Intermediate
doc-type: Tutorial
duration: 126
last-substantial-update: 2024-08-23T00:00:00.000Z
jira: KT-15165
exl-id: cea62272-c7b9-44f7-9c39-5ad3d9122382
TQID: https://experienceleague.adobe.com/Si-izuH329pVtctIZ71FLXHfo48YaFtOGXGtAisu-tw
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 519
ht-degree: 0%

---

# Effektive Support-Anfragen

Bei der Erstellung eines Support-Tickets ist es wichtig, es über die entsprechenden Kanäle einzureichen, genaue und detaillierte Informationen zum Problem bereitzustellen, die richtige Organisation und den richtigen Kontaktgrund auszuwählen, das geeignete Produkt und die passende Version auszuwählen, empfohlene Artikel für potenzielle Lösungen zu lesen, alle Informationen vor dem Einreichen zu überprüfen, den Fortschritt des Tickets zu verfolgen und ein Gespräch mit dem Support-Team zu führen, das Ticket als gelöst zu markieren, wenn das Problem behoben ist, und ein Follow-up-Ticket zu erstellen, wenn weitere Hilfe benötigt wird. &#x200B; Denken Sie daran, das Ticket über die entsprechenden Kanäle einzureichen, genaue und detaillierte Informationen bereitzustellen, die richtige Organisation und den richtigen Kontaktgrund auszuwählen, das passende Produkt und die passende Version auszuwählen, vorgeschlagene Artikel zu überprüfen, alle Informationen vor dem Einreichen zu überprüfen, den Fortschritt des Tickets zu verfolgen, sich mit dem Support-Team zu unterhalten, das Ticket als gelöst zu markieren, wenn das Problem behoben ist, und bei Bedarf ein Folgeticket zu öffnen. &#x200B;

## Protokolle oder Screenshots einschließen

Es gibt mehrere Protokolle, die je nach vorliegendem Problem hilfreich sind. Suchen Sie nach Möglichkeit einen Abschnitt des Protokolls und nehmen Sie ihn in die Support-Anfrage auf. Dieser Protokollausschnitt hilft den Ingenieuren, die angezeigten Fehler zu verstehen, und beschleunigt den Triage-Prozess. Beachten Sie, dass jeder Anwendungs-Server über individuelle Protokolle verfügt und diese Protokolle als Aggregat in New Relic eingespeist werden.  Dies bedeutet, dass Sie an einem Ort nach allen Fehlern suchen können, anstatt die einzelnen Protokolldateien jedes Anwendungsservers zu lesen. Wenn in New Relic ein Eintrag gefunden wird, kann als letzte Option ein Screenshot als zusätzliche Information verwendet werden, um den Prozess zu beschleunigen. Es wird jedoch empfohlen, eine NRQL-Anweisung zu verwenden.

## Stellen Sie sicher, dass auf die Zeitzone verwiesen wird

Sicherstellen, dass Personen, die zu einem Support-Problem beitragen, daran erinnert werden, ihre Zeitzone beim Verweisen auf einen Vorfall anzugeben. Durch die Referenzierung einer Zeitzone wird sichergestellt, dass sich das Support-Engineering-Team bei der Suche nach den Protokollen und Ereignissen auf die tatsächlich relevanten Zeitrahmen konzentrieren kann. Denken Sie daran, dass jemand viele Stunden vor oder hinter dem Server-Log-Zeiten sein kann.

## Beschreiben der durchgeführten anfänglichen Triage und der Ergebnisse

Durch die Erörterung und Dokumentation aller bisher durchgeführten Triage-Schritte hilft den Support-Ingenieuren, frühe Annahmen zu validieren. Wenn die unterstützenden Triage-Schritte und -Ergebnisse bereitgestellt werden, kann dies den Gesamtprozess beschleunigen. Dies wird auch dazu beitragen, Doppelarbeit zu reduzieren und letztendlich eine Möglichkeit bieten, die Ergebnisse mit einem Validierungsgrad zu dokumentieren.

## Links zu New Relic-Berichten oder Bereitstellung einer NRQL-Anweisung

Viele Probleme in Adobe Commerce lassen sich über New Relic nachvollziehen. Durch die Betrachtung der New Relic-Dashboards oder benutzerdefinierten NRQL-Anweisungen erhalten Sie Einblicke, woher einige Probleme stammen. Dieselben Dashboards und benutzerdefinierten New Relic-Abfragen können freigegeben werden. By providing those links in the support ticket, the engineers are able to see exactly what the reporter is.

>[!MORELIKETHIS]
> 
> * [Adobe Commerce Help User Guide](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide){target="_blank"}
