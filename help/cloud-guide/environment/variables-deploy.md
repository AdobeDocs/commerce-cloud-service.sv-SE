---
title: Distribuera variabler
description: Se en lista över miljövariabler som styr åtgärder i Adobe Commerce för driftsättningsfasen av molninfrastrukturen.
feature: Cloud, Configuration, Cache, Deploy, SCD, Storage, Search
recommendations: noDisplay, catalog
role: Developer
exl-id: 673880b5-830b-4837-ac0c-5fa5643ae34c
source-git-commit: b7307faf046884c13cba852df69d4fa9977e9a17
workflow-type: tm+mt
source-wordcount: '2185'
ht-degree: 0%

---

# Distribuera variabler

Följande _driftsätta_ variabelkontrollåtgärder i distributionsfasen och kan ärva och åsidosätta värden från [Globala variabler](variables-global.md). Infoga dessa variabler i `deploy` i `.magento.env.yaml` fil:

```yaml
stage:
  deploy:
    DEPLOY_VARIABLE_NAME: value
```

Mer information om hur du anpassar bygg- och distributionsprocessen:

- [Distributionskonfiguration](configure-env-yaml.md)
- [Distributionsprocess](../deploy/process.md)

## `CACHE_CONFIGURATION`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Konfigurera Redis-sida och standardcachning. När du anger `cm_cache_backend_redis` -parametern måste du ange `server`, `port`och `database` alternativ.

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      frontend:
        default:
          backend: file
        page_cache:
          backend: file
```

{{merge-options}}

I följande exempel sammanfogas nya värden med en befintlig konfiguration:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          backend_options:
            database: 10
        page_cache:
          backend_options:
            database: 11
```

