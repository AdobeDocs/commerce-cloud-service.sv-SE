---
title: Arbetare
description: Lär dig hur du konfigurerar arbetaregenskapen i [!DNL Commerce] programkonfigurationsfil.
feature: Cloud, Configuration
exl-id: d6816925-5912-45ca-8255-6c307e58542d
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Egenskapen Arbetare

Du kan definiera en arbetare som ska köras oberoende av webbinstansen utan att Nginx-instansen körs, men arbetaren använder samma nätverkslagring som används av [!DNL Commerce] program. Du behöver inte konfigurera en webbserver på arbetarinstansen (med Node.js eller Go) eftersom routern inte kan dirigera offentliga begäranden till arbetaren. Detta gör arbetarinstansen idealisk för bakgrundsuppgifter eller för kontinuerliga aktiviteter som riskerar att blockera en distribution.

## Konfigurera en arbetare

Arbetare är endast tillgängliga för användning i Pro Staging- och Production-miljöer. Pro-integrering och Starter-miljöer kan välja att använda [CRON_CONSUMERS_RUNNER](../environment/variables-deploy.md#cron_consumers_runner) variabel.

Så här konfigurerar du en arbetare i Pro Staging eller Production [Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) och innehålla följande information:

- Projekt-ID
- Miljö-ID
- Arbetarnamn
- Starta kommandon

Du kan konfigurera en process per arbetare. En grundläggande, gemensam arbetskonfiguration i `.magento.app.yaml` filen kan se ut så här:

```yaml
workers:
    queue:
        commands:
            start: |
                php ./bin/magento queue:consumers:start commerce.eventing.event.publish
```

I det här exemplet definieras en enskild arbetare med namnet `queue`, med en liten (storlek S) nivå av resurstilldelning och kör `php ./bin/magento` -kommando vid start. Arbetaren `queue` körs sedan på varje nod som en arbetsprocess. Om kommandot avslutas startas det om automatiskt.

## Kommandon och åsidosättningar

The `commands.start` -tangenten krävs för att starta kommandon med arbetarprogrammet. Du kan använda vilket giltigt kommando som helst, men det är idealiskt att använda språket i ditt program. Om kommandot som anges av `start` tangenten avslutas, den startas om automatiskt.

>[!IMPORTANT]
>
>The `deploy` och `post_deploy` krokar och `crons` kommandon körs bara i webbbehållaren, inte i arbetarinstanser.

### Arv

Definitioner för `size`, `relationships`, `access`, `disk` och `mount`och `variables` egenskaper ärvs av en arbetare, såvida de inte uttryckligen åsidosätts.

Följande egenskaper används oftast för att åsidosätta [inställningar på översta nivån](properties.md):

- `size`—tilldela färre resurser till en enda bakgrundsprocess
- `variables`—instruera programmet att köras annorlunda

### Timing och köer

Även om varje arbetare köar bakom en annan skapar följande konfiguration en konsekvent tvåsekundersseparation i tidsstämplar i `var/time.txt` oavsett åtta sekunders strömsparläge i PHP-koden:

```yaml
workers:
    time1:
        commands:
            start: 'php -r "sleep(8); echo time() . PHP_EOL;" >> var/time.txt& sleep 2'
```
