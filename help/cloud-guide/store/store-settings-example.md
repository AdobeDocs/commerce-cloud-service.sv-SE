---
title: Exempel på hantering av systemspecifika inställningar
description: Se ett exempel på hur du hanterar och synkroniserar lagringskonfigurationsinställningar i alla Adobe Commerce-miljöer för molninfrastrukturer.
hidefromtoc: true
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---


# Exempel på hantering av systemspecifika inställningar

I det här exemplet visas hur du använder konfigurationshantering för att se till att lagringsinställningarna är konsekventa i alla miljöer.

I exemplet används följande procedur som definieras i [Lagringsinställningar](store-settings.md):

1. Ange dina konfigurationer i din lagringsadministratör för integreringsmiljön.
1. Skapa en `config.php` och överföra den till din lokala arbetsstation.
1. Push `config.php` till fjärrintegreringsmiljön.
1. Kontrollera att inställningarna inte kan redigeras i Admin.
1. Gör nödvändiga ändringar:

   * Ändra konfigurationsinställningar i integreringsmiljön.
   * Om du vill lägga till konfigurationer kör du kommandot för att skapa `config.php` igen. Nya konfigurationer läggs till i filen.
   * Om du vill ta bort eller redigera befintliga konfigurationer redigerar du filen manuellt.
   * Verkställ och tryck.

Du kan till exempel ange följande inställningar:

