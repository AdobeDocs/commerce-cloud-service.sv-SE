---
title: Startarkitektur
description: Läs mer om de miljöer som stöds av Starter-arkitekturen.
feature: Cloud, Paas
exl-id: 03365d32-4eb4-42d4-82a7-771df5e7b3da
source-git-commit: c61d711b1041ecf76ec6468cd225a34fd77c24b1
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%

---

# Startarkitektur

Din Adobe Commerce på molninfrastruktur Starter-arkitektur stöder upp till **fyra** miljöer, inklusive `master` miljö som innehåller den inledande projektkoden, mellanlagringsmiljön och upp till två integreringsmiljöer.

Alla miljöer finns i PaaS-behållare (Platform as a service). Behållarna distribueras inuti mycket begränsade behållare på ett rutnät med servrar. De här miljöerna är skrivskyddade och godkänner distribuerade kodändringar från grenar som har skickats från den lokala arbetsytan. Varje miljö innehåller en databas- och webbserver.

Du kan använda vilken utvecklings- och förgrenade metod du vill. Skapa en `staging` från `master` miljö. Skapa sedan `integration` miljö genom förgreningar från `staging`.

## Arkitektur för startmiljö

I följande diagram visas de hierarkiska relationerna mellan Starter-miljöerna.

![Högnivåvy av Starter-projekt](../../assets/starter/architecture.png)

## Produktionsmiljö

Produktionsmiljön innehåller källkoden för att distribuera Adobe Commerce till molninfrastrukturen som kör dina offentliga butiker för en och flera platser. Produktionsmiljön använder kod från `master` för att konfigurera och aktivera webbservern, databasen, konfigurerade tjänster och programkoden.

På grund av `production` -miljön är skrivskyddad, använd `integration` miljö för att göra kodändringar, driftsätta i hela arkitekturen från `integration` till `staging`och slutligen till `production` miljö. Se [Distribuera din butik](../deploy/staging-production.md) och [Starta webbplatsen](../launch/overview.md).

Adobe rekommenderar att du använder `staging` förgrening innan du går till `master` gren, som distribuerar till `production` miljö.

## Mellanlagringsmiljö

Adobe rekommenderar att du skapar en gren med namnet `staging` från `master`. The `staging` filialen använder kod i staging-miljön för att tillhandahålla en förproduktionsmiljö för att testa kod, moduler och tillägg, betalningsgateways, leveranser, produktdata och mycket annat. Den här miljön innehåller konfigurationen för alla tjänster som matchar produktionsmiljön, inklusive Fastly, New Relic APM och sökning.

Ytterligare avsnitt i den här guiden innehåller anvisningar för slutgiltig koddistribution och testning av interaktioner på produktionsnivå i en säker mellanlagringsmiljö. För bästa prestanda och funktionstestning ska du replikera databasen till mellanlagringsmiljön.

>[!WARNING]
>
>Adobe rekommenderar att man testar alla interaktioner mellan handlare och kunder i mellanlagringsmiljön innan man driftsätter i produktionsmiljön. Se [Distribuera din butik](../deploy/staging-production.md) och [Testa distributionen](../test/staging-and-production.md).

## Integreringsmiljö

Utvecklare använder `integration` miljö för att utveckla, driftsätta och testa:

- Adobe Commerce-programkod

- Egen kod

- Tillägg

- Tjänster

**Rekommenderade användningsfall:**

Integrationsmiljöer är utformade för begränsad testning och utveckling. Du kan till exempel använda integreringsmiljön för att utföra följande uppgifter:

- Se till att ändringar i CI-processer är molnkompatibla

- Testa viktiga arbetsflöden på nyckelsidor som Hem, Kategori, Produktinformationssida (PDP), Checka ut och Admin

För bästa prestanda i integreringsmiljön bör du följa dessa standarder:

- Begränsa katalogstorlek

- Begränsa användningen till en eller två samtidiga användare

- Inaktivera cron-jobb och kör manuellt efter behov

Du kan ha upp till **två** aktiva integreringsmiljöer. Du skapar en integreringsmiljö genom att skapa en gren från `staging` gren. När du skapar en integreringsmiljö matchar miljönamnet förgreningsnamnet. En integreringsmiljö innehåller en webbserver och en databas. Det omfattar inte alla tjänster, till exempel Fast CDN och New Relic är inte tillgängliga.

