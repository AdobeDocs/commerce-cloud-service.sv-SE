---
title: Projektstruktur
description: Läs om filstrukturen och projektmallarna för Adobe Commerce om molninfrastrukturen.
exl-id: 6dc559bd-116b-4745-a85b-731508e113ff
source-git-commit: 47ef728ea46b137eeaabbdbada940143d8773ef0
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Projektstruktur

Ett Adobe Commerce-projekt för molninfrastruktur innehåller viktiga filer för autentiseringsuppgifter och programkonfiguration. Dessa filer är tillgängliga i som mallar enligt Adobe Commerce-versionen. Se molnmallarna som bygger på Adobe Commerce-versionen i [`magento/magento-cloud` GitHub-databas](https://github.com/magento/magento-cloud).

I följande tabell beskrivs filerna som ingår i ett molnprojekt:

| Fil | Beskrivning |
| ------------------------- | ------------ |
| `/.magento/routes.yaml` | Konfigurationsfil som omdirigeras `www` till huvuddomänen och `php` program för HTTP. Se [Konfigurera flöden](../routes/routes-yaml.md). |
| `/.magento/services.yaml` | En konfigurationsfil som definierar en MySQL-instans (MariaDB), Redis, OpenSearch eller Elasticsearch. Se [Konfigurera tjänster](../services/services-yaml.md). |
| `/app` | The `code` används för anpassade moduler. The `design` används för [egna teman](../store/custom-theme.md). The `etc` -mappen innehåller konfigurationsfiler för programmet. |
| `/m2-hotfixes` | Används för anpassade patchar. |
| `/update` | En tjänstmapp som används av supportmodulen. |
| `.gitignore` | Ange vilka filer och kataloger som ska ignoreras. Se [`.gitignore` referens](#ignoring-files). |
| `.magento.app.yaml` | En konfigurationsfil som definierar egenskaperna för att skapa programmet. Se [Konfigurera program](../application/configure-app-yaml.md). |
| `.magento.env.yaml` | Konfigurationsfil för byggnings-, distributions- och postdistributionsfaserna. The `ece-tools` innehåller ett exempel på den här filen. Se [Konfigurera miljöer](../environment/configure-env-yaml.md). |
| `composer.json` | Hämtar Adobe Commerce och konfigurationsskripten för att förbereda programmet. Se [Obligatoriska paket](../development/overview.md#required-packages). |
| `composer.lock` | Lagrar versionsberoenden för varje paket. Se [Obligatoriska paket](../development/overview.md#required-packages). |
| `magento-vars.php` | Används för att definiera [flera butiker](../store/multiple-sites.md) och webbplatser som använder variabler. |

{style="table-layout:auto"}

>[!NOTE]
>
>När du skickar dina lokala ändringar till fjärrservern använder distributionsskriptet de värden som definieras av konfigurationsfilerna i `.magento` och skriptet tar bort katalogen och dess innehåll. Din lokala utvecklingsmiljö påverkas inte.

## Programmets rotkatalog

Platsen för programmets rotkatalog beror på miljön.

- **Integrering med Starter och Pro**: `/app`
- **Startproduktion**: `/<project-ID>`
- **Pro Staging**: `/<project-ID>_stg`
- **Pro Production**: `/<project-ID>`

### Skrivbara kataloger

Miljöerna för fjärrintegrering, mellanlagring och produktion är skrivskyddade. Följande kataloger är *endast* skrivbara kataloger av säkerhetsskäl:

- `var`
- `pub/static`
- `pub/media`
- `app/etc`
- `/tmp`

>[!NOTE]
>
>I produktions- och mellanlagringsmiljöer har varje nod i klustret med tre noder en `/tmp` katalog som inte delas med andra noder.

## Ignorera filer

Det finns en bas `.gitignore` med Adobe Commerce i molninfrastrukturens projektarkiv. Se de senaste [.gitignore-fil i databasen magento-cloud](https://github.com/magento/magento-cloud/blob/master/.gitignore). Lägga till en fil som finns i `.gitignore` kan du använda `-f` (force) när en implementering mellanlagras:

```bash
git add <path/filename> -f
```

## Ändra basmall

Du kan använda följande steg för att ändra strukturen i ett befintligt projekt så att den återspeglar den senaste basmallen för Adobe Commerce i molninfrastrukturen.

1. Klona projektet till en lokal arbetsstation.

1. Uppdatera `composer.json` fil med följande värden för `extra` -avsnitt.

   ```json
   "extra": {
       "magento-force": true
       "magento-deploystrategy": "copy"
   }
   ```

1. Lägg till `.gitignore` -fil utformad för basmallen. Om du till exempel behöver `.gitignore` -filen för version 2.2.6-mallen använder du [.gitignore för 2.2.6](https://github.com/magento/magento-cloud/blob/2.2.6/.gitignore) som referens.

1. Rensa Git-cachen.

   ```bash
   git rm -r --cached .
   ```

1. Lägg till och verkställ ändringar.

   ```bash
   git add -A && git commit -m "Update base template"
   ```

{{redeploy-warning}}
