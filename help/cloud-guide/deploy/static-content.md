---
title: Statisk innehållsdistribution
description: Lär dig mer om strategier för att distribuera statiskt innehåll, som bilder, skript och CSS, i Adobe Commerce i molninfrastrukturprojekt.
feature: Cloud, Build, Deploy, SCD
exl-id: e128d0d5-1326-44e5-a822-009e11ba105f
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# Strategier för distribution av statiskt innehåll

Distribution av statiskt innehåll (SCD) har stor inverkan på distributionsprocessen för butiken, vilket beror på hur mycket innehåll som ska genereras, till exempel bilder, skript, CSS, videor, teman, språkområden och webbsidor, och när innehållet ska genereras. Standardstrategin genererar till exempel statiskt innehåll under [distributionsfas](process.md#deploy-phase-deploy-phase) när platsen är i underhållsläge, men den här distributionsstrategin tar tid att skriva innehållet direkt till den monterade `pub/static` katalog. Du har flera alternativ eller strategier som hjälper dig att förbättra driftsättningstiden beroende på dina behov.

## Optimera JavaScript och HTML

Du kan använda paketering och miniatyrbilder för att skapa optimerat JavaScript- och HTML-innehåll under distributionen av statiskt innehåll.

### Minimera innehåll

Du kan förbättra SCD-inläsningstiden under distributionsprocessen om du inte kopierar de statiska vyfilerna i `var/view_preprocessed` katalog och generera _minified_ HTML på begäran. Du kan aktivera detta genom att ställa in [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skiphtmlminification) global miljövariabel till `true` i `.magento.env.yaml` -fil.

>[!NOTE]
>
>Börja med `ece-tools` package version 2002.0.13, the default value for the SKIP_HTML_MINIFICATION variable is set to `true`.

Du kan spara **mer** driftsättningstid och diskutrymme genom att minska antalet onödiga temafiler. Du kan till exempel distribuera `magento/backend` tema på engelska och ett anpassat tema på andra språk. Du kan konfigurera de här temainställningarna med [SCD_MATRIX](../environment/variables-deploy.md#scdmatrix) miljövariabel.

## Välja en distributionsstrategi

Distributionsstrategierna skiljer sig åt beroende på om du väljer att generera statiskt innehåll under _bygg_ fas, _driftsätta_ fas, eller _on demand_. Som framgår av följande diagram är det minst optimala alternativet att generera statiskt innehåll under distributionsfasen. Även om det finns en minifierad HTML måste varje innehållsfil kopieras till den monterade `~/pub/static` som kan ta lång tid. Att generera statiskt innehåll on demand verkar vara det optimala valet. Men om innehållsfilen inte finns i cachen genereras den när den begärs, vilket ökar användarens inläsningstid. Därför är det mest optimala att generera statiskt innehåll under byggfasen.

![SCD-belastningsjämförelse](../../assets/scd-load-times.png)

### Ställa in SCD vid skapande

Den optimala konfigurationen för att skapa statiskt innehåll under byggfasen med minifierad HTML [**nolltid** distributioner](reduce-downtime.md), som också kallas **idealiskt läge**. I stället för att kopiera filer till en monterad enhet skapas en länk från `./init/pub/static` katalog.

För att generera statiskt innehåll måste du ha tillgång till teman och språkområden. Adobe Commerce lagrar teman i filsystemet, som är tillgängligt under byggfasen, men i Adobe Commerce lagras språkinställningarna i databasen. Databasen är _not_ som är tillgängliga under byggfasen. För att kunna generera det statiska innehållet under byggfasen måste du använda `config:dump` i `ece-tools` paket för att flytta språkområden till filsystemet. Språken läses och sparas i `app/etc/config.php` -fil.

**Så här konfigurerar du projektet för att generera SCD vid bygget**:

1. Byt till din projektkatalog på din lokala arbetsstation.
1. Använd SSH för att logga in i fjärrmiljön.

   ```bash
   magento-cloud ssh
   ```

1. Flytta språkinställningar till filsystemet och uppdatera sedan [`config.php` fil](../development/commerce-version.md#create-a-configphp-file).

1. The `.magento.env.yaml` konfigurationsfilen ska innehålla följande värden:

   - [SKIP_HTML_MINIFICATION](../environment/variables-global.md#skip_html_minification) är `true`
   - [SKIP_SCD](../environment/variables-build.md#skip_scd) på byggfasen är `false`
   - [SCD_STRATEGY](../environment/variables-build.md#scd_strategy) är `compact`

1. Verifiera konfigurationen av [Krok efter driftsättning](../application/hooks-property.md) i `.magento.app.yaml` -fil.

1. Verifiera inställningarna genom att köra [Smart guide för det idealiska läget](smart-wizards.md).

   ```bash
   php ./vendor/bin/ece-tools wizard:ideal-state
   ```

### Ställa in SCD på begäran

Att generera SCD on demand är optimalt för ett utvecklingsarbetsflöde i integreringsmiljön. Det minskar driftsättningstiden så att du snabbt kan granska implementeringarna och köra integreringstester. Aktivera [SCD_ON_DEMAND](../environment/variables-global.md#scdondemand) miljövariabel i den globala scenen i `.magento.env.yaml` -fil. Variabeln SCD_ON_DEMAND åsidosätter alla andra konfigurationer som är relaterade till SCD och tar bort befintligt innehåll från `~/pub/static` katalog.

När du använder SCD on demand-strategin är det bra att läsa in cachen i förväg med sidor som du förväntar dig, till exempel hemsidan. Lägg till en lista med förväntade sidor i [WARM_UP_PAGES](../environment/variables-post-deploy.md#warmuppages) systemvariabel i post-deploy-fasen i `.magento.env.yaml` -fil.

>[!WARNING]
>
>Använd inte SCD on demand-strategin i produktionsmiljön.

### Hoppar över SCD

Ibland kan du välja att inte generera statiskt innehåll helt. Du kan ange [SKIP_SCD](../environment/variables-build.md#skipscd) miljövariabel i den globala scenen för att ignorera andra konfigurationer relaterade till SCD. Detta påverkar inte befintligt innehåll i `~/pub/static` katalog.
