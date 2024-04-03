---
title: New Relic-övervakning
description: Lär dig hur du får tillgång till din New Relic-kontrollpanel och analyserar data från din Adobe Commerce i molninfrastrukturprojekt.
feature: Cloud, Observability
topic: Performance
exl-id: 8d1e2ad6-14d0-4754-9703-960d93e135a9
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# New Relic-övervakning

New Relic kopplar samman och övervakar din infrastruktur och [!DNL Commerce] program som använder PHP-agenter. När en molnmiljö har anslutit till New Relic kan du logga in på ditt New Relic-konto för att granska de data som samlas in av agenten.

På _APM och tjänster_ väljer du **Sammanfattning** om du vill visa transaktionsinformation om programmet. I den här vyn kan du identifiera potentiella fel och kontrollera den övergripande statusen för dina program och tjänster.

![New Relic - översikt](../../assets/new-relic/dashboard.png)

I den här vyn kan du spåra transaktioner som stöter på långsamma svar eller flaskhalsar, applikationens genomströmning, webbfel med mera.

Granska spårade data:

- **Den mest tidskrävande**- Bestäm tidsåtgången genom att spåra begäranden parallellt. Du kan till exempel ha den högsta transaktionstiden i produkt- och kategorivyer. Om en kundkontosida plötsligt rankas som hög i tidskonsumtion kan programmet påverkas av att användaren ringer eller drar frågor.

- **Högsta genomströmning**—Identifiera sidor som slår störst baserat på storleken och frekvensen av byte som skickas.

Alla insamlade data anger hur lång tid som har ägnats åt åtgärder som överför data, frågor eller _Redis_ data. Om det uppstår problem i en fråga tillhandahåller New Relic information för att spåra och besvara dessa problem.

>[!TIP]
>
>Mer information om hur du använder dessa data för att felsöka prestandaproblem i programmet finns i [Felsöka prestanda med New Relic](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-performance-using-new-relic-on-magento-commerce.html) i _Adobe Commerce Help Center_.

## Övervaka prestanda med hanterade aviseringar

Adobe tillhandahåller _Hanterade aviseringar för Adobe Commerce_ larmpolicy för att spåra resultatmått. Principen innehåller en samling varningar som anger tröskelvärden och utlöser varningar och kritiska meddelanden när infrastruktur- eller programproblem påverkar webbplatsens prestanda. Policyn håller reda på följande mått för produktionsmiljöer:

| Mått | Datainsamling | Tillgänglighet |
|:-------------------|:----------------|:----------------|
| [!DNL Apdex] score | APM | Pro och Starter |
| CPU-användning | NRI | Pro |
| Diskutrymme | NRI | Pro |
| Felfrekvens | APM | Pro och Starter |
| Minnesanvändning | NRI | Pro |
| MariaDB-frågeinläsning | NRI | Pro |
| Redis-minne | NRI | Pro |

När webbplatsinfrastruktur eller programförhållanden utlöser ett tröskelvärde för avisering skickar New Relic varningsmeddelanden så att du kan åtgärda problemet proaktivt. Se [Hanterade aviseringar för Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce.html) i _Adobe Commerce Help Center_ om du vill ha information om varningströsklar och felsökningsåtgärder för att lösa problem som utlöste varningen.

>[!TIP]
>
>För Pro Staging- och integreringsmiljöer samt Starter-miljöer använder du [Hälsoaviseringar](../integrations/health-notifications.md) för att övervaka diskutrymmet.

