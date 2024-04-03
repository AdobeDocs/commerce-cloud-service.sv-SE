---
title: Arkiv med veringsanteckningar för e-postverktyg
description: Lär dig mer om arkiverade förbättringar för verktygen.
hide: true
hidefromtoc: true
recommendations: noDisplay, noCatalog
exl-id: 96663d2f-ef00-4490-ad2e-06e8041b228e
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '7147'
ht-degree: 0%

---

# Arkiv med veringsanteckningar för e-postverktyg

>[!NOTE]
>
>Versionsinformationen innehåller information och uppdateringar för `ece-tools` v2002.0.22 och senare. Se [Versionsinformation om Cloud Tools Suite](cloud-tools-suite.md) för att få de senaste uppdateringarna för `ece-tools` och andra molnpaket.

## v2002.0.22

The `ece-tools` 2002.0.22 Ändrar strukturen i `ece-tools` paket för att koppla loss releasen av `Adobe Commerce on cloud infrastructure` patchar från ECE-Tools-releasen. Från och med den här versionen levereras korrigeringsfiler och viktiga korrigeringar med [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) paket, som är ett nytt beroende för `ece-tools` paket. Vi har gjort dessa ändringar för att minska komplexiteten när det gäller att schemalägga uppdateringar och arbeta med bidrag från communities.

