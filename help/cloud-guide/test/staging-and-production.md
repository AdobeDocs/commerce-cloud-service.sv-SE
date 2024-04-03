---
title: Testning av mellanlagring och produktion
description: Lär dig hur du testar i miljö för förproduktion och produktion.
exl-id: 5b762d59-04c5-4e89-a637-719141759158
source-git-commit: 1253d8357fd2554050d1775fefbc420a2097db5f
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 0%

---

# Testning av mellanlagring och produktion

När du har migrerat kod, filer och data till mellanlagring eller produktion kan du testa dina platser och butiker med hjälp av URL:er för miljön. Nedan finns information om hur du verifierar loggar, testar snabbkonfigurationer, testar för användaracceptans (UAT) och mycket mer.

## Loggfiler

Om du får problem med distributionen eller andra problem när du testar bör du kontrollera loggfilerna. Loggfilerna finns under `var/log` katalog.

Distributionsloggen finns i `/var/log/platform/<prodject-ID>/deploy.log`. Värdet för `<project-ID>` beror på projekt-ID och om miljön är Förproduktion eller Produktion. Med till exempel ett projekt-ID på `yw1unoukjcawe`, mellanlagringsanvändaren är `yw1unoukjcawe_stg` och produktionsanvändaren är `yw1unoukjcawe`.

