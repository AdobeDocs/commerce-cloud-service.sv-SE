---
title: Bakåtkompatibla ändringar
description: Lär dig mer om bakåtkompatibilitet när du uppgraderar befintliga Cloud-projekt.
feature: Cloud, Release Notes
recommendations: noDisplay, catalog
exl-id: 9847c565-6d59-429a-9593-c2eba5cf2da4
source-git-commit: f9edcc85c14354a2eddacbc5219557e107a367cb
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 0%

---

# Bakåtkompatibla ändringar

Bakåtkompatibla ändringar kan kräva att du justerar molnkonfigurationen och processerna för befintliga Cloud-projekt när du uppgraderar till den senaste versionen av `ece-tools` paket eller andra Cloud Tools Suite för Commerce-paket.

## Ändrar till `ece-tools` package

Vissa funktioner som tidigare fanns i `ece-tools` paketet finns nu i separata paket. Dessa paket är dispositionsberoenden för `ece-tools`, som installeras och uppdateras automatiskt när du installerar eller uppdaterar verktyg.

Den nya arkitekturen bör inte påverka installations- eller uppdateringsprocesserna. Du kan dock behöva ändra vissa kommandosyntaxer och processer när du arbetar med ditt Adobe Commerce i ett molninfrastrukturprojekt. Mer information finns i följande bakåtkompatibla ändringsinformation och [Versionsinformation om Cloud Tools Suite](cloud-tools-suite.md).

### Ändringar av tjänstens versionskrav

Vi ändrade minimikravet för PHP-version från 7.0.x till 7.1.x för molnprojekt som använder `ece-tools` v2002.1.0 och senare. Om din miljökonfiguration anger PHP 7.0 ska du uppdatera [php-konfiguration](../application/php-settings.md) i `.magento.app.yaml` -fil.

>[!WARNING]
>
>På grund av ändringen av PHP-versionskraven `ece-tools` 2002.1.0 stöder endast Adobe Commerce i molninfrastrukturprojekt som kör Adobe Commerce 2.1.15 eller senare. Om projektet använder en tidigare version måste du [uppgradera](../development/commerce-version.md) innan du uppdaterar till `ece-tools` 2002.1.0.

### Ändringar av miljökonfiguration

Följande tabell innehåller information om miljövariabler och andra konfigurationsfiler som har tagits bort eller tagits bort i `ece-tools` v2002.1.0.

