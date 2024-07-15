---
title: Konfigurera programdistribution
description: Lär dig hur du konfigurerar egenskaperna i programkonfigurationsfilen som styr hur programmet  [!DNL Commerce] skapar och distribuerar till molnmiljön.
feature: Cloud, Configuration, Build, Deploy
exl-id: 900da20d-98d2-4c9f-97ec-578aee775b55
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Konfigurera programdistribution

Filen `.magento.app.yaml` styr hur programmet byggs och distribueras. Även om Adobe Commerce i molninfrastruktur har stöd för flera program per projekt, har ett projekt vanligtvis ett program med filen `.magento.app.yaml` i roten av databasen.

`.magento.app.yaml` har många standardvärden, se [en exempelfil `.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml). Granska alltid `.magento.app.yaml` för din installerade version. Den här filen kan skilja sig åt mellan olika versioner av Adobe Commerce för molninfrastruktur.

Använd filen `.magento.app.yaml` för att definiera följande konfigurationsvärden:

- [Egenskaper](properties.md) - Definiera egenskapsvärden för programinstansen.
- [Variabler, egenskap](variables-property.md) - Granska miljövariabler som krävs för programversionen [!DNL Commerce].
- [PHP-inställningar](php-settings.md) - Konfigurera PHP-alternativ för körning.
- [Ange cache för statiska filer](set-cache.md) - Ange cache-TTL för dina media och statiska filer.
