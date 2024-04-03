---
title: "Hantera grenar med [!DNL Cloud Console]"
description: Lär dig hur du hanterar miljögrenarna för Adobe Commerce i molninfrastrukturen med [!DNL Cloud Console].
role: Developer
feature: Cloud, Install
exl-id: 2c4ef149-fdb9-473f-91fd-5e6421ac5a43
source-git-commit: a5af3cc6e174a731a8f2ff198acd794384ef4585
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 0%

---

# Hantera grenar med [!DNL Cloud Console]

Du kan hantera dina miljöer med [!DNL Cloud Console] eller `magento-cloud` CLI. Dina projektfiler lagras i en Git-databas. Du kan använda Git-kommandon för att hantera koden, men `magento-cloud` CLI är utformat för att interagera med plattformsfunktioner, vilket Git-kommandona inte gör. Se [Git-kommandon](../dev-tools/cloud-cli-overview.md#git-commands) i Cloud CLI-avsnittet.

I det här avsnittet beskrivs hur du använder [!DNL Cloud Console] till:

- Lägga till eller ta bort en miljö
- Synkronisera (`git pull`) från den överordnade miljön
- Sammanfoga (`git push`) till den överordnade miljön

>[!TIP]
>
>Du kan inte skapa grenar från Pro Staging- och Production-miljöer. Du kan förgrena från `master` gren.

## Skapa en miljö

Förgreningsstrategin använder ett gemensamt Git-arbetsflöde där du utvecklar kod och lägger till tillägg i en utvecklingsgren. Se [Starter](../architecture/starter-architecture.md) och [Pro](../architecture/starter-develop-deploy-workflow.md) översikter över arkitekturen.

- Skapa en `staging` förgrening från `master` förgrening, sedan förgrening från `staging` för utveckling.
- För Pro skapar du en utvecklingsgren från `Integration` miljö.

Ditt konto har stöd för ett begränsat antal ![aktiv gren](../../assets/icon-active.png){width="32"} (active) and an unlimited number of ![inactive branch](../../assets/icon-inactive.png){width="32"} (inaktiva) utvecklingsgrenar. Hantera aktiva och inaktiva grenar genom att lägga till eller ta bort en gren med enbart [!DNL Cloud Console] eller Cloud CLI. Innan du kan ta bort en gren inaktiverar du grenen, som finns kvar i _Miljö_ lista som _inaktiv_. Du kan återaktivera grenen senare eller så kan du [ta bort grenen](../dev-tools/cloud-cli-overview.md#) i miljöinställningarna eller med molnet-CLI.

Om du behöver ytterligare aktiva miljöer för utveckling skickar du en [Supportbiljett](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

**Lägga till en gren**:

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Välj ett projekt i _Alla projekt_ lista.

1. Välj en miljö.

   >[!TIP]
   >
   >Din nya gren klonas från den här miljön. Välj en överordnad miljö som liknar den miljö du ska skapa.

1. Klicka på **[!UICONTROL Branch]**.

   ![Skapa en gren](../../assets/button-branch.png){width="150"}

1. I _Förgrenar från ..._ anger du ett förgreningsnamn.

   Miljön _name_ skiljer sig från miljön _ID_ bara om du använder blanksteg eller versaler i miljönamnet. Ett miljö-ID består av alla gemener, siffror och tillåtna symboler. Versaler i ett miljönamn konverteras till gemener i ID:t. Blanksteg i ett miljönamn konverteras till streck.

   Ett miljönamn **inte** innehåller tecken som är reserverade för ditt Linux-skal eller för reguljära uttryck. Otillåtna tecken innehåller klammerparenteser (`{ }`), parenteser, asterisk (`*`), vinkelparenteser (`>`), et-tecken (`&`), procent (<code>%</code>) och andra tecken.

1. Välj en **[!UICONTROL Environment type]**.

1. Klicka på **[!UICONTROL Create Branch]**.

1. Vänta medan miljön distribueras.

   Under distributionen är miljöstatusen  **Pågår**. När distributionen är klar ändras statusen till en grön bock för **framgång**.

## Skapa inaktiv gren

Du kan inte skapa en inaktiv gren från Adobe Commerce Cloud-konsolen eller CLI. Om du vill skapa en inaktiv gren skapar du den i Git-databasen och skickar den via `environment.Parent` på kommandot.

```bash
git push -o "environment.Parent=<parent branch>" <origin> <branch>
```

## Ta bort en miljö

Innan du kan ta bort en miljö måste du inaktivera den. När en miljö är inaktiv kan du ta bort den.

**Så här inaktiverar du en miljö**:

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Välj ett projekt i _Alla projekt_ lista.

1. Välj miljö i navigeringsfältet _Miljö_ lista.

1. Klicka på konfigurationsikonen till höger i det övre navigeringsfältet, som öppnar miljöinställningarna.

1. På _[!UICONTROL General]_bläddra nedåt till_[!UICONTROL Deactivate environment]_ och klicka **[!UICONTROL Deactivate environment and delete data]** och följ instruktionerna.

## Synkronisera en miljö

Synkronisering av en miljö (eller gren) är detsamma som `git pull origin <parent>`. Du kan synkronisera uppdaterad kod från en överordnad miljö. Du kan använda den här funktionen via [!DNL Cloud Console] för alla Starter- och Pro-miljöer.

För Pro-planen kan du synkronisera från mellanlagring och produktion till `master` gren. Synkroniseringen hämtar och push-tar bara fram kod, inte data. Om du vill synkronisera data dumpar du databasdata och överför dem till en annan miljös databas. Se [Migrera och distribuera statiska filer och data](/help/cloud-guide/deploy/staging-production.md#migrate-static-files).

**Synkronisera en miljö**:

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Välj ett projekt i _Alla projekt_ lista.

1. Klicka på namnet på grenen som ska synkroniseras i miljölistan.

1. Klicka på (synkronisera).

   ![Synkronisera en miljö](../../assets/button-sync.png){width="150"}

1. Markera de objekt som ska synkroniseras.

   - Ersätt data (data och filer) synkroniserar ändringar i databasen och innehållsfilerna från den överordnade grenen.
   - Sammanfoga - (kod) synkroniserar uppdaterad kod från den överordnade grenen.

   Detta skapar också ett CLI-kommando som du kan kopiera och använda.

1. Klicka **Synkronisera**.

## Sammanfoga med överordnad miljö

Att sammanfoga en miljö (eller en gren) är detsamma som att `git push origin`. Du sammanfogar för att skicka uppdaterad kod från en miljö till dess överordnade miljö. Du kan sammanfoga koden med `master`. Du kan distribuera till mellanlagring och produktion med `merge` -kommando.

**Sammanfoga med den överordnade miljön**:

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Välj ett projekt i _Alla projekt_ lista.

1. Klicka på namnet på grenen som ska sammanfogas i miljölistan.

1. Klicka på (sammanfoga).

   ![Sammanfoga en miljö](../../assets/button-merge.png){width="150"}

1. Klicka **Sammanfoga** och bekräfta åtgärden.

## Visa loggar

Via [!DNL Cloud Console]kan du granska olika loggar för olika miljöer, inklusive historik för bygge, driftsättning och driftsättning.

För **Starter** kan du granska bygg- och distributionsloggar och distributionshistoriken. Dessa miljöer innehåller `master` (Produktion) gren och alla grenar som skapats av den.

För **Pro** kan du granska följande loggar i varje miljö:

- Integration - Skapa, driftsätt och driftsättningshistorik
- Mellanlagring - Bygg loggar och driftsättningshistorik. Använd SSH för att logga in på servern för att visa distributionsloggar.
- Produktion - Bygg loggar och driftsättningshistorik. Använd SSH för att logga in på servern för att visa distributionsloggar.

**Så här visar du loggar i[!DNL Cloud Console]**:

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Välj ett projekt i _Alla projekt_ lista.

1. Välj en miljö.

   Miljövyn innehåller en [Aktivitetslista](activity-stream.md) som visas _senaste_ -händelser, en post per åtgärd försökte inkludera synk, sammanfogningar, förgreningar, säkerhetskopiering med mera. Klicka **Alla** för hela driftsättningshistoriken.

1. Om du vill visa byggloggen väljer du länken Slutfört eller Fel per distributionspost på kontot.

>[!TIP]
>
>Klicka på **Filtrera efter** -ikonen för en nedrullningsbar lista och välj vilken typ av meddelanden som ska visas.

## Hämta kod från en privat Git-databas

Ditt Adobe Commerce i molninfrastrukturprojekt kan innehålla kod från en privat Git-databas. Du kan till exempel ha kod för en anpassad modul eller tema i en privat rapport. Om du vill göra det måste du lägga till projektets offentliga SSH-nyckel i din privata Git-databas och uppdatera projektet `composer.json` -fil.

Om du vill lägga till en distributionsnyckel i din privata GitHub-databas måste du vara administratör för den databasen. Med GitHub kan du bara använda en distributionsnyckel för en databas.

Om du föredrar att ditt projekt har åtkomst till flera databaser kan du bifoga en SSH-nyckel till ett automatiskt användarkonto. Eftersom det här kontot inte används av en människa kallas det för [datoranvändare](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys). Lägg till datorkontot som medarbetare eller lägg till datoranvändaren i ett team med åtkomst till databaserna.

>[!INFO]
>
>Adobe rekommenderar att du lägger till och sammanfogar den här koden i dina Git-projektdatabaser. Om du inte konfigurerar anslutningen kan du få problem med bygget.

**För att hitta din offentliga SSH-nyckel**:

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Välj ett projekt i _Alla projekt_ lista.

1. Klicka på konfigurationsikonen till höger i det övre navigeringsfältet.

1. I _Projektinställningar_, klicka **[!UICONTROL Deploy Key]**.

1. Kopiera distributionsnyckeln till Urklipp och använd den på något av följande Git-baserade sätt:

>[!BEGINTABS]

>[!TAB GitHub]

### Ange din GitHub-distributionsnyckel

På GitHub är distributionsnycklar skrivskyddade som standard.

**Ange din offentliga projektnyckel som en GitHub-distributionsnyckel**:

1. Logga in som administratör i din GitHub-databas.
1. Klicka på databasen **[!UICONTROL Settings]** -fliken.

   >[!NOTE]
   >
   >Om du inte ser det här alternativet är du inte inloggad som databasadministratör och du kan inte slutföra den här uppgiften. Be din GitHub-databasadministratör att göra detta.

1. På _Inställningar_ i den vänstra navigeringen klickar du **[!UICONTROL Deploy Keys]**.
1. Klicka på **[!UICONTROL Add deploy key]**.
1. Följ anvisningarna.

I `composer.json`, använder du `<user>@<host>:<.git</code>` eller `ssh://<user>@<host>:<port>/<path>.git` om en port som inte är standard används.

>[!TAB Bitbucket]

### Ange en distributionsnyckel för Bitbucket

**Ange projektets offentliga nyckel som en Bitbucket-distributionsnyckel**:

1. Logga in som administratör i Bitbucket-databasen.
1. Klicka på i den vänstra navigeringen **[!UICONTROL Settings]**.
1. Klicka på Allmänt > **[!UICONTROL Deployment Keys]**.
1. Klicka på **[!UICONTROL Add Key]**.
1. Följ anvisningarna.

>[!TAB GitLab]

### Ange din GitLab-distributionsnyckel

**Lägga till den offentliga SSH-nyckeln för ditt projekt som en GitLab-distributionsnyckel**:

1. Logga in som ägare i din GitLab-databas.
1. Verifiera att _Pipelines_ är aktiverat för ditt projekt:

   1. Utöka **[!UICONTROL Visibility, project, features, permissions]** -avsnitt.
   1. Klicka vid behov på **[!UICONTROL Pipelines]** för att aktivera alternativet.

1. Lägg till den offentliga SSH-nyckeln i CI/CD-inställningarna.

   1. Klicka på Inställningar > **[!UICONTROL CI / CD]**.
   1. Klicka på Distribuera nycklar **Expandera** för att konfigurera nyckeln.
   1. I _Distribuera nyckel_ formulär, lägga till ett distributionsnyckelnamn i **[!UICONTROL Title]** och klistra in den offentliga SSH-nyckeln i **[!UICONTROL Key]** fält.
   1. Klicka **[!UICONTROL Add Key]** för att spara konfigurationen.

>[!ENDTABS]

## Säkra miljöer och grenar

Du kan komma åt dina projekt och miljöer från vilken plats som helst via en webbläsare via [!DNL Cloud Console]. Du kan ha säkerhetsinställningar för din produktionsmiljö, dina butiker och webbplatser. I det här avsnittet får du hjälp att skydda integrerings- och mellanlagringsmiljöer för enbart utvecklare, DBA:er med mera.

>[!WARNING]
>
>**GÖR INTE** Använd följande metoder för att skydda Pro Staging- och Production-miljöer. Det här avbryter cachelagring. Använd [Blockera](../cdn/fastly-vcl-blocking.md) finns i Fast CDN för Adobe Commerce.

**För säkra miljöer**:

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Välj ett projekt i _Alla projekt_ lista.

1. Välj en miljö och klicka på konfigurationsikonen i navigeringsfältet.

1. I miljöinställningarna _Allmänt_ flik, klicka **PÅ** for **[!UICONTROL HTTP access control enabled]** för säker åtkomst. Du kan välja mellan autentiseringsuppgifter och IP-adresser att filtrera för åtkomst.

1. Om du vill filtrera efter autentiseringsuppgifter klickar du på **[!UICONTROL Add Login]**, ange ett användarnamn och lösenord och klicka på **[!UICONTROL Add Login]** att lägga till.

1. Om du vill filtrera efter IP-adress anger du IP-adresserna i en lista med `deny` eller `allow`. Exempel:

   ```text
   123.456.789.111/29 allow
   123.456.789.112/29 allow
   234.123.567.111/29 allow
   0.0.0.0/0 deny
   ```

1. Klicka på **[!UICONTROL Save]**. Miljön distribueras om för att uppdatera säkerhet och inställningar. Adobe rekommenderar att du testar miljön när du har slutfört säkerhetsinställningarna.
