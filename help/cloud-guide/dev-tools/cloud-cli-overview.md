---
title: Cloud CLI
description: Läs mer om magento-cloud CLI och hur det hjälper er att hantera lokala utvecklingsmiljöer för Adobe Commerce i molninfrastrukturprojekt.
exl-id: 70dddd62-0269-4af4-bd2a-1a4fbf11a131
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---


# Cloud CLI

The `magento-cloud` Med CLI-verktyget kan utvecklare och systemadministratörer hantera molnprojekt och miljöer, utföra rutiner och utföra automatiseringsuppgifter. The `magento-cloud` CLI utökar funktionerna i [[!DNL Cloud Console]](../../get-started/cloud-console.md). När du har installerat `magento-cloud` CLI på din lokala arbetsstation kan du använda det för att hantera din Adobe Commerce i molninfrastrukturen Starter- och Pro-integreringsmiljöer.

**Installera `magento-cloud` CLI**:

1. På din lokala arbetsstation byter du till den katalog där du vill klona Cloud-projektet och där [ägare av filsystem](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) har _skriva_ åtkomst.

1. Installera `magento-cloud` CLI.

   ```bash
   curl -sS https://accounts.magento.cloud/cli/installer | php
   ```

1. Lägg till `magento-cloud` CLI till basprofilen.

   ```bash
   export PATH=$PATH:$HOME/.magento-cloud/bin
   ```

1. Läs in den uppdaterade basprofilen igen.

   ```bash
   . ~/.bash_profile
   ```

1. Om du vill starta CLI ringer du `magento-cloud` och ange autentiseringsuppgifter för ditt molnkonto när du uppmanas till detta.

   ```bash
   magento-cloud
   ```

   ```terminal
   Welcome to Magento Cloud!
   Please log in using your Magento Cloud account.
   Your email address or username:
   ```

1. Verifiera `magento-cloud` kommandot finns i din bana. I följande exempel visas de tillgängliga kommandona.

   ```bash
   magento-cloud list
   ```

## Gemensamma kommandon

Adobe har utformat de här kommandona för att hantera molnintegreringsmiljöer och rekommenderar att du kör `magento-cloud` CLI från en projektkatalog så att du kan utelämna `-p <project-ID>` parameter.

Följande lista över vanliga `magento-cloud` CLI-kommandon innehåller endast obligatoriska alternativ. Du kan använda `--help` med valfritt kommando för att se mer information.

| Kommando | Beskrivning |
| ------------------------------------ | -------------------------------------------------- |
| `magento-cloud login` | Logga in på projektet. |
| `magento-cloud list` | Visa en lista över tillgängliga kommandon för CLI-verktyget. |
| `magento-cloud environment:list` | Visa miljöerna i det aktuella projektet. |
| `magento-cloud environment:checkout` | Kolla in en befintlig miljö. |
| `magento-cloud environment:merge -e` | Sammanfoga ändringar i den här miljön med dess överordnade. |
| `magento-cloud variables` | Visa variabler i den här miljön. |
| `magento-cloud ssh` | Använd SSH för att ansluta till fjärrmiljön. |
| `magento-cloud url` | Öppna Adobe Commerce Store i en webbläsare. |
| `magento-cloud web` | Öppna [!DNL Cloud Console]. |

## Miljökommandon

Miljön _name_ skiljer sig från miljön _ID_ bara om du använder blanksteg eller versaler i miljönamnet. Ett miljö-ID består av alla gemener, siffror och tillåtna symboler. Versaler i ett miljönamn konverteras till gemener i ID:t. Blanksteg i ett miljönamn konverteras till streck.

Ett miljönamn _inte_ innehåller tecken som är reserverade för ditt Linux-skal eller för reguljära uttryck. Otillåtna tecken innehåller klammerparenteser (`{ }`), parenteser, asterisk (`*`), vinkelparenteser (`< >`), et-tecken (`&`), procent (`%`) och andra tecken.

The `magento-cloud environment:list` -kommandot visar systemhierarkier, medan `git branch` inte. Om du har kapslade miljöer använder du följande:

```bash
magento-cloud environment:list
```

### Distribuera om miljön

Utlösa en omdistribution utan att använda en push-funktion. Verifiera och bekräfta miljön för omdistribution. Använd inte omdistribuering om det finns ett bygge i ett väntande tillstånd.

```bash
magento-cloud environment:redeploy
```

Exempelsvar:

```terminal
Are you sure you want to redeploy the environment <environment-name>? [Y/n]
```

{{redeploy-warning}}

## Git-kommandon

Vissa av dessa kommandon liknar Git-kommandona. The `magento-cloud` -kommandon ansluter direkt till det Git-baserade Cloud-projektet med ytterligare funktioner. Om du skapar en gren utan att använda `magento-cloud` CLI är det inte&quot;aktiverat&quot; och byggs inte automatiskt när du gör ändringar i fjärrmiljön. The `magento-cloud` CLI-kommandot innefattar aktivering.

Använd `magento-cloud` så att förgreningen aktiveras.

```bash
magento-cloud environment:branch <new-name> <parent-branch>
```

För filialstatus:

- Använd `magento-cloud env` om du vill visa en lista över miljögrenarna och deras status: aktiv eller inaktiv.
- Använd `magento-cloud environment:activate` för att aktivera en miljögren.

Tryck på en tom Git-implementering för att utlösa en distribution. Exempel:

```bash
git commit --allow-empty -m "redeploy" && git push <branch-name>
```

Vissa åtgärder, till exempel att lägga till en användare, leder inte till distribution.

### Skapa en miljögren

Följande steg visar hur du använder kommandona CLI och Git för att hantera din lokala miljö:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Växla till [ägare av filsystem](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html).

1. Logga in på ditt projekt.

   ```bash
   magento-cloud login
   ```

1. Lista dina projekt.

   ```bash
   magento-cloud project:list
   ```

1. Lista miljöer i projektet. Varje miljö innehåller en aktiv Git-gren som innehåller kod, databas, miljövariabler, konfigurationer och tjänster.

   ```bash
   magento-cloud environment:list
   ```

   >[!NOTE]
   >
   >Det är viktigt att du använder `magento-cloud environment:list` eftersom den visar systemhierarkier, medan `git branch` kommandot gör inte det.

1. Hämta ursprungliga grenar för att få den senaste koden.

   ```bash
   git fetch origin
   ```

1. Checka ut, eller växla till, en viss gren och miljö.

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

   Git-kommandon checkar bara ut Git-grenen. The `magento-cloud checkout` kommandot checkar ut grenen och växlar till den aktiva miljön.

   >[!TIP]
   >
   >Du kan skapa en miljögren med `magento-cloud environment:branch <environment-name> <parent-environment-ID>` kommandosyntax. Det kan ta ytterligare tid att skapa och aktivera en miljögren.

1. Använd miljö-ID:t för att hämta uppdaterad kod till din lokala dator. Detta är inte nödvändigt om miljögrenen är ny.

   ```bash
   git pull origin <environment-ID>
   ```

1. (_Valfritt_) Skapa en [ögonblicksbild](../storage/snapshots.md) av miljön som backup.

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

## Uppdatera CLI

The `magento-cloud` CLI söker efter tillgängliga uppdateringar när du loggar in, men du kan söka efter uppdateringar med `self:update` -kommando. Om det finns en uppdatering följer du instruktionerna för att uppdatera CLI.

Om `magento-cloud` CLI är aktuellt, du ser följande svar:

```bash
magento-cloud update
```

```terminal
Checking for Magento Cloud CLI updates (current version: X.XX.X)
No updates found
```
