---
title: GitHub-integrering
description: Lär dig hur du integrerar ditt Adobe Commerce i ett molninfrastrukturprojekt med GitHub.
feature: Cloud, Integration
last-substantial-update: 2023-05-25T00:00:00Z
exl-id: 5305452f-4c8d-438c-ac78-e2e1ec2f8cd9
source-git-commit: 4d32fc596064f01eaefe3ee509a655837fa846de
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# GitHub-integrering

Tack vare GitHub-integreringen kan du hantera dina Adobe Commerce i molninfrastrukturmiljöer direkt från din GitHub-databas. Integreringen hanterar innehåll som redan finns i GitHub och synkroniserar med Adobe Commerce i molninfrastrukturens kodarkiv. Koddatabasen blir alltså en spegling av GitHub-databasen.

{{private-repository}}

Integreringen gör att du kan:

- Skapa en miljö när du skapar en gren
- Distribuera om miljön när du sammanfogar en pull-begäran
- Ta bort miljön när du tar bort grenen

Du måste hämta en GitHub-token och en webkrok för att kunna fortsätta processen.

## Förutsättningar

- Administratörsåtkomst till Adobe Commerce i molninfrastrukturprojektet
- GitHub-databas
- Personlig åtkomsttoken för GitHub

## Generera en GitHub-token

Skapa en klassisk token för personlig åtkomst i inställningarna för GitHub-utvecklare. Du måste vara medlem i en grupp med skrivåtkomst till GitHub-databasen så att du kan _push_ till databasen. Inkludera följande scope när du skapar din token:

- `admin:repo_hook`—Skapa webbhotell
- `repo`—Integrera med databasen
- `read:org`- Integrera med er organisationsdatabas

