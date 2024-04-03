---
title: Webbegenskap
description: Se exempel på hur du konfigurerar egenskapen web i [!DNL Commerce] programkonfigurationsfil.
feature: Cloud, Configuration
exl-id: 2ca94908-6fe1-42fd-bc3b-ef2dd473f1bb
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Webbegenskap

The `web` -egenskapen definierar hur ditt program exponeras för webben (i HTTP), avgör hur webbprogrammet visar innehåll och styr hur programbehållaren svarar på inkommande begäranden genom att ange regler på varje plats _block_. Ett -block representerar en absolut sökväg med ett snedstreck (`/`).

```yaml
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
```

Du kan finjustera dina `locations` konfiguration med följande nyckelvärden för varje `locations` block:

| Attribut | Beskrivning |
| :--- | :--- |
| `allow` | Servera filer som inte matchar reglerna. Standardvärde = `true` |
| `expires` | Ange antalet sekunder som innehållet ska cachelagras i webbläsaren. Den här tangenten aktiverar `cache-control` och `expires` rubriker för statiskt innehåll. Om det här värdet inte anges visas `expires` -direktiv och resulterande sidhuvuden inkluderas inte när statiska innehållsfiler hanteras. Ett negativ 1 (`-1`) resulterar inte i någon cachelagring och är standardvärdet. Du kan uttrycka tidsvärdet med följande enheter:  `ms` (millisekunder), `s` (sekunder), `m` (minuter), `h` (timmar), `d` (dagar), `w` (veckor), `M` (månader, 30d), eller `y` (år, 365d) |
| `headers` | Ange anpassade rubriker, till exempel `X-Frame-Options`, för statiskt innehåll som hanteras från den här platsen. |
| `index` | Visa en lista över statiska filer som kan användas i programmet, t.ex. `index.html` -fil. Den här nyckeln förväntar sig en samling. Detta fungerar bara om åtkomsten till filen eller filerna är&quot;tillåten&quot; av `allow` eller `rules` för den här platsen. |
| `rules` | Ange åsidosättningar för en plats. Använd ett reguljärt uttryck för att matcha en begäran. Om en inkommande begäran matchar regeln åsidosätts den vanliga hanteringen av begäran av nycklarna som används i regeln. |
| `passthru` | Ange den URL som används om en statisk fil eller PHP-fil inte kan hittas. Vanligtvis är den här URL-adressen den främre kontrollenheten för dina program, till exempel `/index.php` eller `/app.php`. |
| `root` | Ange sökvägen i förhållande till roten för programmet som visas på webben. Den offentliga katalogen (plats &quot;/&quot;) för ett Cloud-projekt är som standard inställd på &quot;pub&quot;. |
| `scripts` | Tillåt inläsning av skript på den här platsen. Ange värdet till `true` för att tillåta skript. |

Standardkonfigurationen tillåter följande:

- Från roten (`/`) kan du bara komma åt webb och media
- Från `~/pub/static` och `~/pub/media` sökvägar, alla filer kan öppnas

I följande exempel visas standardkonfigurationen i `.magento.app.yaml` för en uppsättning webbtillgängliga platser som är associerade med en post i  [`mounts` property](properties.md#mounts):

```yaml
 # The configuration of app when it is exposed to the web.
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
            root: "pub"
            # The front-controller script to send non-static requests to.
            passthru: "/index.php"
            index:
                - index.php
            expires: -1
            scripts: true
            allow: false
            rules:
                \.(css|js|map|hbs|gif|jpe?g|png|tiff|wbmp|ico|jng|bmp|svgz|midi?|mp?ga|mp2|mp3|m4a|ra|weba|3gpp?|mp4|mpe?g|mpe|ogv|mov|webm|flv|mng|asx|asf|wmv|avi|ogx|swf|jar|ttf|eot|woff|otf|html?)$:
                    allow: true
                ^/sitemap(.*)\.xml$:
                    passthru: "/media/sitemap$1.xml"
        "/media":
            root: "pub/media"
            allow: true
            scripts: false
            expires: 1y
            passthru: "/get.php"
        "/static":
            root: "pub/static"
            allow: true
            scripts: false
            expires: 1y
            passthru: "/front-static.php"
            rules:
                ^/static/version\d+/(?<resource>.*)$:
                    passthru: "/static/$resource"
```

>[!NOTE]
>
>I det här exemplet visas standardwebbkonfigurationen för ett molnprojekt som har konfigurerats för att stödja en enda domän. För ett projekt som kräver stöd för flera webbplatser eller butiker finns `web` måste konfigureras för att ge stöd åt delade domäner. Se [Konfigurera platser för delade domäner](../store/multiple-sites.md#configure-locations-for-shared-domains).
