---
title: Pro-arkitektur
description: Läs om de miljöer som stöds av Pro-arkitekturen.
feature: Cloud, Auto Scaling, Iaas, Paas, Storage
topic: Architecture
exl-id: d10d5760-44da-4ffe-b4b7-093406d8b702
source-git-commit: 6807b572366d28fd54fbec89e7c119ec158b5e10
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 0%

---

# Pro-arkitektur

Din Adobe Commerce på molninfrastruktur Pro-arkitektur stöder flera miljöer som du kan använda för att utveckla, testa och lansera din butik.

- **Master**—Tillhandahåller en `master` gren distribuerad till plattformar som en tjänstbehållare (PaaS).
- **Integrering**—Tillhandahåller en enda `integration` för utveckling, men du kan skapa ytterligare en gren. Detta tillåter upp till två _aktiv_ grenar som distribueras till plattformar som tjänstbehållare (PaaS).
- **Mellanlagring**—Tillhandahåller en enda `staging` en gren som distribuerats till dedikerad infrastruktur som en IaaS-behållare.
- **Produktion**—Tillhandahåller en enda `production` en gren som distribuerats till dedikerad infrastruktur som en IaaS-behållare.

I följande tabell sammanfattas skillnaderna mellan miljöerna:

|                                        | INTEGRERING | STAGNING | PRODUKTION |
| -------------------------------------- | ----------- | ----------------- | -------------------- |
| Hantering av inställningar i [!DNL Cloud Console] | Ja | Begränsad | Begränsad |
| Stöder flera grenar | Ja | Nej (endast mellanlagring) | Nej (endast produktion) |
| Använder YAML-filer för konfiguration | Ja | Nej | Nej |
| Körs på dedikerad IaaS-maskinvara | Nej | Ja | Ja |
| Fast CDN ingår | Nej | Ja | Ja |
| Inkluderar New Relic | Nej | APM | APM + NRI |
| Automatisk säkerhetskopiering | Nej | Ja | Ja |

>[!NOTE]
>
>Adobe tillhandahåller verktyget Cloud Docker for Commerce för distribution till en lokal Cloud Docker-miljö så att du kan utveckla och testa Adobe Commerce-projekt. Se [Dockningsutveckling](../dev-tools/cloud-docker.md).

## Miljöarkitektur

Ditt projekt är en enda Git-databas med tre huvudgrenar: `integration`, `staging`och `production`. I följande diagram visas det hierarkiska förhållandet mellan Pro-miljöer:

![En högnivåvy över Pro-miljöarkitekturen](../../assets/pro-branch-architecture.png)

### Huvudmiljö

I Pro-projekt är `master` gren tillhandahåller en aktiv PaaS-miljö i din produktionsmiljö. Skicka alltid en kopia av produktionskoden till `master` så att du kan felsöka produktionsmiljön utan att avbryta tjänsterna.

**Caveats:**

- Gör **not** skapa en gren baserat på `master` gren. Använd integreringsmiljön för att skapa aktiva grenar för utveckling.

- Använd inte `master` miljö för utveckling, UAT eller prestandatestning

### Integreringsmiljö

Integreringsmiljön körs i en Linux-behållare (LXC) på ett rutnät med servrar som kallas PaaS. Varje miljö innehåller en webbserver och databas som testar platsen. Se [Regionala IP-adresser](../project/regional-ip-addresses.md) för en lista över IP-adresser för AWS och Azure.

**Rekommenderade användningsfall:**

Integrationsmiljöer är utformade för begränsad testning och utveckling innan ändringar görs i miljöer för testning och produktion. Du kan till exempel använda integreringsmiljön för att utföra följande uppgifter:

- Se till att ändringar i CI-processer är molnkompatibla

- Testa viktiga arbetsflöden på nyckelsidor som Hem, Kategori, Produktinformationssida (PDP), Checka ut och Admin

För bästa prestanda i integreringsmiljön bör du följa dessa standarder:

- Begränsa katalogstorlek

- Begränsa användningen till en eller två samtidiga användare

- Inaktivera cron-jobb och kör manuellt efter behov

**Caveats:**

- CDN- och New Relic-tjänsterna är inte tillgängliga i en integreringsmiljö

