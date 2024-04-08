---
title: Versionsinformation för ECE-verktyg
description: Se en lista över de senaste förbättringarna av ECE-verktygspaketet.
recommendations: noDisplay, catalog
last-substantial-update: 2024-04-08T00:00:00Z
exl-id: a464b940-c56e-4a7c-9948-559539e25361
source-git-commit: e21f21e34f89b62842bd22c99ff5705f984898e0
workflow-type: tm+mt
source-wordcount: '2905'
ht-degree: 0%

---

# Versionsinformation för ECE-verktyg

The [ece-tools](https://github.com/magento/ece-tools) paket är en uppsättning skript och verktyg som är utformade för att hantera och distribuera Cloud-projekt. I versionsinformationen beskrivs de senaste förbättringarna av det här paketet, som ingår i [Cloud Tools Suite for Commerce](cloud-tools-suite.md).

>[!NOTE]
>
>Se [Uppgradera ECE-verktyg](../dev-tools/update-package.md) för information om uppdatering till den senaste versionen av `ece-tools` paket.

The `ece-tools` paketet använder följande versionssekvens: `200<major>.<minor>.<patch>`

Versionsinformationen innehåller:

- ![ny ikon](../../assets/new.svg) Nya funktioner
- ![korrigeringsikon](../../assets/fix.svg) Korrigeringar och förbättringar

<!--Add release notes below-->


## v2002.1.18 {#latest}

Releasedatum: 8 april 2024

- ![ny ikon](../../assets/new.svg) **PHP** - Stöd för PHP 8.3 har lagts till.
- ![korrigeringsikon](../../assets/fix.svg) Validerare - Uppdaterad EOL-validerare.

## v2002.1.17

Releasedatum: 16 januari 2024

- ![korrigeringsikon](../../assets/fix.svg) **Validerare för Elasticsearch och OpenSearch**- Korrigerade den validerare som skapade ett missvisande meddelande för att installera en söktjänst när LiveSearch är aktiverat.<!-- MCLOUD-10167 -->
- ![korrigeringsikon](../../assets/fix.svg) **Distributionsvarning**—Ett problem som resulterade i distributionsvarningar för mappar som inte är tomma har korrigerats.<!-- MCLOUD-8958 -->

## v2002.1.16

Releasedatum: 16 oktober 2023

- ![ny ikon](../../assets/new.svg) **ENABLE_WEBHOOKS global miljövariabel**—Added the [ENABLE_WEBHOOKS](../environment/variables-global.md#enable_webhooks) global variabel som kan användas med Commerce-webhooks för att ansluta till en extern slutpunkt, till exempel en App Builder-körningsåtgärd eller ett lagerhanteringssystem från tredje part.

## v2002.1.15

Releasedatum: 31 juli 2023

- ![korrigeringsikon](../../assets/fix.svg) **Felkoder**—Uppdaterat felkodsschema och dokumentgenerator för felkod.
- ![korrigeringsikon](../../assets/fix.svg) **Validerare för anpassad Redis-modell**-Valideraren för anpassade Redis-backend-modeller har uppdaterats. [Se exemplet för cachekonfiguration](../environment/variables-deploy.md#cache_configuration).
- ![korrigeringsikon](../../assets/fix.svg) **Validerare för RabbitMQ**- Stöd för RabbitMQ 3.11 har lagts till
- ![korrigeringsikon](../../assets/fix.svg) **Korrigerat fel länk**-Korrigerade fel länk till startdokumentationen i välkomstmallen.

## v2002.1.14

Releasedatum: 10 mars 2023

- ![ny ikon](../../assets/new.svg) **PHP**- Stöd för PHP 8.2 har lagts till.
- ![ny ikon](../../assets/new.svg) **Validerare för tjänster**—Uppdaterade validerare för Commerce 2.4.6 kräver tjänster: MariaDB 10.6, Redis 7.0, PHP 8.2, OpenSearch 2.x och RabbitMQ 3.9.
- ![korrigeringsikon](../../assets/fix.svg) **ece-tools db-dump**—Ett problem som orsakade `db-dump` för att stoppa i förtid.

## v2002.1.13

Releasedatum: 27 oktober 2022

- ![ny ikon](../../assets/new.svg) **Stöd för Adobe I/O Events för Adobe Commerce har lagts till**. Tilläggsutvecklare kan nu använda [Adobe I/O Events](https://developer.adobe.com/events/docs/) ramverk för att skicka Commerce-händelseinformation från molninstanser till deras program skrivna för [Adobe App Builder](https://developer.adobe.com/app-builder/docs/overview/). Adobe I/O Events for Adobe Commerce finns i Partner Preview.<!-- CEXT-932 -->
- ![ny ikon](../../assets/new.svg) **Validerare för OPCache-konfiguration**—En validerare har lagts till för att kontrollera om det finns uteslutna sökvägar i OPcache-konfigurationen.<!-- MCLOUD-9485 -->
- ![korrigeringsikon](../../assets/fix.svg) **Ett problem med GraphQL cachekonfiguration har korrigerats**—Nu håller ECE-Tools GraphQL `id_salt` värde i `cache` i `app/etc/env.php` -fil.<!-- MCLOUD-9486 -->

## v2002.1.12

Releasedatum: 13 september 2022

- ![ny ikon](../../assets/new.svg) **Aktivera`synchronous_replication`**—ECE-verktygsuppsättningar `synchronous_replication=>true` i `app/etc/env.php` fil när `MYSQL_USE_SLAVE_CONNECTION` är aktiverat. Den här konfigurationen påverkar bara Commerce 2.4.6+. Se `MYSQL_USE_SLAVE_CONNECTION` variabelbeskrivning i [Distribuera variabler](../environment/variables-deploy.md#mysql_use_slave_connection).<!-- MCLOUD-9142 -->
- ![ny ikon](../../assets/new.svg) **OpenSearch**—Funktioner för att konfigurera och ställa in `opensearch` för nästa version av Adobe Commerce 2.4.6. Se [Konfigurera OpenSearch-tjänsten](../services/opensearch.md).<!-- MCLOUD-9236 -->

## v2002.1.11

Releasedatum: 4 augusti 2022

- ![korrigeringsikon](../../assets/fix.svg) **ElasticSuite Validator och OpenSearch**—Ett problem med validering av ElasticSuite-integritetskontroll när OpenSearch är installerat har åtgärdats.<!-- MCLOUD-8767 -->
- ![korrigeringsikon](../../assets/fix.svg) **Returtyper för distributionskommandon**—Fasta returtyper för distributionskommandon.<!-- AC-3208 -->
- ![korrigeringsikon](../../assets/fix.svg) **[!DNL RabbitMQ]problem med installation av nya Commerce 2.4.5**—Fixed [!DNL RabbitMQ] krasch vid installation av nya Commerce 2.4.5.<!-- MCLOUD-9059 -->

## v2002.1.10

Releasedatum: 31 mars 2022

- ![korrigeringsikon](../../assets/fix.svg) **Elasticsearch 7.10**—Uppdaterade validerare som stöder version 7.10 av Elasticsearch.<!-- MCLOUD-8548 -->

## v2002.1.9

Releasedatum: 10 mars 2022

- ![ny ikon](../../assets/new.svg) **OpenSearch**—Stöd för OpenSearch har lagts till för Adobe Commerce version 2.4.4, 2.4.3-p2 och 2.3.7-p3.<!-- MCLOUD-8296 -->
- ![ny ikon](../../assets/new.svg) **PHP**- Stöd för PHP 8.1 har lagts till.
- ![korrigeringsikon](../../assets/fix.svg) **symfoni/process**—Kompatibiliteten med symbolen/processen ^5.3 har lagts till.<!-- MCLOUD-8283 -->

- ![ny ikon](../../assets/new.svg) **Flera processer för konsumenter**—Added a `multiple_processes` så att du kan ange antalet processer som ska anges för varje kund. Se `CRON_CONSUMERS_RUNNER` variabelbeskrivning i [Distribuera variabler](../environment/variables-deploy.md#cron_consumers_runner).<!-- MCLOUD-8295 -->
- ![ny ikon](../../assets/new.svg) **OpenSearch-schema och fullständig värdsökväg**—Möjligheten att konfigurera ett Elasticsearch-schema och fullständig värdsökväg har lagts till.
- ![korrigeringsikon](../../assets/fix.svg) **AWS S3**—Metoden för aktivering av AWS S3 har ändrats.
- ![korrigeringsikon](../../assets/fix.svg) **Korrigera drivrutinen_options-läsare**—Läste av driver_options-konfiguration för DB-anslutning från `env.php` fil efter `ece-tools` för validerare.<!-- MCLOUD-8420 -->

## v2002.1.8

Releasedatum: 25 oktober 2021

- ![ny ikon](../../assets/new.svg) **Alternativ dumpplats**—Added the `--dump-directory` så att du kan välja en målkatalog för en DB-dump. Nu `/app/var/dump-main` är standardmålkatalog för en DB-dump. Se [Hantering av säkerhetskopiering: Dumpa databasen](../storage/database-dump.md)<!-- MCLOUD-8063 -->
- ![korrigeringsikon](../../assets/fix.svg) **Uppdatera Monolog**—Uppdaterat minimiversionen som krävs för `monolog` paketera till `^2.3`.<!-- ACMP-1263 -->
- ![korrigeringsikon](../../assets/fix.svg) **Uppdatera Symfony**—Symfony-beroendena har uppdaterats så att de är kompatibla med Adobe Commerce 2.4.4.<!-- ACMP-1533 -->
- ![korrigeringsikon](../../assets/fix.svg) **Funktion/lös automatisk inläsning**—Ett problem har korrigerats vid distribution till en integreringsmiljö och `CRITICAL: [9] Required configuration is missed in autoload section of composer.json file.` fel.<!-- https://github.com/magento/ece-tools/pull/799 -->

## v2002.1.7

Releasedatum: 29 juli 2021

**Konfigurationsuppdateringar**—

- ![ny ikon](../../assets/new.svg) Stöd för Composer 2.0 har lagts till.<!--MCLOUD-8003-->

- ![korrigeringsikon](../../assets/fix.svg) **Uppdaterade krav på dispositionsverktyget för`symphony/console`**—Uppdaterade ECE-verktygen `composer.json` versionskrav för `symphony/console` paket för att åtgärda ett problem som orsakade `di:compile` kommandon som ska misslyckas med följande fel: `Incompatible argument type: Required type: int. Actual type: string`<!--MC-42919-->

- ![korrigeringsikon](../../assets/fix.svg) Uppdaterade programvarukontroller vid utgånget (`eol.yaml`) som ska omfatta Elasticsearch 7.9.x.<!--MCLOUD-7938-->

## v2002.1.6

Releasedatum: 20 april 2021

- ![ny ikon](../../assets/new.svg) **Autentiseringsuppgifter för Redis**- Lagt till möjlighet att läsa Redis-autentiseringsuppgifter från `relationships` under distributionsfasen.<!--MCLOUD-7694-->

- ![ny ikon](../../assets/new.svg) **Autentiseringsuppgifter för Elasticsearch**—Elasticsearch har fått möjlighet att läsa autentiseringsuppgifter från `relationships` under distributionsfasen.<!--MCLOUD-7695-->

- ![ny ikon](../../assets/new.svg) **Dedikerad sessionslagringstjänst**—Added `redis-session` som ett andra alternativ för sessionslagring. Du kan använda `redis-session` för att lagra sessionsinformation och använda `redis` för cachen för att ge bättre prestanda.<!--MCLOUD-7698-->

- ![ny ikon](../../assets/new.svg) **Borttagna SPLIT_DB-meddelanden**—Valideringsvarning och viktiga meddelanden för den borttagna `SPLIT_DB` för Adobe Commerce 2.4.2 och borttagningen av den i Adobe Commerce 2.5.0.<!--MCLOUD-7806-->

- ![korrigeringsikon](../../assets/fix.svg) **Elasticsearch version från relationer**—Tjänstvalideraren för att hämta rätt version av Elasticsearch från `relationships` i Cloud Docker och integreringsmiljöer.<!--MCLOUD-7572-->

- ![korrigeringsikon](../../assets/fix.svg) **Flexibel Redis-portvalidering**—Redis kan nu validera porten i en anpassad cacheanslutning från `server` URL. Du kan t.ex. lägga till ditt portnummer till serverns URL-adress på följande sätt: `server: 'tcp://rfs-store-simple-page-cache:26379'`. Detta förhindrar valideringsfel om `port` Alternativet saknas eller är felaktigt.<!--MCLOUD-7722-->

- ![korrigeringsikon](../../assets/fix.svg) **Uppgradera till Adobe Commerce 2.4.2**—Ett problem som innebar att användare måste köra manuellt har åtgärdats `bin/magento setup:upgrade` för att driftsätta sina anläggningar efter uppgradering till Adobe Commerce 2.4.2.<!--MCLOUD-7776-->

## v2002.1.5

Releasedatum: 1 februari 2021

- ![ny ikon](../../assets/new.svg) **Fjärrlagring**—Added the `REMOTE_STORAGE` miljövariabel för att aktivera molnprojekt för fjärrlagring av mediefiler med hjälp av en lagringstjänst, t.ex. AWS S3. Det här konfigurationsalternativet ingår i ECE-verktygspaketet, men stöds inte av Adobe Commerce i molninfrastruktur.<!--MCLOUD-7153-->

- ![ny ikon](../../assets/new.svg) **Nytt `cloud:config:validate` kommando**—Added, kommando `php vendor/bin/ece-tools cloud:config:validate` för att validera `.magento.env.yaml` innan ändringar görs i fjärrmolnmiljön.<!--MCLOUD-7120-->

- ![ny ikon](../../assets/new.svg) **Tömmer opcache**—Stöd för `opcache.enable_cli` PHP-alternativ för att tömma OPcache innan distributionskroken körs. Den här konfigurationen återställer cachekonfigurationen för att säkerställa att de aktuella konfigurationsinställningarna tillämpas på varje distribution.<!--MCLOUD-7015-->

- ![ny ikon](../../assets/new.svg) **Validering av Aurora DB**—Valideringen av databastjänsten har uppdaterats så att den är kompatibel med Aurora-databasen.<!--MCLOUD-7269-->

- ![ny ikon](../../assets/new.svg) **Ny SCD_NO_PARENT-miljövariabel**—Added the `SCD_NO_PARENT` systemvariabel (för Adobe Commerce >=2.4.2) för att hantera genereringen av statiskt innehåll för överordnade teman.<!--MCLOUD-7284-->

- ![korrigeringsikon](../../assets/fix.svg) **Minnesbegränsningar och kommandon**—Ett problem har korrigerats där `php vendor/bin/ece-tools` fungerar inte om storleken på `cloud.log` filen överskred PHP-minnesgränsen. I stället för att läsa hela `cloud.log` till minnet, vi läser nu bara en mindre delmängd av data från loggfilen.<!--MCLOUD-7275--><!--MCLOUD-7400-->

- ![korrigeringsikon](../../assets/fix.svg) **Anpassade databasanslutningar**—Fixed a `.magento.env.yaml` konfigurationsproblem som anpassade databasanslutningar har definierats för `DATABASE_CONFIGURATION` användes inte. Anslutningsinställningarna lades inte till i `app/etc/env.php`.<!--MCLOUD-7426-->

- ![korrigeringsikon](../../assets/fix.svg) **Tomma felloggar**—Korrigerade ett problem som gjorde att distributioner misslyckades om `cloud.error.log` var tom.<!--MCLOUD-7296-->

- ![korrigeringsikon](../../assets/fix.svg) **MariaDB 10.3-validering**—Fixed validation of MariaDB 10.3 for Adobe Commerce 2.3.6-p1.<!--MCLOUD-7416-->

- ![korrigeringsikon](../../assets/fix.svg) **cache:tömningsloggning**—Förbättrade loggposter som anger början och slutet av `cache:flush` steg.<!--MCLOUD-7503-->

## v2002.1.4

Releasedatum: 19 november 2020

- ![korrigeringsikon](../../assets/fix.svg) Ett problem som orsakade ett distributionsfel när sökmotorn som anges i `SEARCH_CONFIGURATION` miljövariabeln är ett annat värde än `elasticsearch`.<!--MCLOUD-7283-->

## v2002.1.3

Releasedatum: 9 november 2020

**Infrastrukturuppdateringar**—

- ![ny ikon](../../assets/new.svg) Stöd för skrivskyddade ECE-verktyg har lagts till `pub/static` katalog när statiskt innehåll är inställt att distribueras på byggscenen.<!--MC-37699-->

- ![ny ikon](../../assets/new.svg) Stöd för Elasticsearch 7.9 och Redis 6 har lagts till för kompatibilitet med kommande Adobe Commerce-versioner.<!--MCLOUD-7191-->

- ![korrigeringsikon](../../assets/fix.svg) Uppdaterade ECE-verktygen `composer.json` om du vill lägga till ett nödvändigt beroende för verktyget Kvalitetskorrigeringar. Detta åtgärdar ett cirkulärt beroende som fanns mellan ECE-Tools- och magento-cloud-patches-paketen.<!--MCLOUD-6910-->

**Förbättrad validering och loggning**—

- ![ny ikon](../../assets/new.svg) Sökmotorvalidering har lagts till för att säkerställa att `elasticsearch` är inställt för Adobe Commerce i molninfrastruktur 2.4 och senare. Om valideringen misslyckas stoppas distributionen med ett kritiskt felmeddelande som föreslår korrigeringar för problemet. Se [Allvarliga fel, driftsättningsfas](../dev-tools/error-reference.md#deploy-stage).<!--MCLOUD-6937-->

- ![ny ikon](../../assets/new.svg) Elasticsearch har lagts till för att kontrollera kompatibiliteten mellan Elasticsearch och Adobe Commerce-versionen.<!--MCLOUD-7193-->

- ![ny ikon](../../assets/new.svg) Elasticsearch-kompatibilitetsfelmeddelandet har uppdaterats för att visa de versioner av Elasticsearch som är kompatibla med Adobe Commerce Elasticsearch. Felmeddelandet innehåller nu de specifika Elasticsearch-versionerna som ska installeras i din molninfrastruktur, så att den är kompatibel med Elasticsearch-modulen som används i din version av Adobe Commerce. Se [Varningsfel, distribuera fas](../dev-tools/error-reference.md#deploy-stage-1).<!--MCLOUD-6698-->

- ![ny ikon](../../assets/new.svg) Lagt till varningsfel `2026` och `2027` för ogiltig `MAGE_MODE` inställning för systemvariabel. Det enda giltiga värdet är `production`. Före den här korrigeringen `MAGE_MODE` kan anges till `developer` utan distributionsfel, endast för att orsaka fel senare vid försök att skriva till skrivskyddade filer. Se [Varningsfel](../dev-tools/error-reference.md#warning-errors).<!--MCLOUD-6708-->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerad validering för Redis, RabbitMQ och MySQL för att säkerställa att dessa versioner är kompatibla med Adobe Commerce-versionen. Giltiga versioner av dessa tjänster är nu skrivna på `cloud.log`.<!--MCLOUD-7098-->

- ![korrigeringsikon](../../assets/fix.svg) Uppdaterade `cloud.log` om du vill inkludera gränsen för antal samtidiga begäranden för att skicka begäranden under cachevärmningen. Detta värde är konfigurerat i [WARM_UP_CONCURRENCY](../environment/variables-post-deploy.md#warm_up_concurrency) variabel efter distribution.<!--MCLOUD-5563-->

**CLI-kommandouppdateringar**—

- ![ny ikon](../../assets/new.svg) Tillagda CLI-kommandon (`cloud:config:create` och `cloud:config:update`) för att skapa och uppdatera `.magento.env.yaml` en fil med en konfiguration som kan innehålla en eller flera variabler för att skapa, distribuera och efterdistribuera. Se [Skapa konfigurationsfil från CLI](../environment/configure-env-yaml.md#create-configuration-file-from-cli).<!--MCLOUD-7072-->

**Miljövariabeluppdateringar**—

- ![ny ikon](../../assets/new.svg) Lagt till [SKIP_COMPOSER_DUMP_AUTOLOAD](../environment/variables-build.md#skip_composer_dump_autoload) build-variabel. Ange variabeln till `true` stoppar programmet från att köra `composer dump-autoload` under en installation av Cloud Docker för Commerce. Variabeln är endast relevant för Cloud Docker för Commerce-behållare med skrivbara filsystem (skapade för testning och utveckling med `./vendor/bin/ece-docker build:compose --with-test`). Hoppa över `composer dump-autoload` -kommandot förhindrar fel när andra kommandon som försöker få åtkomst till filer från en borttagen `generated` katalog.<!--MCLOUD-6939-->

## v2002.1.2

Releasedatum: 5 augusti 2020

**Förbättrad validering och loggning**—

- ![ny ikon](../../assets/new.svg) Lagt till `schema.error.yaml` -fil som innehåller alla fel- och varningsmeddelanden som kan inträffa under processen för att skapa, distribuera och efterdistribuera samt förslag på hur felen kan åtgärdas. Informationen i den här filen finns också i _Cloud Guide for Commerce_. Se [Felmeddelandereferens för e-postverktyg](../dev-tools/error-reference.md).<!--MCLOUD-5878-->

- ![ny ikon](../../assets/new.svg) Ändrad fellogg för molnet (`/var/log/cloud.error.log`) till JSON-format för att göra loggen enklare att tolka programmatiskt.<!--MCLOUD-5879-->

- ![ny ikon](../../assets/new.svg) Ytterligare felkontroller har lagts till för att skapa, distribuera och efterdistribuera bearbetning och förbättra befintliga kontroller:

   - Felkod 2026 - Det gick inte att återställa vissa data som genererats under byggfasen till de monterade katalogerna

   - Felkod 3004 - Det går inte att skapa säkerhetskopior

   - Felkod 102 - Ytterligare kontroller för problem som inträffar när `env.php` filen är inte skrivbar <!--MCLOUD-6221-->

- ![ny ikon](../../assets/new.svg) Lagt till **QUALITY_PATCH** systemvariabel som anger en eller flera kvalitetspatchar som ska användas under distributionsprocessen. Se [Skapa variabler](../environment/variables-build.md#quality_patches).<!--MCLOUD-6375-->

## v2002.1.1

Releasedatum: 25 juni 2020

- ![ny ikon](../../assets/new.svg) **Infrastrukturuppdateringar**—

   - ![ny ikon](../../assets/new.svg) **Förbättrad loggning**—Förbättrad loggspårning genom att tilldela avslutningskoder till kritiska driftsättningsfel och visa avslutskoderna i felmeddelanden och logghändelser. Se [Felmeddelandereferens för e-postverktyg](../dev-tools/error-reference.md).<!-- MCLOUD-5637, 5531-->

   - ![ny ikon](../../assets/new.svg) Förbättrad process för databasdumpar (`vendor/bin/ece-tools db-dump`) och uppdaterade loggmeddelanden för att förtydliga att databasdumpåtgärden växlar programmet till underhållsläge, stoppar konsumentköprocesser och inaktiverar kronijobb innan dumpningen börjar.<!--MCLOUD-5324, MCLOUD-2062-->

   - ![korrigeringsikon](../../assets/fix.svg) Ett problem har korrigerats för att se till att projektets URL uppdateras korrekt vid distributionen till förproduktionsmiljöer. Nu `ece-tools` använder URL:en för vägen med `primary:true` attribut i projektflödeskonfigurationen. Se [Distribuera variabler](../environment/variables-deploy.md#update_urls).<!--MCLOUD-5883-->

   - ![korrigeringsikon](../../assets/fix.svg) Uppdaterade `generate.xml` arbetsflöde för att skapa scenarier för att tillämpa korrigeringar. Patchar måste användas tidigare för att uppdatera Adobe Commerce för att åtgärda problem som kan orsaka `di:compile` och `module:refresh` steg för att misslyckas.<!--MCLOUD-5941-->

   - ![korrigeringsikon](../../assets/fix.svg) Ett fel som felaktigt returnerade `Crypt key missing` fel. The `crypt/key` värdet genereras automatiskt under installationen.<!--MCLOUD-6120-->

- ![ny ikon](../../assets/new.svg) **Tjänstuppdateringar**—

   - ![ny ikon](../../assets/new.svg) Stöd för PHP 7.4 och MariaDB 10.4 har lagts till.<!--MAGECLOUD-2957, MCLOUD-4144-->

- ![ny ikon](../../assets/new.svg) **Miljövariabeluppdateringar**—

   - ![ny ikon](../../assets/new.svg) Lagt till **SCD_USE_BALER** -variabel för att aktivera Baler-modulen för JavaScript-paketering under byggprocessen för Adobe Commerce om molninfrastruktur. Se variabelbeskrivningen i [build-variabler](../environment/variables-build.md#scd_use_baler).<!-- MCLOUD-3456, MCLOUD-3457-->

   - ![ny ikon](../../assets/new.svg) Lagt till **REDIS_BACKEND** systemvariabel för att konfigurera Redis serverdelsmodell för Redis-cache för Adobe Commerce 2.3.5 eller senare. Se variabelbeskrivningen i [driftsättningsvariabler](../environment/variables-deploy.md#redis_backend).<!--MCLOUD-5721, MCLOUD-5865-->

- ![ny ikon](../../assets/new.svg) **CLI-kommandouppdateringar**—

   - ![ny ikon](../../assets/new.svg) Följande CLI-kommandon har uppdaterats med ett alternativ för mer detaljerad loggning:

      - `app:config:dump`
      - `app:config:import`
      - `module:enable`

     Loggningsnivån för varje samtal bestäms av konfigurationen för [`VERBOSE_COMMANDS`](../environment/variables-build.md#verbose_commands) i `.magento.env.yaml` -fil.<!--MCLOUD-3503-->

- ![ny ikon](../../assets/new.svg) **Förbättrad validering**—

   - ![ny ikon](../../assets/new.svg) **Kompatibilitetskontroller för Elasticsearch 7.x**—Elasticsearch-validering för kompatibilitetskontroller av program i Elasticsearch 7.x har uppdaterats.<!--MCLOUD-5542-->

   - ![ny ikon](../../assets/new.svg) **Uppdaterad serviceversion och EOL-validering**—Valideringen har uppdaterats för att kontrollera installerade tjänstversioner mot Adobe Commerce 2.4.-kraven.<!--MCLOUD-6144-->

   - ![korrigeringsikon](../../assets/fix.svg) Ett valideringsfel har korrigerats så att följande varningsmeddelande visas bara om `post-deploy` krokkonfigurationen saknas i `.magento.app.yaml` fil:

     ```text
     Your application does not have the "post_deploy" hook enabled.
     ```

     <!--MCLOUD-4077-->

   - ![ny ikon](../../assets/new.svg) **Tillagd validering för Zend Framework-beroenden**—Added Composer-beroendevalidering för Zend Framework som har migrerats till Laminas-projektet. Om de nödvändiga beroendena saknas visas följande felmeddelande under byggprocessen.

     ```text
     Required configuration is missing from the autoload section of the composer.json file.
     Add ("Laminas\Mvc\Controller\Zend\": "setupsrc/ Zend/Mvc/Controller/") to
     the `autoload -> psr-4` section. Then, re-run the "composer update" command locally, and
     commit the updated composer.json and composer.lock files.
     ```

     Se [Verifiera Zend Framework-beroenden](../development/commerce-version.md#verify-zend-framework-composer-dependencies).<!--MCLOUD-4094-->

   - ![ny ikon](../../assets/new.svg) **Lagt till validering för `env.php` fil och data**—Kontroller för `env.php` filer och data under installations- och uppgraderingsprocessen.<!--MCLOUD-5991-->

      - Om `env.php` filen saknas i installationen, och `crypt/key` värdet har inte angetts i `.magento.app.yaml` filen, distributionen misslyckas med följande meddelande:

        ```text
        The crypt/key key value does not exist in the ./app/etc/env.php file or the CRYPT_KEY cloud environment variable``Missing crypt key for upgrading Magento`.
        ```

      - Om installationen inte innehåller `env.php` -filen, eller så innehåller konfigurationen bara en cachetyp, `cron:enable` under uppgraderingsprocessen för att återställa filen med alla `cache_types`. Följande meddelande läggs till i loggen:

        ```text
        Magento state indicated as installed but configuration file app/etc/env.php was empty or did not exist.
        Required data will be restored from environment configurations and from the .magento.env.yaml file.
        ```

## v2002.1.0

Releasedatum: 6 februari 2020

- ![ny ikon](../../assets/new.svg) **Infrastrukturuppdateringar**—

   - ![ny ikon](../../assets/new.svg) **Ett separat paket för Cloud Docker för Commerce har lagts till**—Docker-paketet kopplades från från `ece-tools` för att upprätthålla kodkvaliteten och tillhandahålla oberoende releaser. Uppdateringar och korrigeringar relaterade till `ece-tools` hanteras från [magento-cloud-docker](https://github.com/magento/magento-cloud-docker) GitHub-databas.<!--MAGECLOUD-2927-->

   - ![ny ikon](../../assets/new.svg) **Uppdaterade patchfunktioner**- Flyttade patchfunktionen från ECE-verktygspaketet till ett separat [magento-cloud-patches](https://github.com/magento/magento-cloud-patches) paket. Under driftsättningen, `ece-tools` använder det nya paketet för att tillämpa korrigeringar. Se [Versionsinformation om molnpatchar](cloud-patches.md).<!--MAGECLOUD-4567-->

   - ![ny ikon](../../assets/new.svg) **Uppdaterade Composer-beroenden**—Uppdaterade `composer.json` fil för Adobe Commerce på molninfrastruktur med ett beroende för `magento/magento-cloud-docker` paket. Nu `ece-tools` innehåller beroenden för alla paket i [`Cloud Tools Suite for Commerce`](cloud-tools-suite.md). Dessa paket installeras och uppdateras automatiskt när du installerar eller uppdaterar `ece-tools`.

- ![ny ikon](../../assets/new.svg) **Stöd för scenariobaserade distributioner**—<!--MAGECLOUD-4101-->

   - ![ny ikon](../../assets/new.svg) Nu kan du anpassa processerna för att bygga, driftsätta och efterdriftsätta med hjälp av XML-konfigurationsfiler för att åsidosätta eller anpassa standardkonfigurationen.

   - ![ny ikon](../../assets/new.svg) **Ändrad `hooks` konfiguration i`.magento.app.yaml`**—Vi uppdaterade `hooks` konfigurationsformat för stöd för scenariobaserade distributioner. Det äldre formatet från den tidigare versionen av ECE-Tools 2002.0.x stöds fortfarande. Du måste dock uppdatera till det nya formatet för att kunna använda den scenariobaserade distributionsfunktionen. Se [Scenariobaserade distributioner](../deploy/scenario-based.md#add-scenarios-using-build-and-deploy-hooks).

>[!NOTE]
>
>Innan du uppdaterar till ECE-Tools version 2002.1.0 bör du läsa [inkompatibla ändringar bakåt](backward-incompatible-changes.md) om du vill veta mer om ändringar som kan kräva att du uppdaterar Adobe Commerce om projektkonfiguration eller processer för molninfrastruktur.

- ![ny ikon](../../assets/new.svg) **Tjänstuppdateringar**—

   - ![ny ikon](../../assets/new.svg) Stöd för PHP 7.3 har lagts till.<!--MAGECLOUD-4022-->

   - ![ny ikon](../../assets/new.svg) Stöd för RabbitMQ 3.8 har lagts till.<!--MAGECLOUD-4674-->

   - ![ny ikon](../../assets/new.svg) Tillagd validering för att kontrollera installerade tjänstversioner mot EOL-datumet för varje tjänst. Nu får kunderna ett meddelande om en tjänstversion är inom tre månader från EOL-datumet och en varning om EOL-datumet redan har infallit.<!--MAGECLOUD-4076-->

   - ![korrigeringsikon](../../assets/fix.svg) Ett konfigurationsproblem för Elasticsearch har korrigerats för att säkerställa att rätt Elasticsearch-inställningar har konfigurerats i alla miljöer.<!--MAGECLOUD-4474-->

>[!NOTE]
>
>Se [Tjänstversioner](../services/services-yaml.md#service-versions) om du vill ha en lista över tjänster som används i Adobe Commerce i molninfrastrukturen och deras versionskompatibilitet med molnmallen.

- ![ny ikon](../../assets/new.svg) **Miljövariabeluppdateringar**—

   - ![ny ikon](../../assets/new.svg) Utökade funktioner för `WARM_UP_PAGES` systemvariabel som stöder cacheförinläsning för specifika produktsidor. Se den utökade definitionen i [variabler efter distribution](../environment/variables-post-deploy.md#warm_up_pages) ämne.<!--MAGECLOUD-4444-->

   - ![ny ikon](../../assets/new.svg) Lagt till `ERROR_REPORT_DIR_NESTING_LEVEL` miljövariabel för att förenkla datahantering i felrapporter i `<magento_root>/var/report/` katalog. Se variabelbeskrivningen i [build-variabler](../environment/variables-build.md#error_report_dir_nesting_level) ämne.

   - ![korrigeringsikon](../../assets/fix.svg) Borttagen `SCD_EXCLUDE_THEMES`, `STATIC_CONTENT_THREADS`,`DO_DEPLOY_STATIC_CONTENT`och `STATIC_CONTENT_SYMLINK` miljövariabler. Se [Bakåtkompatibla ändringar](backward-incompatible-changes.md#environment-configuration-changes).<!--MAGECLOUD-4407, MAGECLOUD-3873-->

   - ![korrigeringsikon](../../assets/fix.svg) Ett problem i konfigurationsprocessen för Elastic Suite har korrigerats så att standardkonfigurationen skrivs över som förväntat när du konfigurerar `ELASTICSUITE_CONFIGURATION` använd variabeln utan `_merge` alternativ.<!--MAGECLOUD-4388-->

- ![ny ikon](../../assets/new.svg) **CLI-kommandouppdateringar**—

   - ![ny ikon](../../assets/new.svg) **Nytt cron-kommando**—Nu kan du hantera kundbearbetningen i din Adobe Commerce i molninfrastrukturmiljö manuellt med `cron:disable` och `cron:enable` kommandon. Använd kommandot disable (inaktivera) för att stoppa alla aktiva cron-processer och inaktivera alla cron-jobb. Använd kommandot enable för att återaktivera cron-jobb när du är klar. Se [Inaktivera cron-jobb](../application/crons-property.md#disable-cron-jobs).

   - ![ny ikon](../../assets/new.svg) **Förbättrad felrapportering**- Bättre loggning har lagts till för CLI-kommandofel som inträffar under ECE-verktygen-bearbetningen.<!--MAGECLOUD-4849-->

   - ![ny ikon](../../assets/new.svg) **Ta bort inaktuella byggkommandon**— Följande build-kommandon har tagits bort: `m2-ece-build`, `m2-ece-deploy`, `m2-ece-scd-dump`och ändrat namn `ece-tools docker` kommandon till `ece-docker`. Se [Bakåtkompatibla ändringar](backward-incompatible-changes.md)<!--MAGECLOUD-4392-->

- ![ny ikon](../../assets/new.svg) Borttagen den borttagna `build_options.ini` filen och den tillagda valideringen misslyckas om filen finns. Använd [.magento.env.yaml](../environment/configure-env-yaml.md) fil för att konfigurera byggalternativ.

- ![korrigeringsikon](../../assets/fix.svg) Ett problem som gjorde att byggprocessen misslyckades när `config.php` filen är tom.<!--MAGECLOUD-4127-->

## 2002.0.23

Releasedatum: 27 februari 2020

- ![korrigeringsikon](../../assets/fix.svg) Korrigerat ett kompatibilitetsproblem med `ece-tools` 2002.0.x-versioner som hindrade generering av statiskt innehåll på begäran från att slutföras korrekt i produktionsläge.

## Äldre versioner

Se [arkiv med veringsanteckningar](cloud-release-archive.md) för version 2002.0.22 och tidigare.
