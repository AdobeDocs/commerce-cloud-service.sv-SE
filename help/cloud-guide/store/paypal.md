---
title: Ställ in PayPal-betalningsmetoder
description: Ställ in betalningsmetoder för PayPal för Adobe Commerce i molninfrastruktur.
feature: Cloud, Checkout, Payments
exl-id: e52fd719-f936-4e8b-8222-af133389d9e2
source-git-commit: aa1a334ca1383559194ca75247679c6fb5411802
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Ställ in PayPal-betalningsmetoder

Adobe Commerce i molninfrastrukturen erbjuder ett startverktyg som konfigurerar PayPal Express Checkout-konton direkt via Admin. Detta verktyg är tillgängligt för ECE 2.1.8 och senare. Om du vill ha bättre stöd för att gå live och testa betalningsmetoder för PayPal kan du aktivera och konfigurera ditt PayPal Express-utcheckningskonto för sandbox- eller produktionskonton.

Du kan konfigurera sandlådan eller produktionskontot i alla miljöer:

* För integrerings- och mellanlagringsmiljöer anger du autentiseringsuppgifter för sandlådan.
* I din produktionsmiljö anger du sandlådeinloggningsuppgifter för inledande testning och ersätter dem sedan med Live-produktionsuppgifter för en butik som har startats.

## PayPal-konto

Det är bäst att använda ett PayPal-handelskonto som har förberetts och konfigurerats, men du kan skapa ett konto eller uppgradera ett personligt konto via administratören.

[!DNL PayPal onboarding] stöder anslutning med följande konton:

* PayPal Business Account
* PayPal personligt konto, konverterar till ett företagskonto. Om du har ett befintligt personligt PayPal-konto kan du logga in med dessa autentiseringsuppgifter och uppgradera det här kontot till ett företagskonto när du slutför synkroniseringen.

Om du inte har något befintligt PayPal-konto skapar du ett. Ange en e-postadress för ett nytt konto. Om inget matchande PayPal-konto hittas följer du anvisningarna för att skapa ett PayPal Business-konto. Du kan också skapa ett konto direkt via [PayPal](https://www.paypal.com/us/webapps/mpp/account-selection).

### PayPal-begränsningar

PayPal har stöd för anslutning av PayPal Express Checkout för länder över hela världen, med undantag för följande begränsningar:

* Indien och Japan (framtida PayPal-uppdateringar kan stödja dessa konton)
* Israel

För Brasilien måste du ha ett befintligt PayPal-företagskonto för att kunna ansluta. Du kan inte konvertera ett befintligt personligt PayPal-konto för Brasilien under den här processen. Om du behöver ett konto, [skapa ett PayPal-företagskonto](https://www.paypal.com/us/webapps/mpp/account-selection).

## Konfigurera PayPal Express-kassan

Så här konfigurerar du PayPal Express Checkout:

1. Gå till Admin for the environment.
1. I navigeringen till vänster väljer du **Lager** > **Konfiguration** väljer **Försäljning** > **Betalningsmetoder**.
1. För PayPal väljer du **Konfigurera**. Konfigurationsfält visas i expanderbara avsnitt för Express Checkout, Adverise PayPal Credit samt Basic and Advanced settings.
1. Anslut ditt PayPal-konto. Tills kontot är anslutet inaktiveras alternativen för att aktivera. Mer information om tillgängliga och stödda konton för anslutning och begränsningar finns i [PayPal-konto](#paypal-account).

   * Om du vill ansluta ditt PayPal-Live-konto klickar du på Anslut med PayPal och följer anvisningarna. Alla kundköp som görs via en PayPal som är komplett och aktivt debiterar kunderna i en direktbutik.
   * Om du vill ansluta ditt sandlådekonto för testning klickar du på Autentiseringsuppgifter för sandlådan och följer anvisningarna. Alla kundköp som använder en sandbox PayPal är slutförda utan att aktivt debitera kunderna.

1. Konfigurera inställningarna för Express Checkout för att autentisera och använda API:t för PayPal:

   * **E-post associerad med PayPal Merchant-konto** (Valfritt) Ange den e-postadress som är kopplad till ditt PayPal-handelskonto. E-postmeddelandet är skiftlägeskänsligt.
   * **API-autentiseringsmetoder** som API-signatur eller API-certifikat.
   * API-användarnamn, lösenord och signatur som hämtats från ditt PayPal-konto.
   * **Sandlådeläge** Välj Ja eller Nej för att ange om inloggningsuppgifterna som du angav gäller för sandlådan. Om du har angett produktionsuppgifter väljer du Nej.
   * **API använder proxy** Välj Ja eller Nej för att ange om systemet använder en proxyserver för att upprätta en anslutning mellan Adobe Commerce och betalningssystemet PayPal. Om Ja, ange proxyvärden och port.

1. Detaljerad information och anvisningar för hur du konfigurerar ditt konto finns i [PayPal Express-kassan](https://docs.magento.com/user-guide/payment/paypal-express-checkout.html) som börjar med steg 2 Slutför inställningarna.

Med kontot konfigurerat och autentiserat kan du aktivera och inaktivera betalningsalternativ för PayPal under Obligatoriska PayPal-inställningar:

* **Aktivera den här lösningen** visar betalningsmetoden PayPal för kunder via webbplatsen.
* **Aktivera sammanhangsbaserad utcheckning**
* **Aktivera PayPal-kredit** ger kunderna möjlighet att använda PayPal-kredit utan extra kostnader. PayPal betalar ordern i förskott och hanterar alla återbetalningar för krediten direkt med kunden.

## PayPal-variabler

När du använder PayPal on-boarding-verktyget med Adobe Commerce i molninfrastrukturen lägger du till följande variabel i `variables:env` i `magento.app.yaml` -fil.

```yaml
# Environment variables
variables:
  env:
    CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
```

Om du uppgraderar till 2.2 från 2.1.8 eller senare måste du fortfarande lägga till den här variabeln.
