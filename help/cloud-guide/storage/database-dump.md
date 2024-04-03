---
title: Säkerhetskopiera databasen
description: Lär dig hur du använder ECE-verktyg för att skapa en säkerhetskopia av databasen för ett Adobe Commerce om molninfrastrukturprojekt.
feature: Cloud, Iaas, Storage
exl-id: 8a96effe-a587-4edf-b0c7-e73ca8d3b56c
source-git-commit: 4d790bff2ba5d02ef10de5c36a2f0d140e31a407
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Säkerhetskopiera databasen

Du kan skapa en kopia av databasen med `ece-tools db-dump` utan att hämta in alla miljödata från tjänster och berg. Som standard skapar det här kommandot säkerhetskopior i `/app/var/dump-main` katalog för alla databasanslutningar som anges i systemkonfigurationen. Databasdumpåtgärden växlar programmet till underhållsläge, stoppar konsumentköprocesser och inaktiverar cron-jobb innan dumpningen börjar.

Titta på följande riktlinjer för DB-dump:

- För produktionsmiljöer rekommenderar Adobe att du slutför databasdumpoperationer under tider med låg belastning för att minimera driftstörningar som inträffar när platsen är i underhållsläge.
- Om ett fel inträffar under dumpåtgärden tar kommandot bort dumpfilen för att spara diskutrymme. Mer information finns i loggarna (`var/log/cloud.log`).
- I Pro Production-miljöer dumpas det här kommandot endast från _en_ av de tre noderna med hög tillgänglighet, så produktionsdata som skrivs till en annan nod under dumpen kanske inte kopieras. Kommandot genererar en `var/dbdump.lock` för att förhindra att kommandot körs på mer än en nod.
- Adobe rekommenderar att du skapar en [säkerhetskopia](snapshots.md).

Du kan välja att säkerhetskopiera flera databaser genom att lägga till databasnamnen till kommandot. I följande exempel säkerhetskopieras två databaser: `main` och `sales`:

```bash
php vendor/bin/ece-tools db-dump main sales
```

Använd `php vendor/bin/ece-tools db-dump --help` om du vill ha fler alternativ:

- `--dump-directory=<dir>`—Välj en målkatalog för databasdumpen
- `--remove-definers`—Ta bort DEFINER-satser från databasdumpen

**Så här skapar du en databasdump i förproduktionsmiljön eller produktionsmiljön**:

1. [Använd SSH för att logga in eller skapa en tunnel för att ansluta till fjärrmiljön](../development/secure-connections.md) som innehåller den databas som ska kopieras.

1. Visa en lista över miljörelationerna och notera databasinloggningsinformationen.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   eller

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

1. Skapa en säkerhetskopia av databasen. Om du vill välja en målkatalog för databasdumpen använder du `--dump-directory` alternativ.

   ```bash
   php vendor/bin/ece-tools db-dump -- main
   ```

   Exempelsvar:

   ```terminal
   The db-dump operation switches the site to maintenance mode, stops all active cron jobs and consumer queue processes, and disables cron jobs before starting the dump process.
   Your site will not receive any traffic until the operation completes.
   Do you wish to proceed with this process? (y/N)? y
   2020-01-28 16:38:08] INFO: Starting backup.
   [2020-01-28 16:38:08] NOTICE: Enabling Maintenance mode
   [2020-01-28 16:38:10] INFO: Trying to kill running cron jobs and consumers processes
   [2020-01-28 16:38:10] INFO: Running Magento cron and consumers processes were not found.
   [2020-01-28 16:38:10] INFO: Waiting for lock on db dump.
   [2020-01-28 16:38:10] INFO: Start creation DB dump for main database...
   [2020-01-28 16:38:10] INFO: Finished DB dump for main database, it can be found here: /tmp/qxmtlseakof6y/dump-main-1580229490.sql.gz
   [2020-01-28 16:38:10] INFO: Backup completed.
   [2020-01-28 16:38:11] NOTICE: Maintenance mode is disabled.
   ```

1. The `db-dump` skapar ett `dump-<timestamp>.sql.gz` arkivera filen i fjärrprojektkatalogen.

>[!TIP]
>
>Om du vill överföra dessa data till en viss miljö, se [Migrera data och statiska filer](../deploy/staging-production.md#migrate-static-files).
