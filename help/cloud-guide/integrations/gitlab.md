---
title: GitLab-integrering
description: Lär dig hur du integrerar ditt Adobe Commerce i ett molninfrastrukturprojekt med GitLab.
feature: Cloud, Integration
exl-id: 37fda8a0-7274-422f-9049-243f2e409f26
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# GitLab-integrering

Du kan konfigurera en GitLab-databas så att den automatiskt genererar och distribuerar en miljö när du skickar kodändringar. Den här integreringen synkroniserar din GitLab-databas med ditt Adobe Commerce på molninfrastrukturskontot.

{{private-repository}}

Integreringen gör att du kan:

- Skapa en miljö när du skapar en gren
- Distribuera om miljön när du sammanfogar en pull-begäran
- Ta bort miljön när du tar bort grenen

Du måste hämta en GitLab-token och en webkrok för att kunna fortsätta processen.

## Förutsättningar

- Administratörsåtkomst till Adobe Commerce i molninfrastrukturprojektet
- [`magento-cloud` CLI](../dev-tools/cloud-cli-overview.md) verktyg i din lokala miljö
- Ett GitLab-konto
- En personlig GitLab-åtkomsttoken med skrivåtkomst till GitLab-databasen. De valda omfattningarna måste vara minst: `api` och `read_repository`.

## Förbered databasen

Klona ditt Adobe Commerce i molninfrastrukturprojekt från en befintlig miljö och migrera projektgrenarna till en ny, tom GitLab-databas, med samma filialnamn intakta. Det är **kritisk** för att behålla ett identiskt Git-träd, så att du inte förlorar några befintliga miljöer eller grenar i ditt Adobe Commerce i molninfrastrukturprojekt.

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
   magento-cloud project:get <project-id>
   ```

1. Lägg till din GitLab-databas som en fjärrdatabas (förutsatt att GitLab används i SaaS-versionen).

   ```bash
   git remote add origin git@gitlab.com:<user-name>/<repo-name>.git
   ```

   Standardnamnet för fjärranslutningen kan vara `origin` eller `magento`. If `origin` finns kan du välja ett annat namn eller så kan du byta namn på eller ta bort den befintliga referensen. Se [git-remote-dokumentation](https://git-scm.com/docs/git-remote).

1. Kontrollera att du har lagt till GitLab-fjärrkontrollen korrekt.

   ```bash
   git remote -v
   ```

   Förväntat svar:

   ```terminal
   origin git@gitlab.com:<user-name>/<repo-name>.git (fetch)
   origin git@gitlab.com:<user-name>/<repo-name>.git (push)
   ```

1. Skicka projektfilerna till din nya GitLab-databas. Kom ihåg att behålla samma namn på alla grenar.

   ```bash
   git push -u origin master
   ```

   Om du börjar med en ny GitLab-databas kan du behöva använda `-f` eftersom fjärrdatabasen inte matchar din lokala kopia.

1. Kontrollera att din GitLab-databas innehåller alla dina projektfiler.

## Aktivera GitLab-integrering

Använd `magento-cloud integration` för att aktivera GitLab-integrering och hämta Payload URL för GitLab-webkroken för att skicka uppdateringar från GitLab till ditt Adobe Commerce i molninfrastrukturprojekt.

```bash
magento-cloud integration:add --type=gitlab --project=<project-ID> --token=<your-GitLab-token> [--base-url=<GitLab-url> --server-project=<GitLab-project> --build-merge-requests={true|false} --merge-requests-clone-parent-data={true|false} --fetch-branches={true|false} --prune-branches={true|false}]
```

| Alternativ | Beskrivning |
| ------ | ----------- |
| `<project-ID>` | Ditt projekt-ID för Adobe Commerce i molnet |
| `<your-GitLab-token>` | Den personliga åtkomsttoken som du genererade för GitLab |
| `--base-url` | URL för GitLab (`https://gitlab.com/` om GitLab används i sin SaaS-version) |
| `--server-project` | Projektnamn i GitLab (del efter bas-url) |
| `--build-merge-requests` | An _valfri_ parameter som instruerar Adobe Commerce om molninfrastruktur att skapa en ny miljö för varje kopplingsbegäran (`true` som standard) |
| `--merge-requests-clone-parent-data` | An _valfri_ parameter som instruerar Adobe Commerce om molninfrastruktur att klona den överordnade miljöns data för sammanfogningsbegäranden (`true` som standard) |
| `--fetch-branches` | An _valfri_ parameter som gör att Adobe Commerce i molninfrastrukturen hämtar alla grenar från fjärrservern (som inaktiva miljöer) (`true` som standard) |
| `--prune-branches` | An _valfri_ parameter som instruerar Adobe Commerce om molninfrastruktur att ta bort grenar som inte finns på fjärrkontrollen (`true` som standard) |

