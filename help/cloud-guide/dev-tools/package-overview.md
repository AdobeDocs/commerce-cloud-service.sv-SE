---
title: '[!DNL ECE-Tools] Package'
description: Läs mer om [!DNL ECE-Tools] och hur det hjälper till att hantera och driftsätta Adobe Commerce.
exl-id: 5583a685-29c5-4de5-8d2e-94cff5ff37ab
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# ECE-verktygspaket

The [!DNL ECE-Tools] paketet är en uppsättning skript och verktyg som är utformade för att hantera och distribuera [!DNL Commerce] program. The `ece-tools` paket förenklar många processer, t.ex. hantering av cron-jobb, verifiering av projektkonfiguration och användning av Adobe-korrigeringar och snabbkorrigeringar. Du kan visa och bidra till [öppen källkod [!DNL ECE-Tools] kodarkiv på GitHub][ece-repo].

{{ece-tools-package}}

The `ece-tools` paketet är kompatibelt med Adobe Commerce - från och med version 2.1.4 - och innehåller skript och Adobe Commerce på molninfrastrukturskommandon som är utformade för att hantera koden och automatiskt bygga och driftsätta dina projekt.

Följande visar tillgängliga `ece-tools` kommandon:

```bash
php ./vendor/bin/ece-tools list
```

## Bygg och driftsätt

The `ece-tools` paketet innehåller kommandon för att utföra åtgärder för att skapa, distribuera och efterdistribuera faser i starten av ditt Adobe Commerce på molninfrastrukturprogram. Till exempel `php ./vendor/bin/ece-tools build` kommandot startar programbyggprocessen.

Som standard är dessa `ece-tools` kommandona finns i [hooks, egenskap](../application/hooks-property.md) i `.magento.app.yaml` konfigurationsfil.

## Dockningskonfigurationsgenerator

The `ece-tools` paketet innehåller ett beroende för [magento/magento-cloud-docker] paket, som innehåller funktioner och konfigurationsfiler för Docker-bilder för att starta en Docker-utvecklingsmiljö för Adobe Commerce i molninfrastrukturen. Du kan också köra Cloud Docker för Commerce som ett fristående paket. Se [Dockningsutveckling](../dev-tools/cloud-docker.md).

## Tjänster, flöden och variabler

Du kan använda `ece-tools` paket för att visa detaljerad information om Base64-kodad [Molnvariabler](../environment/variables-cloud.md) används i alla molnmiljöer. Följande kommando visar alla tjänster, flöden och variabler.

```bash
php ./vendor/bin/ece-tools env:config:show
```

Om du vill visa en viss uppsättning information använder du följande format:

```bash
php ./vendor/bin/ece-tools env:config:show <option>
```

- `services`—Visar relationsdata från `MAGENTO_CLOUD_RELATIONSHIPS` miljövariabel, definierad i `services.yaml` -fil.
- `routes`—Visar de konfigurerade vägarna för projektet med `MAGENTO_CLOUD_ROUTES` miljövariabel.
- `variables`—Visar de konfigurerade variablerna för projektet med `MAGENTO_CLOUD_VARIABLES` miljövariabel.

Exempelutdata för `services` alternativ:

```terminal
Magento Cloud Services:
+-----------------------------------+----------------------------------+
| Service Configuration             | Value                            |
+-----------------------------------+----------------------------------+
| database:                                                            |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| password                          | <password>                       |
| port                              | 3306                             |
+-----------------------------------+----------------------------------+
| opensearch:                                                          |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| port                              | 9200                             |
...
```

## Verifiera miljökonfiguration

Det finns en uppsättning verifieringskommandon som hjälper dig att utvärdera projektets konfiguration. Se [Smarta guider](../deploy/smart-wizards.md) i _Optimera driftsättningen_ för en detaljerad beskrivning av varje guidekommando. The `wizard:ideal-state` -kommandot körs automatiskt under byggfasen. Så här verifierar du det idealiska läget för ditt projekt:

```bash
php ./vendor/bin/ece-tools wizard:ideal-state
```

>[!NOTE]
>
>Du måste köra `wizard:ideal-state` i fjärrmolnmiljön. Kommandot returnerar alltid `The configured state is not ideal` fel vid körning i den lokala utvecklingsmiljön.

Exempel:

```terminal
Ideal state is configured
```

Se [Versionsinformation för islagsverktyg](../release-notes/cloud-tools-suite.md).

## Adobe-patchar och anpassade patchar

The `ece-tools` paketet innehåller ett beroende för [magento/magento-cloud-patches] paket som innehåller korrigeringsfiler för Adobe och snabbkorrigeringar som förbättrar integreringen av alla Adobe Commerce-versioner med molnmiljöer och stöder snabb leverans av viktiga korrigeringsfiler. &quot;Levererar även anpassade korrigeringsfiler som du lägger till i ditt Adobe Commerce i molninfrastrukturprojekt. Se [Tillämpa patchar](../development/apply-patches.md).

<!-- link definitions -->

[ece-repo]: https://github.com/magento/ece-tools
[magento/magento-cloud-docker]: https://github.com/magento/magento-cloud-docker
[magento/magento-cloud-patches]: https://github.com/magento/magento-cloud-patches