Se [GitHub: Skapa](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

## Förbered databasen

Klona ditt Adobe Commerce i molninfrastrukturprojekt från en befintlig miljö och migrera projektgrenarna till en ny, tom GitHub-databas, med samma filialnamn intakta. Det är **kritisk** för att behålla ett identiskt Git-träd, så att du inte förlorar några befintliga miljöer eller grenar i ditt Adobe Commerce i molninfrastrukturprojekt.

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

1. Lägg till din GitHub-databas som en fjärrdatabas.

   ```bash
   git remote add origin git@github.com:<user-name>/<repo-name>.git
   ```

   Standardnamnet för fjärranslutningen kan vara `origin` eller `magento`. If `origin` finns kan du välja ett annat namn eller så kan du byta namn på eller ta bort den befintliga referensen. Se [git-remote-dokumentation](https://git-scm.com/docs/git-remote).

1. Kontrollera att du har lagt till GitHub-fjärrkontrollen korrekt.

   ```bash
   git remote -v
   ```

   Förväntat svar:

   ```terminal
   origin git@github.com:<user-name>/<repo-name>.git (fetch)
   origin git@github.com:<user-name>/<repo-name>.git (push)
   ```

1. Skicka projektfilerna till din nya GitHub-databas. Kom ihåg att behålla samma namn på alla grenar.

   ```bash
   git push -u origin master
   ```

   Om du börjar med en ny GitHub-databas kan du behöva använda `-f` eftersom fjärrdatabasen inte matchar din lokala kopia.

1. Kontrollera att din GitHub-databas innehåller alla dina projektfiler.

## Aktivera GitHub-integrering

Innan du börjar måste projektkoden och miljöerna finnas i GitHub-databasen. När integreringen har aktiverats blir GitHub-databasen kodkälla. Om du trycker på koden ändras den till originalet `magento` -databasen skrivs den över av integreringen när du skickar kodändringar till din GitHub-databas.

Följande aktiverar GitHub-integreringen och tillhandahåller en Payload URL som kan användas när en webkrok skapas.

>[!WARNING]
>
>Följande kommando skriver över _alla_ kod i ditt Adobe Commerce i molninfrastrukturprojekt med kod från din GitHub-databas, som innehåller alla grenar, inklusive `production` gren. Den här åtgärden utförs omedelbart och kan inte ångras. Det är en god vana att klona alla dina grenar från Adobe Commerce i molninfrastrukturprojekt och överföra dem till din GitHub-databas **före** lägga till GitHub-integrering.

Du kan gå igenom CLI-instruktionerna med `magento-cloud integration:add` eller så kan du bygga integrationskommandot med följande alternativ:

| Alternativ | Obligatoriskt? | Beskrivning |
| ----------------------- | --------- | --------------------------------- |
| `--base-url` | Ja | Bas-URL för serverinstallationen, som kan vara `https://github.com/` eller en egen. Utelämna det här alternativet om din databas ligger hos Github. |
| `--token` | Ja | Den personliga åtkomsttoken som du genererade för GitHub |
| `--repository` | Ja | Databasnamnet: `owner-or-organisation/repository` |
| `--build-pull-requests` | Valfritt | Instruerar Adobe Commerce på molninfrastruktur att distribueras när du har sammanfogat en pull-begäran (`true` som standard) |
| `--fetch-branches` | Valfritt | Gör att Adobe Commerce i molninfrastrukturen spårar grenar och distribueras efter att du har uppdaterat en gren (`true` som standard) |
| `--prune-branches` | Valfritt | Ta bort grenar som inte finns på fjärrkontrollen (`true` som standard) |

Det finns många fler alternativ och du kan se dem med hjälp av hjälpalternativet:

```bash
magento-cloud integration:add --help
```

**Aktivera GitHub-integrering**:

1. Aktivera integreringen.

   ```bash
   magento-cloud integration:add --type=github --project=<project-ID> --token=<your-GitHub-token> {--repository=USER/REPOSITORY | --repository=ORGANIZATION/REPOSITORY} [--build-pull-requests={true|false} --fetch-branches={true|false}
   ```

   **Exempel 1**: Aktivera GitHub-integrering för en personlig, privat databas:

   ```bash
   magento-cloud integration:add --type=github --project=ov58dlacU2e --base-url=https://github.com --token=<token> --repository=myUserName/myrepo
   ```

   **Exempel 2**: Aktivera GitHub-integrering för en organisationsdatabas:

   ```bash
   magento-cloud integration:add --type=github --project=ov58dlacU2e --base-url=https://github.com --token=<token> --repository=Magento/teamrepo
   ```

1. Ange den obligatoriska informationen när du uppmanas till det.

1. Kopiera **URL för nyttolast** visas som returutdata.

   ```terminal
   Created integration <integration-ID> (type: github)
   Repository: myUserName/myrepo
   Build PRs: yes
   Fetch branches: yes
   Payload URL: https://us.magento.cloud/api/projects/<project-id>/integrations/wO8a0eoamxwcg/hook
   ```

## Lägg till webkroken i GitHub

Om du vill kommunicera händelser, t.ex. en push-funktion, med din Creative Cloud Git-server måste du skapa en webkrok för din GitHub-databas:

1. Klicka på **Inställningar** -fliken.

1. Klicka på i det vänstra navigeringsfältet **Webhooks**.

1. I _Webhooks_ ruta, klicka **Lägg till webkrok**.

1. I _Webhooks/Lägg till webkrok_ kan du redigera följande fält:

   - **URL för nyttolast**: Ange den URL som returneras när du aktiverade GitHub-integreringen.
   - **Innehållstyp**: Välj **application/json** från listan.
   - **Hemlighet**: Ange en verifieringshemlighet.
   - **Vilka händelser vill du utlösa den här webbkroken?**: Välj **Skicka mig allt**.
   - Välj **Aktiv** kryssrutan.

1. Klicka **Lägg till webkrok**.

## Testa integreringen

När du har konfigurerat GitHub-integreringen kan du verifiera att integreringen fungerar med `magento-cloud` CLI:

```bash
magento-cloud integration:validate
```

Du kan också testa den genom att göra en enkel ändring i din GitHub-databas.

1. Skapa en testfil.

   ```bash
   touch test.md
   ```

1. Verkställ och skicka ändringen till din GitHub-databas.

   ```bash
   git add . && git commit -m "Testing GitHub integration" && git push
   ```

1. Logga in på [[!DNL Cloud Console]](../project/overview.md) och verifiera att ditt implementeringsmeddelande visas och att ditt projekt distribueras.

## Ta bort integreringen

Du kan ta bort GitHub-integreringen från ditt projekt utan att koden påverkas.

**Ta bort GitHub-integreringen**:

1. Logga in på ditt Adobe Commerce i molninfrastrukturprojekt från terminalen.

1. Visa en lista över era integreringar. Du behöver GitHub-integrerings-ID för att kunna slutföra nästa steg.

   ```bash
   magento-cloud integration:list
   ```

1. Ta bort integreringen.

   ```bash
   magento-cloud integration:delete <int-ID>
   ```

Du kan även ta bort GitHub-integreringen genom att logga in på ditt GitHub-konto och ta bort webbokroken i _Webhooks_ databasflik _Inställningar_.