| Objekt | Ersättning |
| -------- | ----------- |
| `SCD_EXCLUDE_THEMES` variabel | [`SCD_MATRIX`](../environment/variables-build.md#scd_matrix) |
| `STATIC_CONTENT_THREADS` variabel | [`SCD_THREADS`](../environment/variables-build.md#scd_threads) |
| `DO_DEPLOY_STATIC_CONTENT` variabel | [`SKIP_SCD`](../environment/variables-build.md#skip_scd) |
| `STATIC_CONTENT_SYMLINK` variabel | Ingen. Nu skapas alltid en länk till den statiska innehållskatalogen `pub/static`. |
| `build_options.ini` fil | Använd [`.magento.env.yaml`](../application/configure-app-yaml.md) för att konfigurera miljövariabler för att hantera bygg- och distributionsåtgärder i alla miljöer.<p>Om du bygger en molnmiljö som innehåller `build_options.ini` filen, bygget misslyckas. |

### Ändringar av CLI-kommandon

Följande tabell sammanfattar ändringar av CLI-kommandon i ECE-Tools v2002.1.0 som kan kräva att du uppdaterar kommandon eller skript.

| Kommando | Ersättning |
|-------- | ----------- |
| `m2-ece-build` | `vendor/bin/ece-tools build` |
| `m2-ece-deploy` | `vendor/bin/ece-tools deploy` |
| `m2-ece-scd-dump` | `vendor/bin/ece-tools config:dump` |
| `vendor/bin/ece-tools patch` | `vendor/bin/ece-patches apply` |
| `vendor/bin/ece-tools docker:build` | `vendor/bin/ece-docker build:compose` |
| `vendor/bin/ece-tools docker:config:convert` | `vendor/bin/ece-docker  image:generate:php` |

I tidigare versioner av ECE-Tools kunde du använda `m2-ece-build` och `m2-ece-deploy` kommandon för att konfigurera distributionsnätverk i `.magento.app.yaml` -fil. När du uppdaterar till v2002.1.0 ska du kontrollera `hooks` i `.magento.app.yaml` för de föråldrade kommandona och ersätt dem vid behov.

## Ändringar av molnkorrigeringar

- **Ta bort hämtade patchar**-The `magento/magento-cloud-patches` paketera alla patchar som finns på [programvarunedladdningar](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/commerce.html) och använder dem automatiskt när du distribuerar till molnet. För att förhindra korrigeringskonflikter efter uppgradering till ECE-Tools 2002.1.0 eller senare, tar du bort eventuella patchar som du laddat ned och lagt till manuellt i ditt projekt.

- **Uppdatera kommandot Tillämpa korrigeringar**-Vi har flyttat kommandot för att använda korrigeringar från `vendor/bin/ece-tools` till `vendor/bin/ece-patches` katalog. Om du använder det här kommandot för att tillämpa korrigeringar manuellt använder du den nya sökvägen.

  > Tillämpa korrigeringar manuellt

  ```bash
  php ./vendor/bin/ece-patches apply
  ```

## Ändringar av Cloud Docker

- **Kravet på lägsta PHP-version är nu PHP 7.1**-Om din Cloud Docker för Commerce-värd kör en tidigare version uppgraderar du till PHP v7.1 eller senare.

- **Kommandoändringar för Cloud Docker för Commerce**-

   - **Uppdaterar molndockning för Commerce-kommandon för Docker-byggåtgärder**-Vi har flyttat kommandona för Cloud Docker för Commerce från `vendor/bin/ece-tools` till `vendor/bin/ece-docker` katalog. Uppdatera skript och kommandon så att de använder den nya sökvägen.

     Efter uppgradering till `ece-tools` 2002.1.0 använder du följande kommando för att visa tillgängliga `ece-docker` kommandon.

     ```bash
     php ./vendor/bin/ece-docker list
     ```

   - **Uppdatera kommandon för Cloud Docker-compose**-Sökvägen till kommandofilen har ändrats från `./bin/docker` till `./bin/magento-docker`. Uppdatera skript och kommandon så att de använder den nya sökvägen.

   - **Kronbehållaren ingår inte längre i standardkonfigurationen för Docker**-Nu måste du lägga till `--with-cron` till `ece-docker build:compose` om du vill inkludera Cron-behållaren i Docker-miljökonfigurationen. Se [Hantera cron-jobb](https://developer.adobe.com/commerce/cloud-tools/docker/configure/manage-cron-jobs/) i _Cloud Docker for Commerce_ guide.

     Skript som tidigare genererade behållare med cron-jobb är nu utan cron-behållare.

   - **Använda tillfälliga behållare**-I tidigare versioner skapades behållare av `bin/magento-docker` kommandoåtgärder togs inte bort, så du kunde använda dem för andra åtgärder. Nu `magento-docker` kommandon tar bort alla behållare som de skapar när kommandot har slutförts.

     Om du vill behålla en behållare som skapats med en Docker-compose-åtgärd använder du kommandot `docker-compose run` i stället för `bin/magento-docker` -kommando.

   - **Köra kopplingar efter driftsättning**-The `cloud-deploy` kommandot kör inte längre kopplingar efter distribution. Använd den nya `cloud-post-deploy` för att köra hooks efter driftsättningen. Uppdatera skripten och lägg till kommandot för att köra kopplingar efter distributionen.

     ```shell
     bin/magento-docker ece-deploy
     bin/magento-docker ece-post-deploy
     ```

     Om du använder `docker-compose` direkt, köra `docker-compose run deploy cloud-post-deploy` efter kommandot deploy.

- **Uppdaterar databasen**-Databasbehållaren lagras nu i `magento-db` beständig dockningsvolym. När du uppdaterar Docker-miljön tas databasen inte längre bort automatiskt. Om det behövs kan du ta bort det manuellt med något av följande kommandon.

   - Ta bort `magento-db` container:

     ```bash
     docker volume rm magento-db
     ```

   - Ta bort alla associerade volymer när du stänger av Docker-behållarna:

     ```bash
     docker-compose down -v
     ```

- **Åsidosätt filsynkroniseringsinställningar för arkiv och säkerhetskopior**-Arkivera och säkerhetskopiera filer med följande tillägg synkroniseras inte längre när du använder Dcker-sync eller mutagen: SQL, GZ, ZIP och BZ2. Du kan åsidosätta standardfilsynkroniseringen för dessa filtyper genom att byta namn på filen så att den slutar med ett annat filtillägg. Till exempel: `synchronize-me.zip-backup`
