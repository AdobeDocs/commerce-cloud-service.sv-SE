---
title: Konfigurera programdistribution
description: Lär dig hur du konfigurerar egenskaperna i programkonfigurationsfilen som styr hur [!DNL Commerce] programmet bygger och distribuerar till molnmiljön.
feature: Cloud, Configuration, Build, Deploy
exl-id: 900da20d-98d2-4c9f-97ec-578aee775b55
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Konfigurera programdistribution

The `.magento.app.yaml` -filen styr hur programmet byggs och distribueras. Även om Adobe Commerce i molninfrastruktur har stöd för flera program per projekt har ett projekt vanligtvis en enda applikation med `.magento.app.yaml` -filen i databasens rot.

The `.magento.app.yaml` har många standardvärden, se [ett exempel `.magento.app.yaml` fil](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml). Granska alltid `.magento.app.yaml` för den installerade versionen. Den här filen kan skilja sig åt mellan olika versioner av Adobe Commerce för molninfrastruktur.

Använd `.magento.app.yaml` fil för att definiera följande konfigurationsvärden:

- [Egenskaper](properties.md)—Definiera egenskapsvärden för programinstansen.
- [Variables, egenskap](variables-property.md)—Granska systemvariabler som krävs för [!DNL Commerce] programversion.
- [PHP-inställningar](php-settings.md)—Konfigurera PHP-alternativ för körning.
- [Ange cache för statiska filer](set-cache.md)—Ange cache TTL för dina media och statiska filer.
