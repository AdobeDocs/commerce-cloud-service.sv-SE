---
title: Felmeddelanden för ECE-verktygspaket
description: Se en lista med felkoder och meddelanden som kan visas under Adobe Commerce när det gäller processer för att bygga, distribuera och efterdistribuera molninfrastrukturer.
recommendations: noDisplay
role: Developer
exl-id: d8cc8d49-32da-43cf-a105-aa56b5334000
source-git-commit: 9dda6fe7f6a9d6064436820a3c8426ec982b5230
workflow-type: tm+mt
source-wordcount: '2763'
ht-degree: 4%

---

# Felmeddelanden för ECE-verktyg

Referensen till det här felmeddelandet innehåller information om felsökning som kan inträffa under byggandet, distributionen och efterdistributionen av Adobe Commerce-infrastrukturen.

Alla viktiga felmeddelanden och varningsmeddelanden som inträffar under distributionen skrivs till båda `var/log/cloud.log` och `/var/log/cloud.error.log` filer. Loggfilen för molnfel innehåller endast fel från den senaste distributionen. En tom fil visar att distributionen lyckades utan fel.

I `cloud.error.log` -fil, formateras varje post som en JSON-sträng för enklare tolkning:

```json
{"errorCode":1006,"stage":"build","step":"validate-config","suggestion":"No stores/website/locales found in config.php\n  To speed up the deploy process do the following:\n  1. Using SSH, log in to your Magento Cloud account\n  2. Run \"php ./vendor/bin/ece-tools config:dump\"\n  3. Using SCP, copy the app/etc/config.php file to your local repository\n  4. Add, commit, and push your changes to the app/etc/config.php file","title":"The configured state is not ideal","type":"warning"}
```

Felmeddelanden kategoriseras efter en av distributionsfaserna: skapa, distribuera och efterdistribuera. Varje avsnitt innehåller en lista med associerade fel med följande information för varje fel:

- **Felkod**: Den Adobe Commerce-tilldelade identifieraren för felmeddelandet
- **Scen**: Anger om felet uppstod under bygget, distributionen eller efter distributionen
- **Steg**: Anger det steg i distributionsscenariot som kan returnera felet. Om _Steg_ -kolumnen är tom. Felet är ett allmänt fel som kan returneras i flera steg eller under förbearbetningsåtgärder. Se [Scenariobaserad driftsättning](../deploy/scenario-based.md) om du vill ha mer information om stegen för att skapa, distribuera och efterdistribuera.
- **Förslag**: Tillhandahåller vägledning för felsökning och lösning av felet
- **Titel (felbeskrivning)**: En beskrivning som sammanfattar orsaken till felet
- **Typ**: Anger om felet är ett kritiskt fel eller en varning

<!-- Note: The error code tables in this file are auto-generated from source code. To request changes to error code descriptions or suggestions, submit a GitHub issue to the magento/ece-tools repository. -->

## Allvarliga fel

Kritiska fel indikerar ett problem med Commerce i molninfrastrukturens projektkonfiguration som orsakar ett distributionsfel, till exempel felaktig, stöds inte eller så saknas en konfiguration för nödvändiga inställningar. Innan du kan distribuera måste du uppdatera konfigurationen för att åtgärda felen.

### Byggfas

