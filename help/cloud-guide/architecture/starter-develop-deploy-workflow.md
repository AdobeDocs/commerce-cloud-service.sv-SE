---
title: Arbetsflöde för startprojekt
description: Lär dig använda arbetsflödena för utveckling och distribution av Starter.
feature: Cloud, Paas
exl-id: f334047a-1e0d-45c7-bf96-5c2964741951
source-git-commit: 08f43a3b0a50cdb2a5e8a45bd2e2448bc6dbca2b
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 0%

---

# Arbetsflöde för startprojekt

Adobe Commerce i molninfrastrukturen innehåller en enda Git-databas med en `master` för produktionsmiljön som kan förgrenade för att skapa en staging och flera integreringsmiljöer för testning och utvecklingsarbete. Du kan ha upp till fyra aktiva miljöer, inklusive en `master` för produktionsservern. Se [Startarkitektur](starter-architecture.md) för en översikt.

För dina miljöer ska du följa [!UICONTROL Development > Staging > Production] arbetsflöde för att utveckla och driftsätta webbplatsen.

- **Produktionsmiljö (aktiv webbplats)**—Tillhandahåller en komplett produktionsmiljö med alla tjänster som byggs och driftsätts från koden på `master` gren.
- **Mellanlagringsmiljö**—Tillhandahåller en komplett staging-miljö som matchar produktionsmiljön med alla tjänster som byggs och driftsätts från en `staging` gren som du skapar genom att klona från `master`.
- **Integreringsmiljöer**—Tillhandahåller upp till två aktiva utvecklingsmiljöer som du skapar med `staging` gren. The `integration` -miljön stöder inte tredjepartstjänster som Fastly och New Relic.

För filialerna kan du följa alla utvecklingsmetoder. Du kan t.ex. använda en Agile-metod, t.ex. scrum, för att skapa förgreningar för varje sprint.

Du kan skapa grenar för alla användarartiklar från varje utskrift. Alla artiklar blir testbara. Du kan sammanfoga hela tiden till Sprint-grenen och validera den grenen kontinuerligt. När utskriften är slut kan du sammanfoga utskriften med `master` att driftsätta alla skärpeändringar i produktionen utan att behöva ta itu med en flaskhals i testningen.

## Arbetsflöde för utveckling

Utveckling och driftsättning i Starter-planer börjar med ditt initiala projekt. Du skapar ditt projekt med den&quot;tomma webbplatsen&quot;, som är en Adobe Commerce på en molninfrastrukturmallskodrepo med en helt förberedd butik. Detta skapar en `master` gren med en kopia av koden från produktionsmiljön.

Utvecklingsarbetsflödet omfattar följande:

