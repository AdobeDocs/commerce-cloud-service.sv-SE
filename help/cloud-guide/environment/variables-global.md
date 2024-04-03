---
title: Globala variabler
description: Se en lista med miljövariabler som styr åtgärder i Adobe Commerce för driftsättning av molninfrastruktur.
feature: Cloud, Configuration, Build, Deploy, Eventing, Logs, SCD
recommendations: noDisplay, catalog
role: Developer
exl-id: 04c2861d-746d-42d4-a678-f6c7b464eb51
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Globala variabler

Globala variabelkontrollåtgärder för varje fas av [!DNL Commerce] driftsättningsprocess: bygga, driftsätta och efterdriftsätta. Eftersom globala variabler påverkar varje fas måste du ange dem i `global` i `.magento.env.yaml` fil:

```yaml
stage:
  global:
    GLOBAL_VARIABLE_NAME: value
```

Mer information om hur du anpassar bygg- och distributionsprocessen:

- [Distributionskonfiguration](configure-env-yaml.md)
- [Distributionsprocess](../deploy/process.md)

## `ENABLE_EVENTING`

- **Standard**-_Ej angiven_
- **Version**—Adobe Commerce 2.4.5 och senare

När inställt på `true`, gör att cron kan köra användare i meddelandekön. Adobe I/O Events för Adobe Commerce använder meddelandeköer för att snabba upp leveransen av viktiga händelser.

