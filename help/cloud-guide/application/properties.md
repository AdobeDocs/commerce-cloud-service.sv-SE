---
title: Egenskaper
description: Använd egenskapslistan som referens när du konfigurerar [!DNL Commerce] applikation för att bygga och driftsätta i molninfrastrukturen.
feature: Cloud, Configuration, Build, Deploy, Roles/Permissions, Storage
exl-id: 58a86136-a9f9-4519-af27-2f8fa4018038
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# Egenskaper för programkonfiguration

The `.magento.app.yaml` filen använder egenskaper för att hantera miljöstöd för [!DNL Commerce] program.

| Namn | Beskrivning | Standard | Obligatoriskt |
| ------ | --------------------------------- | ------- | -------- |
| [`access`](#access) | Anpassa användarroller | — | Nej |
| [`crons`](crons-property.md) | Uppdatera specifikationer och schemalägg cron-jobb | — | Nej |
| [`dependencies`](#dependencies) | Aktivera ytterligare beroenden | `php:composer/composer: '2.2.4'` | Nej |
| [`disk`](#disk) | Definiera den beständiga diskstorleken | `5120` | Ja |
| [`firewall`](firewall-property.md) | (Endast Starter) Kontrollera utgående trafik | — | Nej |
| [`hooks`](hooks-property.md) | Skräddarsy kommandon för faserna för bygge, driftsättning och efterdriftsättning | — | Nej |
| [`mounts`](#mounts) | Ange banor | Banor:<ul><li>`"var": "shared:files/var"`</li><li>`"app/etc": "shared:files/etc"`</li><li>`"pub/media": "shared:files/media"`</li><li>`"pub/static": "shared:files/static"`</li></ul> | Nej |
| [`name`](#name) | Definiera programnamnet | `mymagento` | Ja |
| [`relationships`](#relationships) | Karttjänster | Tjänster:<ul><li>`database: "mysql:mysql"`</li><li>`redis: "redis:redis"`</li><li>`opensearch: "opensearch:opensearch"`</li></ul> | Nej |
| [`runtime`](#runtime) | Egenskapen Runtime innehåller tillägg som krävs av [!DNL Commerce] program. | Tillägg:<ul><li>`xsl`</li><li>`newrelic`</li><li>`sodium`</li></ul> | Ja |
| [`type`](#type-and-build) | Ange basbehållarbilden | `php:8.1` | Ja |
| [`variables`](variables-property.md) | Använda en miljövariabel för en specifik handelsversion | — | Nej |
| [`web`](web-property.md) | Hantera externa begäranden | — | Ja |
| [`workers`](workers-property.md) | Hantera externa begäranden | — | Ja, om inte egenskapen web används |

{style="table-layout:auto"}

## `name`

The `name` egenskapen innehåller programnamnet som används i [`routes.yaml`](../routes/routes-yaml.md) fil för att definiera HTTP-uppströmningen (som standard, `mymagento:http`). Om till exempel värdet för `name` är `app`måste du använda `app:http` i det överordnade fältet.

>[!WARNING]
>
>Ändra inte namnet på programmet efter att det har distribuerats. Detta leder till dataförlust.

## `type` och `build`

The `type`  och `build` -egenskaperna innehåller information om basbehållaravbildningen för att skapa och köra projektet.

De `type` språket är PHP. Ange PHP-versionen enligt följande:

```yaml
type: php:<version>
```

The `build` egenskapen avgör vad som händer som standard när projektet skapas. The `flavor` anger en standarduppsättning med byggåtgärder som ska köras. I följande exempel visas standardkonfigurationen för `type` och `build` från `magento-cloud/.magento.app.yaml`:

```yaml
# The toolstack used to build the application.
type: php:8.1
build:
    flavor: none

dependencies:
    php:
        composer/composer: '2.2.4'
```

### Installera och använda Composer 2

The `build: flavor:` -egenskapen används inte för Composer 2.x. Därför måste du installera Composer manuellt under byggfasen. Om du vill installera och använda Composer 2.x i dina Starter- och Pro-projekt måste du göra tre ändringar i `.magento.app.yaml` konfiguration:

1. Ta bort `composer` som `build: flavor:` och lägga till `none`. Den här ändringen förhindrar att Creative Cloud använder standardversionen av Composer 1.x för att köra byggåtgärder.
1. Lägg till `composer/composer: '^2.0'` som `php` beroende för installation av Composer 2.x.
1. Lägg till `composer` bygga uppgifter till `build` som kör byggåtgärderna med Composer 2.x.

Använd följande konfigurationsfragment i din egen `.magento.app.yaml` konfiguration:

```yaml
# 1. Change flavor to none.
build:
    flavor: none

# 2. Add Composer ^2.0 as a php dependency.
dependencies:
    php:
        composer/composer: '^2.0'

# 3. Add a build hook to run the build tasks using Composer 2.x.
hooks:
    build: |
        set -e
        composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
```

Se [Obligatoriska paket](../development/overview.md#required-packages) för mer information om Composer.

## `dependencies`

Ange beroenden som programmet kan behöva under byggprocessen.

Adobe Commerce stöder beroenden av följande språk:

- PHP
- Ruby
- Node.js

Dessa beroenden är oberoende av programmets eventuella beroenden och är tillgängliga i `PATH`, under byggprocessen och i körningsmiljön för programmet.

Du kan ange dessa beroenden enligt följande:

```yaml
ruby:
   sass: "~3.4"
nodejs:
   grunt-cli: "~0.3"
```

## `runtime`

Används för att ändra PHP-konfigurationen vid körning, till exempel för att aktivera tillägg. Följande tillägg krävs:

```yaml
runtime:
    extensions:
        - xsl
        - newrelic
        - sodium
```

Se [PHP-inställningar](php-settings.md) om du vill ha information om hur du aktiverar tillägg.

## `disk`

Definierar programmets beständiga diskstorlek i MB.

```yaml
disk: 5120
```

Den minsta rekommenderade diskstorleken är 256 MB. Om felet visas `UserError: Error building the project: Disk size may not be smaller than 128MB`, ökar storleken till 256 MB.

>[!NOTE]
>
>För Pro Staging- och Production-miljöer måste du [Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) för att uppdatera `mounts` och `disk` konfiguration för programmet. När du skickar in biljetten anger du de konfigurationsändringar som krävs och inkluderar en uppdaterad version av din `.magento.app.yaml` -fil.

## `relationships`

Definierar tjänstmappningen i programmet.

Relationen `name` är tillgängligt för programmet i `MAGENTO_CLOUD_RELATIONSHIPS` miljövariabel. The `<service-name>:<endpoint-name>` relationer mappas till namn- och typvärdena som definieras i `.magento/services.yaml` -fil.

```yaml
relationships:
    <name>: "<service-name>:<endpoint-name>"
```

Följande är ett exempel på standardrelationerna:

```yaml
relationships:
    database: "mysql:mysql"
    redis: "redis:redis"
    opensearch: "opensearch:opensearch"
    rabbitmq: "rabbitmq:rabbitmq"
```

Se [Tjänster](../services/services-yaml.md) om du vill ha en fullständig lista över de tjänstetyper och slutpunkter som stöds.

## `mounts`

Ett objekt vars nycklar är sökvägar i förhållande till programmets rot. Monteringen är ett skrivbart område på disken för filer. Nedan följer en standardlista över de uppsättningar som har konfigurerats i `magento.app.yaml` filen med `volume_id[/subpath]` syntax:

```yaml
 # The mounts that will be performed when the package is deployed.
mounts:
    "var": "shared:files/var"
    "app/etc": "shared:files/etc"
    "pub/media": "shared:files/media"
    "pub/static": "shared:files/static"
```

Formatet för att lägga till din montering i den här listan är följande:

```bash
"/public/sites/default/files": "shared:files/files"
```

- `shared`- Delar en volym mellan programmen i en miljö.
- `disk`- Definierar storleken som är tillgänglig för den delade volymen.

>[!NOTE]
>
>För Pro Staging- och Production-miljöer måste du [Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) för att uppdatera `mounts` och `disk` konfiguration för programmet. När du skickar in biljetten anger du de konfigurationsändringar som krävs och inkluderar en uppdaterad version av din `.magento.app.yaml` -fil.

Du kan göra monteringen webbtillgänglig genom att lägga till den i [`web`](web-property.md) block med platser.

>[!WARNING]
>
>När din webbplats har data, ändra inte `subpath` del av monteringsnamnet. Det här värdet är den unika identifieraren för `files` område. Om du ändrar det här namnet förlorar du alla webbplatsdata som lagras på den gamla platsen.

## `access`

The `access` anger en lägsta användarrollnivå som tillåter SSH-åtkomst till miljöerna. De tillgängliga användarrollerna är:

- `admin`—Kan ändra inställningar och utföra åtgärder i miljön; har _medverkande_ och _visningsprogram_ rättigheter.
- `contributor`—Kan överföra kod till den här miljön och grenar från miljön; har _visningsprogram_ rättigheter.
- `viewer`—Kan endast visa miljön.

Standardanvändarrollen är `contributor`, vilket begränsar SSH-åtkomsten för användare med endast _visningsprogram_ rättigheter. Du kan ändra användarrollen till `viewer` för att tillåta SSH-åtkomst för användare med endast _visningsprogram_ rättigheter:

```yaml
access:
    ssh: viewer
```
