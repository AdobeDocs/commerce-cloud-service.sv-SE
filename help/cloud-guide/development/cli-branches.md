---
title: Hantera grenar med CLI
description: Lär dig hur du hanterar miljögrenarna för Adobe Commerce i molninfrastrukturen med hjälp av Cloud CLI.
role: Developer
feature: Cloud, Install
exl-id: a871c7e2-4506-4a05-8fc2-fc5ef2afe609
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# Hantera grenar med CLI

Installera `magento-cloud` CLI, se [CLI-referens för molnet](../dev-tools/cloud-cli-overview.md). När du har installerat `magento-cloud` CLI och konfigurera SSH-nycklar för fjärråtkomst till din molninfrastruktur kan du använda `magento-cloud` CLI-kommandon för att hantera projektmiljöer. Mer information om miljöarkitekturen finns i [Startarkitektur](../architecture/starter-architecture.md) eller [Pro-arkitektur](../architecture/pro-architecture.md).

Hantera grenar och miljöer med [!DNL Cloud Console], se [Hantera grenar med [!DNL Cloud Console]](../project/console-branches.md).

## Använda CLI-kommandon

The `magento-cloud` CLI-kommandon liknar Git-kommandon. Du kan använda dem för att ansluta till ditt projekt och hantera dina miljöer. Även om du kan köra kommandona från en katalog bör du köra dem från en projektkatalog. När du kör från en projektkatalog kan du utesluta `-p <project-ID>` parameter. Se [CLI-referens för molnet](../dev-tools/cloud-cli-overview.md).

## Klona projektet

I följande instruktioner används en kombination av `magento-cloud` CLI-kommandon och Git-kommandon för att klona projektet till din lokala arbetsstation. Visa en fullständig lista över `magento-cloud` CLI-kommandon använder du `magento-cloud list` -kommando.

>[!IMPORTANT]
>
>Vissa Git-kommandon kan inte slutföra en åtgärd i Adobe Commerce i ett molninfrastrukturprojekt. Du kan till exempel skapa en gren med ett Git-kommando, men du kan inte skapa och aktivera en ny miljö. Du måste skapa en miljö med `magento-cloud environment:branch <branch-name>` för att miljön ska bli _aktiv_. Du kan också använda [!DNL Cloud Console] för att skapa aktiva miljöer. Se [CLI-referens för molnet](../dev-tools/cloud-cli-overview.md#git-commands).

**Klona ett projekt `master` miljö**:

1. Logga in på din lokala arbetsstation med en [ägare av filsystem](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) konto.

1. Byt till webbservern eller det virtuella värdsystemet _docroot_ katalog.

1. Logga in med `magento-cloud` CLI.

   ```bash
   magento-cloud login
   ```

1. Lista dina projekt.

   ```bash
   magento-cloud project:list
   ```

1. Klona ett projekt.

   ```bash
   magento-cloud project:get <project-ID>
   ```

   Ange ett katalognamn när du uppmanas till detta.

1. Ändra till `magento2` katalog.

1. Visa tillgängliga miljöer för projektet.

   ```bash
   magento-cloud environment:list
   ```

   >[!IMPORTANT]
   >
   >The `magento-cloud environment:list` -kommandot visar systemhierarkier, medan `git branch` kommandot gör inte det.

1. Hämta fjärrgrenarna.

   ```bash
   git fetch origin
   ```

1. Dra in uppdaterad kod.

   ```bash
   git pull origin <environment-ID>
   ```

>[!TIP]
>
>Se [Integreringar](../integrations/overview.md) om du vill ha information om hur du använder Git-baserade värdtjänster med Adobe Commerce om molninfrastruktur.

## Skapa en gren för utveckling

När du har klonat projektet och uppdaterat Adobe Commerce administratörskonfiguration kan du skapa en gren för utvecklingen. Som tidigare nämnts måste du skapa en miljö med `magento-cloud environment:branch <branch-name>` kommandot eller [!DNL Cloud Console] för miljön _aktiv_.

- För [Starter](../architecture/starter-develop-deploy-workflow.md#clone-and-branch)kan du skapa en gren för `staging`och sedan skapa en utvecklingsgren baserat på `staging` gren.
- För [Pro](../architecture/pro-develop-deploy-workflow.md#development-workflow), skapa utvecklingsgrenar baserat på `Integration` gren.

**Skapa en utvecklingsgren**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Skapa en miljö baserad på den gren som rekommenderas för ditt projektarbetsflöde.

   ```bash
   magento-cloud branch <new-environment-name> integration
   ```

1. Uppdatera beroenden.

   ```bash
   composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
   ```

1. [_valfri_] Skapa en [säkerhetskopia](../storage/snapshots.md) av miljön.

### Sammanfoga en gren

När du är klar med utvecklingen sammanfogar du den här grenen med den överordnade:

1. Verkställ och push-kodsändringar:

   ```bash
   git add -A && git commit -m "Add message here"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Sammanfoga med den överordnade miljön:

   ```bash
   magento-cloud environment:merge <environment-ID>
   ```

### Ta bort en miljö

Ta bara bort en miljö om du är säker på att du inte längre behöver den. Du kan inte återställa en miljö efter att du har tagit bort den.

>[!WARNING]
>
>Du kan inte ta bort `master` del av ett projekt.

Du måste vara projektadministratör, miljöadministratör eller kontoägare för att kunna utföra den här åtgärden. Se [Hantera användaråtkomst till molnprojekt](../project/user-access.md).

När du tar bort en miljö ställs miljön in på _inaktiv_. Koden är fortfarande tillgänglig i Git-grenen, men innehåller inte längre tjänsterna eller databasen. Om du vill ta bort miljön helt måste du även ta bort motsvarande Git-fjärrgren.

**Ta bort en miljö**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Hämta uppdateringar från fjärrservern.

   ```bash
   git fetch
   ```

1. Ta bort miljögrenen.

   ```bash
   magento-cloud environment:delete <environment-ID>
   ```

   Du kan också ta bort mer än en miljö åt gången genom att lägga till flera miljö-ID:n i kommandot delete.

   ```bash
   magento-cloud environment:delete <environment-1-ID> <environment-2-ID>
   ```

1. Svara på uppmaningarna att ta bort den lokala miljön och motsvarande fjärrmiljö.

   ```terminal
   The environment <environment-ID> is currently active: deleting it will delete all associated data.
   Are you sure you want to delete the environment <environment-ID>? [Y/n]
   ```

   Om du tar bort miljön placeras den i en _inaktiv_ tillstånd.

   ```terminal
   Delete the remote Git branch too? [Y/n]
   ```

   Om du tar bort Git-fjärrgrenen tas miljön bort från projektet.

1. Vänta tills miljön har tagits bort.

   ```terminal
   Deleting environment <environment-ID>
   Waiting for the activity...
     Deleting environment <project-id>-<environment-ID>-xxxxxx
   
     [============================]  1 min (complete)
   Activity ID succeeded
   Deleted remote Git branch <environment-ID>
   Run git fetch --prune to remove deleted branches from your local cache.
   ```

>[!TIP]
>
>Använd `magento-cloud environment:activate` -kommando.

## Interagera med fjärrmiljöer

Efter dig [konfigurera SSH-nycklar](../development/secure-connections.md)kan du [ansluta från din lokala arbetsyta till en fjärrmiljö](../development/secure-connections.md#connect-to-a-remote-environment) och interagera med projekttjänsterna och ändra inställningarna.
