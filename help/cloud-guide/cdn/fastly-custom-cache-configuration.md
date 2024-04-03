---
title: Anpassa cachekonfigurationen
description: Lär dig hur du granskar och anpassar inställningarna för cachekonfigurationen när tjänsten Snabbt har installerats.
feature: Cloud, Configuration, Iaas, Cache
exl-id: f1fc85d4-7867-4bb5-9f11-bc8d2d80383b
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 0%

---

# Anpassa cachekonfigurationen

Granska och anpassa inställningarna för cachekonfigurationen när du har konfigurerat och testat tjänsten Snabbt i dina miljö för staging och produktion. Du kan till exempel uppdatera inställningarna för att göra det möjligt för TLS att omdirigera HTTP-begäranden till Fast, uppdatera rensningsinställningar och aktivera grundläggande autentisering för att lösenordsskydda webbplatsen under utvecklingen.

I följande avsnitt finns en översikt och instruktioner för hur du konfigurerar vissa cacheinställningar. Mer information om tillgängliga konfigurationsalternativ finns i [Snabb CDN-modul för Magento 2](https://github.com/fastly/fastly-magento2/tree/master/Documentation) dokumentation.

## Tvinga TLS

Med _Tvinga TLS_ för omdirigering av okrypterade begäranden (HTTP) till Snabbt. Efter att din förproduktionsmiljö eller produktionsmiljö har etablerats med en [giltigt SSL/TLS-certifikat](fastly-configuration.md#provision-ssltls-certificates)kan du uppdatera butikens snabbkonfiguration för att aktivera alternativet Tvinga TLS. Se den snabba [Tvinga TLS-guide](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/FORCE-TLS.md) i _Snabb CDN-modul för Magento 2_ dokumentation.

>[!NOTE]
>
>Att aktivera alternativet Force TLS rekommenderas för Adobe Commerce i molninfrastrukturbutiker.

## Utöka tidsgränsen snabbt

I snabbtjänstkonfigurationen anges en standardtidsgräns på 180 sekunder för HTTPS-begäranden till administratören. Alla förfrågningar som överskrider tidsgränsen returnerar ett 503-fel. Det innebär att du kan få 503 fel som svar på förfrågningar som kräver lång bearbetning eller när du försöker utföra gruppåtgärder.

Om du vill slutföra gruppåtgärder som tar längre tid än 3 minuter ändrar du _Tidsgräns för administratörssökväg_ value_ för att förhindra 503 fel.

>[!NOTE]
>
>Information om hur du utökar parametrar för snabb timeout för andra användare än Admin i gränssnittet Snabb finns i [Öka tidsgränser för långa jobb](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-INCREASE-TIMEOUTS-LONG-JOBS.md).

**Utöka tidsgränsen för administratören**:

{{admin-login-step}}

1. Klicka **Lager** > Inställningar > **Konfiguration** > **Avancerat** > **System** och expandera **Helsidescache**.

1. I _Snabb konfiguration_ sektion, expandera **Avancerad konfiguration**.

1. Ange **Tidsgräns för administratörssökväg** värde i sekunder. Värdet får inte vara längre än 10 minuter (600 sekunder).

1. Klicka **Spara konfiguration** överst på sidan.

1. När sidan har lästs in igen väljer du **Ladda upp VCL snabbt** i _Snabb konfiguration_ -avsnitt.

Hämtar snabbt Admin-sökvägen för att generera VCL-filen från `app/etc/env.php` konfigurationsfil.

## Konfigurera rensningsalternativ

Du kan snabbt välja mellan flera olika typer av rensningsalternativ på Magento-cacheminnets hanteringssida, bland annat alternativ för att rensa produktkategori, produktresurser och innehåll. När det här alternativet är aktiverat letar programmet efter händelser som automatiskt tömmer cacheminnen. Om du inaktiverar ett rensningsalternativ kan du rensa bort cacheminnen manuellt när du har slutfört uppdateringarna via sidan Cachehantering.

Rensningsalternativen är:

- **Rensa kategori**-Tar bort innehåll i produktkategorier (inte produktinnehåll) när du lägger till och uppdaterar en enskild produkt. Du kanske vill hålla den inaktiverad och aktivera rensning av produkten, vilket tömmer produkter och produktkategorier.
- **Rensa produkt**-Tömmer allt innehåll i produkt och produktkategori när du sparar en enskild ändring i en produkt. Det kan vara praktiskt att aktivera rensning av produkter för att omedelbart få uppdateringar till kunderna när de ändrar ett pris, lägger till ett produktalternativ och när produktlagret är slut.
- **Rensa CMS-sida**-Tar bort sidinnehåll när sidor uppdateras och läggs till i Adobe Commerce CMS. Du kanske till exempel vill rensa när du uppdaterar villkoren eller returprincipen. Om du sällan gör dessa ändringar kan du inaktivera automatisk rensning.
- **Mjuk tömning**-Ställer in ändrat innehåll till inaktuellt och tömt enligt inaktuell tidpunkt. Förutom tidsförskjutningen får kunderna inaktuellt innehåll medan de snabbt uppdaterar innehållet i bakgrunden.

![Konfigurera rensningsalternativ](../../assets/cdn/fastly-purge-options.png)

**Konfigurera alternativ för snabb tömning**:

1. I _Snabb konfiguration_ sektion, expandera **Avancerad konfiguration** för att visa alternativen för tömning.

1. För varje rensningsalternativ väljer du **Ja** för att möjliggöra automatisk tömning, eller **Nej** om du vill inaktivera automatisk rensning.

   När du inaktiverar ett rensningsalternativ måste du manuellt rensa cacheminnet för den kategorin från _Cachehantering_ sida.

1. Klicka **Spara konfiguration** överst på sidan.

1. När sidan har lästs in igen väljer du **Ladda upp VCL snabbt** i _Snabb konfiguration_ -avsnitt.

Mer information finns i [de snabba konfigurationsalternativen](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/CONFIGURATION.md#further-configuration-options).

## Konfigurera GeoIP-hantering

I modulen Snabbt finns GeoIP-hantering som automatiskt omdirigerar besökare eller en lista över butiker som matchar deras landskod. Om du redan använder ett tillägg för GeoIP-hantering kan du behöva verifiera funktionerna med alternativen Snabbt.

**Konfigurera GeoIp-hantering**:

{{admin-login-step}}

1. Klicka **Lager** > Inställningar > **Konfiguration** > **Avancerat** > **System** och expandera **Helsidescache**.

1. I _Snabb konfiguration_ sektion, expandera **Avancerad konfiguration**.

1. Bläddra nedåt och markera **Ja** till **Aktivera GeoIP**. Ytterligare konfigurationsalternativ visas.

1. Välj om besökaren ska omdirigeras automatiskt med för GeoIP-åtgärd **Omdirigering** eller tillhandahöll en lista med butiker att välja bland med **Dialog**.

1. För **Landsmappning**, markera **Lägg till** om du vill ange en landskod på två bokstäver som ska mappas med en viss Adobe Commerce-butik från en lista.

   ![Lägg till GeoIP-landskartor](/help/assets/cdn/fastly-geo-code.png)

1. Klicka **Spara konfiguration** överst på sidan.

1. När sidan har lästs in igen väljer du **Ladda upp VCL snabbt** i _Snabb konfiguration_ -avsnitt.

>[!NOTE]
>
>Den nuvarande implementeringen av Adobe Commerce Fast GeoIP-modulen stöder inte omdirigeringar mellan flera webbplatser.

Här finns också en serie [geolokaliseringsrelaterade VCL-funktioner](https://developer.fastly.com/reference/vcl/variables/geolocation/) för anpassad geopositioneringskodning.

## Aktivera moduler med fast kant

Moduler med fast kant är ett flexibelt ramverk som gör det möjligt att definiera gränssnittskomponenter och tillhörande VCL-kod via en mall. Dessa moduler gör det enkelt att anpassa och utöka konfigurationen för tjänsten Snabb via användargränssnittet i stället för att använda anpassade VCL-fragment.

Med Edge-moduler kan du aktivera specifika funktioner som CORS-huvuden, omskrivningar av Cloud Sitemap och konfigurera integrering mellan din Adobe Commerce-butik och andra CMS-system eller backend-system.

Om du vill visa, konfigurera och hantera tillgängliga moduler på menyn Edge-moduler aktiverar du _Aktivera moduler med fast kant_ alternativ. Se [Moduler med fast kant](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULES.md) i dokumentationen för modulen Snabbt CDN.

## Konfigurera bakändar och origin-skydd

Med backend-inställningarna kan du finjustera prestanda snabbt med skärmsläckning och timeout. A _back end_ är en specifik plats (IP eller domän) med konfigurerad origin-skydd och timeout-inställningar för att kontrollera och tillhandahålla cachelagrat innehåll.

_Origo-skyddsfunktioner_ skickar alla förfrågningar för din butik till en viss POP (Point of Presence). När en begäran tas emot söker POP efter cachelagrat innehåll och skickar det. Om den inte cachelagras fortsätter den till sköld-POP och sedan till origin-servern som cachelagrar innehållet. Sköldarna minskar trafiken direkt till origo.

Standardvärdet för Fast VCL-kod anger standardvärden för Origin-avskärmning och timeout för din Adobe Commerce på molninfrastruktursajter. I vissa fall kan du behöva ändra standardvärdena. Om du till exempel får TTFB-fel (Time to First Byte) kan du behöva justera _timeout för första byte_ värde.

>[!NOTE]
>
>Om sajten kräver funktioner som levereras via en serverdelsintegrering som [Wordpress](fastly-vcl-wordpress.md), anpassa konfigurationen av tjänsten Snabb för att lägga till serverdelen och hantera omdirigeringar från din Adobe Commerce-butik till Wordpress. Mer information finns i [Moduler med fast kant - annan integrering med CMS/backend](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-OTHER-CMS-INTEGRATION.md) i dokumentationen för modulen Snabbt.

**Granska konfigurationen av serverdelsinställningarna**:

{{admin-login-step}}

1. Klicka **Lager** > Inställningar > **Konfiguration** > **Avancerat** > **System** och expandera **Helsidescache**.

1. Expandera **Snabb konfiguration** -avsnitt.

1. Expandera **Inställningar för backend** och välj den växel som ska användas för att kontrollera standardbakänden. En modal öppnas som visar aktuella inställningar med alternativ för att ändra dem.

   ![Ändra bakänden](../../assets/cdn/fastly-backend.png)

1. Välj **Sköld** plats (eller datacenter).

   Med standardkonfigurationen Snabbt för ditt projekt anges den plats som ligger närmast din molntjänstregion. Om du behöver ändra den väljer du en plats som ligger nära standardplatsen.

1. Ändra timeoutvärdena (i mikrosekunder) för anslutningen till skölden, tiden mellan byte och tiden för den första byten. Vi rekommenderar att du behåller standardinställningarna för timeout.

1. Du kan också välja att **Aktivera serverdelen och skölden när du har redigerat eller sparat**.

1. Klicka **Överför** för att spara ändringarna och överföra dem till snabbservrarna.

1. Välj **Spara konfiguration**.

Mer information finns i [Stödlinje för backend-inställningar](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/Guides/BACKEND-SETTINGS.md) i dokumentationen för modulen Snabbt.

## Grundläggande autentisering

Grundläggande autentisering är en funktion som skyddar alla sidor och resurser på din webbplats med ett användarnamn och lösenord. Vi **rekommendera inte** aktivera grundläggande autentisering i produktionsmiljön. Du kan konfigurera den på mellanlagring för att skydda din plats under utvecklingsprocessen. Se [Grundläggande autentiseringshandbok](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BASIC-AUTH.md) i dokumentationen för modulen Snabbt CDN.

Om du lägger till användaråtkomst och aktiverar grundläggande autentisering på mellanlagring, kan du fortfarande komma åt administratören utan att ytterligare autentiseringsuppgifter krävs.

## Skapa anpassade VCL-fragment

Stöd för en anpassad version av VCL (Varnish Configuration Language) för att anpassa konfigurationen av tjänsten snabbt. Du kan till exempel tillåta, blockera eller omdirigera åtkomst för specifika användare eller IP-adresser med hjälp av VCL-kodblock med edge- och Access Control List-ordlistor (ACL).

Instruktioner om hur du skapar anpassade VCL-fragment, kantordlistor och ACL:er finns i [Anpassade VCL-fragment snabbt](fastly-vcl-custom-snippets.md).

>[!NOTE]
>
>Innan du lägger till anpassad VCL-kod, kantordlistor och åtkomstkontrollistor i din snabbmodulskonfiguration måste du kontrollera att cachelagringstjänsten Snabbt fungerar med standardkonfigurationen. Se [Konfigurera snabbt](fastly-configuration.md).

## Hantera domäner

Du kan använda [!UICONTROL Domains] för att lägga till och hantera Snabb domänkonfiguration för din butik.

- För startprojekt går du till Project URL under [!UICONTROL Domains] i [!DNL Cloud Console] för att lägga till din projekt-URL.

- För Pro-projekt skickar du en [Adobe Commerce Support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) för att lägga till domänen i din molnprojektskonfiguration. Supportteamet uppdaterar även kontokonfigurationen för Adobe Commerce Fast för att lägga till domänen.

**Hantera snabb domänkonfiguration från administratören**:

{{admin-login-step}}

1. Välj **Lager** > Inställningar > **Konfiguration** > **Avancerat** > **System** och expandera **Helsidescache**.

1. I Admin _Snabb konfiguration_ avsnitt, markera **Domäner**.

1. Klicka **Hantera domäner** för att öppna sidan Domäner.

1. Lägg till namnen på den översta nivån och underdomänerna för butikerna i molnmiljön.

   Du kan bara ange domäner som redan har lagts till i din konfiguration för molninfrastruktur.

   ![Lägg till snabb domänkonfiguration för Starter](../../assets/cdn/fastly-starter-activate-domain.png)

1. Klicka **Aktivera** för att uppdatera Snabdomänkonfigurationen.

>[!NOTE]
>
>Om samma domän har konfigurerats på ett annat snabbkonto måste du skicka en Adobe Commerce-supportanmälan för att begära domändelegering innan du kan lägga till domänen i Adobe Commerce. Se [Flera snabbkonton och tilldelade domäner](fastly.md#multiple-fastly-accounts-and-assigned-domains).

## Aktivera underhållsläge

Använd _Underhållsläge_ för att ge administrativ åtkomst till din webbplats från angivna IP-adresser samtidigt som en felsida returneras för alla andra förfrågningar.

**Aktivera underhållsläge med administrativ åtkomst**:

1. Öppna _Snabb konfiguration_ i Admin.

1. I _Kant-ACL_ -avsnittet, uppdatera `maint_allow` ACL (access control list) med de administrativa IP-adresser som kan komma åt din butik när den är i underhållsläge.

   ![Uppdatera IP-underhållsläge tillåtelselista](../../assets/cdn/fastly-maint-allowlist.png)

1. I _Underhållsläge_ avsnitt, markera **Aktivera underhållsläge**.

   När du har aktiverat underhållsläget blockeras all trafik utom förfrågningar från IP-adresserna i `maint_allowlist` ACL. Du kan uppdatera `maint_allowlist` om du vill ändra IP-adresserna i åtkomstkontrollistan.

   Detaljerade konfigurationsinstruktioner finns i [Handbok för underhållsläge](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/MAINTENANCE-MODE.md) i dokumentationen för modulen Fastly CDN för Magento 2.
