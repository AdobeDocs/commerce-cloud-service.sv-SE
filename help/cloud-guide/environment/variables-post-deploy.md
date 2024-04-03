---
title: Variabler efter distribution
description: Se en lista med miljövariabler som styr åtgärder i Adobe Commerce för efterdriftsättning av molninfrastruktur.
feature: Cloud, Configuration, Cache
recommendations: noDisplay, catalog
role: Developer
exl-id: e460335f-cd2b-4c98-b1ff-32504599b33d
source-git-commit: 8b02757591c4e8f607e936de4eda74d76953d9b7
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Variabler efter distribution

Följande _efter driftsättning_ variabelkontrollåtgärder i fasen efter distributionen och kan ärva och åsidosätta värden från [Globala variabler](variables-global.md). Infoga dessa variabler i `post-deploy` i `.magento.env.yaml` fil:

```yaml
stage:
  post-deploy:
    POST-DEPLOY_VARIABLE_NAME: value
```

Mer information om hur du anpassar bygg- och distributionsprocessen:

- [Distributionskonfiguration](configure-env-yaml.md)
- [Distributionsprocess](../deploy/process.md)

## `TTFB_TESTED_PAGES`

- **Standard**— `[]` (en tom array)
- **Version**—Adobe Commerce 2.1.4 och senare

Konfigurera _Tid till första byte_ (TTFB) testa för angivna sidor för att testa platsens prestanda. Ange en absolut sökvägsreferens, eller URL med protokoll och värd, för varje sida som kräver testet.

```yaml
stage:
  post-deploy:
    TTFB_TESTED_PAGES:
       - "index.php"
       - "index.php/customer/account/create"
       - "https://example.com/catalog/some-category"
```

När du har angett vilka sidor som ska testas och verkställas, kan du _Tid till första byte_ testkörningar under fasen efter distributionen och skickar resultat för varje sökväg till molnloggen:

```terminal
[2019-06-20 20:42:22] INFO: TTFB test result: 0.313s {"url":"https://staging-tkyicst-xkmwgjkwmwfuk.us-4.magentosite.cloud/customer/account/create","status":200}
[2019-06-20 20:42:22] INFO: TTFB test result: 0.408s {"url":"https://staging-tkyicst-xkmwgjkwmwfuk.us-4.magentosite.cloud/checkout/cart","status":200}
```

För omdirigerade sökvägar rapporterar loggen sökvägen till omdirigeringsmålet i stället för den som konfigurerats i miljövariabeln. Om du anger en ogiltig sökväg visas ett varningsmeddelande i loggen.

## `WARM_UP_CONCURRENCY`

- **Standard**—_Ej angiven_
- **Version**—Adobe Commerce 2.1.4 och senare

Ange gränsen för antalet samtidiga begäranden som ska skickas under cachevärmaråtgärder för att minska serverbelastningen. Detta värde begränsar antalet parallella anslutningar och är användbart för miljökonfigurationer där `WARM_UP_PAGES` variabeln post-deploy anger flera sidor för cacheförinläsning.

```yaml
stage:
  post-deploy:
    WARM_UP_CONCURRENCY: 4
```

## `WARM_UP_PAGES`

- **Standard**— `index.php`
- **Version**—Adobe Commerce 2.1.4 och senare

Anpassa listan med sidor som används för att förhandsladda cacheminnet i `post_deploy` stage. Du måste konfigurera kroken efter distributionen. Se [krokavsnitt](../application/hooks-property.md) i `.magento.app.yaml` -fil.

- **enstaka sidor**—Ange en sida som ska läggas till i cachen. Du behöver inte ange standardbas-URL:en. I följande exempel cachelagras `BASE_URL/index.php` sida:

  ```yaml
  stage:
    post-deploy:
      WARM_UP_PAGES:
        - "index.php"
  ```

- **flera domäner**—Visa flera URL:er. I följande exempel cachelagras sidor från två domäner:

  ```yaml
  stage:
    post-deploy:
      WARM_UP_PAGES:
        - 'http://example1.com/test'
        - 'http://example2.com/test'
  ```

- **flera sidor**—Använd följande format för att cachelagra flera sidor enligt ett specifikt mönster för reguljära uttryck:

  ```terminal
  <entity_type>:<pattern|url|product_sku>:<store_id|store_code>
  ```

   - `entity_type`: Möjliga varianter `category`, `cms-page`, `product`, `store-page`
   - `pattern|url|product_sku`: Använd en `regexp` mönster eller en exakt matchning `url` om du vill filtrera URL-adresserna eller använda en asterisk (\*) för alla sidor. Använd produktskal för `product` entitetstyp
   - `store_id|store_code`: Använd ID:t eller koden för butiken eller en asterisk (\*) för alla butiker kan du skicka flera butiks-ID:n eller koder åtskilda med `|`

  Följande exempel cachelagrar för `category` och `cms-page` entitetstyper baserade på dessa kriterier:
   - alla kategorisidor för butik med ID `1`
   - alla kategorisidor för butiker med kod `store1` och `store2`
   - kategorisida `cars` för butik med kod `store_en`
   - cms page `contact` för alla butiker
   - cms page `contact` för butiker med ID `1` och `2`
   - alla kategorisidor som innehåller `car_` och slutar med `html` för butik med ID 2
   - alla kategorisidor som innehåller `tires_` för butik med kod `store_gb`

     ```yaml
     stage:
       post-deploy:
         WARM_UP_PAGES:
           - "category:*:1"
           - "category:*:store1|store2"
           - "category:cars:store_en"
           - "cms-page:contact:*"
           - "cms-page:contact:1|2"
           - "category:|car_.*?\\.html$|:2"
           - "category:|tires_.*|:store_gb"
     ```

  Följande exempel cachelagrar för `product` entitetstyp baserad på dessa kriterier:
   - alla produkter för alla butiker (programmatiskt begränsat till 100 per butik för att undvika prestandaproblem)
   - alla produkter för butik `store1`
   - produkter med `sku1` för alla butiker
   - produkter med `sku1` för butiker med kod `store1` och `store2`
   - produkter med `sku1`, `sku2` och `sku3` för butiker med kod `store1` och `store2`

     ```yaml
     stage:
       post-deploy:
         WARM_UP_PAGES:
           - "product:*:*"
           - "product:*:store1"
           - "product:sku1:*"
           - "product:sku1:store1|store2"
           - "product:sku1|sku2|sku3:store1|store2"
     ```

  Följande exempel cachelagrar för `store-page` entitetstyp baserad på dessa kriterier:
   - page `/contact-us` för alla butiker
   - page `/contact-us` för butik med ID `1`
   - page `/contact-us` för butiker med kod `code1` och `code2`

  ```yaml
        stage:
          post-deploy:
            WARM_UP_PAGES:
              - "store-page:/contact-us:*"
              - "store-page:/contact-us:1"
              - "store-page:/contact-us:code1|code2"
  ```
