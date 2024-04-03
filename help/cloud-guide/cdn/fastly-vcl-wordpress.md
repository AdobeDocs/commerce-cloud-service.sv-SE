---
title: Dirigera om begäranden till en CMS-serverdel
description: Lär dig hur du dirigerar om inkommande begäranden från en Adobe Commerce-butik till en separat WordPress-webbplats med hjälp av modulen Snabb.
feature: Cloud, Configuration, Routes
exl-id: 5bd9c56f-4412-4643-89b6-590a8ec65ac0
source-git-commit: 7a181af2149eef7bfaed4dd4d256b8fa19ae1dda
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Dirigera om begäranden till en CMS-serverdel

Omdirigera inkommande begäranden från en Adobe Commerce-butik till en separat WordPress-webbplats med hjälp av modulen Snabbkant _Annan CMS/backend-integrering_ med en Edge Dictionary. Du kan följa en liknande process för att dirigera om begäranden till andra CMS-backends.

Använd Fastt Edge-moduler för att skapa och överföra anpassad VCL-kod från administratören i stället för att manuellt skriva VCL-koden och överföra den med API:t Snabb.

>[!NOTE]
>
>Vi rekommenderar att du lägger till anpassade VCL-konfigurationer i en mellanlagringsmiljö där du kan testa dem innan du uppdaterar snabbtjänstkonfigurationen i produktionsmiljön.

**Förutsättningar**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

**Så här dirigerar du om begäranden från Adobe Commerce till WordPress**:

1. Aktivera moduler med fast kant i miljö för staging och produktion.

   - Logga in på Admin.

   - Navigera till **Lager** > Inställningar > **Konfiguration** > **Avancerat** > **System** > **Helsidescache** > **Snabb konfiguration** > **Avancerad konfiguration**.

   - Ange värdet för **Moduler med fast kant** till **Ja**.

   - Spara konfigurationen.

1. Identifiera de URL-sökvägar som ska dirigeras om till WordPress-serverdelen.

1. Utför följande uppgifter för att konfigurera tjänsten Snabbt och skapa den anpassade VCL-koden för omdirigering av begäranden till WordPress-backend.

   - Skapa en Edge Dictionary som anger de banor som ska dirigeras om från Adobe Commerce Store till backend-objektet.

   - Lägg till backend-objektet för WordPress i snabbtjänstkonfigurationen och bifoga villkoret för begäran om URL-omskrivning.

   - Konfigurera _Annan CMS/backend-integrering_ Edge Module för att hantera URL-omskrivningar från Adobe Commerce till WordPress-backend.

     Detaljerade anvisningar finns i [Moduler med fast kant - annan integrering med CMS/backend](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-OTHER-CMS-INTEGRATION.md) i _Snabb CDN-modul för Magento 2_ dokumentation.

1. När du har uppdaterat konfigurationen för tjänsten Snabb testar du Adobe Commerce Store för att kontrollera att de angivna URL-förfrågningarna för WordPress dirigeras om korrekt.
