---
title: Egenskapen Crons
description: Se exempel på hur du konfigurerar egenskapen "crons" i [!DNL Commerce] programkonfigurationsfil.
feature: Cloud, Configuration
exl-id: 67d592c1-2933-4cdf-b4f6-d73cd44b9f59
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 0%

---

# Egenskapen Crons

Adobe Commerce använder `crons` för att schemalägga repetitiva aktiviteter. Det är idealiskt för schemaläggning av en viss uppgift som ska köras vid vissa tidpunkter på dygnet. På grund av skrivskyddade miljöer kan endast ett kroniskt jobb köras åt gången på webbinstansen för Adobe Commerce i molninfrastrukturprojekt. Det är en god rutin att dela upp långvariga uppgifter i mindre uppgifter som ligger i kö. Du kan även skapa en [arbetarinstans](workers-property.md).

Adobe rekommenderar att du kör `crons` som [ägare av filsystem](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html). Gör _not_ run `crons` as `root` eller som webbserveranvändare.

Den här konfigurationen skiljer sig från lokala distributioner av Adobe Commerce, som har flera standardcron-jobb. Se [Konfigurera cron-jobb](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html) i _Konfigurationsguide_.

## Ställ in cron-jobb

The `crons` egenskap beskriver processer som aktiveras enligt ett schema. Varje jobb kräver ett namn och följande alternativ:

- `spec`—Kronuttrycket som används för schemaläggning.
- `cmd`—Det kommando som ska köras på `start` och `stop`.
- `shutdown_timeout`—(_Valfritt_) Om ett cron-jobb avbryts är detta antalet sekunder som en SIGKILL-signal skickas för att stoppa jobbet eller processen. Standardvärdet är 10 sekunder.
- `timeout`—(_Valfritt_) Den längsta tid ett cron-jobb kan köras före timeout. Standardvärdet är det högsta tillåtna värdet 86400 sekunder (24 timmar).

Som standard har varje Commerce Cloud-projekt följande standardvärde `crons` i `.magento.app.yaml` fil:

```yaml
crons:
    cronrun:
        spec: "* * * * *"
        cmd: "php bin/magento cron:run"
```

