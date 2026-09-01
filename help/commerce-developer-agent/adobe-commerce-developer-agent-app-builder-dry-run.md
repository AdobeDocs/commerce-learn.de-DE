---
title: Adobe Commerce Developer Agent App Builder - Probelauf
description: In diesem praktischen App Builder-Probelauf erfahren Sie, wie Sie drei Anwendungsfälle für die Erweiterbarkeit von Commerce mit dem Adobe Commerce Developer Agent erstellen, bereitstellen und testen.
feature: Extensibility, App Builder, Eventing, Configuration
topic: App Builder, Development, Integrations
role: Developer
level: Intermediate
doc-type: Tutorial
duration: 438
last-substantial-update: 2026-08-28T00:00:00Z
source-git-commit: 92af5355fa31c1ce9e627679b0a1bb92cce0e1d8
workflow-type: tm+mt
source-wordcount: '1700'
ht-degree: 0%

---

# Adobe Commerce Developer Agent App Builder - Probelauf

Eine praktische Anleitung zum Erstellen, Bereitstellen und Testen von Anwendungsfällen für die Erweiterbarkeit von Commerce mit dem Adobe Commerce Developer Agent (CDA). Dieser Probelauf deckt drei Anwendungsfälle ab: einen Webhook zur Begrenzung der Warenkorbmenge, einen hochwertigen Auftragsbestand und eine ereignisgesteuerte Archivierung für gespeicherte Aufträge, von der Blueprint bis hin zu Funktionstests.

## Erste Schritte

### Melden von Problemen und Feedback

Während des gesamten Trockenlaufs stoßen Sie auf raue Kanten - das wird erwartet, wenn Sie mit einer neuen Funktion arbeiten. Erfassen und teilen Sie alle Probleme mit Ihrem Adobe-Programmkontakt mithilfe der Feedback-Vorlage, die beim Onboarding bereitgestellt wurde.

>[!TIP]
>
> Beim Melden eines Problems:
>
> * Schließen Sie die `projectId` ein (in Ihrer Browser-URL sichtbar).
> * Schließen Sie Screenshots bei Bedarf ein.

### Voraussetzungen

**Konten und Zugriff**

* Wählen Sie zumindest die Rolle **Entwickler** in Ihrer Early Access IMS-Organisation aus.
* Administratorzugriff auf eine Adobe Commerce as a Cloud Service (ACCS)-Instanz innerhalb dieser Organisation, verfügbar unter experience.adobe.com unter **Cloud Service-Instanzen**.
* Ein GitHub-Konto.

**Tools**

Für die funktionale Validierung ist eine Edge Delivery Services (EDS)-Storefront erforderlich. Sie benötigen:

* Node.js 22+
* Adobe I/O CLI: `npm install -g @adobe/aio-cli`
* AIO CLI Commerce-Plug-in: `aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce`

Installieren Sie die Storefront-Textvorlage in einem leeren Ordner und wählen Sie Ihre ACS-Instanz aus, wenn Sie dazu aufgefordert werden:

```bash
aio commerce extensibility app-setup -s aem-boilerplate-commerce -n storefront
```

Starten Sie die Storefront:

```bash
cd storefront
npm run start
```

## Öffnen des Commerce Developer Agent

1. Navigieren Sie unter experience.adobe.com zum Commerce Developer Agent unter **Developer Agent**.
1. Melden Sie sich mit Ihren Anmeldedaten für die Early Access IMS-Organisation an.

## Anwendungsfall 1: Webhook für maximale Einheiten im Warenkorb

In diesem Anwendungsbeispiel werden mithilfe eines synchronen Commerce-Webhooks die Mengenbeschränkungen für den Warenkorb validiert, bevor ein Produkt hinzugefügt wird.

### Blueprint-Phase

Geben Sie die folgende Eingabeaufforderung ein und klicken Sie auf **Blueprint erstellen**:

