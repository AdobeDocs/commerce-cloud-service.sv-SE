---
title: Miljövariabler
description: Se en lista över miljövariabler som är specifika för Adobe Commerce om molninfrastruktur.
feature: Cloud, Build, Configuration, Deploy
exl-id: bfee2f69-93a6-4d26-bb9e-be8acc5673c3
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Miljövariabler

Med Adobe Commerce i molninfrastruktur kan du tilldela miljövariabler för att åsidosätta konfigurationsalternativen. The `ece-tools` paket anger värden i `env.php` fil baserad på värden från [Molnvariabler](variables-cloud.md), variabler som anges i [!DNL Cloud Console]och `.magento.env.yaml` konfigurationsfil.

Miljövariablerna i `.magento.env.yaml` anpassa molnmiljön genom att åsidosätta din befintliga Commerce-konfiguration. Om ett standardvärde är `Not Set`och sedan `ece-tools` paket **NEJ** och använder [!DNL Commerce] standard eller värdet från `MAGENTO_CLOUD_RELATIONSHIPS` konfiguration. Om standardvärdet är inställt visas `ece-tools` paketet fungerar för att ange den standardinställningen.

Typerna av miljövariabler är bland annat:

- [ADMIN](variables-admin.md)—variables override project ADMIN variables
- [MAGENTO_CLOUD](variables-cloud.md)—variabler som är specifika för molninfrastrukturen
- Variabler i `.magento.env.yaml` fil:
   - [Global](variables-global.md)—variabler påverkar bygg-, distributions- och postdriftsättningsfaser
   - [Bygge](variables-build.md)—variabelkontrollbygge
   - [Distribuera](variables-deploy.md)—variabelstyrningsdistributionsåtgärder
   - [Efter driftsättning](variables-post-deploy.md)—variabelkontrollåtgärder efter distributionen

Variabler är _hierarkisk_, vilket innebär att om en variabel inte åsidosätts ärvs den från den överordnade miljön.

Du kan ange [ADMIN-variabler](variables-admin.md) från [!DNL Cloud Console] eller med Adobe Commerce CLI. Du kan hantera andra miljövariabler från [`.magento.env.yaml`](configure-env-yaml.md) -fil för att hantera byggåtgärder och driftsättningsåtgärder i alla miljöer - inklusive Pro Staging och Production - utan att behöva ett supportärende.

>[!TIP]
>
>YAML-filer är skiftlägeskänsliga och tillåter inte tabbar. Var noga med att använda konsekvent indrag i hela `.magento.env.yaml` filen eller konfigurationen kanske inte fungerar som förväntat. Exemplen i den här dokumentationen och i exempelfilen använder _två blanksteg_ indrag. Använd [ece-tools validate, kommando](configure-env-yaml.md#validate-configuration-file) för att kontrollera konfigurationen.
