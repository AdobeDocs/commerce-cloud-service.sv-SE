---
title: Bästa praxis för driftsättning
description: Upptäck de bästa sätten att driftsätta Adobe Commerce i molninfrastruktur.
feature: Cloud, Deploy, Best Practices
exl-id: bac3ca83-0eee-4fda-9a5c-a84ab25a837a
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 0%

---

# Bästa praxis för driftsättning

Bygg och distribuera skript som aktiveras när du sammanfogar kod till en fjärrmiljö. Dessa skript använder miljön [konfigurationsfiler](../environment/overview.md) och programkod för att tillhandahålla molninfrastruktur med lämpliga data och tjänster. Dessa skript används också för att installera eller uppdatera Adobe Commerce-programmet, tredjepartstjänster och anpassade tillägg i molnmiljön.

Processen för att skapa och distribuera skiljer sig något åt för varje plan:

- **Startplaner**- För integreringsmiljön bygger och driftsätter alla aktiva avdelningar en komplett miljö för åtkomst och testning. Testa koden fullständigt efter sammanslagning med `staging` gren. Om du vill starta webbplatsen trycker du på `staging` till `master` för att driftsätta i produktionsmiljön. Du har fullständig åtkomst till alla grenar via [!DNL Cloud Console] och kommandona i CLI.

- **Pro-planer**- För integreringsmiljön bygger och driftsätter alla aktiva avdelningar en komplett miljö för åtkomst och testning. Sammanfoga koden med `integration` förgrening innan du sammanfogar till miljö för förproduktion och produktion. Du kan sammanfoga till miljö för förproduktion och produktion med hjälp av [!DNL Cloud Console] eller med SSH och `magento-cloud` CLI-kommandon.

## Spåra processen

Du kan spåra bygg- och distributionsåtgärder i realtid med terminalen eller [!DNL Cloud Console] Statusmeddelanden—`in-progress`, `pending`, `success`, eller `failed`—visa under distributionsprocessen. Du kan visa information i loggfilerna. Se [Visa loggar](../test/log-locations.md).

Om du använder externa GitHub-databaser visas inte åtgärdsloggen i GitHub-sessionen. Du kan dock fortfarande följa aktiviteten i gränssnittet för den externa databasen och [!DNL Cloud Console]. Se [Integreringar](../integrations/overview.md).