```text
Add a validation webhook that runs before a product is added to the cart.

Use the Commerce webhook method observer.sales_quote_item_save_before (type before) — do not use
observer.checkout_cart_product_add_before, observer.sales_quote_add_item, or any other event.

Calculate the total by summing all quote line quantities and the quantity of the current item.
If the same SKU already exists in the quote, exclude its existing quantity to avoid double-counting.

If the total is greater than the maximum allowed, block the add and show:
"You have reached the maximum amount of items."

The maximum allowed must be configurable in Commerce Admin as max_cart_units, with default 10.

Map payload fields using name and source properties:
- name: item.qty, source: data.item.qty
- name: item.sku, source: data.item.sku
- name: quote, source: context_checkout_session.get_quote[items.qty,items.sku]

Set required: true and fallback_error_message: "You have reached the maximum amount of items."
on the webhook config.

When blocking the add, do not use exceptionOperation, because it serializes exceptionClass as class.
Instead, manually return an exception operation response whose body includes type:
{
  "op": "exception",
  "message": "You have reached the maximum amount of items.",
  "type": "\\Magento\\Framework\\GraphQl\\Exception\\GraphQlInputException"
}
```

>[!NOTE]
>
> Achten Sie auf Folgendes:
>
> * Es wird ein Blueprint (v1) zur Erfassung der Anforderungen erstellt.
> * Es werden Aufgaben erstellt, die die Implementierung leiten.

Verfeinern Sie den Blueprint, indem Sie Details in das Chat-Feld eingeben oder auf eine der Pillen über dem Chat-Feld klicken (*Challenge-Annahmen*, *Designlücken finden* usw.). Wenn Sie zufrieden sind, klicken Sie auf **Plan genehmigen**, um fortzufahren.

### Stadium entwickeln

Der Agent wechselt in die Entwicklungsphase und beginnt mit der Bereitstellung des Arbeitsbereichs.

>[!NOTE]
>
> Suchen Sie im Explorer-Bedienfeld nach diesen Dateien:
>
> * `app.commerce.config.ts`
> * `app.config.yaml`
> * `install.yaml`
> * `package-lock.json`
> * `package.json`

Nach der Bereitstellung zeigt der Agent eine Liste der Implementierungsaufgaben an und beginnt mit der Erstellung.

>[!NOTE]
>
> Achten Sie auf Folgendes:
>
> * Der generierte Code entspricht den Anforderungen.
> * Der Bildschirm Streaming `Validate` zeigt den Fortschritt bei der Workspace-Validierung (`aio app build`) an.
> * Der Agent korrigiert den generierten Code selbst, wenn die Validierung fehlschlägt.

Wenn Sie mit dem Code zufrieden sind, klicken Sie auf die Registerkarte **Integrationen**, um fortzufahren.

### Integrationen konfigurieren

**Verbinden oder Erstellen eines App Builder-Arbeitsbereichs**

Um ein App Builder-Projekt zu erstellen oder zu verbinden, folgen Sie den Anweisungen auf dem Bildschirm.

Wenn Sie eine Verbindung zu einem vorhandenen Arbeitsbereich herstellen, stellen Sie sicher, dass Folgendes zutrifft:

* Der hinzugefügte `Runtime`-Service.
* Die folgenden APIs wurden hinzugefügt: Adobe Commerce as a Cloud Service, I/O-Management-API, App Builder Data Services, I/O-Ereignisse, Adobe I/O Events für Adobe Commerce.

Wenn Sie einen neuen Arbeitsbereich erstellen, fügen Sie die **Adobe Commerce as a Cloud Service**-API manuell hinzu.

>[!IMPORTANT]
>
> Sobald die Verbindung zu einem bestehenden App Builder-Projekt hergestellt ist **erweitern Sie „Erweiterte Konfiguration** und fügen Sie die Workspace-JSON ein. Klicken Sie dann **Status erneut überprüfen**, um zu bestätigen, dass alle erforderlichen APIs installiert sind.

Klicken Sie **Weiter** um fortzufahren.

**Verbindung zu Commerce herstellen**

