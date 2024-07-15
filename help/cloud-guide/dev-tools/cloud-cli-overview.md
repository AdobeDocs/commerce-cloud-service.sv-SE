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

Med CLI-verktyget `magento-cloud` kan utvecklare och systemadministratörer hantera molnprojekt och miljöer, utföra rutiner och köra automatiseringsåtgärder. CLI:n `magento-cloud` utökar funktionerna i [[!DNL Cloud Console]](../../get-started/cloud-console.md). När du har installerat CLI:n för `magento-cloud` på din lokala arbetsstation kan du använda den för att hantera din Adobe Commerce i integreringsmiljöer för Starter och Pro i molnet.

**Så här installerar du `magento-cloud` CLI**:

1. På din lokala arbetsstation ändrar du till den katalog där du vill klona Cloud-projektet och där [filsystemägaren](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) har _write_ -åtkomst.

1. Installera CLI:n för `magento-cloud`.

   ```bash
   curl -sS https://accounts.magento.cloud/cli/installer | php
   ```

1. Lägg till `magento-cloud` CLI i basprofilen.

   ```bash
   export PATH=$PATH:$HOME/.magento-cloud/bin
   ```

1. Läs in den uppdaterade basprofilen igen.

   ```bash
   . ~/.bash_profile
   ```

1. Om du vill initiera CLI ringer du `magento-cloud` och anger autentiseringsuppgifterna för ditt molnkonto när du uppmanas till det.

   ```bash
   magento-cloud
   ```

   ```terminal
   Welcome to Magento Cloud!
   Please log in using your Magento Cloud account.
   Your email address or username:
   ```

1. Kontrollera att kommandot `magento-cloud` finns i sökvägen. I följande exempel visas de tillgängliga kommandona.

   ```bash
   magento-cloud list
   ```

## Gemensamma kommandon

Adobe har utformat de här kommandona för att hantera molnintegreringsmiljöer och rekommenderar att du kör CLI:n för `magento-cloud` från en projektkatalog så att du kan utelämna parametern `-p <project-ID>`.

Följande lista med vanliga `magento-cloud` CLI-kommandon innehåller endast obligatoriska alternativ. Du kan använda alternativet `--help` tillsammans med valfritt kommando för att visa mer information.

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

Miljön _name_ skiljer sig bara från miljön _ID_ om du använder blanksteg eller versaler i miljönamnet. Ett miljö-ID består av alla gemener, siffror och tillåtna symboler. Versaler i ett miljönamn konverteras till gemener i ID:t. Blanksteg i ett miljönamn konverteras till streck.

Miljönamnet _får inte_ innehålla tecken som är reserverade för ditt Linux-skal eller för reguljära uttryck. Otillåtna tecken är klammerparenteser (`{ }`), parenteser, asterisk (`*`), vinkelparenteser (`< >`), et-tecken (`&`), procent (`%`) och andra tecken.

Kommandot `magento-cloud environment:list` visar miljöhierarkier, men det gör inte `git branch`. Om du har kapslade miljöer använder du följande:

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

Vissa av dessa kommandon liknar Git-kommandona. `magento-cloud`-kommandona ansluter direkt till det Git-baserade Cloud-projektet med ytterligare funktioner. Om du skapar en gren utan att använda CLI:n för `magento-cloud`,&quot;aktiveras&quot; den inte och byggs inte automatiskt när du gör ändringar i fjärrmiljön. CLI-kommandot `magento-cloud` innehåller aktivering.

Om du vill skapa en gren använder du kommandot `magento-cloud` så att grenen aktiveras.

```bash
magento-cloud environment:branch <new-name> <parent-branch>
```

För filialstatus:

- Använd kommandot `magento-cloud env` för att visa en lista över miljögrenarna och deras status: aktiv eller inaktiv.
- Använd kommandot `magento-cloud environment:activate` för att aktivera en miljögren.

Tryck på en tom Git-implementering för att utlösa en distribution. Exempel:

```bash
git commit --allow-empty -m "redeploy" && git push <branch-name>
```

Vissa åtgärder, till exempel att lägga till en användare, leder inte till distribution.

### Skapa en miljögren

Följande steg visar hur du använder kommandona CLI och Git för att hantera din lokala miljö:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Växla till [filsystemets ägare](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html).

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
   >Det är viktigt att använda kommandot `magento-cloud environment:list` eftersom det visar systemhierarkier, vilket kommandot `git branch` inte gör.

1. Hämta ursprungliga grenar för att få den senaste koden.

   ```bash
   git fetch origin
   ```

1. Checka ut, eller växla till, en viss gren och miljö.

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

   Git-kommandon checkar bara ut Git-grenen. Kommandot `magento-cloud checkout` checkar ut grenen och växlar till den aktiva miljön.

   >[!TIP]
   >
   >Du kan skapa en miljögren med kommandosyntaxen `magento-cloud environment:branch <environment-name> <parent-environment-ID>`. Det kan ta ytterligare tid att skapa och aktivera en miljögren.

1. Använd miljö-ID:t för att hämta uppdaterad kod till din lokala dator. Detta är inte nödvändigt om miljögrenen är ny.

   ```bash
   git pull origin <environment-ID>
   ```

1. (_Valfritt_) Skapa en [ögonblicksbild](../storage/snapshots.md) av miljön som en säkerhetskopia.

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

## Uppdatera CLI

CLI:n `magento-cloud` söker efter tillgängliga uppdateringar när du loggar in, men du kan söka efter uppdateringar med kommandot `self:update`. Om det finns en uppdatering följer du instruktionerna för att uppdatera CLI.

Om ditt `magento-cloud` CLI är uppdaterat ser du följande svar:

```bash
magento-cloud update
```

```terminal
Checking for Magento Cloud CLI updates (current version: X.XX.X)
No updates found
```
