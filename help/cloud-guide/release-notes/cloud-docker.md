---
title: Cloud Docker-paket
description: Se en lista över de senaste förbättringarna av Cloud Docker-paketet.
feature: Cloud, Docker, Release Notes
recommendations: noDisplay, catalog
last-substantial-update: 2024-04-08T00:00:00Z
exl-id: 907d977f-2e9c-4553-a46b-000bc6a57b28
source-git-commit: bc76cba0219f16fd055c20289811b51c35c9b026
workflow-type: tm+mt
source-wordcount: '3662'
ht-degree: 0%

---

# Cloud Docker-paket

The [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker) paket med funktioner och Docker-bilder för att distribuera Adobe Commerce till en lokal molnmiljö. I versionsinformationen beskrivs de senaste förbättringarna av det här paketet, som är en komponent i [Cloud Tools Suite for Commerce](cloud-tools-suite.md).

The `magento/magento-cloud-docker` paketet använder följande versionssekvens: `<major>.<minor>.<patch>`

Versionsinformationen innehåller:

- ![ny ikon](../../assets/new.svg) Nya funktioner
- ![korrigeringsikon](../../assets/fix.svg) Korrigeringar och förbättringar

<!--Add release notes below-->

## v1.3.7 {#latest}

Releasedatum: 8 april 2024

- ![ny ikon](../../assets/new.svg) **PHP** - Stöd för bilder i PHP 8.3 och PHP 8.3 har lagts till.
- ![ny ikon](../../assets/new.svg) **Nginx** — Added image nginx v. 1.24.
- ![ny ikon](../../assets/new.svg) **Öppna sökning** - Lagt till bild OpenSearch v. 2.12, 1.3.
- ![ny ikon](../../assets/new.svg) **Disposition** - Uppdaterad Composer-version till 2.2.23.

## v1.3.6

Releasedatum: 31 juli 2023

