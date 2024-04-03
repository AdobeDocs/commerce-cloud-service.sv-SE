---
title: Omdirigeringar
description: Lär dig hur du hanterar omdirigeringsregler för Adobe Commerce i molninfrastrukturprojekt.
feature: Cloud, Routes
exl-id: 7089a790-6341-4443-990a-df42091f0680
source-git-commit: 649c11b111aa9c9105e54908bf9c6f48741f10e4
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Omdirigeringar

Hantering av omdirigeringsregler är ett vanligt krav för webbprogram, särskilt när du inte vill förlora inkommande länkar som har ändrats eller tagits bort över tid.

Följande visar hur du hanterar omdirigeringsregler på din Adobe Commerce i molninfrastrukturprojekt med hjälp av `routes.yaml` konfigurationsfil. Om omdirigeringsmetoderna som beskrivs i det här avsnittet inte fungerar för dig kan du använda cachelagringshuvuden för att göra samma sak.

{{route-placeholder}}

## Uppdateringar av Pro-miljöer

{{pro-self-service-warning}}

>[!WARNING]
>
>För Adobe Commerce i molninfrastrukturprojekt konfigureras flera icke-regex-omdirigeringar och omskrivningar i `routes.yaml` filen kan orsaka prestandaproblem. Om `routes.yaml` filen är 32 kB eller större, avlastar du icke-regex omdirigerar och skriver om till Fastly. Se [Avlasta icke-regex-omdirigeringar till Fast istället för Nginx (rutter)](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/offload-non-regex-redirects-to-fastly-instead-of-nginx-routes.html) i _Adobe Commerce Help Center_.

## Omdirigeringar i hela flödet

Med omdirigeringar i hela flödet kan du definiera enkla vägar med `routes.yaml` -fil. Du kan till exempel omdirigera från en apex-domän till en `www` underdomän enligt följande:

```yaml
http://{default}/:
    type: redirect
    to: http://www.{default}/
```

## Omdirigeringar för delväg

I `.magento/routes.yaml` kan du lägga till regler för partiell omdirigering till befintliga flöden baserat på mönstermatchning:

```yaml
http://{default}/:
    redirects:
        expires: 1d
        paths:
          "/from": { to: "http://example.com/" }
          "/regexp/(.*)/matching": { to: "http://example.com/$1", regexp: true }
```

Delvisa omdirigeringar fungerar med alla typer av vägar, inklusive flöden som betjänas direkt av programmet.

Två nycklar finns under `redirects`:

- **förfaller**- Valfritt, anger hur lång tid det tar att cachelagra omdirigeringen i webbläsaren. Exempel på giltiga värden är `3600s`, `1d`, `2w`, `3m`.

- **banor**—Ett eller flera nyckelvärdepar som anger konfigurationen för omdirigeringsregler för partiell väg.

  För varje omdirigeringsregel är nyckeln ett uttryck för att filtrera sökvägar för omdirigering. Värdet är ett objekt som anger målmålet för omdirigeringen och alternativ för bearbetning av omdirigeringen.

  Objektet value har följande egenskaper:

  | Egenskap | Beskrivning |
  | ---------- | ----------- |
  | `to` | Obligatoriskt, en partiell absolut sökväg, URL med protokoll och värd, eller mönster som anger målmålet för omdirigeringsregeln. |
  | `regexp` | Valfritt, standardvärdet är `false`. Anger om sökvägsnyckeln ska tolkas som ett reguljärt PCRE-uttryck. |
  | `prefix` | Anger om omdirigeringen gäller både banan och alla dess underordnade objekt, eller bara själva banan. Standardvärdet är `true`. Detta värde stöds inte om `regexp` är `true`. |
  | `append_suffix` | Avgör om suffixet överförs med omdirigeringen. Standardvärdet är `true`. Detta värde stöds inte om `regexp` key is `true` eller* om `prefix` key is `false`. |
  | `code` | Anger HTTP-statuskoden. Giltiga statuskoder [`301` (Flyttad permanent)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.2), [`302`](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.3), [`307`](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.8)och [`308`](https://www.rfc-editor.org/rfc/rfc7238). Standardvärdet är `302`. |
  | `expires` | Valfritt, anger hur lång tid det tar att cachelagra omdirigeringen i webbläsaren. Standardvärdet är `expires` värde definierat direkt under `redirects` på den här nivån kan du finjustera cacheminnets förfallotid för enskilda partiella omdirigeringar. |

## Exempel på delvägsomdirigeringar

I följande exempel visas hur du anger delvägsomdirigeringar i `routes.yaml` fil med olika `paths` konfigurationsalternativ.

### Mönstermatchning för reguljära uttryck

Använd följande format för att konfigurera omdirigeringsbegäranden baserat på ett reguljärt uttryck.

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths:
        "/regexp/(.*)/match": { to: "http://example.com/$1", regexp: true }
```

Den här konfigurationen filtrerar sökvägar mot ett reguljärt uttryck och dirigerar om matchande begäranden till `https://example.com`. Till exempel en begäran till `https://example.com/regexp/a/b/c/match` omdirigerar till `https://example.com/a/b/c`.

### Matchning av prefixmönster

Använd följande format för att konfigurera omdirigeringsbegäranden för sökvägar som börjar med ett angivet prefixmönster.

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths:
        "/from": { to: "https://{default}/to", prefix: true }
```

Den här konfigurationen fungerar så här:

- Omdirigerar begäranden som matchar mönstret `/from` till banan `http://{default}/to`.

- Omdirigerar begäranden som matchar mönstret `/from/another/path` till `https://{default}/to/another/path`.

- Om du ändrar `prefix` egenskap till `false`, begäranden som matchar `/from` mönstret utlöser en omdirigering, men förfrågningar som matchar `/from/another/path` inte mönstret.

### Matchning av suffixmönster

Använd följande format för att konfigurera omdirigeringsbegäranden som bifogar sökvägssuffixet från begäran till målmålet:

```yaml
http://{default}/:
    type: upstream
    redirects:
    paths: "/from": { to: "https://{default}/to", append_suffix: false }
```

Den här konfigurationen fungerar så här:

- Omdirigerar begäranden som matchar mönstret `/from/path/suffix` till banan `https://{default}/to`.

- Om du ändrar `append_suffix` egenskap till `true`och sedan förfrågningar som matchar `/from/path/suffix`  omdirigera till banan `https://{default}/to/path/suffix`.

### Sökvägsspecifik cachekonfiguration

Använd följande format om du vill anpassa tiden för att cachelagra en omdirigering från en viss sökväg:

```yaml
http://{default}/:
    type: upstream
    redirects:
    expires: 1d
    paths:
        "/from": { to: "https://example.com/" }
        "/here": { to: "https://example.com/there", expires: "2w" }
```

Den här konfigurationen fungerar så här:

- Omdirigerar från den första banan (`/from`) cachelagras i en dag.

- Omdirigerar från den andra sökvägen (`/here`) cachas i två veckor.
