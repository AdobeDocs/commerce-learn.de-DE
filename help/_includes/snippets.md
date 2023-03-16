---
title: Edition Banner
description: Wiederverwendete visuelle Elemente zur Notiz von Funktionen oder Seiten, die auf eine bestimmte Bearbeitung angewendet werden
source-git-commit: 8c7c64ddff456815b0a1649f497e917da8b8fca0
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Edition Banner

## Nur Funktion {#ee-feature}

<table style="border:1px solid red">
<tr><td><img alt="Adobe Commerce-Funktion" src="../assets/adobe-logo.svg" width="20" height="20" /> Ausschließliche Funktion nur in Adobe Commerce (<a href="https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html#product-editions">Weitere Infos</a>)</td></tr>
</table>

## Nur B2B-Funktion {#b2b-feature}

<table style="border:1px solid green">
<tr><td><img alt="Adobe Commerce-Funktion" src="../assets/b2b.svg" width="20" height="20" /> Ausschließliche Funktion nur mit <a href="https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html#product-editions">B2B für Adobe Commerce</a></td></tr>
</table>

## 400 Fragen {#avoid-400-error}

>[!CAUTION]
>
>Stellen Sie bei API-Aufrufen sicher, dass eine Art von searchCriteria verwendet wird. Sie können auch die Paginierung in Erwägung ziehen. Wenn das Ergebnis von Adobe Commerce zu groß ist, kann die Adobe Developer App Builder-Kapazität erfüllt sein und ein unerwartetes Ende der Datei verursachen. Das Ergebnis ist ein fehlerhaftes Antwortergebnis als 400-Fehler.\
> Angenommen, alle aktuellen Produkte müssen von Adobe Commerce angefordert werden. Die resultierende URL würde `{{base_url}}rest/V1/products?searchCriteria=all`. Je nach der Größe des zurückgegebenen Katalogs kann die JSON zu groß sein, um von App Builder genutzt werden zu können. Verwenden Sie stattdessen die Paginierung und stellen Sie einige Anforderungen, um `Response is not valid 'message/http'.`