- ![ny ikon](../../assets/new.svg) **Ny tjänstversion har lagts till**—OpenSearch 2.5.
- ![ny ikon](../../assets/new.svg) **Aktivera Composer-cache**- Nu kan du utöka Docker-konfigurationen för att aktivera rensningscache för Composer när du startar Docker-behållaren. Se [Utöka Docker-konfigurationen](https://developer.adobe.com/commerce/cloud-tools/docker/configure/extend-docker-configuration/) i _Cloud Docker for Commerce_ guide.

## v1.3.5

Releasedatum: 10 mars 2023

- ![ny ikon](../../assets/new.svg) **ionCube**- Tillägg av jonCube för bilden PHP 8.1 har lagts till.
- ![ny ikon](../../assets/new.svg) **Nya tjänsteversioner har lagts till**—OpenSearch 2.3 och 2.4, PHP 8.2, lack 7.1.1.
- ![ny ikon](../../assets/new.svg) **Förbättrat stöd för PHP 8.2**—Korrigerade kompatibilitetsproblem med vissa PHP 8.2.x-versioner som stöder Commerce 2.4.6.
- ![korrigeringsikon](../../assets/fix.svg) **Problem med disposition**—Problem som uppstod efter uppdatering av Composer-versionen i Docker-behållarna har åtgärdats.

## v1.3.4

Releasedatum: 27 oktober 2022

- ![ny ikon](../../assets/new.svg) **Nya lack-bilder har lagts till**—Lagt till bilder för lack 6.5, 7.0 och 7.1.<!-- MCLOUD-7879 -->

## v1.3.3

Releasedatum: 13 september 2022

- ![ny ikon](../../assets/new.svg) **Stöd för Apple M1 (ARM64)**—Ändringar har gjorts i Docker-bilder för att aktivera stöd för arkitekturen Apple M1 (ARM64).<!-- MCLOUD-7989-2 MCLOUD-7989 -->
- ![korrigeringsikon](../../assets/fix.svg) **Mailhog**—Ett problem har korrigerats där e-postmeddelanden inte kunde identifieras i Mailhog-tjänsten i utvecklarläge.<!-- MCLOUD-8643 -->
- ![korrigeringsikon](../../assets/fix.svg) **init-docker.sh**—Tjänstversionernas validerare i `init-docker.sh` skript.<!-- MCLOUD-8765 -->

## v1.3.2

Releasedatum: 31 mars 2022

- ![ny ikon](../../assets/new.svg) **Elasticsearch 7.10-bild har lagts till**<!-- MCLOUD-8548 -->

## v1.3.1

Releasedatum: 10 mars 2022

- ![ny ikon](../../assets/new.svg) **Stöd för PHP 8.1**- Stöd för PHP 8.1 har lagts till.
- ![ny ikon](../../assets/new.svg) **OpenSearch**—Bilder av OpenSearch version 1.1 och 1.2 har lagts till.
- ![ny ikon](../../assets/new.svg) **Disposition 2.1**—Ange disposition 2.1.x som standard i PHP 8.x-bilder.
- ![ny ikon](../../assets/new.svg) **Förbättringar av PHP-bilder**—

   - PHP 8.1-bilder har lagts till
   - Uppgraderad xDebug version 3.1.2
   - Uppgraderad xmlrpc 1.0.0RC3

- ![korrigeringsikon](../../assets/fix.svg) **Förbättringar i Elasticsearch och OpenSearch**—Förbättringar i Elasticsearch och OpenSearch Dockerfiles; bilden i Elasticsearch 5.2 har tagits bort.
- ![korrigeringsikon](../../assets/fix.svg) **Natriumtillägg**—Aktiverad för `sodium` som standard i alla PHP-bilder.
- ![korrigeringsikon](../../assets/fix.svg) **Cachevolym för Composer**—En fast sökväg för cacheminnesvolymen för Composer har korrigerats så att Composer-paket har cachelagrats.
- ![korrigeringsikon](../../assets/fix.svg) **Minnesbegränsning i nginx**—Begränsningen för minne i NGINX-bilden har åtgärdats.

## v1.3.0

Releasedatum: 25 oktober 2021

- ![korrigeringsikon](../../assets/fix.svg) **Förbättra arbetsflödet i utvecklarläget**- Tidigare behövde du ange läge i bygg- och distributionsstegen. Nu `--mode` i `build` steg bestämmer läget i det senare `deploy` steg. Du behöver inte längre ställa in läget efter distributionen. Se [Utvecklarläge](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html).<!-- ACMP-1086 -->
- ![korrigeringsikon](../../assets/fix.svg) **Förbättringar för skrivskyddat filsystem**—<!-- ACMP-1106 -->
   - Åtgärda problem med att starta en PHP-behållare för e-postkonfiguration.
   - Kan använda miljövariabler i INI-filer.
   - Kontrollera att PHP-startpunkterna inte behöver skrivbehörighet.
- ![korrigeringsikon](../../assets/fix.svg) **Uppdatera nod**—Uppdatera den paketerade nodversionen. När du installerar Node i PHP-CLI-bilder används nu den aktuella LTS-versionen.<!-- ACMP-1539 -->
- ![korrigeringsikon](../../assets/fix.svg) **Uppdatera Symfony**—Symfony-konfigurationsberoendena har uppdaterats så att de är kompatibla med Adobe Commerce 2.4.4.<!-- ACMP-1533 -->

## v1.2.4

Releasedatum: 29 juli 2021

- ![ny ikon](../../assets/new.svg) **Nytt `Zookeeper` container**—Added a [Zookeeper-behållare](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#zookeeper-container) för att hantera låsproviderkonfiguration för projekt som inte distribueras till Adobe Commerce i molninfrastrukturen.<!--MCLOUD-8000-->

- ![ny ikon](../../assets/new.svg) **Stöd för Composer 2.0 har lagts till.**—Kompositör version 2.0 har lagts till i Composer-konfigurationsfilen med stöd för uppgraderingar från Composer 1.0, som närmar sig slutet av livscykeln.<!--MCLOUD-8003-->

## v1.2.3

Releasedatum: 14 juni 2021

- ![ny ikon](../../assets/new.svg) **PHP 8.0 har lagts till**—PHP har uppdaterats till version 8.0 och du kan utnyttja alla nya funktioner och optimeringar i PHP 8.0.<!--MCLOUD-7941-->
- ![ny ikon](../../assets/new.svg) **Uppdaterat till engelska 6.6 och Elasticsearch 7.11.2**—Följande länkar innehåller versionsinformation om [Finska cache 6.6](https://varnish-cache.org/releases/rel6.6.0.html#rel6-6-0) och Elasticsearch 7.11.2<!--MCLOUD-7921-->
- ![ny ikon](../../assets/new.svg) **Tillagd `ioncube` tillägg för PHP 7.4-bild**—The `ioncube` tillägget har lagts till i PHP 7.4-bilden på nytt efter att först ha uteslutits från uppgraderingen av PHP 7.3 till PHP 7.4. *[Skickat av maskskr](https://github.com/magento/magento-cloud-docker/pull/314).*<!--PR #314-->
- ![ny ikon](../../assets/new.svg) **Ett filsynkroniseringsalternativ har lagts till:`manual-native`**—The `manual-native` filsynkroniseringsalternativ ger manuell kontroll över synkroniseringen, vilket ger bästa prestanda för macOS- och Windows-miljöer. Läs om hur du använder `manual-native` alternativ i [Utvecklarläge](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) och [Synkronisera data i en Docker-utvecklingsmiljö](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html#file-synchronization-options).<!--MCLOUD-7977-->
- ![ny ikon](../../assets/new.svg) **Borttagna volymborttagningar från `up` och `down` kommandon**—The `--volume` alternativet har tagits bort från `bin/magento-docker up` och `bin/magento-docker down` kommandon, som ersätts av nya `bin/magento-docker init` med en varning om dataförlust. Den här ändringen förhindrar dataförlust av misstag. *[Inskickat av joeshelton-wagento](https://github.com/magento/magento-cloud-docker/pull/319).*<!--PR #319-->
- ![korrigeringsikon](../../assets/fix.svg) **Uppdaterat `CN` värde för det genererade certifikatet**—Den hårdkodade filen togs bort `CN` från Dockerfile. Detta värde skapade ett certifikatfel (`NET::ERR_CERT_INVALID`) som orsakade `--host` för `ece-docker build:compose` som ska ignoreras.<!--MCLOUD-7934-->

## v1.2.2

Releasedatum: 20 april 2021

- ![ny ikon](../../assets/new.svg) **Uppdaterat `host.docker.internal` vara plattformsoberoende**—Nu kan du skapa samma Docker Compose-skript för Ubuntu, Windows och macOS. Xdebug på Ubuntu kräver inte längre en separat miljövariabel. [Fix från Igor Vitol](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #298-->
- ![ny ikon](../../assets/new.svg) **Uppdaterat init-docker.sh**—Added the `mounts` objekt till `MAGENTO_CLOUD_APPLICATION` miljövariabel. [Fix inskickad av Chiranjeevi](https://github.com/magento/magento-cloud-docker/pull/299).<!--Issue #299-->
- ![ny ikon](../../assets/new.svg) **Uppdaterat init-docker.sh**—Uppdaterade `init-docker.sh` skript med PHP 7.4 och Cloud Docker 1.2.1. [Fix inskickad av Adarsh Manickam](https://github.com/magento/magento-cloud-docker/pull/300).<!--Issue #300-->
- ![ny ikon](../../assets/new.svg) **Natrium är aktiverat som standard**—Aktiverad för `sodium` PHP-tillägg som standard i PHP Docker-bilder.<!--MCLOUD-7548-->
- ![ny ikon](../../assets/new.svg) **`custom-registry`option**—Added a `--custom-registry` alternativ till `php ./vendor/bin/ece-docker build:compose` för att använda ditt eget bildregister.<!--MCLOUD-7476-->

  ```bash
  ./vendor/bin/ece-docker build:compose --custom-registry=my-registry.example.com
  ```

- ![ny ikon](../../assets/new.svg) **Tidigare versioner av Elasticsearch har tagits bort**—Elasticsearch version 1.7 och 2.4 har tagits bort från bilderna i Elasticsearch.<!--MCLOUD-7504-->
- ![ny ikon](../../assets/new.svg) **Autogenerera NGINX-certifikat**—Befintliga certifikat har tagits bort från NGINX-bilden. NGINX-certifikaten genereras nu automatiskt med varje ny distribution för förbättrad säkerhet.<!--MCLOUD-7396-->
- ![korrigeringsikon](../../assets/fix.svg) **Aktiverad`opcache.validate_timestamps`**—Aktiverad för `opcache.validate_timestamps` PHP-inställning som standard i utvecklarläge. Om du aktiverar den här inställningen åtgärdas problemet där ändringar i filsystemet inte kändes igen i Docker.<!--MCLOUD-7466-->
- ![korrigeringsikon](../../assets/fix.svg) **Fast`build:custom:compose`**—Fixed the `build:custom:compose` om du vill generera ett fel när filer inte kan skrivas över under byggprocessen. Ett fel förhindrar situationer där `docker-compose up` kan använda fel filer.<!--MCLOUD-7457-->
- ![korrigeringsikon](../../assets/fix.svg) **Fast `--sync_engine="native"` option**—Ett problem har korrigerats där i produktionsläge (`--mode="production"`), `--sync_engine="native"` kan inte skapa poster för lokala mappar i `docker.composer.yml` -fil.<!--MCLOUD-7254-->
- ![korrigeringsikon](../../assets/fix.svg) **Verifieringsfel för tjänstversion har åtgärdats**—Tjänstversioner har lagts till för [!DNL RabbitMQ], Elasticsearch och andra tjänster till `type` -egenskapen i `MAGENTO_CLOUD_RELATIONSHIP` variabel. Lägga till dessa versioner i `relationships` variabeln åtgärdade de valideringsfel som inträffade under distributionsfasen.<!--MCLOUD-7572-->

## v1.2.1

Releasedatum: 21 december 2020

- ![ny ikon](../../assets/new.svg) **NGINX-kommandoalternativ**—Alternativ för byggkommandon har lagts till för att ändra antalet NGINX `worker_processes` och NGINX `worker_connections` för TLS och Web services. The `worker_process` parametern behåller möjligheten att ange värdet till `auto`. Exempel: <!--MCLOUD-7259-->

  ```terminal
  ./vendor/bin/ece-docker build:compose --nginx-worker-processes=2
  ./vendor/bin/ece-docker build:compose --nginx-worker-connections=2048
  ```

- ![ny ikon](../../assets/new.svg) **TLS, kommandoalternativ**—Lagt till kommandoalternativ för att skapa en konfiguration utan TLS-tjänsten. Exempel: <!--MCLOUD-7259-->

  ```terminal
  ./vendor/bin/ece-docker build:compose --no-tls
  ```

- ![ny ikon](../../assets/new.svg) **NGINX-minnesförbrukning**- Minskar mängden minne som NGINX-processen kräver för TLS och Web services.<!--MCLOUD-7259-->

- ![ny ikon](../../assets/new.svg) **Blackfire**—Inaktiverat PHP-tillägg för Blackfire som standard i molnavbildningen.

- ![korrigeringsikon](../../assets/fix.svg) **PHP-FPM-behållare**—PHP-FPM-behållarens hälsokontroll har åtgärdats genom ändring av `WEB_PORT` från `80` till `8080`.<!--MCLOUD-7232-->

- ![korrigeringsikon](../../assets/fix.svg) **Ogiltig volymnamngivning**—Ett fel med ogiltig volymnamngivning i utvecklarläge har korrigerats.<!--MCLOUD-7442-->

- ![korrigeringsikon](../../assets/fix.svg) **NGINX-port för övre ström**—Docker NGINX 1.19-bilden har uppdaterats för att använda port 8080 för att undvika en oändlig slinga. [Fix inskickad av Adarsh Manickam](https://github.com/magento/magento-cloud-docker/pull/296).<!--Issue 295-->

## v1.2.0

Releasedatum: 9 november 2020

- ![ny ikon](../../assets/new.svg) **Behållaruppdateringar—**

   - ![ny ikon](../../assets/new.svg) **PHP-FPM-behållare**- Stöd för GPU-tillägget har lagts till. [Korrigering från G Arvind från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/210).<!--MCLOUD-5981-->

   - ![korrigeringsikon](../../assets/fix.svg) **Databasbehållare**- Åtgärdade hälsokontrollen för databasbehållaren genom att lägga till det obligatoriska databaslösenordet till hälsokontrollskommandot.<!--MCLOUD-7122-->

   - ![ny ikon](../../assets/new.svg) **Elasticsearch container**

      - Stöd för Elasticsearch 7.9 har lagts till för kompatibilitet med kommande Adobe Commerce-versioner.<!--MCLOUD-7190-->

      - **Elasticsearch plug-in-konfiguration**—Stöd har lagts till för att använda konfigurationsinformation för plugin-programmet för Elasticsearch från `services.yaml` filen som ska generera `docker-compose.yaml` för en Cloud Docker för Commerce-miljö. Se [Elasticsearch plugins](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-plugins).<!--MCLOUD-2789-->

      - **Stöd för Elasticsearch-plugin**—Stöd för följande Elasticsearch-plugin-program har lagts till: `analysis-icu`, `analysis-phonetic`, `analysis-stempel`och `analysis-nori`. The `analysis-icu` och `analysis-phonetic` plugin-program installeras som standard. Du kan lägga till eller ta bort `analysis-stempel` och `analysis-nori` plugin-program efter behov.<!--MCLOUD-2789-->

   - ![ny ikon](../../assets/new.svg) **CLI-behållare**

      - **Kör kommandon i Docker PHP-behållare**- Nu kan du använda Cloud Docker CLI för att köra kommandon i PHP-behållare i Docker-miljön utan att behöva installera PHP på värden. Följande kommando skapar till exempel konfigurationen:  `./bin/magento-docker php 7.3 vendor/bin/ece-docker build:compose`. Se [Cloud Docker CLI](https://devdocs.magento.com/cloud/docker/docker-quick-reference.html#magento-cloud-docker-cli). [Korrigering från G Arvind från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/209).<!--MCLOUD-5982-->

      - OpenSSH-klienten har lagts till i PHP CLI-behållare. Nu kan du använda Ssh-agent-vidarebefordran för Composer om `composer.json` filen innehåller privata Git-databaser som kräver att en SSH-klient använder Composer-kommandon.<!--MCLOUD-6008-->

   - ![korrigeringsikon](../../assets/fix.svg) **TLS-behållare**—Nu finns [TLS-behållare](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) baseras på `https://hub.docker.com/r/magento/magento-cloud-docker-nginx` Dockerbild i stället för CentOS-bilden. Den här ändringen åtgärdar problem som orsakade fel när HTTPS-begäranden skickas mellan behållare i Cloud Docker-miljön.<!--MCLOUD-6469-->

   - ![ny ikon](../../assets/new.svg) **Testbehållare**—En testbehållare för programtestning har lagts till och `--with-test` till Docker `build:compose` om du bara vill skapa behållaren när du testar i Docker-miljön. Se [programtestning](https://devdocs.magento.com/cloud/docker/docker-test-app-mftf.html).<!--MCLOUD-6394-->

   - ![ny ikon](../../assets/new.svg) **FPM-XDEBUG-behållare**

      - ![ny ikon](../../assets/new.svg) **Konfigurera Xdebug i Linux**—Added the `--set-docker-host` till `ece-docker build:compose` konfigurera `host.docker.internal` i Xdebug-behållaren. Det här alternativet krävs för att använda Xdebug på Linux-system. Se [Konfigurera Xdebug för Docker](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-6430-->

      - ![korrigeringsikon](../../assets/fix.svg) Korrigerade Xdebug-variabelkonfigurationen för Docker ENTRYPOINT som ska matchas `uninitialized "with_xdebug" variable` fel i loggarna. [Fix inlämnat av Florent Olivaud](https://github.com/magento/magento-cloud-docker/pull/218)<!--MCLOUD-6043-->

- ![ny ikon](../../assets/new.svg) **Ändringar av dockningskonfiguration**

   - **MailHog-konfiguration**—Nu kan du använda följande `ece-docker build:compose` kommandoalternativ för att inaktivera MailHog och ange portar: `--no-mailhog`, `--mailhog-http-port`och `--mailhog-smtp-port`. Se [Konfigurera e-post](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-6898, MCLOUD-6660-->

   - För Cloud Docker för Commerce 1.2.0 och senare tillhandahåller Adobe nu Docker-bilder för varje korrigeringsversion, och Docker-konfigurationsgeneratorn skapar Docker-konfigurationen med en angiven korrigeringsversion i stället för att använda den senaste. Tidigare byggde Docker-konfigurationsgeneratorn konfigurationen med den senaste korrigeringsversionen som kunde bryta Cloud Docker för Commerce-miljöer som byggts med en tidigare version.<!--MCLOUD-7093-->

   - **Ange egna bilder och versioner i den anpassade konfigurationen för Cloud Docker**—Uppdaterade `build:custom:compose` med alternativ för att ange anpassade bilder och versioner när en anpassad Docker compose-konfigurationsfil skapas (`docker-compose.yaml`). Se [Skapa en anpassad Docker Compose-konfiguration](https://devdocs.magento.com/cloud/docker/docker-config-sources.html#build-a-custom-docker-compose-configuration). <!--MCLOUD-7089-->

   - Docker-värdkonfigurationen har uppdaterats så att port 443 exponeras för åtkomst till Adobe Commerce (`https://magento2.docker`) från alla CLI-behållare. Du kan ändra standardporten genom att lägga till `--tls-port` när du genererar Docker-konfigurationsfilen.<!--MCLOUD-6806-->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett problem som gjorde att molndockningsstationen för Commerce misslyckades om `app/etc/env.php` filen finns.<!--MCLOUD-6732-->

- ![korrigeringsikon](../../assets/fix.svg) Uppdaterade byggkonfigurationen för att ersätta namngivna volymer med vanliga volymer för att förhindra problem vid distribuering av Cloud Docker för Commerce i Linux eller Windows Subsystem för Linux (WSL2).<!--MCLOUD-6732-->

- ![korrigeringsikon](../../assets/fix.svg) Cloud Docker för Commerce-funktionstester har uppdaterats med stöd för Composer 2.0.<!--MCLOUD-7183-->

## v1.1.2

Releasedatum: 9 september 2020

- ![ny ikon](../../assets/new.svg) Stöd för Elasticsearch 7.7 har lagts till<!--MCLOUD-6219-->

## v1.1.1

Releasedatum: 5 augusti 2020

- ![korrigeringsikon](../../assets/fix.svg) **Uppdaterad e-postkonfiguration**- Uppdaterade standardkonfigurationen för Cloud Docker för Commerce så att den stöder tjänsten MailHog i stället för att använda SendMail. Se [Konfigurera e-post](https://devdocs.magento.com/cloud/docker/docker-config.html#set-up-email).<!--MCLOUD-5624-->

- ![korrigeringsikon](../../assets/fix.svg) PS-biblioteket återställdes till molndockningsmiljökonfigurationen för att åtgärda `ps:  command not found` fel.<!--MCLOUD-6621-->

- ![korrigeringsikon](../../assets/fix.svg) Uppdaterade standardkonfigurationen för Cloud Docker för Commerce för att ta bort automatisk montering av databasentrypoint och MariaDB-volymer för att korrigera `Cannot create container for service db` fel som kan inträffa när du startar Cloud Docker-miljön.

  Nu kan du konfigurera Cloud Docker-miljön för att montera databaskatalogerna genom att lägga till följande alternativ i `ece-docker build:compose` kommando: `--with-entry-point` och `with-mariadb-conf`. Se [Alternativ för tjänstkonfiguration](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-6424-->

- ![ny ikon](../../assets/new.svg) **CLI-kommandouppdateringar**

| Åtgärd | Kommando |
| ------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| Lägg till en startpunkt i databasbehållaren för att återställa databasen från en säkerhetskopia | `./vendor/bin/ece-docker build:compose --db --with-entrypoint` |
| Lägg till en MariaDB-konfigurationsvolym | `./vendor/bin/ece-docker build:compose --db --mariadb-conf` |

## v1.1.0

Releasedatum: 25 juni 2020

- ![ny ikon](../../assets/new.svg) **Stöd för den delade databasens prestandalösning har lagts till**- Nu kan du konfigurera och driftsätta en butik med prestandalösningen Delad databas i Cloud Docker-miljön.<!--MCLOUD-3740-->

- ![ny ikon](../../assets/new.svg) **Stöd för driftsättning av Adobe Commerce och Magento Open Source**- Nu kan du använda Cloud Docker för Commerce för att distribuera en lokal utvecklingsmiljö för projekt som inte ligger på Adobe Commerce i molninfrastruktur.<!--MCLOUD-5667-->

- ![ny ikon](../../assets/new.svg) **Stöd för Blackfire.io**—Stöd för användning av [Blackfire.io-tillägg](https://devdocs.magento.com/cloud/docker/docker-config-blackfire-io.html) för automatiserad prestandatestning. [Fix från Adarsh Manickam från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/202)<!--MCLOUD-5857-->

- ![ny ikon](../../assets/new.svg) **Behållaruppdateringar**

   - **Varnish**—Nu är lack standardcache när du distribuerar Adobe Commerce i en Cloud Docker-miljö med en version av molnprogrammallen som stöds. Se [Varnish-behållare](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container).<!--MCLOUD-2634-->

   - Lagt till `--no-varnish` om du vill hoppa över installationen av tjänsten lack när du genererar konfigurationsfilen för Cloud Docker.<!--MCLOUD-2634-->

   - ![ny ikon](../../assets/new.svg) **Databas**

      - Stöd för MySQL-databasen har lagts till. Nu kan du konfigurera molndockningsmiljön med MariaDB eller MySQL. Se [Alternativ för tjänstkonfiguration](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-configuration-options).<!--MCLOUD-5691-->

      - Lagt till möjlighet att ange inställningar för ökning och förskjutning för databasreplikering när du genererar Docker-dispositionsfilen. Se [Tjänstbehållare](https://devdocs.magento.com/cloud/docker/docker-containers.html#service-containers).<!--MCLOUD-5735-->

   - ![ny ikon](../../assets/new.svg) **PHP-FPM**

      - Stöd för PHP 7.4 har lagts till. [Fix från Mohanela Murugan från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/198)<!--MCLOUD-198-->

      - Lagt till möjlighet att kopiera en `php.ini` i rotprojektkatalogen i Cloud Docker-miljön och tillämpa anpassade PHP-inställningar på PHP-FPM- och CLI-behållarna. Se [Anpassa PHP-inställningar](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#customize-php-settings). [Fix som lämnats in av Mathew Beane från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/130).<!--MCLOUD-6012-->

      - En hälsokontroll för behållare har lagts till. [Fix inskickad av Visanth Sampath från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/188).<!--MCLOUD-5752-->

   - ![korrigeringsikon](../../assets/fix.svg) **Node.js**—Uppdaterade standardversionen av Node.js från version 8 till version 10 för att förbättra säkerheten. Node.js version 8 är inaktuell och inte längre uppdaterad med felkorrigeringar eller säkerhetspatchar. [Fix från Mohan Elamurgan från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/183).<!--MCLOUD-5586-->

   - ![ny ikon](../../assets/new.svg) **Elasticsearch**

      - Stöd för Elasticsearch 6.8, 7.2, 7.5 och 7.6 har lagts till.<!--MCLOUD-4050, MCLOUD-5855,MCLOUD-5860-->

      - Lagt till möjlighet att anpassa [Konfiguration av Elasticsearch-behållare](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) när du genererar Docker compose-konfigurationsfilen.<!--MCLOUD-3059-->

      - Lagt till `--no-es` alternativ för tjänstkonfigurationsalternativ för att generera konfigurationsfilen för Docker Compose. Använd det här alternativet om du vill hoppa över installationen av behållaren i Elasticsearch och använda MySQL-sökningen i stället. Det här alternativet stöds endast för Adobe Commerce version 2.3.5 och tidigare.<!--MCLOUD-3766-->

   - ![ny ikon](../../assets/new.svg) **FPM-XDEBUG-behållare**—Ett tjänstkonfigurationsalternativ har lagts till för att installera och konfigurera Xdebug för felsökning av PHP i molndockningsmiljön. Se [Konfigurera Xdebug](https://devdocs.magento.com/cloud/docker/docker-development-debug.html).<!--MCLOUD-4098-->

- ![ny ikon](../../assets/new.svg) **Ändringar av dockningskonfiguration**

   - Lagt till hälsokontroller för tjänstbehållarna PHP-FPM, Redis, Elasticsearch och MySQL Docker.<!--MCLOUD-3335 and MCLOUD-5856-->

   - Ändrade standardfilsynkroniseringsläget till `native` i utvecklarläge.<!--MCLOUD-3890 -->

   - Versionsinformation har lagts till i behållarbilden för den generiska Docker-tjänsten vid generering av `docker-compose.yml` -fil.<!--MCLOUD-3878-->

   - Förbättrade möjligheter att hantera stora svar från PHP-FPM-behållaren uppströms genom att öka `fastcgi_buffers` värdet för Nginx-servern.<!--MCLOUD-5980-->

   - Förbättrade prestanda för synkronisering av mutagena filer genom att lägga till en andra synkroniseringssession för att synkronisera filer i `vendor` katalog. Den här ändringen förhindrar att mutagen fastnar under filsynkroniseringsprocessen. [Fix som lämnats in av Mathew Beane från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

   - ![ny ikon](../../assets/new.svg) **CLI-kommandouppdateringar**

| Åtgärd | Kommando |
| -------- | --------------- |
| Rensa Redis-cache | `bin/magento-docker flush-redis` |
| Rensa lack-cache | `bin/magento-docker flush-varnish` |
| Hoppa över standardinstallation av lack | `.vendor/bin/ece-docker build:compose --no-varnish`<!--MCLOUD-2634--> |
| [Anpassa alternativ för Elasticsearch](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) | `.vendor/bin/ece-docker build:compose --es-env-var`<!--MCLOUD-3059--> |
| [Ta bort Elasticsearch-konfiguration](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#elasticsearch-container) | `.vendor/bin/ece-docker build:compose --no-es`<!--MCLOUD-3766--> |
| Konfigurera DB-behållare med MySQL version 5.6 eller 5.7 | `./vendor/bin/ece-docker build:compose --db <mysql-version-number> --db-image mysql`<!--MCLOUD-5691--> |
| Ange anpassad bas-URL | `./vendor/bin/ece-docker build:compose --host=<hostname> --port=<port-number>`<!--MCLOUD-3063--> |
| [Lägg till behållare för Xdebug-konfiguration](https://devdocs.magento.com/cloud/docker/docker-development-debug.html) | `.vendor/bin/ece-docker build:compose --mode developer --sync-engine native --with-xdebug`<!--MCLOUD-4098--> |

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade konfigurationen av synkronisering av mutagenfiler för att förhindra att mutagen skapar stale-sessioner. [Fix som lämnats in av Mathew Beane från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/127).<!--MCLOUD-6010-->

- ![korrigeringsikon](../../assets/fix.svg) Ett konfigurationsproblem som orsakade syntaxfel i Docker-dispositionsloggen när PHP-FPM-behållaren startades har åtgärdats. [Fix som lämnats in av Mathew Beane från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/129)<!--MCLOUD-3958-->

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade volymkonfliktsfel som ibland uppstod när flera Docker-miljöer användes. [Korrigering från G Arvind från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/168).

- ![korrigeringsikon](../../assets/fix.svg) Ett problem som orsakade `ece-docker build:compose` om konfigurationen innehåller Blackfire.io. [Korrigering från G Arvind från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/199). <!--MCLOUD-5797-->

- ![korrigeringsikon](../../assets/fix.svg) PHP CLI-bildkonfigurationen har uppdaterats för att förhindra fel av typen slut på minne som uppstod när flera paket installerades med Cloud Docker för Commerce. [Fix från Mohan Elamurgan från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/197).*<!--MCLOUD-5818-->

- ![korrigeringsikon](../../assets/fix.svg) Stöd för flera MySQL-användare i Cloud Docker-miljön har lagts till. I tidigare versioner finns `build:compose` åtgärden misslyckades om `magento.app.yaml` filen angav flera databasanvändare. [Korrigering från G Arvind från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/181).<!--MCLOUD-5670-->

- ![korrigeringsikon](../../assets/fix.svg) Borttagen `rsyslog` från PHP-behållarna i Cloud Docker för Commerce för att lösa kompatibilitetsproblem som orsakade varningsmeddelanden under distributionen. Cloud Docker använder inte rsyslog-verktyget.<!--MCLOUD-6173-->

## v1.0.0

Releasedatum: 5 feb 2020

- ![ny ikon](../../assets/new.svg) **Skapade ett separat paket att leverera`Cloud Docker for Commerce`**—Källkoden har flyttats för att leverera Cloud Docker för Commerce från `ece-tools` till [new `magento-cloud-docker` databas](https://github.com/magento/magento-cloud-docker) för att upprätthålla kodkvaliteten och tillhandahålla oberoende releaser. Det nya paketet är beroende av ECE-Tools v2002.1.0 och senare.

  När du uppdaterar hjälpverktygen uppdaterar du även `magento/magento-cloud-docker` till version 1.0.0. Om du använde Cloud Docker för Commerce med en tidigare version `ece-tools` version (2002.0.x), se [inkompatibiliteter bakåt](backward-incompatible-changes.md) och uppdatera projektet som skript, kommandon och processer efter behov.

- ![ny ikon](../../assets/new.svg) **Tillagd versionshantering för Docker-bilder**—Du måste nu uppdatera `magento/magento-cloud-docker` för att hämta uppdaterade bilder.<!--MAGECLOUD-4737-->

- ![ny ikon](../../assets/new.svg) **Behållaruppdateringar**—

   - ![ny ikon](../../assets/new.svg) **PHP-FPM-behållare**—

      - ![ny ikon](../../assets/new.svg) **Stöd för Node.js**—PHP-FPM-bilden har uppdaterats för att stödja nod, npm och de grymt-cli-funktioner som finns i PHP-behållaren.<!--MAGECLOUD-3953-->

      - ![ny ikon](../../assets/new.svg) **Stöd för [ionCube](https://www.ioncube.com/)**—Standardkonfigurationen för Docker har uppdaterats så att den stöder jonCube i den lokala Docker-utvecklingsmiljön.<!--MAGECLOUD-4354-->

   - ![ny ikon](../../assets/new.svg) **Webbbehållare**—

      - ![ny ikon](../../assets/new.svg) **Anpassa NGINX-konfiguration**—Möjligheten att montera en anpassad `nginx.conf` till Cloud Docker för Commerce-miljön. Se [Webbbehållare](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#web-container).<!--MAGECLOUD-4204-->

      - ![ny ikon](../../assets/new.svg) **Autogenererade NGINX-certifikat**- Docker-konfigurationsfilen innehåller nu konfigurationen för automatisk generering av NGINX-certifikat för webbbehållaren.<!--MAGECLOUD-4258-->

   - ![ny ikon](../../assets/new.svg) **Ny selenbehållare**—Added a [Selenummerbehållare](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#selenium-container) som har stöd för Adobe Commerce programtestning med Magento Functional Testing Framework (MFTF).<!--MAGECLOUD-4040-->

   - ![ny ikon](../../assets/new.svg) **[!DNL RabbitMQ]versionsstöd**—Uppdaterade [!DNL RabbitMQ] behållarkonfiguration som stöds [!DNL RabbitMQ] version 3.8.<!--MAGECLOUD-4674-->

   - ![korrigeringsikon](../../assets/fix.svg) **Beständig databasbehållare**—The `magento-db: /var/lib/mysql` databasvolymen kvarstår nu när du har stoppat och tagit bort Docker-konfigurationen och återställer när du startar om Docker-konfigurationen. Nu måste du ta bort databasvolymen manuellt. Se [Databasbehållare].<!--MAGECLOUD-3978-->

   - ![ny ikon](../../assets/new.svg) **TLS-behållare**—

      - ![ny ikon](../../assets/new.svg) **Behållarbasbilden har uppdaterats så att den officiella bilden används**—The [TLS-behållare i molnet](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#tls-container) bilden baseras nu på `debian:jessie` Dockerbild...<!--MAGECLOUD-4163-->

      - ![ny ikon](../../assets/new.svg) **Stöd för [Avbrottsproxy för Pound TLS]**—The [Pund konfigurationsfil](https://github.com/magento/magento-cloud-docker/blob/1.0/images/tls/) lägger till följande ENV-variabler för att anpassa Docker-konfigurationen för TLS-behållaren:

         - **`TimeOut`**- Anger tidsgränsen för TTFB (Time to First Byte). Standardvärdet är 300 sekunder.

         - **`RewriteLocation`**—Avgör om Pound-proxyn skriver om platsen till begärande-URL som standard. Standardvärdet är `0` för att förhindra att omskrivningen avbryter omdirigeringar till externa webbplatser som en extern SSO-plats. [Fix inskickad av Sorin Sugar](https://github.com/magento/magento-cloud-docker/pull/37)<!--MAGECLOUD-4061-->

      - ![ny ikon](../../assets/new.svg) Ökade timeout-värdet i TLS-behållarkonfigurationen från 15 till 300 sekunder. [Fix som lämnats in av Mathew Beane från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

   - ![ny ikon](../../assets/new.svg) **Varnish-behållare**—

      - ![ny ikon](../../assets/new.svg) **Behållarbasbilden har uppdaterats så att den officiella bilden används**—The [Cloud-lack-behållare](https://devdocs.magento.com/cloud/docker/docker-containers-service.html#varnish-container) baseras nu på `centos` Dockerbild.<!--MAGECLOUD-4163-->

      - ![ny ikon](../../assets/new.svg) **Förbättrad standardkonfiguration för timeout**-Added `.first_byte_timeout` och `.between_bytes_timeout` konfiguration till behållaren för lack. Standardvärdet för båda timeout-värdena är `300s` (5 minuter). [Fix som lämnats in av Mathew Beane från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/78)<!--MAGECLOUD-4460-->

      - ![korrigeringsikon](../../assets/fix.svg) **Hoppa över lack under Xdebug-sessioner**—Konfigurationen för behållaren i lack har uppdaterats för att returneras `pass` på begäranden som tas emot när Xdebug är aktiverat. I tidigare versioner gick det inte att använda Xdebug om Docker-miljön innehöll lack. [Fix som lämnats in av Mathew Beane från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/111).<!--MAGECLOUD-4873-->

- ![ny ikon](../../assets/new.svg) **Ändringar av dockningskonfiguration**—

   - ![ny ikon](../../assets/new.svg) **Hantera montage och volymer för ditt projekt**- Lagt till möjlighet att hantera berg och volymer när en Docker-miljö startas för lokal utveckling. Se [Dela projektdata].<!--MAGECLOUD-3248-->

   - ![ny ikon](../../assets/new.svg) **Stöd för nätverksbryggan**- Stöd för nätverksbryggan har lagts till för att möjliggöra anslutningar mellan Docker-behållare i det lokala nätverket.<!--MAGECLOUD-4165-->

   - ![ny ikon](../../assets/new.svg) **Kronbehållaren är inaktiverad som standard**- För att förbättra prestanda är Cron-behållaren inte längre konfigurerad som standard när du bygger Docker-miljön. Du kan använda `--with-cron` på Docker build-kommandot för att lägga till en Cron-behållare i miljön. Se [Hantera cron-jobb](https://devdocs.magento.com/cloud/docker/docker-manage-cron-jobs.html).<!--MAGECLOUD-5181-->

   - ![ny ikon](../../assets/new.svg) **Stoppa synkronisering av stora säkerhetskopior**—Tillagda DB-dumpar och arkivfiler - ZIP, SQL, GZ och BZ2 - har lagts till i exkluderingslistan i `dist/docker-sync.yml` och `dist/mutagen.sh` filer. Synkronisering av stora filer (>1 GB) kan orsaka en viss inaktivitet och säkerhetskopieringsfiler kräver normalt inte synkronisering eftersom du kan återskapa dem.<!--MAGECLOUD-3979-->

- ![ny ikon](../../assets/new.svg) **Kommandoändringar**—

   - ![korrigeringsikon](../../assets/fix.svg) Bytt namn på `./bin/docker` fil till `./bin/magento-docker` för att åtgärda ett problem som gjorde att vissa Docker-miljöer kraschade på grund av `./bin/docker` filen skriver över befintliga binära Docker-filer. Det här är en [inkompatibel ändring bakåt](backward-incompatible-changes.md) som kräver uppdateringar av skript och kommandon.<!-- MAGECLOUD-4038 -->

   - ![ny ikon](../../assets/new.svg) **Ett tjänstkonfigurationsalternativ har lagts till för att visa databasporten för värden**—Använd `--expose-db-port= [Fix submitted by Adarsh Manickam from Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/101).<PORT>` möjlighet att exponera databasporten för värddatorn när värddatorn skapas `docker-compose.yml` fil: `bin/ece-docker build:compose --expose-db-port=<PORT>`<!--MAGECLOUD-4454-->

   - ![ny ikon](../../assets/new.svg) **Nytt kommando för efterdistribution**—Tidigare var det de efterdistribuerade kopplingar som definierats i `.magento.app.yaml` filen kördes automatiskt när du distribuerade Adobe Commerce till en Cloud Docker-behållare med `cloud-deploy` -kommando. Nu måste du skapa en separat `cloud-post-deploy` om du vill köra hookarna efter distributionen. Se de uppdaterade startinstruktionerna för [utvecklare](https://devdocs.magento.com/cloud/docker/docker-mode-developer.html) och [produktion](https://devdocs.magento.com/cloud/docker/docker-mode-production.html) läge.<!--MAGECLOUD-3996-->

   - ![ny ikon](../../assets/new.svg) Lagt till `--rm` alternativ till `./bin/magento-docker` -kommandon för byggbehållarna och distributionsbehållarna. Behållaren tas bort när uppgiften är klar.<!--MAGECLOUD-4205-->

   - ![ny ikon](../../assets/new.svg) **Uppdateringar till `build:compose` kommando**—

      - ![ny ikon](../../assets/new.svg) Lagt till `--sync-engine="native"` till `docker-build` om du vill inaktivera filsynkronisering när du genererar Docker Compose-konfigurationsfilen i utvecklarläge. Använd det här alternativet när du utvecklar på Linux-system, som inte kräver filsynkronisering för lokal Docker-utveckling. Se [Synkronisera data i Docker-miljön](https://devdocs.magento.com/cloud/docker/docker-syncing-data.html).<!--MCLOUD-3231, MCLOUD-3890-->

   - ![ny ikon](../../assets/new.svg) Ändrade standardinställningen för filsynkronisering från `docker-sync` till `native`. [Fix som lämnats in av Mathew Beane från Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/124).<!--MAGECLOUD-5066-->

- ![ny ikon](../../assets/new.svg) **Förbättrad validering**—

   - ![ny ikon](../../assets/new.svg) Valideringen har lagts till i distributionsprocessen för lokala Docker-utvecklingsmiljöer för att verifiera att molnmiljökonfigurationen innehåller den krypteringsnyckel som krävs för att dekryptera databasen. Du får nu ett felmeddelande i loggen om miljökonfigurationen inte anger något värde för krypteringsnyckeln.<!--MAGECLOUD-4423-->

   - ![ny ikon](../../assets/new.svg) En hälsokontroll för behållaren har lagts till i tjänsten Elasticsearch för att säkerställa att tjänsten är klar innan du fortsätter med bearbetningen av bygget och distributionen. Om hälsokontrollen returnerar ett fel startar behållaren om automatiskt.<!--MAGECLOUD-4456-->
