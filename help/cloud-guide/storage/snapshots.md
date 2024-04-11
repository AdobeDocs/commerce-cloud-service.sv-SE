---
title: Hantering av säkerhetskopiering
description: Lär dig hur du manuellt skapar och återställer en säkerhetskopia för ditt Adobe Commerce i molninfrastrukturprojekt.
feature: Cloud, Paas, Snapshots, Storage
exl-id: 1cb00db7-2375-4761-9c07-1e20a74859e0
source-git-commit: 069cbc233492d22932e8dce5bf0426dce8459727
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# Hantering av säkerhetskopiering

Du kan när som helst utföra en manuell säkerhetskopiering av aktiva startmiljöer med **[!UICONTROL Backup]** knappen i [!DNL Cloud Console] eller med `magento-cloud snapshot:create` -kommando.

En säkerhetskopia eller _ögonblicksbild_ är en fullständig säkerhetskopiering av miljödata som innehåller alla beständiga data från tjänster som körs (MySQL-databas) och alla filer som lagras på de monterade volymerna (var, pub/media, app/etc). Ögonblicksbilden gör _not_ inkludera kod, eftersom koden redan lagras i den Git-baserade databasen. Du kan inte hämta en kopia av en ögonblicksbild.

Funktionen för säkerhetskopiering/fixering gör **not** gäller för Pro Staging and Production-miljöer, som som standard får regelbundna säkerhetskopieringar för katastrofåterställning. Se [Säkerhetskopiering och katastrofåterställning för Pro](../architecture/pro-architecture.md#backup-and-disaster-recovery) för mer information. Till skillnad från automatiska direktsäkerhetskopieringar i Pro Staging- och Production-miljöer är det **not** automatisk. Det är _din_ ansvar för att manuellt skapa en säkerhetskopia eller konfigurera ett cron-jobb för att regelbundet skapa en säkerhetskopia av dina integreringsmiljöer i Starter eller Pro.

## Skapa manuell säkerhetskopiering

Du kan skapa en manuell säkerhetskopia av alla aktiva Starter-miljöer och integreringstjänstmiljö från [!DNL Cloud Console] eller skapa en ögonblicksbild från Cloud CLI. Du måste ha en [Administratörsroll](../project/user-access.md) för miljön.

**Skapa en säkerhetskopia av valfri Starter-miljö med[!DNL Cloud Console]**:

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Välj en miljö i projektnavigeringsfältet. Miljön måste vara aktiv.
1. I _Säkerhetskopior_ visa, klicka **[!UICONTROL Backup]**. Det här alternativet är inte tillgängligt för en Pro-miljö.

   ![Säkerhetskopiera](../../assets/button-backup.png){width="150"}

**Skapa en säkerhetskopia av en integreringsmiljö med[!DNL Cloud Console]**:

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Välj en integrerings-/utvecklingsmiljö i projektnavigeringsfältet. Miljön måste vara aktiv.
1. Välj **[!UICONTROL Backup]** i den övre högra menyn. Det här alternativet är tillgängligt för både Starter- och Pro-miljöer.
1. Klicka på **[!UICONTROL Yes]** -knappen.

**Skapa en ögonblicksbild med `magento-cloud` CLI**:

1. Byt till din projektkatalog på din lokala arbetsstation.
1. Kolla in miljögrenen för att ta en ögonblicksbild.
1. Skapa fixeringen.

   ```bash
   magento-cloud snapshot:create --live
   ```

   Du kan också använda `magento-cloud backup` kortkommando. The `--live` gör att miljön inte körs för att undvika driftavbrott. Om du vill se en fullständig lista över alternativen anger du `magento-cloud snapshot:create --help`.

   Exempelsvar:

   ```terminal
   Creating a snapshot of develop-branch
   Waiting for the activity ID (User created a backup of develop-branch):
   
   Creating backup of develop-branch
   Created backup my-snapshot
   [============================] 45 secs (complete)
   Activity ID succeeded
   Snapshot name: my-snapshot
   ```

1. Verifiera de senaste fixeringarna.

   ```bash
   magento-cloud snapshot:list
   ```

   Listan returnerar information om ögonblicksbildens status:

   ```terminal
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

## Återställa en manuell säkerhetskopia

Du måste ha [Administratörsåtkomst](../project/user-access.md) till miljön. Du har upp till **sju dagar** till _återställ_ manuell säkerhetskopiering. Koden för den aktuella Git-grenen ändras inte när du återställer en säkerhetskopia. Återställning av en säkerhetskopia på det här sättet gäller inte för testnings- och produktionsmiljöer i Pro. Se [Säkerhetskopiering och katastrofåterställning för Pro](../architecture/pro-architecture.md#backup-and-disaster-recovery).

Återställningstiden varierar beroende på databasens storlek:

- stor databas (200+ GB) kan ta 5 timmar
- en medelstor databas (150 GB) kan ta 2 1/2 timmar
- liten databas (60 GB) kan ta en timme

>[!TIP]
>
>Återställa utan säkerhetskopiering:
>
>- Om du vill återställa till föregående kod eller ta bort tillagda tillägg i en miljö läser du [Återställningskod](#roll-back-code).
>- Återställa en instabil miljö som _not_ har en säkerhetskopia, se [Återställa en miljö](../development/restore-environment.md).

**Så här återställer du en säkerhetskopia med[!DNL Cloud Console]**:

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Välj en miljö i projektnavigeringsfältet.
1. I _Säkerhetskopior_ välj en säkerhetskopia i _Lagrad_ lista. Säkerhetskopieringsfunktionen gör det **not** gäller för Pro-miljöerna.
1. I ![Mer](../../assets/icon-more.png){width="32"} (_mer_)-menyn, klicka **Återställ**.
1. Granska informationen för Återställ från säkerhetskopia och klicka på **Ja, återställ**.

**Återställa en ögonblicksbild med hjälp av molnet-CLI**:

1. Byt till din projektkatalog på din lokala arbetsstation.
1. Kolla in den miljögren som ska återställas.
1. Visa alla tillgängliga ögonblicksbilder.

   ```bash
   magento-cloud snapshot:list
   ```

   Listan returnerar information om tillgängliga ögonblicksbilder:

   ```terminal
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

1. Återställ en ögonblicksbild med ID för ögonblicksbild i listan.

   ```bash
   magento-cloud snapshot:restore <snapshot-id>
   ```

## Återställningskod

Säkerhetskopior och fixeringar gör det _not_ ta med en kopia av koden. Koden lagras redan i den Git-baserade databasen, så du kan använda Git-baserade kommandon för att återställa (återställa) kod. Använd till exempel `git log --oneline` för att bläddra igenom tidigare implementeringar och sedan använda [`git revert`](https://git-scm.com/docs/git-revert) för att återställa kod från en specifik implementering.

Du kan också välja att lagra kod i en _inaktiv_ gren. Skapa en gren med Git-kommandon i stället för att använda `magento-cloud` kommandon. Se om [Git-kommandon](../dev-tools/cloud-cli-overview.md#git-commands) i Cloud CLI-avsnittet.
