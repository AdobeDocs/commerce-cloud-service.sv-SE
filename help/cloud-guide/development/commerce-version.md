---
title: Uppgradera Commerce-version
description: Lär dig hur du uppgraderar Adobe Commerce-versionen i molninfrastrukturprojektet.
feature: Cloud, Upgrade
exl-id: 87821007-4979-4a20-940b-aa3c82c192d8
source-git-commit: 99272d08a11f850a79e8e24857b7072d1946f374
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Uppgradera Commerce-version

Du kan uppgradera Adobe Commerce kodbas till en nyare version. Innan du uppgraderar ditt projekt bör du granska [Systemkrav](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) i _Installation_ för de senaste versionskraven.

Beroende på din projektkonfiguration kan din uppgradering innehålla följande:

- Uppdateringstjänster - som MariaDB (MySQL), OpenSearch, RabbitMQ och Redis - för kompatibilitet med nya Adobe Commerce-versioner.
- Konvertera en äldre konfigurationshanteringsfil.
- Uppdatera `.magento.app.yaml` fil med nya inställningar för krokar och miljövariabler.
- Uppgradera tillägg från tredje part till den senaste version som stöds.
- Uppdatera `.gitignore` -fil.

{{upgrade-tip}}

{{pro-update-service}}

## Uppgradera från äldre versioner

Om du påbörjar en uppgradering från en Commerce-version som är äldre än 2.1 kan vissa begränsningar i Adobe Commerce kodbas påverka din förmåga att _uppdatera_ till en särskild ECE-verktygsrelease eller till _uppgradera_ till nästa version av Commerce som stöds. Använd följande tabell för att fastställa den bästa banan:

