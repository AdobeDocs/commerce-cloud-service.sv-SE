---
title: Konfigurera tjänsten Elasticsearch
description: Lär dig hur du aktiverar tjänsten Elasticsearch för Adobe Commerce i molninfrastruktur.
feature: Cloud, Search, Services
exl-id: ac559cbb-342a-4756-ade5-49eba4827965
source-git-commit: 8147b43b26370d9305c3c7dc47865ddcbae1904d
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# Konfigurera tjänsten Elasticsearch

[Elasticsearch](https://www.elastic.co) är en öppen källkodsprodukt som gör att du kan hämta data från alla källor, alla format och söka och visualisera den i realtid.

{{elasticsearch-support}}

För Adobe Commerce version 2.4.4 och senare, se [Konfigurera OpenSearch-tjänsten](opensearch.md).

- Elasticsearch gör snabba och avancerade sökningar i produktkatalogen
- Elasticsearch Analyzers har stöd för flera språk
- Stöder stoppord och synonymer
- Indexeringen påverkar inte kunderna förrän omindexeringsåtgärden har slutförts

>[!TIP]
>
>Adobe rekommenderar att du alltid ställer in Elasticsearch för ditt Adobe Commerce i molninfrastrukturprojekt, även om du tänker konfigurera ett tredjepartssökverktyg för ditt Adobe Commerce-program. När du konfigurerar Elasticsearch finns ett reservalternativ om det inte går att använda tredjepartssökverktyget.

{{service-instruction}}

**Aktivera Elasticsearch**:

1. För Starter-projekt lägger du till `elasticsearch` till `.magento/services.yaml` fil med Elasticsearch-version och tilldelat diskutrymme i MB.

   ```yaml
   elasticsearch:
       type: elasticsearch:<version>
       disk: 1024
   ```

   För Pro-projekt måste du skicka in en Adobe Commerce Support-biljett för att ändra Elasticsearch-versionen i mellanlagrings- och produktionsmiljöerna.

1. Ange `relationships` -egenskapen i `.magento.app.yaml` -fil.

   ```yaml
   relationships:
       elasticsearch: "elasticsearch:elasticsearch"
   ```

1. Lägg till, implementera och push-ändra kod.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable Elasticsearch" && git push origin <branch-name>
   ```

   Mer information om hur dessa förändringar påverkar dina miljöer finns i [Tjänster](services-yaml.md).

1. När distributionen är klar använder du SSH för att logga in på fjärrmiljön.

   ```bash
   magento-cloud ssh
   ```

1. Indexera om indexet för katalogsökning.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Rensa cachen.

   ```bash
   bin/magento cache:clean
   ```

{{service-change-tip}}

## Kompatibilitet med Elasticsearch-program

När du installerar eller uppgraderar din Adobe Commerce i ett molninfrastrukturprojekt ska du alltid kontrollera om Elasticsearch-versionen är kompatibel med [ELASTICSEARCH PHP](https://github.com/elastic/elasticsearch-php) för Adobe Commerce.

- **Inställning för första gången**-Bekräfta att Elasticsearch-versionen som anges i `services.yaml` filen är kompatibel med Elasticsearch PHP-klienten som konfigurerats för Adobe Commerce.

- **Projektuppgradering**-Kontrollera att Elasticsearch PHP-klienten i den nya programversionen är kompatibel med den Elasticsearch-tjänstversion som är installerad i molninfrastrukturen.

Tjänstversion och kompatibilitetsstöd för Adobe Commerce i molninfrastruktur avgörs av vilka versioner som distribueras i molninfrastrukturen, och skiljer sig ibland från de versioner som stöds av Adobe Commerce lokala distributioner. Se [Tjänstversioner](services-yaml.md#service-versions).

**Så här kontrollerar du kompatibiliteten med Elasticsearch**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Visa information om Elasticsearch för den aktiva miljön.

   ```bash
   magento-cloud relationships --property=elasticsearch
   ```

1. Du kan också använda SSH för att logga in på fjärrmiljön.

   ```bash
   magento-cloud ssh
   ```

1. Kontrollera Composer-paketets version för `elasticsearch/elasticsearch`.

   ```bash
   composer show elasticsearch/elasticsearch
   ```

   Kontrollera den installerade versionen i `versions` -egenskap.

   ```terminal
   name     : elasticsearch/elasticsearch
   descrip. : PHP Client for Elasticsearch
   keywords : client, elasticsearch, search
   versions : * v7.17.1
   type     : library
   license  : Apache License 2.0 (Apache-2.0) (OSI approved) https://spdx.org/licenses/Apache-2.0.html#licenseText
   license  : GNU Lesser General Public License v2.1 only (LGPL-2.1-only) (OSI approved) https://spdx.org/licenses/LGPL-2.1-only.html#licenseText
   homepage :
   source   : [git] git@github.com:elastic/elasticsearch-php.git f1b8918f411b837ce5f6325e829a73518fd50367
   dist     : [zip] https://api.github.com/repos/elastic/elasticsearch-php/zipball/f1b8918f411b837ce5f6325e829a73518fd50367 f1b8918f411b837ce5f6325e829a73518fd50367
   path     : ~/vendor/elasticsearch/elasticsearch
   names    : elasticsearch/elasticsearch
   ```

   Du hittar även Elasticsearch PHP-klientversionen i  `composer.lock` i miljöns rotkatalog.

1. Hämta tjänstanslutningsinformationen för Elasticsearch från kommandoraden.

   ```bash
   vendor/bin/ece-tools env:config:show services
   ```

   I svaret hittar du IP-adressen för Elasticsearch-tjänstslutpunkten:

   ```terminal
   | elasticsearch:                                                                                                  |
   +------------------------------------------+----------------------------------------------------------------------+
   | username                                 | null                                                                 |
   | scheme                                   | http                                                                 |
   | service                                  | elasticsearch                                                        |
   | fragment                                 | null                                                                 |
   | ip                                       | 169.254.220.11                                                       |
   | hostname                                 | dzggu33f75wi3sd24lgwtoupxm.elasticsearch.service._.magentosite.cloud |
   | public                                   | false                                                                |
   | cluster                                  | fo3qdoxtla4j4-master-7rqtwti                                         |
   | host                                     | elasticsearch.internal                                               |
   | rel                                      | elasticsearch                                                        |
   | query                                    |                                                                      |
   | path                                     | null                                                                 |
   | password                                 | null                                                                 |
   | type                                     | elasticsearch:6.5                                                    |
   | port                                     | 9200                                                                 |
   +------------------------------------------+----------------------------------------------------------------------+
   ```

1. Hämta den installerade Elasticsearch-tjänsten `version:number` från tjänstslutpunkten.

   ```bash
   curl -XGET <elasticsearch-service-endpoint-ip-address>:9200/
   ```

   ```terminal
   {
      "name" : "-AqGi9D",
      "cluster_name" : "elasticsearch",
      "cluster_uuid" : "_yze6-ywSEW1MaAF8ZPWyQ",
      "version" : {
        "number" : "6.5.4",
        "build_flavor" : "default",
        "build_type" : "deb",
        "build_hash" : "82a8aa7",
        "build_date" : "2019-01-23T12:07:18.760675Z",
        "build_snapshot" : false,
        "lucene_version" : "7.5.0",
        "minimum_wire_compatibility_version" : "5.6.0",
        "minimum_index_compatibility_version" : "5.0.0"
   },
   "  tagline" : "You Know, for Search"
   }
   ```

1. Kontrollera versionskompatibiliteten mellan Elasticsearch och PHP-klienten.

   Om versionerna inte är kompatibla gör du någon av följande uppdateringar av din miljökonfiguration:

   - Ändra Elasticsearch PHP-klienten till en version som är kompatibel med Elasticsearch.

     ```bash
     composer require "elasticsearch/elasticsearch:~<version>"
     ```

   - Ändra tjänstversionen för Elasticsearch i dialogrutan `services.yaml` till en version som är kompatibel med Elasticsearch PHP-klienten.

     {{pro-update-service}}

## Starta om tjänsten Elasticsearch

Om du behöver starta om [Elasticsearch](https://www.elastic.co) måste du kontakta Adobe Commerce support.

## Ytterligare sökkonfiguration

- Som standard återskapas sökkonfigurationen för molnmiljöer varje gång du distribuerar. Du kan använda `SEARCH_CONFIGURATION` distribuera variabel för att behålla anpassade sökinställningar mellan distributioner. Se [Distribuera variabler](../environment/variables-deploy.md#search_configuration).

- När du har konfigurerat tjänsten Elasticsearch för ditt projekt kan du testa Elasticsearch-anslutningen och anpassa Elasticsearch-inställningarna för Adobe Commerce med hjälp av administratörsgränssnittet.

### Lägg till plugin-program för Elasticsearch

Du kan också lägga till plugin-program för Elasticsearch genom att lägga till `configuration:plugins` till tjänsten Elasticsearch i `.magento/services.yaml` -fil. Följande kod aktiverar till exempel ICU-analys och plugin-program för fonetisk analys.

```yaml
elasticsearch:
    type: elasticsearch:<service-version>
    disk: 1024
    configuration:
        plugins:
            - analysis-icu
            - analysis-phonetic
```

Om du använder ett plugin-program från en annan leverantör måste du [uppdatera `ece-tools` package](../dev-tools/update-package.md) till version 2002.0.19 eller senare.
När du konfigurerar Elastic Suite lägger du till konfigurationsinställningarna i `ELASTICSUITE_CONFIGURATION` distributionsvariabel. Den här konfigurationen sparar inställningarna mellan distributioner.

### Ta bort plugin-program för Elasticsearch

Ta bort plugin-programposterna från `elasticsearch:` in `.magento/services.yaml` avinstallerar eller inaktiverar inte dem som du kan förvänta dig. Du måste indexera om dina Elasticsearch-data. Detta beteende är avsiktligt för att förhindra att data som är beroende av dessa plugin-program går förlorade eller skadas.

**Ta bort plugin-program för Elasticsearch**:

1. Ta bort Elasticsearch-pluginposterna från `.magento/services.yaml` -fil.
1. Lägg till, implementera och push-överföra kodändringar.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Remove Elasticsearch plugin"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Verkställ `.magento/services.yaml` ändringar i Cloud-rapporten.
1. Indexera om indexet för katalogsökning.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Rensa cachen.

   ```bash
   bin/magento cache:clean
   ```

>[!TIP]
>
>Mer information om hur du använder eller felsöker Elastic Suite-plugin med Adobe Commerce finns i [Dokumentation för Elastic Suite](https://github.com/Smile-SA/elasticsuite).

## Felsökning

Se följande Adobe Commerce supportartiklar för hjälp med felsökning av Elasticsearch-problem:

- [Elasticsearch 5 är konfigurerat, men söksidan läses inte in med felmeddelandet &quot;FieldData is disabled...&quot;.](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-5-is-configured-but-search-page-does-not-load-with-fielddata-is-disabled...-error.html)
- [Katalognumrering fungerar inte när Elasticsearch 6.x används](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/catalog-pagination-doesn-t-work-when-elasticsearch-6.x-is-used.html)
- [Elasticsearch i Adobe Commerce felsökare](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-in-magento-troubleshooter.html)
- [Elasticsearch-indexstatus är `yellow` eller `red`](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-index-status-is-yellow-or-red.html)
