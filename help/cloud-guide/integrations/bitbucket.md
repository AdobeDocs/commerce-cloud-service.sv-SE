---
title: Bitbucket-integrering
description: Lär dig hur du integrerar ditt Adobe Commerce i molninfrastrukturprojekt med Bitbucket.
feature: Cloud, Integration
exl-id: cd3cffbe-268f-429b-a2ea-0306159f4a6b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# Bitbucket-integrering

Du kan konfigurera Bitbucket-databasen så att den automatiskt skapar och distribuerar en miljö när du skickar kodändringar. Den här integreringen synkroniserar Bitbucket-databasen med ditt Adobe Commerce på molninfrastrukturskontot.

{{private-repository}}

## Förutsättningar

- Administratörsåtkomst till Adobe Commerce i molninfrastrukturprojektet
- [`magento-cloud` CLI](../dev-tools/cloud-cli-overview.md) verktyg i din lokala miljö
- Ett Bitbucket-konto
- Administratörsåtkomst till Bitbucket-databasen
- En SSH-åtkomstnyckel för Bitbucket-databasen

## Förbered databasen

Klona ditt Adobe Commerce i molninfrastrukturprojekt från en befintlig miljö och migrera projektgrenarna till en ny, tom Bitbucket-databas, med samma filialnamn intakta. Det är **kritisk** för att behålla ett identiskt Git-träd, så att du inte förlorar några befintliga miljöer eller grenar i ditt Adobe Commerce i molninfrastrukturprojekt.

1. Logga in på ditt Adobe Commerce i molninfrastrukturprojekt från terminalen.

   ```bash
   magento-cloud login
   ```

1. Lista dina projekt och kopiera projekt-ID:t.

   ```bash
   magento-cloud project:list
   ```

1. Klona projektet till din lokala miljö.

   ```bash
   magento-cloud project:get <project-ID>
   ```