Du kan ha ett obegränsat antal inaktiva grenar för kodlagring. Om du vill få åtkomst till, visa och testa en inaktiv gren måste du aktivera den

{{enhanced-integration-envs}}

## Produktions- och stagingteknologi

Produktions- och staging-miljöerna omfattar följande tekniker. Du kan ändra och konfigurera dessa tekniker via [`.magento.app.yaml`](../application/configure-app-yaml.md) -fil.

- Snabbt för HTTP-cachning och CDN
- Nginx webbserver som talar till PHP-FPM, en instans med flera arbetare
- Redis-server
- Elasticsearch för katalogsökning i Adobe Commerce 2.2 till 2.4.3-p2
- OpenSearch - katalogsökning efter Adobe Commerce 2.3.7-p3, 2.4.3-p2 och 2.4.4 och senare
- Tryckfiltrering (utgående brandvägg)

### Tjänster

Adobe Commerce i molninfrastruktur stöder för närvarande följande tjänster: PHP, MySQL (MariaDB), Elasticsearch (Adobe Commerce 2.2 till 2.4.3-p2), OpenSearch (2.3.7-p3, 2.4.3-p2, 2.4.4 och senare), Redis och [!DNL RabbitMQ].

Varje tjänst körs i en separat, säker behållare. Behållare hanteras tillsammans i projektet. Vissa tjänster är standard, till exempel följande:

- HTTP-router (hanterar inkommande begäranden, men också cachelagring och omdirigeringar)

- PHP-programserver

- Git

- Secure Shell (SSH)

### Programversioner

Adobe Commerce i molninfrastruktur använder operativsystemet Debian GNU/Linux och NGINX-webbservern. Du kan inte uppgradera den här programvaran, men du kan konfigurera versioner för följande:

- [PHP](../application/php-settings.md)

- [MySQL](../services/mysql.md)

- [Redis](../services/redis.md)

- [RabbitMQ](../services/rabbitmq.md)

- [Elasticsearch](../services/elasticsearch.md)

- [OpenSearch](../services/opensearch.md)

I testmiljöer och produktionsmiljöer använder du snabbt för CDN och cachning. Den senaste versionen av tillägget Snabbt CDN installeras när ditt projekt etableras. Du kan uppgradera tillägget för att få de senaste felkorrigeringarna och förbättringarna. Se [Snabb CDN-modul för Magento 2](https://github.com/fastly/fastly-magento2). Du har även tillgång till [New Relic](../monitor/account-management.md) för prestandaövervakning.

Använd följande filer för att konfigurera de programversioner som du vill använda i implementeringen.

- [`.magento.app.yaml`](../application/configure-app-yaml.md)

- [`vägar.yaml`](../routes/routes-yaml.md)

- [&quot;services.yaml&quot;](../services/services-yaml.md)

### Säkerhetskopiering och katastrofåterställning

Du kan skapa en säkerhetskopia av databasen och filsystemet med hjälp av [!DNL Cloud Console] eller CLI. Se [Hantering av säkerhetskopiering](../storage/snapshots.md).

## Förbered för utveckling

I följande arbetsflöde sammanfattas processen för att dela ut koden, utveckla och distribuera butiken:

1. Konfigurera din lokala miljö

1. Klona `master` till din lokala miljö

1. Skapa en `staging` förgrening från `master`

1. Skapa grenar för utveckling från `staging`

1. Skicka kod till Git som bygger och distribuerar till en miljö för testning

I följande avsnitt finns detaljerade anvisningar och genomgångar för att utveckla, testa och driftsätta butiken:

- [Arbetsflöde för utveckling och driftsättning](starter-develop-deploy-workflow.md)

- [Dockningsutveckling](../dev-tools/cloud-docker.md) (lokal utvecklingsmiljö aktiverad av Cloud Docker för Commerce)

- [Hantera grenar](../project/console-branches.md)

- [Distribuera din butik](../deploy/staging-production.md)

- [Starta webbplatsen](../launch/overview.md)
