---
source-git-commit: b08443d937dfc18120daa0d6a1277b9c7bca67aa
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---
# Molnfragment

## Elasticsearch-varning {#elasticsearch-support}

>[!WARNING]
>
>Elasticsearch 7.11 och senare stöds inte för Adobe Commerce i molninfrastruktur. Adobe Commerce version 2.3.7-p3, 2.4.3-p2 och 2.4.4 och senare stöder OpenSearch-tjänsten. De lokala anläggningarna fortsätter att stödja Elasticsearch.

## Förbättrad integrering {#enhanced-integration-envs}

>[!NOTE]
>
>Projekt som etablerades före den 5 juni 2020 hade flera mindre integreringsmiljöer. Om du behöver en större integreringsmiljö för testning och utveckling kan du begära en uppgradering till förbättrade integreringsmiljöer. Se [Begäran om integreringsmiljö](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/announcements/commerce-announcements/integration-environment-enhancement-request-pro-and-starter.html) artikel i _Adobe Commerce Help Center_ för mer information.

## Sammanfogningsalternativ {#merge-options}

Som standard skriver distributionsprocessen över alla inställningar i `env.php` kan du välja att sammanfoga ett eller flera värden för en tjänstkonfiguration utan att skriva över alla värden.

Ange `_merge` till något av följande:

- `true`—**Sammanfoga** de konfigurerade tjänstvärdena med miljövariabelvärdena.
- `false`—**Skriv över** de konfigurerade tjänstvärdena med miljövariabelvärdena.

## Privat databas {#private-repository}

>[!NOTE]
>
>Adobe rekommenderar starkt att du använder ett privat arkiv för Adobe Commerce i molninfrastrukturprojekt för att skydda all tillverkarspecifik information eller allt utvecklingsarbete, som tillägg och känsliga konfigurationer.

## Självbetjäningsvarning för proffs {#pro-self-service-warning}

>[!WARNING]
>
>Några **Pro-projekt** kräver en supportbiljett för att uppdatera ruttkonfigurationen i `routes.yaml` och cron-konfigurationen i `.magento.app.yaml` -fil. Adobe rekommenderar att du uppdaterar och testar YAML-konfigurationsfiler i en integreringsmiljö och sedan distribuerar ändringar i mellanlagringsmiljön. Om dina ändringar inte tillämpas på mellanlagringsplatser efter att du har omdistribuerat och det inte finns några relaterade felmeddelanden i loggen, så använder du **MÅSTE** [Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) som beskriver de konfigurationsändringar som gjorts. Inkludera eventuella uppdaterade YAML-konfigurationsfiler i biljetten.

## Support för Pro services {#pro-update-service}

>[!TIP]
>För Pro-projekt måste du [skicka en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) installera eller uppdatera [tjänster](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/services-yaml.html) in `Staging` och `Production` endast i miljöer.
>
>Ange vilka tjänständringar som behövs, inkludera dina uppdaterade `.magento.app.yaml` och `services.yaml` och ange PHP-versionen i biljetten. Information om självbetjäningsändringar av PHP-version, tillägg eller miljöinställningar finns i [PHP-inställningar](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/app/php-settings.html) in _Programkonfiguration_.
>
>För ändringar i en _live_ Produktionsmiljö (**Endast Pro**) måste du lämna minst 48 timmars meddelande så att molninfrastrukturteamet får tillräckligt med tid för att registrera resurser och genomföra en säker uppgradering.

## Pro-säkerhetskopiering {#pro-backups}

>[!TIP]
>
>I Pro Staging- och Production-miljöer måste du [skicka en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) för att hämta en specifik säkerhetskopia med information om datum, tid och tidszon i biljetten.
>
>Adobe gör **not** återställa miljöer från en automatisk säkerhetskopiering. Se [Återställ en DB-ögonblicksbild från mellanlagring eller produktion](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/restore-a-db-snapshot-from-staging-or-production.html) om du vill ha hjälp med att välja en metod för att återställa en ögonblicksbild av förproduktion eller produktion.

## Återdistribuera varning {#redeploy-warning}