1. Lägg till din Bitbucket-databas som en fjärrdatabas.

   ```bash
   git remote add origin git@bitbucket.org:<user-name>/<repo-name>.git
   ```

   Standardnamnet för fjärranslutningen kan vara `origin` eller `magento`. If `origin` finns kan du välja ett annat namn eller så kan du byta namn på eller ta bort den befintliga referensen. Se [git-remote-dokumentation](https://git-scm.com/docs/git-remote).

1. Kontrollera att du har lagt till Bitbucket-fjärrkontrollen korrekt.

   ```bash
   git remote -v
   ```

   Förväntat svar:

   ```terminal
   origin git@bitbucket.org:<user-name>/<repo-name>.git (fetch)
   origin git@bitbucket.org:<user-name>/<repo-name>.git (push)
   ```

1. Skicka projektfilerna till din nya Bitbucket-databas. Kom ihåg att behålla samma namn på alla grenar.

   ```bash
   git push -u origin master
   ```

   Om du börjar med en ny Bitbucket-databas kan du behöva använda `-f` eftersom fjärrdatabasen inte matchar din lokala kopia.

1. Kontrollera att Bitbucket-databasen innehåller alla dina projektfiler.

## Skapa en OAuth-kund

Bitbucket-integreringen kräver en [OAuth-kund](https://support.atlassian.com/bitbucket-cloud/docs/use-oauth-on-bitbucket-cloud/). Du behöver OAuth `key` och `secret` från den här konsumenten till nästa avsnitt.

**Skapa en OAuth-konsument i Bitbucket**:

1. Logga in på [Bitbucket](https://id.atlassian.com/login) konto.

1. Klicka **Inställningar** > **Åtkomsthantering** > **OAuth**.

1. Klicka **Lägg till kund** och konfigurera det enligt följande:

   ![Bitbucket OAuth-konsumentkonfiguration](../../assets/oauth-consumer-config.png)

   >[!WARNING]
   >
   >Ett giltigt **Återanrops-URL** är inte obligatoriskt, men du måste ange ett värde i det här fältet för att kunna slutföra integreringen.

1. Klicka **Spara**.

1. Klicka på konsumenten **Namn** för att visa din OAuth `key` och `secret`.

1. Kopiera din OAuth `key` och `secret` för att konfigurera integreringen.

## Konfigurera integreringen

1. Gå till Adobe Commerce i molninfrastrukturprojekt från terminalen.

1. Skapa en temporär fil med namnet `bitbucket.json` och lägg till följande och ersätt variablerna inom vinkelparenteser med dina värden:

   ```json
   {
     "type": "bitbucket",
     "repository": "<bitbucket-user-name/bitbucket-repo-name>",
     "app_credentials": {
       "key": "<oauth-consumer-key>",
       "secret": "<oauth-consumer-secret>"
     },
     "prune_branches": true,
     "fetch_branches": true,
     "build_pull_requests": true,
     "resync_pull_requests": true
   }
   ```

   >[!TIP]
   >
   >Var noga med att använda namnet på Bitbucket-databasen och inte URL:en. Integreringen misslyckas om du använder en URL.

1. Lägg till integrationen i ditt projekt med `magento-cloud` CLI-verktyg.

   >[!WARNING]
   >
   >Följande kommando skriver över _alla_ koda i ditt Adobe Commerce i molninfrastrukturprojekt med kod från Bitbucket-databasen. Detta omfattar alla filialer, inklusive `production` gren. Den här åtgärden utförs omedelbart och kan inte ångras. Det är en god vana att klona alla dina grenar från Adobe Commerce i molninfrastrukturprojekt och överföra dem till Bitbucket-databasen **före** lägga till Bitbucket-integrering.

   ```bash
   magento-cloud project:curl -p '<project-ID>' /integrations -i -X POST -d "$(< bitbucket.json)"
   ```

   Detta returnerar ett långt HTTP-svar med rubriker. En lyckad integrering returnerar statuskoden 200 eller 201. Statusen 400 eller högre anger att ett fel har inträffat.

1. Ta bort den tillfälliga `bitbucket.json` -fil.

1. Verifiera projektintegreringen.

   ```bash
   magento-cloud integrations -p <project-ID>
   ```

   ```terminal
   +----------+-----------+--------------------------------------------------------------------------------+
   | ID       | Type      | Summary                                                                        |
   +----------+-----------+--------------------------------------------------------------------------------+
   | <int-id> | bitbucket | Repository: bitbucket_Account/magento-int                                      |
   |          |           | Hook URL:                                                                      |
   |          |           | https://magento-url.cloud/api/projects/<project-id>/integrations/<int-id>/hook |
   +----------+-----------+--------------------------------------------------------------------------------+
   ```

   Anteckna **URL för krok** för att konfigurera en webkrok i BitBucket.

### Lägg till en webkrok i BitBucket

Om du vill kunna kommunicera händelser, till exempel en push-funktion, med din Creative Cloud Git-server, måste du ha en webkrok för din BitBucket-databas. Metoden för att konfigurera en Bitbucket-integrering som är detaljerad på den här sidan skapar automatiskt en webkrok när den följs korrekt. Det är viktigt att verifiera webbkroken för att undvika att skapa flera integreringar.

1. Logga in på [Bitbucket](https://id.atlassian.com/login) konto.

1. Klicka **Databaser** och välj projekt.

1. Klicka **Databasinställningar** > **Arbetsflöde** > **Webhooks**.

1. Kontrollera webkroken innan du fortsätter.

   Om kroken är aktiv hoppar du över de återstående stegen och [Testa integreringen](#test-the-integration). Haken ska ha ett namn som liknar **&quot;Adobe Commerce i molninfrastruktur &lt;project_id>&quot;** och ett krok-URL-format som liknar: `https://<zone>.magento.cloud/api/projects/<project_id>/integrations/<id>/hook`

1. Klicka **Lägg till webkrok**.

1. I _Lägg till ny webbkrok_ redigera följande fält:

   - **Titel**: Adobe Commerce Integration
   - **URL**: Använd Hook-URL:en från `magento-cloud` integreringslista
   - **Utlösare**: Standardvärdet är en grundläggande _Databasöverföring_

1. Klicka **Spara**.

### Testa integreringen

När du har konfigurerat Bitbucket-integreringen kan du kontrollera att integreringen fungerar med `magento-cloud` CLI:

```bash
magento-cloud integration:validate
```

Du kan också testa den genom att göra en enkel ändring i Bitbucket-databasen.

1. Skapa en testfil.

   ```bash
   touch test.md
   ```

1. Verkställ och skicka ändringen till Bitbucket-databasen.

   ```bash
   git add . && git commit -m "Testing Bitbucket integration" && git push
   ```

1. Logga in på [[!DNL Cloud Console]](../project/overview.md) och verifiera att ditt implementeringsmeddelande visas och att ditt projekt distribueras.

   ![Testa Bitbucket-integreringen](../../assets/bitbucket-integration.png)

## Skapa en molngren

Bitbucket-integreringen kan inte aktivera nya miljöer i ditt Adobe Commerce i molninfrastrukturprojekt. Om du skapar en miljö med Bitbucket måste du aktivera miljön manuellt. För att undvika det här extra steget är det bäst att skapa miljöer med `magento-cloud` CLI eller [!DNL Cloud Console].

**Så här aktiverar du en förgrening som har skapats med Bitbucket**:

1. Använd `magento-cloud` CLI för att driva filialen.

   ```bash
   magento-cloud environment:push from-bitbucket
   ```

   ```terminal
   Pushing from-bitbucket to the new environment from-bitbucket
   Activate from-bitbucket after pushing? [Y/n] y
   Parent environment [master]: integration
   --- (Validation and activation messages)
   ```

1. Kontrollera att miljön är aktiv.

   ```bash
   magento-cloud environment:list
   ```

   ```terminal
   Your environments are:
   +---------------------+----------------+--------+
   | ID                  | Name           | Status |
   +---------------------+----------------+--------+
   | master              | Master         | Active |
   |  integration        | integration    | Active |
   |    from-bitbucket * | from-bitbucket | Active |
   +---------------------+----------------+--------+
   * - Indicates the current environment
   ```

När du har skapat en miljö kan du överföra motsvarande gren till din Bitbucket-fjärrdatabas med vanliga Git-kommandon. Efterföljande ändringar av din gren i Bitbucket skapar och driftsätter automatiskt miljön.

## Ta bort integreringen

Du kan ta bort Bitbucket-integreringen från ditt projekt utan att koden påverkas.

**Ta bort Bitbucket-integrering**:

1. Logga in på ditt Adobe Commerce i molninfrastrukturprojekt från terminalen.

1. Visa en lista över era integreringar. Du behöver Bitbucket-integrerings-ID för att kunna slutföra nästa steg.

   ```bash
   magento-cloud integration:list
   ```

1. Ta bort integreringen.

   ```bash
   magento-cloud integration:delete <int-ID>
   ```

Du kan även ta bort Bitbucket-integreringen genom att logga in på ditt Bitbucket-konto och återkalla OAuth-anslaget för kontot _Inställningar_ sida.

## Bitbucket-serverintegration

Om du vill använda Bitbucket-serverintegreringen behöver du följande:

- [Bitbucket-åtkomsttoken](https://confluence.atlassian.com/bitbucketserver/http-access-tokens-939515499.html)—Generera en token som beviljar Project `read` åtkomst och arkiv `admin` åtkomst
- [URL för Bitbucket-server](https://confluence.atlassian.com/bitbucketserver/specify-the-bitbucket-base-url-776640392.html)—Lägg till bas-URL:en för Bitbucket-instansen

Även om du kan använda Cloud CLI för att gå igenom integreringsstegen för Bitbucket-servern ser det fullständiga kommandot ut ungefär så här:

```bash
magento-cloud integration:add --type=bitbucket_server --base-url=<bitbucket-url> --username=<username> --token=<bitbucket-access-token> --project=<project-ID>
```

Använd kommandot help om du vill ha fler användningskrav och alternativ: `magento-cloud integration:add --help`
