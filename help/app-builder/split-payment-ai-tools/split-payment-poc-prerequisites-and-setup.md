---
title: 'Aufspaltung des Zahlungs-POC: Voraussetzungen und Einrichtung der Umgebung'
description: Learn how to set up Commerce, Admin for COD and store credit, OAuth integration, I/O Events, App Builder, and aio CLI before the split payment build prompts.
feature: App Builder, Configuration, Eventing, Extensibility, Paas, Payments, REST
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Tutorial
duration: 262
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 1e2c7e0e6d0f2d174b88406ce3fb7c787676ecee
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 1%

---

# Aufspaltung des Zahlungs-POC: Voraussetzungen und Einrichtung der Umgebung

Complete every step in this tutorial before you run any of the build prompts. Missing a single step is the most common reason the flow breaks mid-tutorial.

## 1. Adobe Commerce requirements

* Adobe Commerce **2.4.5 or later** (on-premises or Commerce Cloud)
* Git access to the Commerce project (you add a module under `app/code/`)
* Access to **[!UICONTROL Commerce Admin]**

### Commerce Cloud only: enable I/O eventing

Add the following to `.magento.env.yaml` and deploy before you add the module:

```yaml
stage:
  global:
    ENABLE_EVENTING: true
```

> **Warning:** This deploy must finish successfully before the I/O Event module dependency can resolve.


## 2. Commerce Admin configuration

Do these steps before anything else. Der Checkout-JavaScript hängt von den exakten Zeichenfolgen-Übereinstimmungen ab.

### 2a. Enable Cash on Delivery with the exact title

**[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Payment Methods]** > **[!UICONTROL Cash On Delivery Payment]**

* **[!UICONTROL Enabled]**: **Ja**
* **[!UICONTROL Title]**: **`Cash`** (this exact string is what the checkout JavaScript matches)

> **Note:** If your store uses a different cash-on-delivery (COD) implementation or title, adjust `payment-method-helper.js` in the Commerce module.

### 2b. Enable store credit

**[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Customers]** > **[!UICONTROL Customer Configuration]** > **[!UICONTROL Store Credit Options]**

* **[!UICONTROL Enable Store Credit Functionality]**: **Ja**

### 2c. Hinzufügen von Warenkorb-Guthaben zu einem Testkunden

**[!UICONTROL Customers]** > **[!UICONTROL All Customers]** > *[Ihr Testkunde]* > **[!UICONTROL Store Credit]** > **[!UICONTROL Update Balance]**

Fügen Sie mindestens **$ 50** als Warenkorb hinzu. Testen Sie mit einer Bestellung unter insgesamt $100.

### 2 T. Erstellen der Commerce-Integration

**[!UICONTROL System]** > **[!UICONTROL Integrations]** > **[!UICONTROL Add New Integration]**

* **[!UICONTROL Name]**: `Split Payment App Builder` (oder ein beliebiger Name)
* Geben Sie auf der Registerkarte **[!UICONTROL API]** mindestens Folgendes ein:
   * `Magento_Sales::actions` (erforderlich für den `cash-received`-Endpunkt)
   * `Magento_Sales::cancel` (erforderlich für den `cash-decline`-Endpunkt)
   * Verwaltung von Angeboten oder Warenkörben (vollständig oder eine relevante Teilmenge)
   * **[!UICONTROL Customer balance]** (vollständig oder eine relevante Teilmenge)

Wählen Sie **[!UICONTROL Save]** und dann **[!UICONTROL Activate]** aus.

**Kopieren Sie alle vier Werte; sie werden nur einmal angezeigt:**

| Wert | Umgebungsvariable |
| --- | --- |
| Consumer Key | `COMMERCE_CONSUMER_KEY` |
| Verbrauchergeheimnis | `COMMERCE_CONSUMER_SECRET` |
| Zugriffstoken | `COMMERCE_ACCESS_TOKEN` |
| Zugriffstoken-Geheimnis | `COMMERCE_ACCESS_TOKEN_SECRET` |

Speichern Sie diese Werte sicher. Sie benötigen sie in jeder App Builder-`.env`.


## &#x200B;3. Adobe Developer Console und App Builder

* Zugriff auf eine Adobe Developer Console-Organisation
* Ein **App Builder-Projekt** (neu oder wiederverwendet)
* Ein Arbeitsbereich wurde konfiguriert. Die Eingabeaufforderungen gehen von **[!UICONTROL Stage]** aus
* **[!UICONTROL Adobe I/O Events]** wurde als Service zum Arbeitsbereich hinzugefügt
* **Commerce** als Ereignisanbieter für den Arbeitsbereich verbunden

Der im Konzeptnachweis verwendete Ereigniscode lautet: `com.adobe.commerce.observer.sales_order_place_before`

