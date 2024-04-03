---
title: Aktivera B2B-modulen
description: Lär dig hur du aktiverar modulen business-to-business för Adobe Commerce i molninfrastrukturen.
feature: Cloud, B2B
exl-id: 01d02ea0-1e7d-4608-adbf-1dad7f5e2182
source-git-commit: bb7a866b1896a8a43d01ad3f83dc655bcf383374
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Aktivera B2B-modulen

Om era kunder är företag kan ni installera B2B for Adobe Commerce-modulen för att utöka ert Adobe Commerce i molnbaserade infrastrukturprojekt för att passa en affärsmodell. Även om det här avsnittet innehåller information om hur du installerar och konfigurerar B2B-modulen för Adobe Commerce i molninfrastrukturen finns det ytterligare B2B-information i följande handböcker:

- [Adobe Commerce B2B Developer Guide](https://developer.adobe.com/commerce/webapi/rest/b2b/)
- [Användarhandbok för Adobe Commerce B2B](https://experienceleague.adobe.com/docs/commerce-admin/b2b/guide-overview.html)

>[!TIP]
>
>Eftersom B2B är en modul för Adobe Commerce i molninfrastruktur rekommenderar Adobe att du distribuerar Adobe Commerce-programmet till en integrerings- eller mellanlagringsmiljö innan du börjar.

## Installera B2B-modulen

Adobe rekommenderar att du arbetar i en utvecklingsgren när du lägger till B2B-modulen i ditt projekt. Om du inte har någon gren kan du läsa [Skapa en gren för utveckling](../development/cli-branches.md#create-a-branch-for-development). När du installerar B2B-modulen `Magento_B2b` modulnamnet infogas automatiskt i `app/etc/config.php` -fil. Du behöver inte redigera filen direkt.

**Installera B2B-modulen**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Skapa eller checka ut en utvecklingsgren.

1. Lägg till B2B-modulen i `require` i `composer.json` -fil.

   ```bash
   composer require magento/extension-b2b --no-update
   ```

1. Uppdatera projektberoenden.

   ```bash
   composer update
   ```

1. Lägg till, implementera och push-ändra kod.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Install the B2B module."
   ```

   ```bash
   git push origin <branch-name>
   ```

1. När bygget och distributionen är klar loggar du in på fjärrmiljön med SSH och kontrollerar att B2B-modulen är installerad.

   ```bash
   bin/magento module:status Magento_B2b
   ```

   Ett tilläggsnamn har formatet: `<VendorName>_<ComponentName>`.

   Exempelsvar:

   ```terminal
   Magento_B2b : Module is enabled
   ```

   Om du råkar ut för distributionsfel finns mer information i [Återställning efter komponentfel](../deploy/recover-failed-deployment.md).

## Aktivera B2B-modulen

När du installerar B2B-modulen med Composer aktiveras modulen automatiskt i distributionsprocessen. Om du redan har B2B-modulen installerad kan du aktivera eller inaktivera modulen med CLI

Aktivera B2B-modulen:

```bash
bin/magento module:enable Magento_B2b
```

Exempelsvar:

```terminal
The following modules have been enabled:
- Magento_B2b

Cache cleared successfully.
Generated classes cleared successfully. Please run the 'setup:di:compile' command to generate classes.
Info: Some modules might require static view files to be cleared. To do this, run 'module:enable' with the --clear-static-content option to clear them.
```

Se [Hantera tillägg](extensions.md).

## Konfigurera B2B-modulen

När du har installerat modulen B2B för Adobe Commerce måste du [skapa budskap till konsumenterna](https://experienceleague.adobe.com/docs/commerce-admin/b2b/install.html#start-message-consumers) så att _Delad katalog_ och du måste [aktivera B2B-funktionerna](https://experienceleague.adobe.com/docs/commerce-admin/b2b/enable-basic-features.html).