I följande exempel används [Förinläsningsfunktion för Redis](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/redis-pg-cache.html#redis-preload-feature) enligt definitionen i _Konfigurationsguide_:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          id_prefix: '061_'
          backend_options:
            preload_keys:
              - '061_EAV_ENTITY_TYPES:hash'
              - '061_GLOBAL_PLUGIN_LIST:hash'
              - '061_DB_IS_UP_TO_DATE:hash'
              - '061_SYSTEM_DEFAULT:hash'
```

Använda en anpassad [REDIS_BACKEND](#redis_backend) modell (inte bara från tillåtelselista), ange `_custom_redis_backend` alternativ till `true` för att aktivera korrekt validering som i följande exempel:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      frontend:
        default:
          _custom_redis_backend: true
          backend: '\CustomRedisModel'
```

## `CLEAN_STATIC_FILES`

- **Standard**—`true`
- **Version**—Adobe Commerce 2.1.4 och senare

Aktiverar eller inaktiverar rengöring [statiska innehållsfiler](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html) genereras under bygg- eller distributionsfasen. Använd standardvärdet _true_ i utvecklingen som en god praxis.

- **`true`**—Tar bort allt befintligt statiskt innehåll innan det uppdaterade statiska innehållet distribueras.
- **`false`**—Distributionen skriver bara över befintliga statiska innehållsfiler om det genererade innehållet innehåller en nyare version.

Om du ändrar statiskt innehåll genom en separat process anger du värdet till _false_.

```yaml
stage:
  deploy:
    CLEAN_STATIC_FILES: false
```

Om du inte rensar statiska vyfiler innan du distribuerar dem kan det orsaka problem om du distribuerar uppdateringar till befintliga filer utan att ta bort tidigare versioner. Av [statisk filreserv](https://developer.adobe.com/commerce/frontend-core/guide/caching/#clean-static-files-cache) regler kan reservåtgärder visa fel fil om katalogen innehåller flera versioner av samma fil.

## `CRON_CONSUMERS_RUNNER`

- **Standard**—`cron_run = false`, `max_messages = 1000`
- **Version**—Adobe Commerce 2.2.0 och senare

Använd den här miljövariabeln för att bekräfta att meddelandeköer körs efter en distribution.

- `cron_run`—Ett booleskt värde som aktiverar eller inaktiverar `consumers_runner` cron-jobb (standard = `false`).
- `max_messages`—Ett tal som anger det maximala antalet meddelanden som varje konsument måste behandla innan det avbryts (standard = `1000`). Du kan ställa in värdet på `0` för att förhindra konsumenten från att säga upp sig.
- `consumers`—En array med strängar som anger vilka konsumenter som ska köras. En tom array körs _alla_ konsumenter.

- `multiple_processes`-Ett tal som anger antalet processer som ska anges för varje kund. Stöds i Commerce **2.4.4** eller större.

>[!NOTE]
>
>Returnera en lista med meddelandekön `consumers`, kör `./bin/magento queue:consumers:list` i fjärrmiljön.

Exempelarray som kör en specifik `consumers` och `multiple_processes` för varje konsument

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers:
        - example_consumer_1
        - example_consumer_2
-     multiple_processes:
        example_consumer_1: 4
        example_consumer_2: 3
```

Exempel på en tom array som kör alla `consumers`:

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers: []
```

Som standard skriver distributionsprocessen över alla inställningar i `env.php` -fil. Se [Hantera meddelandeköer](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/manage-message-queues.html) i _Handbok för Commerce Configuration_ för lokal Adobe Commerce.

## `CONSUMERS_WAIT_FOR_MAX_MESSAGES`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.2.0 och senare

Konfigurera hur `consumers` bearbeta meddelanden från meddelandekön genom att välja något av följande alternativ:

- `false`—`Consumers` bearbeta tillgängliga meddelanden i kön, stänga TCP-anslutningen och avsluta. `Consumers` väntar inte på att fler meddelanden ska komma in i kön, även om antalet bearbetade meddelanden är mindre än `max_messages` det värde som anges i `CRON_CONSUMERS_RUNNER` distributionsvariabel.

- `true`—`Consumers` fortsätta bearbeta meddelanden från meddelandekön tills maximalt antal meddelanden har uppnåtts (`max_messages`) som anges i `CRON_CONSUMERS_RUNNER` distribuera variabeln innan TCP-anslutningen stängs och konsumentprocessen avslutas. Om kön töms innan den når `max_messages`, väntar konsumenten på fler meddelanden.

>[!WARNING]
>
>Om du använder arbetare för att köra `consumers` I stället för att använda ett cron-jobb anger du variabeln till true.

```yaml
stage:
  deploy:
    CONSUMERS_WAIT_FOR_MAX_MESSAGES: false
```

## `CRYPT_KEY`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

>[!WARNING]
>
>Ange `CRYPT_KEY` genom [!DNL Cloud Console] i stället för `.magento.env.yaml` för att undvika att visa nyckeln i källkodsdatabasen för din miljö. Se [Ange miljö- och projektvariabler](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html#configure-environment).

När du flyttar databasen från en miljö till en annan utan någon installationsprocess behöver du motsvarande kryptografisk information. Adobe Commerce använder det krypteringsnyckelvärde som anges i [!DNL Cloud Console] som `crypt/key` värdet i `env.php` -fil.

## `DATABASE_CONFIGURATION`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Om du definierade en databas i [relationship, egenskap](../application/properties.md#relationships) i `.magento.app.yaml` kan du anpassa databasanslutningarna för distribution.

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_value'
```

{{merge-options}}

I följande exempel sammanfogas nya värden med en befintlig konfiguration:

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_new_value'
      _merge: true
```

Du kan också konfigurera ett tabellprefix.

>[!WARNING]
>
>Om du inte använder sammanslagningsalternativet med tabellprefixet måste du ange standardanslutningsinställningar, annars misslyckas distributionen.

I följande exempel används `ece_` tabellprefix med standardanslutningsinställningar i stället för att använda `_merge` alternativ:

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      connection:
        default:
          username: user
          host: host
          dbname: magento
          password: password
      table_prefix: 'ece_'
```

Exempel:

```terminal
MariaDB [main]> SHOW TABLES;
+-------------------------------------+
| Tables_in_main                      |
+-------------------------------------+
| ece_admin_passwords                 |
| ece_admin_system_messages           |
| ece_admin_user                      |
| ece_admin_user_session              |
| ece_adminnotification_inbox         |
| ece_amazon_customer                 |
| ece_authorization_rule              |
| ece_cache                           |
| ece_cache_tag                       |
| ece_captcha_log                     |
...
```

## `ELASTICSUITE_CONFIGURATION`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.2.0 och senare

Behåller anpassade [!DNL Elastic Suite] tjänstinställningar mellan distributioner och använder dem i avsnittet &#39;system/default/Le_elasticsuite_core_base_settings&#39; i huvudprogrammet [!DNL Elastic Suite] konfiguration. Om [!DNL Elastic Suite] dispositionspaketet installeras, det konfigureras automatiskt.

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      es_client:
        servers: 'remote-host:9200'
      indices_settings:
        number_of_shards: 1
        number_of_replicas: 0
```

{{merge-options}}

I följande exempel sammanfogas ett nytt värde med den befintliga konfigurationen:

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      indices_settings:
        number_of_shards: 3
        number_of_replicas: 2
      _merge: true
```

**Kända begränsningar**:

- Ändra sökmotorn till någon annan typ än `elasticsuite` orsakar ett distributionsfel som följs av ett lämpligt valideringsfel
- Om du tar bort tjänsten Elasticsearch uppstår ett distributionsfel som följs av ett lämpligt valideringsfel

>[!NOTE]
>
>Mer information om hur du använder eller felsöker [!DNL Elastic Suite] plugin-program med Adobe Commerce, se [[!DNL Elastic Suite] dokumentation](https://github.com/Smile-SA/elasticsuite).

## `ENABLE_GOOGLE_ANALYTICS`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.1.4 och senare

Aktiverar och inaktiverar Google Analytics vid distribuering till miljöer för förproduktion och integrering. Som standard gäller Google Analytics endast för produktionsmiljön. Ange det här värdet till `true` för att aktivera Google Analytics i mellanlagrings- och integreringsmiljöer.

- **`true`**—Aktiverar Google Analytics i mellanlagrings- och integreringsmiljöer.
- **`false`**—Inaktiverar Google Analytics i mellanlagrings- och integreringsmiljöer.

Lägg till `ENABLE_GOOGLE_ANALYTICS` miljövariabel till `deploy` scenen i `.magento.env.yaml` fil:

```yaml
stage:
  deploy:
    ENABLE_GOOGLE_ANALYTICS: true
```

>[!NOTE]
>
>Distributionsprocessen aktiverar alltid Google Analytics i produktionsmiljöer.

## `FORCE_UPDATE_URLS`

- **Standard**—`true`
- **Version**—Adobe Commerce 2.1.4 och senare

Vid distribution till Pro eller Starter Staging and Production-miljöer ersätter den här variabeln Adobe Commerce base URL:er i databasen med de projekt-URL:er som anges av [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) variabel. Använd den här inställningen för att åsidosätta standardbeteendet för [UPDATE_URLS](#update_urls) driftsättningsvariabel, som ignoreras vid driftsättning i mellanlagrings- eller produktionsmiljöer.

```yaml
stage:
  deploy:
    FORCE_UPDATE_URLS: true
```

## `LOCK_PROVIDER`

- **Standard**—`file`
- **Version**—Adobe Commerce 2.2.5 och senare

Lås-providern förhindrar att duplicerade cron-jobb och cron-grupper startas. Använd `file` låsleverantör i produktionsmiljön. Startmiljöer och den professionella integreringsmiljön använder inte [MAGENTO_CLOUD_LOCKS_DIR](variables-cloud.md) variabel, so `ece-tools` använder `db` låsningsprovider automatiskt.

```yaml
stage:
  deploy:
    LOCK_PROVIDER: "db"
```

Se [Konfigurera låset](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/lock-provider.html) i _Installationsguide_.

## `MYSQL_USE_SLAVE_CONNECTION`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.1.4 och senare

>[!TIP]
>
>The `MYSQL_USE_SLAVE_CONNECTION` variabeln stöds bara i Adobe Commerce i molninfrastrukturerna Staging och Production Pro och stöds inte i Starter-projekt.

Adobe Commerce kan läsa flera databaser asynkront. Ange till `true` att automatiskt använda _skrivskyddad_ anslutning till databasen för att ta emot skrivskyddad trafik på en icke-huvudnod. Den här anslutningen förbättrar prestanda genom belastningsutjämning, eftersom bara en nod hanterar läs- och skrivtrafik. Ange till `false` om du vill ta bort en befintlig skrivskyddad anslutningsmatris från `env.php` -fil.

```yaml
stage:
  deploy:
    MYSQL_USE_SLAVE_CONNECTION: true
```

När `MYSQL_USE_SLAVE_CONNECTION` variabeln är inställd på `true`, `synchronous_replication` parametern är inställd på `true` som standard i `env.php` på Pro Staging and Production-miljöer. När `MYSQL_USE_SLAVE_CONNECTION` är inställd på `false`, `synchronous_replication` parametern är inte konfigurerad.

## `QUEUE_CONFIGURATION`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Använd den här systemvariabeln för att behålla anpassade AMQP-tjänstinställningar mellan distributioner. Om du till exempel föredrar att använda en befintlig meddelandekötjänst i stället för att förlita dig på molninfrastrukturen för att skapa den åt dig använder du `QUEUE_CONFIGURATION` systemvariabel för att ansluta den till din plats:

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      amqp:
        host: test.host
        port: 1234
      amqp2:
        host: test.host2
        port: 12345
      mq:
        host: mq.host
        port: 1234
```

{{merge-options}}

I följande exempel sammanfogas nya värden med en befintlig konfiguration:

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      _merge: true
      amqp:
        host: changed1.host
        port: 5672
      amqp2:
        host: changed2.host2
        port: 12345
      mq:
        host: changedmq.host
        port: 1234
```

## `REDIS_BACKEND`

- **Standard**—`Cm_Cache_Backend_Redis`
- **Version**—Adobe Commerce 2.3.0 och senare

Anger serverdelsmodellens konfiguration för Redis-cachen.

Adobe Commerce version 2.3.0 och senare innehåller följande backend-modeller:

- `Cm_Cache_Backend_Redis`
- `\Magento\Framework\Cache\Backend\Redis`
- `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache`

Exemplet med hur du anger `REDIS_BACKEND`

```yaml
stage:
  deploy:
    REDIS_BACKEND: '\Magento\Framework\Cache\Backend\RemoteSynchronizedCache'
```

>[!NOTE]
>
>Om du anger `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache` som Redis backend-modell för att aktivera [L2-cache](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html), `ece-tools` skapar cachekonfigurationen automatiskt. Se ett exempel [konfigurationsfil](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html#configuration-example) i _Konfigurationshandbok för Adobe Commerce_. Använd [CACHE_CONFIGURATION](#cache_configuration) distributionsvariabel.

## `REDIS_USE_SLAVE_CONNECTION`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.1.16 och senare

>[!WARNING]
>
>Gör _not_ aktivera variabeln på en [skalad arkitektur](../architecture/scaled-architecture.md) projekt. Det orsakar Redis-anslutningsfel. Redis-slavar är fortfarande aktiva men används inte för Redis-läsningar. Adobe rekommenderar att du använder Adobe Commerce 2.3.5 eller senare, implementerar en ny Redis-backend-konfiguration och implementerar L2-cachning för Redis.

>[!TIP]
>
>The `REDIS_USE_SLAVE_CONNECTION` variabeln stöds bara i Adobe Commerce i molninfrastrukturerna Staging och Production Pro och stöds inte i Starter-projekt.

Adobe Commerce kan läsa flera Redis-instanser asynkront. Ange till `true` att automatiskt använda _skrivskyddad_ anslutning till en Redis-instans för att ta emot skrivskyddad trafik på en icke-huvudnod. Den här anslutningen förbättrar prestanda genom belastningsutjämning, eftersom bara en nod hanterar läs- och skrivtrafik. Ange till `false` om du vill ta bort en befintlig skrivskyddad anslutningsmatris från `env.php` -fil.

```yaml
stage:
  deploy:
    REDIS_USE_SLAVE_CONNECTION: true
```

Du måste ha en Redis-tjänst konfigurerad i `.magento.app.yaml` -filen och i `services.yaml` -fil.

[ECE-verktyg version 2002.0.18](../release-notes/cloud-release-archive.md#v2002018) och senare använder mer feltoleranta inställningar. Om Adobe Commerce inte kan läsa data från Redis _slav_ -instans, sedan läses data från Redis _master_ -instans.

Den skrivskyddade anslutningen kan inte användas i integreringsmiljön eller om du använder [`CACHE_CONFIGURATION` variabel](#cache_configuration).

## `RESOURCE_CONFIGURATION`

- **Standard**—Inte inställd
- **Version**—Adobe Commerce 2.1.4 och senare

Kopplar ett resursnamn till en databasanslutning. Den här konfigurationen motsvarar `resource` i `env.php` -fil.

{{merge-options}}

I följande exempel sammanfogas nya värden med en befintlig konfiguration:

```yaml
stage:
  deploy:
    RESOURCE_CONFIGURATION:
      _merge: true
      default_setup:
        connection: default
```

## `SCD_COMPRESSION_LEVEL`

- **Standard**—`4`
- **Version**—Adobe Commerce 2.1.4 och senare

Anger vilken [gzip](https://www.gnu.org/software/gzip) komprimeringsnivå (`0` till `9`) som ska användas vid komprimering av statiskt innehåll, `0` inaktiverar komprimering.

```yaml
stage:
  deploy:
    SCD_COMPRESSION_LEVEL: 5
```

## `SCD_COMPRESSION_TIMEOUT`

- **Standard**—`600`
- **Version**—Adobe Commerce 2.1.4 och senare

När den tid det tar att komprimera de statiska resurserna överskrider tidsgränsen för komprimering avbryts distributionsprocessen. Ange den maximala körningstiden i sekunder för det statiska kommandot för innehållskomprimering.

```yaml
stage:
  deploy:
    SCD_COMPRESSION_TIMEOUT: 800
```

## `SCD_MATRIX`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Du kan konfigurera flera språkinställningar per tema. Den här anpassningen snabbar upp distributionsprocessen genom att minska antalet onödiga temafiler. Du kan till exempel distribuera _magento/backend_ tema på engelska och ett anpassat tema på andra språk.

I följande exempel distribueras `Magento/backend` tema med tre språkområden:

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

Du kan också välja att _not_ distribuera ett tema:

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend": [ ]
```

## `SCD_MAX_EXECUTION_TIME`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.2.0 och senare

Gör att du kan öka den maximala förväntade körningstiden för statisk innehållsdistribution.

Som standard sätter Adobe Commerce den maximala förväntade körningen till 900 sekunder, men i vissa fall behöver du mer tid för att slutföra distributionen av statiskt innehåll för ett Cloud-projekt.

```yaml
stage:
  deploy:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.4.2 och senare

Under distributionsfasen anger du `SCD_NO_PARENT: true` så att det statiska innehållet för överordnade teman inte genereras under distributionsfasen. Den här inställningen minimerar driftsättningstiden och förhindrar driftstopp som kan inträffa om det statiska innehållet inte kan byggas under distributionen. Se [Statisk innehållsdistribution](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SCD_NO_PARENT: true
```

## `SCD_STRATEGY`

- **Standard**—`quick`
- **Version**—Adobe Commerce 2.2.0 och senare

Här kan du anpassa [distributionsstrategi](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy.html) för statiskt innehåll. Se [Distribuera statiska vyfiler](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

Använd dessa alternativ _endast_ om du har fler än ett språk:

- `standard`—distribuerar alla statiska vyfiler för alla paket.
- `quick`—(_standard_) minimerar driftsättningstiden.
- `compact`—sparar diskutrymme på servern. I Adobe Commerce version 2.2.4 och tidigare åsidosätter den här inställningen värdet för `scd_threads` med värdet `1`.

```yaml
stage:
  deploy:
    SCD_STRATEGY: "compact"
```

## `SCD_THREADS`

- **Standard**—Automatisk
- **Version**—Adobe Commerce 2.1.4 och senare

Anger antalet trådar för distribution av statiskt innehåll. Standardvärdet baseras på antalet CPU-tråd som identifierats och överstiger inte värdet 4. Om du ökar antalet trådar går det snabbare att distribuera statiskt innehåll, och om du minskar antalet trådar blir det långsammare. Du kan ange ett trådvärde, till exempel:

```yaml
stage:
  deploy:
    SCD_THREADS: 2
```

Om du vill minska driftsättningstiden ytterligare använder du [Konfigurationshantering](../store/store-settings.md) med `scd-dump` för att flytta statisk distribution till byggfasen.

## `SEARCH_CONFIGURATION`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Använd den här systemvariabeln för att behålla anpassade inställningar för söktjänsten mellan distributioner. Exempel:

Elasticsearch-konfiguration:

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: elasticsearch
      elasticsearch_server_hostname: http://elasticsearch.internal
      elasticsearch_server_port: '9200'
      elasticsearch_index_prefix: magento2
      elasticsearch_server_timeout: '15'
```

OpenSearch-konfiguration (för Commerce 2.4.6 och senare):

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: opensearch
      opensearch_server_hostname: 'http://opensearch.internal'
      opensearch_server_port: '9200'
      opensearch_index_prefix: 'magento2'
      opensearch_server_timeout: '15'
```

{{merge-options}}

I följande exempel sammanfogas ett nytt värde med den befintliga konfigurationen:

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: elasticsearch
      elasticsearch_server_port: '9200'
      _merge: true
```

## `SESSION_CONFIGURATION`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Konfigurera Redis-sessionslagring. Kräver `save`, `redis`, `host`, `port`och `database` alternativ för sessionslagringsvariabeln. Exempel:

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      redis:
        bot_first_lifetime: 100
        bot_lifetime: 10001
        database: 0
        disable_locking: 1
        host: redis.internal
        max_concurrency: 10
        max_lifetime: 10001
        min_lifetime: 100
        port: 6379
      save: redis
```

{{merge-options}}

I följande exempel sammanfogas ett nytt värde med den befintliga konfigurationen:

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      _merge: true
      redis:
        max_concurrency: 10
```

## `SKIP_SCD`

- **Standard**— _Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Ange till `true` för att hoppa över statisk innehållsdistribution under distributionsfasen.

Under distributionsfasen anger du `SKIP_SCD: true` så att det statiska innehållsbygget inte inträffar under distributionsfasen. Den här inställningen minimerar driftsättningstiden och förhindrar driftstopp som kan inträffa om det statiska innehållet inte kan byggas under distributionen. Se [Statisk innehållsdistribution](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SKIP_SCD: true
```

## `UPDATE_URLS`

- **Standard**—`true`
- **Version**—Adobe Commerce 2.1.4 och senare

Ersätt Adobe Commerce bas-URL:er i databasen med de projekt-URL:er som anges av [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) variabel. Den här konfigurationen är användbar för lokal utveckling, där bas-URL:er har konfigurerats för din lokala miljö. När du distribuerar till en molnmiljö uppdateras URL:erna så att du kan komma åt din butik och administratör via projektets URL:er.

Om du måste uppdatera URL:er när du distribuerar till Pro- eller Starter Staging- och Production-miljöer använder du [`FORCE_UPDATE_URLS`](#force_update_urls) variabel.

```yaml
stage:
  deploy:
    UPDATE_URLS: false
```

## `VERBOSE_COMMANDS`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Aktivera eller inaktivera [Symfony](https://symfony.com/doc/current/console/verbosity.html) felsökningsnivå för `bin/magento` CLI-kommandon som utförs under distributionsfasen.

>[!NOTE]
>
>Använd inställningen VERBOSE_COMMANDS för att styra detaljerna i kommandoutdata för både lyckad och misslyckad `bin/magento` CLI-kommandon måste du ange [MIN_LOGGING_LEVEL](variables-global.md#minlogginglevel) `debug`.

Välj detaljnivå i loggarna:

- `-v`= normal utskrift
- `-vv`= mer utförlig utskrift
- `-vvv` = utförlig utskrift idealisk för felsökning

```yaml
stage:
  deploy:
    VERBOSE_COMMANDS: "-vv"
```
