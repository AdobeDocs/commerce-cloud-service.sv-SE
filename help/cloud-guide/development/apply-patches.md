---
title: Tillämpa patchar
description: Lär dig hur du använder korrigeringsfiler i Adobe Commerce i molninfrastrukturprojekt.
feature: Cloud, Upgrade
exl-id: a7bf672f-7b89-45cd-8436-e885bca9029d
source-git-commit: e67d3259b1b5195147e4e441fe9efd82e48241ab
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# Tillämpa patchar

[Cloud Patches for Commerce](https://github.com/magento/magento-cloud-patches) och [Verktyget Kvalitetspatchar](https://github.com/magento/quality-patches) levererar patchar till dina installerade Adobe Commerce-program.

- Cloud Patches for Commerce-paketet innehåller nödvändiga korrigeringar med viktiga korrigeringar
- Quality Patches deliver optional, low-impact quality fixes as as [enskilda korrigeringsfiler](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/versioning-policy.html#individual-patch) som inte innehåller inkompatibla ändringar bakåt

Se [Tillgängliga korrigeringar](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) i _Handbok för Commerce Operations Tools_ för att se en fullständig lista över de släppta plåstren.

Båda paketen förbättrar integreringen av alla Adobe Commerce-versioner med molnmiljöer och stöder snabb leverans av viktiga, valfria och anpassade korrigeringar. Du kan använda de här paketen för att tillämpa, återställa och visa allmän information om alla enskilda korrigeringsfiler som är tillgängliga för Commerce.

>[!TIP]
>
>Du kan använda [Verktyget Kvalitetspatchar](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) och Cloud Patches for Commerce as stand-alone packages for Magento Open Source and Adobe Commerce projects. Vi rekommenderar att du använder verktyget Kvalitetskorrigeringar för icke-molnprojekt.

När du distribuerar ändringar i fjärrmiljön `ece-tools` paket använder `magento/magento-cloud-patches` och `magento/quality-patches` för att söka efter väntande korrigeringar och tillämpa dem automatiskt i följande ordning:

1. Använd alla nödvändiga Commerce-korrigeringar som ingår i molnkorrigeringarna för Commerce-paketet.
1. Använd valda valfria Commerce-korrigeringar som ingår i verktyget Kvalitetspatchar.
1. Använda anpassade patchar i `/m2-hotfixes` i alfabetisk ordning efter korrigeringens namn.

>[!NOTE]
>
>När du uppdaterar `ece-tools` paket eller Cloud Patches for Commerce-paketet, de senaste nödvändiga korrigeringarna tillämpas nästa gång du distribuerar projektet, eller så kan du distribuera dem direkt med `ece-patches apply` CLI-kommando och omdistribution av din molnmiljö. Du kan inte hoppa över [nödvändiga korrigeringar](https://github.com/magento/magento-cloud-patches/tree/develop/patches) under distributionsprocessen.

## Förutsättningar

{{upgrade-tip}}

Verktyget Kvalitetskorrigeringar är beroende av molnkorrigeringar för Commerce och `ece-tools` paket. Om du vill använda de senaste korrigeringarna måste du ha [den senaste versionen av ECE-Tools](../dev-tools/update-package.md) installerade. Minimiversionen av ECE-Tools är 2002.1.2.

## Visa tillgängliga korrigeringar och status

Så här visar du en lista över tillgängliga enskilda korrigeringar:

```bash
php ./vendor/bin/ece-patches status
```

Exempelsvar:

```terminal
More detailed information about patches you can find on https://support.magento.com/
╔════════════════╤═════════════════════════════════════════════════╤══════════╤═════════════╤═════════════════════════════════╗
║ Id             │ Title                                           │ Type     │ Status      │ Details                         ║
╠════════════════╪═════════════════════════════════════════════════╪══════════╪═════════════╪═════════════════════════════════╣
║ MAGECLOUD-5069 │ FPC is getting disabled during deployments      │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-page-cache    ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MCLOUD-5650    │ Hold deployment config after reading from file  │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/framework            ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MCLOUD-5684    │ Pagination Not working - product_list_limit=all │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-elasticsearch ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-65837       │ Fix load balancer issue                         │Deprecated│ Applied     │ Recommended replacement: MC-1   ║
║                │                                                 │          │             │ Affected components:            ║
║                │                                                 │          │             │  - magento/framework            ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ BUNDLE-2554    │ Set Payment info bug                            │ Required │ Not applied │ Affected components:            ║
║                │                                                 │          │             │  - amzn/amazon-pay-module       ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-1           │ Fixes issue 1                                   │ Optional │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-2           │ Fixes issue 2                                   │ Optional │ Not applied │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-3           │ Fixes issue 3                                   │ Optional │ Not applied │ Required patches:               ║
║                │                                                 │          │             │  - MC-2                         ║
║                │                                                 │          │             │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ N/A            │ ../m2-hotfixes/MDVA_custom__2.3.5_ce.patch      │ Custom   │ N/A         │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-framework     ║
╚════════════════╧═════════════════════════════════════════════════╧══════════╧═════════════╧═════════════════════════════════╝
Magento 2 Enterprise Edition, version 2.3.5.0
```

Statustabellen innehåller följande typer av information:

- **Typ**:
   - `Optional`—Alla korrigeringsfiler från kvalitetsuppdateringsverktyget och Cloud Patches-paketet är valfria för Adobe Commerce- och Magento Open Source-installationer. För Adobe Commerce i molninfrastruktur är alla korrigeringsfiler valfria.
   - `Required`—Alla korrigeringsfiler från paketet Cloud Patches for Commerce krävs för molnkunder.
   - `Deprecated`- Den enskilda korrigeringen är markerad som inaktuell och vi rekommenderar att du återställer den om du har använt den. När du har återställt en borttagen korrigering visas den inte längre i statustabellen.
   - `Custom`—Alla korrigeringar från katalogen m2-hotfixes.

- **Status**:
   - `Applied`- Korrigeringen har installerats.
   - `Not applied`- Korrigeringen har inte tillämpats.
   - `N/A`—Det går inte att definiera status för korrigeringen på grund av konflikter.

- **Information**:
   - `Affected components`- Listan med berörda moduler.
   - `Required patches`—Listan över nödvändiga korrigeringar (beroenden).
   - `Recommended replacement`- Den korrigering som rekommenderas som ersättning för en borttagen korrigering.

## Tillämpa en korrigering i en lokal miljö

Du kan tillämpa korrigeringsfiler manuellt i en lokal miljö och testa dem innan du distribuerar dem.

**Använda enskilda korrigeringsfiler i en lokal utvecklingsmiljö**:

1. Lägg till variabeln QUALITY_PATCH i `.magento.env.yaml` och visa de korrigeringar som behövs under.

   ```yaml
   stage:
     build:
       QUALITY_PATCHES:
         - MCTEST-1002
         - MCTEST-1003
   ```

1. Använd patcharna från projektets rot.

   ```bash
   php ./vendor/bin/ece-patches apply
   ```

   The `ece-patches apply` kommandot använder korrigeringar i följande ordning:
   - Nödvändiga patchar
   - Valfria enskilda korrigeringsfiler
   - Egna patchar från `/m2-hotfixes` katalog

1. Rensa cachen.

   ```bash
   php ./bin/magento cache:clean
   ```

1. Testa patcharna och gör nödvändiga ändringar i anpassade patchar.

## Tillämpa en korrigering i en fjärrmiljö

>[!WARNING]
>
>Vi rekommenderar att du testar alla korrigeringsfiler i en integrations- eller mellanlagringsmiljö innan du distribuerar dem till produktionsmiljön.

**Använda korrigeringsfiler i en fjärrmiljö**:

1. Lägg till `QUALITY_PATCHES` variabeln till `.magento.env.yaml` och visa de korrigeringar som behövs under.

   ```yaml
   stage:
     build:
       QUALITY_PATCHES:
         - MCTEST-1002
         - MCTEST-1003
   ```

   >[!NOTE]
   >
   >När du har uppgraderat till en ny version av Adobe Commerce måste du tillämpa korrigeringarna igen om de inte ingår i den nya versionen.

1. Lägg till, implementera och push-överföra den uppdaterade `.magento.env.yaml` -fil.

   ```bash
   git add .magento.env.yaml
   ```

   ```bash
   git commit -m "Apply patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

## Tillämpa en anpassad korrigering

När du distribuerar programmet använder ECE-Tools alla Adobe-patchar och alla anpassade patchar som du lägger till i `/m2-hotfixes` i projektets rot.

>[!NOTE]
>
>Alla korrigeringsfilnamn måste sluta med `.patch` tillägg.

**Använda och testa en anpassad korrigering i en molnmiljö**:

1. Skapa en katalog med namnet i projektets rot `m2-hotfixes` om den inte finns

   ```bash
   mkdir m2-hotfixes
   ```

1. Kopiera korrigeringsfilen till `/m2-hotfixes` katalog.

1. Lägg till, implementera och push-ändra kod.

   ```bash
   git add m2-hotfixes/
   ```

   ```bash
   git commit -m "Apply patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!NOTE]
   >
   >Testa alla korrigeringsfiler i en förproduktionsmiljö. För Adobe Commerce i molninfrastruktur kan du skapa grenar med `magento-cloud environment:branch <branch-name>` CLI-kommando.

## Återställa en anpassad korrigering

Så här återställer eller avinstallerar du en tidigare tillämpad anpassad korrigering:

1. Ta bort korrigeringsfilen från `/m2-hotfixes` katalog.

1. Lägg till, implementera och push-ändra kod.

   ```bash
   git add m2-hotfixes/
   ```

   ```bash
   git commit -m "Revert patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!NOTE]
   >
   >Testa i förproduktionsmiljö. För Adobe Commerce i molninfrastruktur kan du skapa grenar med `magento-cloud environment:branch <branch-name>` CLI-kommando.

## Tillämpa korrigeringar på ett icke-molnprojekt

Använd [Verktyget Kvalitetspatchar](https://github.com/magento/quality-patches) för projekt i Magento Open Source och Adobe Commerce.

## Återställa en korrigering i en lokal miljö

Du kan återställa alla tidigare tillämpade korrigeringsfiler i en lokal utvecklingsmiljö med hjälp av `ece-patches` CLI.

Så här återställer du alla tillämpade patchar:

```bash
php ./vendor/bin/ece-patches revert
```

Med det här kommandot återställs alla patchar i följande ordning:

- Återställer alla tillämpade anpassade korrigeringar från katalogen /m2-hotfixes.
- Återställer alla tillämpade valfria enskilda korrigeringsfiler.
- Återställer alla nödvändiga korrigeringar som används.

## Loggning

Verktyget Kvalitetspatchar loggar alla åtgärder till `<Project_root>/var/log/patch.log` -fil.