Om ditt projekt kräver anpassade cron-jobb kan du lägga till dem i standardinställningarna `crons` konfiguration. Se [Bygg ett cron-jobb](#build-a-cron-job).

### `crontab`

Adobe Commerce har lagt till ett konfigurationsalternativ för automatiska kroner endast i Pro-projekt som stöder självbetjäning `crons` konfiguration i mellanlagrings- och produktionsmiljöer. Om det här alternativet är aktiverat kan du använda `crontab` för att granska cron-konfigurationen. Det här är _not_ som är tillgängliga med Starter-projekt.

Du kan använda `crontab` för att granska konfiguration i Pro-projekt, använder inte Adobe Commerce `crontab` för att köra cron-jobb för webbplatser som distribueras i molninfrastrukturen.

**Granska cron-konfigurationen i Pro-miljöer**:

1. Använd [SSH](../development/secure-connections.md#use-an-ssh-command) för att logga in på fjärrmiljön.

1. Visa en lista över schemalagda kroniprocesser.

   ```shell
   crontab -l
   ```

   >[!NOTE]
   >
   >Om `crontab -l` returnerar ett `Command not found` fel måste du [Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) för att aktivera självbetjäningskonfigurationsalternativet för automatiska kroner i ditt Pro-projekt.

I följande exempel visas `crontab` utdata för en miljö som bara har standardvärdet `crons` konfiguration:

```terminal
username@hostname:~$ crontab -l
# Crontab is managed by the system, attempts to edit it directly will fail.
SHELL=/etc/platform/6fck2obu3244c/cron-run
MAILTO=""

# m h  dom mon dow  job_name

* * * * *           cronrun
```

## Bygg ett cron-jobb

Ett cron-jobb innehåller schema- och timingspecifikationen och det kommando som ska köras vid den schemalagda tidpunkten. För Starter-miljöer och Pro `integration` i miljöer är minimiintervallet en gång per fem minuter. För Pro Staging- och Production-miljöer är minimiintervallet en gång per minut. På Adobe Commerce i molninfrastruktur lägger du till anpassade kundvärdesjobb i `.magento.app.yaml` i `crons` -avsnitt. Det allmänna formatet är `spec` för planering och `cmd` för att ange det kommando eller anpassade skript som ska köras.

### Specifikation

Adobe Commerce använder ett femvärdesuttryck för `crons` specifikation (spec): `* * * * *`

1. Minut (0 till 59) För alla Starter- och Pro-miljöer är den minsta frekvens som stöds för kronijobb fem minuter. Du kan behöva konfigurera inställningarna i din administratör.
2. Timme (0 till 23)
3. Dag i månaden (1 till 31)
4. Månad (1 till 12)
5. Veckodag (0 till 6) (söndag till lördag; 7 är också söndag på vissa system)

Några exempel:

- `00 */3 * * *` kör var tredje timme på den första minuten (12:00, 3:00, 6:00)
- `20 */8 * * *` kör var 8:e timme klockan 20 (12:20, 8:20, 4:20)
- `00 00 * * *` kör en gång om dagen vid midnatt
- `00 * * * 1` kör en gång i veckan på måndag vid midnatt.

>[!NOTE]
>
>The `crons` den tid som anges i `.magento.app.yaml` filen baseras på serverns tidszon, inte på den tidszon som anges i lagringskonfigurationsvärdena i databasen.

När du bestämmer schemaläggningen bör du tänka på hur lång tid det tar att slutföra uppgiften. Om du till exempel kör ett jobb var tredje timme och aktiviteten tar 40 minuter att slutföra kan du ändra den schemalagda tidpunkten.

### Kommando

The `cmd` anger det kommando eller anpassade skript som ska köras. Kommandots skriptformat kan innehålla följande:

```text
<path-to-php-binary> <project-dir>/<script-command>
```

Exempel:

```yaml
crons:
    spec: "00 */8 * * *"
    cmd: "/usr/bin/php /app/abc123edf890/bin/magento export:start catalog_category_product"
```

I detta exempel `<path-to-php-binary>` är `/usr/bin/php`. Installationskatalogen som innehåller projekt-ID:t är `/app/abc123edf890/bin/magento`och skriptåtgärden är `export:start catalog_category_product`.

### Lägg till anpassade cron-jobb i ditt projekt

På Adobe Commerce om molninfrastrukturplattform kan du lägga till anpassningar i `crons` i [`.magento.app.yaml`](../application/configure-app-yaml.md) -fil.

>[!NOTE]
>
>För Starter-miljöer och Pro `integration` i miljöer är minimiintervallet en gång per fem minuter. För Pro Staging- och Production-miljöer är minimiintervallet en gång per minut. Du kan inte konfigurera mer frekventa intervall än standardminimumen.

I Adobe Commerce Pro-projekt finns [funktionen för automatiska kroner](#set-up-cron-jobs) måste vara aktiverat i ditt projekt innan du kan lägga till anpassade cron-jobb i förings- och produktionsmiljöer med `.magento.app.yaml` -fil. Om funktionen inte är aktiverad [Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) för att aktivera autocrons.

**Lägga till anpassade cron-jobb**:

1. I den lokala utvecklingsmiljön kan du redigera `.magento.app.yaml` i ADOBE COMMERCE `/app` katalog.

1. I `crons` lägger du till din anpassning med följande format:

   ```yaml
   crons:
       <cron_name_1>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
       <cron_name_2>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
   ```

   I följande exempel `productcatalog` exporterar produktkatalogen var 8:e timme, 20:e minut efter timmen.

   ```yaml
   crons:
       magento:
           spec: '* * * * *'
           cmd: 'php bin/magento cron:run'
       productcatalog:
           spec: '20 */8 * * *'
           cmd: 'bin/magento export:start catalog_product_category'
   ```

1. Lägg till, implementera och push-ändra kod.

   ```bash
   git add .magento.app.yaml && git commit -m "cron config updates" && git push origin <branch-name>
   ```

### Uppdatera cron-jobb

Om du vill lägga till, ta bort eller uppdatera ett anpassat jobb ändrar du konfigurationen i `crons` i `.magento.app.yaml` -fil. Testa sedan uppdateringarna på fjärrkontrollen `integration` miljö innan ändringarna implementeras i förproduktionsmiljö.

## Inaktivera cron-jobb

Du kan inaktivera cron-jobb manuellt innan du slutför underhållsåtgärder som att indexera om eller rensa cachen för att förhindra prestandaproblem. Du kan använda `ece-tools` CLI, kommando `cron:disable` för att inaktivera alla kronjobb och stoppa alla aktiva kronprocesser.

**Så här inaktiverar du cron-jobb**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Använd SSH för att logga in i fjärrmiljön.

   ```bash
   magento-cloud ssh
   ```

1. Inaktivera cron-jobb och stoppa aktiva cron-processer.

   ```shell
   ./vendor/bin/ece-tools cron:disable
   ```

1. När du har slutfört nödvändiga underhållsåtgärder måste du aktivera cron-jobben igen.

   ```shell
   ./vendor/bin/ece-tools cron:enable
   ```

## Felsökning av cron-jobb

Adobe har uppdaterat Adobe Commerce om molninfrastrukturspaket för att optimera kundbearbetningen på Adobe Commerce om molninfrastrukturplattformen och för att åtgärda kronrelaterade problem. Om du får problem med seriebearbetningen bör du kontrollera att projektet använder den senaste versionen av `ece-tools` paket. Se [Uppdatera ECE-verktyg](../dev-tools/update-package.md).

Du kan granska information om cron processing i loggfiler på programnivå för varje miljö. Se [Programloggar](../test/log-locations.md#application-logs).

Se följande Adobe Commerce supportartiklar för hjälp med felsökning av kronrelaterade problem:

- [Kravuppgifter låser uppgifter från andra grupper](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-tasks-lock-tasks-from-other-groups.html)

- [Återställ fastnade cron-jobb manuellt i molnet](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/reset-stuck-magento-cron-jobs-manually-on-cloud.html)
