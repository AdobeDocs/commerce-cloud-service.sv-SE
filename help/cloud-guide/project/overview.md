---
title: Molninfrastrukturprojekt
description: Läs en översikt om Adobe Commerce om molninfrastruktur [!DNL Cloud Console] och lär dig hur du får åtkomst till kontoinställningarna.
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: ae862898-9b4d-45ed-b370-e82cc6f99017
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Molninfrastrukturprojekt

Adobe Commerce on cloud infrastructure project innehåller all kod i Git-grenar, tillhörande miljöer och skript för att distribuera [!DNL Commerce] program. Miljöer innehåller tjänster som stöder [!DNL Commerce] -program, inklusive en databas, webbserver och cachningsserver.

Adobe tillhandahåller en [!DNL Cloud Console] och utvecklingsverktyg för att hantera alla aspekter av ditt projekt. Som kontoägare har du fullständig åtkomst till alla miljöer.

## [!DNL Cloud Console]

The [!DNL Cloud Console] innehåller interaktiva metoder för att skapa, hantera och distribuera Commerce-kod i ett användarvänligt format. [Logga in på [!DNL Cloud Console]](https://console.adobecommerce.com) för att visa projektlistan. Du kan bara se projekt som du har behörighet att använda som administratör eller för särskilda miljötyper. Om du är Adobe Solutions Partner kan du se flera projekt för kunder som du stöder.

>[!TIP]
>
>Om du inte ser några projekt måste du kontakta [Kontoägare eller projektadministratör](../project/user-access.md) som är associerad med projektet och begär åtkomst. För förstagångsanvändare, se [Onboarding-ämne](../../get-started/onboarding.md#cloud-console) i _Kom igång_ guide.

The _Alla projekt_ visar en lista över alla projekt som du har behörighet att komma åt. Klicka **[!UICONTROL Show filters]** och filtrera projektlistan efter typ, region eller plan.

![Projektlista](../../assets/ui-allprojects-list.png)

### Projektöversikt

Välja ett projekt i _Alla projekt_ öppnar projektöversikten. I projektöversikten visas alltid ett projektnavigeringsfält, som innehåller en miljöväljare och en konfigurationsknapp:

![Projektnavigering](../../assets/project-nav.png)

I projektöversikten visas en sammanfattning av projektinformationen i förhandsvisningsområdet, så länge du inte har valt någon miljö:

- Projektnamn
- Region, projekt-ID
- Planera, allokerad lagring, miljöer, användare
- Storefront URL med **[!UICONTROL Set a custom domain]** knapp

Och i huvudprojektöversikten:

- Miljövyn visar en lista eller trädvy med ![aktiv gren](../../assets/icon-active.png){width="32"} (active) and ![inactive branch](../../assets/icon-inactive.png){width="32"} (inaktiva) miljöer.
- [Aktivitetsström](activity-stream.md) visar pågående, väntande och senaste aktiviteter för projektet.
<!-- - Apps & Services—Shows a topology of service containers -->

För **Starter** projekt, det finns en hierarki med grenar från `master` (Produktion). Alla förgreningar som du skapar visas som underordnade i `master` gren. Adobe rekommenderar att du skapar en `staging` förgrening, skapa sedan en `integration` för utveckling. Se [Startarkitektur](../architecture/starter-architecture.md).

För **Pro**, finns det en hierarki med grenar som börjar från `production` till `staging` till `integration`. The ![Dedikerad ikon](../../assets/icon-dedicated.png){width="32"} ikon anger att grenen distribuerar till en dedikerad miljö. Alla förgreningar som du skapar visas som underordnade `integration` gren. Se [Pro-arkitektur](../architecture/pro-architecture.md).

![Miljölista för Pro](../../assets/pro-environments.png)

### Miljööversikt

Om du väljer en miljö i projektnavigeringsfältet ändras översikten och navigeringsfältet så att det fokuserar på den valda miljön. Navigeringsfältet innehåller förgreningskontroller (förgrening, sammanfogning och synkronisering) och en konfigurationsknapp:

![Miljö vald](../../assets/environment-selected.png)

I miljööversikten visas en sammanfattning av miljöinformationen i förhandsvisningsområdet:

- Miljönamn, typ
- Region, projekt-ID
- Datum och tid för senaste aktivitet, inklusive säkerhetskopiering
- HTTP-åtkomst och sökmotorstatus
- Datornamn som tilldelats miljön
- Miljöstatus (aktiv eller inaktiv)
- Storefront URL med **[!UICONTROL Set a custom domain]** knapp

Och i huvudmiljööversikten:

- [Aktivitetsström](activity-stream.md) utgör huvudmiljööversikten och visar pågående, väntande och senaste aktiviteter för den valda miljön.
<!-- - Services tab shows and Apps & Services menu, including overview and configuration tabs for each service. -->
- [Fliken Säkerhetskopior](../storage/snapshots.md#create-a-manual-backup) innehåller en lista med lagrade säkerhetskopior, historik över säkerhetskopieringsåtgärder och knappen Säkerhetskopiera.

### Åtkomstbutik

Varje aktiv miljö har en bakgrund. Välj en miljö i den översta navigeringen och klicka på URL-adressen i miljööversikten. Dessutom finns det en **[!UICONTROL URLs]** till höger ovanför listan Activity (Aktivitet).

Webbåtkomstadressen kan innehålla följande:

```terminal
https://<branch>-<unique-ID>-<project-ID>.<region>.magentosite.cloud/
```

- **Unikt ID** = 7 slumpmässiga alfanumeriska tecken
- **Projekt-ID** = projekt-ID med 13 tecken
- **Län** = AWS- eller Azure-regionens namn, se [Regionala IP-adresser](regional-ip-addresses.md)

Proproduktion- och mellanlagringsmiljöerna innehåller tre noder som du kommer åt via följande länkar:

- URL för belastningsutjämnare:

   - `http[s]://<your-domain>.c.<project-ID>.ent.magento.cloud`
   - `http[s]://<your-staging-domain>.c.<project-ID>.ent.magento.cloud`

- Direktåtkomst till en av de tre redundanta servrarna:

   - `http[s]://<your-domain>.{1|2|3}.<project-ID>.ent.magento.cloud`
   - `http[s]://<your-staging-domain>.{1|2|3}.<project-ID>.ent.magento.cloud`

  Produktions-URL:en används av leveransnätverket (CDN).

## Inställningar

Öppna _Inställningar_ genom att klicka på ![konfigurera projektikon](../../assets/icon-configure.png){width="36"} (konfigurera) ikon till höger om projektnavigeringen.

### Projektinställningar

**[!UICONTROL Project Settings]** utökar en meny med kontroller på projektnivå för att hantera användare, variabler och mycket annat:

| Alternativ | Beskrivning |
|--------------|-------------------------------------------------------------------------------------------------------------------------------|
| Allmänt | Hantera tidszonen för användning med schemaläggning av säkerhetskopieringar eller underhåll. |
| Åtkomst | Hantera [användaråtkomst](user-access.md) till projekt- och miljötyper. |
| Certifikat | Visa en lista över SSL-certifikat som är associerade med projektet. |
| Distribuera nyckel | Lägg till och visa den offentliga nyckeln i projektkoddatabasen. |
| Domäner | Lägg till ett domännamn i projektet. Se [Hantera domäner](../cdn/fastly-custom-cache-configuration.md#manage-domains). |
| Integreringar | Lägg till och hantera [integreringar](../integrations/overview.md), t.ex. hälsomeddelanden och webbhooks. |
| Variabel | Lägg till [projektnivåvariabler](../environment/variable-levels.md) som är tillgängliga vid byggandet och körningen i alla miljöer. |

{style="table-layout:auto"}

### Miljöinställningar

Klicka **[!UICONTROL Environments]** och välj en specifik miljö i listan för kontroller för att hantera platsinställningar, miljövariabler med mera:

| Alternativ | Beskrivning |
| --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Allmänt | Konfigurera visningsnamn, miljötyp och överordnad miljö.<br>Växla mellan olika miljöinställningar: |
|           | **Aktivera utgående e-post**: Skicka [utgående e-post](outgoing-emails.md) från miljön med protokollet SMTP. |
|           | **Dölj från sökmotorer**: Blockera sökmotorindexerare och crawlningar från webbplatsen. |
|           | **HTTP-åtkomstkontroll**: Aktivera säkerhetskonfiguration för [!DNL Cloud Console] med en inloggnings- och IP-adressåtkomstkontroll. |
|           | Status är `active` eller `inactive`. Det mesta av ditt arbete är i en aktiv miljö. Du kan inaktivera eller ta bort miljön. |
| Variabel | Visa, skapa och hantera [miljönivåvariabler](../environment/variable-levels.md) som är tillgängliga vid körning. |
| Domäner | Visa en lista med [konfigurerade vägar](../routes/routes-yaml.md). |

{style="table-layout:auto"}

>[!WARNING]
>
>**GÖR INTE** Använd HTTP-åtkomstkontrollmetoden för att skydda Pro Staging- och Production-miljöer. Det här avbryter cachelagring. Använd i stället [Blockera](../cdn/fastly-vcl-blocking.md) finns i Fast CDN för Adobe Commerce.

## Snabbt och New Relic

Ditt projekt innehåller [Snabbt](../cdn/fastly.md) och [New Relic](../monitor/new-relic-service.md). Projektinformationen visar information för din projektplan och viktiga licenser och tokens för dessa integreringar. Endast licensägaren har initial åtkomst till autentiseringsuppgifterna och tjänsterna. Ge de här autentiseringsuppgifterna till tekniska resurser och utvecklarresurser efter behov.

- [Snabbt](https://www.fastly.com/) tillhandahåller innehållsleverans (CDN), bildoptimering och säkerhetstjänster (DDoS och WAF) för dina Adobe Commerce i molninfrastrukturprojekt. Se [Få inloggningsuppgifter snabbt](../cdn/fastly-configuration.md#get-fastly-credentials).

- [New Relic](../monitor/new-relic-service.md) ger programmått och prestandainformation för miljöer för förproduktion och produktion.

Använd [Cloud CLI](../dev-tools/cloud-cli-overview.md) för att granska integreringstoken, ID:n med mera:

```bash
magento-cloud subscription:info services
```
