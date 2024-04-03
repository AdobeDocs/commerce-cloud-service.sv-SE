---
title: Skapa variabler
description: Se en lista över miljövariabler som styr åtgärder i Adobe Commerce när det gäller byggfasen av molninfrastruktur.
feature: Cloud, Configuration, Build, SCD, Upgrade
recommendations: noDisplay, catalog
role: Developer
exl-id: 243aaa45-a5ef-4ed2-8800-3d0f07bf3740
source-git-commit: 7b9c6a4cd17069c25455195bd8f273664b8a29eb
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# Skapa variabler

Följande _bygg_ variabelkontrollåtgärder i byggfasen och kan ärva och åsidosätta värden från [Globala variabler](variables-global.md). Infoga dessa variabler i `build` i `.magento.env.yaml` fil:

```yaml
stage:
  build:
    BUILD_VARIABLE_NAME: value
```

Mer information om hur du anpassar bygg- och distributionsprocessen:

- [Distributionskonfiguration](configure-env-yaml.md)
- [Distributionsprocess](../deploy/process.md)

Följande variabler togs bort i v2.2:

- `skip_di_clearing`
- `skip_di_compilation`

## `ERROR_REPORT_DIR_NESTING_LEVEL`

- **Standard**—`1`
- **Version**—Adobe Commerce 2.1.4 och senare

Ange nivån för katalogkapsling för att spara felrapportfiler för att undvika att fylla i rapportkatalogen med tiotusentals filer, vilket kan göra det svårt att hantera och granska data. Den här inställningen är som standard `1`. Normalt behöver du inte ändra standardvärdet om du inte har problem med att hantera felrapportfiler i `<magento_root>/var/report/` katalog.

```yaml
stage:
  build:
    ERROR_REPORT_DIR_NESTING_LEVEL: 2
```

## `QUALITY_PATCHES`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Ange en lista över Adobe Commerce-kvalitetsuppdateringar som ska användas under distributionen.

```yaml
stage:
  build:
    QUALITY_PATCHES: [ ]
```

I följande exempel anges tre korrigeringar som ska användas under distributionen.

```yaml
stage:
  build:
    QUALITY_PATCHES:
      - MC-31387
      - MDVA-4567
      - MC-456345
```

Se [Tillämpa patchar](../development/apply-patches.md).

## `SCD_COMPRESSION_LEVEL`

- **Standard**—`6`
- **Version**—Adobe Commerce 2.1.4 och senare

