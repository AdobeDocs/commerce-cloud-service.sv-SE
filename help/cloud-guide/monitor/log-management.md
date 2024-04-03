---
title: New Relic logghantering
description: Lär dig använda New Relic-loggen
feature: Cloud, Logs, Observability
exl-id: d8afb5c0-9727-4123-8944-81cd6ad7cbb7
source-git-commit: ebe1746ee9fd08480da5ad07d7f1f8299ad9af7e
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# New Relic logghantering

Alla molninfrastrukturprojekt innehåller [New Relic logghantering](https://docs.newrelic.com/docs/logs/get-started/get-started-log-management/). Tjänsten är förkonfigurerad för att samla alla loggdata från din miljö för förproduktion och produktion och visa dem i en centraliserad kontrollpanel för logghantering.

De aggregerade uppgifterna innehåller information från följande loggar:

- Alla `ece-tools` och programloggar från `~/var/log` katalog
- Loggar för molntjänster från `var/log/platform/<project-ID>` katalog
- Snabbt CDN och WAF

När ditt projekt är anslutet till New Relic kan du använda tjänsten New Relic Logs för att utföra följande uppgifter:

- Använd New Relic-frågor för att söka efter aggregerade loggdata
- Visualisera loggdata via programmet New Relic Logs
- Skapa egna diagram, kontrollpaneler och aviseringar
- Felsöka prestandaproblem från en enda kontrollpanel

## Visa och analysera loggdata

Använd New Relic Logs-programmet för att söka igenom samlade loggdata och felsöka program-, infrastruktur-, CDN- och WAF-fel. Du kan skapa diagram, kontrollpaneler och aviseringar med loggdata som samlats in från New Relic APM och infrastrukturtjänster.

**Så här använder du New Relic Logs-programmet**:

1. Logga in på [New Relic](https://login.newrelic.com/login).

1. Välj **Loggar** på menyn i Utforskaren.

1. Verifiera att ditt konto är markerat högst upp i _Alla loggar_ vy.

1. Välj ett tidsintervall för loggfrågan.

1. Granska infrastrukturloggdata för molntjänster (loggar från `~/var/log/`) anger du frågesträngen `has: "filePath"` i _Sök efter loggar_ fält. Klicka sedan på **[!UICONTROL Query logs]**.

   Namnen på loggfilerna lagras i `filePath` -kolumn, med fullständiga sökvägar till loggfilen.

   ![Data i New Relic-tjänstloggen för molnprojekt](../../assets/new-relic/var-log-query.png)

1. Om du snabbt vill granska loggdata anger du frågesträngen `has: "client_ip"` i _Sök efter loggar_ fält. Klicka sedan på **[!UICONTROL Query logs]**.

1. Om du vill filtrera loggresultaten efter landskod klickar du på **[!UICONTROL Add column]** väljer **[!UICONTROL geo_country_code]**.

   ![New Relic CDN-loggattributfilter för molnprojekt](../../assets/new-relic/fastly-countrycode-filter.png)

>[!TIP]
>
>Du kan spara frågevyn från _Sparade vyer_ nedrullningsbar meny. Klicka **[!UICONTROL Create new]**, ange ett namn, markera alternativ och klicka på **[!UICONTROL Save view]**.
>
>Se [Kom igång med logghantering](https://docs.newrelic.com/docs/logs/get-started/get-started-log-management/) och [Introduktion till New Relic-frågespråket](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/introduction-nrql-new-relics-query-language/) på _New Relic Docs_ webbplats.