| Felkod | Bygg steg | Felbeskrivning (rubrik) | Föreslagen åtgärd |
| - | - | - | - |
| 2 |  | Kan inte skriva till `./app/etc/env.php` fil | Distributionsskriptet kan inte göra nödvändiga ändringar i `/app/etc/env.php` -fil. Kontrollera din behörighet i filsystemet. |
| 3 |  | Konfigurationen har inte definierats i `schema.yaml` fil | Konfigurationen har inte definierats i `./vendor/magento/ece-tools/config/schema.yaml` -fil. Kontrollera att namnet på config-variabeln är korrekt och definierat. |
| 4 |  | Det gick inte att analysera `.magento.env.yaml` fil | The `./.magento.env.yaml` filformatet är ogiltigt. Använd en YAML-tolk för att kontrollera syntaxen och åtgärda eventuella fel. |
| 5 |  | Kan inte läsa `.magento.env.yaml` fil | Kan inte läsa `./.magento.env.yaml` -fil. Kontrollera filbehörigheter. |
| 6 |  | Kan inte läsa `.schema.yaml` fil | Kan inte läsa `./vendor/magento/ece-tools/config/magento.env.yaml` -fil. Kontrollera filbehörigheter och omdistribuera (`magento-cloud environment:redeploy`). |
| 7 | refresh-modules | Kan inte skriva till `./app/etc/config.php` fil | Distributionsskriptet kan inte göra nödvändiga ändringar i `/app/etc/config.php` -fil. Kontrollera din behörighet i filsystemet. |
| 8 | validate-config | Kan inte läsa `composer.json` fil | Kan inte läsa `./composer.json` -fil. Kontrollera filbehörigheter. |
| 9 | validate-config | The `composer.json` filen saknar obligatoriskt avsnitt för automatisk inläsning | Obligatoriskt `autoload` -avsnittet saknas i `composer.json` -fil. Jämför avsnittet för automatisk inläsning med `composer.json` i molnmallen och lägg till den saknade konfigurationen. |
| 10 | validate-config | The `.magento.env.yaml` filen innehåller ett alternativ som inte har deklarerats i schemat, eller ett alternativ som har konfigurerats med ett ogiltigt värde eller en ogiltig scen | The `./.magento.env.yaml` filen innehåller ogiltig konfiguration. Mer information finns i felloggen. |
| 11 | refresh-modules | Kommandot misslyckades: `/bin/magento module:enable --all` | Försök att köra `composer update` lokalt. Bekräfta och tryck sedan på den uppdaterade `composer.lock` -fil. Kontrollera även `cloud.log` för mer information. Om du vill ha mer detaljerade kommandoutdata lägger du till `VERBOSE_COMMANDS: '-vvv'` till `.magento.env.yaml` -fil. |
| 12 | apply-patches | Det gick inte att tillämpa korrigeringen |  |
| 13 | set-report-dir-nesting-level | Det går inte att skriva till filen `/pub/errors/local.xml` |  |
| 14 | copy-sample-data | Det gick inte att kopiera exempeldatafiler |  |
| 15 | compile-di | Kommandot misslyckades: `/bin/magento setup:di:compile` | Kontrollera `cloud.log` för mer information. Lägg till `VERBOSE_COMMANDS: '-vvv'` till `.magento.env.yaml` för mer detaljerad kommandoutskrift. |
| 16 | dump-autoload | Kommandot misslyckades: `composer dump-autoload` | The `composer dump-autoload` kommandot misslyckades. Kontrollera `cloud.log` för mer information. |
| 17 | run-baler | Kommandot som ska köras `Baler` för Javascript-paketering misslyckades | Kontrollera `SCD_USE_BALER` systemvariabel för att verifiera att Baler-modulen är konfigurerad och aktiverad för JS-paketering. Om du inte behöver Baler-modulen anger du `SCD_USE_BALER: false`. |
| 18 | compress-static-content | Nödvändigt verktyg hittades inte (timeout, bash) |  |
| 19 | deploy-static-content | Kommando `/bin/magento setup:static-content:deploy` misslyckades | Kontrollera `cloud.log` för mer information. Om du vill ha mer detaljerade kommandoutdata lägger du till `VERBOSE_COMMANDS: '-vvv'` till `.magento.env.yaml` -fil. |
| 20 | compress-static-content | Komprimeringen av statiskt innehåll misslyckades | Kontrollera `cloud.log` för mer information. |
| 21 | säkerhetskopieringsdata: statiskt innehåll | Det gick inte att kopiera statiskt innehåll till `init` katalog | Kontrollera `cloud.log` för mer information. |
| 22 | säkerhetskopieringsdata: skrivbara kataloger | Det gick inte att kopiera vissa skrivbara kataloger till `init` katalog | Det gick inte att kopiera skrivbara kataloger till `./init` mapp. Kontrollera din behörighet i filsystemet. |
| 23 |  | Det går inte att skapa ett logger-objekt |  |
| 24 | säkerhetskopieringsdata: statiskt innehåll | Det gick inte att rensa `./init/pub/static/` katalog | Det gick inte att rensa `./init/pub/static` mapp. Kontrollera din behörighet i filsystemet. |
| 25 |  | Det går inte att hitta Composer-paketet | Om du installerade Adobe Commerce-programversionen direkt från GitHub-databasen kontrollerar du att `DEPLOYED_MAGENTO_VERSION_FROM_GIT` systemvariabel är konfigurerad. |
| 26 | validate-config | Ta bort modulkonfigurationen Magento Braintree som inte längre stöds i Adobe Commerce och Magento Open Source 2.4 och senare versioner. | Stöd för modulen Braintree ingår inte längre i Magento 2.4.0 och senare. Ta bort variabeln CONFIG_STORES_DEFAULT_PAYMENT_BRAINTREE__CHANNEL från variabeln variabeln variabler i `.magento.app.yaml` -fil. Använd en officiell förlängning från Commerce Marketplace i stället för betalningsstöd från Braintree. |

