---
title: Cloud Patches for Commerce
description: Se en lista över de senaste förbättringarna av Cloud Patches-paketet.
recommendations: noDisplay, catalog
last-substantial-update: 2024-01-16T00:00:00Z
exl-id: ae6b511b-a37d-4776-9a5e-ad7d9f9f6611
source-git-commit: 1e06545340cb63df483d1db5b2a890499e99e6d3
workflow-type: tm+mt
source-wordcount: '2175'
ht-degree: 0%

---

# Cloud Patches for Commerce

The [Molnkorrigeringar](https://github.com/magento/magento-cloud-patches) paket innehåller en uppsättning nödvändiga korrigeringsfiler som förbättrar integreringen av alla Adobe Commerce-versioner med molnmiljöer och stöder snabb leverans av viktiga korrigeringsfiler.

Cloud Patches for Commerce-paketet är beroende av ECE-verktygspaketet och installeras och uppdateras när du installerar eller uppdaterar ECE-verktygspaketet. Du kan också använda och hantera molnkorrigeringar för Commerce som ett fristående paket för att tillämpa korrigeringar på ett Adobe Commerce-projekt som inte finns på molnplattformen. I versionsinformationen beskrivs de senaste förbättringarna av det här paketet.

>[!TIP]
>
>Uppdatera till [den senaste versionen av verktygen](../dev-tools/update-package.md).

>[!NOTE]
>
>Se [Tillämpa patchar](../development/apply-patches.md) för instruktioner om hur du använder korrigeringsfiler i dina projekt.

The `magento/magento-cloud-patches` paketet använder följande versionssekvens: `<major>.<minor>.<patch>`

<!--Add release notes below-->

## v1.0.25 {#latest}

Releasedatum: 16 januari 2024

- **Förbättringar av cache**-Den här korrigeringen förbättrar effektiviteten i layoutcachen och minskar minnesanvändningen avsevärt för Adobe Commerce version 2.4.4 och senare.<!-- MCLOUD-11514 -->
- **Förbättringar av CRON-jobb**-Den här korrigeringen åtgärdar ett problem där missade jobb i onödan väntar på cron job locks för Adobe Commerce version 2.4.4 och senare.<!-- MCLOUD-11329 -->

## v1.0.24

Releasedatum: 15 september 2023

- **Prestandaförbättring**-Den här korrigeringen åtgärdar ett problem som påverkar prestandan genom att minska antalet gånger som samma distributionskonfigurationer läses in för Adobe Commerce 2.4.6 till 2.4.6-p1<!-- MCLOUD-10604 -->

## v1.0.23

Releasedatum: 31 juli 2023

- **Korrigeringen MCLOUD-10604 har tagits bort**-Den här korrigeringen flyttades till QPT.<!-- MCLOUD-10736 -->

## v1.0.22

Releasedatum: 19 juni 2023

- **Förbättrad QPT CLI-guide/utdata**- En varning har lagts till i QPT CLI-guiden/utdatafilen som påminner dig om att verifiera korrigeringsinformation och -krav om det finns beroenden.<!-- ACP2E-1963 -->
- **Lagt till patchar för Commerce 2.4.6:**
   - Korrigerade `regexp cache tag` validering.<!-- MCLOUD-10226 -->
   - Förbättrade prestanda genom att minska antalet gånger som samma distributionskonfigurationer läses in.<!-- MCLOUD-10604 -->
- **Lagt till patchar för Commerce 2.3.7 till 2.4.6**—Korrigerade ett problem som orsakade en ökning med ett slumpmässigt värde i stället för en ökning med 1 för `catalog_product_entity_*` tabeller.<!-- MCLOUD-10032 -->
- **Lagt till patchar för Commerce 2.4.0 till 2.4.6**—Ett fel som anger att `The file can't be deleted. Warning!unlink: No such file or directory`som inträffade när JS/CSS-cache tömdes från administratören.<!-- MCLOUD-10279 -->

## v1.0.21

Releasedatum: 10 mars 2023

- **Förbättrat stöd för PHP 8.2**—Korrigerade kompatibilitetsproblem med vissa PHP 8.2.x-versioner som stöder Commerce 2.4.6.

## v1.0.20

Releasedatum: 27 oktober 2022

- **Lagt till förbättringar av L2-cache**- Den här korrigeringen åtgärdar ett problem med att tömma den lokala L2-cachen för Commerce version 2.4.0 och 2.4.1.<!-- MCLOUD-7845 -->

## v1.0.19

Releasedatum: 13 september 2022

- **Förbättrat stöd för PHP 8.1**—Kompatibilitetsproblem med vissa PHP 8.1.x-versioner har åtgärdats.

## v1.0.18

Releasedatum: 11 augusti 2022

Viktig patch för Adobe Commerce 2.4.5:

- **Utfärda order med Braintree-betalningar**- Korrigeringen åtgärdar ett kritiskt problem som förhindrar administratörer från att göra nya beställningar eller beställningar.<!-- MCLOUD-9137 -->

Se [Administratören kan inte skapa en order eller beställa om när Braintree-betalning är aktiverat](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/admin-cant-create-order-reorder-when-braintree-payment-enabled.html).

## v1.0.17

Releasedatum: 24 maj 2022

Fasta begränsningar för säkerhetspatchar i `patches.json` -fil.

## v1.0.16

Releasedatum: 31 mars 2022

Viktig patch för Adobe Commerce 2.3.3-p1 och senare:

Uppdaterade patchar för att lösa en **kritisk** sårbarhet som leder till oautentiserad fjärrexekvering av kod.<!-- MCLOUD-8479 -->

Se [Adobe säkerhetsbulletin APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.15

Releasedatum: 10 mars 2022

- **Stöd för PHP 8.1**- Stöd för PHP 8.1 har lagts till och stödet för PHP 7.0 och 7.1 har tagits bort.
- **Lagt till patch för Adobe Commerce 2.3.3**—Fast valuta visas på produktsidan.

## v1.0.14

Releasedatum: 13 februari 2022

Viktig patch för Adobe Commerce 2.3.3-p1 och senare:

Lagt till en korrigeringsfil för att lösa en **kritisk** sårbarhet som leder till oautentiserad fjärrexekvering av kod.<!-- MCLOUD-8461 -->

Se [Adobe säkerhetsbulletin APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.13

Releasedatum: 25 oktober 2021

- **Uppdatera Monolog**—Uppdaterat minimiversionen som krävs för `monolog` paketera till `^2.3`.<!-- ACMP-1263 -->
- **Inkompatibel PHP-metod**—Fixed compatible PHP method for Adobe Commerce versions 2.4.3 and 2.3.7-p1.<!-- AC-384 -->
- **PHP-fel**—Fixed a `PHP error 'Undefined variable: errorMessage' ...` fel som inträffade när en korrigering skulle tillämpas.<!-- ACP2E-138 -->

## v1.0.12

Releasedatum: 12 augusti 2021

Viktig patch för Adobe Commerce 2.4.3 och 2.3.7-p1:

- **Problem med API-hastighetsbegränsning**- Den här korrigeringen åtgärdar en standardhastighetsgräns som förhindrade att webb-API:er bearbetar begäranden med mer än 20 objekt i en array. Den här korrigeringen höjer standardvärdet för hastighetsgränsen. Se Adobe Commerce [2.4.3 Versionsinformation](https://devdocs.magento.com/guides/v2.4/release-notes/commerce-2-4-3.html#apply-mc-43048__set_rate_limits__243patch-to-address-issue-with-api-rate-limiting) och [2.3.7 Versionsinformation](https://devdocs.magento.com/guides/v2.3/release-notes/2-3-7-p1.html#apply-mc-43048__set_rate_limits__237-p1patch-to-address-issue-with-api-rate-limiting).<!-- MC-43048 -->

## v1.0.11

Releasedatum: 29 juli 2021

- **Ett problem som orsakades av att navigeringsrutan i B2B-lager användes har åtgärdats**- För kunder som har implementerat navigeringspatchen för B2B-lager åtgärdar den här korrigeringen ett `Undefined offset` fel som visas på söksidan efter att butiksvyn har växlats.<!--MCLOUD-5287-->

- **Betalpal Checkout-korrigering**—Korrigerar ett Adobe Commerce 2.3.7-problem med PayPal Express där det tidigare inköpspriset visas.<!--MC-42674-->

- **Stöd för lagningskategori**- Stöd för bearbetning av korrigeringskategorier och ursprungskällor som tilldelats kvalitetspatchar har lagts till. Med kategorierna kan kunderna använda filter och sortering för att hitta patchar snabbare när de använder [Verktyget Kvalitetspatchar](https://github.com/magento/quality-patches) och Site-wide Analysis Tool (SWAT). <!--MC-38577-->

## v1.0.10

Releasedatum: 10 maj 2021

- **Kompatibilitet med Adobe Commerce 2.3.7**—Konflikt i matchade dispositionsberoenden vid installation på Adobe Commerce 2.3.7 har åtgärdats.<!--MC-42131-->
- **Korrigerat ett problem som orsakats av att en lagning har tillämpats flera gånger**- Om du använder en paketerad patch (en som innehåller andra borttagna patchar) mer än en gång kan de inkluderade borttagna paketen återställas. Alla patchar används nu bara en gång. Om du försöker tillämpa samma paket igen visas ett meddelande om att korrigeringen redan har tillämpats.<!--MC-41912-->
- **Navigeringsruta i B2B-lager**—Ett annat problem som gjorde att navigering i flera lager inte kunde visa alla produktalternativ när användaren aktiverade den delade B2B-katalogen har åtgärdats.<!--MCLOUD-7742-->

## v1.0.9

Releasedatum: 1 februari 2021

- **Navigeringsruta i B2B-lager**—Ett problem som hindrade navigering i flera lager från att visa alla produktalternativ när den delade B2B-katalogen var aktiverad har åtgärdats.<!--MCLOUD-6923-->
- **Kompatibilitet med PHP 7.4**—Ett kompatibilitetsproblem med PHP 7.4 i molnet har korrigerats.<!--MCLOUD-7367-->
- **Föråldrade patchar blir synliga**—Korrigerade ett problem med molnkorrigeringar där borttagna korrigeringar visas i patchtabellen efter att en ersättningskorrigering som innehåller hela innehållet i den borttagna korrigeringen har lagts till. Det här kan hända om du har använt en patch som kombinerar flera andra plåster.<!--MC-40626-->
- **Tysta fel vid tillämpning av korrigeringar**—Ett problem med molnkorrigeringar där `git apply` i vissa miljöer gick det inte att använda korrigeringsfiler.<!--MC-40529-->

## v1.0.8

Releasedatum: 14 oktober 2020

- **Kompatibilitetsuppdateringar för magento/magento-cloud-patches**—Uppdaterade `symfony` och `semver` versionsbegränsningar i `composer.json` för kompatibilitet med Adobe Commerce 2.4.1 och senare versioner.<!--MCLOUD-7111-->

## v1.0.7

Releasedatum: 14 oktober 2020

- **Redis-patchar för Adobe Commerce 2.3.0 till 2.3.5, 2.4.0**—Redis-korrigeringarna uppdaterades för att ge stöd för att lägga till produkter i en kategori när en nivå 2-cache implementerades. <!--MCLOUD-6659-->

- **Braintree VBE-patch**—Korrigerar ett fel som genererade ett fel när en administratör försökte visa en avvecklingsrapport för Braintree. <!--MCLOUD-6684-->

- Nu `ece-patches apply` kommandot använder Unix `patch` om du vill använda korrigeringsfiler om Git inte är tillgängligt på värdsystemet. <!--MCLOUD-7069-->

## v1.0.6

Utgivningsdatum:

- **Redis-korrigeringar för Adobe Commerce 2.3.0 - 2.3.4**—Optimera kommunikationen och förbättra prestandan
   - Minska storleken på nätverksöverföringar mellan Redis och Adobe Commerce
   - Åtgärda konkurrensförhållanden vid inläsning och skrivning av Redis
   - Skriv om bascachekortet för att hantera fel när du sparar
   - Minska Redis CPU-förbrukning<!--MCLOUD-6139-->

- **Redis-korrigeringar för Adobe Commerce 2.3.0 - 2.3.5**—Förbättra prestanda och åtgärda fel
   - Åtgärda implementeringen av cache-låset för att förhindra oändliga lås
   - Förbättra den nuvarande låsmekanismen
   - Implementera signerade lås för att förhindra upplåsning från parallella förfrågningar
   - Åtgärda följande fel som inträffar vid Redis-skrivåtgärd: `OOM command not allowed when used memory > maxmemory`
   - Korrigera bearbetning för rensad cache med `cat_p` som körs under produktuppdateringar<!--MCLOUD-6110-->

- Ett problem som orsakade ett fel när nödvändiga `amzn/amazon-pay-module` till Adobe Commerce i molninfrastrukturprojekt med Adobe Commerce v2.2.6 eller 2.3.5, som inte innehåller denna modul. Korrigeringsprocessen hoppar över `amzn/amazon-pay-module` korrigering om modulen inte är installerad.<!--MCLOUD-6588-->

## v1.0.5

Releasedatum: 26 juni 2020

- **Prestandaförbättringar i Redis**—Lägger till Redis-optimeringsfunktioner i Adobe Commerce version 2.3.3 och 2.3.4. Dessa korrigeringar ingick i Adobe Commerce version 2.3.5. Se [Prestandaförbättringar](https://devdocs.magento.com/guides/v2.3/release-notes/release-notes-2-3-5-commerce.html#performance-boosts) i _Versionsinformation om Adobe Commerce 2.3.5_.<!--MCLOUD-5771-->

- **New Relic logganrikare**—Lägger till det Monolog ProcessorInterface som krävs för att stödja förbättringar av loggningsfunktionerna i New Relic som introducerades i molnkomponenter i Commerce version 1.0.4. Den här korrigeringen krävs för att installera Adobe Commerce 2.1.x. Om korrigeringen inte tillämpas misslyckas bygget under `di:compile` -processen.<!--MCLOUD-6029-->

## v1.0.4

Releasedatum: 12 maj 2020

- **Amazon Pay-kassan**—Korrigerar ett problem med betalningswidgeten Amazon Pay som hindrade kunderna från att ändra betalningsmetoden på _Granska och betala_ under utcheckningsprocessen.<!--MCLOUD-5930-->

- **Produktvisning på kategorisida**—Ett problem som gjorde att produkter inte kunde visas på kategorisidan i har korrigerats _Visa alla sidor_ vy.<!--MCLOUD-5684-->

- **Page Builder - bildöverföring**—Korrigerar ett Page Builder-gränssnittsproblem som ibland orsakade följande fel när bilder överfördes till bildgalleriet: `Destination folder is not writable or does not exist`<!--MCLOUD-5837-->

- **Undvik onödiga varningar för webbplatskartor**- Lägger till ett nytt försök när fel uppstår under webbplatskartor och hoppar över e-postmeddelanden från kunder i fall där fel kan återställas automatiskt.<!--MCLOUD-3025-->

- **Förbättrade prestanda**—Ett prestandaproblem med `Magento\Framework\App\DeploymentConfig\Reader::load` som periodvis har haft långa laddningstider som påverkar webbplatsens prestanda. <!--MCLOUD-5650-->

- Uppdaterad korrigeringstilldelning för betalningsmetodkorrigeringar för betalningsmodulerna i stället för Magento baspaketet (magento/magento2-base) så att betalningskorrigeringarna bara tillämpas om betalningsmodulerna finns.<!--MCLOUD-5666-->

- Uppdaterade patchar för kompatibilitet med Magento Open Source.<!--MCLOUD-5701-->

## v1.0.3

Releasedatum: 28 april 2020

- Korrigering för korrigeringen &quot;FPC håller på att inaktiveras under distributioner&quot; som stöd för Adobe Commerce 2.3.5 har lagts till.

## v1.0.2

Releasedatum: 27 februari 2020

Den här versionen innehåller följande korrigeringar och viktiga korrigeringar:

- **Kompatibilitetsuppdateringar för magento/magento-cloud-patches**

   - Uppdaterade `symfony` och `semver` versionsbegränsningar i `composer.json` för kompatibilitet med Adobe Commerce 2.4 och senare versioner.<!--MAGECLOUD-5127-->

   - Uppdaterade begränsningar i `composer.json` för kompatibilitet med `ece-tools` 2002.0.22 och senare versioner av 2002.0.x.

- **PayPal Express-kassan**- Den publicerades den 12 februari 2020. Korrigeringen åtgärdar ett problem som påverkar beställningar som gjorts med PayPal Express Checkout där leveransadressen för ordern anger ett land som manuellt har angetts i textfältet i stället för valts i listrutan på sidan Leverans. Se hela patchbeskrivningen på sidan för hämtning av patchar.

- **Programdistributionsfix**- En patch har lagts till för att åtgärda ett problem som inaktiverade helsidescachen under distributionsprocessen. Den här programfixen gäller för Adobe Commerce 2.3.2 och senare versioner.

- **Scope-parameter för Async/Bulk API**—Den här korrigeringen har uppdaterats för att åtgärda ett syntaxfel i `composer.json` -fil. Detta gäller Magento Open Source 2.3.1 och 2.3.2. Se hela patchbeskrivningen på sidan för hämtning av patchar.

## v1.0.1

Releasedatum: 6 februari 2020

Vi har tagit med alla Magento Open Source 2.x-patchar från programvarunedladdningssidan i utgåvan magento/magento-cloud-patches v1.0.1. Om du har kopierat korrigeringar till ditt projekt tidigare bör du ta bort dem för att undvika konflikter.

Den här versionen innehåller följande korrigeringar och viktiga korrigeringar:

- **Åtgärda krondödläge och förbättra kronlåsning**—

   - Åtgärdar ett problem med att vissa kronijobb inte körs på grund av ett felaktigt statusvärde i `cron_schedule` tabell. Nu använder vi Adobe Commerce låsramverk för att kontrollera och uppdatera kundjobbstatus i stället för att använda `cron_schedule` tabell. Kronjobb som har avslutats med en felstatus provas igen under nästa kronkörning i stället för att vänta i 24 timmar.

   - Lägger till en _försök igen_ åtgärd för att undvika dödläge vid uppdateringar av data i `cron_schedule` tabell.

- **Uppdaterat `magento/magento-cloud-patches` för att inkludera alla tillgängliga patchar för Magento Open Source 2.x**—Paketet magento/magento-cloud-patches har uppdaterats så att det innehåller alla Magento Open Source 2.x-patchar som finns på nedladdningssidan. Om du tidigare har kopierat korrigeringsfiler från Magento Open Source till ditt Adobe Commerce i ett molninfrastrukturprojekt bör du ta bort dem för att undvika konflikter.<!--MAGECLOUD-4606-->

- **Korrigering för katalogsidnumrering i Elasticsearch** - Ersatte den Elasticsearch catalog pagination patch som levererades i magento/magento-cloud-patches v1.0 med en effektivare korrigering.<!--MAGECLOUD-4847-->

- **Page Builder-korrigeringar**- I Cloud Patches for Commerce 1.0.0 paketerade vi Page Builder-patchar för att åtgärda en känd Page Builder-sårbarhet (RCE) för fjärrexekvering av kod, med den initiala korrigeringen som baseras på Adobe Commerce 2.3.3. Vi har uppdaterat dessa patchar med en stabilare implementering som baseras på Adobe Commerce 2.3.4, som innehåller flera optimeringar för att åtgärda problemet.<!--MAGECLOUD-4884-->

  Om du har paketet magento/magento-cloud-patches 1.0.0 är du fortfarande skyddad från Page Builder RCE-säkerhetsluckor. Om du uppdaterar till 1.0.1 eller senare har du en bättre implementering av samma korrigering.

## v1.0.0

Releasedatum: 14 november 2019

Detta är den första versionen av [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) paket, som är ett nytt beroende för `ece-tools` paketversion 2002.0.22 eller senare.

Den här versionen innehåller följande korrigeringar och viktiga korrigeringar:

- **Page Builder säkerhetspatchar för version 2.3.1.x och 2.3.2.x**—Korrigerar ett fel i förhandsgranskningen i Page Builder som gör att oautentiserade användare kan komma åt vissa mallmetoder som kan användas för att aktivera godtycklig kodkörning över nätverket (RCE), vilket resulterar i globala informationsläckor. Problemet kan uppstå om du använder versioner av Page Builder som inte stöds i Adobe Commerce version 2.3.1 och 2.3.2.<!--MAGECLOUD-4649-->

- **MSI-korrigeringar**—Åtgärdar problem som orsakade indexeringsfel och prestandaproblem när standardlagerinställningar användes för att hantera lager.<!--MAGECLOUD-4428-->

- **Bakåtkompatibilitet för nya e-postgränssnitt**-Korrigerar ett bakåtkompatibilitetsproblem som orsakas av `Magento\Framework\Mail\EmailMessageInterface` PHP-gränssnittet introducerades i Adobe Commerce v2.3.3. Den nya `EmailMessageInterface` ärver från gamla `MessageInterface`och Adobe Commerce kärnmoduler återställs till beroende av `MessageInterface`.<!--MAGECLOUD-4422-->

- **Katalogsidindelning fungerar inte i Elasticsearch 6.x**—Åtgärdar ett kritiskt problem med sökresultatnumrering som påverkar kunder som använder Elasticsearch 6.x som katalogsökmotor.<!--MAGECLOUD-4448-->