>[!NOTE]
>
>I integreringsmiljöer kan du inte visa distributionsloggarna från [!DNL Cloud Console]. Den här funktionen är endast tillgänglig för produktions- och mellanlagringsmiljöer. Du kan dock visa loggar för varje distributionsfas i vilken miljö som helst med hjälp av [bygga och driftsätta](../test/log-locations.md#build-and-deploy-logs) loggar. Felsökningsinformation finns i [Distributionsfelreferens](../dev-tools/error-reference.md).

Du kan aktivera [Spåra driftsättningar med New Relic](../monitor/track-deployments.md) för att övervaka distributionshändelser och analysera prestanda mellan distributioner.

## Bästa tillvägagångssätt för byggen och driftsättningen

Granska de bästa metoderna och övervägandena för din distributionsprocess:

- **Kontrollera att du använder den senaste versionen av `ece-tools` package**

  Se [Versionsinformation för ECE-verktyg](../release-notes/ece-tools-package.md).

- **Följ byggprocessen och distributionsprocessen**

  Se till att du har rätt kod i varje miljö för att undvika att skriva över konfigurationer när du sammanfogar kod mellan miljöer. Om du till exempel vill använda konfigurationsändringar i alla miljöer ändrar och testar du ändringarna i den lokala miljön innan du distribuerar till fjärrintegreringsmiljön. Distribuera och testa sedan ändringarna i mellanlagringsmiljön innan du distribuerar till Production. När du sammanfogar från en miljö till en annan skrivs all kod i miljön över, förutom miljöspecifik konfiguration och inställningar.

- **Använd samma variabler i olika miljöer**

  Värdena för dessa variabler kan variera mellan olika miljöer, men du behöver vanligtvis samma variabler i varje miljö. Se [Konfigurationshantering för lagringsinställningar](../store/store-settings.md).

- **Behåll känsliga konfigurationsvärden och data i miljöspecifika variabler**

  Dessa värden inkluderar variabler som anges med Cloud CLI, [!DNL Cloud Console], eller har lagts till i `env.php` -fil. Se [Variabelnivåer](../environment/variable-levels.md).

- **Kontrollera att all kod är tillgänglig i miljögrenen**

  Att referera till kod från andra grenar, till exempel en privat gren, kan orsaka problem under bygg- och distributionsprocessen. Om du till exempel refererar till ett tema från en privat gren är temat inte tillgängligt och kan inte byggas med programkoden.

- **Lägg till tillägg, integreringar och kod i itererade grenar**

  Gör och testa ändringar lokalt, tryck på `integration`och sedan `staging` och `production`. Testa och åtgärda problem i varje miljö innan du sammanfogar uppdateringarna med nästa miljö. Vissa tillägg och integreringar måste aktiveras och konfigureras i en viss ordning på grund av beroenden. Om du lägger till och testar i grupper kan det göra bygg- och driftsättningsprocessen mycket enklare och hjälpa till att avgöra var problemen uppstår.

- **Verifiera tjänsteversioner och relationer samt möjligheten att ansluta**

  Kontrollera vilka tjänster som är tillgängliga för ditt program och se till att du använder den senaste kompatibla versionen. Se [Servicerelationer](../services/services-yaml.md#service-relationships) och [Systemkrav](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) i _Installationsguide_ för rekommenderade versioner.

- **Testa lokalt och i integreringsmiljön innan du distribuerar till Förproduktion**

  Identifiera och åtgärda problem i den lokala miljön och integreringsmiljön för att förhindra längre driftstopp när du distribuerar till förproduktionsmiljöer.

  >[!TIP]
  >
  >Det finns [smart guide](../deploy/smart-wizards.md) kommandon som du kan använda för att verifiera att molnprojektskonfigurationen följer bästa praxis för bygg- och distributionskonfigurationer, inklusive en strategi för statisk innehållsdistribution (SCD).

- **När du är klar med testningen i lokala miljöer och integreringsmiljöer ska du driftsätta och testa i mellanlagringsmiljön**

  Se [Testning av mellanlagring och produktion](../test/staging-and-production.md).

- **Kontrollera konfiguration av produktionsmiljö**

  Utför följande uppgifter innan du distribuerar till Production:

   - Se till att du kan ansluta till alla tre noderna i produktionsmiljön med [SSH](../development/secure-connections.md).

   - Verifiera att indexerare är inställda på _Uppdatera enligt schema_. Se [Indexeringsläge](https://developer.adobe.com/commerce/php/development/components/indexing/) i _Handbok för tilläggsutvecklare_.

   - Förbered miljön genom att uppdatera alla miljöspecifika variabler i produktionskoden, verifiera tjänstens tillgänglighet och kompatibilitet samt göra andra nödvändiga konfigurationsändringar.

- **Övervaka distributionsprocessen**

  Granska distributionsstatusmeddelandena och åtgärda problemen efter behov. Granska molnet [loggar](../test/log-locations.md#) för detaljerade loggmeddelanden.

## Fem faser av integration, skapande och driftsättning

Följande faser utförs i den lokala utvecklingsmiljön och i integreringsmiljön. För Pro-planer distribueras koden inte till förproduktionsmiljöer eller produktionsmiljöer i dessa initiala faser.

### Fas 1: Validering av kod och konfiguration

När du först skapar ett projekt [mallen för molninfrastruktur](https://github.com/magento/magento-cloud) utgör grunden för kodfilerna. Kodrepon klonas till ditt projekt som `master` gren.

- **För Starter**—`master` är din produktionsmiljö.
- **För Pro**—`master` börjar som ursprunglig gren för integreringsmiljön.

Skapa en gren från `master` för egen kod, tillägg och moduler samt integreringar från tredje part. Det finns en fjärrintegrerad miljö för att testa koden i molnet.

När du skickar koden från den lokala arbetsytan till fjärrdatabasen slutförs en serie kontroller och kodvalideringar innan skripten byggs och distribueras. Den inbyggda Git-servern validerar det du gör och gör ändringar. Om du till exempel lägger till en OpenSearch-tjänst verifierar den inbyggda Git-servern att topologin för ditt kluster ändras i enlighet med detta.

Om du har ett syntaxfel i en konfigurationsfil avvisar Git-servern push-åtgärden. Se [Skyddsblock](../development/protective-block.md).

Den här fasen körs också `composer install` för att hämta beroenden.

### Fas 2: Bygge

>[!NOTE]
>
>Under byggfasen är platsen inte i underhållsläge och om fel eller problem uppstår inte tas bort. Den skapar bara den kod som har ändrats sedan föregående version.

Den här fasen bygger kodbasen och kör kopplingar i `build` avsnitt i `.magento.app.yaml`. Standardbyggkroken är `php ./vendor/bin/ece-tools` och utför följande:

- Tillämpar patchar i `vendor/magento/ece-patches`och valfria, projektspecifika programfixar i `m2-hotfixes`
- Återskapar kod och [beroendeinjektion](https://experienceleague.adobe.com/docs/commerce-operations/operational-playbook/glossary.html) konfiguration (d.v.s. `generated/` katalog, som innehåller `generated/code` och `generated/metapackage`) med `bin/magento setup:di:compile`.
- Kontrollerar om [`app/etc/config.php`](../store/store-settings.md) filen finns i koddatabasen. Adobe Commerce genererar automatiskt den här filen om den inte upptäcks under byggfasen och innehåller en lista med moduler och tillägg. Om den finns fortsätter byggfasen som vanligt, statiska filer komprimeras med GZIP och distribueras, vilket minskar driftstoppen i distributionsfasen. Se [byggalternativ](../environment/variables-build.md) om du vill veta mer om hur du anpassar eller inaktiverar filkomprimering.

>[!WARNING]
>
>För närvarande har klustret inte skapats, så försök inte ansluta till en databas eller anta att det finns en aktiv daemon-process.

När programmet har byggts monteras det på en **skrivskyddat filsystem**. Du kan konfigurera specifika monteringspunkter som ska läsas/skrivas. Du kan inte använda FTP på servern och lägga till moduler. I stället måste du lägga till kod i din lokala databas och köra `git push`, som bygger och driftsätter miljön. Information om projektstrukturen finns i [Lokal projektkatalogstruktur](../project/file-structure.md).

### Fas 3: Förbered instruktionsmarginalen

Resultatet av byggfasen är ett skrivskyddat filsystem som kallas _instruktionsmarginal_. Den här fasen skapar ett arkiv och placerar instruktionsmarginalen i permanent förvaring. Nästa gång du trycker på kod används instruktionsmarginalen från arkivet om tjänsten inte ändrades.

- Gör att integrationen går fortare genom att återanvända oförändrad kod
- Om koden ändras uppdateras instruktionsmarginalen för nästa version så att den återanvänds
- Möjliggör omedelbar återställning av en distribution vid behov
- Inkluderar statiska filer om `app/etc/config.php` filen finns i koddatabasen

Instruktionsmarginalen innehåller alla filer och mappar **förutom följande** uppsättningar konfigurerade i `magento.app.yaml`:

- `"var": "shared:files/var"`
- `"app/etc": "shared:files/etc"`
- `"pub/media": "shared:files/media"`
- `"pub/static": "shared:files/static"`

### Fas 4: Distribuera instruktionsmarginaler och kluster

Dina program och alla [serverdel](https://experienceleague.adobe.com/docs/commerce-operations/operational-playbook/glossary.html) Tillhandahållande av tjänster enligt följande:

- Monterar varje tjänst i en behållare, till exempel webbserver, OpenSearch, [!DNL RabbitMQ]
- Monterar filsystemet för läsbehörighet (monterat på ett distribuerat lagringsrutnät med hög tillgänglighet)
- Konfigurerar nätverket så att tjänsterna kan &quot;se&quot; varandra (och bara varandra)

>[!NOTE]
>
>Gör ändringarna i en Git-gren när alla bygg- och driftsättningar är klara och kör igen. Alla miljöfilsystem är _skrivskyddad_. Ett skrivskyddat system garanterar deterministiska driftsättningar och förbättrar säkerheten på platsen dramatiskt eftersom ingen process kan skriva till filsystemet. Det fungerar också för att säkerställa att koden är identisk i miljö som omfattar integrering, mellanlagring och produktion.

### Fas 5: Distributionsnätverk

>[!NOTE]
>
>Den här fasen placerar [!DNL Commerce] i underhållsläge tills distributionen är klar.

I det sista steget körs ett distributionsskript som du kan använda för att anonymisera data i utvecklingsmiljöer, rensa cacheminnen och fråga efter externa verktyg för kontinuerlig integrering. När det här skriptet körs har du tillgång till alla tjänster i din miljö, till exempel Redis.

Om `app/etc/config.php` filen finns inte i koddatabasen, statiska filer komprimeras med `gzip` och driftsättas under denna fas, vilket ökar driftsättningsfasens längd och webbplatsens underhåll.

>[!NOTE]
>
>Se [driftsättningsvariabler](../environment/variables-deploy.md) om du vill veta mer om hur du anpassar eller inaktiverar filkomprimering.

Det finns två driftsättningskrokar. The `pre-deploy.php` kroken slutför nödvändig rensning och hämtning av resurser och kod som genererats i byggkroken. The `php ./vendor/bin/ece-tools deploy` krok kör en serie kommandon och skript:

- Om Adobe Commerce **inte installerat** installeras den med `bin/magento setup:install`, uppdaterar distributionskonfigurationen, `app/etc/env.php`och databasen för den miljö du anger, till exempel Redis och webbplatsens URL:er. **Viktigt:** När du slutfört [Första gången du distribuerar](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/launch/overview.html) under installationen installerades och driftsattes Adobe Commerce i alla miljöer.

- Om Adobe Commerce **är installerat** utför uppgraderingar. Distributionsskriptet körs `bin/magento setup:upgrade` uppdatera databasschemat och data (vilket är nödvändigt efter tilläggs- eller kärnkodsuppdateringar) och även uppdatera distributionskonfigurationen, `app/etc/env.php`och databasen för din miljö. Distributionsskriptet rensar slutligen cachen för Adobe Commerce.

- Skriptet genererar eventuellt statiskt webbinnehåll med kommandot `magento setup:static-content:deploy`.

- Använder omfång (`-s` flagga i byggskript) med standardinställningen `quick` för en strategi för statisk innehållsdistribution. Du kan anpassa strategin med miljövariabeln [`SCD_STRATEGY`](../environment/variables-deploy.md#scd_strategy). Mer information om dessa alternativ och funktioner finns i [Distributionsstrategier för statiska filer](../deploy/static-content.md) och `-s` flagga för [Distribuera statiska vyfiler](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

>[!NOTE]
>
>Distributionsskriptet använder de värden som definieras av konfigurationsfilerna i `.magento` och skriptet tar bort katalogen och dess innehåll. Din lokala utvecklingsmiljö påverkas inte.

### Efterdistribution: konfigurera routning

När distributionen körs stoppas inkommande trafik vid startpunkten i 60 sekunder och routningen konfigureras om så att webbtrafiken kommer till det nyligen skapade klustret.

Slutförd distribution tar bort underhållsläget för att ge normal åtkomst och skapar säkerhetskopierade (BAK) filer för `app/etc/env.php` och `app/etc/config.php` konfigurationsfiler.

Aktivera generering av statiskt innehåll med `SCD_ON_DEMAND` -variabeln och konfigurera [`post_deploy` krok](../application/hooks-property.md) så att cachen rensas och cachen förinläses (varms) _efter_ behållaren börjar acceptera anslutningar och _under_ normal, inkommande trafik.

Om du vill granska bygg- och distributionsloggar kan du läsa [Visa loggar](../test/log-locations.md#view-and-manage-logs).