Wenn Sie Commerce nicht als Ereignisanbieter verbunden haben, finden Sie weitere Informationen unter [Konfigurieren von Commerce zum Ausgeben von Ereignissen an Adobe I/O](https://developer.adobe.com/commerce/extensibility/events/configure-commerce/){target="_blank"} im Commerce-Erweiterbarkeitshandbuch.


## &#x200B;4. Lokale Entwicklungsumgebung

```bash
# Required versions
node --version    # 18.x or later
npm --version     # any recent version

# Adobe I/O CLI
npm install -g @adobe/aio-cli

# Authenticate
aio login

# Select your project and workspace
aio app use
# Confirm the org, project, and workspace shown are correct
```


## &#x200B;5. Zwei Projektverzeichnisse

In diesem Tutorial werden zwei separate Ordnerstämme verwendet. Getrennt halten.

**Commerce-Projektstamm** (Ihr Magento-Git-Repository):

```text
<commerce-root>/
└── app/code/Client/SplitPayment/   ← Module goes here
```

**Stammordner des App Builder**-Projekts (der `split-payment-orchestrator` aus dem Quellpaket oder ein neues Projekt, das Sie erstellen):

```text
split-payment-orchestrator/
├── app.config.yaml
├── package.json
├── .env                            ← Copy from .env.example, then fill in
└── actions/
```


## &#x200B;6. entity_id verglichen mit increment_id

> **Verwenden Sie in REST-Aufrufen immer `entity_id` (die numerische Datenbank-ID), nicht `increment_id` (z. B. `000000042`)**

`entity_id` finden Sie in der **[!UICONTROL Commerce Admin]**-URL:

```text
/admin/sales/order/view/order_id/42/   →   entity_id = 42
```

Oder vom Simulationsskript:

```bash
node scripts/simulate-split-payment.mjs show 42
```


## &#x200B;7. Der Schwellenwert von 100 Dollar

Die aufgeteilte Zahlungs-Benutzeroberfläche und der Schwellenwert-Guard zielen auf Bestellungen **$100.00 oder weniger** ab. Der Fluss verhält sich wie folgt:

* **Bei oder unter 100 $:** die Benutzeroberfläche für aufgeteilte Zahlungen angezeigt. Der Kunde kann eine Aufteilung von Bargeld und Warenkorb festlegen.
* **Über $100:** `CheckoutPlugin` gibt beim Zahlungsschritt einen Fehler aus

Um zu testen, erstellen Sie einen Warenkorb, dessen Zwischensumme, Versand und Steuer **kleiner oder gleich 100 $)** z. B. ein Produkt unter 90 $, sodass Versand und Steuer immer noch unter die Obergrenze passen).

Der Schwellenwert wird gespeichert in:

* Commerce-Konfiguration: `split_payment/general/threshold` (Standard-`100` in `etc/config.xml`)
* App Builder-Umgebung: `PAYMENT_THRESHOLD=100` (muss mit Commerce übereinstimmen)


## &#x200B;8. Fastly (nur Commerce Cloud)

App Builder-Aktionen rufen Commerce über REST auf (`/rest/V1/split-payment/orders/...`). Wenn Ihr Commerce Cloud-Projekt Fastly mit IP-Zulassungsauflistung verwendet, müssen die Egress-IP-Adressen der App Builder-Laufzeitumgebung auf die Zulassungsliste gesetzt werden.

**Überprüfen:** Sie zuerst das Simulationsskript aus (direkte cURL mit OAuth-Signierung). Wenn dies funktioniert, die App Builder-Aktion jedoch `403` zurückgibt, blockiert Fastly wahrscheinlich die Anfrage.

Verwenden Sie die aktuelle Dokumentation von Adobe für App Builder Egress-IP-Bereiche und fügen Sie sie nach Bedarf zu Ihrer Fastly-Konfiguration hinzu.


## Verifizierungs-Checkliste

Bevor Sie mit den Buildaufforderungen beginnen, bestätigen Sie Folgendes:

* [ ] Commerce-Version ist 2.4.5 oder höher
* [ ] I/O-Eventing ist aktiviert (Commerce Cloud) und wird bereitgestellt
* [ ] Nachnahme ist aktiviert, wobei der Titel exakt auf `Cash` gesetzt ist
* [ ] Store-Guthaben ist aktiviert
* [ ] Der Testkunde hat mindestens 50 USD Warenkorb-Guthaben.
* [ ] Die Commerce-Integration wird erstellt und aktiviert, und alle vier OAuth-Werte werden gespeichert
* [ ] Für das App Builder-Projekt ist der I/O Events-Service und der Commerce Event Provider konfiguriert
* [ ] `aio login` ist abgeschlossen und der richtige Arbeitsbereich wird mit `aio app use` ausgewählt
* [ ] Node.js 18 oder höher wird installiert und die `aio` CLI wird installiert
* [ ] `.env` Dateien werden pro ([ POC: Umgebungsvariablen-Referenz](split-payment-poc-env-reference.md) (und Ihr Quellpaket, falls Sie eines verwenden) vorbereitet


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
