---
title: New Relic
description: Läs mer om New Relic-tjänsten som finns i ditt Adobe Commerce i molninfrastrukturprojekt.
feature: Cloud, Observability
last-substantial-update: 2023-09-06T00:00:00Z
exl-id: 613f0694-5338-4037-8ee4-ac5eca376159
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Översikt över tjänsten New Relic

I alla Adobe Commerce-projekt om molninfrastruktur ingår tillgång till New Relic-tjänsten för att övervaka prestandan och undersöka händelser i [!DNL Commerce] program- och molninfrastruktur.

Följande New Relic-funktioner kan användas i produktions- och mellanlagringsmiljöer:

- [NEW RELIC APM](#new-relic-apm) (Pro och Starter)
- [New Relic Infrastructure](#new-relic-infrastructure) (Endast Pro)
- [New Relic Log Management](#new-relic-logs) (Endast Pro)

>[!INFO]
>
>Andra New Relic-funktioner är inte tillgängliga i Adobe Commerce-projekt.

## NEW RELIC APM

[New Relic för hantering av programprestanda (APM)](https://docs.newrelic.com/introduction-apm/) är en programanalysprodukt som hjälper er att analysera och förbättra applikationsinteraktioner. New Relic APM är tillgängligt för alla Adobe Commerce i molninfrastrukturprojekt och har följande funktioner:

- **Fokusera på specifika transaktioner**- Markera och övervaka aktivt viktiga kundåtgärder på er webbplats, t.ex. tillägg i kundvagnen, utcheckning eller bearbetning av en betalning.
- **Övervakning av databasfråga**—Leta upp och övervaka databasfrågor som påverkar prestandan.
- **Appkarta**—Visa alla programberoenden på din plats, tillägg och externa tjänster.
- **[!DNL Apdex]bakgrundsmusik**- Utvärdera prestanda och skapa varningar som identifierar problem och meddelar dig när de inträffar, t.ex. om webbplatsen påverkas av en Flash-försäljning eller en webbhändelse. Se [Apdex-poäng](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction/).
- **Hanterade aviseringar för Adobe Commerce**-Använd den här New Relic-varningspolicyn för att övervaka program- och infrastrukturprestanda baserat på bästa praxis i branschen. Se [Övervaka prestanda med Hanterade aviseringar för Adobe Commerce aviseringspolicy](investigate-performance.md/#monitor-performance-with-managed-alerts).
- **Spåra distributioner**—Övervaka driftsättningshändelser och analysera driftsättningseffekten för övergripande prestanda. Se [Spåra distributioner](track-deployments.md).

I ditt infrastrukturprojekt för Adobe Commerce i molnet ingår programvaran för New Relic APM-tjänsten tillsammans med en licensnyckel. Du behöver inte köpa eller installera någon ytterligare programvara.

## New Relic Infrastructure

Pro-projekten innehåller [New Relic Infrastructure (NRI)](https://docs.newrelic.com/docs/infrastructure/infrastructure-monitoring/get-started/get-started-infrastructure-monitoring/) som automatiskt ansluter till programdata och prestandaanalyser för att tillhandahålla dynamisk serverövervakning. Den här tjänsten är tillgänglig i Pro Production- och Staging-miljöer.

## New Relic Log Management

Alla molninfrastrukturprojekt innehåller [New Relic logghantering](log-management.md). Tjänsten är förkonfigurerad för att samla alla loggdata från din miljö för förproduktion och produktion och visa dem i en centraliserad kontrollpanel för logghantering.