>[!PREREQUISITES]
>
>- **New Relic-autentiseringsuppgifter**—Autentiseringsuppgifter för att logga in på New Relic-kontot för ditt Cloud-projekt
>- **Integrering med Active New Relic**—Verifiera att din molnmiljö är ansluten till New Relic
>- **Meddelande om arbetsflöde**—Konfigurera minst en [arbetsflöde](#set-up-a-workflow-for-notifications) för att ta emot varningsmeddelanden

**Så här granskar du principen för hanterade aviseringar för Adobe Commerce**:

1. Logga in på [New Relic](https://login.newrelic.com/login).

1. Leta reda på _Hanterade aviseringar för Adobe Commerce_ policy:

   - Klicka på **[!UICONTROL Alerts & AI]**.

   - Under _Identifiera_, klicka **[!UICONTROL Alert Conditions & Policies]**.

   - Verifiera att ditt konto är markerat högst upp i _Villkor och principer för avisering_ vy.

   - I _Policy_ lista, välj **Hanterade aviseringar för Adobe Commerce** policy.

     ![Genererade aviseringsprinciper](../../assets/new-relic/managed-alerts-policy.png)

     >[!NOTE]
     >
     >Om _Hanterade aviseringar för Adobe Commerce_ profilen är inte tillgänglig, se [Hanterade aviseringar för Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce.html) i _Adobe Commerce Help Center_.

1. Klicka på **[!UICONTROL Alert conditions]** om du vill granska de varningsvillkor som definierats i profilen.

## Skapa aviseringsprinciper

Ändra inte några aviseringar som ingår i policyn för hanterade aviseringar för Adobe Commerce. Adobe uppdaterar och förbättrar aviseringsvillkoren i den här principen över tid, vilket skriver över eventuella anpassningar som du lägger till i principen.

I stället för att ändra en befintlig avisering kan du skapa en aviseringsprincip. Kopiera sedan varningsvillkoren till den nya profilen. Se [Uppdatera principer eller villkor](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/alert-policies/update-or-disable-policies-conditions/) i _New Relic_ dokumentation.

>[!TIP]
>
>Se [Introduktion till aviseringar](https://docs.newrelic.com/docs/alerts-applied-intelligence/new-relic-alerts/learn-alerts/alerts-concepts-workflow/) i _New Relic_ dokumentation för mer detaljerad information om aviseringar, aviseringsprinciper och arbetsflöden.

## Konfigurera ett arbetsflöde för meddelanden

Nu kan du konfigurera en _arbetsflöde_, tidigare kallat en meddelandekanal, för att få meddelanden om webbplatsens prestanda baserat på filtrerade data, till exempel en aviseringsprincip. Meddelanden om prestandaproblem skickas till alla arbetsflöden som är kopplade till en aviseringsprincip när villkoren i programmet eller infrastrukturen utlöser en avisering. Du får också meddelanden när en utgåva har bekräftats och stängts.

New Relic innehåller mallar för konfigurering av olika typer av arbetsflödesmeddelanden, bland annat e-post, Slack, PagerDuty, webhooks med flera.

**Konfigurera ett arbetsflöde**:

1. Logga in på [New Relic](https://login.newrelic.com/login).

1. Skapa ett arbetsflöde.

   - Klicka på **[!UICONTROL Alerts & AI]**.

   - Navigering till vänster under _Förbättra och meddela_, klicka **[!UICONTROL Workflows]**.

   - Klicka **[!UICONTROL Add a workflow]** till höger.

     ![New Relic lägger till ett arbetsflöde](../../assets/new-relic/add-a-workflow.png)

   - På _Konfigurera ditt arbetsflöde_ anger du ett namn för arbetsflödet.

   - I _Filtrera data_ avsnitt, markera **[!UICONTROL Managed Alerts for Adobe Commerce]** från **[!UICONTROL Policy]** listruta.

   - I _Meddela_ markerar du en kanal och följer instruktionerna.

   - Klicka **[!UICONTROL Test workflow]** för att verifiera din konfiguration.

1. Klicka på **[!UICONTROL Activate workflow]**.

Läs New Relic dokumentation om [Arbetsflöden](https://docs.newrelic.com/docs/alerts-applied-intelligence/applied-intelligence/incident-workflows/incident-workflows/).

>[!WARNING]
>
>Aviseringarna i principen Managed Alerts för Adobe Commerce har standardarbetsflöden konfigurerade för att meddela Adobe-team som stöder Adobe Commerce om molninfrastrukturskunder. Ändra inte konfigurationen för dessa standardkanaler och ta inte bort eventuella varningsprofiler som tilldelats dem.
