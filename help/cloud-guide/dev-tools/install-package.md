---
title: Uppgradera projekt till ECE-Tools
description: Lär dig hur du uppgraderar din Adobe Commerce i molninfrastrukturprojekt så att du kan använda ECE-verktygspaketet och dra nytta av de senaste fixarna och funktionerna.
feature: Cloud, Install
exl-id: 820cca84-2817-4881-829f-ebb78400d8c7
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Uppgradera projekt till ECE-verktygspaket

Adobe har ersatt `magento/magento-cloud-configuration` och `magento/ece-patches` paket till förmån för `ece-tools` som förenklar många molnprocesser. Om du använder ett äldre Adobe Commerce-program i ett molninfrastrukturprojekt som _not_ innehåller `ece-tools` paketet, måste du utföra en engångshandbok _uppgradera_ till projektet.

>[!WARNING]
>
>Om ditt projekt innehåller `ece-tools` kan du hoppa över följande uppgradering. Verifiera genom att hämta [!DNL Commerce] version med `php vendor/bin/ece-tools -V` på projektets lokala rotkatalog.

Du måste uppdatera `magento/magento-cloud-metapackage` versionsbegränsning i `composer.json` i rotkatalogen. Begränsningen gör att Adobe Commerce kan uppdateras i molninfrastruktursmetapaket, inklusive borttagning av borttagna paket, utan att du behöver uppgradera din nuvarande Adobe Commerce-version.

{{upgrade-tip}}

## Ta bort inaktuella paket

Innan du uppgraderar ska du använda `ece-tools` paket, kontrollera `composer.lock` -fil för följande borttagna paket:

- `magento/magento-cloud-configuration`
- `magento/ece-patches`

## Uppdatera metapaketet

För varje Adobe Commerce-version krävs en annan begränsning som bygger på följande:

```terminal
>=current_version <next_version
```

- För `current_version`, anger vilken version av Adobe Commerce som ska installeras.
- För `next_version`anger du nästa patch-version efter värdet som anges i `current_version`.

Om du vill installera Adobe Commerce `2.3.5-p2`, ange `current_version` till `2.3.5` och `next_version` till `2.3.6`. Begränsningen `">=2.3.5 <2.3.6"` installerar det senaste tillgängliga paketet för 2.3.5.

Du hittar alltid den senaste metapackage-begränsningen i [`magento-cloud` mall](https://github.com/magento/magento-cloud/blob/master/composer.json).

I följande exempel begränsas Adobe Commerce i molninfrastrukturmetapaketet till alla versioner som är större än eller lika med den aktuella versionen, 2.4.5, och lägre än nästa version, 2.4.6:

```json
"require": {
    "magento/magento-cloud-metapackage": ">=2.4.5 <2.4.6"
},
```

## Uppgradera projektet

Så här uppgraderar du ditt projekt till `ece-tools` måste du uppdatera metapaketet och `.magento.app.yaml` skapar länkar för egenskaper och utför en Composer-uppdatering.

**Så här uppgraderar du projekt till att använda stilverktyg**:

1. Uppdatera `magento/magento-cloud-metapackage` versionsbegränsning i `composer.json` -fil.

   ```bash
   composer require "magento/magento-cloud-metapackage":">=2.4.5 <2.4.6" --no-update
   ```

1. Uppdatera metapaketet.

   ```bash
   composer update magento/magento-cloud-metapackage
   ```

1. Ändra krokkommandona i dialogrutan `magento.app.yaml` -fil.

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. Sök efter och ta bort [inaktuella paket](#remove-deprecated-packages). De borttagna paketen kan förhindra en lyckad uppgradering.

   ```bash
   composer remove magento/magento-cloud-configuration
   ```

   ```bash
   composer remove magento/ece-patches
   ```

1. Det kan bli nödvändigt att uppdatera `ece-tools` paket.

   ```bash
   composer update magento/ece-tools
   ```

1. Lägg till och verkställ kodändringarna. I det här exemplet uppdaterades följande filer:

   ```terminal
   .magento.app.yaml
   composer.json
   composer.lock
   ```

1. Skicka dina kodändringar till fjärrservern och sammanfoga den här grenen med `integration` gren.

   ```bash
   git push origin <branch-name>
   ```