- ![ny ikon](../../assets/new.svg) **Ändringar av ECE-verktygspaketet**

   - ![ny ikon](../../assets/new.svg) Flyttade Adobe Commerce-patchar från `ece-tools` paketera till ett nytt [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) dispositionspaket.

   - ![ny ikon](../../assets/new.svg) Uppdaterade `composer.json` filen för `ece-tools` paket för att lägga till ett beroende för `magento/magento-cloud-patches` v1.0.0-paket.

   - ![korrigeringsikon](../../assets/fix.svg) Ett problem som orsakade `ece-tools` korrigeringsprocess som ska pausas när korrigeringsfiler används ovanpå säkerhetsutgåvor, med början från version 2.3.2-p2 och senare. Den här frågan introducerades av det nya versionshanteringssystemet för [säkerhetspatchar](https://devdocs.magento.com/guides/v2.3/release-notes/bk-release-notes.html#security-only-patches).<!--MAGECLOUD-4661-->

- ![korrigeringsikon](../../assets/fix.svg) **Korrigeringar och viktiga korrigeringar**-Uppdatera dina molnmiljöer med `ece-tools` version 2002.0.22 för att använda följande korrigeringar och viktiga korrigeringar. Dessa patchar ingår i `magento/magento-cloud-patches` v1.0.0-paket.

   - ![korrigeringsikon](../../assets/fix.svg) **Page Builder säkerhetspatchar för version 2.3.1.x och 2.3.2.x**-Korrigerar ett fel i förhandsgranskningen i Page Builder som gör att oautentiserade användare kan komma åt vissa mallmetoder som kan användas för att aktivera godtycklig kodkörning över nätverket (RCE), vilket resulterar i globala informationsläckor. Problemet kan uppstå om du använder versioner av Page Builder som inte stöds i Adobe Commerce version 2.3.1 och 2.3.2.<!--MAGECLOUD-4649-->

   - ![korrigeringsikon](../../assets/fix.svg) **MSI-korrigeringar**-Åtgärdar problem som orsakade indexeringsfel och prestandaproblem när standardlagerinställningar användes för att hantera lager.<!--MAGECLOUD-4428-->

   - ![korrigeringsikon](../../assets/fix.svg) **Bakåtkompatibilitet för nya e-postgränssnitt**-Korrigerar ett bakåtkompatibilitetsproblem som orsakas av `Magento\Framework\Mail\EmailMessageInterface` PHP-gränssnittet introducerades i Adobe Commerce v2.3.3. Den nya `EmailMessageInterface` ärver från gamla `MessageInterface`och Adobe Commerce kärnmoduler återställs till beroende av `MessageInterface`.<!--MAGECLOUD-4422-->

   - ![korrigeringsikon](../../assets/fix.svg) **Katalogsidindelning fungerar inte i Elasticsearch 6.x**-Korrigerar ett kritiskt problem med sökresultatsidnumrering som påverkar kunder som använder Elasticsearch 6.x som katalogsökmotor.<!--MAGECLOUD-4448-->

## v2002.0.21

- ![ny ikon](../../assets/new.svg) **Dockningsuppdateringar**—

   - ![ny ikon](../../assets/new.svg) **Nya dockningsbilder**- Stöds av version 2.3.3 och senare<!-- MAGECLOUD-3345 -->

      - PHP version 7.3.<!-- MAGECLOUD-4017 -->

      - Finska cachen 6.2.0<!-- MAGECLOUD-4017 -->

   - ![ny ikon](../../assets/new.svg) Stöd har lagts till för att tillämpa anpassad krokkonfiguration som anges i `.magento.app.yaml` i Docker-miljön. Tidigare hade Docker-miljön bara stöd för den förvalda krokkonfigurationen.<!-- MAGECLOUD-3505-->

   - ![ny ikon](../../assets/new.svg) Docker ENV-filer genereras inte längre under Docker-bygget och `docker:config:convert` kommandot är inaktuellt. Motsvarande data lagras nu i `docker-compose.yml` -fil.<!-- MAGECLOUD-3816-->

   - ![ny ikon](../../assets/new.svg) **Uppdaterad PHP-bild**-Added Node.js to the PHP Docker image to support node, npm, and grunt-cli capabilities.<!-- MAGECLOUD-3953 -->

- ![ny ikon](../../assets/new.svg) **Miljövariabeluppdateringar**-

   - ![ny ikon](../../assets/new.svg) Lagt till **LOCK_PROVIDER** använd variabel för att konfigurera låsprovidern som förhindrar att dubblettcron-jobb och cron-grupper startas. Se variabelbeskrivningen i [driftsättningsvariabler](../environment/variables-deploy.md#lock_provider) ämne.<!-- MAGECLOUD-4052 -->

   - ![ny ikon](../../assets/new.svg) Lagt till **CONSUMERS_WAIT_FOR_MAX_MESSAGES** systemvariabel för att konfigurera hur konsumenter ska bearbeta meddelanden från meddelandekön när de använder `CRON_CONSUMERS_RUNNER` systemvariabel för att hantera cron-jobb. Se variabelbeskrivningen i [driftsättningsvariabler](../environment/variables-deploy.md#consumers_wait_for_max_messages) ämne.<!-- MAGECLOUD-4071 -->

   - ![korrigeringsikon](../../assets/fix.svg) Ett problem som kan orsaka databasdeadlock-fel när `consumers_runner` cron-jobbet startar flera instanser av samma konsument på olika noder. Om du har aktiverat [**CRON_CONSUMERS_RUNNER**](../environment/variables-deploy.md#cron_consumers_runner) driftsätta variabeln i din miljö, `consumers_runner` jobbet använder `single-thread` möjlighet att starta en instans av varje konsument på endast en nod.<!-- MAGECLOUD-3913 -->

   - ![korrigeringsikon](../../assets/fix.svg) Ett problem som påverkade har åtgärdats [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) funktioner som använder en standard-webblänk. Om `config:show:default-url` det går inte att hämta en bas-URL, används URL:en från variabeln MAGENTO_CLOUD_ROUTES.<!-- MAGECLOUD-3866 -->

- ![ny ikon](../../assets/new.svg) Loggningsinformationen som returnerades av `module:refresh` -kommando. Nu kan du se en detaljerad lista över aktiverade moduler i `cloud.log` -fil.<!-- MAGECLOUD-2514 -->

- ![ny ikon](../../assets/new.svg) Förbättrad versionskompatibilitetsvalidering och varningsmeddelanden om kompatibilitetsproblem mellan Adobe Commerce-versionen och installerade tjänster som Elasticsearch. [!DNL RabbitMQ], Redis och DB.<!-- MAGECLOUD-3535 -->

- ![ny ikon](../../assets/new.svg) Stöd för RabitMQ version 3.8 har lagts till.<!-- MAGECLOUD-4674-->

- ![ny ikon](../../assets/new.svg) Uppdaterade interaktiva valideringar för kompatibilitet med tjänster som återspeglar vilka versioner som stöds för nya utgåvor av Adobe Commerce 2.3.3 och 2.2.10. Se [Systemkrav](https://devdocs.magento.com/guides/v2.4/install-gde/system-requirements.html) i _Installationsguide_ för rekommenderade versioner.<!-- MAGECLOUD-4018 -->

- ![korrigeringsikon](../../assets/fix.svg) Förbättrade loggmeddelandet som returneras när processen för hantering av cron-jobb i distributionsfasen försöker stoppa ett cron-jobb som redan har slutförts för att klargöra att problemet inte är ett fel. Loggnivån har ändrats från `INFO` till `DEBUG`.<!-- MAGECLOUD-3653-->

- ![korrigeringsikon](../../assets/fix.svg) Ett problem som uppstod när `setup:upgrade` kommando som inte avbryter distributionsprocessen när ett fel uppstod under `app:config:import` uppgift.<!-- MAGECLOUD-3806 -->

- ![ny ikon](../../assets/new.svg) Ändrade standardloggnivån för filhanteraren till `debug` för att minska detaljmängden i loggen som visas i [!DNL Cloud Console], samtidigt som du fortfarande tillhandahåller detaljerad information för felsökning.<!-- MAGECLOUD-3871 -->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett problem som orsakade ett fel med statisk innehållsdistribution under bygget. Efter installationen och `ece-tools` config dump, an error occurred if there was no locale specified for the admin user in `config.php` -fil. Nu finns det en standardspråkinställning för administratörsanvändaren i `config.php` -fil.<!-- MAGECLOUD-3957 -->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerat ett `Undefined index error` som inträffar när en `magento-cloud` CLI-kommandot fungerar inte i en miljö som inte har konfigurerats med en säker URL (https). Nu används bas-URL:en (http) i paketet ECE-Tools om den säkra URL:en inte är tillgänglig.<!-- MAGECLOUD-4009 -->

## v2002.0.20

- ![ny ikon](../../assets/new.svg) **Docker Updates**—

   - ![ny ikon](../../assets/new.svg) Nu kan du utföra funktionstestning med `ece-tools` i Docker-miljön. Se [programtestning](https://devdocs.magento.com/cloud/docker/docker-test-magecloud-pkg-code.html).<!-- MAGECLOUD-3129/3684 -->

   - ![ny ikon](../../assets/new.svg) Stöd för konfiguration av PHP-moduler har lagts till med `.magento.app.yaml` -fil. Alla [PHP-tillägg som anges i `.magento.app.yaml` fil](https://devdocs.magento.com/cloud/project/magento-app-php-application.html#php-extensions) blir tillgängliga i Docker PHP-behållarna.<!-- MAGECLOUD-3357 -->

   - ![ny ikon](../../assets/new.svg) Det finns nya kommandon som förbättrar Docker-kommandoradsupplevelsen. Se [`bin/magento-docker` avsnitt i Docker-referensen](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli).<!-- MAGECLOUD-3569 -->

   - ![ny ikon](../../assets/new.svg) Lagt till möjlighet att använda Mutagen.io för att synkronisera filer under utvecklingen mellan den lokala värden och Docker.<!-- MAGECLOUD-3559 -->

   - ![korrigeringsikon](../../assets/fix.svg) Standardsökvägen har korrigerats när Docker-miljön används. När du loggar in i Docker-behållaren med SSH är du nu i projektroten i `/app` som förväntat.<!-- MAGECLOUD-3582 -->

   - ![korrigeringsikon](../../assets/fix.svg) Natriumbiblioteket har uppdaterats från version 1.0.11 till version 1.0.18 och tillägget Natrium-PHP har uppdaterats.<!-- MAGECLOUD-3832 -->

     >[!WARNING]
     >
     >Adobe Commerce i molninfrastruktur måste [Skicka in en Adobe Commerce-supportanmälan](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) för att uppgradera libnatriumpaketet i Pro Production- och Stage-miljöer innan du uppgraderar till Adobe Commerce 2.3.2. För närvarande kan du inte uppgradera Starter-miljöer till Adobe Commerce 2.3.2.

   - ![korrigeringsikon](../../assets/fix.svg) Lagt till `analysis-icu` och `analysis-phonetic` Elasticsearch plugin-program till alla Docker-bilder.<!-- MAGECLOUD-3446 -->

   - ![korrigeringsikon](../../assets/fix.svg) Förbättrade valideringar: När du använder alternativ för `docker:build` måste du ange ett värde när du använder ett alternativ. Dessutom lades valideringen för nodversionen till när `docker:build run` -kommando.<!-- MAGECLOUD-3486 & MAGECLOUD-3678 -->

- ![ny ikon](../../assets/new.svg) **Miljövariabeluppdateringar**—

   - ![ny ikon](../../assets/new.svg) Stöd för databastabellprefix har lagts till med [DATABASE_CONFIGURATION-miljövariabel](../environment/variables-deploy.md#database_configuration).<!-- MAGECLOUD-2901 -->

   - ![ny ikon](../../assets/new.svg) Lagt till **FORCE_UPDATE_URLS** driftsätta variabel för att uppdatera bas-URL:er vid driftsättning i Pro- och Starter-produktions- och staging-miljöer. Se definitionen i [driftsättningsvariabler](../environment/variables-deploy.md#force_update_urls) innehåll.<!-- MAGECLOUD-3602 -->

   - ![ny ikon](../../assets/new.svg) Lagt till **TTFB_TESTED_PAGES** variabel för postdistribution för att konfigurera _Tid till första byte_ sidtester för att kontrollera programprestanda på webbplatser som distribueras till molninfrastrukturen. Se variabelbeskrivningen i [variabler efter distribution](../environment/variables-post-deploy.md).<!-- MAGECLOUD-3643 -->

   - ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett problem med flertrådig SCD, som orsakade slumpmässiga fel vid distribution av statiskt innehåll. Den lösning som medförde att **SCD_THREADS** variabel till `1`. Nu kan du öka antalet efter behov. Se definitionerna i [driftsättningsvariabler](../environment/variables-deploy.md#scd_threads) och [build-variabler](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3611 -->

   - ![korrigeringsikon](../../assets/fix.svg) Du kan konfigurera **WARM_UP_PAGES** systemvariabel för cache-lagring av enstaka sidor, flera domäner och flera sidor. Se den utökade definitionen i [variabler efter distribution](../environment/variables-post-deploy.md#warm_up_pages) innehåll.<!-- MAGECLOUD-3258 -->

- ![korrigeringsikon](../../assets/fix.svg) Lagt till `pub/static/.htaccess` till exkluderingslistan. [Fix inskickad av Björn Kraus på PHOENIX MEDIA GmbH](https://github.com/magento/ece-tools/pull/455).<!-- MAGECLOUD-3545/Github#455 -->

- ![korrigeringsikon](../../assets/fix.svg) Ett fel har korrigerats när alla valideringsmeddelanden visades som `Critical` om minst en validerare på kritisk nivå returnerade ett fel.<!-- MAGECLOUD-3178 -->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett problem som orsakade ett distributionsfel om bas-URL:en inte fanns i databasen.<!-- MAGECLOUD-3075 -->

- ![ny ikon](../../assets/new.svg) Lagt till en ny **`env:config:show`kommando** till `ece-tools` paket som visar miljötjänster, vägar eller variabler. Se [Tjänster, flöden och variabler](https://devdocs.magento.com/cloud/reference/ece-tools-reference.html#services-routes-and-variables). [Funktion från Vladimir Kerkhoff](https://github.com/magento/ece-tools/pull/486).<!-- MAGECLOUD-3451 -->

- ![korrigeringsikon](../../assets/fix.svg) Ett problem som orsakade ett kritiskt fel vid försök att installera Adobe Commerce 2.2.6 eller tidigare med har åtgärdats `ece-tools` utvecklas efter omfaktorisering av skalet.<!-- MAGECLOUD-3665 -->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett problem som medförde att installationer av Adobe Commerce 2.1.x och 2.2.x misslyckades med en varning om att en föråldrad version av Carbon användes.<!-- MAGECLOUD-3704 -->

- ![korrigeringsikon](../../assets/fix.svg) Minskade `cloud.log` loggnivå för gränssnittsutdata från `info` till `debug`.<!-- MAGECLOUD-3277 -->

- ![korrigeringsikon](../../assets/fix.svg) Lagt till `--remove-definers (-d)` till `ece-tools db-dump` om du vill ta bort definitioner från dumpfilen.<!-- MAGECLOUD-3510 -->

## v2002.0.19

- ![korrigeringsikon](../../assets/fix.svg) Korrigerat ett problem som skrev över `env.php` under en distribution, vilket resulterar i att anpassade konfigurationer går förlorade. Denna uppdatering säkerställer att Adobe Commerce om molninfrastruktur uppdaterar `env.php` fil vid varje driftsättning, med bevarade anpassade konfigurationer.<!-- MAGECLOUD-3668 -->

## v2002.0.18

- ![ny ikon](../../assets/new.svg) **Docker Updates**—

   - ![ny ikon](../../assets/new.svg) Nu har Docker-miljön stöd för den cron-konfiguration som definieras i [crons, egenskap i filen .magento.app.yaml](https://devdocs.magento.com/cloud/project/magento-app-properties.html#crons).<!-- MAGECLOUD-3150 -->

   - ![ny ikon](../../assets/new.svg) **Ny dockningsbehållare**—Added a [TLS-termineringsproxybehållare](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) för att underlätta varnishs SSL-terminering via HTTPS.<!-- MAGECLOUD-2890 -->

   - ![ny ikon](../../assets/new.svg) **Ny dockningsbild**—En Node.js-bild har lagts till för Gulp och andra funktioner, som Jasmine JS Unit Testing.<!-- MAGECLOUD-3345 -->

   - ![ny ikon](../../assets/new.svg) **Dockningsbygglägen**—Nu kan du välja att starta Docker-miljön i [Produktionsläge eller utvecklarläge](https://devdocs.magento.com/cloud/docker/docker-launch.html#set-the-launch-mode). Utvecklarläget stöder aktiv utveckling med fullständig, skrivbar behörighet för filsystemet.<!-- MAGECLOUD-3152/3511 -->

   - ![korrigeringsikon](../../assets/fix.svg) Ett problem som orsakade att Docker-distributionen misslyckades med ett `Name or service not known` fel om cachen är konfigurerad för en tjänst som inte är tillgänglig. Nu kan du ta bort en tjänst från [`.magento/services.yaml` fil](https://devdocs.magento.com/cloud/project/services.html). Docker-konfigurationsgeneratorn uppdaterar tjänsten i `docker/config.php.dist` automatiskt.<!-- MAGECLOUD-3369 -->

   - ![ny ikon](../../assets/new.svg) Interaktiva valideringar har lagts till för kompatibilitet med tjänster. Om en begärd tjänst inte är kompatibel med Adobe Commerce-versionen eller andra tjänster _interaktivt läge_ uppmanar användaren med ett meddelande och ett val att fortsätta. Se [Tjänstversioner](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers) för Docker. Använd `-n` för att hoppa över interaktiviteten i CICD-syfte.<!-- MAGECLOUD-3251 -->

   - ![korrigeringsikon](../../assets/fix.svg) Ett problem med Docker-dispositionen har korrigerats `db-dump` som raderade befintliga dumpar.<!-- MAGECLOUD-3366 -->

   - ![korrigeringsikon](../../assets/fix.svg) Ett problem som tilldelade Redis har korrigerats `session`, `default`och `page_cache` cachelagring till samma databas-ID.<!-- MAGECLOUD-3172 -->

- ![ny ikon](../../assets/new.svg) **Miljövariabeluppdateringar**—

   - ![ny ikon](../../assets/new.svg) Den nya **ELASTICSUITE\_CONFIGURATION** systemvariabeln behåller dina anpassade tjänstinställningar mellan distributioner. Se definitionen i [driftsättningsvariabler](../environment/variables-deploy.md#elasticsuite_configuration) innehåll.<!-- MAGECLOUD-3205 -->

   - ![ny ikon](../../assets/new.svg) Lagt till **SCD_MAX_EXECUTION_TIMEOUT** miljövariabel så att du kan öka tiden för att slutföra distributionen av statiskt innehåll från `.magento.env.yaml` -fil. Se definitionen i [driftsättningsvariabler](../environment/variables-deploy.md#scd_max_execution_time), [build-variabler](../environment/variables-build.md#scd_max_execution_time)och [globala variabler](../environment/variables-global.md#scd_max_execution_time).<!-- MAGECLOUD-2822 -->

      - ![ny ikon](../../assets/new.svg) Lagt till **MAGENTO_CLOUD_LOCKS_DIR** miljövariabel för att konfigurera sökvägen till monteringspunkten för låsprovidern i molninfrastrukturen. Lås-providern förhindrar att duplicerade cron-jobb och cron-grupper startas. Den här variabeln stöds i Adobe Commerce version 2.2.5 och senare och konfigureras automatiskt. Se definitionen i [Molnvariabler](../environment/variables-cloud.md).<!-- MAGECLOUD-3135 -->

      - ![korrigeringsikon](../../assets/fix.svg) Ändrad **SCD_THREADS** standardvärden för systemvariabel som automatiskt fastställer det optimala värdet baserat på det upptäckta CPU-trådantalet. Se de uppdaterade definitionerna i [driftsättningsvariabler](../environment/variables-deploy.md#scd_threads) och [build-variabler](../environment/variables-build.md#scd_threads).<!-- MAGECLOUD-3382 -->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett problem med en korrigering för DB Isolation Mechanism som orsakade ett fel vid uppgradering till Adobe Commerce i molninfrastrukturversion 2002.0.16.<!-- MAGECLOUD-3383 -->

- ![korrigeringsikon](../../assets/fix.svg) Lagt till en patch som ersätter _Google Image Charts_ med _Bildscheman_. Läs DevBlog-artikeln [Borttagning och uppdatering av Google Image Charts för M1](https://community.magento.com/t5/Magento-DevBlog/Google-Image-Charts-deprecation-and-update-for-M1/ba-p/125006).<!-- MAGECLOUD-3456 -->

- ![korrigeringsikon](../../assets/fix.svg) Tillagd validering för [SEARCH_CONFIGURATION-variabel](../environment/variables-deploy.md#search_configuration). Distributionen misslyckas när alternativet &quot;engine&quot; inte är inställt och `_merge` är inte obligatoriskt.<!-- MAGECLOUD-3470 -->

- ![korrigeringsikon](../../assets/fix.svg) Ett problem som exponerade känsliga data efter ett undantag har korrigerats. Nu maskeras den känsliga informationen på rätt sätt.<!-- MAGECLOUD-3525 -->

- ![korrigeringsikon](../../assets/fix.svg) Förbättrade feltoleranta inställningar för paketet Magento Open Source. Om Adobe Commerce inte kan läsa data från Redis `slave` en läsning görs från Redis `master` -instans. Se [REDIS_USE_SLAVE_CONNECTION](../environment/variables-deploy.md#redis_use_slave_connection).<!-- MAGECLOUD-2899 -->

## v2002.0.17

>[!NOTE]
>
>The `ece-tools` version 2002.0.17 innehåller en viktig säkerhetskorrigering. Se [Tekniska resurser: Magento Open Source Patchar](https://magento.com/tech-resources/download#download2288).

- ![ny ikon](../../assets/new.svg) **Tjänstuppdateringar**—Stöds av följande Adobe Commerce-versioner: 2.2.8 och senare 2.2.x, 2.3.1 och senare 2.3.x

   - Stöd för Elasticsearch version 6.x har lagts till.<!-- MAGECLOUD-3196 -->

   - Stöd för Redis version 5.0 har lagts till.

- ![ny ikon](../../assets/new.svg) **Nya dockningsbilder**—Följande tjänster har lagts till i Docker-bygget:

   - Elasticsearch 6.5<!-- MAGECLOUD-3196 -->

   - Redis 5.0<!-- MAGECLOUD-3223 -->

- ![ny ikon](../../assets/new.svg) **Ny miljövariabel**- Tidigare fanns det en hårdkodad timeout för SCD-komprimering. Nu kan du konfigurera tidsgränsen för SCD-komprimering med **SCD_COMPRESSION_TIMEOUT** miljövariabel. Se definitionerna i [build-variabler](../environment/variables-build.md#scd_compression_timeout) och [driftsättningsvariabler](../environment/variables-deploy.md#scd_compression_timeout) innehåll.<!-- MAGECLOUD-2870 -->

- ![korrigeringsikon](../../assets/fix.svg) Lagt till `--use-rewrites` till installationskommandot så att det använder webbserveromskrivningar för genererade länkar i butiken och administratörsåtkomst för att förbättra säkerheten och kundupplevelsen.<!-- MAGECLOUD-3246 -->

- ![korrigeringsikon](../../assets/fix.svg) Lagt till tidsstämplar i `var/log/install_upgrade.log` så att den visar datum för installations- och uppgraderingshändelser.<!-- MAGECLOUD-2895 -->

## v2002.0.16

- ![ny ikon](../../assets/new.svg) **Dockningsuppdateringar**—

   - Standardkonfigurationen som genereras i Docker-miljön är nu densamma som standardkonfigurationen i Cloud-mallen.<!-- MAGECLOUD-3025 -->

   - Du kan skicka e-post från Docker-miljön med `sendmail` service.<!-- MAGECLOUD-2907 -->

   - Lagt till möjlighet att [konfigurera Xdebug](https://devdocs.magento.com/cloud/docker/docker-development-debug.html) för att felsöka i Cloud Docker-miljön.<!-- MAGECLOUD-2891 -->

   - Ett problem med webbtjänstbehörigheter när `docker-compose.yml` -fil.<!-- MAGECLOUD-2883 -->

- ![ny ikon](../../assets/new.svg) **Förbättrad uppgradering**—Valideringen har lagts till för att bekräfta att `autoload` -egenskapen i `composer.json` filen innehåller nödvändiga konfigurationsändringar innan du uppgraderar till Adobe Commerce v2.3. Se [Uppgraderingsversion](https://devdocs.magento.com/cloud/project/project-upgrade.html).<!-- MAGECLOUD-2392 -->

- ![ny ikon](../../assets/new.svg) Komprimeringsprocessen vid distribution av statiskt innehåll innehåller nu alla resurser - internt genererade eller anpassade - och inträffar under byggfasen i början av [`build:transfer` section](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks). Tidigare inträffade komprimeringsprocessen innan anpassade miniatyrbilder och paketering av statiska resurser tillämpades. [Fix inskickad av Rafael Garcia Lepper från Tryzens Limited](https://github.com/magento/ece-tools/pull/413).<!-- MAGECLOUD-3104 -->

- ![korrigeringsikon](../../assets/fix.svg) Ett databasanslutningsfel som uppstod under distributionen omedelbart efter konfigurering av en ytterligare databas- och tjänstrelation har korrigerats. Den här korrigeringen åtgärdar också ett problem som uppstod under konfigurationsprocessen för Commerce Reporting för Starter. För Starter är denna uppgradering ett måste för att kunna använda Commerce Reporting.<!-- MAGECLOUD-3035 -->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett valideringsfel med databaskonfigurationen som gjorde att distributionsprocessen misslyckades.<!-- MAGECLOUD-3003 -->

- ![korrigeringsikon](../../assets/fix.svg) Begränsningen har uppdaterats med rätt version av `symfony/yaml` paket som ska användas med [PHP-konstanter](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants). Konstantparsning fungerar inte när en `symfony/yaml` tidigare än 3.2. [Fix inlämnad av Vladimir Kerkhoff](https://github.com/magento/ece-tools/pull/404).<!-- MAGECLOUD-2956 -->

- ![ny ikon](../../assets/new.svg) **Kontroll av miljökonfiguration**—Valideringen har lagts till för att kontrollera PHP-versionen och varna användarna om de inte använder den senaste rekommenderade versionen.<!--MAGECLOUD-2903-->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett problem med bearbetning av felformade JSON-variabler. Om en JSON-variabel orsakar ett syntaxfel visas nu en varning i `cloud.log` fil och distribution fortsätter med standardvariabeln.<!-- MAGECLOUD-2851 -->

- ![korrigeringsikon](../../assets/fix.svg) Ett anslutningsfel som uppstod under distributionen omedelbart efter att Redis-tjänsten inaktiverats har åtgärdats.<!-- MAGECLOUD-2747 -->

- ![ny ikon](../../assets/new.svg) **Loggningsändringar**—Uppdaterade [loggnivå](../environment/log-handlers.md#log-levels) från `Info` till `Notice` för följande bygg- och driftsättningshändelser:<!--MAGECLOUD-2925-->

   - Början och slutet av processen för avstämning av installerade moduler i `composer.json` med delade konfigurationsinställningar i `app/etc/config.php` fil

   - Starta och avsluta konfigurationsvalideringsprocessen

   - Början och slutet av `setup:di:compile` process för att generera klasser

- ![ny ikon](../../assets/new.svg) **Nya miljövariabler**—

   - **[RESOURCE_CONFIGURATION - distribueringsvariabel](../environment/variables-deploy.md#resource_configuration)**—Använd den här variabeln för att mappa ett resursnamn till en databasanslutning.<!-- MAGECLOUD-3026 & MAGECLOUD-2963-->

   - **[X_FRAME_CONFIGURATION, global variabel](../environment/variables-global.md#x_frame_configuration)**—Använd den här variabeln för att ändra `X-Frame-Options` huvudkonfiguration för återgivning av en Adobe Commerce-sida i en `<frame>`, `<iframe>`, eller `<object>`.<!-- MAGECLOUD-3048 -->

- ![korrigeringsikon](../../assets/fix.svg) **Miljövariabeluppdateringar**—Följande miljövariabler har ändrats:

   - **[WARM_UP_PAGES](../environment/variables-post-deploy.md)**- Lagt till möjlighet att förhandsladda cacheminnet för angivna sidor på alla domäner som definierats för en Adobe Commerce-butik. Tidigare, om din plats konfigurerades med flera domäner, misslyckades processen efter distributionen med att läsa in cachen för de angivna sidorna i icke-standarddomäner och returnerade följande fel i loggen efter distributionen: `ERROR: Warming up failed: <uri>`<!-- MAGECLOUD-2466 -->

   - **SCD_COMPRESSION_LEVEL**—Dokumentationen och exemplet har uppdaterats `.magento.env.yaml` fil med rätt standardvärden för SCD-komprimeringsnivå. Se definitionerna i [build-variabler](../environment/variables-build.md#scd_compression_level) och [driftsättningsvariabler](../environment/variables-deploy.md#scd_compression_level) innehåll.<!-- MAGECLOUD-2823 -->

   - **SCD_EXCLUDE_THEMES**- Den här systemvariabeln är inaktuell. Använd [SCD_MATRIX](../environment/variables-build.md#scd_matrix) för att styra temats konfiguration.<!--MAGECLOUD-2882-->

   - **SCD\_MATRIX**—Verifieringsprocessen för att förhindra ett problem som uppstod när SCD_MATRIX ignorerade ett temavärde som innehöll olika teckenfall har åtgärdats. Se definitionerna i [build-variabler](../environment/variables-build.md#scd_matrix) och [driftsättningsvariabler](../environment/variables-deploy.md#scd_matrix) innehåll.<!-- MAGECLOUD-2904 -->

   - **ADMIN-variabler**—<!-- MAGECLOUD-2573/MAGECLOUD-2848 -->

      - Förbättrad säkerhet vid hantering av autentiseringsuppgifter för Admin-användaren med hjälp av systemvariabler. Du kan inte längre använda miljövariablerna ADMIN_EMAIL, ADMIN_USERNAME och ADMIN_PASSWORD för att åsidosätta administratörsautentiseringsuppgifter under uppgraderingar. Om du inte kan komma åt administratörspanelen använder du _Glömt lösenord_ funktionen eller `admin:user:create` CLI-kommando för att skapa en ny administratörsanvändare. Se [Öppna din Admin-panel](https://devdocs.magento.com/cloud/onboarding/onboarding-tasks.html#admin).

      - ADMIN_EMAIL behövs inte längre när du uppgraderar eller använder korrigeringsfiler.

## v2002.0.15

- ![ny ikon](../../assets/new.svg) **Dockningsuppdateringar**—

   - Nu använder Docker-generatorn de tjänster som anges i `.magento.app.yaml` och `.magento/services.yaml` konfigurationsfiler när [bygga din Docker-miljö](https://devdocs.magento.com/cloud/docker/docker-config.html). Du kan välja en annan tjänstversion med build-parametrar.<!-- MAGECLOUD-2888 -->

   - PHP 7.2-bild har lagts till - Stöd för PHP 7.2 i Cloud Docker har lagts till; uppdaterat [Starta Docker-konfiguration](https://devdocs.magento.com/cloud/docker/docker-config.html) som innehåller `docker:build --php` om du vill ange vilken version av PHP som är kompatibel med din version av Adobe Commerce.<!-- MAGECLOUD-2799 -->

   - Lagt till en [Kronbehållare](https://devdocs.magento.com/cloud/docker/docker-containers-cli.html#cron-container) baserat på PHP-CLI-bilden.<!-- MAGECLOUD-2565 -->

   - Följande tjänster har lagts till i Docker-bygget:

      - [!DNL RabbitMQ] 3.5 och 3.7<!-- MAGECLOUD-2567 & 2889-->

      - Elasticsearch 1.7, 2.4 och 5.2<!-- MAGECLOUD-2569 & 2887 -->

      - Redis 3.2 och 4.0<!-- MAGECLOUD-2886 -->

- ![ny ikon](../../assets/new.svg) **Konfigurera med PHP-konstanter**—Stöd för [PHP-konstanter](https://devdocs.magento.com/cloud/project/magento-env-yaml.html#php-constants) i `.magento.env.yaml` konfigurationsfil.<!-- MAGECLOUD- 2575 -->

- ![ny ikon](../../assets/new.svg) **Ny miljövariabel**—Som standard är det bara produktionsmiljön som har Google Analytics aktiverat. Du kan aktivera Google Analytics i mellanlagrings- och integreringsmiljöer med  [ENABLE_GOOGLE_ANALYTICS - miljövariabel](../environment/variables-deploy.md#enable_google_analytics).<!--MAGECLOUD-2879-->

- ![korrigeringsikon](../../assets/fix.svg) Ett problem som tog bort anpassade korrigeringskonfigurationer från `env.php` efter en omdistribution. Nu finns anpassade cron-konfigurationer kvar i `env.php` -fil.<!-- MAGECLOUD-2923 -->

- ![korrigeringsikon](../../assets/fix.svg) Inkonsekvenser i meddelandena och [loggnivåer](../environment/log-handlers.md#log-levels) för att bygga, driftsätta och efterdriftsätta faser. Ökade meddelandenivåerna för inledande och avslutande loggmeddelanden från **info** till **meddelande** för alla faser och delfaser. Inledande och avslutande loggmeddelanden har lagts till, där så är lämpligt.<!-- MAGECLOUD-2919 -->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett problem med kronprocesser som förhindrade att fasen efter distributionen startades, när den konfigurerades. Om du har aktiverat funktionen efter distributionen aktiveras nu kroniprocesserna igen i början av fasen efter distributionen.<!-- MAGECLOUD-2862 -->

- ![korrigeringsikon](../../assets/fix.svg) Ett problem som gjorde att Adobe Commerce inte kunde installeras när en anpassad databaskonfiguration angavs har åtgärdats. Tidigare användes databaskonfigurationen från [MAGENTO_CLOUD_RELATIONSHIP-variabel](../environment/variables-cloud.md) även om du har angett anpassad anslutningsinformation i [DATABASE_CONFIGURATION-miljövariabel](../environment/variables-deploy.md#database_configuration).<!--MAGECLOUD-2736-->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade `config:dump` så att den inkluderar alla webbplatsspråk i `system` i `config.php` -fil.<!--MAGECLOUD-2740-->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerat ett problem som resulterade i _uppvärmning_ fel under fasen efter distributionen genom att URL-referensen för källbasen korrigeras.<!--MAGECLOUD-2797-->

- ![korrigeringsikon](../../assets/fix.svg) Ett problem som genererade filer felaktigt under `setup:di:compile` som påverkar Amazon Pay-modulen.<!--MAGECLOUD-2850-->

## v2002.0.14

- ![ny ikon](../../assets/new.svg) **Verifiera idealiskt läge**—The `ideal-state` Guiden verifierar nu den aktuella konfigurationen under varje distribution och ger tydliga instruktioner för hur konfigurationen uppdateras för att uppnå en snabbare driftsättning utan driftavbrott.<!--MAGECLOUD-2372-->

- ![korrigeringsikon](../../assets/fix.svg) **PCI-kompatibilitet**—Meddelandeprotokollen för Adobe Commerce i molninfrastruktur har uppdaterats så att TLS (Transport Layer Security) version 1.2 krävs vid anslutning till meddelandetjänster från tredje part. Om du använder en meddelandetjänst som inte stöder TLS version 1.2 måste du uppgradera tjänsten. I annat fall visas följande felmeddelande när ditt Adobe Commerce-program försöker ansluta till meddelandeservern för att skicka ett e-postmeddelande: `Unable to connect via TLS`.<!--MAGECLOUD-2521-->

- ![ny ikon](../../assets/new.svg) **Förbättrad distribution**—Valideringen har lagts till för att varna kunderna om en mellanlagrings- eller produktionsmiljö har `dev`, `debug`, eller `debug_logging` för att förhindra prestandaproblem som orsakas av för stor loggningsaktivitet.<!--MAGECLOUD-2517-->

- ![korrigeringsikon](../../assets/fix.svg) **Distributionskorrigeringar**—

   - Nu aktiveras underhållsläget i början av distributionsfasen och inaktiveras i slutet. Om distributionen misslyckas förblir platsen i underhållsläge tills distributionsproblemen har lösts. Tidigare återgick webbplatsen till produktionsläge även om distributionen misslyckades.<!--MAGECLOUD-2603-->

      - Omprövade valideringskontrollerna för distributionsfasen för att nedgradera felnivån för följande distributionsproblem `CRITICAL` till `WARNING` så att distributionen slutförs. Tidigare orsakade dessa problem att distributionen misslyckades.

      - Miljökonfigurationen innehåller felaktiga värden för distribuerings- eller molnvariabler.

   - Elasticsearch-versionen i molninfrastrukturen är inte kompatibel med den version av modulen elasticsearch/elasticsearch som stöds av Adobe Commerce i molninfrastrukturen. Se [Elasticsearch felsökningsartikel](https://support.magento.com/hc/en-us/articles/360015758471-Deployment-fails-or-interrupts-with-cloud-log-error-Elasticsearch-version-is-not-compatible-with-current-version-of-magento) i Adobe Commerce Support Knowledgebase.<!--MAGECLOUD-2600-->

   - Ett problem med de delade konfigurationsinställningarna i dialogrutan har korrigerats `app/etc/config.php` fil som orsakade `recursion detected` fel under distributionen.<!--MAGECLOUD-2173-->

- ![korrigeringsikon](../../assets/fix.svg) **Korrigeringar**—

   - Korrigerade ett problem med cron-schemaläggning som förhindrade att jobb kördes om du angav en annan kronifrekvens än standardfrekvensen (1 minut).<!--MAGECLOUD-2602-->

   - Korrigerade ett fel i distributionsfasen som gjorde att kronijobb kunde fortsätta att köras under distributionen, vilket kan orsaka databaslås och andra kritiska problem. Nu stoppas alla cron-jobb innan distributionsfasen börjar och startas om när distributionen är klar.&lt;!—MAGECLOUD—2537—>

   - Korrigerade cron job-arbetsflödet i version 2.2.x för att låsa upp frysta cron-jobb så att de kan stoppas innan distributionen påbörjas. Tidigare avbröts distributionen av ett låst kron.<!--MAGECLOUD-2501-->

- ![korrigeringsikon](../../assets/fix.svg) Ändrad formatering för `config.php` filen som genereras av `vendor/bin/ece-tools config:dump` om du vill använda korta matrissyntaxer och indrag med 4 blanksteg för att följa Adobe Commerce kodningsstandarder.<!--MAGECLOUD-2527-->

- ![korrigeringsikon](../../assets/fix.svg) Ett distributionsfel som inträffar när `.magento.env.yaml` innehåller `{{ base_url }}` och `{{ unsecure_base_url }}` platshållare för webbkonfigurationer i stället för standardkonfigurationen för URL för ett Adobe Commerce i molninfrastrukturprojekt./<!--MAGECLOUD-2607-->

## v2002.0.13

- ![ny ikon](../../assets/new.svg) **Aktivera driftsättning utan driftstopp**—Nu köar Adobe Commerce på molninfrastruktur förfrågningar med nödvändiga databasändringar under distributionen och tillämpar ändringarna så snart distributionen är klar. Förfrågningar kan hållas i upp till 5 minuter för att säkerställa att inga sessioner går förlorade. Se [Statiska alternativ för innehållsdistribution för att minska driftsättningsdriftsavbrott i molnet](https://support.magento.com/hc/en-us/articles/360004861194-Static-content-deployment-options-to-reduce-deployment-downtime-on-Cloud).<!--MAGECLOUD-2169-->

- ![ny ikon](../../assets/new.svg) **Docker Compose for Cloud**—Gav följande förbättringar av [Dockningskonfiguration](https://devdocs.magento.com/cloud/docker/docker-config.html) process:

   - Lagt till ett kommando—`docker:config:convert` för att konvertera PHP-konfigurationsfiler till Docker ENV-format för att förenkla miljökonfigurationen. Nu kopierar du PHP-konfigurationsfilerna till Docker-katalogen och konverterar dem till Docker ENV-filer. Se [Starta Docker](https://devdocs.magento.com/cloud/docker/docker-config.html).<!--MAGECLOUD-2359-->

   - Installationsprocessen för Adobe Commerce i molninfrastruktur stöder nu driftsättning i både skrivskyddade och skrivskyddade filsystem för att mer noggrant emulera molnfilsystemet. Se [Konfigurera Docker](https://devdocs.magento.com/cloud/docker/docker-config.html).&lt;!—MAGECLOUD—2357—>

   - **Stöd för Redis-tjänster**- En Redis-bild har lagts till, som distribueras till en Docker-behållare och konfigureras automatiskt för att fungera med Docker-installationen.&lt;!—MAGECLOUD—2442—>

   - Nu har du möjlighet att dumpa DB när du använder Cloud Docker [databasbehållare](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#database-container). Du kan också [dela filer](https://devdocs.magento.com/cloud/docker/docker-containers.html#sharing-data-between-host-machine-and-container) mellan en värddator och en behållare med `docker/mnt` katalog.<!-- MAGECLOUD-2577 -->

   - **Stöd för tjänster i varnish**— En lack-bild har lagts till som automatiskt distribueras till en Docker-behållare. Efter distributionen kan du konfigurera lack manuellt enligt Adobe Commerce bästa praxis. Se [Konfigurera och använda engelska](https://devdocs.magento.com/guides/v2.3/config-guide/varnish/config-varnish.html).&lt;!—MAGECLOUD—2358—>

   - Säker åtkomst till webbplatser - SSL-stöd har lagts till för att du ska få åtkomst till Adobe Commerce Store och administratörspanelen.&lt;!—MAGECLOUD—2360—>

- ![korrigeringsikon](../../assets/fix.svg) **Förbättrat stöd för Adobe Commerce i tillägg till molninfrastruktur**—Minimiversionskraven för guzzlehttp-/guzzle-paketet i Adobe Commerce på molninfrastrukturen har försämrats [filen Composer.json](https://devdocs.magento.com/cloud/reference/cloud-composer.html) till version 6.2 så att `ece-tools` paketet är kompatibelt med fler tillägg.<!--MAGECLOUD-2205-->

- ![ny ikon](../../assets/new.svg) **Använd anpassade ändringar i Adobe Commerce-programmet under byggfasen**- Vi delar upp byggfasen i två separata processer så att du kan använda krokar för att göra anpassade ändringar i det statiska innehåll som genereras innan du paketerar programmet för distribution. The _bygg:generera_ skapar kod, använder korrigeringar och genererar statiskt innehåll. The _bygge:överföring_ processen överför genererad kod och statiskt innehåll till slutmålet. Se [Programkopplingar](https://devdocs.magento.com/cloud/project/magento-app-properties.html#hooks).<!--MAGECLOUD-2363-->

- ![korrigeringsikon](../../assets/fix.svg) **Miljökonfigurationskontroller**- Förbättrad validering av miljökonfigurationen för att varna kunderna om versionsinkompatibilitet och konfigurationsfel innan Adobe Commerce byggs och distribueras i molninfrastrukturen.

   - Versionsspecifik validering har lagts till för att identifiera miljövariabler och -värden som inte stöds eller är inaktuella.<!--MAGECLOUD-2183-->

   - En kompatibilitetskontroll för Elasticsearch har lagts till för att varna användare om konfigurationsproblem i Elasticsearch. Distributionen misslyckas nu om serverversionen av Elasticsearch inte är kompatibel med Adobe Commerce. Tidigare gick distributionen att genomföra även om Elasticsearch-versionen var inkompatibel, vilket orsakade problem med produktkatalogen efter webbplatsdistributionen.<!--MAGECLOUD-2389-->

     Du kan lösa inkompatibiliteten genom att [skicka ett supportärende](https://devdocs.magento.com/cloud/trouble/trouble.html) om du vill uppgradera Elasticsearch till en kompatibel version eller ändra Adobe Commerce-konfigurationen för att ange en kompatibel version av Elasticsearch PHP-klienten.

      - För Adobe Commerce version 2.1.x till 2.2.2, uppgradera Elasticsearch till version 2.4.

      - För Adobe Commerce version 2.2.3 och senare, uppgradera Elasticsearch till version 5.2.

      - Om du har Elasticsearch 1.x eller 2.x och inte vill uppgradera ska du uppdatera Adobe Commerce Elasticsearch PHP-klientversionskravet i Composer.json till `"elasticsearch/elasticsearch": "~2.0"`.

   - Förbättrad validering av miljövariabler för att identifiera konfigurationsinställningar som kan orsaka konflikter under bygg-, distributions- och efterdriftfaserna. Ett varningsmeddelande visas till exempel under installations- och uppgraderingsprocessen om den globala inställningen för distribution av statiskt innehåll står i konflikt med inställningarna under bygg- eller distributionsfasen.<!--MAGECLOUD-2156-->

- ![korrigeringsikon](../../assets/fix.svg) **Miljövariabeluppdateringar**—Följande miljövariabler har ändrats:

   - **[SKIP_HTML_MINIFICATION, global variabel](../environment/variables-global.md#skip_html_minification)**—Standardvärdet har ändrats till `true` för att möjliggöra behovsstyrd miniatyrproduktion av HTML, vilket minimerar driftstopp vid driftsättning i miljöer med förproduktion och produktion. Den här konfigurationen krävs för driftsättningar utan driftavbrott.<!--MAGECLOUD-2435-->

   - **[CLEAN_STATIC_FILES - distribuera variabel](../environment/variables-deploy.md#clean_static_files)**- Lagt till funktioner för att hantera bearbetning av rena statiska filer för statiskt innehåll som genereras under byggfasen baserat på miljövariabelinställningen CLEAN_STATIC_FILES. Tidigare rensades alltid statiska innehållsfiler som genererades under byggfasen.<!--MAGECLOUD-1506-->

- ![korrigeringsikon](../../assets/fix.svg) **Loggning**—Utför följande ändringar för att förbättra loggmeddelanden och minska loggstorleken:

   - Loggposter för distributionsfel inkluderar nu kommandoutdata från de åtgärder som orsakar felen, även om miljökonfigurationen inte anger loggning på felsökningsnivå. Se [`MIN_LOGGING_LEVEL`](../environment/variables-global.md#min_logging_level).<!--MAGECLOUD-2489-->

   - Lagt till loggning för distributionsfel som inträffar när genererade fabriker som krävs av vissa tillägg inte kan genereras korrekt eftersom filsystemet är i skrivskyddat läge.<!--MAGECLOUD-2209-->

   - Minskade loggstorlekar och problem med korrigerad formatering orsakade av konfigurationskommandon som använder den interaktiva förloppsindikatorn.<!--MAGECLOUD-2402-->

   - Eliminerade onödig komplexitet och uppdaterade prioritetsnivåerna för vissa loggsatser.<!--MAGECLOUD-2227-->

- ![korrigeringsikon](../../assets/fix.svg) **Korrigeringar**—

   - Ändrade standardinställningarna för konfiguration av cron-jobb för historikens livslängd från 3d (4320 min) till 1h (60 min) för att förhindra prestandaproblem och distributionsfel som kan uppstå när cron-kön fylls för snabbt.<!--MAGECLOUD-2427-->

   - Förbättrad process för hantering av cron-jobb under driftsättningsfasen för att förhindra databaslås och andra kritiska problem. Nu stoppas alla cron-jobb under distributionsfasen och omstart när distributionen har slutförts.<!--MAGECLOUD-2445-->

   - Korrigerade ett problem med låsmekanismen för schemaläggning av konsumenter som startades av cron-jobb i Adobe Commerce version 2.2.0 och senare för att förhindra att cron-jobb startar dubblettkonsumenter.<!--MAGECLOUD-2464-->

- ![korrigeringsikon](../../assets/fix.svg) Ett problem med [komprimeringsprocess för statiskt innehåll](../environment/variables-intro.md) (`gzip`) som orsakade `not overwritten` och `no such file or directory` fel när den komprimerade filen refereras under distributionsprocessen.<!-- MAGECLOUD-2182-->

- ![korrigeringsikon](../../assets/fix.svg) Ett problem som förhindrade `php ./vendor/bin/ece-tools config:dump` kommandot inte ta bort överflödiga avsnitt från `config.php` filen under dumpprocessen om butikens språkområde inte anges. Nu kan du enkelt flytta konfigurationsfiler mellan miljöer. När du har uppdaterat till `ece-tools` v2002.0.13, återskapa äldre `config.php` filer med de förbättrade `config:dump` -kommando. Se [Konfigurationshantering för lagringsinställningar](https://devdocs.magento.com/cloud/live/sens-data-over.html).<!--MAGECLOUD-2444-->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett problem som orsakade ett fel under distributionsfasen om flödeskonfigurationen i `.magento/routes.yaml` filen omdirigeras från en [apex](https://blog.cloudflare.com/zone-apex-naked-domain-root-domain-cname-supp/) till en `www` domän.<!--MAGECLOUD-2556-->

- ![korrigeringsikon](../../assets/fix.svg) Ett problem med `_merge` för [`SEARCH_CONFIGURATION`](../environment/variables-deploy.md#search_configuration) variabel som orsakade felaktiga sammanfogningsresultat om du inte inkluderar `engine` parameter i den uppdaterade `.magento.env.yaml` konfigurationsfil. Sammanfogningsåtgärden skriver nu bara över de värden som du angav i den uppdaterade `.magento.env.yaml` utan att du behöver ange `engine` parameter.<!--MAGECLOUD-2520-->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett Redis-konfigurationsproblem som felaktigt aktiverade sessionslås för Adobe Commerce i molninfrastrukturversion 2.2.1 och senare, vilket kan orsaka långsamma prestanda och timeout. Sessionslås är nu inaktiverat som standard. Problemet orsakades av en ändring av standardbeteendet för `disable_locking` parameter som introducerades i v1.3.4 i Redis-sessionshanterarpaketet. Se [colinblöenhour/php-redis-session-abstract package](https://github.com/colinmollenhour/php-redis-session-abstract).<!-- MAGECLOUD-2515-->

## v2002.0.12

- ![ny ikon](../../assets/new.svg) **Docker Compose for Cloud**—Ett kommando har lagts till—`docker:build`—för att generera en [Docker Compose](https://devdocs.magento.com/cloud/docker/docker-config.html) konfiguration från molnet `ece-tools` databas.<!-- MAGECLOUD-2250 -->

- ![ny ikon](../../assets/new.svg) **Ändra språk**—Nu kan du ändra språkområdet för butiken utan export och import av konfigurationsprocessen. Medan programmet är i produktion och SCD_ON_DEMAND är aktiverat är språkinställningarna för lagring och administration tillgängliga.<!-- MAGECLOUD-2019 -->

- ![ny ikon](../../assets/new.svg) <!-- MAGECLOU-1998 -->**Webbplatskarta och robotar**—Skapade en [arbetsflöde](../store/robots-sitemap.md) för att lägga till `robots.txt` och generera en `sitemap.xml` för en enda domänkonfiguration utan att infrastrukturen behöver ändras.

- ![ny ikon](../../assets/new.svg) **Guider**—Två har lagts till [guider](../deploy/smart-wizards.md) för att hjälpa dig med molnkonfigurationen:<!-- MAGECLOUD-1910 -->

   - `ideal-state`—konfigurera det idealiska läget för minimal driftsättning

   - `master-slave`—configure load balance for database and Redis

- ![ny ikon](../../assets/new.svg) **Moduluppdatering**—Ett molnkommando har lagts till—`module:refresh`- för att aktivera moduler som har inaktiverats eller inte uttryckligen aktiverats, på samma sätt som det görs automatiskt under ett bygge.<!-- MAGECLOUD-1521 -->

- ![ny ikon](../../assets/new.svg) Lagt till möjlighet att välja att sammanfoga eller skriva över konfiguration för tjänster med `_merge` alternativ i [CACHE](../environment/variables-deploy.md#cache_configuration), [SESSION](../environment/variables-deploy.md#session_configuration), [KÖ](../environment/variables-deploy.md#queue_configuration)och [SÖK](../environment/variables-deploy.md#search_configuration) konfigurationer.<!-- MAGECLOUD-2105 -->

- ![ny ikon](../../assets/new.svg) **Exempelfil för miljökonfiguration**—Vi lade till en `.magento.env.yaml` Exempelfil till paketet ECE-Tools som innehåller en detaljerad beskrivning och möjliga värden för varje miljövariabel.<!-- MAGECLOUD-1908 -->

   - Vi har också lagt till en djupgående validering för `.magento.env.yaml` konfiguration som förhindrar fel i distributionsprocessen orsakade av oväntade värden. När ett fel inträffar får du nu ett detaljerat felmeddelande som börjar med: `Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:`<!-- MAGECLOUD-1907 -->

- ![ny ikon](../../assets/new.svg) Följande har lagts till [**Miljövariabler**](../environment/variables-intro.md):

   - Nu kan du definiera flera språkområden för varje tema med hjälp av den nya [SCD_MATRIX](../environment/variables-deploy.md#scd_matrix) systemvariabel, vilket minskar antalet temafiler som ska distribueras.<!-- MAGECLOUD-1501 -->

   - Lagt till [DATABASE_CONFIGURATION](../environment/variables-deploy.md#database_configuration) systemvariabel för att anpassa databasanslutningar för distribution.<!-- MAGECLOUD-2047 -->

   - Den nya [MIN_LOGGING_LEVEL](../environment/variables-global.md#min_logging_level) variabeln åsidosätter den lägsta loggningsnivån för alla utdataströmmar utan att göra ändringar i koden.<!-- MAGECLOUD-2129 -->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett problem som orsakade driftstopp mellan driftsättnings- och postdistributionsfasen. Nu börjar fasen efter driftsättningen _omedelbart_ efter att distributionsfasen har avslutats.

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett problem som inte rensade de lyckade kronjobben, de med `status = success`, från schemat.<!-- MAGECLOUD-2268 -->

- ![korrigeringsikon](../../assets/fix.svg) Ett problem med `post_deploy` som rensade cacheminnet i distributionsfasen i stället för i projektfasen efter distributionen.<!-- MAGECLOUD-2113 -->

- ![korrigeringsikon](../../assets/fix.svg) Ett problem har korrigerats vid användning av SCD med flera språkområden som genererade samma `js-translation.json` fil för varje språkområde.<!-- MAGECLOUD-2034 -->

- ![korrigeringsikon](../../assets/fix.svg) Optimerad `db:dump` i `ece-tools` för att undvika att låsa tabeller och öka hastigheten.<!-- MAGECLOUD-2033 -->

## v2002.0.11

>[!NOTE]
>
>ECE-verktygen version 2002.0.11 krävs för kompatibilitet med 2.2.4.

- ![ny ikon](../../assets/new.svg) **Konfigurera skrivskyddade anslutningar till icke-huvudnoder**—Den här versionen ger möjlighet att konfigurera en skrivskyddad anslutning till en icke-huvudnod för att ta emot skrivskyddad trafik (för  [MariaDB](../environment/variables-deploy.md#mysql_use_slave_connection)).<!--MAGECLOUD-143 -->[Redis](../environment/variables-deploy.md#redis_use_slave_connection) och for <!--MAGECLOUD-143 -->

- ![ny ikon](../../assets/new.svg) **Konfigurationsguiden**- En guide har lagts till för att verifiera din konfiguration för statisk innehållsdistribution. Se [Smarta guider](../deploy/smart-wizards.md).<!--MAGECLOUD-1910 -->

- ![ny ikon](../../assets/new.svg) **Stöd för Symfony Console**—Stöd för Symfony Console 4 har lagts till med Adobe Commerce 2.3.<!-- MAGECLOUD-1966 -->

- ![korrigeringsikon](../../assets/fix.svg) **Optimeringar för Cron-planering**- Förbättrad köhantering och förbättrad loggning för felsökning av kronrelaterade problem.<!-- MAGECLOUD-1607 -->

- ![korrigeringsikon](../../assets/fix.svg) Distributionsvalideringen misslyckas om en `ADMIN_EMAIL` eller `ADMIN_USERNAME` är samma som ett befintligt administratörskonto.<!-- MAGECLOUD-1221 -->

- ![korrigeringsikon](../../assets/fix.svg) SOLR-stöd för 2.2.x-versioner har tagits bort. 2.1.x-versionerna behåller möjligheten att aktivera SOLR.<!-- MAGECLOUD-1282 -->

- ![korrigeringsikon](../../assets/fix.svg) Den första installationen av Staging- och Production-miljöerna i ett PRO-projekt innehåller nu olika indexprefix för Elasticsearch för att förhindra eventuella konflikter samtidigt som man identifierar poster som tillhör respektive miljö.<!-- MAGECLOUD-1489 -->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett problem som avbröt byggfasen för äldre arkitektur under distributionen av statiskt innehåll.<!-- MAGECLOUD-2021 -->

- ![korrigeringsikon](../../assets/fix.svg) **Kronspecifika förbättringar**—Kronimplementeringen har omarbetats:<!-- MAGECLOUD-1607 -->

   - Korrigerade ett problem som gjorde att cron-kön snabbt fylldes. Nu kan man ta bort de gamla cron-jobben på ett mer tillförlitligt sätt.

   - Ordnade om sekvensen av kroniska jobb så att alla jobb i separata trådar startar före den allmänna gruppen.

   - Förbättrad loggning för att underlätta felsökning av kron.

   - **ANMÄRKNING**- Den här versionen åtgärdar många kronrelaterade problem. Om du använder vissa kronrelaterade korrigeringar i _m2-snabbkorrigeringar_, tar bort dem.

- ![korrigeringsikon](../../assets/fix.svg) **SCD-specifika förbättringar**—

   - Du kan använda `VERBOSE_COMMANDS` och `SCD_COMPRESSION_LEVEL` miljövariabler under båda _bygg_ och de_ploy-faser.<!-- MAGECLOUD-1819 -->

   - Ett problem som orsakade att distributionen misslyckades med ett slumpmässigt fel när ett oväntat värde för `SCD_COMPRESSION_LEVEL` miljövariabel. Förbättrad konfigurationsvalidering för att ge meningsfulla meddelanden. Se [`SCD_COMPRESSION_LEVEL`](../environment/variables-build.md#scd_compression_level) för godtagbara värden.<!-- MAGECLOUD-2043 -->

   - Åtgärdade beteendet för `SCD_COMPRESSION_LEVEL` konfigurationsflöde för systemvariabel så att åsidosättningarna fungerar som förväntat.<!-- MAGECLOUD-2044 -->

   - Ett problem som förhindrade konfigurationen av `SCD_THREADS` miljövariabel i `.magento.env.yaml` fil _driftsätta_ stage.<!-- MAGECLOUD-2046 -->

## v2002.0.10

- ![ny ikon](../../assets/new.svg) **Statisk innehållsdistribution (SCD)**—Det finns en ny, alternativ distributionsprocess för att generera statiskt innehåll när det efterfrågas (on-demand). Detta minskar driftstoppen och förbättrar cachehanteringen genom att generera de mest kritiska resurserna.<!-- MAGECLOUD-1285 -->

   - **Ny miljövariabel**—Added the `SCD_ON_DEMAND` global miljövariabel för att generera statiskt innehåll vid behov.<!-- MAGECLOUD-1738 -->

   - **Krok efter driftsättning**—Added a `post_deploy` krok för `.magento.app.yaml` fil som rensar cachen och läser in cachen i förväg (varmar) _efter_ behållaren accepterar anslutningar. Det är bara tillgängligt för Pro-projekt som innehåller miljöer för stapling och produktion i [!DNL Cloud Console] och för Starter-projekt. Även om det inte är nödvändigt fungerar detta tillsammans med `SCD_ON_DEMAND` miljövariabel.<!-- MAGECLOUD-1788 -->

- ![ny ikon](../../assets/new.svg) **Optimering**- Optimerad flyttning eller kopiering av filer under driftsättningen för att förbättra driftsättningshastigheten och minska belastningen på filsystemet.<!-- MAGECLOUD-1842 -->

- ![ny ikon](../../assets/new.svg) **Distributionsloggning**- Lagt till möjlighet att aktivera hanterare för Syslog och GELF (Graylog Extended Log Format) för att mata ut loggar under distributionsprocessen. Se [Loggningshanterare](../environment/log-handlers.md).<!-- MAGECLOUD-1751 -->

- ![ny ikon](../../assets/new.svg) Följande har lagts till [**Miljövariabler**](../environment/variables-intro.md):

   - `CRYPT_KEY`—Ange en kryptografisk nyckel för en annan miljö när du flyttar en databas.<!-- MAGECLOUD-1556 -->

   - `SKIP_HTML_MINIFICATION`—_Global_ miljövariabel som hoppar över kopiering av statiska vyfiler i `var/view_preprocessed` och genererar minifierad HTML vid begäran.<!-- MAGECLOUD-1621 and MAGECLOUD-1736-->

   - `SCD_ON_DEMAND`—_Global_ systemvariabel för att generera statiskt innehåll vid begäran.<!-- MAGECLOUD-1738 -->

   - `WARM_UP_PAGES`- Du kan lista de sidor som ska användas för att läsa in cachen i förväg. Finns i nya [Variabler efter distribution](../environment/variables-post-deploy.md).

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett problem som involverade en lokalt tillämpad korrigering som bryter distributionen på en instans. Nu kan ECE-Tools upptäcka att en patch har lagts på.<!-- MAGECLOUD-982 -->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade en konflikt mellan JavaScript-paketering och GZIP-funktioner. Nu fungerar de här funktionerna tillsammans på rätt sätt.<!-- MAGECLOUD-1735 -->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett problem som gjorde att CLI-kommandon för ECE-Tools misslyckades i tidigare PHP 7.0.x-versioner.<!-- MAGECLOUD-1744 -->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett problem som förhindrade statisk innehållsdistribution med den kompakta strategin i flera trådar.<!-- MAGECLOUD-1822 -->

- ![korrigeringsikon](../../assets/fix.svg) Ett problem med Redis-sessionslås som orsakade fördröjd administratörsinloggning har åtgärdats. Dessutom är programfixen tillgänglig för 2.1.x.<!-- MAGECLOUD-1853 -->

## v2002.0.9

>[!NOTE]
>
>Du måste [uppgradera Adobe Commerce på molninfrastruktursmetapaket](../dev-tools/install-package.md#update-the-metapackage) för att få detta och alla framtida uppdateringar.

- ![ny ikon](../../assets/new.svg) **ece-tools**—The `ece-tools` paketet har nu stöd för Adobe Commerce 2.1.x.<!-- MAGECLOUD-1086 -->

- ![ny ikon](../../assets/new.svg) **Redis-konfiguration**—Nu kan du [konfigurera Redis](../environment/variables-deploy.md#cache_configuration) sida- och standardcache och Redis-sessionslagring med hjälp av en miljövariabel.<!-- MAGECLOUD-1552 -->

- ![ny ikon](../../assets/new.svg) **Förbättringar av tjänsterna Search, AMQP och Redis**—Vi förenade tjänstkonfigurationsflödet så att det nu fungerar på samma sätt för alla tjänster. Redigera `env.php` fil för att konfigurera tjänster stöds inte längre. Du måste använda systemvariabler eller `.magento.env.yaml` i stället.<!-- MAGECLOUD-1437 -->

- ![korrigeringsikon](../../assets/fix.svg) **Miljövariabler**—

   - Användning av `env:STATIC_CONTENT_THREADS` har tagits bort och kommer att tas bort i en framtida version. Använd [SCD_THREADS](../environment/variables-deploy.md#scd_threads) i stället.<!-- MAGECLOUD-1507 -->

   - The `STATIC_CONTENT_EXCLUDE_THEMES` miljövariabeln har tagits bort. Du måste använda `SCD_EXCLUDE_THEMES` miljövariabel i stället.<!-- MAGECLOUD-1640 -->

- ![korrigeringsikon](../../assets/fix.svg) **Loggning**- Vi förenklade loggningen runt inbyggda korrigeringsåtgärder.<!-- MAGECLOUD-1674 -->

- ![korrigeringsikon](../../assets/fix.svg) Vi har tagit bort `developer` stöd för lägen och `APPLICATION_MODE` miljövariabel eftersom de orsakade oväntat beteende.<!-- MAGECLOUD-1615 -->

- ![korrigeringsikon](../../assets/fix.svg) Vi har åtgärdat ett problem som orsakade statiska innehållsdistributionsfel relaterade till Redis. Nu kan flertrådad statisk innehållsdistribution köras som avsett.<!-- MAGECLOUD-1630 -->

- ![korrigeringsikon](../../assets/fix.svg) Vi har åtgärdat ett problem som hindrade användare från att spara ändringar i konfigurationsfält i Admin, som markerats som känsliga efter att ha kört `app:config:dump` -kommando.<!-- MAGECLOUD-1175 -->

- ![korrigeringsikon](../../assets/fix.svg) Vi har lagt till stöd för en tidigare version av `symfony/yaml` för att korrigera konflikter med vissa paket som ännu inte är kompatibla med den senaste versionen.<!-- MAGECLOUD-1674 -->

## v2002.0.8

>[!NOTE]
>
>Vi gick samman `vendor/magento/ece-patches` med `vendor/magento/ece-tools` i den här versionen. Du behöver inte längre uppdatera `vendor/magento/ece-patches` separat.

**Nya funktioner:**

- **Förbättrad loggning**<!-- MAGECLOUD-1253 -MAGECLOUD-1495 -->
   - Vi förbättrade loggmeddelanden för att ge bättre förklaringar när bygg- eller distributionsprocessen åsidosätter en miljövariabel.
   - Du kan nu se installations- och uppgraderingsförloppet i realtid. Tail the `install_update.log` -fil för att visa förloppet. Exempel:

     ```bash
     tail -f var/log/install_upgrade.log
     ```

- **Nytt cron-kommando**—Du kan nu låsa upp specifika fastnade cron-jobb i stället för att stoppa och starta om alla med [`cron:unlock`](https://support.magento.com/hc/en-us/articles/360033099451) -kommando. Finns inte i 2.1.<!-- MAGECLOUD-1367 -->

- **Enhetlig konfigurationsfil**—Du kan nu konfigurera bygg- och driftsättningsfaser med en [`.magento.env.yaml`](https://devdocs.magento.com/cloud/project/magento-env-yaml.html) -fil.<!-- MAGECLOUD-1369 -->

- **Säkerhetskopiera konfigurationsfiler**—Distributionsprocessen skapar nu automatiskt en säkerhetskopia av `app/etc/env.php` och `app/etc/config.php` konfigurationsfiler efter distributionen. Vi har även lagt till en [nytt CLI-kommando](https://support.magento.com/hc/en-us/articles/360033182871) för att återställa dessa konfigurationsfiler från en säkerhetskopia.<!-- MAGECLOUD-1372 -->

- **Felsöka valideringsfel**—Vi har ändrat det kommando som du måste använda för att åtgärda valideringsfel när `config.php` innehåller inte tillräckligt med data för statisk innehållsdistribution. Tidigare instruerades du av felmeddelandet att köra `bin/magento app:config:dump`. Nu måste du springa `php ./vendor/bin/ece-tools config:dump`.<!-- MAGECLOUD-1491 -->

- **Nya miljövariabler**—Du kan nu använda miljövariabler för att ansluta anpassade [sök](../environment/variables-deploy.md#search_configuration) och [AMQP-baserad](../environment/variables-deploy.md#queue_configuration) till er webbplats.<!-- MAGECLOUD-1410 -->

- Vi implementerade smarta patchar. Paketet tillämpar nu patchar som inte baseras på Adobe Commerce molninfrastrukturversion, utan på patchade paketversioner.<!--MAGECLOUD-1090-->

**Lösta problem:**

- Vi har åtgärdat ett loggningsproblem som orsakade byggfel.<!-- MAGECLOUD-1162 -->

- Vi har åtgärdat ett problem som orsakade timeout-undantag när distributioner körs i interaktivt läge.<!-- MAGECLOUD-1389 -->

- Vi har åtgärdat ett problem som orsakade fel när vi använde den kompakta strategin för att generera statiskt innehåll. Finns inte i 2.1.<!-- MAGECLOUD-1446 MAGECLOUD-1485-->

- Vi har åtgärdat ett problem som hindrade distributionsskriptet från att identifiera miljöer för staging och produktion på rätt sätt.<!-- MAGECLOUD-1493 -->

- Vi har åtgärdat ett problem som orsakade att nätverksproblem orsakade avbrott i databasanslutningar och orsakade fel under installations- och uppgraderingsprocessen.<!-- MAGECLOUD-1520 -->

- Vi har åtgärdat ett problem som förhindrar dig från att exportera konfigurationsfiler med `app:config:dump` mer än en gång. Finns inte i 2.1.<!--  MAGECLOUD-1567  -->

- Vi har åtgärdat en Redis-session _låsning_ problem som orsakade _Administratör_ inloggningsfördröjning. Finns inte i 2.1.<!--  MAGECLOUD-1582  -->

- Vi har åtgärdat ett implementeringsproblem relaterat till versionshantering som orsakade en konflikt med andra Composer-baserade patchningsmoduler.<!-- MAGECLOUD-1450 -->

- Ett problem som orsakade PHP-minnesproblem under importen har åtgärdats.<!-- MAGECLOUD-1310 -->

- Borttagen korrigering; åtgärda fel i `colinmollenhour/credis` v1.6 för att aktivera stöd för Adobe Commerce i molninfrastruktur 2.2.1. Finns inte i 2.1.<!-- MAGECLOUD-1033 -->

## v2002.0.7

**Lösta problem:**

- Vi har tagit bort `var/view_preprocessed` länka för att åtgärda ett problem som orsakade JavaScript-miniatyrbildskonflikter.<!-- MAGECLOUD-1454 -->

## v2002.0.6

**Lösta problem:**

- Vi har åtgärdat ett fel som orsakade `gzip` fel när ett fil- eller katalognamn innehåller blanksteg.<!-- MAGECLOUD-1413 -->

- Vi har åtgärdat ett problem som hindrade distributionsskript från att identifiera och aktivera modulberoenden korrekt.<!-- MAGECLOUD-1424 -->

## v2002.0.5

**Nya funktioner:**

- **Konfigurera en cron-konsument med en miljövariabel**—Nu kan du konfigurera kunderna med nya `CRON_CONSUMERS_RUNNER` miljövariabel.

- **Konfigurationssökning**- Vi söker nu efter viktiga komponenter under bygg-/driftsättningsprocessen och stoppar processen om genomsökningen misslyckas, vilket förhindrar onödiga driftavbrott på grund av att webbplatsen är i underhållsläge.

- **Skapa/distribuera meddelanden**—Vi har lagt till en konfigurationsfil som du kan använda för [konfigurera Slack och/eller e-postmeddelanden](../environment/set-up-notifications.md) för att skapa/driftsätta åtgärder i alla dina miljöer.

- **Komprimering av statiskt innehåll**—Vi komprimerar nu statiskt innehåll med [gzip](https://www.gnu.org/software/gzip/) under bygg- och driftsättningsfaserna. Den här komprimeringen, i kombination med snabb komprimering, minskar storleken på din butik och ökar distributionshastigheten. Om det behövs kan du inaktivera komprimering med en [byggalternativ](../environment/variables-build.md) eller [driftsättningsvariabel](../environment/variables-deploy.md). Mer information finns i följande avsnitt:

   - [Programmiljövariabler](../application/variables-property.md)

   - [Prestanda för statisk innehållsdistribution](../deploy/static-content.md)

   - [Distributionsprocess](https://devdocs.magento.com/cloud/reference/discover-deploy.html)

- **Konfigurationshantering**—Vi genererar nu automatiskt en `app/etc/config.php` -filen i Git-databasen under byggfasen om den inte redan finns. Den automatiskt genererade filen innehåller bara en lista med moduler och tillägg. Om filen redan finns fortsätter byggfasen som vanligt. Om du följer [Konfigurationshantering](../store/store-settings.md) vid ett senare tillfälle uppdaterar kommandona filen utan att ytterligare steg krävs. Se [Distributionsprocess](https://devdocs.magento.com/cloud/reference/discover-deploy.html) för mer information.

- **Databasdumpar**—Vi lade till en `magento/ece-tools` CLI-kommando för att skapa databasdumpar i alla miljöer. I Pro-planproduktionsmiljöer dumpas det här kommandot endast från en av tre noder med hög tillgänglighet, vilket innebär att produktionsdata som skrivs till en annan nod under dumpningen inte kan kopieras. Vi rekommenderar att du sätter programmet i underhållsläge innan du gör en databasdump i produktionsmiljöer. Se [Hantering av säkerhetskopiering](https://devdocs.magento.com/cloud/project/project-webint-snap.html#db-dump) för mer information.

- **Begränsningar för kroniskt intervall har tagits bort**—Standardvärdet för kroniskt intervall för alla miljöer som tillhandahålls i områdena us-3, eu-3 och ap-3 är 1 minut. Standardkronidintervallet i alla andra regioner är 5 minuter för Pro Integration-miljöer och 1 minut för Pro Staging- och Production-miljöer. Om du vill ändra dina befintliga cron-jobb redigerar du inställningarna i `.magento.app.yaml` eller skapa en supportanmälan för produktions-/mellanlagringsmiljöer. Se [Ställ in cron-jobb](../application/crons-property.md#set-up-cron-jobs) för mer information.

**Lösta problem:**

- Ett problem som orsakade långa driftsättningstider på grund av distributionsprocessen som anropar `cache-clean` före statisk innehållsdistribution.<!-- MAGECLOUD-1327 -->

- Vi har åtgärdat ett problem som orsakade fel under det statiska innehållsgenereringssteget i distributionen i produktionsmiljöer.<!-- MAGECLOUD-1322 -->

- Vi har åtgärdat ett problem som förhindrar vissa `magento/ece-tools` kommandon från loggning av utdata till `stderr`.<!-- MAGECLOUD-1264 -->

- Ett problem som förhindrar att bas-URL-värden i `env.php` från att uppdateras i förgreningar.<!-- MAGECLOUD-1242 -->

- Ett problem som orsakade `magento setup:install` kommando för att lägga till ett osäkert prefix (`http://`) för att skydda bas-URL:er.<!-- MAGECLOUD-1171 -->

- Vi har åtgärdat ett problem som förhindrar att korrigeringsfel orsakar distributionsfel.<!-- MAGECLOUD-1170 -->

- Vi har åtgärdat ett problem som förhindrar `ece-tools` från att stoppa körningen och utlösa ett undantag om inga korrigeringsfiler kan användas.<!-- MAGECLOUD-1152 -->

- Ett problem som orsakade fel när butiken lästes in efter att HTML-miniatyrerna aktiverats i Admin har åtgärdats.<!-- MAGECLOUD-1138 -->

## v2002.0.4

**Lösta problem:**

- Nu kan du [manuellt återställa fastnade cron-jobb](https://support.magento.com/hc/en-us/articles/360033099451) med ett CLI-kommando i alla miljöer via SSH-åtkomst. Distributionsprocessen återställer automatiskt cron-jobb.<!-- MAGECLOUD-1355 -->

## v2002.0.3

**Lösta problem:**

- Vi har åtgärdat ett problem som gjorde att sidor gick ut eftersom Redis tog för lång tid att läsa/skriva. Nu kan du använda `disable_locking` i Redis-konfigurationer för att förhindra problemet.<!-- MAGECLOUD-1311 -->

## v2002.0.2

**Lösta problem:**

- The [!DNL RabbitMQ] konfigurationsprocessen hämtar nu alla nödvändiga parametrar automatiskt.<!-- MAGECLOUD-1246 -->

## v2002.0.1

**Nya funktioner:**

- Adobe Commerce i molninfrastrukturen har nu stöd för omfattningar och [strategier för statisk innehållsdistribution](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-static-deploy-strategies.html). Vi har lagt till `–s` parameter med standardinställningen `quick` för den statiska strategin för innehållsdistribution. Du kan använda systemvariabeln [SCD_STRATEGY](../environment/variables-deploy.md) för att anpassa och använda dessa strategier med era bygg- och driftsättningsåtgärder. Den här variabeln stöder alternativen `standard`, `quick`, eller `compact`. Om du väljer `compact`, åsidosätter vi `STATIC_CONTENT_THREADS` värde med `1`, vilket kan göra driftsättningen långsammare, särskilt i produktionsmiljöer. Finns inte i 2.1.<!--- MAGECLOUD-1057 -->

- Vi har skapat en loggfil över miljöer för att hämta in och kompilera bygg- och distributionsåtgärder. The `var/log/cloud.log` filen finns i programmets rotkatalog.<!--- MAGECLOUD-1014 & MAGECLOUD-1023 -->

**Lösta problem:**

- Refactored the `ece-tools` så att det blir kompatibelt med Adobe Commerce i molninfrastruktur 2.2.0 och senare.<!-- MAGECLOUD-919 & MAGECLOUD-1030 -->

- Vi har åtgärdat ett problem som hindrade `ece-tools` från att stoppa körningen och utlösa ett undantag om inga korrigeringsfiler kan användas.<!-- MAGECLOUD-1186 -->

- Vi har åtgärdat ett problem som medförde att undantag uppstod när beroendeinjektionskompilering (di) hoppades över under byggen.<!-- MAGECLOUD-1047 & MAGECLOUD-1049 -->

- Vi har åtgärdat ett problem som gjorde att distributionsprocessen skrev över anpassade Redis-konfigurationer i `env.php` -fil.<!-- MAGECLOUD-1019 -->

- Vi har åtgärdat ett problem som orsakade omdirigeringsslingor på grund av inaktivering som standard av säker administratör.<!-- MAGECLOUD-1020 -->

## v2002.0.0

>[!WARNING]
>
>Det här paketet är inte längre kompatibelt med andra versioner av Adobe Commerce för molninfrastruktur och **bör inte** användas.

### Inledande version

Ursprunglig version av `ece-tools` för Adobe Commerce om molninfrastruktur 2.2.0.
