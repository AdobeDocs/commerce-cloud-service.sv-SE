---
title: Konfigurera tjänster
description: Lär dig hur du konfigurerar tjänster som används av Adobe Commerce i molninfrastruktur.
feature: Cloud, Configuration, Services
exl-id: 48091c10-c53f-4aad-afbe-b4516653bda1
source-git-commit: 4d790bff2ba5d02ef10de5c36a2f0d140e31a407
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Konfigurera tjänster

The `services.yaml` filen definierar de tjänster som stöds och används av Adobe Commerce i molninfrastruktur, som MySQL, Redis och Elasticsearch eller OpenSearch. Du behöver inte prenumerera på externa tjänsteleverantörer. Den här filen finns i `.magento` projektkatalog.

Distributionsskriptet använder konfigurationsfilerna i `.magento` katalog för att tillhandahålla miljön med de konfigurerade tjänsterna. En tjänst blir tillgänglig för ditt program om den ingår i [`relationships`](../application/properties.md#relationships) egenskapen för `.magento.app.yaml` -fil. The `services.yaml` filen innehåller _type_ och _disk_ värden. Tjänsttypen definierar tjänsten _name_ och _version_.

Om du ändrar en tjänstkonfiguration tillhandahålls miljön med de uppdaterade tjänsterna, vilket påverkar följande miljöer:

- Alla startmiljöer inklusive Production `master`
- Integreringsmiljöer för Pro

{{pro-update-service}}

## Standardtjänster och tjänster som stöds

Molninfrastrukturen stöder och distribuerar följande tjänster:

- [MySQL](mysql.md)
- [Redis](redis.md)
- [RabbitMQ](rabbitmq.md)
- [Elasticsearch](elasticsearch.md)
- [OpenSearch](opensearch.md)

Du kan visa standardversioner och diskvärden i den aktuella, [standard `services.yaml` fil](https://github.com/magento/magento-cloud/blob/master/.magento/services.yaml). I följande exempel visas `mysql`, `redis`, `opensearch` eller `elasticsearch`och `rabbitmq` tjänster som definieras i `services.yaml` konfigurationsfil:

```yaml
mysql:
    type: mysql:10.4
    disk: 5120

redis:
    type: redis:6.2

opensearch:
    type: opensearch:2  # minor version not required; uses latest
    disk: 1024

rabbitmq:
    type: rabbitmq:3.9
    disk: 1024
```

## Tjänstvärden

Du måste ange tjänstens ID och tjänsttypskonfigurationen `type: <name>:<version>`. Om tjänsten använder beständig lagring måste du ange ett diskvärde.

Använd följande format:

```yaml
<service-id>:
    type: <name>:<version>
    disk: <value-MB>
```

### `service-id`

The `service-id` värde identifierar tjänsten i projektet. Du kan bara använda gemena alfanumeriska tecken: `a` till `z` och `0` till `9`, till exempel `redis`.

Detta _service-id_ värdet används i [`relationships`](../application/properties.md#relationships) egenskapen för `.magento.app.yaml` konfigurationsfil:

```yaml
relationships:
    redis: "<name>:redis"
```

Du kan namnge flera instanser av varje tjänsttyp. Du kan till exempel använda flera Redis-instanser - en för en session och en för cache.

```yaml
redis:
    type: redis:<version>

redis2:
    type: redis:<version>
```

Byta namn på en tjänst i `services.yaml` fil **permanent tar bort** följande:

- Den befintliga tjänsten innan du skapar en tjänst med det nya namn du anger.
- Alla befintliga data för tjänsten tas bort. Adobe rekommenderar starkt att du [säkerhetskopiera startmiljön](../storage/snapshots.md) innan du ändrar namnet på en befintlig tjänst.

### `type`

The `type` värdet anger tjänstens namn och version. Exempel:

```yaml
mysql:
    type: mysql:10.4
```

### `disk`

The `disk` värdet anger storleken på den beständiga disklagringen (i MB) som ska allokeras till tjänsten. Tjänster som använder beständig lagring, till exempel MySQL, måste ange ett diskvärde. Tjänster som använder minne i stället för beständig lagring, som Redis, kräver inget diskvärde.

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
```

Det aktuella standardlagringsutrymmet per projekt är 5 GB eller 512 MB. Du kan distribuera det här beloppet mellan programmet och var och en av dess tjänster.

## Servicerelationer

I Adobe Commerce om molninfrastrukturprojekt [relationer](../application/properties.md#relationships) som konfigurerats i `.magento.app.yaml` filen avgör vilka tjänster som är tillgängliga för ditt program.

Du kan hämta konfigurationsdata för alla tjänstrelationer från [`$MAGENTO_CLOUD_RELATIONSHIPS`](../environment/variables-cloud.md) miljövariabel. Konfigurationsdata innehåller tjänstnamn, typ och version tillsammans med all nödvändig anslutningsinformation, t.ex. portnummer och inloggningsuppgifter.

**Så här verifierar du relationer i lokal miljö**:

1. Visa relationerna för den aktiva miljön i din lokala miljö.

   ```bash
   magento-cloud relationships
   ```

1. Bekräfta `service` och `type` från svaret. Svaret ger anslutningsinformation, t.ex. IP-adress och portnummer.

   >Förkortat provsvar

   ```terminal
   redis:
       -
   ...
           type: 'redis:7.0'
           port: 6379
   elasticsearch:
       -
   ...
           type: 'opensearch:2'
           port: 9200
   database:
       -
   ...
           type: 'mysql:10.6'
           port: 3306
   ```

**Verifiera relationer i fjärrmiljöer**:

1. Använd SSH för att logga in i fjärrmiljön.

1. Visa konfigurationsdata för relationer för alla tjänster som konfigurerats i miljön.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   eller använd följande `ece-tools` kommando för att visa relationer:

   ```bash
   php ./vendor/bin/ece-tools env:config:show services
   ```

1. Bekräfta `service` och `type` från svaret. Svaret innehåller anslutningsinformation, t.ex. IP-adress och portnummer samt eventuella inloggningsuppgifter för användarnamn och lösenord.

## Tjänstversioner

Tjänstversion och kompatibilitetsstöd för Adobe Commerce i molninfrastruktur avgörs av vilka versioner som distribueras och testas i molninfrastrukturen, och skiljer sig ibland från de versioner som stöds av Adobe Commerce lokala distributioner. Se [Systemkrav](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) i _Installation_ för att få en lista över programvaruberoenden från tredje part som Adobe har testat med specifika utgåvor av Adobe Commerce och Magento Open Source.

### EOL-kontroller för programvara

Under distributionsprocessen `ece-tools` paketet kontrollerar installerade tjänstversioner mot slutdatum (EOL) för varje tjänst.

- Om en tjänstversion är inom tre månader från EOL-datumet visas ett meddelande i distributionsloggen.
- Om EOL-datumet redan har infallit visas ett varningsmeddelande.

För att upprätthålla säkerheten måste du uppdatera de installerade programversionerna innan de når EOL. Du kan läsa EOL-datumen i [ece-tools&#39; `eol.yaml` fil](https://github.com/magento/ece-tools/blob/develop/config/eol.yaml).

### Migrera till OpenSearch

{{elasticsearch-support}}

För Adobe Commerce version 2.4.4 och senare, se [Konfigurera OpenSearch-tjänsten](opensearch.md).

## Ändra tjänstversion

Du kan uppgradera den installerade tjänstversionen för kompatibilitet med den Adobe Commerce-version som är distribuerad i din molnmiljö.

Du kan inte nedgradera tjänstversionen för en installerad tjänst direkt. Du kan dock skapa en tjänst med den version som krävs. Se [Nedgradera serviceversion](#downgrade-version).

### Uppgradera installerad tjänstversion

Du kan uppgradera den installerade tjänstversionen genom att uppdatera tjänstkonfigurationen i `services.yaml` -fil.

1. Ändra [`type`](#type) värdet för tjänsten i `.magento/services.yaml` fil:

   > Ursprunglig tjänstdefinition

   ```yaml
   mysql:
       type: mysql:10.3
       disk: 2048
   ```

   > Uppdaterad tjänstdefinition

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   ```

1. Lägg till, implementera och push-överföra kodändringar.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Upgrade MySQL from MariaDB 10.3 to 10.4."
   ```

   ```bash
   git push origin <branch-name>
   ```

### Nedgraderingsversion

Du kan inte nedgradera en installerad tjänst direkt. Du har två alternativ:

1. Byt namn på en befintlig tjänst till den nya versionen, som tar bort den befintliga tjänsten och data, och lägger till en ny.

1. Skapa en tjänst och spara data från den befintliga tjänsten.

När du ändrar tjänstversionen måste du uppdatera tjänstkonfigurationen i `services.yaml` och uppdatera relationerna i `.magento.app.yaml` -fil.

**Så här nedgraderar du en tjänstversion genom att byta namn på en befintlig tjänst**:

1. Byt namn på den befintliga tjänsten i `.magento/services.yaml` och ändra versionen.

   >[!WARNING]
   >
   >Om du byter namn på en befintlig tjänst ersätts den och alla data tas bort. Om du behöver behålla data skapar du en tjänst i stället för att byta namn på den befintliga.

   Om du till exempel vill nedgradera MariaDB-versionen för _mysql_ från version 10.4 till 10.3, ändra den befintliga _service-id_ och _type_ konfiguration.

   > Original `services.yaml` definition

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   ```

   > Nytt `services.yaml` definition

   ```yaml
   mysql2:
        type: mysql:10.3
        disk: 5120
   ```

1. Uppdatera relationerna i `.magento.app.yaml` -fil.

   > Original `.magento.app.yaml` konfiguration

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > Uppdaterat `.magento.app.yaml` konfiguration

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. Lägg till, implementera och push-överföra kodändringar.

**Så här minskar du en tjänst genom att skapa en tjänst**:

1. Lägg till en tjänstdefinition i `services.yaml` -fil för ditt projekt med den nedgraderade versionsspecifikationen. Se _mysql2_ i följande exempel:

   > services.yaml

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   mysql2:
       type: mysql:10.3
       disk: 5120
   ```

1. Ändra relationskonfigurationen i `.magento.app.yaml` som ska använda den nya tjänsten.

   > Original `.magento.app.yaml` konfiguration

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > Nytt `.magento.app.yaml` konfiguration

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. Lägg till, implementera och push-överföra kodändringar.
