---
title: Distribuera till mellanlagring och produktion
description: Lär dig hur du distribuerar din Adobe Commerce på molninfrastrukturkod till miljöer för stapling och produktion för ytterligare testning.
feature: Cloud, Console, Deploy, SCD, Storage
exl-id: 4b82289f-ee04-4b14-a0ed-7a8a19fc6a6a
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 0%

---

# Distribuera till mellanlagring och produktion

Processen för att distribuera och publicera börjar med utveckling, fortsätter till Förproduktion och slutar med att publicera i Produktion. Adobe är en totallösning för hela miljön som ger enhetliga konfigurationer. Alla miljöer har stöd för direkt URL-åtkomst till butiken och administratörs- och SSH-åtkomst för CLI-kommandon.

När du är redo att distribuera din butik måste du slutföra distributionen och testningen i mellanlagringsmiljön innan du distribuerar till Production. I det här avsnittet finns detaljerade anvisningar och information om bygg- och distributionsprocessen, migrering av data och innehåll samt testning.

>[!TIP]
>
>Adobe rekommenderar att du skapar en [säkerhetskopia](../storage/snapshots.md) av miljön före driftsättning.

Du kan även aktivera [Spåra driftsättningar med New Relic](../monitor/track-deployments.md) för att övervaka distributionshändelser och hjälpa er att analysera prestanda mellan distributioner.

## Startdistributionsflöde

Adobe rekommenderar att du skapar en `staging` förgrening från `master` för att ge bästa möjliga stöd för utveckling och driftsättning av Starter-planer. Sedan har du två av fyra aktiva miljöer: `master` för produktion och `staging` för mellanlagring.

Detaljerad information om processen finns i [Arbetsflöde för att utveckla och distribuera](../architecture/starter-develop-deploy-workflow.md).

## Driftsättningsflöde

Pro har en stor integrationsmiljö med två aktiva grenar, en global `master` filialer, förproduktionsavdelningar och produktionsavdelningar. När du skapar ditt projekt är koden redo att förgrena, utveckla och pusha för att bygga och driftsätta din webbplats. Även om integreringsmiljön kan ha många grenar har Förproduktion och Produktion bara en gren för varje miljö.

Detaljerad information om processen finns i [Arbetsflöde för utveckling och distribution av Pro](../architecture/pro-develop-deploy-workflow.md).

## Distribuera kod till mellanlagring

I mellanlagringsmiljön finns en nästan produktionsmiljö som innehåller en databas, webbserver och alla tjänster, inklusive Fastly och New Relic. Du kan pusha, sammanfoga och distribuera via [[!DNL Cloud Console]](../project/overview.md) eller [CLI-kommandon i molnet](../dev-tools/cloud-cli-overview.md) via en terminalapplikation.

### Distribuera kod med [!DNL Cloud Console]

The [!DNL Cloud Console] innehåller funktioner för att skapa, hantera och distribuera kod i integrerings-, mellanlagrings- och produktionsmiljöer för Starter- och Pro-planer.

**För Pro-projekt distribuerar du integreringsgrenen till mellanlagring**:

