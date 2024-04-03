---
title: Arbetsflöde för Pro-projekt
description: Lär dig använda arbetsflödena för Pro-utveckling och -distribution.
feature: Cloud, Iaas, Paas
exl-id: 103e90d5-2ef2-4fef-845c-439344666b00
source-git-commit: 08f43a3b0a50cdb2a5e8a45bd2e2448bc6dbca2b
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# Arbetsflöde för Pro-projekt

Pro-projektet innehåller en enda Git-databas med en global `master` grenen och tre huvudmiljöer:

1. **Produktion** miljö för att starta och underhålla den publicerade webbplatsen
1. **Mellanlagring** miljö för testning med alla tjänster
1. **Integrering** miljö för utveckling och testning

![Miljölista för Pro](../../assets/pro-environments.png)

Dessa miljöer `read-only`, som godkänner distribuerade kodändringar från grenar som har flyttats från den lokala arbetsytan. Se [Pro-arkitektur](pro-architecture.md) för en fullständig översikt över Pro-miljöerna. Se [[!DNL Cloud Console]](../project/overview.md#cloud-console) om du vill ha en översikt över Pro-miljölistan i projektvyn.

I följande bild visas arbetsflödet för Pro-utveckling och -distribution, som använder en enkel Git-förgrening. Du [utveckla](#development-workflow) kod som använder en aktiv gren baserad på `integration` miljö, _push_ och _dra_ koden ändras till och från din aktiva gren på fjärrbasis. Distribuera verifierad kod med _sammanfoga_ fjärrgrenen till basgrenen, som aktiverar en automatiserad [bygga och driftsätta](#deployment-workflow) för den miljön.

![Översikt över arbetsflödet för utveckling av Pro-arkitektur](../../assets/pro-dev-workflow.png)

## Arbetsflöde för utveckling

Integreringsmiljön ger en enda bas `integration` en gren som innehåller din Adobe Commerce på molninfrastrukturkoden. Du kan skapa ytterligare en aktiv miljögren. Detta tillåter upp till två aktiva grenar som distribueras till plattformsbehållare (PaaS). Det finns ingen gräns för antalet inaktiva miljöer.

{{enhanced-integration-envs}}

Projektmiljöerna har stöd för en flexibel, kontinuerlig integrationsprocess. Börja med att klona `integration` till din lokala projektmapp. Skapa en gren, eller flera grenar, utveckla nya funktioner, konfigurera ändringar, lägga till tillägg och distribuera uppdateringar:

- **Hämta** ändringar från `integration`

- **Gren** från `integration`

- **Utveckla** kod på en lokal arbetsstation, inklusive [!DNL Composer] uppdateringar

- **Push** kodsändringar i fjärrkatalogen och validera

- **Sammanfoga** till `integration` och testa

Med en utvecklad kodgren och motsvarande konfigurationsfiler är dina kodändringar klara att sammanfogas med `integration` för mer omfattande testning. The `integration` passar också bäst för:

- **Integrera tredjepartstjänster**- Alla tjänster är inte tillgängliga i PaaS-miljön.

- **Genererar konfigurationshanteringsfiler**—Vissa konfigurationsinställningar är _Skrivskyddad_ i en distribuerad miljö.

- **Konfigurera din butik**- Du bör konfigurera alla butiksinställningar fullständigt i integreringsmiljön. Du hittar **Administratörs-URL för butik** på _integration_ miljövyn i _[!DNL Cloud Console]_.

## Arbetsflöde för distribution

Varje gång du skickar kod från din lokala arbetsstation till fjärrmiljön eller lägger samman kod till en miljögren genererar skripten ny kod och tillhandahåller de konfigurerade tjänsterna till fjärrmiljön.

Skapa skriptåtgärder:

- Webbplatsen i målmiljön fortsätter att köras under en bygge

- Kontrollera och kör Adobe Commerce på korrigeringar och snabbkorrigeringar för molninfrastruktur

- Kompilera kod med en bygg- och distributionslogg

- Kontrollera om det finns Configuration Management, statisk innehållsdistribution sker under den här fasen

- Skapa eller använd en instruktionsmarginal med oförändrad kod för att snabba upp processen

- Tillhandahåller alla backend-tjänster och program

Distribuera skriptåtgärder:

- Placera platsen i målmiljön i en _Underhåll_ läge

- Distribuera statiskt innehåll om det inte slutförs under bygget

- Installera eller uppdatera Adobe Commerce i molninfrastrukturen

- Konfigurera routning för trafik

Efter bygg- och distributionsprocessen kommer din butik tillbaka online med dina senaste kodändringar och konfigurationer. Se [Distributionsprocess](../deploy/process.md).

### Sammanfoga till integration

Kombinera alla verifierade kodändringar genom att sammanfoga din aktiva utvecklingsgren i basen `integration` gren. Du kan testa alla dina ändringar på `integration` innan du befordrar ändringar i mellanlagringsmiljön.

### Sammanfoga till mellanlagring

Mellanlagring är en förproduktionsmiljö som tillhandahåller alla tjänster och inställningar så nära produktionsmiljön som möjligt. Flytta alltid dina kodändringar från `integration` miljö till `staging` så att du kan utföra grundliga tester med alla tjänster. Första gången du använder testmiljön måste du konfigurera tjänster, som [Snabb CDN](../cdn/fastly.md) och [New Relic](../monitor/new-relic-service.md). Konfigurera betalningsgatewayar, leveranser, meddelanden och andra viktiga tjänster med sandlåda eller testningsreferenser.

Det är bäst att noggrant testa alla tjänster, verifiera prestandatestningsverktygen och utföra UAT-tester som administratör och kund tills du känner att butiken är redo för produktionsmiljön. Se [Distribuera din butik](../deploy/staging-production.md).

### Koppla till produktion

Efter grundlig testning i staging-miljön kan du slå samman till produktionsmiljön och grundligt testa med Live-inloggningsuppgifter. Så fort ni lanserar er produktionsplats måste kunderna kunna slutföra sina inköp och administratörerna måste kunna hantera livebutiken. Se följande avsnitt för en detaljerad och tydlig genomgång av hur du distribuerar butiken och publicerar den:

- [Distribuera din butik](../deploy/staging-production.md)
- [Starta webbplatsen](../launch/overview.md)

### Sammanfoga till global mallsida

Skicka alltid en kopia av produktionskoden till Global `master` om det finns ett akut behov av att felsöka produktionsmiljön utan att avbryta tjänsterna.

Gör **not** skapa en gren från Global `master`. Använd `integration` gren för att skapa nya, aktiva grenar för utveckling och korrigeringar.
