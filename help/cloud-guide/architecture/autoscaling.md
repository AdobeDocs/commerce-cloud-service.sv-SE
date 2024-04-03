---
title: Automatisk skalning
description: Läs om hur Adobe Commerce i molninfrastruktur kan skalas upp för att tillgodose resurskrav.
feature: Cloud, Auto Scaling
topic: Architecture
exl-id: 2ba49c55-d821-4934-965f-f35bd18ac95f
source-git-commit: c61d711b1041ecf76ec6468cd225a34fd77c24b1
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# Automatisk skalning

Automatisk skalning lägger automatiskt till eller tar bort resurser i molninfrastrukturen för att upprätthålla optimala prestanda och rimliga kostnader. Den här funktionen är för närvarande endast tillgänglig för projekt som konfigurerats med en [Skalbar arkitektur](scaled-architecture.md).

## Webbservernoder

The [webbnivå](scaled-architecture.md#web-tier) skalas för att tillgodose en ökning av antalet processförfrågningar och högre trafikkrav. För närvarande skalas funktionen för automatisk skalförändring bara vågrätt genom att webbservernoder läggs till eller tas bort.

En automatisk skalningshändelse inträffar när CPU-användning och trafik når ett fördefinierat tröskelvärde:

- **Noder har lagts till**—CPU:er/kärnor i alla aktiva webnoder har 75 % kapacitet i 1 minut och trafiken ökar med 20 % under 5 minuter i följd.
- **Borttagna noder**—CPU:er/kärnor för alla aktiva webnoder läses in med 60 % under 20 minuter. Noderna tas bort i den ordning som de lades till.

Minimi- och maximitröskelvärdena fastställs och fastställs utifrån de avtalade resursgränserna för varje handlare. Detta minskar risken för oändlig skalning.

## Övervaka tröskelvärden med New Relic

Du kan använda [New Relic](../monitor/new-relic-service.md) för att övervaka vissa tröskelvärden, t.ex. värdantal och CPU-användning. Följande New Relic-frågor använder en variabelnotation för `cluster-id` till exempel bara.

>[!TIP]
>
>En referens om hur du skapar frågor finns på [NRQL-syntax, satser och funktioner](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/) i _New Relic_ dokumentation.
>Använd dina frågor för att skapa en [New Relic Dashboard](https://docs.newrelic.com/docs/query-your-data/explore-query-data/dashboards/introduction-dashboards/).

### Värdantal

Följande exempel på New Relic-fråga visar värdantalet i miljön:

```sql
SELECT uniqueCount(SystemSample.entityId) AS 'Infrastructure hosts', uniqueCount(Transaction.host) AS 'APM hosts seen' FROM SystemSample, Transaction where (Transaction.appName = 'cluster-id_stg' AND Transaction.transactionType = 'Web') OR SystemSample.apmApplicationNames LIKE '%|cluster-id_stg|%' TIMESERIES SINCE 3 HOURS AGO
```

På följande skärmbild **APM-värdar** refererar till antalet värdar med transaktioner som loggats under den valda perioden.

![New Relic-värdantal](../../assets/new-relic/host-count.png)

### CPU-användning

Följande exempel på New Relic-fråga visar processoranvändning för webbnoder:

```sql
SELECT average(cpuPercent) FROM SystemSample FACET hostname, apmApplicationNames WHERE instanceType LIKE 'c%' TIMESERIES SINCE 3 HOURS AGO
```

![CPU-användning för New Relic-webbnoder](../../assets/new-relic/web-node-cpu-usage.png)

## Aktivera automatisk skalförändring

Om du vill aktivera eller inaktivera automatisk skalning för ditt Adobe Commerce i molninfrastrukturprojekt [Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). Välj följande orsaker i biljetten:

- **Kontaktorsak**: Begäran om infrastrukturändring
- **Orsak till kontakt med Adobe Commerce-infrastruktur**: Annan begäran om ändring av infrastruktur

>[!IMPORTANT]
>
>Funktionen för autoskalning fångar upp oväntade händelser. Även om automatisk skalförändring är aktiverat rekommenderar Adobe att du fortsätter [Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om du förväntar dig en kommande händelse.

### Belastningstestning

Adobe aktiverar automatisk skalning i ditt Cloud-projekt _mellanlagring_ kluster först. När du har utfört och slutfört inläsningstestning i din miljö aktiverar Adobe sedan automatisk skalning i ditt produktionskluster. Anvisningar om lastprovning finns i [Prestandatestning](../launch/checklist.md#performance-testing).

### IP TILLÅTELSELISTA

När automatisk skalning har aktiverats kommer den utgående webbnodstrafiken från tjänstnodernas IP-adresser. Om du använder ett tillåtelselista med en tredjepartstjänst som inte medföljer ditt Adobe Commerce i ett molninfrastrukturprojekt bör du kontrollera IP-adresserna i tillåtelselista för tredjepartstjänsten.

Exempel:

- Om tillåtelselista innehåller IP-adresserna för dina tjänstnoder (1, 2 och 3) behövs ingen åtgärd.
- Om tillåtelselista innehåller IP-adresserna för dina tjänstnoder (1, 2 och 3) och webbnoder (4, 5 och 6) - i det här fallet alla sex noder - krävs ingen åtgärd.
- Om tillåtelselista innehåller IP-adresserna _endast_ för dina webbnoder (4, 5 och 6) måste du uppdatera tillåtelselista så att den innehåller IP-adresserna för tjänstnoderna.