>[!WARNING]
>
>The `magento-cloud integration` kommandoöverskrivningar _alla_ koda i ditt Adobe Commerce i molninfrastrukturprojekt med koden från din GitLab-databas. Detta omfattar alla filialer, inklusive `production` gren. Den här åtgärden utförs omedelbart och kan inte ångras. Det är en god vana att klona alla dina grenar från Adobe Commerce i molninfrastrukturprojekt och överföra dem till din GitLab-databas innan du lägger till GitLab-integreringen.

**Aktivera GitLab-integrering**:

1. Från terminalen lägger du till GitLab-integreringen i ditt Adobe Commerce i molninfrastrukturprojekt:

   ```bash
   magento-cloud integration:add --type gitlab --project=3txxjf32gtryos --token=qVUfeEn4ouze7A7JH --base-url=https://gitlab.com/ --server-project=my-agency/project-name --build-merge-requests=false --merge-requests-clone-parent-data=false --fetch-branches=true --prune-branches=true
   ```

1. När du uppmanas till det anger du `y` för att lägga till integreringen.

   ```terminal
   Warning: adding a 'gitlab' integration will automatically synchronize code from the external Git repository.
   This means it can overwrite all the code in your project.
   Are you sure you want to continue? [y/N] y
   ```

1. Kopiera **URL för krok** visas som returutdata.

   ```terminal
   Hook URL: https://eu-3.magento.cloud/api/projects/3txxjf32gtryos/integrations/eolmpfizzg9lu/hook
   Created integration eolmpfizzg9lu (type: gitlab)
   +----------------------------------+---------------------------------------------------------------------------------------+
   | Property                         | Value                                                                                 |
   +----------------------------------+---------------------------------------------------------------------------------------+
   | id                               | <integration-id>                                                                      |
   | type                             | gitlab                                                                                |
   | token                            | ******                                                                                |
   | base_url                         | https://gitlab.com/                                                                   |
   | project                          | my-agency/project-name                                                                |
   | fetch_branches                   | true                                                                                  |
   | prune_branches                   | true                                                                                  |
   | build_merge_requests             | false                                                                                 |
   | merge_requests_clone_parent_data | false                                                                                 |
   | hook_url                         | https://eu-3.magento.cloud/api/projects/<project-id>/integrations/<integration-id>/hook |
   +----------------------------------+---------------------------------------------------------------------------------------+
   ```

### Lägg till webkroken i GitLab

För att kunna kommunicera händelser - som push- eller merge-begäranden - med din Creative Cloud Git-server måste du [skapa en webkrok](https://docs.gitlab.com/ee/user/project/integrations/webhooks.html#overview) för din GitLab-databas

1. Klicka på **Inställningar** -fliken.

1. Klicka på i det vänstra navigeringsfältet **Webhooks**.

1. I _Webhooks_ kan du redigera följande fält:

   - **URL**: Ange `Hook URL` returneras när du aktiverat GitLab-integreringen.
   - **Hemlig token**: Ange en verifieringshemlighet om det behövs.
   - **Utlösare**: Kontrollera `Merge request events` och/eller `Push events` beroende på dina behov.
   - **Aktivera SSL-verifiering**: Du måste välja det här alternativet.

1. Klicka **Lägg till webkrok**.

### Testa integreringen

När du har konfigurerat GitLab-integreringen kan du verifiera att integreringen fungerar med `magento-cloud` CLI:

```bash
magento-cloud integration:validate
```

Du kan också testa den genom att göra en enkel ändring i din GitLab-databas.

1. Skapa en testfil.

   ```bash
   touch test.md
   ```

1. Verkställ och skicka ändringen till din GitLab-databas.

   ```bash
   git add . && git commit -m "Testing GitLab integration" && git push
   ```

1. Logga in på [[!DNL Cloud Console]](../project/overview.md) och verifiera att ditt implementeringsmeddelande visas och att ditt projekt distribueras.

## Skapa en molngren

Använd `magento-cloud` CLI `environment:push` för att skapa och aktivera en ny miljö. Se [Skapa en molngren](bitbucket.md#create-a-cloud-branch).

## Ta bort integreringen

Använd `magento-cloud` CLI `integration:delete` för att ta bort integreringen. Se [Ta bort integreringen](bitbucket.md#remove-the-integration).
