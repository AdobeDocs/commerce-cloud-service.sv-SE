---
title: Variabla nivåer och alternativ
description: Lär dig mer om de olika variabelnivåerna och alternativen som används för att anpassa din Adobe Commerce i körningsmiljön för molninfrastrukturprojekt.
feature: Cloud, Configuration, Security
exl-id: 11aa0862-94c0-47fb-946a-0148f75cc24c
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Variabelnivåer

Projektvariabler gäller för alla miljöer i projektet. Miljövariabler gäller för en viss miljö eller gren. En miljö _ärver_ variabeldefinitioner från den överordnade miljön.

Du kan åsidosätta ett ärvt värde genom att definiera variabeln specifikt för miljön. Om du till exempel vill ange variabler för utveckling definierar du variabelvärdena i `.magento.env.yaml` i integreringsmiljön. Alla miljöer som härstammar från integreringsmiljön ärver dessa värden. Se [Distributionskonfiguration](configure-env-yaml.md) om du vill ha mer information om hur du konfigurerar miljön med `.magento.env.yaml` -fil.

>[!BEGINTABS]

>[!TAB CLI]

**Ställa in variabler med hjälp av CLI i molnet**:

- **Projektspecifika variabler**—Att ange samma värde för _alla_ miljöer i ditt projekt. Dessa variabler är tillgängliga vid bygge och körning i alla miljöer.

  ```bash
  magento-cloud variable:create --level project --name <variable-name> --value <variable-value>
  ```

- **Miljöspecifika variabler**—Att ange ett unikt värde för _specifik_ miljö. Dessa variabler är tillgängliga vid körning och ärvs av underordnade miljöer. Ange miljön i kommandot med `-e` alternativ.

  ```bash
  magento-cloud variable:create --level environment --name <variable-name> --value <variable-value>
  ```

När du har angett projektspecifika variabler måste du distribuera om fjärrmiljön manuellt för att ändringen ska börja gälla. Tryck på de nya implementeringarna för att utlösa en omdistribution.

>[!TAB Konsol]

**Ange variabler med[!DNL Cloud Console]**:

1. I _[!DNL Cloud Console]_klickar du på konfigurationsikonen till höger om projektnavigeringen.

   ![Konfigurera projekt](../../assets/icon-configure.png){width="36"}

1. Så här anger du en variabel på projektnivå under _Projektinställningar_ klicka **Variabel**.

   ![Projektvariabler](../../assets/ui-project-variables.png)

1. Om du vill ange en variabel på miljönivå går du till _Miljö_ väljer du en miljö och klickar på **[!UICONTROL Variables]** -fliken.

   ![Fliken Miljövariabler](../../assets/ui-environment-variables.png)

1. Klicka på **[!UICONTROL Create variable]**.

1. Ange ett namn och värde för variabeln. Välj bland alternativen:

   - Tillgängligt under körning
   - Tillgängligt under byggtid
   - JSON-värde
   - Känslig variabel (dolt värde i konsolen och CLI-svar)
   - Gör ärftlig (underordnade miljöer kan ärva miljönivåvariabler)

1. Klicka på **[!UICONTROL Create variable]**.

>[!CAUTION]
>
>Ange miljöspecifika variabler i [!DNL Cloud Console] distribuerar automatiskt om miljön.

>[!ENDTABS]

## Synlighet

Du kan begränsa synligheten för en variabel under byggandet eller körningen med `--visible-<build|runtime>` -kommando. Det finns även alternativ för att ange arv och känslighet.

Använd följande alternativ för att förhindra att en variabel visas eller ärvs:

- `--inheritable false`—inaktiverar arv för underordnade miljöer. Detta är användbart när du vill ange värden som bara är för produktion på `master` och tillåter att alla andra miljöer använder en projektnivåvariabel med samma namn.
- `--sensitive true`—gör variabeln som _ej läsbar_ i [!DNL Cloud Console]. Du kan inte visa variabeln i användargränssnittet, men du kan visa variabeln från programbehållaren, precis som andra variabler.

I följande exempel visas ett specifikt fall som förhindrar att en variabel visas eller ärvs. Du kan bara ange dessa alternativ i CLI. Det här fallet gäller inte alla tillgängliga miljövariabler.

```bash
magento-cloud variable:create --name <variable-name> --value <variable-value> --inheritable false --sensitive true
```

## Verifiera variabelnivåer och värden

Du kan visa en lista med befintliga variabler med hjälp av CLI i molnet.

```bash
magento-cloud variables
```

```terminal
Variables on the project Project-Name (<project-id>), environment <environment-name>:
+----------------------------+-------------+-------------------------------------------+
| Name                       | Level       | Value                                     |
+----------------------------+-------------+-------------------------------------------+
| env:COMPOSER_AUTH          | project     | {                                         |
|                            |             |    "http-basic": {                        |
|                            |             |       "repo.magento.com": {               |
|                            |             |       "username":                         |
|                            |             | "<public-key>",                           |
|                            |             |       "password":                         |
|                            |             | "<private-key>"                           |
|                            |             |     }                                     |
|                            |             |   }                                       |
|                            |             | }                                         |
| ADMIN_EMAIL                | project     | admin@123.com                             |
| ADMIN_EMAIL                | environment | admin@123.com                             |
| ADMIN_PASSWORD             | environment | password                                  |
| ADMIN_URL                  | environment | admin123                                  |
| ADMIN_USERNAME             | environment | admin                                     |
| php:newrelic.license       | environment | xxxx71fb030366182117f955a22e4baf8exxxxxx  |
+----------------------------+-------------+-------------------------------------------+
```
