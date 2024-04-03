---
title: Molnspecifika variabler
description: Se en lista över miljövariabler som är specifika för Adobe Commerce om molninfrastruktur.
feature: Cloud, Configuration
recommendations: noDisplay, catalog
role: Developer
exl-id: 84b7c0fc-f0b0-4ff5-9f33-9d17180a9306
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Molnspecifika variabler

Miljövariabler som är specifika för Adobe Commerce i molninfrastruktur använder `MAGENTO_CLOUD_*` prefix:

| Variabel | Beskrivning |
| -------- | --------------- |
| `MAGENTO_CLOUD_APP_DIR` | Den absoluta sökvägen till programkatalogen. |
| `MAGENTO_CLOUD_APPLICATION` | Ett base64-kodat JSON-objekt som beskriver programmet. Det mappas till `.magento.app.yaml` filinnehåll och har undernycklar. |
| `MAGENTO_CLOUD_APPLICATION_NAME` | Namnet på programmet som konfigurerats i `.magento.app.yaml` -fil. |
| `MAGENTO_CLOUD_DOCUMENT_ROOT` | Den absoluta sökvägen till webbdokumentets rot, om tillämpligt. |
| `MAGENTO_CLOUD_ENVIRONMENT` | Namnet på miljögrenen. |
| `MAGENTO_CLOUD_PROJECT` | Projekt-ID. |
| `MAGENTO_CLOUD_RELATIONSHIPS` | Ett base64-kodat JSON-objekt som representerar slutpunktsdefinition för nyckel (relationsnamn) och värde (arrayer för relationspar). Varje relationsslutpunktsdefinition är en uppdelad form av en URL. Den har en `scheme`, a `host`, a `port`och _valfritt_ a `username`, `password`, `path`och ytterligare information i `query`. |
| `MAGENTO_CLOUD_ROUTES` | Beskriv de vägar som definieras i miljön `.magento/routes.yaml` -fil. |
| `MAGENTO_CLOUD_TREE_ID` | Programmets träd-ID, som motsvarar SHA för trädet i Git. |
| `MAGENTO_CLOUD_VARIABLES` | Ett base64-kodat JSON-objekt med nyckelvärdepar, som `"key":"value"`. |
| `MAGENTO_CLOUD_LOCKS_DIR` | Anger sökvägen till monteringspunkten för låsleverantören i molninfrastrukturen. Lås-providern förhindrar att duplicerade cron-jobb och cron-grupper startas. |

>[!WARNING]
>
>Lägga till miljövariabler i [åsidosätta konfigurationsinställningar](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html) med [[!DNL Cloud Console]](../project/overview.md)måste variabelnamnet föregås av `env:` som i följande exempel:
>
>![Exempel på miljövariabel](../../assets/set-env-variable-ui.png)

Eftersom värdena kan ändras över tid är det bäst att granska variabeln under körning och använda den för att konfigurera programmet. Använd till exempel `MAGENTO_CLOUD_RELATIONSHIPS` variabel för att hämta miljörelaterade relationer enligt följande:

```php
<?php
/**
  * Get relationships information from cloud environment variable.
  *
  * @return mixed
  */
    protected function getRelationships()
    {
        return json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]), true);
    }
```

## Visa miljövariabler

Du kan använda `env:config:show` från [den `ece-tools` package](../dev-tools/package-overview.md) för att visa en lista med variabler för den aktuella miljön.

```bash
php ./vendor/bin/ece-tools env:config:show variables
```

Exempelutdata för `variables` alternativ:

```terminal
Magento Cloud Environment Variables:
+-----------------------------------+----------------------------------+
| Variable name                     | Value                            |
+-----------------------------------+----------------------------------+
| ADMIN_EMAIL                       | commerceadmin@company.com        |
| ADMIN_PASSWORD                    | 123123q                          |
+-----------------------------------+----------------------------------+
```