- [Klona och förgrena](#clone-and-branch) från `master` att skapa `staging` och utvecklingsavdelningar
- [Utveckla kod](#develop-code) och installera tillägg lokalt i en utvecklingsgren, inklusive [!DNL Composer] uppdateringar
- [Konfigurera](#configure-store) dina inställningar för butik och tillägg
- [Generera konfiguration](#generate-configuration-management-files) hanteringsfiler
- [Push-kod](#push-code-and-test) och konfiguration för att bygga och distribuera till `staging` och `production` miljöer

![Utveckla och distribuera arbetsflöden](../../assets/starter/workflow.png)

Du kan också utföra några valfria steg för att utveckla och testa koden och dina lagringsdata:

- [Installera exempeldata](#optional-install-sample-data) till din butik
- [Hämta produktionsarkivdata](#optional-pull-production-data) ned till miljöer

I den här processen förutsätts att du har konfigurerat [lokal utvecklararbetsyta](../development/overview.md).

### Klona och förgrena

För ett nytt Starter Plan-projekt, `master` grenen klonades från Adobe Commerce i Git-databasen för molninfrastruktur. Klona `master` till din lokala miljö.

Formatet för Git-klonkommandot är:

```bash
git fetch origin
```

```bash
git pull origin <environment-ID>
```

Första gången du börjar arbeta i grenar för ditt Starter-projekt skapar du en `staging` gren. Detta skapar en kodgren som matchar `master` gren som distribuerar till en mellanlagringsmiljö för att testa konfigurations- och kodändringar innan den distribueras till produktionsmiljön.

Skapa sedan grenar från `staging` för att utveckla kod, lägga till tillägg och konfigurera tredjepartsintegreringar. När du utvecklar egen kod, lägger till tillägg, integrerar med en tredjepartstjänst, arbetar du i en utvecklingsgren som skapats från `staging` gren. Det finns fyra aktiva integreringsmiljöer. När du trycker på en aktiv gren distribuerar en av dessa integreringsmiljöer automatiskt koden för att testa.

Git-kommandot har följande format:

```bash
git checkout <branch-name>
```

Cloud CLI-formatet `branch` kommandot är:

```bash
magento-cloud environment:branch <environment-name> <parent-environment-ID>
```

![Förgrening från mallsida](../../assets/starter/branching.png)

### Utveckla kod

Med Adobe Commerce basgren för molninfrastrukturkod kan du börja installera tillägg, utveckla anpassad kod, lägga till teman och mycket annat.

Använd en förgreningsstrategi i utvecklingsarbetet. Om du använder en gren för att göra allt ditt arbete samtidigt kan det göra testningen svår. Du kan till exempel följa kontinuerliga integrerings- och Sprint-metoder för att arbeta:

- Lägg till några tillägg och konfigurera dem med din första gren
- Överför koden, testa och sammanfoga till mellanlagring och sedan Produktion
- Konfigurera dina tjänster fullständigt i `services.yaml` och lägga till ett tema
- Överför koden, testa och sammanfoga till mellanlagring och sedan Produktion
- Integrera med en tredjepartstjänst
- Överför koden, testa och sammanfoga till mellanlagring och sedan Produktion

Tills butiken är helt byggd, konfigurerad och redo att startas. Men om du fortsätter att läsa finns det många alternativ för din butik och kodkonfiguration.

>[!NOTE]
>
>Slutför inga konfigurationer på din lokala arbetsstation än.

![Push-kod från lokal](../../assets/starter/push-code.png)

### Konfigurera butik

När du är redo att konfigurera butiken skickar du all kod till `integration` miljö. Konfigurera dina butiksinställningar från administratören för integreringsmiljön, inte i den lokala miljön. Du kan hitta URL:en genom att klicka på **Åtkomstplats** i [!DNL Cloud Console]

Mer information om konfigurationer finns i dokumentationen för Adobe Commerce och de installerade tilläggen. Här är några länkar och idéer som hjälper dig att komma igång:

- [Bästa tillvägagångssätt för butikskonfiguration](../store/best-practices.md) för bästa praxis i molnet
- [Grundkonfiguration](https://docs.magento.com/user-guide/configuration/configuration-basic.html) för administratörsåtkomst, namn, språk, valutor, varumärken, webbplatser, butiksvyer med mera
- [Tema](https://docs.magento.com/user-guide/design/design-theme.html) för webbplatsens och butikernas utseende och känsla, inklusive CSS och layouter
- [Systemkonfiguration](https://docs.magento.com/user-guide/system/system.html) för roller, verktyg, meddelanden och din krypteringsnyckel för databasen
- Tilläggsinställningar med hjälp av deras dokumentation

Förutom att bara lagra inställningar kan du konfigurera flera webbplatser och butiker, konfigurerade tjänster och mycket mer. Se [Konfigurera din butik](../store/overview.md).

### Generera konfigurationshanteringsfiler

Om du är bekant med Adobe Commerce kanske du är orolig för hur du hämtar konfigurationsinställningarna från databasen under utvecklingen till testnings- och produktionsmiljöerna. Tidigare var du tvungen att kopiera alla konfigurationsinställningar på papper eller i en fil och sedan manuellt tillämpa inställningarna i andra miljöer. Eller så har du dumpat databasen och överfört data till en annan miljö.

Adobe Commerce i molninfrastruktur innehåller två [Konfigurationshantering](../store/store-settings.md) kommandon som exporterar konfigurationsinställningar från miljön till en fil. Dessa kommandon är bara tillgängliga för **Adobe Commerce om molninfrastruktur 2.2 och senare**.

- `php .vendor/bin/ece-tools config:dump`—Exporterar endast de konfigurationsinställningar som du har angett eller ändrat från standardinställningar till en konfigurationsfil. _Rekommenderas_.
- `php bin/magento app:config:dump`—Exporterar alla konfigurationsinställningar, inklusive ändrade och standardinställningar, till en konfigurationsfil.

Den genererade filen är `app/etc/config.php`.

Generera filen i den integreringsmiljö där du konfigurerade Adobe Commerce. Stega genom processen att skapa filen, lägga till den i din gren och distribuera den.

**Viktiga anteckningar** på Configuration Management:

- Alla konfigurationsinställningar som ingår i filen som genereras från `app:config:dump` -kommandot är låst för redigering, eller skrivskyddat, i den distribuerade miljön. Detta är en anledning till att Adobe rekommenderar att du använder `.vendor/bin/ece-tools config:dump` -kommando.

  Du kan till exempel installera en modul för Snabb i utvecklingsmiljön. Du kan bara konfigurera den här modulen i staging- och produktionsmiljön. Använda `.vendor/bin/ece-tools config:dump` -kommandot gör att standardfälten förblir redigerbara när du distribuerar dina utvecklingsändringar till mellanlagrings- och produktionsmiljön.

- Den genererade filen kan vara lång beroende på hur stor distributionen är. The `.vendor/bin/ece-tools config:dump` kommandot genererar en mindre fil än den fil som skapas av `app:config:dump` -kommando.

Om du använder Adobe Commerce version 2.2 eller senare innehåller konfigurationshanteringskommandona en extra funktion för att skydda känsliga data, till exempel sandlådeautentiseringsuppgifter för en PayPal-modul. Under exportprocessen exporteras alla värden som innehåller känsliga data till en separat konfigurationsfil -`env.php` i `app/etc/` katalog. Den här filen finns kvar i din lokala miljö och kopieras inte när du skickar koden till en annan gren. Du kan också skapa miljövariabler med CLI-kommandon i alla Adobe Commerce-program för molninfrastrukturversioner.

![Miljövariabler genererar](../../assets/starter/env-variables.png)

Se [Konfigurationshantering](../store/store-settings.md).

### Skjut kod och testa

Nu bör du ha en utvecklad kodgren med en konfigurationsfil (`config.local.php` eller `config.php`) redo att testa.

Varje gång du skickar kod från din lokala miljö körs en serie skript för att skapa och distribuera. Dessa skript genererar ny kod och distribuerar den till fjärrmiljön. Om du till exempel flyttar en utvecklingsgren från den lokala miljön till fjärrgrenen uppdateras tjänster, kod och statiskt innehåll av en matchande miljö.

Du kan komma åt den här miljön direkt med en butiks-URL, Admin-URL och SSH. Dessa miljöer omfattar en webbserver, en databas och konfigurerade tjänster. När det är klart kan du börja distribuera och testa i mellanlagringsmiljön.

Mer information finns i [Arbetsflöde för distribution](#deployment-workflow).

### Valfritt: Installera exempeldata

Om du behöver exempeldata när du utvecklar din butik kan du installera exempeldata. Dessa data simulerar en aktiv butik, inklusive kunder, produkter och andra data. Dessa exempeldata fungerar bäst med en&quot;tom webbplats&quot;-installation av Adobe Commerce i en molninfrastrukturmall när du skapar ditt projekt. Det bästa är att ta bort exempeldata innan du publicerar. Se [Installera valfria exempeldata](../test/sample-data.md).

![Installera valfria exempeldata](../../assets/starter/sample-data.png)

### Valfritt: Hämta produktionsdata

Lägg till alla produkter, kataloger, webbplatsinnehåll och så vidare, direkt i `production` miljö. Genom att lägga till dessa data i produktionsmiljön kan ni tillhandahålla uppdaterade priser, kuponger, lageraktier, säljinformation, information om framtida erbjudanden med mera till era kunder. Dessa data inkluderar inte tilläggskonfigurationer som du konfigurerar i din lokala utvecklingsgren.

När du utvecklar funktioner kan du lägga till tillägg och utforma teman, så att du kan arbeta med riktiga data. Du kan när som helst [skapa en databasdump](../storage/database-dump.md) från produktionsmiljön och skicka det vidare till dina förproduktionsmiljöer och integreringsmiljöer efter behov.

Så här exporterar du produktionsdata som testdata som kan användas i miljöer med staging och integration:

- [Kör supportverktygen](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/run-support-utilities.html) CLI-kommandon (rekommenderas) vid export av en skyddad säkerhetskopia av kund- och butiksdata med Adobe Commerce krypteringsnyckel

- [Datainsamling](https://docs.magento.com/user-guide/system/support-data-collector.html) verktyg för att generera och exportera data

Information om hur du migrerar dessa data finns i [Migrera och distribuera statiska filer och data](../deploy/staging-production.md#migrate-static-files).

![Dra in och sanera produktionsdata](../../assets/starter/data-code-process.png)

>[!NOTE]
>
>Innan du överför data till en annan miljö bör du överväga att sanera dina data. Du har ett par alternativ, bland annat [med supportverktyg](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/run-support-utilities.html) eller utveckla ett skript som rensar bort kunddata.

>[!WARNING]
>
>Överför inte en databas från en integration- eller staging-miljö till en produktionsmiljö. Om du gör det skriver data från integrerings- eller staging-miljön över era produktionsdata, inklusive försäljning, beställningar, nya och uppdaterade kunder och mycket annat.

## Arbetsflöde för distribution

Så som beskrivs i arkitekturinformationen är Adobe Commerce om molninfrastruktur Git-drivet. Driftsättningen av Adobe Commerce i molninfrastrukturen ingår i era Git-push-processer för filialer.

När du skickar förgrenad kod från din lokala miljö till fjärrgrenen börjar en serie skript för att skapa och distribuera.

Skapa skript:

- Webbplatsen i målmiljön fortsätter att köras under en bygge

- Kontrollera och kör Adobe Commerce på korrigeringar och snabbkorrigeringar för molninfrastruktur

- Kompilera koden med en logg för bygge och driftsättning

- Kontrollera om Configuration Management är installerat om statiskt innehåll inträffar under den här fasen

- Skapa eller använda en instruktionsmarginal med oändrad kod för en snabbare process

- Tillhandahåller alla backend-tjänster och program

Distribuera skript:

- Placerar platsen i målmiljön i underhållsläge

- Distribuerar statiskt innehåll om det inte slutförs under bygget

- Installerar eller uppdaterar Adobe Commerce i molninfrastrukturen

- Konfigurera routning för trafik

När allt är klart återkommer din butik online, live, med all uppdaterad kod och alla konfigurationer.

Se [Distributionsprocess](../deploy/process.md).

### Skjut till mellanlagring och testa

Flytta alltid koden i iterationer till `staging` för fullständig testning. Första gången du använder den här miljön måste du konfigurera några tjänster, inklusive [Snabbt](/help/cloud-guide/cdn/fastly.md) och [New Relic](../monitor/new-relic-service.md). Konfigurera även betalningsgatewayer, leverans, meddelanden och andra viktiga tjänster med sandlåda eller testningsreferenser.

Mellanlagring är en förproduktionsmiljö som ger alla tjänster och inställningar så nära produktionen som möjligt. Testa noga alla tjänster, verifiera prestandatestningsverktygen, utför UAT-tester som administratör och som kund tills du känner att butiken är redo för produktion.

Se [Distribuera din butik](../deploy/staging-production.md).

### Skjut till produktion

När du trycker på `master` -förgreningen, du går till `production` miljö. Komplettera konfigurations- och testningsaktiviteterna i produktionsmiljön på samma sätt som i testmiljön, med en viktig skillnad. I produktionsmiljön använder du live-autentiseringsuppgifter för konfiguration och testning. Så fort du lanserar webbplatsen kan kunderna slutföra inköpen och administratörer kan hantera livebutiken.

Se [Distribuera din butik](../deploy/staging-production.md).

### Starta webbplatsen

Det finns en tydlig genomgång för att publicera din webbplats. När du är klar med de här stegen kan din butik leverera produkter i ditt skräddarsydda tema till försäljning direkt.

Se [Starta webbplatsen](../launch/overview.md).

## Kontinuerlig integrering

Med er förgrening- och utvecklingsmetod kan ni enkelt utveckla nya funktioner, konfigurera ändringar och lägga till tillägg för att kontinuerligt utveckla och driftsätta uppdateringar.

Alla miljöer med molninfrastruktur har stöd för kontinuerlig integrering för konstanta uppdateringar. Det här arbetsflödet stöder releaser flera gånger om dagen eller enligt ett schema som passar ditt företags behov.

- Skapa utvecklingsgrenar med framtida funktioner och ändringar

- Testa koden i `integration` miljö

- Distribuera och testa i `staging` miljö

- Distribuera till `production` miljö