1. [Logga in](https://accounts.magento.cloud) till ditt projekt.
1. Välj `integration` gren.
1. Välj **Sammanfoga** möjlighet att distribuera till mellanlagring.

   ![Sammanfoga](../../assets/button-merge.png){width="150"}

1. Slutför alla [testning](../test/staging-and-production.md) i mellanlagringsmiljön.
1. När mellanlagring är klar väljer du **Sammanfoga** möjlighet att distribuera till produktion.

**Distribuera utvecklingsgrenen till mellanlagring för Starter**:

1. [Logga in](https://accounts.magento.cloud) till ditt projekt.
1. Välj den förberedda kodgrenen.
1. Välj **Sammanfoga** möjlighet att distribuera till mellanlagring.

   ![Sammanfoga](../../assets/button-merge.png){width="150"}

1. Slutför alla [testning](../test/staging-and-production.md) i mellanlagringsmiljön.
1. När mellanlagring är klar väljer du **Sammanfoga** möjlighet att distribuera till produktion (`master`).

### Distribuera kod med kommandoraden

Cloud CLI innehåller kommandon för att distribuera kod. Du behöver SSH- och Git-åtkomst till ditt projekt.

#### Steg 1: Distribuera och testa integreringsmiljön

1. När du har loggat in i projektet ska du ta en titt på integreringsmiljön:

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

1. Synkronisera den lokala integreringsmiljön med fjärrmiljön:

   ```bash
   magento-cloud environment:synchronize <environment-ID>
   ```

1. Skapa en ögonblicksbild av miljön som en säkerhetskopia:

   ```bash
   magento-cloud snapshot: create -e <environment-ID>
   ```

1. Uppdatera kod i din lokala gren efter behov.

1. Lägg till, implementera och skicka ändringar till miljön.

   ```bash
   git add -A && git commit -m "Commit message" && git push origin <environment-ID>
   ```

1. Komplett testning.

#### Steg 2: Sammanfoga ändringar i Förproduktion och distribuera

1. Ta en titt på Mellanlagringsmiljön:

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

1. Synkronisera din lokala mellanlagringsmiljö med fjärrmiljön:

   ```bash
   magento-cloud environment:synchronize <environment-ID>
   ```

1. Skapa en ögonblicksbild av miljön som en säkerhetskopia:

   ```bash
   magento-cloud snapshot: create -e <environment-ID>
   ```

1. Koppla integreringsmiljön till mellanlagring för att distribuera:

   ```bash
   magento-cloud environment:merge <integration-ID>
   ```

1. Komplett testning.

#### Steg 3: Distribuera till produktion

1. Kolla in, synkronisera och skapa en ögonblicksbild av din lokala produktionsmiljö.

1. Koppla mellanlagringsmiljön till produktionen för att distribuera:

   ```bash
   magento-cloud environment:merge <staging-ID>
   ```

1. Komplett testning.

## Migrera statiska filer

[Statiska filer](https://experienceleague.adobe.com/docs/commerce-operations/operational-playbook/glossary.html) lagras i `mounts`. Det finns två metoder för att migrera filer från en källmonteringsplats, till exempel din lokala miljö, till en målmonteringsplats. Båda metoderna använder `rsync` men Adobe rekommenderar att du använder `magento-cloud` CLI för att flytta filer mellan den lokala miljön och fjärrmiljön. Och Adobe rekommenderar att du använder `rsync` när du flyttar filer från en fjärrkälla till en annan fjärrplats.

### Migrera filer med CLI

Du kan använda `mount:upload` och `mount:download` CLI-kommandon för att migrera filer mellan den lokala miljön och fjärrmiljön. Båda kommandona använder `rsync` men CLI-kommandona innehåller alternativ och instruktioner som är anpassade till Adobe Commerce i molninfrastrukturmiljö. Om du till exempel använder det enkla kommandot utan alternativ uppmanas du att välja vilka monteringar som ska laddas upp eller laddas ned.

```bash
magento-cloud mount:download
```

Exempelsvar:

```terminal
Enter a number to choose a mount to download from:
  [0] app/etc
  [1] pub/static
  [2] var
  [3] pub/media
  [4] All mounts
 > 3

Target directory: ~/pub/media/

Downloading files from the remote mount pub/media to pub/media

Are you sure you want to continue? [Y/n] Y
```

**Så här överför du filer från en lokal `pub/media/` mapp till fjärrmappen `pub/media/` mapp för den aktuella miljön**:

```bash
magento-cloud mount:upload --source /path/to/project/pub/media/ --mount pub/media/
```

Exempelsvar:

```terminal
Uploading files from pub/media to the remote mount pub/media

Are you sure you want to continue? [Y/n] Y

  building file list ...   done
  ./
  sample-file.jpeg

  sent 8.43K bytes  received 48 bytes  3.39K bytes/sec
  total size is 154.57K  speedup is 18.23
```

Använd `--help` för `mount:upload` och `mount:download` om du vill se fler alternativ. Det finns till exempel en `--delete` för att ta bort överflödiga filer under migreringen.

### Migrera filer med hjälp av synkronisering

Du kan också använda `rsync` verktyg för att migrera filer.

```bash
rsync -azvP <source> <destination>
```

Det här kommandot använder följande alternativ:

- `a`-archive
- `z`-komprimera filer under migreringen
- `v`-verbose
- `P`-delvis förlopp

Se [rsync](https://linux.die.net/man/1/rsync) hjälp.

>[!NOTE]
>
>Om du vill överföra media direkt från fjärr-till-fjärrmiljöer måste du aktivera vidarebefordran av SSH-agenten, se [GitHub-vägledning](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding).

**Migrera statiska filer från fjärrmiljöer till fjärrmiljöer direkt (snabb hantering)**:

1. Använd SSH för att logga in i källmiljön. Använd inte `magento-cloud` CLI. Använda `-A` Alternativet är viktigt eftersom det möjliggör vidarebefordran av autentiseringsagentanslutningen.

   >[!TIP]
   >
   >För att hitta **SSH-åtkomst** länk i [!DNL Cloud Console], väljer miljö och klickar på **Åtkomstplats**.

   ```bash
   ssh -A <environment_ssh_link@ssh.region.magento.cloud>
   ```

1. Använd `rsync` för att kopiera `pub/media` från källmiljön till en annan fjärrmiljö.

   ```bash
   rsync -azvP pub/media/ <destination_environment_ssh_link@ssh.region.magento.cloud>:pub/media/
   ```

1. Logga in på den andra fjärrmiljön för att verifiera att filerna har migrerats.

## Migrera databasen

>[!WARNING]
>
>Det kan ta lång tid att importera och exportera databaser, vilket kan påverka webbplatsens prestanda och tillgänglighet. Schemalägg import- och exportåtgärder under tider med låg belastning för att förhindra långsamma prestanda eller avbrott på produktionsplatser.

>[!BEGINSHADEBOX]

**Krav:** En databasdump (se steg 3) bör innehålla databasutlösare. Bekräfta att du har [UTLÖSARprivilegium](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html#priv_trigger).

>[!IMPORTANT]
>
>Integreringsmiljödatabasen är endast till för utvecklingstestning och kan innehålla data som du inte vill migrera till Förproduktion och Produktion.

För kontinuerlig integration, Adobe **rekommenderar inte** migrera data från integrering till förproduktion och produktion. Du kan skicka testdata eller skriva över viktiga data. Alla viktiga konfigurationer skickas med [konfigurationsfil](../store/store-settings.md) och `setup:upgrade` under bygge och driftsättning.

>[!ENDSHADEBOX]

Adobe **rekommenderas** migrera data från produktion till mellanlagring för att testa webbplatsen och lagra den i en nära produktionsmiljö med alla tjänster och inställningar.

>[!NOTE]
>
>Om du vill överföra media från fjärr-till-fjärrmiljöer direkt måste du aktivera vidarebefordran av Ssh Agent finns i [GitHub-vägledning](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding).

### Säkerhetskopiera databasen

Det är en god vana att skapa en säkerhetskopia av databasen. Följande procedur använder vägledningen från [Säkerhetskopiera databasen](../storage/database-dump.md).

**Så här dumpar du databasen**:

1. [Använd SSH för att logga in på fjärrmiljön](../development/secure-connections.md#use-an-ssh-command) som innehåller den databas som ska kopieras.

1. Visa en lista över miljörelationerna och notera databasinloggningsinformationen.

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

   För Pro Staging and Production heter databasen i `MAGENTO_CLOUD_RELATIONSHIPS` variabel (vanligtvis samma som programnamnet och användarnamnet).

1. Skapa en säkerhetskopia av databasen. Om du vill välja en målkatalog för databasdumpen använder du `--dump-directory` alternativ.

   För Starter-miljöer och Pro-integreringsmiljöer använder du `main` som databasens namn:

   ```bash
   php vendor/bin/ece-tools db-dump main
   ```

   Dumpa alternativ:
   - `--dump-directory=<dir>`—Välj en målkatalog för databasdumpen
   - `--remove-definers`—Ta bort DEFINER-satser från databasdumpen

1. Även om metoden ECE-Tools är att föredra är en annan metod att skapa en databasdumpfil med hjälp av MySQL i GZIP-format.

   ```bash
   mysqldump -h <database-host> --user=<database-username> --password=<password> --single-transaction --triggers <database-name> | gzip - > /tmp/database.sql.gz
   ```

   Om du har konfigurerat tvåfaktorsautentisering i målmiljön är det bättre att exkludera relaterade 2FA-tabeller för att undvika att konfigurera om den efter databasmigrering:

   ```bash
   mysqldump -h <database-host> --user=<database-username> --password=<password> --single-transaction --triggers --ignore-table=<database-name>.tfa_user_config --ignore-table=<database-name>.tfa_country_codes <database-name> | gzip - > /tmp/database.sql.gz
   ```

1. Typ `logout` för att avsluta SSH-anslutningen.

### Släpp och återskapa databasen

När du importerar data måste du släppa och skapa en databas.

**Så här släpper och återskapar du databasen**:

1. Upprätta en [SSH-tunnel](../development/secure-connections.md#ssh-tunneling) till fjärrmiljön.

1. Anslut till databastjänsten.

   ```bash
   mysql --host=127.0.0.1 --user='<database-username>' --pass='<user-password>' --database='<name>' --port='<port>'
   ```

1. På `MariaDB [main]>` släpper du databasen.

   För integrering med Starter och Pro:

   ```shell
   drop database main;
   ```

   För produktion:

   ```shell
   drop database <cluster-id>;
   ```

   För mellanlagring:

   ```shell
   drop database <cluster-ID_stg>;
   ```

1. Återskapa databasen.

   För integrering med Starter och Pro:

   ```shell
   create database main;
   ```

   Import för produktion:

   ```shell
   zcat <cluster-ID>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <database-username> <database-name>;
   ```

   Import för mellanlagring:

   ```shell
   zcat <cluster-ID_stg>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <database-username> <database-name>;
   ```