### Distribuera fas

| Felkod | Distribuera steg | Felbeskrivning (rubrik) | Föreslagen åtgärd |
| - | - | - | - |
| 101 | fördistribution: cache | Felaktig cachekonfiguration (port eller värd saknas) | Cachekonfigurationen saknar obligatoriska parametrar `server` eller `port`. Kontrollera `cloud.log` för mer information. |
| 102 |  | Kan inte skriva till `./app/etc/env.php` fil | Distributionsskriptet kan inte göra nödvändiga ändringar i `/app/etc/env.php` -fil. Kontrollera din behörighet i filsystemet. |
| 103 |  | Konfigurationen har inte definierats i `schema.yaml` fil | Konfigurationen har inte definierats i `./vendor/magento/ece-tools/config/schema.yaml` -fil. Kontrollera att namnet på config-variabeln är korrekt och att det är definierat. |
| 104 |  | Det gick inte att analysera `.magento.env.yaml` fil | Konfigurationen har inte definierats i `./vendor/magento/ece-tools/config/schema.yaml` -fil. Kontrollera att namnet på config-variabeln är korrekt och att det är definierat. |
| 105 |  | Kan inte läsa `.magento.env.yaml` fil | Kan inte läsa `./.magento.env.yaml` -fil. Kontrollera filbehörigheter. |
| 106 |  | Kan inte läsa `.schema.yaml` fil |  |
| 107 | fördistribution: rensning-redis-cache | Det gick inte att rensa Redis-cachen | Det gick inte att rensa Redis-cachen. Kontrollera att Redis cachekonfigurationen är korrekt och att Redis-tjänsten är tillgänglig. Se [Installera Redis-tjänsten](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/redis.html). |
| 108 | fördriftsätta: set-production-mode | Kommando `/bin/magento maintenance:enable` misslyckades | Kontrollera `cloud.log` för mer information. Om du vill ha mer detaljerade kommandoutdata lägger du till `VERBOSE_COMMANDS: '-vvv'` till `.magento.env.yaml` -fil. |
| 109 | validate-config | Felaktig databaskonfiguration | Kontrollera att `DATABASE_CONFIGURATION` systemvariabeln är korrekt konfigurerad. |
| 110 | validate-config | Felaktig sessionskonfiguration | Kontrollera att `SESSION_CONFIGURATION` systemvariabeln är korrekt konfigurerad. Konfigurationen måste innehålla minst `save` parameter. |
| 111 | validate-config | Felaktig sökkonfiguration | Kontrollera att `SEARCH_CONFIGURATION` systemvariabeln är korrekt konfigurerad. Konfigurationen måste innehålla minst `engine` parameter. |
| 112 | validate-config | Felaktig resurskonfiguration | Kontrollera att `RESOURCE_CONFIGURATION` systemvariabeln är korrekt konfigurerad. Konfigurationen måste innehålla minst `connection` parameter. |
| 113 | validate-config:elasticsuite-integrity | ElasticSuite är installerat, men tjänsten Elasticsearch är inte tillgänglig | Kontrollera att `SEARCH_CONFIGURATION` Miljövariabeln är korrekt konfigurerad och verifierar att tjänsten Elasticsearch är tillgänglig. |
| 114 | validate-config:elasticsuite-integrity | ElasticSuite är installerat, men en annan sökmotor används | ElasticSuite har installerats, men en annan sökmotor har konfigurerats. Uppdatera `SEARCH_CONFIGURATION` miljövariabel för att aktivera Elasticsearch och verifiera tjänstkonfigurationen i Elasticsearch i `services.yaml` -fil. |
| 115 |  | Databasfrågekörningen misslyckades |  |
| 116 | install-update: installation | Kommando `/bin/magento setup:install` misslyckades | Kontrollera `cloud.log` och `install_upgrade.log` för mer information. Om du vill ha mer detaljerade kommandoutdata lägger du till `VERBOSE_COMMANDS: '-vvv'` till `.magento.env.yaml` -fil. |
| 117 | install-update: config-import | Kommando `app:config:import` misslyckades | Kontrollera `cloud.log` för mer information. Om du vill ha mer detaljerade kommandoutdata lägger du till `VERBOSE_COMMANDS: '-vvv'` till `.magento.env.yaml` -fil. |
| 118 |  | Nödvändigt verktyg hittades inte (timeout, bash) |  |
| 119 | install-update: deploy-static-content | Kommando `/bin/magento setup:static-content:deploy` misslyckades | Kontrollera `cloud.log` för mer information. Om du vill ha mer detaljerade kommandoutdata lägger du till `VERBOSE_COMMANDS: '-vvv'` till `.magento.env.yaml` -fil. |
| 120 | compress-static-content | Komprimeringen av statiskt innehåll misslyckades | Kontrollera `cloud.log` för mer information. |
| 121 | deploy-static-content:generate | Kan inte uppdatera den distribuerade versionen | Kan inte uppdatera `./pub/static/deployed_version.txt` -fil. Kontrollera din behörighet i filsystemet. |
| 122 | rent statiskt innehåll | Det gick inte att rensa statiska innehållsfiler |  |
| 123 | install-update: split-db | Kommando `/bin/magento setup:db-schema:split` misslyckades | Kontrollera `cloud.log` för mer information. Om du vill ha mer detaljerade kommandoutdata lägger du till `VERBOSE_COMMANDS: '-vvv'` till `.magento.env.yaml` -fil. |
| 124 | rensa-vy-förbearbetad | Det gick inte att rensa `var/view_preprocessed` mapp | Det går inte att rensa `./var/view_preprocessed` mapp. Kontrollera din behörighet i filsystemet. |
| 125 | install-update: reset-password | Kunde inte uppdatera `/var/credentials_email.txt` fil | Kunde inte uppdatera `/var/credentials_email.txt` -fil. Kontrollera din behörighet i filsystemet. |
| 126 | install-update: update | Kommando `/bin/magento setup:upgrade` misslyckades | Kontrollera `cloud.log` och `install_upgrade.log` för mer information. Om du vill ha mer detaljerade kommandoutdata lägger du till `VERBOSE_COMMANDS: '-vvv'` till `.magento.env.yaml` -fil. |
| 127 | rensningscache | Kommando `/bin/magento cache:flush` misslyckades | Kontrollera `cloud.log` för mer information. Om du vill ha mer detaljerade kommandoutdata lägger du till `VERBOSE_COMMANDS: '-vvv'` till `.magento.env.yaml` -fil. |
| 128 | disable-maintain-mode | Kommando `/bin/magento maintenance:disable` misslyckades | Kontrollera `cloud.log` för mer information. Lägg till `VERBOSE_COMMANDS: '-vvv'` till `.magento.env.yaml` för mer detaljerad kommandoutskrift. |
| 129 | install-update: reset-password | Det går inte att läsa mallen för lösenordsåterställning |  |
| 130 | install-update: cache_type | Kommandot misslyckades: `php ./bin/magento cache:enable` | Kommando `php ./bin/magento cache:enable` körs endast när Adobe Commerce installeras men `./app/etc/env.php` filen saknades eller var tom i början av distributionen. Kontrollera `cloud.log` för mer information. Lägg till `VERBOSE_COMMANDS: '-vvv'` till `.magento.env.yaml` för mer detaljerad kommandoutskrift. |
| 131 | install-update | The `crypt/key`  nyckelvärdet finns inte i `./app/etc/env.php` eller `CRYPT_KEY` cloud environment variable | Det här felet inträffar om `./app/etc/env.php` filen inte finns när Adobe Commerce-distributionen börjar, eller om `crypt/key` värdet är odefinierat. Om du migrerade databasen från en annan miljö hämtar du krypteringsnyckelvärdet från den miljön. Lägg sedan till värdet i [CRYPT_KEY](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html#crypt_key) molnmiljövariabel i din nuvarande miljö. Se [Adobe Commerce krypteringsnyckel](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/overview.html#gather-credentials). Om du av misstag har tagit bort `./app/etc/env.php` använder du följande kommando för att återställa den från säkerhetskopiefiler som har skapats från en tidigare distribution: `./vendor/bin/ece-tools backup:restore` CLI-kommando.&quot; |
| 132 |  | Det går inte att ansluta till tjänsten Elasticsearch | Kontrollera om Elasticsearch har giltiga inloggningsuppgifter och verifiera att tjänsten körs |
| 137 |  | Det går inte att ansluta till OpenSearch-tjänsten | Kontrollera om det finns giltiga OpenSearch-autentiseringsuppgifter och verifiera att tjänsten körs |
| 133 | validate-config | Ta bort modulkonfigurationen Magento Braintree som inte längre stöds i Adobe Commerce eller Magento Open Source 2.4 och senare versioner. | Stöd för modulen Braintree ingår inte längre i Adobe Commerce eller Magento Open Source 2.4.0 och senare. Ta bort variabeln CONFIG_STORES_DEFAULT_PAYMENT_BRAINTREE__CHANNEL från variabeln variabeln variabler i `.magento.app.yaml` -fil. För stöd från Braintree ska du i stället använda en officiell Braintree-betalningsförlängning från Commerce Marketplace. |
| 134 | validate-config | Adobe Commerce och Magento Open Source 2.4.0 kräver att tjänsten Elasticsearch installeras | Installera tjänsten Elasticsearch |
| 138 | validate-config | Adobe Commerce och Magento Open Source 2.4.4 kräver att tjänsten OpenSearch eller Elasticsearch är installerad | Installera OpenSearch-tjänsten |
| 135 | validate-config | Sökmotorn måste anges till Elasticsearch för Adobe Commerce och Magento Open Source >= 2.4.0 | Kontrollera variabeln SEARCH_CONFIGURATION för `engine` alternativ. Om den är konfigurerad tar du bort alternativet eller anger värdet som elasticsearch. |
| 136 | validate-config | Delad databas har tagits bort från Adobe Commerce och Magento Open Source 2.5.0. | Om du använder en delad databas måste du återgå till eller migrera till en enda databas eller använda ett annat tillvägagångssätt. |
| 139 | validate-config | Felaktig sökmotor | Denna version av Adobe Commerce eller Magento Open Source stöder inte OpenSearch. Du måste använda version 2.3.7-p3, 2.4.3-p2 eller senare |

### Steg efter driftsättning

| Felkod | Steg efter distribution | Felbeskrivning (rubrik) | Föreslagen åtgärd |
| - | - | - | - |
| 201 | is-deploy-failed | Distributionsfasen misslyckades |  |
| 202 |  | The `./app/etc/env.php` filen är inte skrivbar | Distributionsskriptet kan inte göra nödvändiga ändringar i `/app/etc/env.php` -fil. Kontrollera din behörighet i filsystemet. |
| 203 |  | Konfigurationen har inte definierats i `schema.yaml` fil | Konfigurationen har inte definierats i `./vendor/magento/ece-tools/config/schema.yaml` -fil. Kontrollera att namnet på config-variabeln är korrekt och att det är definierat. |
| 204 |  | Det gick inte att analysera `.magento.env.yaml` fil | The `./.magento.env.yaml` filformatet är ogiltigt. Använd en YAML-tolk för att kontrollera syntaxen och åtgärda eventuella fel. |
| 205 |  | Kan inte läsa `.magento.env.yaml` fil | Kontrollera filbehörigheter. |
| 206 |  | Kan inte läsa `.schema.yaml` fil |  |
| 207 | uppvärmning | Det gick inte att förhandsladda vissa uppvärmningssidor |  |
| 208 | time-to-first-byte | Det gick inte att testa tiden till den första byten (TTFB) |  |
| 227 | rensningscache | Kommando `/bin/magento cache:flush` misslyckades | Kontrollera `cloud.log` för mer information. Lägg till `VERBOSE_COMMANDS: '-vvv'` till `.magento.env.yaml` för mer detaljerad kommandoutskrift. |

### Allmänt

| Felkod | Allmänt steg | Felbeskrivning (rubrik) | Föreslagen åtgärd |
| - | - | - | - |
| 243 |  | Konfigurationen har inte definierats i `schema.yaml` fil | Kontrollera att namnet på config-variabeln är korrekt och att det är definierat. |
| 244 |  | Det gick inte att analysera `.magento.env.yaml` fil | The `./.magento.env.yaml` filformatet är ogiltigt. Använd en YAML-tolk för att kontrollera syntaxen och åtgärda eventuella fel. |
| 245 |  | Kan inte läsa `.magento.env.yaml` fil | Kan inte läsa `./.magento.env.yaml` -fil. Kontrollera filbehörigheter. |
| 246 |  | Kan inte läsa `.schema.yaml` fil |  |
| 247 |  | Det går inte att generera en modul för inaktivering | Kontrollera `cloud.log` för mer information. |
| 248 |  | Det går inte att aktivera en modul för inaktivering | Kontrollera `cloud.log` för mer information. |
| 249 |  | Det gick inte att generera modulen AdobeCommerceWebhookPlugins | Kontrollera `cloud.log` för mer information. |
| 250 |  | Det gick inte att aktivera modulen AdobeCommerceWebhookPlugins | Kontrollera `cloud.log` för mer information. |

## Varningsfel

Varningsfel indikerar ett problem med konfigurationen av Commerce för molninfrastrukturprojekt, till exempel felaktig, borttagen, stöds inte eller saknade konfigurationsinställningar för valfria funktioner som kan påverka webbplatsens funktion. Även om en varning inte orsakar ett distributionsfel bör du granska varningsmeddelanden och uppdatera konfigurationen för att åtgärda dem.

### Byggfas

| Felkod | Bygg steg | Felbeskrivning (rubrik) | Föreslagen åtgärd |
| - | - | - | - |
| 1001 | validate-config | Filen app/etc/config.php finns inte |  |
| 1002 | validate-config | The ./build_options.ini stöds inte längre |  |
| 1003 | validate-config | Modulavsnittet saknas i den delade konfigurationsfilen |  |
| 1004 | validate-config | Konfigurationen är inte kompatibel med den här versionen av Magento |  |
| 1005 | validate-config | SCD-alternativ ignorerade |  |
| 1006 | validate-config | Det konfigurerade tillståndet är inte idealiskt |  |
| 1007 | run-baler | Baler JS-paketering kan inte användas |  |

### Distribuera fas

| Felkod | Distribuera steg | Felbeskrivning (rubrik) | Föreslagen åtgärd |
| - | - | - | - |
| 2001 | fördistribution:cache | Cachen är konfigurerad för en Redis-tjänst som inte är tillgänglig. Konfigurationen ignoreras. |  |
| 2002 | validate-config | Det konfigurerade tillståndet är inte idealiskt |  |
| 2003 | validate-config | Värdet för katalogkapslingsnivån för felrapportering har inte konfigurerats |  |
| 2004 | validate-config | Ogiltig konfiguration i ./pub/errors/local.xml fil. |  |
| 2005 | validate-config | Administratörsdata används endast för att skapa en administratörsanvändare under den första installationen. Alla ändringar av administratörsdata ignoreras under uppgraderingsprocessen. | Efter den första installationen kan du ta bort admindata från konfigurationen. |
| 2006 | validate-config | Administratörsanvändaren skapades inte eftersom administratörens e-postadress inte har angetts | Efter installationen kan du skapa en administratörsanvändare manuellt: Använd ssh för att ansluta till din miljö. Kör sedan `bin/magento admin:user:create` -kommando. |
| 2007 | validate-config | Uppdatera PHP-version till rekommenderad version |  |
| 2008 | validate-config | Solr-stödet har ersatts i Adobe Commerce och Magento Open Source 2.1. |  |
| 2009 | validate-config | Solr stöds inte längre av Adobe Commerce och Magento Open Source 2.2 eller senare. |  |
| 2010 | validate-config | Tjänsten Elasticsearch installeras på infrastrukturnivå, men används inte som sökmotor. | Överväg att ta bort tjänsten Elasticsearch från infrastrukturskiktet för att optimera resursanvändningen. |
| 2011 | validate-config | Elasticsearch-tjänstversionen i infrastrukturskiktet är inte kompatibel med den aktuella versionen av modulen elasticsearch/elasticsearch som används av ditt Adobe Commerce-program. |  |
| 2012 | validate-config | Den aktuella konfigurationen är inte kompatibel med den här versionen av Adobe Commerce |  |
| 2013 | validate-config | SCD-alternativ ignorerades eftersom distributionsprocessen inte kördes i byggfasen |  |
| 2014 | validate-config | Konfigurationen innehåller inaktuella variabler eller värden |  |
| 2015 | validate-config | Miljökonfigurationen är inte giltig |  |
| 2016 | validate-config | Det går inte att avkoda JSON-typkonfigurationen |  |
| 2017 | validate-config | Den aktuella konfigurationen är inte kompatibel med den här versionen av Adobe Commerce |  |
| 2018 | validate-config | Vissa tjänster har genomgått EOL |  |
| 2019 | validate-config | Konfigurationsalternativet för MySQL-sökning är föråldrat | Använd Elasticsearch i stället. |
| 2029 | validate-config | Delad databas har tagits bort i Adobe Commerce och Magento Open Source 2.4.2 och kommer att tas bort i 2.5. | Om du använder delad databas bör du börja planera för att återgå till eller migrera till en enskild databas eller använda ett annat tillvägagångssätt. |
| 2020 | install-update | Adobe Commerce-installationen är klar, men `app/etc/env.php` konfigurationsfilen saknas eller är tom. | Nödvändiga data återställs från miljökonfigurationer och från filen .magento.env.yaml. |
| 2021 | install-update:db-connection | För delade databaser används anpassade anslutningar |  |
| 2022 | install-update:db-connection | Du har ändrat till en databaskonfiguration som inte är kompatibel med slavanslutningen. |  |
| 2023 | install-update:split-db | Aktivering av en delad databas kommer att hoppas över. |  |
| 2024 | install-update:split-db | Variabeln SPLIT_DB saknar konfigurationen för delade anslutningstyper. |  |
| 2025 | install-update:split-db | Slavanslutningen har inte angetts. |  |
| 2026 | pre-deploy:restore-writable-dirs | Det gick inte att återställa vissa data som genererats under byggfasen till de monterade katalogerna | Kontrollera `cloud.log` för mer information. |
| 2027 | validate-config:image-mode-variable | Lägesvärdet för miljövariabeln MAGE_MODE stöds inte | Ta bort miljövariabeln MAGE_MODE eller ändra dess värde till &quot;production&quot;. Adobe Commerce i molninfrastrukturen har endast stöd för produktionsläget. |
| 2028 | fjärrlagring | Det gick inte att aktivera fjärrlagring. | Verifiera autentiseringsuppgifter för fjärrlagring. |
| 2030 | validate-config | Elasticsearch och OpenSearch-tjänsterna installeras båda i infrastrukturskiktet. Adobe Commerce och Magento Open Source 2.4.4 och senare använder OpenSearch som standard | Ta bort Elasticsearch eller OpenSearch-tjänsten från infrastrukturlagret för att optimera resursanvändningen. |

### Steg efter driftsättning

| Felkod | Steg efter distribution | Felbeskrivning (rubrik) | Föreslagen åtgärd |
| - | - | - | - |
| 3001 | validate-config | Felsökningsloggning är aktiverat i Adobe Commerce | Aktivera inte felsökningsloggning för produktionsmiljöerna om du vill spara diskutrymme. |
| 3002 | uppvärmning | Det går inte att hämta arkiv-URL:er |  |
| 3003 | uppvärmning | Det går inte att hämta arkiv-URL |  |
| 3004 | säkerhetskopia | Kan inte skapa säkerhetskopior |  |

### Allmänt

| Felkod | Allmänt steg | Felbeskrivning (rubrik) | Föreslagen åtgärd |
| - | - | - | - |
| 4001 |  | Det går inte att hämta antalet systemprocessorer: |  |