>[!WARNING]
>
>Distributionsprocessen börjar när du sammanfogar, push eller synkroniserar miljön, eller när du utlöser en manuell omdistribution, under vilken [!DNL Commerce] programmet är i underhållsläge. För en produktionsmiljö rekommenderar Adobe att man slutför detta under tider med låg belastning för att undvika avbrott i tjänsten.

## Flödesplatshållare {#route-placeholder}

>[!NOTE]
>
>I följande exempel på flödeskonfiguration används flödesmallar med platshållare. The `{default}` platshållaren representerar standarddomänen som konfigurerats för platsen. Om projektet har flera domäner använder du `{all}` platshållare för att konfigurera routning för standarddomänen och alla alias. Se [Konfigurera flöden](/help/cloud-guide/routes/routes-yaml.md).

## SCD-timing {#scd-timing-warning}

>[!WARNING]
>
>Om du har problem med statiska innehållsfiler i programmet efter distributionen, till exempel om det saknas anpassade temafiler, ökar du den förväntade körningstiden till 900 sekunder eller mer.

## Scenariobaserad driftsättning {#scenarios}

>[!NOTE]
>
>Med [!DNL ECE-Tools] 2002.1.0 och senare versioner kan du använda den scenariobaserade distributionsfunktionen för att anpassa processerna för att skapa, distribuera och efterdistribuera för ditt Adobe Commerce i molninfrastrukturprojekt. Se [Scenariobaserad driftsättning](/help/cloud-guide/deploy/scenario-based.md).

## Tjänstinstruktion {#service-instruction}

Använd följande instruktioner för konfiguration av tjänster i Pro Integration-miljöer och Starter-miljöer, inklusive `master` gren.

>[!NOTE]
>
>[Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om du vill ändra tjänstkonfigurationen i Pro Production- och Staging-miljöer.

## Tjänständring {#service-change-tip}

>[!TIP]
>
>Efter den första konfigurationen kan du ändra programversionen för en installerad tjänst genom att uppdatera `services.yaml` och `.magento.app.yaml` konfigurationsfiler. Se [Ändra tjänstversion](/help/cloud-guide/services/services-yaml.md#change-service-version) för vägledning om uppgradering eller nedgradering av en tjänst.

## Tips för distribution av Studio {#stuck-deployment-tip}

>[!TIP]
>
>Om du vill ha hjälp med fasta distributioner använder du [Adobe Commerce felsökare vid driftsättning](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html) i _Commerce Help Center_.

## Uppdatera till ECE-verktyg {#ece-tools-package}

>[!NOTE]
>
>Om du använder en version av Adobe Commerce i molninfrastrukturen som inte innehåller `ece-tools` måste du utföra en [engångsuppgradering](/help/cloud-guide/dev-tools/install-package.md) till ditt molnprojekt för att ta bort föråldrade paket. Om du använder `ece-tools` och du behöver uppdatera det, se [Uppdatera ECE-verktygspaketet](/help/cloud-guide/dev-tools/update-package.md).

## Uppgradering {#upgrade-tip}

>[!TIP]
>
>Innan du påbörjar en uppgradering eller en korrigeringsprocess skapar du en aktiv gren i integreringsmiljön och checkar ut den nya grenen till din lokala arbetsstation. Genom att dedikera en gren till uppgraderingen eller korrigeringsprocessen undviker du störningar i pågående arbete.

<!-- Fastly-related snippets begin -->

## Administratörsinloggning {#admin-login-step}

1. [Logga in](/help/get-started/onboarding.md#access-your-admin-panel) till administratören.

## Automatisera anpassad VCL-fragmentdistribution {#automate-vcl-snippet-deployment}

>[!NOTE]
>
>I stället för att överföra anpassade VCL-fragment manuellt kan du lägga till fragment i `$MAGENTO_CLOUD_APP_DIR/var/vcl_snippets_custom` i din miljö. Kodavsnitt i den här katalogen överförs automatiskt när du klickar på _ladda upp VCL snabbt_ i handelsadministratören. Se [Automatiserad installation av anpassade VCL-fragment](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md#automated-custom-vcl-snippets-deployment) i modulen Fastly CDN för Magento 2-dokumentation.

<!-- Fastly-related snippets end -->
