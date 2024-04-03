---
title: Konfigurera miljö
description: Lär dig hur du konfigurerar bygg- och distributionsåtgärder i alla Commerce för molninfrastrukturmiljöer, inklusive Pro Staging och Production, med hjälp av miljövariabler.
feature: Cloud, Build, Configuration, Deploy, SCD
role: Developer
exl-id: 66e257e2-1eca-4af5-9b56-01348341400b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# Konfigurera miljövariabler för distribution

The `.magento.env.yaml` -filen använder miljövariabler för att centralisera hanteringen av bygg- och distributionsåtgärder i alla dina miljöer, inklusive Pro Staging och Production. Om du vill konfigurera unika åtgärder i varje miljö måste du ändra den här filen i varje miljö.

>[!TIP]
>
>YAML-filer är skiftlägeskänsliga och tillåter inte tabbar. Var noga med att använda konsekvent indrag i hela `.magento.env.yaml` filen eller konfigurationen kanske inte fungerar som förväntat. Exemplen i dokumentationen och i exempelfilen använder _två blanksteg_ indrag. Använd [ece-tools validate, kommando](#validate-configuration-file) för att kontrollera konfigurationen.

## Filstruktur

The `.magento.env.yaml` filen innehåller två avsnitt: `stage` och `log`. The `stage` -avsnittet kontrollerar åtgärder som utförs under faserna i [Driftsättningsprocess i molnet](../deploy/process.md).

- `stage`—Använd scenavsnittet för att definiera vissa åtgärder för följande distributionssteg:
   - `global`—Styr åtgärder i både bygg-, distributions- och efterdriftfaserna. Du kan åsidosätta dessa inställningar i avsnitten för att skapa, distribuera och efterdistribuera.
   - `build`—Kontrollerar endast åtgärder i byggfasen. Om du inte anger några inställningar i det här avsnittet, kommer byggfasen att använda inställningar från det globala avsnittet.
   - `deploy`—Kontrollerar endast åtgärder i distributionsfasen. Om du inte anger inställningar i det här avsnittet används inställningarna från det globala avsnittet i distributionsfasen.
   - `post-deploy`—Kontrollerar åtgärder _efter_ driftsätta ditt program och _efter_ behållaren accepterar anslutningar.
- `log`—Konfigurera med loggavsnittet [meddelanden](set-up-notifications.md), inklusive meddelandetyper och detaljnivå.
   - `slack`—Konfigurera ett meddelande som ska skickas till en robot från Slack.
   - `email`- Konfigurera ett e-postmeddelande som ska skickas till en eller flera e-postmottagare.
   - [logghanterare](log-handlers.md)- Konfigurera maskinvaru- och programmeddelanden som skickas till en fjärrloggningsserver.

### Miljövariabler

The `ece-tools` paket anger värden i `env.php` fil baserad på värden från [Molnvariabler](variables-cloud.md), variabler som anges i [!DNL Cloud Console]och `.magento.env.yaml` konfigurationsfil. Miljövariablerna i `.magento.env.yaml` anpassa molnmiljön genom att åsidosätta din befintliga Commerce-konfiguration. Om ett standardvärde är `Not Set`och sedan `ece-tools` paket **NEJ** och använder [!DNL Commerce] standard eller värdet från MAGENTO_CLOUD_RELATIONSHIPS-konfigurationen. Om standardvärdet är inställt visas `ece-tools` paketet fungerar för att ange den standardinställningen.

Följande avsnitt innehåller detaljerade definitioner, t.ex. om ett standardvärde har angetts eller inte, av alla variabler som du kan använda i `.magento.env.yaml` fil:

- [Global](variables-global.md)—variabelkontrollåtgärder i varje fas: skapa, distribuera och efterdistribuera
- [Bygge](variables-build.md)—variabelkontrollbygge
- [Distribuera](variables-deploy.md)—variabelstyrningsdistributionsåtgärder
- [Efter driftsättning](variables-post-deploy.md)—variabelkontrollåtgärder efter distributionen

### Skapa konfigurationsfil från CLI

Du kan generera en `.magento.env.yaml` konfigurationsfil för en molnmiljö med följande `ece-tools` kommandon.

>Skapar en konfigurationsfil

```bash
php ./vendor/bin/ece-tools cloud:config:create `<configuration-json>`
```

>Uppdatera värden i konfigurationsfilen

```bash
php ./vendor/bin/ece-tools cloud:config:update `<configuration-json>`
```

Båda kommandona kräver ett enda argument: en JSON-formaterad array som anger ett värde för minst en variabel för build, deploy eller post-deploy. Följande kommando anger till exempel värden för `SCD_THREADS` och `CLEAN_STATIC_FILES` variabler:

```bash
php vendor/bin/ece-tools cloud:config:create '{"stage":{"build":{"SCD_THREADS":5}, "deploy":{"CLEAN_STATIC_FILES":false}}}'
```

Och skapar `.magento.env.yaml` fil med följande inställningar:

```yaml
stage:
  build:
    SCD_THREADS: 5
  deploy:
    CLEAN_STATIC_FILES: false
```

Du kan använda `cloud:config:update` för att uppdatera den nya filen. Följande kommando ändrar till exempel `SCD_THREADS` värdet och lägger till `SCD_COMPRESSION_TIMEOUT` konfiguration:

```bash
php vendor/bin/ece-tools cloud:config:update '{"stage":{"build":{"SCD_THREADS":3, "SCD_COMPRESSION_TIMEOUT":1000}}}'
```

Den uppdaterade filen innehåller följande konfiguration:

```yaml
stage:
  build:
    SCD_THREADS: 3
    SCD_COMPRESSION_TIMEOUT: 1000
  deploy:
    CLEAN_STATIC_FILES: false
```

### Verifiera konfigurationsfil

Använd följande `ece-tools` för att validera `.magento.env.yaml` konfigurationsfilen innan ändringar skickas till fjärrmolnmiljön.

```bash
php ./vendor/bin/ece-tools cloud:config:validate
```

Följande exempelsvar innehåller en lista med objekt som ska korrigeras:

```terminal
Environment configuration is not valid. Correct the following items in your .magento.env.yaml file:
The SCD_THREADS variable contains an invalid value of type string. Use the following type: integer.
The SCD_STRATEGY variable contains an invalid value fast. Use one of the available value options: compact, quick, standard.
The NOT_EXIST_OPTION variable is not allowed in configuration.
```

## PHP-konstanter

Du kan använda PHP-konstanter i `.magento.env.yaml` fildefinitioner i stället för hårdkodade värden. I följande exempel definieras `driver_options` med en PHP-konstant:

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      connection:
        default:
          driver_options:
            !php/const:\PDO::MYSQL_ATTR_LOCAL_INFILE : 1
        indexer:
          driver_options:
            !php/const:\PDO::MYSQL_ATTR_LOCAL_INFILE : 1
      _merge: true
```

>[!WARNING]
>
>Konstantparsning fungerar inte när en `symfony/yaml` tidigare än 3.2.

## Felhantering

När ett fel inträffar på grund av ett oväntat värde i `.magento.env.yaml` konfigurationsfilen får du ett felmeddelande. I följande felmeddelande visas en lista med föreslagna ändringar av varje objekt med ett oväntat värde, som ibland innehåller giltiga alternativ:

```terminal
- Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:
  Item CRON_CONSUMERS_RUNNER is not supposed to be in stage build. Please move it to one of possible stages: global, deploy
  Item SKIP_SCD has unexpected type string. Please use one of next types: boolean
  Item VERBOSE_COMMANDS has unexpected type boolean. Please use one of next types: string
  Item SKIP_HTML_MINIFICATION has unexpected type string. Please use one of next types: boolean
  Item CRON_CONSUMERS_RUNNER has unexpected type boolean. Please use one of next types: array
  Item VAR_WARM_UP_PAGES is not allowed in configuration.
  Item WARM_UP_PAGES has unexpected type string. Please use one of next types: array
```

Gör eventuella korrigeringar, implementera och skicka ändringarna vidare. Om du inte får något felmeddelande godkänns valideringen av ändringarna i konfigurationsfilen.

## Optimering av konfigurationshantering

Om du har aktiverat Configuration Management efter att ha dumpat konfigurationerna, bör du flytta SCD_*-variablerna från distributionen till byggfasen. Se [Strategier för distribution av statiskt innehåll](../deploy/static-content.md).

>Före konfigurationshantering:

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
    REDIS_USE_SLAVE_CONNECTION: 1
```

>När du har aktiverat Configuration Management flyttar du SCD_*-variablerna till byggfasen:

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    REDIS_USE_SLAVE_CONNECTION: 1
  build:
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
```