Wählen Sie Ihre ACS-Instanz aus der Liste aus oder geben Sie die URL in das Feld **Commerce REST-Basis-URL** ein und klicken Sie dann auf **Commerce-Instanz verbinden**. Klicken Sie **Weiter** um fortzufahren.

**Verbindung zu GitHub herstellen**

Verbinden Sie den Arbeitsbereich mit einem GitHub-Repository, indem Sie die Repository-URL eingeben und entweder die GitHub-App oder ein persönliches Zugriffstoken verwenden. Klicken Sie **Weiter** um fortzufahren.

**Konfigurieren von Umgebungsvariablen**

Füllen Sie alle für das Projekt erforderlichen Umgebungsvariablen aus.

### Bereitstellen

Klicken Sie **Entwickeln**, um zur Entwicklungsphase zurückzukehren, und bitten Sie dann den Agenten, die Bereitstellung im Eingabeaufforderungsfeld vorzunehmen.

>[!NOTE]
>
> Suchen Sie nach der Meldung „Bereitstellung bestätigen“, die den Namespace „Organisation“, „Projekt“, &quot;Workspace&quot; und „Laufzeit“ anzeigt.

Bestätigen Sie die Bereitstellung.

>[!NOTE]
>
> Suchen Sie nach:
>
> * Der `Validate`-Streaming-Bildschirm zeigt den Fortschritt der Validierung vor der Bereitstellung an.
> * Der Agent korrigiert den Code selbst, wenn die Validierung fehlschlägt.
> * Der `Deploy`-Streaming-Bildschirm mit dem Bereitstellungsfortschritt (`aio app deploy`).
> * Der Agent korrigiert den Code selbst, wenn die Bereitstellung fehlschlägt.

### App in App Management verknüpfen

1. Navigieren Sie zur Admin-URL Ihrer ACS-Instanz und melden Sie sich an.
1. Wählen Sie **Menü links** Apps“ und dann **App-Verwaltung** aus.
1. Klicken Sie auf **+ Programm** verknüpfen) (oben rechts).
1. Wählen Sie das Projekt und die Workspace aus, für die die geräteübergreifende Analyse bereitgestellt wurde, und klicken Sie dann auf **Verknüpfen**.

>[!NOTE]
>
> Suchen Sie nach einer Karte, die den Namen und die Version des Programms sowie die implementierten Funktionen (Geschäftskonfiguration, Webhooks, Ereignisse usw.) anzeigt.

### Installieren und Konfigurieren von in App Management

1. Klicken Sie in der Zeile für Ihre Anwendung auf **Installieren** und dann auf **Schließen**.
1. Klicken Sie in derselben Zeile auf **Konfigurieren**, um Geschäftskonfigurationswerte einzugeben, und klicken Sie dann auf **Schließen**.

>[!NOTE]
>
> Suchen Sie nach einem Formular, das alle durch den Blueprint angegebenen Konfigurationsfelder anzeigt und mit den von Ihnen angegebenen Standardwerten vorausgefüllt ist.

### Funktionstests

1. Legen Sie in der App-Management **App-Konfiguration „Maximale Warenkorbeinheiten** auf 3 fest (ein niedriger Wert für einen Schnelltest).
1. Beginnen Sie in der Storefront mit einem leeren Warenkorb.
1. Fügen Sie Produkte von der Produktdetailseite (PDP) hinzu, bis die Gesamtmenge 3 überschreitet - die letzte Hinzufügung schlägt fehl.
1. Im PDP sehen Sie: *„Sie haben die maximale Anzahl von Elementen erreicht.“*
1. Unter dem Limit ist das Hinzufügen weiterhin erfolgreich.

>[!NOTE]
>
> Auf der Produktlistenseite (PLP) schlägt eine blockierte Hinzufügung ohne Meldung im Hintergrund fehl. Dies ist ein Storefront-Verhalten, kein Webhook-Fehler. PDP zur Überprüfung vorziehen.

## Anwendungsfall 2: Hochwertiger Auftragssperre- und Verifizierungs-Code