Adobe rekommenderar att du också lägger till [`CRON_CONSUMERS_RUNNER`](./variables-deploy.md#cron_consumers_runner) variabeln till `deploy` i `.magento.env.yaml` fil med `cron_run` ange till `true`.

I följande exempel visas en fullständigt konfigurerad `ENABLE_EVENTING` variabel.

```yaml
stage:
  global:
    ENABLE_EVENTING: true
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 0
      consumers: []
```

## ENABLE_WEBHOOKS

- **Standard**-_Ej angiven_
- **Version**—Adobe Commerce 2.4.4 och senare

När inställt på `true`, aktiverar Commerce-webhooks. Webbhoten körs på en extern slutpunkt, till exempel en App Builder-körningsåtgärd eller ett lagerhanteringssystem från tredje part. The [_Webhooks Guide_](https://developer.adobe.com/commerce/extensibility/webhooks) beskriver den här funktionen i detalj.

```yaml
stage:
  global:
    ENABLE_WEBHOOKS: true
```

## `MIN_LOGGING_LEVEL`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Åsidosätter den lägsta loggningsnivån för alla utdataströmmar utan att ändra koden, vilket hjälper vid felsökning av problem med distributionen. Om distributionen misslyckas kan du använda den här variabeln för att öka loggningsgranulariteten globalt. Se [Loggnivåer](log-handlers.md#log-levels). The `min_level` värdet i Logging-hanterare skriver över den här inställningen.

```yaml
stage:
  global:
    MIN_LOGGING_LEVEL: debug
```

>[!WARNING]
>
>Inställningen för `MIN_LOGGING_LEVEL` variabeln ändrar inte loggnivåkonfigurationen för filhanteraren, som är inställd på `debug` som standard.

## `SCD_ON_DEMAND`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Aktivera generering av statiskt innehåll när en användare begär det (SCD). Statiskt innehåll on demand är idealiskt för utvecklings- och testarbetsflöden eftersom det minskar driftsättningstiden.

Läs in cacheminnet i förväg med [`post_deploy` krok](../application/hooks-property.md) minskar driftstoppen. Cachevärmaren är bara tillgänglig för Pro-projekt som innehåller miljöer för stapling och produktion i [!DNL Cloud Console] och för Starter-projekt. Lägg till `SCD_ON_DEMAND` miljövariabel till `global` scenen i `.magento.env.yaml` fil:

```yaml
stage:
  global:
    SCD_ON_DEMAND: true
```

The `SCD_ON_DEMAND` -variabeln hoppar över SCD i båda faserna (skapa och distribuera), rensar `pub/static` och `var/view_preprocessed` och skriver följande till `app/etc/env.php` fil:

```php?start_inline=1
return array(
   ...
   'static_content_on_demand_in_production' => 1,
   ...
);
```

## `SCD_MAX_EXECUTION_TIME`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.2.0 och senare

Gör att du kan öka den maximala förväntade körningstiden för statisk innehållsdistribution.

Som standard sätter Adobe Commerce den maximala förväntade körningen till 900 sekunder, men i vissa fall behöver du mer tid för att slutföra distributionen av statiskt innehåll för ett Cloud-projekt.

```yaml
stage:
  global:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.4.2 och senare

Ange till `true` för att förhindra att statiskt innehåll genereras för överordnade teman under bygg- och distributionsfaserna. När det här alternativet är inställt på `true`, genereras mindre statiskt innehåll, vilket förbättrar genererings- och driftsättningstiden.

```yaml
stage:
  global:
    SCD_NO_PARENT: true
```

## `SCD_USE_BALER`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.3.0 och senare

[Balare](https://github.com/magento/baler) är en modul som skannar den genererade JavaScript-koden och skapar ett optimerat JavaScript-paket. Genom att distribuera det optimerade paketet till din webbplats kan du minska antalet nätverksförfrågningar när du läser in webbplatsen och förbättra sidinläsningstiden.

Ange till `true` för att köra Baler efter att ha implementerat statiskt innehåll.

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>Installera och konfigurera Baler-modulen innan du använder den här funktionen. Eftersom Balans är i alfaversion kan du bara aktivera det här alternativet i mellanlagringsmiljöer.

## `SKIP_HTML_MINIFICATION`

- **Standard**:
   - `true`—for `ece-tools` 2002.0.13 och senare
   - `false`—för tidigare versioner av `ece-tools`
- **Version**—Adobe Commerce 2.1.4 och senare

Aktiverar eller inaktiverar kopiering av statiska vyfiler till `<magento_root>/init/` i slutet av byggfasen. Om inställt på `true`, filer kopieras inte och miniatyrbilder för HTML är tillgängliga på begäran. Ange det här värdet till `true` för att minska driftstoppen vid driftsättning i förproduktionsmiljöer och produktionsmiljöer.

- **`false`**—Kopierar `view_preprocessed` till `<magento_root>/init/` i slutet av byggfasen och återställer katalogen i `<magento_root>/var` katalog i början av distributionsfasen.
- **`true`**—Aktiverar on-demand-minification; gör _not_ kopiera `<magento_root>var/view_preprocessed` till `<magento_root>/init/` i slutet av byggfasen.

Lägg till `SKIP_HTML_MINIFICATION` miljövariabel till `global` scenen i `.magento.env.yaml` fil:

```yaml
stage:
  global:
    SKIP_HTML_MINIFICATION: true
```

## `X_FRAME_CONFIGURATION`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Använd `X_FRAME_CONFIGURATION` variabel för att ändra [`X-Frame-Options`](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/security/xframe-options.html) huvudkonfiguration för din Adobe Commerce-webbplats. Den här konfigurationen styr hur webbläsaren återger en sida i en `<frame>`, `<iframe>`, eller `<object>`. Använd något av följande alternativ:

- `DENY`—Det går inte att visa sidan i en ram.
- `SAMEORIGIN`—(Standardinställningen för Adobe Commerce.) Sidan kan bara visas i en ram med samma ursprung som sidan.

>[!WARNING]
>
>The `ALLOW-FROM <uri>` eftersom webbläsare som stöds av Adobe Commerce inte längre stöder det. Se [Webbläsarkompatibilitet](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options#Browser_compatibility).

Lägg till `X_FRAME_CONFIGURATION` miljövariabel till `global` scenen i `.magento.env.yaml` fil:

```yaml
stage:
  global:
    X_FRAME_CONFIGURATION: SAMEORIGIN
```