När du loggar in i produktions- eller mellanlagringsmiljöer använder du SSH för att logga in på var och en av de tre noderna för att hitta loggarna. Eller så kan du använda [New Relic logghantering](../monitor/log-management.md) för att visa och fråga efter aggregerade loggdata från alla noder. Se [Visa loggar](log-locations.md#application-logs).

## Kontrollera kodbasen

Verifiera att din kodbas är korrekt distribuerad till förproduktionsmiljöer. Miljöerna bör ha identiska kodbaser.

## Verifiera konfigurationsinställningar

Kontrollera konfigurationsinställningarna via panelen Admin, bland annat bas-URL:en, grundläggande administratörs-URL:en och inställningarna för flera platser. Om du måste göra ytterligare ändringar slutför du redigeringarna i den lokala Git-grenen och går vidare till `master` gren i Integration, Staging och Production.

## Kontrollera cachelagring snabbt

[Konfigurera snabbt](../cdn/fastly-configuration.md) kräver stor noggrannhet: använd rätt autentiseringsuppgifter för snabb service-ID och snabb API-token, ladda upp den snabba VCL-koden, uppdatera DNS-konfigurationen och tillämpa SSL-/TLS-certifikaten i dina miljöer. När du har slutfört dessa konfigurationsuppgifter kan du verifiera snabb cachelagring i mellanlagrings- och produktionsmiljöer.

**Så här verifierar du snabbtjänstkonfigurationen**:

1. Logga in på Admin for Staging and Production med URL:en med `/admin`eller [uppdaterad administratörs-URL](../environment/variables-admin.md#admin-url).

1. Navigera till **Lager** > **Inställningar** > **Konfiguration** > **Avancerat** > **System**. Rulla och klicka **Helsidescache**.

1. Se till att **Cachelagra program** värdet är inställt på _Snabb CDN_ .

1. Testa inloggningsuppgifterna snabbt.

   - Klicka **Snabb konfiguration**.

   - Kontrollera att värdena för autentiseringsuppgifterna för snabbservice-ID och snabbprogrammeringstoken är korrekta. Se [Få inloggningsuppgifter snabbt](/help/cloud-guide/cdn/fastly-configuration.md#get-fastly-credentials).

   - Klicka **Testa autentiseringsuppgifter**.

   >[!WARNING]
   >
   >Se till att du har angett rätt Service ID och API-token i dina mellanlagrings- och produktionsmiljöer. Autentiseringsuppgifter skapas och mappas snabbt per tjänstmiljö. Om du anger autentiseringsuppgifter för mellanlagring i produktionsmiljön kan du inte överföra dina VCL-kodfragment, cachelagring fungerar inte korrekt och cachelagringskonfigurationen pekar på fel server och arkiv.

**Kontrollera cachelagring snabbt**:

1. Kontrollera om det finns rubriker med `dig` kommandoradsverktyg för att få information om platskonfigurationen.

   Du kan använda valfri URL med `dig` -kommando. I följande exempel används Pro-URL:er:

   - Mellanlagring: `dig https://mcstaging.<your-domain>.com`
   - Produktion: `dig https://mcprod.<your-domain>.com`

   För ytterligare `dig` tester, se Fastlys [Testar innan DNS ändras](https://docs.fastly.com/en/guides/working-with-domains).

1. Använd `cURL` för att verifiera svarsrubrikinformationen.

   ```bash
   curl https://mcstaging.<your-domain>.com -H "host: mcstaging.<your-domain.com>" -k -vo /dev/null -H Fastly-Debug:1
   ```

   Se [Kontrollera svarsrubriker](../cdn/fastly-troubleshooting.md#check-cache-hit-and-miss-response-headers) om du vill ha information om hur du verifierar rubrikerna.

1. När du är klar använder du `cURL` för att kontrollera din publicerade webbplats.

   ```bash
   curl https://<your-domain> -k -vo /dev/null -H Fastly-Debug:1
   ```

## Fullständig UAT-testning

Slutför UAT (User Acceptance Testing) på mellanlagring och produktion. Följande tester är en snabb lista över möjliga uppgifter och områden att testa som marknadsförare och kund. Listan kan vara längre och innehålla ytterligare tester för anpassade moduler, tillägg och tredjepartsintegreringar. Använd stationära datorer, bärbara datorer och mobila enheter när du testar.

Om du råkar ut för problem kan du spara dina reproduktionssteg, felmeddelanden, konstiga skärmdumpar och länkar. Använd den här informationen för att undersöka och åtgärda problem i integreringsmiljöns kod och konfigurationer eller i miljöinställningarna.

<table>
<tr>
<td style="width:150px">Användarhantering</td>
<td>
<ul>
<li>Skapa och redigera kundkonton, verifiera e-post</li>
<li>Skapa administratörsroller för handlare</li>
<li>Skapa handelskonton med specifika roller</li>
<li>Testa åtkomst till handelskonton per roll</li>
</ul>
</td>
</tr>
<tr>
<td>Kataloger och produkter</td>
<td>
<ul>
<li>Skapa en katalog med associerade produkter</li>
<li>Skapa produkter för butiken, inklusive alla produkttyper: enkla, konfigurerbara, paketerade</li>
<li>Lägg till produktbilder, färgrutor, videor och andra mediealternativ</li>
<li>Konfigurera pris, rabatter, prisregler </li>
<li>Konfigurera avancerade funktioner som prisintervall, aktuella produkter, tillgänglighetsdatum</li>
<li>Ändra lager och verifiera korrekta värden för visning och ändring per ökning och slutfört köp</li>
</ul>
</td>
</tr>
<tr>
<td>Korgar och kassor</td>
<td>
<ul>
<li>Sök efter produkter och välj filtreringsalternativ</li>
<li>Lägg till produkter i kundvagnen från sökresultat, kategorisidor, produktsidor</li>
<li>Testa alla produkttyper</li>
<li>Visa kundvagnen och ändra innehållet genom att ta bort eller ändra belopp </li>
<li>Gå igenom kassan för att verifiera orderbeloppen mot kundvagnen och produktinformationen</li>
<li>Kontrollera att momsen är korrekt beräknad för vagnen</li>
<li>Slutför ett köp med olika alternativ: lägg till en kupong, välj frakt, ange frakt- och faktureringsinformation samt betalningsinformation</li>
<li>Verifiera betalningsgatewayar och alternativ under utcheckning</li>
<li>Kontrollera om det finns meddelanden på skärmen, beställningar i kundkontot och e-postmeddelanden</li>
<li>Testa gäst- och kundutcheckning</li>
</ul>
</td>
</tr>
<tr>
<td>Orderhantering</td>
<td>
<ul>
<li>Skapa en order för en kund</li>
<li>Söka efter och visa order</li>
<li>Ändra en order genom att lägga till och ta bort produkter, ändra belopp, ändra frakt- och faktureringsinformation</li>
<li>Hantera en återbetalning</li>
<li>Avbryt en beställning</li>
<li>Använda kupongkoder och rabatter</li>
</ul>
</td>
</tr>
<tr>
<td>Webbplatsinnehåll</td>
<td>
<ul>
<li>Kontrollera att alla teman och resurser läses in korrekt</li>
<li>Kontrollera att CSS visas korrekt, inklusive responsiva mediestorlekar</li>
<li>Kontrollera villkor, återbetalningsvillkor och annan policyinformation</li>
<li>Kontrollera kontaktinformation, länkar och annat om ditt företag</li>
<li>Sök efter produkter och innehåll, kontrollera filtrering av resultat</li>
<li>Verifiera sidfotsblock och övre navigeringsblock</li>
<li>Testa sidorna 404 och Maintenance</li>
</ul>
</td>
</tr>
<tr>
<td>Tillägg</td>
<td>
<ul>
<li>Verifiera alla tilläggsinställningar, särskilt för alla skatte-, leverans- och betalningsmoduler (exempel: order som skickas till lagerställe och system för ekonomisk förvaltning)</li>
<li>Testa alla anpassade interaktioner för moduler och installerade tillägg</li>
<li>Kontrollera data för interaktioner som ska slutföras (betalningar, order, e-postmeddelanden)</li>
<li>Kontrollera konfigurationer per miljö för dina tillägg</li>
<li>Verifiera beroenden mellan moduler och tillägg</li>
<li>Kontrollera alla åtgärder som handlare och kund</li>
</ul>
</td>
</tr>
<tr>
<td>Tredjepartsintegreringar</td>
<td>
<ul>
<li>Verifiera att data sparas korrekt i Adobe Commerce och exporterar, push-meddelanden eller är tillgängliga för tredjepartstjänsten (exempel: beställningar visas i orderhanteringssystem från tredje part)</li>
<li>Verifiera alla konfigurationer och interaktioner per integrering</li>
<li>Utför rundtustester som kommer från Adobe Commerce och din tredjepartstjänst</li>
<li>Verifiera att autentiseringen har slutförts</li>
<li>Kontrollera om det finns loggade problem med att uppdatera kodintegreringar eller felmeddelanden på kontrollpaneler</li>
</ul>
</td>
</tr>
<tr>
<td>Backend-testning</td>
<td>
<ul>
<li>Testa och rensa cache </li>
<li>Utför omindexering och verifiera resultat</li>
<li>Kontrollera cron-jobb, kontrollera om det finns cron_schedule-fel</li>
<li>Verifiera och sök efter eventuella gränssnittsskriptproblem</li>
<li>Kontrollera om det finns loggade problem: programloggar, PHP-loggar, MySQL-loggar, e-postloggar</li>
</ul>
</td>
</tr>
</table>

## Belastnings- och stresstestning

Innan du startar är det bäst att utföra omfattande trafik- och prestandatestning i dina miljö för staging och produktion. Överväg att testa prestanda för era frontend- och backend-processer.

Innan du börjar testa anger du en biljett med supportinformation om de miljöer du testar, vilka verktyg du använder och tidsramen. Uppdatera biljetten med resultat och information för att spåra prestanda. När du är klar med testningen lägger du till de uppdaterade resultaten och antecknar i biljetttestningen som slutförd med datum- och tidsstämpel.

Granska [Performance Toolkit](https://github.com/magento/magento2/tree/2.4/setup/performance-toolkit) som en del av beredskapen inför lanseringen.

Använd följande verktyg för bästa resultat:

- [Testning av programprestanda](../environment/variables-post-deploy.md#ttfb_tested_pages)—Testa programmets prestanda genom att konfigurera `TTFB_TESTED_PAGES` systemvariabel för att testa responstiden på plats.
- [Siege](https://www.joedog.org/siege-home/)- Trafikformnings- och testprogram för att nå ut till butiken. Besök webbplatsen med ett konfigurerbart antal simulerade klienter. Siege har stöd för grundläggande autentisering, cookies, HTTP, HTTPS och FTP-protokoll.
- [Jmeter](https://jmeter.apache.org)- Utmärkt laddningstestning som hjälper till att mäta prestanda för spikad trafik, t.ex. för blixtförsäljning. Skapa anpassade tester som körs mot din plats.
- [New Relic](../monitor/new-relic-service.md) (tillhandahålls) - Hjälper dig att hitta processer och områden på webbplatsen som ger långsam prestanda med spårad tid per åtgärd, som överföring av data, frågor, Redis med mera.
- [WebPageTest](https://www.webpagetest.org) och [Prike](https://www.pingdom.com)—Realtidsanalys av webbplatsens sidor läses in med olika ursprungsplatser. Riket kan kräva en avgift. WebPageTest är ett kostnadsfritt verktyg.

## Funktionstestning

Du kan använda Magento Functional Testing Framework (MFTF) för att slutföra funktionstestningen för Adobe Commerce från Cloud Docker-miljön. Se [Programtestning](https://developer.adobe.com/commerce/cloud-tools/docker/test/application-testing/) i _Handbok för Cloud Docker for Commerce_.

## Konfigurera verktyget för säkerhetsgenomsökning

Det finns ett kostnadsfritt säkerhetssökningsverktyg för dina webbplatser. Information om hur du lägger till platser och kör verktyget finns i [Verktyg för säkerhetsgenomsökning](../launch/overview.md#set-up-the-security-scan-tool).
