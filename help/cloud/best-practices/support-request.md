---
title: Erstellen einer effektiven Supportanfrage
description: Erfahren Sie, wie Sie ein Support-Ticket erstellen können, um die Effizienz der Anfrage zu maximieren.
feature: Best Practices, Customer Service, Support
topic: Commerce
role: Admin, Developer, User
level: Beginner, Intermediate
doc-type: Tutorial
duration: 0
last-substantial-update: 2024-08-23T00:00:00Z
jira: KT-15165
source-git-commit: b3ec1230e5efa198d71e1a5c0756a47666065117
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# Effektive Supportanfragen

Bei der Erstellung eines Support-Tickets ist es wichtig, das Ticket über die entsprechenden Kanäle einzureichen, genaue und detaillierte Informationen zu dem Problem bereitzustellen, die richtige Organisation und den richtigen Kontaktgrund auszuwählen, das entsprechende Produkt und die entsprechende Version auszuwählen, die vorgeschlagenen Artikel für potenzielle Lösungen zu überprüfen, alle Informationen vor der Übermittlung zu überprüfen, den Fortschritt des Tickets zu verfolgen und mit dem Support-Team zu kommunizieren, das Ticket nach Behebung des Problems zu markieren und ein Follow-Ticket zu öffnen, wenn weitere Hilfe benötigt wird. &#x200B; Denken Sie daran, das Ticket über die entsprechenden Kanäle zu senden, genaue und detaillierte Informationen bereitzustellen, die richtige Organisation und den richtigen Kontaktgrund auszuwählen, das entsprechende Produkt und die entsprechende Version auszuwählen, die vorgeschlagenen Artikel zu überprüfen, alle Informationen vor dem Senden zu überprüfen, den Fortschritt des Tickets zu verfolgen, mit dem Supportteam in Kontakt zu treten, das Ticket bei Lösung des Problems als gelöst zu markieren und bei Bedarf ein Folgenachticket zu öffnen. &#x200B;

## Enthält Protokolle oder Screenshots

Je nach dem vorliegenden Problem sind verschiedene Protokolle hilfreich. Suchen Sie nach Möglichkeit einen Abschnitt des Protokolls und fügen Sie ihn als Teil der Support-Anfrage ein. Dieses Protokollfragment hilft den Ingenieuren, die angezeigten Fehler zu verstehen, und beschleunigt den Testprozess. Beachten Sie, dass jeder Anwendungsserver über individuelle Protokolle verfügt und diese Protokolle als Aggregat in New Relic eingespeist werden.  Dies bedeutet, dass Sie an einem Ort nach allen Fehlern suchen können, anstatt die einzelnen Protokolldateien des jeweiligen Anwendungsservers zu lesen. Wenn ein Eintrag in New Relic gefunden wird, kann als letzte Option auch ein Screenshot als zusätzliche Information verwendet werden, um den Prozess zu beschleunigen. Es wird jedoch empfohlen, eine NRQL-Anweisung zu haben.

## Stellen Sie sicher, dass auf die Zeitzone verwiesen wird.

Sicherstellen, dass Personen, die zu einem Support-Problem beitragen, sie daran erinnern, ihre Zeitzone bei der Bezugnahme auf einen Vorfall zu präzisieren. Durch Referenzierung einer Zeitzone wird sichergestellt, dass sich das Support-Team bei der Suche nach den Protokollen und Ereignissen auf die tatsächlich relevanten Zeitrahmen konzentrieren kann. Denken Sie daran, dass der Server viele Stunden vor oder hinter der Serverprotokollzeit liegen kann.

## Beschreiben Sie die durchgeführte Anfangsstudie und die Ergebnisse.

Durch die Erörterung und Dokumentation aller bisher durchgeführten Triage-Schritte hilft den Support-Ingenieuren bei der Validierung früherer Annahmen. Werden die unterstützenden Triage-Schritte und -Ergebnisse bereitgestellt, kann dies den Gesamtprozess beschleunigen. Dies wird auch dazu beitragen, Doppelarbeit zu reduzieren und schließlich eine Möglichkeit bieten, die Ergebnisse mit einem Grad an Validierung zu dokumentieren.

## Links zu New Relic-Berichten oder Bereitstellung der NRQL-Anweisung

Viele der Probleme in Adobe Commerce sind über New Relic nachvollziehbar. Indem Sie sich die New Relic-Dashboards oder benutzerdefinierte NRQL-Anweisungen ansehen, erhalten Sie Einblicke, woher einige Probleme kommen. Dieselben Dashboards und benutzerdefinierten New Relic-Abfragen können freigegeben werden. Durch die Bereitstellung dieser Links im Support-Ticket können die Ingenieure genau sehen, was der Reporter ist.

>[!MORELIKETHIS]
> 
> - [Adobe Commerce-Hilfe-Benutzerhandbuch](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide){target="_blank"}
