---
title: Konfigurera flera webbplatser eller butiker
description: Lär dig hur du konfigurerar flera webbplatser eller butiker för Adobe Commerce i molninfrastrukturen.
feature: Cloud, Configuration, Routes, Site Navigation
exl-id: 16e932ef-f083-44d7-977f-0c78899e151a
source-git-commit: 85aa54af10e7ea44adde5403b69ff03d4a0c622f
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# Konfigurera flera webbplatser eller butiker

Du kan konfigurera Adobe Commerce så att det finns flera webbplatser eller butiker, till exempel en engelsk butik, en fransk butik och en tysk butik. Se [Förstå webbplatser, butiker och butiksvyer](best-practices.md#store-views).

>[!WARNING]
>
>Katalogdata utökas allt eftersom du ökar antalet webbplatser och butiker. Beroende på din projektarkitektur kan de extra butikerna leda till en längre indexeringsprocess och längre svarstider för icke-cachelagrade katalogsidor. Adobe rekommenderar att du noga övervakar webbplatsens prestanda.

Hur du konfigurerar flera arkiv beror på om du väljer att använda unika eller delade domäner.

Flera butiker med unika domäner:

```terminal
https://first.store.com/
https://second.store.com/
```

Flera butiker med samma domän:

```terminal
https://store.com/first/
https://store.com/second/
```

>[!TIP]
>
>Om du vill lägga till en butiksvy i webbplatsens bas-URL behöver du inte skapa flera kataloger. Se [Lägg till butikskoden i bas-URL:en](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-admin.html) i _Konfigurationshandbok_.

## Lägg till domäner

Anpassade domäner kan läggas till i Pro Staging och valfri produktionsmiljö. De kan inte läggas till i integreringsmiljöer.

Hur du lägger till en domän beror på typen av molnkonto:

- För Pro Staging and Production

  Lägg till den nya domänen snabbt, se [Hantera domäner](../cdn/fastly-custom-cache-configuration.md#manage-domains)eller öppna en supportanmälan för att få hjälp. Dessutom måste du [Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) för att begära att nya domäner läggs till i ett kluster.

- Endast för startproduktion

  Lägg till den nya domänen snabbt, se [Hantera domäner](../cdn/fastly-custom-cache-configuration.md#manage-domains), eller [Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) för att begära hjälp. Dessutom måste du lägga till den nya domänen i **Domäner** i [!DNL Cloud Console]: `https://<zone>.magento.cloud/projects/<project-ID>/edit`

## Konfigurera lokal installation

Information om hur du konfigurerar din lokala installation att använda flera butiker finns i [Flera webbplatser eller butiker][config-multiweb] i _Konfigurationshandbok_.

När du har skapat och testat den lokala installationen för att kunna använda flera butiker måste du förbereda din integreringsmiljö:

1. **Konfigurera vägar eller platser**—ange hur inkommande URL:er hanteras av Adobe Commerce

   - [Vägar för separata domäner](#configure-routes-for-separate-domains)
   - [Platser för delade domäner](#configure-locations-for-shared-domains)

1. **Konfigurera webbplatser, butiker och butiksvyer**—configure using the Adobe Commerce Admin UI
1. **Ändra variabler**—ange värdena för `MAGE_RUN_TYPE` och `MAGE_RUN_CODE` variabler i `magento-vars.php` fil
1. **Driftsätt och testa miljöer**—driftsätta och testa `integration` bankkontor

>[!TIP]
>
>Du kan använda en lokal miljö för att konfigurera flera webbplatser eller butiker. Se anvisningarna för Cloud Docker för att [Konfigurera flera webbplatser eller butiker](https://developer.adobe.com/commerce/cloud-tools/docker/configure/multiple-sites/).

### Konfigurationsuppdateringar för Pro-miljöer

{{pro-self-service-warning}}

### Konfigurera vägar för separata domäner

Rutorna definierar hur inkommande URL:er ska behandlas. Flera arkiv med unika domäner kräver att du definierar varje domän i `routes.yaml` -fil. Hur du konfigurerar vägar beror på hur du vill att webbplatsen ska fungera.

**Konfigurera vägar i en integreringsmiljö**:

1. Öppna `.magento/routes.yaml` i en textredigerare.

1. Definiera domänen och underdomänerna. The `mymagento` värdet upstream är samma värde som egenskapen name i `.magento.app.yaml` -fil.

   ```yaml
   "http://{default}/":
       type: upstream
       upstream: "mymagento:http"
   
   "http://<second-site>.{default}/":
       type: upstream
       upstream: "mymagento:http"
   ```

1. Spara ändringarna i `routes.yaml` -fil.

1. Fortsätt till [Konfigurera webbplatser, butiker och butiksvyer](#set-up-websites-stores-and-store-views).

### Konfigurera platser för delade domäner

Där flödeskonfigurationen definierar hur URL-adresserna behandlas, `web` -egenskapen i `.magento.app.yaml` -filen definierar hur programmet exponeras för webben. Webb _platser_ tillåter mer granularitet för inkommande begäranden. Om din domän till exempel är `store.com`kan du använda `/first` (standardplats) och `/second` för begäranden till två olika butiker som delar en domän.

**Konfigurera en ny webbplats**:

1. Skapa ett alias för roten (`/`). I det här exemplet är alias `&app` på rad 3.

   ```yaml
   web:
       locations:
           "/": &app
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
   ```

1. Skapa en vidarekoppling för webbplatsen (`/website`) och referera till roten med hjälp av aliaset från föregående steg.

   Aliaset tillåter `website` om du vill komma åt värden från rotplatsen. I det här exemplet har webbplatsen `passthru` står på rad 21.

   ```yaml
   web:
       locations:
           "/": &app
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/media":
               root: "pub/media"
               ...
           "/static":
               root: "pub/static"
               allow: true
               scripts: false
               passthru: "/front-static.php"
               rules:
                   ^/static/version\d+/(?<resource>.*)$:
                       passthru: "/static/$resource"
           "/<website>": *app
             ...
   ```

**Konfigurera en plats med en annan katalog**:

1. Skapa ett alias för roten (`/`) och för de statiska (`/static`).

   ```yaml
   web:
       locations:
           "/": &root
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/static": &static
               root: "pub/static"
   ```

1. Skapa en underkatalog för webbplatsen under `pub` katalog: `pub/<website>`

1. Kopiera `pub/index.php` till `pub/<website>` och uppdatera `bootstrap` bana (`/../../app/bootstrap.php`).

   ```
   try {
       require __DIR__ . '/../../app/bootstrap.php';
   } catch (\Exception $e) { 
   ```

1. Skapa en vidarekoppling för `index.php` -fil.

   ```yaml
   web:
       locations:
           "/": &root
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/media":
               root: "pub/media"
               ...
           "/static": &static
               root: "pub/static"
               allow: true
               scripts: false
               passthru: "/front-static.php"
               rules:
                   ^/static/version\d+/(?<resource>.*)$:
                       passthru: "/static/$resource"
           "/<website>":
               <<: *root
               passthru: "<website>/index.php"
           "/<website>/static": *static
             ...
   ```

1. Verkställ och skicka de ändrade filerna.

   - `pub/<website>/index.php` (Om den här filen finns i `.gitignore`, kan push-funktionen kräva kraftalternativet.)
   - `.magento.app.yaml`

### Konfigurera webbplatser, butiker och butiksvyer

I _Administratörsgränssnitt_, konfigurera din Adobe Commerce **Webbplatser**, **Lager** och **Lagra vyer**. Se [Konfigurera flera webbplatser, butiker och butiksvyer i administratören](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-admin.html) i _Konfigurationshandbok_.

Det är viktigt att du använder samma namn och kod för dina webbplatser, butiker och butiksvyer från din administratör när du konfigurerar din lokala installation. Du behöver dessa värden när du uppdaterar `magento-vars.php` -fil.

### Ändra variabler

I stället för att konfigurera en virtuell NGINX-värd skickar du `MAGE_RUN_CODE` och `MAGE_RUN_TYPE` variabler med `magento-vars.php` i projektets rotkatalog.

**Skicka variabler med `magento-vars.php` fil**:

1. Öppna `magento-vars.php` i en textredigerare.

   The [standard `magento-vars.php` fil](https://github.com/magento/magento-cloud/blob/master/magento-vars.php) ska se ut så här:

   ```php
   <?php
   // enable, adjust and copy this code for each store you run
   // Store #0, default one
   //if (isHttpHost("example.com")) {
   //    $_SERVER["MAGE_RUN_CODE"] = "default";
   //    $_SERVER["MAGE_RUN_TYPE"] = "store";
   //}
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
           return false;
       }
       return $_SERVER['HTTP_HOST'] === $host;
   }
   ```

1. Flytta kommenterade `if` blockera så att den _efter_ den `function` och inte längre kommenterade.

   ```php
   <?php
   // enable, adjust and copy this code for each store you run
   // Store #0, default one
   
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
           return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("example.com")) {
       $_SERVER["MAGE_RUN_CODE"] = "default";
       $_SERVER["MAGE_RUN_TYPE"] = "store";
   }
   ```

1. Ersätt följande värden i `if (isHttpHost("example.com"))` block:
   - `example.com`- med bas-URL:en för _webbplats_
   - `default`- med den unika KODEN för _webbplats_ eller _butiksvy_
   - `store`—med ett av följande värden:
      - `website`—load the _webbplats_ i butiken
      - `store`—load a _butiksvy_ i butiken

   För flera platser som använder unika domäner:

   ```php
   <?php
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
       return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("second.store.com")) {
       $_SERVER["MAGE_RUN_CODE"] = "<second-site>";
       $_SERVER["MAGE_RUN_TYPE"] = "website";
   }elseif (isHttpHost("store.com")){
       $_SERVER["MAGE_RUN_CODE"] = "base";
       $_SERVER["MAGE_RUN_TYPE"] = "website";
   }
   ```

   För flera webbplatser med samma domän måste du kontrollera _värd_ och _URI_:

   ```php
   <?php
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
       return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("store.com")) {
      $code = "base";
      $type = "website";
   
      $uri = explode('/', $_SERVER['REQUEST_URI']);
      if (isset($uri[1]) && $uri[1] == 'second') {
        $code = '<second-site>';
        $type = 'website';
      }
      $_SERVER["MAGE_RUN_CODE"] = $code;
      $_SERVER["MAGE_RUN_TYPE"] = $type;
   }
   ```

1. Spara ändringarna i `magento-vars.php` -fil.

### Distribuera och testa på integreringsservern

Gör ändringar i er Adobe Commerce i molninfrastruktursintegreringsmiljö och testa er webbplats.

1. Lägg till, implementera och skicka kodändringar till fjärrgrenen.

   ```bash
   git add -A && git commit -m "Implement multiple sites" && git push origin <branch-name>
   ```

1. Vänta tills distributionen är klar.

1. Efter distributionen öppnar du din Store-URL i en webbläsare.

   Använd formatet med en unik domän: `http://<magento-run-code>.<site-URL>`

   Exempel: `http://french.master-name-projectID.us.magentosite.cloud/`

   Använd formatet med en delad domän: `http://<site-URL>/<magento-run-code>`

   Exempel: `http://master-name-projectID.us.magentosite.cloud/french/`

1. Testa webbplatsen noggrant och sammanfoga koden med `integration` för vidare driftsättning.

## Distribuera till mellanlagring och produktion

Följ distributionsprocessen för [driftsätta till förproduktion och produktion](../deploy/staging-production.md). För Starter- och Pro-miljöer använder du [!DNL Cloud Console] för att föra över kod mellan olika miljöer.

Adobe rekommenderar att du gör en fullständig testning i mellanlagringsmiljön innan du går vidare till produktionsmiljön. Gör kodändringar i integreringsmiljön och börja distribuera i olika miljöer igen.

<!-- link definitions -->

[config-multiweb]: https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-overview.html
