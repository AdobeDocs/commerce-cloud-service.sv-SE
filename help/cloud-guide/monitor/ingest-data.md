---
title: Intag av data
description: Lär dig hur du visar och hanterar dataöverföring i Commerce i New Relic.
feature: Cloud, Observability
exl-id: f88bf20c-604b-4986-b71c-bb726b2f00b8
source-git-commit: bf3debc5986d51a721537b52ffced58b2ee521ea
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Intag av data

New Relic är beroende av omfattande data för att kunna tillhandahålla effektiv övervakning och analys, men stora datauppsättningar kan påverka resultaten, prestandan och efterlevnaden i rätt tid. I det här avsnittet finns vägledning om hur du hanterar datainmatning och strategier för att förfina data så att de blir så effektiva som möjligt.

New Relic erbjuder _Datahantering_ en vy som sammanfattar din plananvändning per datakälla.

**Så här visar du dina importdata och -källor**:

1. På New Relic-menyn klickar du på **[!UICONTROL Manage your data]**.
1. Klicka **[!UICONTROL Data management]** i _Administration_ lista.

   ![Datahantering](../../assets/new-relic/data-ingestion.png)

   The **[!UICONTROL Data ingestion]** -fliken visar data som har importerats för dagen och datakällan.
Fliken för datalagring visar och styr hur länge data lagras.

1. Välj **[!UICONTROL Limits]** och se gränserna för ditt konto.

Datakällor för Adobe Commerce:

- **APM-händelser**—händelsedata som används i diagram och kontrollpaneler
- **Infrastruktur**—process- och värdstatistik, som processor, lagring, nätverk
- **Loggning**—loggar för CDN, APM och programserver

Loggdata bidrar till en stor del av intaget. Se hur man [Visa och analysera loggdata](log-management.md#view-and-analyze-log-data) och samarbeta med er Adobe-representant för att utforma en strategi för datainhämtning och lagring. Läs mer om [hantera datainhämtning](https://docs.newrelic.com/docs/data-apis/manage-data/manage-data-coming-new-relic/) i _New Relic-dokumentation_.