* Inaktivera [locale](https://glossary.magento.com/locale) och statiska inställningar för filoptimering i din integreringsmiljö
* Möjliggör statisk filoptimering i miljö för förproduktion och produktion
* Konfigurera snabbt i mellanlagring och produktion med specifika autentiseringsuppgifter för varje

_Optimering av statiska filer_ innebär att sammanfoga och miniatyrbilder av JavaScript och CSS (Cascading Style Sheets) samt att miniatyrbilder av HTML-mallar används. Se [Strategier för distribution av statiskt innehåll](../deploy/static-content.md).

## Förutsättningar

För att kunna utföra dessa konfigurationshanteringsåtgärder behöver du följande:

* Projektläsarroll med [environment &quot;admin&quot;](../project/user-access.md) behörigheter
* Admin-URL och autentiseringsuppgifter för integrering, mellanlagring och produktion

## Konfigurera handelsadministratören

I integreringsmiljön kan du logga in på Admin för att ändra systemkonfigurationsinställningar för butiker, webbplatser, moduler eller tillägg, statisk filoptimering och systemvärden för statisk innehållsdistribution. Se [Konfigurationsdata](store-settings.md#scd-performance).

**Ändra inställningar för språkområde och statisk filoptimering**:

1. Logga in på administratören för integreringsmiljön. Du kommer åt den här URL:en via [[!DNL Cloud Console]](../project/overview.md).
1. Navigera till **Lager** > Inställningar > **Konfiguration** > Allmänt > **Allmänt**.
1. Expandera i sidnavigeringen **Nationella inställningar**.
1. Från **Språk** ändra språkinställningen. Du kan ändra tillbaka den senare.

   ![Ändra språkområde](../../assets/locale-options.png)

1. Klicka **Spara konfiguration**.
1. Om du uppmanas att göra det [tömma cachen](https://docs.magento.com/user-guide/system/cache-management.html).
1. Logga ut från administratören.

## Exportera värden och överför config.php till ditt lokala system

Det här steget skapar och överför `config.php` konfigurationsfilen i integreringsmiljön med ett kommando som du kör på den lokala datorn.

Denna procedur motsvarar steg 2 i [rekommenderad procedur](store-settings.md). När du har skapat `config.php`, överför det till ditt lokala system så att du kan lägga till det i Git.

**Skapa och överföra`config.php`**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Byt till integreringsmiljön.

   ```bash
   magento-cloud environment:checkout integration
   ```

1. Skapa en lokal dump av fjärrdatabasen.

   ```bash
   magento-cloud db:dump
   ```

Följande utdrag från `config.php` visar ett exempel på hur du ändrar standardspråkområdet till `en_GB` och ändra inställningarna för statisk filoptimering:

```php?start_inline=1
'general' => [
     'locale' => [
         'code' => 'en_GB',
         'timezone' => 'UTC',
     ],

     ... more ...

 'dev' => [
     'template' => [
         'allow_symlink' => '0',
         'minify_html' => '0',
     ],
     'js' => [
         'merge_files' => '0',
         'enable_js_bundling' => '0',
         'minify_files' => '0',
     ],
     'css' => [
         'merge_css_files' => '0',
         'minify_files' => '0',
     ],

     ... more ...
```

## Tryck och distribuera config.php till miljöer

Nu när du har skapat `config.php` och överförde det till ditt lokala system, implementera det på Git och skicka det till dina miljöer. Detta förfarande motsvarar steg 3 och 4 i [rekommenderad procedur](store-settings.md).

Följande kommando lägger till, implementerar och push-ar i `master` gren:

```bash
git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
```

Komplett koddistribution till Förproduktion och staging. För Starter går du vidare till `staging` och `master` grenar. Mer information om distributionskommandon finns i [Distribuera din butik](../deploy/staging-production.md).

Vänta tills distributionen är klar i alla miljöer.

## Verifiera konfigurationsändringarna

När du har tryckt `config.php` i dina miljöer ska de värden du ändrar vara skrivskyddade i Admin. I det här exemplet bör de ändrade inställningarna för standardinställningar för språkområde och statisk filoptimering inte kunna redigeras i Admin. Dessa konfigurationsinställningar anges i `config.php`.

Så här verifierar du konfigurationsändringarna:

1. Logga ut från administratören i någon av miljöerna.
1. Logga in igen i Admin.
1. Klicka **Lager** > Inställningar > **Konfiguration** > Allmänt > **Allmänt**.
1. Expandera i den högra rutan **Nationella inställningar**.

   Observera att flera fält inte kan redigeras, vilket visas i följande exempel. Dessa konfigurationsinställningar hanteras av `config.php`.

   ![Vissa värden kan inte längre redigeras i administratören](../../assets/locale-options-disabled.png)

1. Logga ut från administratören.

## Ändra och uppdatera systemspecifika konfigurationsinställningar

Om du behöver ändra någon av dessa inställningar ändrar du `config.php` filen manuellt med en textredigerare. När du är klar med redigeringar eller borttagningar kan du implementera och överföra den till fjärrmiljön enligt föregående steg.

Om du vill lägga till konfigurationer ändrar du integreringsmiljön och kör kommandot igen för att generera filen. Alla nya konfigurationer läggs till i koden i filen. Skicka det till Git enligt föregående steg.

I det här exemplet ändrar du inställningarna för optimering av statiska filer och lägger till en ny inställning för JavaScript.

### Lägg till konfigurationer i integrering

Så här lägger du till konfigurationsvärden i integreringsmiljöns administratör. I det här exemplet sammanfogas JavaScript-filer.

1. Logga ut från integreringsadministratören.
1. Logga in på integreringsadministratören igen.
1. Klicka **Lager** > Inställningar > **Konfiguration** > **Avancerat** > **Utvecklare**.
1. Expandera i den högra rutan **JavaScript-inställningar**.
1. Från **Sammanfoga JavaScript-filer** lista, klicka på **Ja**.
1. Klicka **Spara konfiguration**.
1. Om du uppmanas att göra det [tömma cachen](https://docs.magento.com/user-guide/system/cache-management.html).
1. Logga ut från administratören.

Genom att köra dumpkommandot igen läggs den nya konfigurationen till i filen.

```bash
magento-cloud db:dump
```

### Redigera config.php med nya inställningar

Använd en textredigerare för att redigera den uppdaterade `app/etc/config.php` -fil. Redigera de här inställningarna för att aktivera miniatyrbilder för JavaScript-, HTML och CSS-filer.

```php?start_inline=1
 'dev' => [
     'template' => [
         'allow_symlink' => '0',
         'minify_html' => '0',
     ],

     ... more ...

     'js' => [
         'merge_files' => '0',
         'enable_js_bundling' => '0',
         'minify_files' => '0',
     ],
     'css' => [
         'merge_css_files' => '0',
         'minify_files' => '0',
     ],
```

Om du vill ändra inställningarna så att miniatyrbilder tillåts redigerar du `'0'` till `'1'` for `'minify_html'` och `'minify_files'` alternativ:

```php?start_inline=1
 'dev' => [
     'template' => [
         'allow_symlink' => '0',
         'minify_html' => '1',
     ],

     ... more ...

     'js' => [
         'merge_files' => '0',
         'enable_js_bundling' => '0',
         'minify_files' => '1',
     ],
     'css' => [
         'merge_css_files' => '0',
         'minify_files' => '1',
     ],
```

Spara ändringarna i filen.

### Överför ändringarna till Git

Ange följande om du vill göra ändringar:

```bash
git add app/etc/config.php
```

```bash
git commit -m "Add system-specific configuration and edit settings"
```

```bash
git push origin master
```

Vänta tills distributionen är klar.

Upprepa distributionsprocessen för att skicka koden till alla miljöer.
