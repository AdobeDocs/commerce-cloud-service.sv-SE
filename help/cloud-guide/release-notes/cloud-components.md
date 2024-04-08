---
title: Cloud Components for Commerce
description: Se en lista med de senaste förbättringarna av Cloud Components-paketet.
recommendations: noDisplay, catalog
exl-id: b4e2508a-3558-4fa8-bae0-3eb76c7b2775
source-git-commit: c02dfd2709cdc63ac1630edaa8c89cad5f737ea1
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# Cloud Components for Commerce

The [Molnkomponenter](https://github.com/magento/magento-cloud-components) paket innehåller utökad Adobe Commerce-funktionalitet för webbplatser som körs i molninfrastrukturen. Detta paket är beroende av ECE-verktygspaketet. I versionsinformationen beskrivs de senaste förbättringarna av det här paketet, som är en komponent i [Cloud Tools Suite for Commerce](cloud-tools-suite.md).

The `magento/magento-cloud-components` paketet använder följande versionssekvens: `<major>.<minor>.<patch>`

Versionsinformationen innehåller:

- ![ny ikon](../../assets/new.svg) Nya funktioner
- ![korrigeringsikon](../../assets/fix.svg) Korrigeringar och förbättringar

<!--Add release notes below-->

## v1.0.14 {#latest}

Releasedatum: 8 april 2024

- ![ny ikon](../../assets/new.svg) **PHP** - Stöd för PHP 8.3 har lagts till.

## v1.0.13

Releasedatum: 10 mars 2023

- ![ny ikon](../../assets/new.svg) **Förbättrat stöd för PHP 8.2**—Korrigerade kompatibilitetsproblem med vissa PHP 8.2.x-versioner som stöder Commerce 2.4.6.

## v1.0.12

Releasedatum: 13 september 2022

- ![korrigeringsikon](../../assets/fix.svg) **Fel vid uppvärmning**—Ett problem som försökte åtgärdas har korrigerats [värma](../environment/variables-post-deploy.md#warm_up_pages) när sidsynligheten är inställd på [**Inte synlig enskilt**](https://docs.magento.com/user-guide/system/data-attributes-product.html#simple-product-csv-file-structure) i Admin, vilket resulterar i `ERROR: Warming up failed: <link to page>` fel i distributionsloggen.<!-- MCLOUD-9134 -->

## v1.0.11

Releasedatum: 4 augusti 2022

- ![korrigeringsikon](../../assets/fix.svg) **Stöd för Symfony 5.4-kompatibilitet har lagts till**—Fixes for compatibility with Symfony 5.4.<!-- AC-3550 -->

## v1.0.10

Releasedatum: 10 mars 2022

- ![ny ikon](../../assets/new.svg) **Stöd för PHP 8.1**- Stöd för PHP 8.1 har lagts till och stödet för PHP 7.1 har tagits bort.

## v1.0.9

Releasedatum: 25 oktober 2021

- ![korrigeringsikon](../../assets/fix.svg) **Uppdatera Monolog**—Uppdaterat minimiversionen som krävs för `monolog` paketera till `^2.3`.<!-- ACMP-1263 -->

## v1.0.8

Releasedatum: 29 juli 2021

- ![korrigeringsikon](../../assets/fix.svg) **Borttagen avslutande snedstreck från autogenererade URL:er**—De avslutande snedstrecken från URL:er för kategorisidor som genererades när cacheminnet skulle värmas har tagits bort.<!--MCLOUD-7192-->

## v1.0.7

Releasedatum: 9 september 2020

- ![ny ikon](../../assets/new.svg) **Förbättrad loggning**—Minska storleken på `cache.log` för att förbättra prestandan.<!--MCLOUD-6859-->

- ![korrigeringsikon](../../assets/fix.svg) Ett typfel i de cachekonfigurationsvärden som orsakade `php bin/magento cache:evict` CLI-kommandot misslyckas.

## v1.0.6

Releasedatum: 5 augusti 2020

- ![ny ikon](../../assets/new.svg) **Förbättra Redis prestanda**—Added the `./bin/magento cache:evict` för att ta bort utgångna Redis-nycklar, vilket minskar Redis-minnesanvändningen för att förbättra prestandan.<!--MCLOUD-6023-->

- ![korrigeringsikon](../../assets/fix.svg) Borttaget stöd för *New Relic Loggar in Context* för att åtgärda ett prestandaproblem.<!--MCLOUD-6422-->

## v1.0.5

Releasedatum: 25 juni 2020

- ![korrigeringsikon](../../assets/fix.svg) Korrigerade ett fel som introducerades i magento/magento-cloud-components version 1.0.4 som gjorde att flush-cacheåtgärden misslyckades under distributionsfasen, vilket avbröt distributionsprocessen.

## v1.0.4

Releasedatum: 25 juni 2020

- ![ny ikon](../../assets/new.svg) **Implementerade New Relic Logs in Context**- Programloggar som genererats av Adobe Commerce visas nu i spår i New Relic för att förbättra felsökningsfunktionerna.<!--MCLOUD-6029-->

- ![ny ikon](../../assets/new.svg) **Förbättrad loggning**- Loggning har lagts till för att spåra cacheogiltigförklaring och fullständiga indexeringshändelser.<!--MCLOUD-6157-->

## v1.0.3

Releasedatum: 27 februari 2020

- ![korrigeringsikon](../../assets/fix.svg) Korrigerat ett kompatibilitetsproblem som ska stödjas `ece-tools` 2002.0.x-versioner som använder äldre PHP-versioner.

## v1.0.2

Releasedatum: 6 februari 2020

- ![ny ikon](../../assets/new.svg) Utökade funktioner för `WARM_UP_PAGES` systemvariabel som stöder cacheförinläsning för specifika produktsidor. Se [variabler efter distribution](../environment/variables-post-deploy.md#warm_up_pages) om du vill ha en detaljerad funktionsbeskrivning.<!--MAGECLOUD-4444-->

- ![korrigeringsikon](../../assets/fix.svg) Ett problem har korrigerats där en ogiltig arkiv-URL gör att kroken efter distributionen misslyckas när `WARM_UP_PAGES` för att fylla i cachen. Problemet uppstod bara när URL-omskrivning inaktiverades.<!-- MAGECLOUD-4094 -->

## v1.0.1

Releasedatum: 23 juli 2019

- ![korrigeringsikon](../../assets/fix.svg) Ett problem som påverkade har åtgärdats [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) funktioner som använder en standard-webblänk. Om `config:show:default-url` det går inte att hämta en bas-URL, används URL:en från variabeln MAGENTO_CLOUD_ROUTES.<!-- MAGECLOUD-3866 -->

## v1.0.0

Releasedatum: 12 juni 2019

Detta är den första versionen av [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components) paket, som är ett nytt beroende för `ece-tools` paketversion 2002.0.20 och senare.

- ![ny ikon](../../assets/new.svg) Lagt till funktioner för att använda regex-mönster för att konfigurera **WARM_UP_PAGES** systemvariabel för cache-lagring av enstaka sidor, flera domäner och flera sidor. Se [Variabler efter distribution](../environment/variables-post-deploy.md#warm_up_pages).<!--MAGECLOUD-3258-->
