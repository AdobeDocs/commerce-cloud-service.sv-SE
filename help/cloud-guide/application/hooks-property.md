---
title: Hooks, egenskap
description: Se exempel på hur du konfigurerar hooks-egenskapen i [!DNL Commerce] programkonfigurationsfil.
feature: Cloud, Configuration, Build, Deploy
exl-id: d9561f09-5129-4b72-978e-2e3873e8efae
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Hooks, egenskap

Använd `hooks` för att köra kommandon i kommandotolken under bygg-, distributions- och efterdriftfaserna:

- **`build`**—Kör kommandon _före_ paketera programmet. Tjänster, som databasen eller Redis, är inte tillgängliga eftersom programmet ännu inte har distribuerats. Lägga till egna kommandon _före_ standardvärdet `php ./vendor/bin/ece-tools` så att anpassat innehåll fortsätter till distributionsfasen.

- **`deploy`**—Kör kommandon _efter_ paketera och distribuera programmet. Du kan nu komma åt andra tjänster. Sedan standardinställningen `php ./vendor/bin/ece-tools` kommandot kopierar `app/etc` till rätt plats måste du lägga till egna kommandon _efter_ kommandot deploy för att förhindra att anpassade kommandon misslyckas.

- **`post_deploy`**—Kör kommandon _efter_ driftsätta ditt program och _efter_ behållaren accepterar anslutningar. The `post_deploy` kroken rensar cachen och läser in cachen i förväg (varmar). Du kan anpassa sidlistan med `WARM_UP_PAGES` i [Steg efter driftsättning](../environment/variables-post-deploy.md). Även om det inte är nödvändigt fungerar detta tillsammans med `SCD_ON_DEMAND` miljövariabel.

I följande exempel visas standardkonfigurationen i `.magento.app.yaml` -fil. Lägg till CLI-kommandon under `build`, `deploy`, eller `post_deploy` avsnitt _före_ den `ece-tools` kommando:

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        composer install
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    # We run deploy hook after your application has been deployed and started.
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml
    # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

Du kan också anpassa byggfasen ytterligare med `generate` och `transfer` -kommandon för att utföra ytterligare åtgärder när du specifikt skapar kod eller flyttar filer.

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        php ./vendor/bin/ece-tools build:generate
        # php /path/to/your/script
        php ./vendor/bin/ece-tools build:transfer
```

- `set -e`—gör att kopplingar misslyckas vid det första misslyckade kommandot i stället för det sista misslyckade kommandot.
- `build:generate`—använder korrigeringsfiler, validerar konfiguration, genererar ID och genererar statiskt innehåll om SCD är aktiverat för byggfasen.
- `build:transfer`—överför genererad kod och statiskt innehåll till slutmålet.

Kommandona körs från programmet (`/app`). Du kan använda `cd` om du vill ändra katalogen. Hakarna misslyckas om det sista kommandot i dem misslyckas. Lägg till `set -e` till början av kroken.

**Kompilera Sass-filer med grunt**:

```yaml
dependencies:
    ruby:
        sass: "3.4.7"
    nodejs:
        grunt-cli: "~0.1.13"

hooks:
    build: |
        cd public/profiles/project_name/themes/custom/theme_name
        npm install
        grunt
        cd
        php ./vendor/bin/ece-tools build
```

Kompilera Sass-filer med `grunt` före statisk innehållsdistribution, som sker under bygget. Placera `grunt` före `build` -kommando.

{{scenarios}}
