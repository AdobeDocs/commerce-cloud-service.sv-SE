---
title: Autentiseringsnycklar
description: Lär dig hur du använder autentiseringsnycklar i ett utvecklingsprojekt i Adobe Commerce i molninfrastruktur.
feature: Cloud, Security
topic: Security
exl-id: b05cd4c2-0804-49c8-980a-4c7b6932082b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Autentiseringsnycklar

Du måste ha en autentiseringsnyckel för att få tillgång till Adobe Commerce-databasen och för att kunna aktivera installations- och uppdateringskommandon för ditt Adobe Commerce i molninfrastrukturprojekt. Det finns två metoder för att ange autentiseringsuppgifter för Composer-autentisering.

- **autentiseringsfil**—En fil som innehåller din Adobe Commerce [autentiseringsuppgifter](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/authentication-keys.html) i Adobe Commerce i molninfrastrukturens rotkatalog.
- **miljövariabel**- En miljövariabel som konfigurerar autentiseringsnycklar i ditt Adobe Commerce-infrastrukturprojekt för att förhindra oavsiktlig exponering.

>[!BEGINSHADEBOX]

**Säkerhetsanvisning**

Adobe rekommenderar att du använder [miljövariabel](#composer-auth-environment-variable) i ditt molnprojekt för att förhindra oavsiktlig exponering av dina autentiseringsuppgifter.

Metoden för autentiseringsfilen är idealisk när du använder Cloud Docker för Commerce som ett lokalt utvecklingsverktyg, men var noga med att inte överföra `auth.json` till en offentlig Git-baserad databas. Du kan lägga till `auth.json` till [`.gitignore` fil](../project/file-structure.md#ignoring-files).

>[!ENDSHADEBOX]

## Autentiseringsfil

**Skapa en `auth.json` fil**:

1. Om du inte har en `auth.json` i projektets rotkatalog, skapa en.

   - Skapa en `auth.json` i projektets rotkatalog.
   - Kopiera innehållet i [exempel `auth.json`](https://github.com/magento/magento2/blob/2.3/auth.json.sample) till nya `auth.json` -fil.

1. Ersätt `<public-key>` och `<private-key>` med dina inloggningsuppgifter för Adobe Commerce.

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. Spara ändringarna och avsluta textredigeraren.

## Miljövariabel för Composer-autentisering

Följande metod är det bästa sättet att förhindra oavsiktlig exponering av känsliga uppgifter i en offentlig Git-baserad databas.

**Lägga till autentiseringsnycklar med en miljövariabel**:

1. I _[!DNL Cloud Console]_klickar du på konfigurationsikonen till höger om projektnavigeringen.

   ![Konfigurera projekt](../../assets/icon-configure.png){width="36"}

1. I _Projektinställningar_ lista, klicka på **[!UICONTROL Variables]**.

1. Klicka på **[!UICONTROL Create variable]**.

1. I **[!UICONTROL Variable name]** fält, ange `env:COMPOSER_AUTH`.

1. I _Värde_ lägg till följande och ersätt `<public-key>` och `<private-key>` med dina inloggningsuppgifter för Adobe Commerce:

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. Välj **[!UICONTROL Available during buildtime]** och avmarkera **[!UICONTROL Available during runtime]**.

1. Klicka på **[!UICONTROL Create variable]**.

1. Ta bort `auth.json` fil från varje miljö.