Navigieren Sie zurück zum **Blueprint**-Schritt, um diesen Anwendungsfall zu starten.

### Blueprint-Phase

Geben Sie die folgende Eingabeaufforderung ein und klicken Sie auf **Blueprint erstellen**:

```text
Add a Commerce event priority subscription to `plugin.sales.api.order_management.place`.

Extract `entity_id` and `grand_total` from the Commerce event payload using event `fields` in `app.commerce.config.ts`.

Important: the runtime action receives a CloudEvents-shaped payload. For Commerce eventing extracted fields,
parse them from `params.data.value`, not directly from `params.data`. The handler must use:
- `params.data.value.entity_id`
- `params.data.value.grand_total`

When `grand_total` is greater than `order_hold_threshold`:
1. Generate a verification code locally.
2. Put the order on hold with state and status `holded`.
When putting the order on hold, save the verification code using `custom_attributes`, not `extension_attributes`.
The Commerce `POST V1/orders` payload should include:
{
  "entity": {
    "entity_id": <entity_id>,
    "state": "holded",
    "status": "holded",
    "custom_attributes": [
      {
        "attribute_code": "<hold_verification_attribute>",
        "value": "<verification_code>"
      }
    ]
  }
}
3. Save the verification code via a `POST V1/orders` Commerce REST API call.

Make these configurable in Commerce Admin:
- `order_hold_threshold`, default `500`
- `hold_verification_attribute`, default `lab_verification_code`

Validate inputs before use:
- `entity_id` must be a positive integer.
- `grand_total` must be a non-negative number.
```

>[!NOTE]
>
> Achten Sie auf Folgendes:
>
> * Es wird ein Blueprint (v2) zur Erfassung der Anforderungen erstellt.
> * Die ursprünglichen Planaufgaben werden beibehalten.
> * Neue Aufgaben, die den neuen Anforderungen entsprechen, wurden hinzugefügt.

Verfeinern Sie den Blueprint nach Bedarf und klicken Sie dann auf **Plan genehmigen**, um fortzufahren.

### Entwickeln, Bereitstellen, Verknüpfen und Installieren

Folgen Sie dem gleichen Prozess wie in Anwendungsfall 1, um von den Anforderungen zu einer installierten Anwendung zu wechseln - es ist nicht erforderlich, Integrationen neu zu konfigurieren.

>[!IMPORTANT]
>
> Um Änderungen an einer bereits verknüpften App zu erfassen, müssen Sie die Verknüpfung **aufheben** und **verknüpfen** erneut in der App-Verwaltung aktivieren.

### Funktionstests

1. Legen Sie in der App-Management **App-Konfiguration „Schwellenwert für Bestellungssperre (USD)** auf 50 fest (einfach zu überschreiten in einem Testwagen).
1. Bestätigen Sie, dass das benutzerdefinierte Attribut für die Bestellung vorhanden ist (`lab_verification_code`).
1. Bestellung mit einem Gesamtwert von über 50 $.
1. Warten Sie ca. 30 Sekunden (Ereignisse sind asynchron; die Bereitstellung ohne Priorität kann bis zu ca. 59 Sekunden dauern).
1. Öffnen Sie in Commerce Admin → Sales → Orders die Bestellung. Status ist **Halten** (`holded`); benutzerdefinierte Attribute schließen `lab_verification_code` mit einem zufälligen Wert ein.
1. Optional: Geben Sie zuerst eine Bestellung unter 50 $ auf - dieser Handler hält sie nicht zurück.

## Anwendungsfall 3: Ereignisgesteuerte Archivierung für ausgeführte Aufträge

Navigieren Sie zurück zum **Blueprint**-Schritt, um diesen Anwendungsfall zu starten.

### Blueprint-Phase

Geben Sie die folgende Eingabeaufforderung ein und klicken Sie auf **Blueprint erstellen**:

```text
When an order is saved with state holded, archive it to external storage and
record a reference that can be looked up later by order ID.

Add an event priority subscription on observer.sales_order_save_after, filtered to fire only when
state equals holded. From the event payload, extract:
- `entity_id`
- `payment.amount_ordered`
- `custom_attributes` (to read the `lab_verification_code` attribute set in Step 3)

The event handler must:
1. Persist the order details to the `held_orders` App Builder DB collection:
{
  "order_id": <entity_id>,
  "grand_total": <payment.amount_ordered>,
  "verification_code": <lab_verification_code>,
  "archived_at": <ISO timestamp>
}
2. Ensure the record can be looked up later by order ID.

The `held_orders` collection must exist before the handler runs:
- Provision persistent App Builder Database Storage in region `amer`.
- Create the collection during app installation.
- Create a unique index on `order_id` during installation.
- Drop the whole `held_orders` collection when the app is uninstalled.

Register the event handler separately from the existing cart validation webhook and high-value order hold action:
- runtime action: `order-archive/archive-held-order`
- non-web action
- `include-ims-credentials: true` on the archive action and the installation action

Follow the `commerce-app-storage` skill for DB auth, installation steps, and ext.config wiring.
Do not use custom IMS credential normalization or `Core.AuthClient.generateAccessToken`.
```

>[!NOTE]
>
> Achten Sie auf Folgendes:
>
> * Es wird ein Blueprint (v3) zur Erfassung der Anforderungen erstellt.
> * Die ursprünglichen Planaufgaben werden beibehalten.
> * Neue Aufgaben, die den neuen Anforderungen entsprechen, wurden hinzugefügt.

Verfeinern Sie den Blueprint nach Bedarf und klicken Sie dann auf **Plan genehmigen**, um fortzufahren.

### Entwickeln, Bereitstellen, Verknüpfen und Installieren

Folgen Sie dem gleichen Prozess wie in den vorherigen Anwendungsfällen, um von den Anforderungen zu einer installierten Anwendung zu wechseln - es ist nicht erforderlich, Integrationen neu zu konfigurieren.

>[!IMPORTANT]
>
> Um Änderungen an einer bereits verknüpften App zu erfassen, müssen Sie die Verknüpfung **aufheben** und **verknüpfen** erneut in der App-Verwaltung aktivieren.

### Funktionstests

1. Stellen Sie sicher, dass der Schwellenwert für Anwendungsfall 2 niedrig genug ist, um getestet zu werden (z. B. 50 $ in der App-Konfiguration).
1. Ordnen Sie eine Bestellung über diesem Schwellenwert an, sodass Anwendungsfall 2 sie zurückstellt (~30 Sekunden).
1. Öffnen Sie in Adobe Developer Console → Ihr Projekt → Staging → Events die Registrierung für das Archivierungsereignis „held-order“ (bei der Installation hinzugefügt oder aktualisiert).
1. Bestätigen Sie, dass ein Ereignis an diese Registrierung gesendet wurde, nachdem die Bestellung in den Haltebereich verschoben wurde. Verwenden Sie die Ereignisablaufverfolgung oder -überwachung für das mit `order-archive/archive-held-order` verknüpfte Commerce-Ereignis.

>[!NOTE]
>
> Ereignisse sind asynchron - erlauben Sie bis zu 30-59 Sekunden, nachdem die Bestellung zurückgestellt wurde.

## Fehlerbehebung

Wenn sich die von der geräteübergreifenden Analyse generierte Anwendung nicht wie erwartet verhält oder Fehler verursacht, bitten Sie den Agenten, die Fehlerbehebung in der Entwicklungsphase durchzuführen.

>[!NOTE]
>
> Die geräteübergreifende Analyse hat keine Einsicht in Schritte, die außerhalb der geräteübergreifenden Analyse stattfinden. Zuordnungs-, Installations-, Konfigurations- und Funktionstests werden alle in Commerce Admin, App Management oder der Storefront ausgeführt - nicht in der geräteübergreifenden Analyse. Wenn ein Problem in einem dieser Bereiche auftritt, kann der Agent es nicht sehen. Geben Sie ihm also das, was fehlt:
>
> * Was Sie getan haben und wo (z. B. „Auf Installieren in App Management geklickt„).
> * Was du erwartet hast, zu passieren.
> * Was ist passiert?
> * Der genaue Fehlertext oder die Fehlermeldung, die auf dem Bildschirm angezeigt wird.
> * Alle relevanten Fehler in der Browser-Konsole oder in den App Builder-Protokollen und Debugspuren zur Ereignisregistrierung von Adobe Developer Console.