Anger vilken [gzip](https://www.gnu.org/software/gzip) komprimeringsnivå (`0` till `9`) som ska användas vid komprimering av statiskt innehåll, `0` inaktiverar komprimering.

```yaml
stage:
  build:
    SCD_COMPRESSION_LEVEL: 4
```

## `SCD_COMPRESSION_TIMEOUT`

- **Standard**—`600`
- **Version**—Adobe Commerce 2.1.4 och senare

När den tid det tar att komprimera de statiska resurserna överskrider tidsgränsen för komprimering avbryts distributionsprocessen. Ange den maximala körningstiden i sekunder för det statiska kommandot för innehållskomprimering.

```yaml
stage:
  build:
    SCD_COMPRESSION_TIMEOUT: 800
```

## `SCD_NO_PARENT`

- **Standard**—`false`
- **Version**—Adobe Commerce 2.4.2 och senare

Ange till `true` för att förhindra att statiskt innehåll genereras för överordnade teman under byggfasen.

Ange `SCD_NO_PARENT: false` under byggfasen så att genereringen av statiskt innehåll för de överordnade temana inte påverkar webbplatsens driftsättning eller orsakar onödiga driftavbrott. Se [Statisk innehållsdistribution](../deploy/static-content.md).

```yaml
stage:
  build:
    SCD_NO_PARENT: false
```

## `SCD_MATRIX`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Du kan konfigurera flera språkinställningar per tema. Den här anpassningen snabbar upp byggprocessen genom att minska antalet onödiga temafiler. Du kan till exempel skapa _magento/backend_ tema på engelska och ett anpassat tema på andra språk.

Följande exempel bygger `Magento/backend` tema med tre språkområden:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

I följande exempel byggs tre teman med tre språkområden:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
      "Magento/blank":
        language:
          - en_US
          - fr_FR
          - af_ZA
      "Magento/luma":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

Eller så kan du välja att _not_ distribuera ett tema:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend": [ ]
```

## `SCD_MAX_EXECUTION_TIME`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.2.0 och senare

Gör att du kan öka den maximala förväntade körningstiden för statisk innehållsdistribution.

Som standard sätter Adobe Commerce i molninfrastrukturen den maximala förväntade körningen till 900 sekunder, men i vissa fall behöver du mer tid för att slutföra den statiska innehållsdistributionen för ett Cloud-projekt.

```yaml
stage:
  build:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_STRATEGY`

- **Standard**—`quick`
- **Version**—Adobe Commerce 2.2.0 och senare

Anpassa [distributionsstrategi](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy.html) för statiskt innehåll. Se [Distribuera statiska vyfiler](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html).

Använd dessa alternativ _endast_ om du har fler än ett språk:

- `standard`—distribuerar alla statiska vyfiler för alla paket.
- `quick`—(_standard_) minimerar driftsättningstiden.
- `compact`—sparar diskutrymme på servern. I Adobe Commerce version 2.2.4 och tidigare åsidosätter den här inställningen värdet för `scd_threads` med värdet `1`.

```yaml
stage:
  build:
    SCD_STRATEGY: "compact"
```

## `SCD_THREADS`

- **Standard**—Automatisk
- **Version**—Adobe Commerce 2.1.4 och senare

Anger antalet trådar för distribution av statiskt innehåll. Standardvärdet baseras på antalet CPU-tråd som identifierats och överstiger inte värdet 4. Om du ökar antalet trådar går det snabbare att distribuera statiskt innehåll, och om du minskar antalet trådar blir det långsammare. Du kan ange ett trådvärde, till exempel:

```yaml
stage:
  build:
    SCD_THREADS: 2
```

Om du vill minska driftsättningstiden ytterligare använder du [Konfigurationshantering](../store/store-settings.md) med `scd-dump` för att flytta statisk distribution till byggfasen.

## `SCD_USE_BALER`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.3.0 och senare

[Balare](https://github.com/magento/baler) skannar den genererade JavaScript-koden och skapar ett optimerat JavaScript-paket. Genom att distribuera det optimerade paketet till din webbplats kan du minska antalet nätverksförfrågningar när du läser in webbplatsen och förbättra sidinläsningstiden.

Ange till `true` för att köra Baler efter att ha implementerat statiskt innehåll.

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>Eftersom Baler är i alfaversion bör du inte använda det i produktionsmiljöer.

## `SKIP_COMPOSER_DUMP_AUTOLOAD`

- **Standard**— _Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Ange till `true` för att hoppa över `composer dump-autoload` under en installation av Cloud Docker. Den här variabeln gäller endast för Cloud Docker-behållare med skrivbara filsystem. Om du hoppar över kommandot förhindras i så fall fel från andra kommandon som försöker få åtkomst till kod från de borttagna `generated` katalog.

När Adobe Commerce körs `composer dump-autoload`skapas automatiskt inläsningsfiler med länkar till genererade klasser i `generated` -mapp, vilket inte är något problem i produktionsmiljöer med skrivskyddade filsystem. För installation av Cloud Docker med skrivbara filsystem (skapas endast för testning och utveckling med `./vendor/bin/ece-docker build:compose --with-test`) kan du köra `bin/magento -n setup:upgrade` utan `--keep-generated` som tar bort `generated` katalog. Om katalogen tas bort visas `composer dump-autoload` kommandot misslyckas eftersom den automatiska inläsningen innehåller länkar till filer i den borttagna katalogen.

```yaml
stage:
  build:
    SKIP_COMPOSER_DUMP_AUTOLOAD: true
```

## `SKIP_SCD`

- **Standard**— _Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Ange till `true` för att hoppa över statisk innehållsdistribution under byggfasen.

Om du redan distribuerar statiskt innehåll under byggfasen med [Konfigurationshantering](../store/store-settings.md)kan du hoppa över statisk innehållsdistribution för att snabbt testa byggprocessen.

Under byggfasen anger du `SKIP_SCD: false` så att det statiska innehållet byggs under byggfasen där processen inte påverkar webbplatsens driftsättning eller orsakar onödiga driftavbrott. Se [Statisk innehållsdistribution](../deploy/static-content.md).

```yaml
stage:
  build:
    SKIP_SCD: false
```

## `VERBOSE_COMMANDS`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Aktivera eller inaktivera [Symfony](https://symfony.com/doc/current/console/verbosity.html) felsökningsnivå för `bin/magento` CLI-kommandon som utförs under distributionsfasen.

>[!NOTE]
>
>Använd VERBOSE_COMMANDS för att styra detaljerna i kommandoutdata för både lyckade och misslyckade `bin/magento` CLI-kommandon måste du ange [MIN_LOGGING_LEVEL](variables-global.md#minlogginglevel) `debug`.

Välj detaljnivå i loggarna:

- `-v`= normal utskrift
- `-vv`= mer utförlig utskrift
- `-vvv` = utförlig utskrift idealisk för felsökning

```yaml
stage:
  build:
    VERBOSE_COMMANDS: "-vv"
```
