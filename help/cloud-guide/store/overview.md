---
title: Översikt över butiksalternativ och konfigurationshantering
description: Skräddarsy din Adobe Commerce-butik för molninfrastruktur.
feature: Cloud, Configuration, Services
exl-id: 06d477e4-02de-4742-8495-541458400e93
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# Översikt över butiksalternativ och konfigurationshantering

Det finns många sätt att anpassa din butik, till exempel genom att lägga till ett anpassat tema, installera ett tillägg eller använda en specifik konfiguration i olika miljöer i molnet. Du kan konfigurera inställningar för specifika tjänster direkt i mellanlagrings- och produktionsmiljöer. Du kan konfigurera flera webbplatser och butiker. Med Store-konfigurationen kan du konfigurera de här alternativen i din lokala arbetsstation och distribuera specifika inställningar i olika miljöer.

Om du vill få åtkomst till din butik använder du kommandot `magento-cloud url` och svarar på uppmaningarna. Du kan också hitta URL:en i [!DNL Cloud Console] under **Åtkomstwebbplatsen**.

## Konfigurera butiksalternativ

Butiksalternativen är följande:

* [Affärsmoduler (B2B)](b2b-module.md)
* [Egna teman](custom-theme.md)
* [Tillägg](extensions.md)
* [Flera platser](multiple-sites.md)
* [Betalningstjänster](paypal.md)

## Konfigurera tjänster och integreringar

Det finns specifika [konfigurationsfiler](../environment/overview.md) som hanterar vissa distributionsbeteenden till fjärrmiljöer. Du kan läsa dessa ämnen separat:

* [Programdistribution](../application/configure-app-yaml.md)
* [Åtgärder för att bygga och driftsätta miljöer](../environment/configure-env-yaml.md)
* [Inkommande förfrågningsvägar](../routes/routes-yaml.md)
* [Tjänster som stöds](../services/services-yaml.md)

## Konfigurationshantering

När du har konfigurerat butiksalternativ, tjänster och integreringar kan du använda konfigurationshantering för att distribuera dessa konfigurationer i alla miljöer på ett enhetligt sätt och med minimala driftavbrott. Se [Konfigurationshantering](store-settings.md).
