---
title: Hälsoaviseringar
description: Lär dig hur du konfigurerar Slack, e-post och PagerDuty-meddelanden för diskutrymmesanvändning i ditt Adobe Commerce i molninfrastrukturprojekt.
feature: Cloud, Observability, Integration
exl-id: d3173098-78ed-42a8-aeb3-9ccbaccc4d32
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Hälsoaviseringar

Adobe Commerce i molninfrastruktur övervakar diskutrymmesanvändningen i alla program och tjänster i Starter-miljön eller i Pro-integreringsmiljön. En databasdisk som tar slut på utrymme kan orsaka skadade data. Hälsostatuskontrollen utförs var femte minut och kan meddela dig via e-post eller annan extern tjänst. Det finns tre felmeddelanden på hårddisken för hälsomeddelanden:

- **Varning**—tillgängligt diskutrymme minskar till mindre än 20 %
- **Kritisk**—tillgängligt diskutrymme minskar till mindre än 10 %
- **Helt klar**—tillgängligt diskutrymme återgår till över 20 % efter en händelse på grund av låg disknivå

>[!NOTE]
>
>I Pro Production-miljöer kan du övervaka diskutrymmet med hjälp av varningspolicyn för Adobe Commerce för New Relic. Se [Övervaka prestanda med hanterade aviseringar](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts).

## E-postaviseringar

Integreringen av e-post för hälsa kräver en ursprungsadress och minst en mottagaradress. Du kan använda samma e-postadress för `from-address` och `recipients` adress. I följande exempel registreras en e-postintegration för hälsa med två mottagare:

```bash
magento-cloud integration:add --type health.email --from-address you@example.com --recipients them@example.com --recipients others@example.com
```

## Meddelanden via Slack-kanal

Slack är en extern tjänst som använder interaktiva appar som kallas bots för att publicera meddelanden i ett chattrum. Innan du kan ta emot hälsomeddelanden i Slack måste du skapa en [robotanvändare](https://api.slack.com/bot-users) för Slack. När du har konfigurerat robotanvändaren för kanalen, eller kanalerna, sparar du [bocktoken](https://api.slack.com/docs/token-types#bot) som tillhandahålls av Slack för att registrera din integrering. I följande exempel registreras hälsomeddelanden i en Slack-kanal:

```bash
magento-cloud integration:add --type health.slack --token SLACK_BOT_TOKEN --channel '#slack-channel-name'
```

## PagerDuty notifications

PagerDuty är en extern tjänst som kan meddela medlemmar i kontaktgruppen om viktiga problem. Innan du kan ta emot hälsomeddelanden i PagerDuty måste du skapa en [PagerDuty integration](https://developer.pagerduty.com/v2/docs/integrating) som använder Event API version 2. Använd integreringsnyckeln, eller _routningsnyckel_ för att registrera integreringen. I följande exempel registreras meddelanden för PagerDuty med en routningsnyckel:

```bash
magento-cloud integration:add --type health.pagerduty --routing-key PAGERDUTY_ROUTING_KEY
```
