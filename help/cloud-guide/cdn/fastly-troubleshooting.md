---
title: Snabbt felsökning
description: Lär dig hur du felsöker och hanterar snabbuppdateringsmodulen och tjänsterna för Adobe Commerce.
feature: Cloud, Configuration, Cache, Services
exl-id: e4c47035-cbad-4838-8d44-fa5eaaac42d1
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 0%

---

# Snabbt felsökning

Använd följande information för att felsöka och hantera snabbuppdateringsmodulen för CDN för Magento 2 i dina Adobe Commerce i miljöer med molninfrastrukturprojekt. Du kan till exempel undersöka svarshuvudets värden och cachningsbeteendet för att lösa problem med snabb service och prestanda.

I Pro Production- och Staging-miljöer kan du använda [New Relic loggar](../monitor/log-management.md) för att visa och analysera snabbt CDN- och WAF-loggdata för att felsöka fel och prestandaproblem.

>[!NOTE]
>
>Mer information om hur du konfigurerar och konfigurerar snabbt finns i [Konfigurera snabbt](fastly.md).

## Hitta snabbt tjänst-ID

Du behöver ett snabb service-ID för att konfigurera snabbt från administratören eller för att skicka in snabba API-begäranden för avancerad snabb konfiguration och felsökning.

Om Snabbt är aktiverat i din projektmiljö kan du hämta service-ID:t från administratören. Se [Få inloggningsuppgifter snabbt](fastly-configuration.md#get-fastly-credentials).

Utvecklare och avancerade VCL-användare kan använda anpassad VCL för att hämta service-ID:t med hjälp av variabeln Fast `req.service_id`. Du kan till exempel lägga till `req.service_id` till det anpassade loggningsdirektivet i ditt VCL för att hämta tjänstens ID-värde:

```json
log {"syslog"} req.service_id {" my_logging_endpoint_name :: "}
```

Du kan använda samma VCL för produktions- och mellanlagringsmiljöer. Se [Konfigurera vcl_log](https://support.fastly.com/hc/en-us/community/posts/360040447172-How-to-configure-vcl-log).

## Problem med webbplatsprestanda, rensning och cache

Använd följande lista för att identifiera och felsöka problem som rör Snabb tjänstkonfiguration för din Adobe Commerce i molninfrastrukturmiljö.

- **Menyn Butik visas inte och fungerar inte**- Du kan använda en länk eller tillfällig länk direkt till den ursprungliga servern i stället för att använda den aktiva webbplatsens URL, eller så använde du `-H "host:URL"` i en [cURL, kommando](#check-live-site-through-fastly). Om du snabbt kringgår den ursprungliga servern fungerar inte huvudmenyn och felaktiga rubriker visas som tillåter cachelagring på webbläsarsidan.

- **Övre navigering fungerar inte**- Den översta navigeringen är beroende av ESI-bearbetning (Edge Side Includes) som aktiveras när du överför de vanliga VCL-kodfragmenten för Magento snabbt. Om navigeringen inte fungerar [ladda upp den snabba VCL-filen](fastly-configuration.md#upload-vcl-to-fastly) och kontrollera om webbplatsen.

- **Geo-location/GeoIP fungerar inte**— Standardvärdet för VCL-kodfragment för Magento snabbt lägger till landskoden i URL:en. Om landskoden inte fungerar [ladda upp den snabba VCL-filen](fastly-configuration.md#upload-vcl-to-fastly) och kontrollera om webbplatsen.

- **Sidorna cachelagras inte**—Som standard cachelagras inte sidor med `Set-Cookies` header. Adobe Commerce ställer in cookies även på cachebara sidor (TTL > 0). Med standardinställningen Magento-VCL raderas dessa cookies på cacheable-sidor. Om sidorna inte cachelagras, [ladda upp den snabba VCL-filen](fastly-configuration.md#upload-vcl-to-fastly) och kontrollera om webbplatsen.

  Detta kan även inträffa om ett sidblock i en mall markeras som oåtkomligt. I så fall beror problemet troligen på att en modul från tredje part eller ett tillägg blockerar eller tar bort Adobe Commerce-huvuden. Information om hur du löser problemet finns i [X-Cache innehåller bara MISS, ingen HIT](#x-cache-contains-only-miss-no-hit).

- **Rensningsbegäranden misslyckas**—Följande fel returneras snabbt när du skickar en rensningsbegäran:

  ```text
  The purge request was not processed successfully.
  ```

  Problemet kan bero på något av följande:

   - Ogiltiga snabbreferenser i snabbtjänstkonfigurationen för Adobe Commerce i molninfrastrukturens projektmiljö
   - Ogiltig kod i ett anpassat VCL-fragment

  Information om hur du löser problemet finns i [Fel vid snabb rensning av cache i molnet](https://support.magento.com/hc/en-us/articles/115001853194-Error-purging-Fastly-cache-on-Cloud-The-purge-request-was-not-processed-successfully-) i Adobe Commerce Help Center.

## 503 fel från Snabb

Om du snabbt returnerar 503 timeout-fel kontrollerar du felloggarna och felsidan 503 för att identifiera rotorsaken.

>[!NOTE]
>
>Om timeout inträffar när gruppåtgärder körs kan du [förlänga tidsgränsen för Admin](fastly-custom-cache-configuration.md#extend-fastly-timeout).

Om du får ett 503-fel bör du kontrollera felloggen för produktions- eller mellanlagringsmiljön och PHP-åtkomstloggen för att felsöka problemet.

**Kontrollera felloggarna**:

- [Fellogg](../test/log-locations.md#application-logs)

  ```text
  /var/log/platform/<project-ID>/error.log
  ```

  Den här loggen innehåller fel från programmet eller PHP-motorn, till exempel `memory_limit` eller `max_execution_time exceeded` fel. Om du inte hittar några snabbrelaterade fel kontrollerar du PHP-åtkomstloggen.

- PHP-åtkomstlogg

  ```text
  /var/log/platform/<project-ID>/php.access.log
  ```

  Sök i loggen efter HTTP 200-svar efter den URL som returnerade felet 503. Om du hittar 200-svaret innebär det att Adobe Commerce returnerade sidan utan fel. Detta anger att problemet kan ha inträffat efter det intervall som överskrider `first_byte_timeout` som anges i snabbtjänstkonfigurationen.

När ett 503-fel inträffar returnerar Snabb orsaken på fel- och underhållssidan. Du kanske inte kan se orsaken om du har lagt till kod för en [anpassad svarssida](fastly-custom-response.md). Om du vill visa orsakskoden på standardfelsidan kan du ta bort HTML-koden för den anpassade felsidan.

**Så här kontrollerar du snabbt felsidan för 503**:

{{admin-login-step}}

1. Klicka **Lager** > **Inställningar** > **Konfiguration** > **Avancerat** > **System**.

1. Expandera i den högra rutan **Helsidescache**.

1. I **Snabb konfiguration** sektion, expandera **Anpassade syntetiska sidor** som bilden nedan visar.

   ![Anpassad felsida 503](../../assets/cdn/fastly-custom-synthetic-pages-edit-html.png)

1. Klicka **Ange HTML**.

1. Ta bort den anpassade koden. Du kan spara det i ett textprogram och lägga tillbaka det senare.

1. Klicka **Överför** för att skicka uppdateringar till Fast.

1. Klicka **Spara konfiguration** överst på sidan.

1. Öppna URL:en som orsakade felet 503 igen. Returnerar snabbt en felsida med orsaken som visas i följande exempel.

   ![Snabbt fel](../../assets/cdn/fastly-503-example.png)

## Apex och underdomäner som redan är kopplade till ett Fast-konto

Om API-domänen och underdomänerna för ditt Adobe Commerce i ett molninfrastrukturprojekt redan är kopplade till ett befintligt Fast-konto med ett tilldelat tjänst-ID, kan du inte starta förrän du uppdaterar din snabbkonfiguration:

- Uppdatera API- och underdomänskonfigurationen på det befintliga snabbkontot. Se [Flera snabbkonton och tilldelade domäner](fastly.md#domain).

- [Aktivera och konfigurera snabbt](fastly-configuration.md#enable-fastly-caching) och fylla i [DNS-konfiguration](../launch/checklist.md#update-dns-configuration-with-production-settings)

## Verifiera eller felsök snabbt tjänster

Du kan felsöka prestanda- eller cachelagringsproblem för en Adobe Commerce på en molninfrastrukturwebbplats genom att testa webbplatsens URL:er och undersöka de rubrikvärden som returneras i svaret.

### Kontrollera publicerad webbplats snabbt

Använd API:t Snabb för att kontrollera  `Fastly-Magento-VCL-Uploaded` och `X-Cache` svarsrubriker som returneras från din publicerade webbplats.

API-begäranden skickas snabbt via tillägget Fast för att få svar från era ursprungliga servrar. Om svaret returnerar felaktiga rubriker testar du [ursprungsservrar direkt](#bypass-fastly-cache-to-check-adobe-commerce-sites).

**Kontrollera svarshuvuden**:

1. Använd följande i en terminal: `curl` för att testa din webbplats-URL:

   ```bash
   curl https://<live URL> -vo /dev/null -H Fastly-Debug:1
   ```

   Använd kommandot `--resolve` som åsidosätter DNS-namnmatchning.

   ```bash
   curl -svo /dev/null --resolve '<your_hostname>:443:<IP-address-of-cache-node>' <https-URL>
   ```

   >[!NOTE]
   >
   >Om du vill använda kommandot med `--resolve` måste du ha TLS aktiverat med Snabbt via ett SSL/TLS-certifikat och hitta cachenodens IP-adress.

1. I svaret kontrollerar du att [rubriker](#check-cache-hit-and-miss-response-headers) för att säkerställa att Fastly fungerar. Du bör se följande unika rubriker i svaret:

   ```http
   < Fastly-Magento-VCL-Uploaded: yes
   < X-Cache: HIT, MISS
   ```

Om rubrikerna inte har rätt värden kan du läsa följande information:

- [Kontrollera VCL-överföring](#fastly-vcl-has-not-been-uploaded)

- [X-Cache innehåller bara MISS, ingen HIT](#x-cache-contains-only-miss-no-hit)

### Hoppa över snabbcachelagring för att kontrollera Adobe Commerce webbplatser

Om snabbtjänsten returnerar felaktiga rubriker kan du skapa ett VCL-kodfragment som gör att du kan skicka begäranden som kringgår snabbcachen. Se [Kringgå snabbcache](fastly-vcl-bypass-to-origin.md).

När du har lagt till VCL-fragmentet använder du cURL-kommandon för att skicka begäranden till den ursprungliga servern från den angivna IP-adressen. Kontrollera sedan om svaren innehåller fel.

### Kontrollera headers för HIT- och MISS-svar i cache

Kontrollera att det returnerade svaret innehåller följande information:

- Innehåller `X-Magento-Tags` header

- Värdet för `Fastly-Module-Enabled` header är antingen `Yes` eller versionsnumret för modulen Fastly for CDN Magento 2 som installerats i projektmiljön

- [Cache-Control: max-age](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) är större än 0

- [Pragma](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.32) inställningen är `cache`

Följande utdrag från utdata för cURL-kommandot visar de korrekta värdena för `Pragma`, `X-Magento-Tags`och `Fastly-Module-Enabled` sidhuvuden:

```terminal
* STATE: INIT => CONNECT handle 0x600057800; line 1402 (connection #-5000)
* Rebuilt URL to: https://www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud/
* Added connection 0. The cache now contains 1 members
* Trying 192.0.2.31...
* STATE: CONNECT => WAITCONNECT handle 0x600057800; line 1455 (connection #0)

% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* Connected to www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud (54.229.163.31) port 443 (#0)

* STATE: WAITCONNECT => SENDPROTOCONNECT handle 0x600057800; line 1562 (connection #0)
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* ALPN, offering h2

... portion omitted for brevity ...

< Set-Cookie: mage-messages=%5B%5D; expires=Wed, 22-Nov-2017 17:39:58 GMT; Max-Age=31536000; path=/
< Pragma: cache
< Expires: Wed, 23 Nov 2016 17:39:56 GMT
< Cache-Control: max-age=86400, public, s-maxage=86400, stale-if-error=5, stale-while-revalidate=5
< X-Magento-Tags: cb_welcome_popup store cb cb_store_info_mobile cb_header_promotional_bar cb_store_info cb_discount-promo-bar cpg_2 cb_83 cb_81 cb_84 cb_85 cb_86 cb_87 cb_88 cb_89 p5646 catalog_product p5915 p6040 p6197 p6227 p7095 p6109 p6122 p6331 p7592 p7651 p7690
< Fastly-Module-Enabled: yes
< Strict-Transport-Security: max-age=31536000
    < Content-Security-Policy: upgrade-insecure-requests
    < X-Content-Type-Options: nosniff
    < X-XSS-Protection: 1; mode=block
    < X-Frame-Options: SAMEORIGIN
    < X-Platform-Server: i-dff64b52
    <
    * STATE: PERFORM => DONE handle 0x600057800; line 1955 (connection #0)
    * multi_done
      0     0    0     0    0     0      0      0 --:--:--  0:00:02 --:--:--     0
    * Connection #0 to host www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud left intact
```

>[!NOTE]
>
>Mer information om träffar och missar finns i [Förstå headers för cache-HIT och MISS med skärmade tjänster](https://docs.fastly.com/guides/performance-tuning/understanding-cache-hit-and-miss-headers-with-shielded-services) i Snabbas dokumentation.

### Åtgärda fel i svarshuvuden

I det här avsnittet ges förslag på hur du löser fel som returneras när du kontrollerar svarshuvuden med API:t Snabbt.

#### Modulen Snabbt är inte aktiverad

Om snabbmodulen inte är aktiverad (`Fastly-Module-Enabled: no`) eller om sidhuvudet saknas, [använda SSH för att logga in](../development/secure-connections.md#connect-to-a-remote-environment) till projektet. Kör sedan följande kommando för att kontrollera modulens status.

```bash
php bin/magento module:status Fastly_Cdn
```

Baserat på den returnerade statusen kan du uppdatera snabbkonfigurationen med följande instruktioner.

- `Module does not exist`—Om modulen inte finns [installera och konfigurera](https://github.com/fastly/fastly-magento2/blob/master/Documentation/INSTALLATION.md) Snabbt CDN-modul för Magento 2 i en integrationsgren. Aktivera och konfigurera modulen när installationen är klar. Se [Konfigurera snabbt](fastly-configuration.md).

- `Module is disabled`—Om modulen Snabbt är inaktiverad uppdaterar du miljökonfigurationen på en `integration` i din lokala miljö för att aktivera den. Flytta sedan ändringarna till Förproduktion. Se [Hantera tillägg](../store/extensions.md#install-an-extension).

  Om du [Konfigurationshantering](../store/store-settings.md#configure-store)kontrollerar du statusen för snabbast-CDN-modulen i dialogrutan `app/etc/config.php` konfigurationsfilen innan du skickar ändringarna till produktions- eller mellanlagringsmiljön.

  Om modulen inte är aktiverad (`Fastly_CDN => 0`) i `config.php` tar du bort filen och kör följande kommando för att uppdatera `config.php` med de senaste konfigurationsinställningarna.

  ```bash
  bin/magento magento-cloud:scd-dump
  ```

#### Snabb VCL har inte överförts

Om Snabbt VCL inte har överförts (`Fastly-Magento-VCL-Uploaded`: `false`), använd *Överför VCL* i Admin för att överföra den. Se [Ladda upp VCL-fragment snabbt](fastly-configuration.md#upload-vcl-to-fastly).

#### X-Cache innehåller bara MISS, ingen HIT

Om `X-Cache` header contains `HIT` (`HIT, HIT` eller `HIT, MISS`) visas att det cachelagrade innehållet returneras snabbt.

Om `X-Cache` header is `MISS, MISS` och innehåller inte `HIT`, kör `curl` igen för att kontrollera att sidan inte nyligen rensades från cachen.

Om du får samma resultat använder du [`curl` kommandon](#check-live-site-through-fastly) och verifiera [svarsrubriker](#check-cache-hit-and-miss-response-headers):

- `Pragma` är `cache`
- `X-Magento-Tags` exists
- `Cache-Control: max-age` är större än 0

Om problemet kvarstår är det troligt att ett annat tillägg återställer dessa rubriker. Upprepa följande procedur i mellanlagringsmiljön genom att inaktivera alla tillägg och aktivera om var och en för att avgöra vilket tillägg som återställer rubrikerna. När du har identifierat tillägget som orsakar problemet måste du inaktivera det i produktionsmiljön.

**Så här identifierar du ett tillägg som återställer svarshuvuden:**

{{admin-login-step}}

1. Navigera till **Lager** > **Inställningar** > **Konfiguration** > **Avancerat** > **Avancerat**.

1. I *Inaktivera modulutdata* i den högra rutan, hitta alla dina tillägg och inaktivera dem.

1. Klicka **Spara konfiguration**.

1. Klicka **System** > **verktyg** > **Cachehantering**.

1. Klicka **Rensa Magento-cache**.

1. Utför följande steg för varje tillägg som kan orsaka problem med snabbrubriker:

   - Aktivera ett tillägg i taget, spara konfigurationen och tömma Adobe Commerce-cachen.

   - Kör [`curl` kommandon](#check-live-site-through-fastly) för att verifiera [svarsrubriker](#check-cache-hit-and-miss-response-headers).

   Upprepa den här processen för varje tillägg. Om rubrikerna för snabbsvar inte längre visas har du identifierat det tillägg som orsakar problem med Snabbt.

När du har identifierat det tillägg som återställer snabbrubriker kontaktar du tilläggsutvecklaren för ytterligare hjälp. Vi kan inte tillhandahålla korrigeringar eller uppdateringar för att få tillägg från tredje part att fungera med Snabb cachelagring.

## Snabb återställning

Om uppdateringar av anpassade VCL-kodfragment eller andra snabba konfigurationsändringar gör att fel bryts eller returneras på en Adobe Commerce på molninfrastrukturen använder du API:t Snabbt [activate](https://docs.fastly.com/api/config#version_0b79ae1ba6aee61d64cc4d43fed1e0d5) om du vill återställa till en tidigare VCL-version. Du kan inte återställa VCL-versionen från administratören.

**Återställa VCL-versionen**:

1. Om du vill visa en lista över tillgängliga VCL-versioner för en tjänst kör du följande kommando

   ```bash
   curl -H "Fastly-Key: <FASTLY_API_TOKEN>" -H "Accept: application/json" https://api.fastly.com/service/<FASTLY_SERVICE_ID>/version
   ```

1. Kör följande kommando för att ändra den aktiva VCL-versionen till en angiven version.

   ```bash
   curl -H "Fastly-Key: <FASTLY_API_TOKEN>" -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -X PUT https://api.fastly.com/service/<FASTLY_SERVICE_ID>/version/<VERSION_ID>/activate
   ```

Mer information om hur du använder API:t Snabb för att granska och hantera VCL finns i [Hantera VCL med API](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api).
