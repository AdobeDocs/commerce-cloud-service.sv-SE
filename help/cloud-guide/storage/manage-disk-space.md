---
title: Hantera diskutrymme
description: Lär dig hur du hanterar diskutrymme med hjälp av kommandoradsgränssnittet.
feature: Cloud, Storage
exl-id: 480cb33b-ac83-441d-946e-5b4de09ad84e
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 0%

---

# Hantera diskutrymme

Du kan hitta den totala lagringskapaciteten för ditt Cloud-projekt i ditt Adobe Commerce på molninfrastrukturkontrakt och på din [kontosida](https://accounts.magento.cloud/user). Varje projektkort i ditt konto visar antalet _miljöer_, _lagring_ kapaciteten i GB och antalet _användare_. Du kan också använda följande molnkommando:

```bash
magento-cloud subscription:info | grep storage
```

Exempelsvar:

```terminal
| storage              | 51200
```

När en Pro-produktion eller staging-miljö når eller överskrider 95 % av lagringskapaciteten utlöser verktyget för övervakning av molninfrastruktur en supportvarning som meddelar dig om en automatisk ökning av lagringskapaciteten.

Exempelmeddelande:

>[!BEGINSHADEBOX]

_&quot;Vår övervakning har upptäckt att fillagringen i ditt kluster (projekt-id-miljö) börjar bli full. Diskanvändningen är för närvarande på en kritisk användningsnivå med mindre än 1 GiB kvar. Den delade lagringsvolymen håller på att uppgraderas från 60 GiB till 70 GiB för att hålla tjänsterna igång. Ta en titt på hur produktions- och mellanlagringsfilerna används för att se om du kan frigöra utrymme.&quot;_

>[!ENDSHADEBOX]

>[!TIP]
>
>Vi rekommenderar att du regelbundet övervakar din lagringskapacitet och underhåller den väl under 90 % för att undvika dessa automatiska ökningar. Lagringsökningen för Pro-testning och -produktion kan inte återställas när den har tilldelats.

## Kontrollera integreringsmiljön

Du kan kontrollera hur mycket diskutrymme som används i integreringsmiljön med `magento-cloud` CLI.

**Kontrollera ungefärlig användning av diskutrymme**:

```bash
magento-cloud db:size
```

Exempelsvar:

```terminal
Checking database service mysql...

+----------------+-----------------+--------+
| Allocated disk | Estimated usage | % used |
+----------------+-----------------+--------+
| 2.0 GiB        | 193.3 MiB       | ~ 9%   |
+----------------+-----------------+--------+
```

Alla monteringar delar en skiva. Du kan kontrollera hur mycket diskutrymme som används för montering med `magento-cloud` CLI.

**Kontrollera ungefärlig diskanvändning för mängder**:

```bash
magento-cloud mount:size
```

Exempelsvar:

```terminal
Checking disk usage for all mounts on <project>-<environment>-mymagento@ssh.us.magento.cloud...

+------------+-----------+---------+-----------+-----------+--------+
| Mount(s)   | Size(s)   | Disk    | Used      | Available | % Used |
+------------+-----------+---------+-----------+-----------+--------+
| app/etc    | 184 KiB   | 1.9 GiB | 481.3 MiB | 1.4 GiB   | 24.7%  |
| pub/media  | 128 KiB   |         |           |           |        |
| pub/static | 158.2 MiB |         |           |           |        |
| var        | 316.7 MiB |         |           |           |        |
+------------+-----------+---------+-----------+-----------+--------+
```

## Kontrollera dedikerade kluster

För Pro Staging- och Production-miljöer kan du kontrollera hur mycket diskutrymme som används i varje miljö med `disk free` som anger hur mycket diskutrymme som används i filsystemet. Du måste använda SSH för att logga in i en fjärrmiljö.

```bash
df -h
```

The `-h` visar rapporten i ett läsbart format (KB, MB eller GB).

I följande exempelsvar `/mnt/shared` mängden visar diskutrymme för media och `/data/mysql/` mängd visar diskutrymme för databasen:

```terminal
Filesystem                                    Size  Used Avail Use% Mounted on
udev                                           16G     0   16G   0% /dev
tmpfs                                         3.2G  9.1M  3.2G   1% /run
/dev/xvda1                                     59G  8.9G   48G  16% /
tmpfs                                          16G   36K   16G   1% /dev/shm
tmpfs                                         5.0M     0  5.0M   0% /run/lock
tmpfs                                          16G     0   16G   0% /sys/fs/cgroup
/dev/xvdj                                     9.8G  2.3G  7.6G  23% /data/mysql
/dev/xvdi                                     9.8G  491M  9.3G   5% /data/exports
192.168.5.5:/shared                           9.8G  591M  9.3G   6% /mnt/shared
/dev/loop0                                     91M   91M     0 100% /app/project
192.168.5.5:/shared/project/var         9.8G  591M  9.3G   6% /app/project/var
192.168.5.5:/shared/project/app/etc     9.8G  591M  9.3G   6% /app/project/app/etc
192.168.5.5:/shared/project/pub/media   9.8G  591M  9.3G   6% /app/project/pub/media
192.168.5.5:/shared/project/pub/static  9.8G  591M  9.3G   6% /app/project/pub/static
```

Du kan begränsa svaret genom att ange en katalog. Exempel:

```bash
df -h var/
```

Exempelsvar:

```terminal
Filesystem                                    Size  Used Avail Use% Mounted on
192.168.5.5:/shared/project/var         9.8G  591M  9.3G   6% /app/project/var
```

## Allokera diskutrymme

Två [konfigurationsfiler](../environment/overview.md) styra allokeringen av diskutrymme i molnmiljöer: `.magento.app.yaml` -filen och `.magento/services.yaml` -fil. Varje fil innehåller `disk` som definierar diskstorleksvärdet i MB för respektive konfiguration. Du kan bara ändra diskutrymme för Pro-integrering och Starter-miljöer.

>[!IMPORTANT]
>
>För proffsproduktions- och mellanlagringsmiljöer måste du [Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om du vill ändra diskutrymme. En storleksökning av Pro Production- och Staging-miljöerna kan endast utföras med vissa intervall, så beroende på hur mycket diskutrymme du använder kan stödet rekommendera att du ökar diskutrymmet med minst 10 GB. Lagringsökningen för Pro-testning och -produktion kan inte återställas när den har tilldelats.

### Programdiskutrymme

The `.magento.app.yaml` -filen styr [beständigt diskutrymme](../application/properties.md#disk) som är tillgängliga för programmet.

**Öka programmets diskutrymme**:

1. I den lokala utvecklingsmiljön öppnar du `.magento.app.yaml` konfigurationsfil.

1. Ange ett nytt värde för `disk` (i MB).

   ```yaml
   disk: <value-mb>
   ```

1. Spara ändringarna i filen.

1. Lägg till, implementera och push-överföra kodändringar.

   ```bash
   git add .magento.app.yaml && git commit -m "Increase disk space for application" && git push origin <branch-name>
   ```

   Ändringarna börjar gälla när du har överfört den uppdaterade YAML-filen till fjärrmiljön.

### Tjänstdiskutrymme

The `.magento/services.yaml` -filen kontrollerar vilket diskutrymme som är tillgängligt för varje tjänst, till exempel MySQL och Redis.

**Öka diskutrymmet för en tjänst**:

1. I den lokala utvecklingsmiljön öppnar du `.magento/services.yaml` konfigurationsfil.

1. Lägg till eller hitta en tjänst i filen. Se [mer om hur du konfigurerar tjänster](../services/services-yaml.md).

1. Ange ett nytt värde för diskegenskapen (i MB).

   ```yaml
   <name>:
       type: <service-name>:<service-version>
       disk: <value-mb>
   ```

1. Spara ändringarna i filen.

1. Lägg till, implementera och push-överföra kodändringar.

   ```bash
   git add .magento/services.yaml && git commit -m "Increase disk space for service" && git push origin <branch-name>
   ```

   Ändringarna börjar gälla när du har överfört den uppdaterade YAML-filen till fjärrmiljön.

## Övervaka diskutrymme

I Pro Production-miljöer kan du övervaka diskutrymme och andra prestandaindikatorer med hjälp av varningspolicyn för Adobe Commerce för New Relic. Mer information finns i [Övervaka prestanda med hanterade aviseringar](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts). Mer information finns i [Bästa tillvägagångssätt för att lösa databasprestandaproblem](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html).

## Inget utrymme kvar

Build-cachen kan växa med tiden. Om du får en varning om lägen `No space left on device`, försök rensa byggcachen och omdistribuera:

```bash
magento-cloud project:clear-build-cache
```
