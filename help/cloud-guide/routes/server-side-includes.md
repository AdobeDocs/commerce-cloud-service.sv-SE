---
title: SSI (Server-side includes)
description: Lär dig hur du använder SSI (server-side includes) med Adobe Commerce i molninfrastrukturen.
feature: Cloud, Routes
exl-id: 34a38cb5-5f0e-49ac-9dba-bb581a06aeed
source-git-commit: 649c11b111aa9c9105e54908bf9c6f48741f10e4
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# SSI (Server-side includes)

[SSI (Server-side includes)](https://nginx.org/en/docs/http/ngx_http_ssi_module.html) (SSI) är direktiv på HTML-sidor som utvärderas på servern medan sidorna återges. Med SSI kan du lägga till dynamiskt genererat innehåll på en befintlig HTML-sida utan att hela sidan behöver skickas.

Du kan aktivera eller inaktivera SSI per väg i `.magento/routes.yaml`; till exempel:

```yaml
    "http://{default}/":
        type: upstream
        upstream: "myapp:php"
        cache:
            enabled: false
            ssi:
                enabled: true
    "http://{default}/time.php":
        type: upstream
        upstream: "myapp:php"
        cache:
            enabled: true
```

Med SSI kan du inkludera HTML i dina svarsdirektiv som gör att servern fyller i delar av HTML, med hänsyn tagen till eventuella befintliga [cachelagringskonfiguration](caching.md).

I följande exempel visas hur du infogar en dynamisk datumkontroll längst upp på en sida och en annan datumkontroll längst ned som uppdateras var 600:e sekund:

Lägg till följande på alla sidor, till exempel `/index.php`:

```php?start_inline=1
echo date(DATE_RFC2822);
<!--#include virtual="time.php" -->
```

Lägg till följande i `time.php`:

```php?start_inline=1
header("Cache-Control: max-age=600");
echo date(DATE_RFC2822);
```

Bläddra till sidan som du lade till kontrollen på. Uppdatera sidan flera gånger och lägg märke till att tiden högst upp på sidan ändras, men att tiden längst ned bara ändras var 600:e sekund.
