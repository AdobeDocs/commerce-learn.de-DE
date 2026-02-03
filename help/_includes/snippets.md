---
title: Banner bearbeiten
description: Wiederverwendete visuelle Elemente zur Notiz von Funktionen oder Seiten, die auf eine bestimmte Bearbeitung angewendet werden
source-git-commit: 0cf8b11019cbe9d863ef8f281c09e715c1acb4b9
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Banner bearbeiten

## Funktion nur anzeigen {#ee-feature}

<table style="border:1px solid red">
<tr><td><img alt="Adobe Commerce-Funktion" src="../assets/adobe-logo.svg" width="20" height="20" /> Exklusive Funktion nur in Adobe Commerce (<a href="https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html?lang=de#product-editions">Weitere Informationen</a>)</td></tr>
</table>

## Funktion nur B2B {#b2b-feature}

<table style="border:1px solid green">
<tr><td><img alt="Adobe Commerce-Funktion" src="../assets/b2b.svg" width="20" height="20" /> Exklusive Funktion nur bei <a href="https://experienceleague.adobe.com/docs/commerce-admin/b2b/guide-overview.html?lang=de">B2B für Adobe Commerce verfügbar</a></td></tr>
</table>

## 400 Anfragen {#avoid-400-error}

>[!CAUTION]
>
>Stellen Sie bei API-Aufrufen sicher, dass eine Art von Suchkriterien verwendet wird. Sie können auch eine Paginierung in Betracht ziehen. Wenn das Ergebnis von Adobe Commerce zu groß ist, kann die Adobe Developer App Builder-Kapazität erreicht werden und zu einem unerwarteten Dateiende führen. Das Ergebnis ist ein falsch formatiertes Antwortergebnis als 400-Fehler.\
> Angenommen, es besteht die Notwendigkeit, alle aktuellen Produkte von Adobe Commerce anzufordern. Die resultierende URL würde `{{base_url}}rest/V1/products?searchCriteria=all` ähneln. Je nach Größe des von zurückgegebenen Katalogs kann die JSON zu groß für App Builder sein. Verwenden Sie stattdessen Paginierung und stellen Sie einige Anfragen, um `Response is not valid 'message/http'.` zu vermeiden

## Nur PaaS und Commerce Cloud {#only-for-on-prem-commerce-cloud}

| On-Premise | Adobe Commerce Cloud | Adobe Commerce as a Cloud Service | Adobe Commerce Optimizer |
| --- | --- | --- | --- |
| Ja | Ja | Nein | Nein |
