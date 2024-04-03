---
title: Distributionsprocess
description: Lär dig hur driftsättning fungerar för Adobe Commerce i molninfrastrukturprojekt.
feature: Cloud, Build, Deploy, SCD
exl-id: 378fa290-5a71-4ac2-816a-a7c837e45b2f
source-git-commit: 3d9e3294872fedcc43744f54a71c71d8951ed853
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Distributionsprocess

Distributionsprocessen börjar när du sammanfogar, kör eller synkroniserar miljön, eller när du utlöser en [manuell ominstallation](../dev-tools/cloud-cli-overview.md#redeploy-the-environment). Distributionsprocessen tar tid, men det finns sätt att optimera distributionen som beror på om du utvecklar och testar eller arbetar med en aktiv webbplats. Det viktigaste är att du kan styra [statisk innehållsdistribution](static-content.md).

Distributionsprocessen består av tre olika faser: bygg, driftsätt och postdriftsättning. Varje fas utför specifika åtgärder med begränsade resurser:

## ![Byggfas](../../assets/status-build.png) Byggfas

The _bygg_ fassammanställer behållare för de tjänster som definieras i konfigurationsfilerna, installerar beroenden baserat på `composer.lock` och kör de build-kopplingar som definieras i `.magento.app.yaml` -fil. Utan möjlighet att ansluta till tjänster eller komma åt databasen beror byggfasen på de resurser som är begränsade till miljön.

## ![Distributionsfas](../../assets/status-deploy.png) Distributionsfas

The _driftsätta_ fas gör att en tillfällig spärr placeras på inkommande begäranden och webbplatsen övergår till [underhållsläge](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html). Distributionsfasen använder de nya behållarna och när filsystemet har monterats aktiveras nätverksanslutningarna för de tjänster som definieras i `relationships` i `.magento.app.yaml` och kör de distributionsnätverk som definierats i `.magento.app.yaml` -fil. Allt är _skrivskyddad_, förutom för kataloger som definieras i `.magento.app.yaml` -fil. Som standard är [`mounts` property](../application/properties.md#mounts) innehåller följande kataloger:

- `app/etc`—innehåller `env.php` och `config.php` konfigurationsfiler
- `pub/media`—innehåller alla mediedata, t.ex. produkter eller kategorier
- `pub/static`—innehåller genererade statiska filer
- `var`—innehåller tillfälliga filer som skapades under körning

Alla andra kataloger har skrivskyddad behörighet. Den nya platsen blir aktiv i slutet av distributionsfasen när den övergår från underhållsläge och frigör det tillfälliga undantaget för inkommande begäranden.

Under driftsättningsfasen: kopior av `app/etc/config.php` och `app/etc/env.php` konfigurationsfiler för distribution sparas med BAK-tillägget. Se [Lagringsinställningar](../store/store-settings.md#restore-configuration-files) om du vill veta mer om hur du återställer dessa filer.

## ![Fas efter driftsättning](../../assets/status-post-deploy.png) Fas efter driftsättning

The _efter driftsättning_ fas kör de kopplingar efter distribution som definieras i `.magento.app.yaml` -fil. Om du utför en åtgärd i den här fasen kan det påverka webbplatsens prestanda, men du kan använda [WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages) systemvariabel för att fylla i cachen.

## ![Verifiera läge](../../assets/status-verify.png) Verifiera konfigurationer

Du kan testa den optimala konfigurationen för projektets status genom att köra [Smarta guider](smart-wizards.md).

>[!NOTE]
>
>Med `ece-tools` 2002.1.0 och senare versioner kan du använda den scenariobaserade distributionsfunktionen för att anpassa processerna för att skapa, distribuera och efterdistribuera för ditt Adobe Commerce i molninfrastrukturprojekt. Se [Scenariobaserad driftsättning](scenario-based.md).
