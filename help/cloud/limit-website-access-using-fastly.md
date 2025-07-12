---
title: Verwenden Sie Fastly, um den Zugriff auf eine gesamte Website zu verweigern.
description: Beschränken des Adobe Commerce-Site-Zugriffs mit Fastly Edge-ACLs und einer benutzerdefinierten VCL
feature: Cloud, Configuration, Site Management, System
topic: Administration,Commerce,Development, Security
role: Admin, Developer, User
level: Intermediate, Experienced
doc-type: Technical Video
duration: 200
last-substantial-update: 2025-07-11T00:00:00Z
jira: KT-18494
source-git-commit: 810d1a17e9fe564e8450b091bbeb5574d7d76075
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Verwenden Sie Fastly, um den Zugriff für eine gesamte Website zu verweigern.

Erfahren Sie, wie Sie den Zugriff auf Ihre Adobe Commerce Cloud-Site mithilfe von Fastly Edge-ACLs und benutzerdefinierten VCL-Snippets einschränken. Diese schrittweise Anleitung hilft Ihnen, Ihre Umgebung vor dem Start zu schützen, indem nur bestimmte IP-Adressen zugelassen werden. So wird sichergestellt, dass Ihre Entwicklungs-Site privat bleibt.

## Was Sie lernen werden

Beschränken des Adobe Commerce-Site-Zugriffs mit Fastly Edge ACLs und benutzerdefiniertem VCL | Sichere Pre-Launch-Umgebungen

## Für wen ist dieses Video bestimmt?

* DevOps-Engineer
* Adobe Commerce Developer
* Site Reliability Engineer

>[!VIDEO](https://video.tv.adobe.com/v/3464788/?learn=on&enablevpops&captions=ger)

## Code-Beispiel

Dies ist ein Beispiel für die verwendete VCL

```BASH
if ( !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 "Forbidden";}
```

## Verwandte Dokumentation

* [Erkennen bösartiger IP-Adressen](https://experienceleague.adobe.com/de/docs/commerce-learn/tutorials/tools/new-relic/malicious-ip)
* [Benutzerdefinierte VCL zum Zulassen von Anfragen](https://experienceleague.adobe.com/de/docs/commerce-on-cloud/user-guide/cdn/custom-vcl-snippets/fastly-vcl-allowlist)
* [Benutzerdefinierte VCL zum Blockieren von Anfragen](https://experienceleague.adobe.com/de/docs/commerce-on-cloud/user-guide/cdn/custom-vcl-snippets/fastly-vcl-blocking)