- Integreringsmiljöns arkitektur matchar inte arkitekturen för förproduktion och produktion

- Använd inte `integration` miljö för utvecklingstestning, prestandatestning eller UAT (User accept testing)

- Använd inte `integration` miljö för att testa B2B-funktioner för Adobe Commerce

- Du kan inte återställa databasen i integreringsmiljön från databasproduktionen eller mellanlagringen

{{enhanced-integration-envs}}

### Mellanlagringsmiljö

Mellanlagringsmiljön är en miljö för närproduktion som du kan använda för att testa platsen. Den här miljön, som finns på dedikerad IaaS-maskinvara, innehåller alla tjänster, som Fastly CDN, New Relic APM och sökning.

**Rekommenderade användningsfall:**

Miljön matchar produktionsarkitekturen och är utformad för UAT, innehållstagning och slutgranskning innan funktionerna skickas till `production` miljö. Du kan till exempel använda `staging` miljö för att utföra följande uppgifter:

- Regressionstestning mot produktionsdata

- Prestandatestning med snabb cachelagring aktiverat

- Testa nya byggen i stället för att laga i produktionen

- UAT-testning för nya byggen

- Testa B2B för Adobe Commerce

- Anpassa cron-konfiguration och testa cron-jobb

Se [Arbetsflöde för distribution](pro-develop-deploy-workflow.md#deployment-workflow) och [Testa distributionen](../test/staging-and-production.md).

**Caveats:**

- När du har startat produktionsplatsen använder du i första hand testmiljön för att testa korrigeringar för produktionskritiska buggfixar.

- Du kan inte skapa en gren från `staging` gren. I stället skickar du kodändringar från `integration` förgrena till `staging` gren.

### Produktionsmiljö

Produktionsmiljön kör dina offentliga butiker för en och flera platser. Den här miljön använder dedikerad IaaS-maskinvara med redundanta noder med hög tillgänglighet för kontinuerlig åtkomst och failover-skydd för dina kunder. Produktionsmiljön innehåller alla tjänster i staging-miljön, plus [New Relic Infrastructure (NRI)](../monitor/new-relic-service.md#new-relic-infrastructure) som automatiskt ansluter till programdata och prestandaanalyser för att tillhandahålla dynamisk serverövervakning.

**Caveat:**

Du kan inte skapa en gren från `production` gren. I stället skickar du kodändringar från `staging` förgrena till `production` gren.

### Production Technology stack

Produktionsmiljön har tre virtuella datorer (VM) bakom en elastisk belastningsutjämnare som hanteras av en HAProxy per VM. Varje virtuell dator innehåller följande tekniker:

- **Snabb CDN**—HTTP-cachning och CDN

- **NGINX**-webbserver med PHP-FPM, en instans med flera arbetare

- **GlusterFS**—filserver för hantering av alla statiska fildistributioner och synkronisering med fyra kataloginstallationer:

   - `var`
   - `pub/media`
   - `pub/static`
   - `app/etc`

- **Redis**—en server per VM med endast en aktiv och de andra två som repliker

- **Elasticsearch**—sök efter Adobe Commerce om molninfrastruktur 2.2 till 2.4.3-p2

- **OpenSearch**—sök efter Adobe Commerce om molninfrastruktur 2.3.7-p3, 2.4.3-p2, 2.4.4 och senare

- **Galera**—databaskluster med en MariaDB MySQL-databas per nod med en inställning för automatisk ökning på tre för unika ID:n i alla databaser

Följande bild visar vilka tekniker som används i produktionsmiljön:

![Production Technology stack](../../assets/az-stack-diagram.png)

## Redundanta maskinvara

Istället för att köra en traditionell, aktiv-passiv `master` eller en primär sekundär installation, kör Adobe Commerce i molninfrastrukturen en _redundant arkitektur_ där alla tre förekomsterna accepterar läsningar och skrivningar. Denna arkitektur erbjuder inga driftavbrott vid skalning och ger garanterad transaktionsintegritet.

På grund av den unika, redundanta maskinvaran kan Adobe tillhandahålla tre gateway-servrar. De flesta externa tjänster gör att du kan lägga till flera IP-adresser till en tillåtelselista, så att det inte är något problem att ha fler än en fast IP-adress. De tre gatewayarna mappas till de tre servrarna i produktionsmiljöklustret och behåller statiska IP-adresser. Den är helt överflödig och mycket tillgänglig på alla nivåer:

- DNS
- CDN (Content Delivery Network)
- Elastisk belastningsutjämnare (ELB)
- Tre serverkluster som omfattar alla Adobe Commerce-tjänster, inklusive databas- och webbservern

## Säkerhetskopiering och katastrofåterställning

Adobe Commerce i molninfrastruktur använder en arkitektur med hög tillgänglighet som replikerar varje Pro-projekt på tre separata AWS- eller Azure-tillgänglighetszoner, där varje zon har ett separat datacenter. Förutom denna redundans får Pro staging- och produktionsmiljöer regelbundna, livesäkerhetskopieringar som är utformade för att användas i fall av _katastrofalt fel_.

**Automatisk säkerhetskopiering** innehåller beständiga data från alla tjänster som körs, som MySQL-databasen och filer som lagras på de monterade volymerna. Säkerhetskopiorna sparas i krypterad Elastic Block Storage (EBS) i samma region som produktionsmiljön. De automatiska säkerhetskopiorna är inte tillgängliga för allmänheten eftersom de lagras i ett separat system.

{{pro-backups}}

Du kan skapa **manuell säkerhetskopiering** databasen för dina mellanlagrings- och produktionsmiljöer med CLI-kommandon. Se [Säkerhetskopiera databasen](../storage/database-dump.md). För `integration` Adobe rekommenderar att du skapar en säkerhetskopia som ett första steg efter att du har öppnat ditt Adobe Commerce i ett molninfrastrukturprojekt och innan du gör några större ändringar. Se [Hantering av säkerhetskopiering](../storage/snapshots.md).

### Mål för återställningspunkt

RPO är sex timmars maximal tid för senaste säkerhetskopiering (till exempel 06:00, 12:00 och sedan 18:00). Hur ofta säkerhetskopieringar ska göras beror på schemat för säkerhetskopiering av din plan och hur många ändringar som ska skrivas till lagringstjänsten.

### Bevarandeprincip

Adobe behåller automatiska säkerhetskopieringar enligt följande datalagringspolicy:

| Tidsperiod | Princip för kvarhållning av säkerhetskopia |
| ------------------ | ----------------------- |
| Dag 1 till 3 | En säkerhetskopia per timme |
| Dagar 4 till 7 | En säkerhetskopiering per dag |
| Vecka 2 till 6 | En säkerhetskopia per vecka |
| Vecka 8 till 12 | En säkerhetskopiering varannan vecka |
| Månad 3 till 5 | En säkerhetskopia per månad |

Den här principen kan variera beroende på din molninfrastrukturplan.

### Mål för återställningstid

RTO beror på lagringens storlek. Stora EBS-volymer tar längre tid att återställa. Återställningstiden kan variera beroende på databasens storlek:

- En stor databas (200+ GB) kan ta 5 timmar
- En medelstor databas (150 GB) kan ta 2 1/2 timmar
- En liten databas (60 GB) kan ta en timme

{{pro-backups}}

## Pro, klusterskalning

Pro-klusterstorlek och _compute_ olika konfigurationer beroende på vald molnleverantör (AWS, Azure), region och tjänstberoenden. Adobe molninfrastruktur kan skala Pro-kluster för att passa trafikens förväntningar och servicekraven när efterfrågan förändras.

Den redundanta arkitekturen gör att molninfrastrukturen i Adobe kan byggas ut utan driftstopp. Vid uppskalning roterar var och en av de tre instanserna till uppgraderingskapacitet utan att påverka webbplatsens funktion. Du kan till exempel lägga till extra webbservrar i ett befintligt kluster om gränsen är på PHP-nivå i stället för på databasnivå. Detta ger _vågrät skalförändring_ som komplement till den vertikala skalning som extra processorer ger på databasnivå. Se [Skalbar arkitektur](scaled-architecture.md).

Om du förväntar dig en avsevärd ökning av trafiken för en händelse eller av någon annan anledning kan du begära en tillfällig kapacitetsökning. Se [Så här begär du en tillfällig storlek](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-request-temporary-magento-upsize.html) i _Commerce Help Center_.