| Aktuell version | Uppgraderingssökväg |
| ----------------- | ------------ |
| 2.1.3 och tidigare versioner | Uppgradera Adobe Commerce till version 2.1.4 eller senare innan du fortsätter. Utför sedan en [engångsuppgradering för att installera ECE-Tools](../dev-tools/install-package.md). |
| 2.1.4 - 2.1.14 | [Uppdatera ECE-verktyg](../dev-tools/update-package.md) paket.<br>Se versionsinformation för [2002.0.9](../release-notes/cloud-release-archive.md#v200209) och senare versioner 2002.0.x. |
| 2.1.15 - 2.1.16 | [Uppdatera ECE-verktyg](../dev-tools/update-package.md) paket.<br>Se versionsinformation för[2002.0.9](../release-notes/cloud-release-archive.md#v200209) och senare. |
| 2.2.x och senare | [Uppdatera ECE-verktyg](../dev-tools/update-package.md) paket.<br>Se versionsinformation för[2002.0.8](../release-notes/cloud-release-archive.md#v200208) och senare. |

{style="table-layout:auto"}

{{ece-tools-package}}

## Konfigurationshantering

Äldre versioner av Adobe Commerce, som 2.1.4 eller senare till 2.2.x eller senare, använde en `config.local.php` fil för Configuration Management. Adobe Commerce version 2.2.0 och senare använder `config.php` -filen, som fungerar exakt som `config.local.php` -filen, men den har olika konfigurationsinställningar som innehåller en lista över dina aktiverade moduler och ytterligare konfigurationsalternativ.

När du uppgraderar från en äldre version måste du migrera `config.local.php` filen som ska användas i det nyare `config.php` -fil. Gör så här för att säkerhetskopiera konfigurationsfilen och skapa en.

**Skapa en tillfällig `config.php` fil**:

1. Skapa en kopia av `config.local.php` fil och namnge den `config.php`.

1. Lägg till den här filen i `app/etc` projektmapp.

1. Lägg till och implementera filen på din gren.

1. Skicka filen till din integrationsgren.

1. Fortsätt med uppgraderingsprocessen.

>[!WARNING]
>
>Efter uppgraderingen kan du ta bort `config.php` och generera en ny, fullständig fil. Du kan bara ta bort den här filen om du vill ersätta den här gången. När en ny, fullständig `config.php` kan du inte ta bort filen för att skapa en ny. Se [Konfigurationshantering och distribution av pipeline](../store/store-settings.md).

### Verifiera Zend Framework Composer-beroenden

Vid uppgradering till **2.3.x eller senare från 2.2.x**, verifiera att Zend Framework-beroenden har lagts till i `autoload` egenskapen för `composer.json` som stöder Laminas. Denna plugin stöder nya krav för Zend Framework, som har migrerat till Laminas-projektet. Se [Migrering av Zend Framework till Laminas Project](https://community.magento.com/t5/Magento-DevBlog/Migration-of-Zend-Framework-to-the-Laminas-Project/ba-p/443251) på _Magento DevBlog_.

**För att kontrollera `auto-load:psr-4` konfiguration**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Ta en titt på er integreringsgren.

1. Öppna `composer.json` i en textredigerare.

1. Kontrollera `autoload:psr-4` för Zend plugin-hanterarimplementeringen för styrenheternas beroende.

   ```json
    "autoload": {
       "psr-4": {
          "Magento\\Framework\\": "lib/internal/Magento/Framework/",
          "Magento\\Setup\\": "setup/src/Magento/Setup/",
          "Magento\\": "app/code/Magento/",
          "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
       },
   }
   ```

1. Om Zend-beroendet saknas uppdaterar du `composer.json` fil:

   - Lägg till följande rad i `autoload:psr-4` -avsnitt.

     ```json
     "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
     ```

   - Uppdatera projektberoenden.

     ```bash
     composer update
     ```

   - Lägg till, implementera och push-ändra kod.

     ```bash
     git add -A
     ```

     ```bash
     git commit -m "Add Zend plugin manager implementation for controllers dependency for Laminas support"
     ```

     ```bash
     git push origin <branch-name>
     ```

   - Sammanfoga ändringarna i mellanlagringsmiljön och sedan till Produktion.

## Konfigurationsfiler

Innan du uppgraderar programmet måste du uppdatera dina projektkonfigurationsfiler så att de tar hänsyn till ändringar av standardkonfigurationsinställningarna för Adobe Commerce i molninfrastrukturen eller för programmet. De senaste standardinställningarna finns i [magento-cloud GitHub-databas](https://github.com/magento/magento-cloud).

### .magento.app.yaml

Granska alltid värdena i [.magento.app.yaml](../application/configure-app-yaml.md) -filen för den installerade versionen eftersom den styr hur ditt program bygger och distribuerar till molninfrastrukturen. Följande exempel är för version 2.4.7 och använder Composer 2.7.2. The `build: flavor:` egenskapen används inte för Composer 2.x; se [Installera och använda Composer 2](../application/properties.md#installing-and-using-composer-2).

**Uppdatera `.magento.app.yaml` fil**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Öppna och redigera `magento.app.yaml` -fil.

1. Uppdatera PHP-alternativen.

   ```yaml
   type: php:8.3
   
   build:
       flavor: none
   dependencies:
       php:
           composer/composer: '2.7.2'
   ```

1. Ändra `hooks` property `build` och `deploy` kommandon.

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           composer install
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. Lägg till följande miljövariabler i slutet av filen.

   För Adobe Commerce 2.2.x till 2.3.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

   För Adobe Commerce 2.4.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

1. Spara filen. Verkställ eller skicka inga ändringar till fjärrmiljön än.

1. Fortsätt med uppgraderingsprocessen.

### composer.json

Kontrollera alltid att beroendena i `composer.json` filen är kompatibel med Adobe Commerce.

**Uppdatera `composer.json` för Adobe Commerce version 2.4.4 och senare**:

1. Lägg till följande `allow-plugins` till `config` avsnitt:

   ```json
   "config": {
      "allow-plugins": {
         "dealerdirect/phpcodesniffer-composer-installer": true,
         "laminas/laminas-dependency-plugin": true,
         "magento/*": true
      }
   },
   ```

1. Lägg till följande plugin-program i `require` avsnitt:

   ```json
   "require": {
       "magento/composer-root-update-plugin": "^2.0.3"
   },
   ```

1. Lägg till följande komponent i `extra:component_paths` avsnitt:

   ```json
   "extra": {
      "component_paths": {
         "tinymce/tinymce": "lib/web/tiny_mce_5"
      },
   },
   ```

1. Spara filen. Verkställ eller skicka inte ändringar till din gren än.

1. Fortsätt med uppgraderingsprocessen.

## Säkerhetskopiering av projekt

Vi rekommenderar att du skapar en säkerhetskopia av ditt projekt före en uppgradering. Gör så här för att säkerhetskopiera integrerings-, mellanlagrings- och produktionsmiljöer.

**Säkerhetskopiera databasen och koden för integreringsmiljön**:

1. Skapa en lokal säkerhetskopia av fjärrdatabasen.

   ```bash
   magento-cloud db:dump
   ```

   >[!NOTE]
   >
   >The `magento-cloud db:dump` kommandot kör [mysqldump](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) med kommandot `--single-transaction` -flagga som gör att du kan säkerhetskopiera databasen utan att låsa tabellerna.

1. Säkerhetskopiera kod och media.

   ```bash
   php bin/magento setup:backup --code [--media]
   ```

   Du kan också utelämna `[--media]` om du har ett stort antal statiska filer som redan finns i källkontrollen.

**Så här säkerhetskopierar du databasen för förproduktionsmiljö eller produktionsmiljö innan du distribuerar**:

1. Använd SSH för att logga in i fjärrmiljön.

1. Skapa en [databasdump](../storage/database-dump.md). Om du vill välja en målkatalog för databasdumpen använder du `--dump-directory` alternativ.

   ```bash
   vendor/bin/ece-tools db-dump
   ```

   Dumpningsåtgärden skapar en `dump-<timestamp>.sql.gz` arkivera filen i din fjärrprojektkatalog. Se [Säkerhetskopiera databas](../storage/database-dump.md).

## Programuppgradering

Granska [tjänsteversioner](../services/services-yaml.md#service-versions) information om de senaste versionskraven innan du uppgraderar programmet.

**Så här uppgraderar du programversionen**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Ange uppgraderingsversionen med [versionsbegränsningssyntax](overview.md#cloud-metapackage).

   ```bash
   composer require "magento/magento-cloud-metapackage":">=CURRENT_VERSION <NEXT_VERSION" --no-update
   ```

   >[!NOTE]
   >
   >Du måste använda versionsbegränsningssyntaxen för att kunna uppdatera `ece-tools` paket. Versionsbegränsningen finns i `composer.json` -fil för versionen av [programmall](https://github.com/magento/magento-cloud/blob/master/composer.json) som du använder för uppgraderingen.

1. Uppdatera projektet.

   ```bash
   composer update
   ```

1. Lägg till, implementera och push-ändra kod.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Upgrade"
   ```

   ```bash
   git push origin <branch-name>
   ```

   `git add -A` måste lägga till alla ändrade filer i källkontrollen på grund av hur Composer konverterar baspaket. Båda `composer install` och `composer update` konvertera filer från baspaketet (`magento/magento2-base` och `magento/magento2-ee-base`) till paketroten.

   De filer som Composer konverterar tillhör den nya versionen av Adobe Commerce, som skriver över den gamla versionen av samma filer. För närvarande är konvertering inaktiverat i Adobe Commerce, så du måste lägga till de konverterade filerna i källkontrollen.

1. Vänta tills distributionen är klar.

1. Verifiera uppgraderingen i integrerings-, mellanlagrings- eller produktionsmiljön genom att använda SSH för att logga in och kontrollera versionen.

   ```bash
   php bin/magento --version
   ```

### Skapa filen config.php

Som anges i [Konfigurationshantering](#configuration-management)måste du skapa en uppdaterad `config.php` -fil. Slutför eventuella ytterligare konfigurationsändringar via administratören i din integreringsmiljö.

**Skapa en systemspecifik konfigurationsfil**:

1. Använd ett SSH-kommando från terminalen för att generera `/app/etc/config.php` för miljön.

   ```bash
   ssh <SSH-URL> "<Command>"
   ```

   För Pro kör du `scd-dump` på `integration` gren:

   ```bash
   ssh <project-id-integration>@ssh.us.magentosite.cloud "php vendor/bin/ece-tools config:dump"
   ```

1. Överför `config.php` till dina lokala arbetsstationer med `rsync` eller `scp`. Du kan bara lägga till den här filen lokalt i grenen.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Lägg till, implementera och push-ändra kod.

   ```bash
   git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
   ```

   Detta genererar en uppdaterad `/app/etc/config.php` med en modullista och konfigurationsinställningar.

>[!WARNING]
>
>För en uppgradering tar du bort `config.php` -fil. När den här filen har lagts till i koden bör du **not** ta bort den. Om du måste ta bort eller redigera inställningar redigerar du filen manuellt.

### Uppgradera tillägg

Granska tillägg- och modulsidor från tredje part på Marketplace eller andra företagswebbplatser och verifiera stödet för Adobe Commerce och Adobe Commerce i molninfrastrukturen. Om du måste uppgradera tillägg och moduler från tredje part rekommenderar Adobe att du arbetar i en ny integreringsgren med dina tillägg inaktiverade.

**Verifiera och uppgradera dina tillägg**:

1. Skapa en gren på din lokala arbetsstation.

1. Inaktivera tilläggen efter behov.

1. Ladda ned tilläggsuppgraderingar när de blir tillgängliga.

1. Installera uppgraderingen enligt dokumentationen från tredje part.

1. Aktivera och testa tillägget.

1. Lägg till, implementera och skicka kodändringarna till fjärrkontrollen.

1. Kör till och testa i er integreringsmiljö.

1. Kör till mellanlagringsmiljön för att testa i en förproduktionsmiljö.

Adobe rekommenderar starkt att du uppgraderar din produktionsmiljö _före_ inkluderar de uppgraderade tilläggen i webbplatsens startprocess.

>[!NOTE]
>
>När du uppgraderar din programversion uppdateras uppgraderingsprocessen till den senaste versionen av [Snabb CDN-modul](../cdn/fastly.md#fastly-cdn-module-for-magento-2) automatiskt.

## Felsök uppgraderingen

Om uppgraderingen misslyckades får du ett felmeddelande i webbläsaren om att du inte kan komma åt butiken eller administrationspanelen:

```terminal
There has been an error processing your request
Exception printing is disabled by default for security reasons.
  Error log record number: <error-number>
```

**Lös felet**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Använd SSH för att logga in i fjärrmiljön.

   ```bash
   magento-cloud ssh
   ```

1. Öppna `./app/var/report/<error number>` -fil.

1. [Granska loggarna](../test/log-locations.md) och fastställa orsaken till problemet.

1. Lägg till, implementera och push-ändra kod.

   ```bash
   git add -A && git commit -m "Fixed deployment failure" && git push origin <branch-name>
   ```
