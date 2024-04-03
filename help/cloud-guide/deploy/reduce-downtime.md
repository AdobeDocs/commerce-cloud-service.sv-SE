---
title: Driftsättning utan driftstopp
description: Lär dig hur du minskar den totala driftstoppen när du distribuerar Adobe Commerce i molninfrastrukturprojekt.
feature: Cloud, Deploy, SCD, Themes
exl-id: ff89d2e1-dfc8-4f6d-bd98-947559af13f0
source-git-commit: 225fba1acfd8b3ce4d7ce989c7851e7b0b218680
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Driftsättning utan driftstopp

Adobe Commerce i molninfrastrukturen kör programmet i [_underhåll_ läge](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html#production-mode) under driftsättningsfasen, som tar din webbplats offline tills distributionen är klar. Hur lång tid produktionsplatsen är i underhållsläge beror på platsens storlek, antalet ändringar som gjorts under distributionen och konfigurationen för statisk innehållsdistribution. Det går att konfigurera projektet så att det distribueras med en **noll** driftstopp.

Under distributionsprocessen bevarar alla anslutningsköer i upp till 5 minuter alla aktiva sessioner och väntande åtgärder, som att lägga till i kundvagnen eller i kassan. Efter distributionen släpps kön och anslutningarna fortsätter utan avbrott. Använd detta _anslutningsspärr_ till din fördel och minska driftsättningen till _noll_ driftstopp måste du konfigurera projektet så att det använder den mest effektiva distributionsstrategin.

Följ de här stegen för att minska den tid det tar för butiken att distribuera en uppdatering till produktionen:

1. [Uppgradera till `ece-tools` package](../dev-tools/install-package.md) eller [uppdatera `ece-tools` version](../dev-tools/update-package.md)
Ditt Adobe Commerce i molninfrastrukturprojekt måste ha det senaste `ece-tools` så att du har de verktyg du behöver för att konfigurera en optimal distribution. Om du har de senaste `ece-tools`fortsätter du till nästa steg.

   >[!NOTE]
   >
   >Även om det är en god vana att använda den senaste `ece-tools` paket fungerar distributionsmetoden utan driftstopp med `ece-tools` [version 2002.0.13](../release-notes/cloud-release-archive.md#v2002013) och senare.

1. [Konfigurera statisk innehållsdistribution](static-content.md)
Om statisk innehållsdistribution misslyckas i distributionsfasen fastnar platsen i underhållsläge. När ett fel inträffar under byggfasen undviker processen driftavbrott eftersom den aldrig påbörjar distributionsfasen. [Generera statiskt innehåll under byggfasen med minifierad HTML](static-content.md#setting-the-scd-on-build), även känt som det idealiska läget, är den optimala konfigurationen för driftsättningar utan driftavbrott och _förhindrar_ driftstopp om ett fel inträffar.

1. [Konfigurera kroken efter driftsättning](../application/hooks-property.md)
Du måste konfigurera kroken efter distributionen för att rensa och värma cachen. Som standard rensas cacheminnet under distributionsfasen när platsen är nere. Att flytta cacheminnet till fasen efter distributionen innebär att cacheminnet förblir levande tills distributionsfasen är klar och sedan kan du rensa cacheminnet på ett säkert sätt.

   Anpassa listan med sidor som används för att läsa in cachen i förväg med [WARM_UP_PAGES-miljövariabel](../environment/variables-post-deploy.md#warmuppages).

1. [Minska temafiler](../environment/variables-deploy.md#scdmatrix)
Du kan minska antalet onödiga temafiler genom att konfigurera miljövariabeln SCD\_MATRIX.

1. [Snabba upp distributionen av statiskt innehåll](../environment/variables-deploy.md#scdthreads)
Du kan snabba upp distributionsprocessen genom att uppdatera miljövariabeln SCD\_THREADS för att öka antalet trådar för distribution av statiskt innehåll.

>[!NOTE]
>
>Du kan validera projektkonfigurationen för optimal distribution genom att [köra guiden för det idealiska läget](smart-wizards.md#verifying-an-ideal-configuration).
