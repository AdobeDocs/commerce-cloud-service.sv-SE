---
title: Återställa en miljö
description: Lär dig hur du avinstallerar Adobe Commerce-programmet från ett molninfrastrukturprojekt och återställer en miljö till ett stabilt tillstånd.
role: Developer
topic: Development
exl-id: b76bd6c3-986e-4adc-abd0-5b27db0d8a3b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Återställa en miljö

Om du stöter på problem i integreringsmiljön och inte har en [giltig säkerhetskopia](../storage/snapshots.md)provar du att återställa miljön på något av följande sätt:

- Återställ eller återställa koden i Git-grenen
- Avinstallera [!DNL Commerce] program
- Tvinga omdistribution
- Återställ databasen manuellt

{{stuck-deployment-tip}}

## Återställ Git-grenen

Om du återställer Git-grenen återställs koden till ett stabilt läge tidigare.

**Återställ din gren**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Granska implementeringshistoriken för Git. Använd `--oneline` om du vill visa förkortade implementeringar på en rad:

   ```bash
   git log --oneline
   ```

   Exempelsvar:

   ```terminal
   6bf9f45 (HEAD -> master, magento/master, magento/develop, magento/HEAD, develop) Create composer.lock
   34d7434 2.4.6 upgrade
   b69803c Update composer.lock
   c1bca24 Add sample data
   ec604c3 Update magento/ece-tools
   ...
   ```

1. Välj en implementeringshash som representerar det senast kända stabila läget för koden.

   Om du vill återställa din gren till det ursprungliga initierade läget söker du efter den första implementeringen som har skapat din gren. Du kan använda `--reverse` för att visa historik i omvänd kronologisk ordning.

1. Använd alternativet för hårddiskåterställning för att återställa din gren. Var försiktig med det här kommandot eftersom alla ändringar sedan den valda implementeringen ignoreras.

   ```bash
   git reset --hard <commit>
   ```

1. Gör ändringarna och utlösa en omdistribution som installerar om Adobe Commerce.

   ```bash
   git push --force <origin> <branch>
   ```

## Avinstallera Commerce

Avinstallerar [!DNL Commerce] programmet återställer miljön till ett ursprungligt tillstånd genom att återställa databasen, ta bort distributionskonfigurationen och rensa `var/` underkataloger. Den här vägledningen återställer också Git-grenen till ett tidigare stabilt läge. Om du inte har en nyligen använd säkerhetskopia, men kan komma åt fjärrmiljön med SSH, följer du de här stegen för att återställa miljön:

- Inaktivera konfigurationshantering
- Avinstallera Adobe Commerce
- Återställ Git-grenen

Om du avinstallerar Adobe Commerce tas databasen bort och återställs, distributionskonfigurationen tas bort och `var/` underkataloger. Det är viktigt att inaktivera [Konfigurationshantering](../store/store-settings.md) så att de tidigare konfigurationsinställningarna inte tillämpas automatiskt vid nästa distribution. Se till att `app/etc/` katalogen innehåller inte `config.php` -fil.

**Avinstallera Adobe Commerce**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Använd SSH för att logga in i fjärrmiljön.

   ```bash
   magento-cloud ssh
   ```

1. Ta bort konfigurationsfilen.
   - För Adobe Commerce 2.2 och senare:

     ```bash
     rm app/etc/config.php
     ```

   - För Adobe Commerce 2.1:

     ```bash
     rm app/etc/config.local.php
     ```

1. Avinstallera Adobe Commerce.

   ```bash
   php bin/magento setup:uninstall -n
   ```

1. Bekräfta att Adobe Commerce har avinstallerats.

   Följande meddelande visas för att bekräfta att avinstallationen lyckades:

   ```terminal
   [SUCCESS]: Magento uninstallation complete.
   ```

1. Rensa `var/` underkataloger.

   ```bash
   rm -rf var/*
   ```

1. Logga ut.

>[!TIP]
>
>Det kan också vara bra att rengöra byggcacheminnen.
>
>```bash
>magento-cloud project:clear-build-cache
>```

## Tvinga omdistribution

Om du har försökt avinstallera Adobe Commerce och distributionen fortsätter att misslyckas kan du försöka tvinga en omdistribution manuellt.

```bash
git commit --allow-empty -m "<message>" && git push <origin> <branch>
```

## Återställ databasen

Om du har försökt avinstallera Adobe Commerce och kommandot misslyckades eller inte kunde slutföras kan du återställa databasen manuellt.

**Återställ databasen**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Använd SSH för att logga in i fjärrmiljön.

   ```bash
   magento-cloud ssh
   ```

1. Anslut till databasen.

   ```bash
   mysql -h database.internal
   ```

1. Släpp `main` databas.

   ```shell
   drop database main;
   ```

1. Skapa en tom `main` databas.

   ```shell
   create database main;
   ```

1. Ta bort följande konfigurationsfiler.

   - `config.php`
   - `config.php.bak`
   - `env.php`
   - `env.php.bak`

1. Logga ut och utlösa en omdistribution.

   ```bash
   magento-cloud environment:redeploy
   ```

{{redeploy-warning}}