Je konkreter der Bericht, desto besser kann der Agent das Problem diagnostizieren.

## Optionale Schritte

**Code herunterladen**

Um mit der Verfeinerung oder Bearbeitung in Ihrer bevorzugten IDE fortzufahren, laden Sie den von CDA generierten Code herunter, indem Sie auf der Symbolleiste des Explorers für die Entwicklungsphase auf das Symbol Herunterladen klicken. Wählen Sie einen Zielordner aus, klicken Sie auf **Speichern** und entpacken Sie dann das Arbeitsbereich-Paket.

>[!NOTE]
>
> Suchen Sie nach:
>
> * Alle im Entwicklungs-Staging-Explorer angezeigten Dateien befinden sich im entpackten Ordner.
> * Keine „Kompilierungsfehler“ beim Erstellen des Projekts mit `aio app build`.

Um dieselben Agentenfähigkeiten, die CDA verwendet, zu verwenden, installieren Sie diese in Ihrem Projektordner:

```bash
npx skills add adobe/aio-commerce-sdk --skill commerce-app-init -y && \
npx skills add adobe/aio-commerce-sdk --skill commerce-app-eventing -y && \
npx skills add adobe/aio-commerce-sdk --skill commerce-app-webhooks -y && \
npx skills add adobe/aio-commerce-sdk --skill commerce-app-business-config -y && \
npx skills add adobe/aio-commerce-sdk --skill commerce-app-storage -y && \
npx skills add adobe/skills --skill appbuilder-project-init -y
```

Starten Sie dann Ihre IDE oder CLI und beginnen Sie mit der Eingabeaufforderung.

**Kontext über Datei oder Link anhängen**

Anstatt direkt im Blueprint- oder Entwicklungs-Schritt dazu aufzufordern, können Sie den Kontext mithilfe einer Textdatei oder eines Links anhängen:

1. Klicken Sie auf das Anlagensymbol im Chat-Feld.
1. Klicken Sie auf **Datei hinzufügen**, um eine lokale Textdatei hochzuladen, oder geben Sie eine URL ein und klicken Sie auf **Link hinzufügen**, um Kontext über eine Remote-Datei hinzuzufügen.
1. Klicken Sie **Fertig** und geben Sie eine Eingabeaufforderung ein, um den Agenten zu bewegen.

>[!NOTE]
>
> Suchen Sie nach dem Agenten, der den Kontext aus Ihren Anlagen in die nächste Reihe integriert.

## Bekannte Probleme und Problemumgehungen

**Die Blueprint-Phase generiert keine Aufgaben**

Um die Blockierung aufzuheben und fortzufahren, bewegen Sie den Agenten, Aufgaben zu generieren.

**Die Schaltflächen zum Pushen und Abrufen von GitHub funktionieren nicht**

Laden Sie stattdessen die ZIP-Projektdatei aus der Entwicklungsphase herunter.

{{$include /help/_includes/commerce-developer-agent-related-links.md}}

## Zusätzliche Ressourcen

* [Übersicht über den Commerce Developer Agent](https://developer.adobe.com/commerce/extensibility/developer-agent/)
* [Erste Schritte mit dem Commerce Developer Agent](https://developer.adobe.com/commerce/extensibility/developer-agent/getting-started)
* [Aufforderungstipps für den Commerce Developer Agent](https://developer.adobe.com/commerce/extensibility/developer-agent/prompting)
* [Support und Feedback für Commerce Developer Agent](https://developer.adobe.com/commerce/extensibility/developer-agent/support)
