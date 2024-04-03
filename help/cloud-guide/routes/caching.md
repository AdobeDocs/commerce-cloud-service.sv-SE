---
title: Cachning
description: Lär dig hur du aktiverar cachelagring för din Adobe Commerce i molnmiljöer.
feature: Cloud, Cache, Routes
exl-id: 4856aa94-2947-4dc8-b0d1-0960869dc39c
source-git-commit: 7b9c6a4cd17069c25455195bd8f273664b8a29eb
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Cachning

Du kan aktivera cachelagring i din projektmiljö för molninfrastruktur. Om du inaktiverar cachelagring visas filerna direkt i Adobe Commerce.

{{route-placeholder}}

## Konfigurera cachelagring

Aktivera cachelagring för programmet genom att konfigurera cacheregler i `.magento/routes.yaml` på följande sätt:

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
        headers: [ "Accept", "Accept-Language", "X-Language-Locale" ]
        cookies: ["*"]
        default_ttl: 60
```

## Flödesbaserad cachelagring

Aktivera detaljerad cachelagring genom att ange cachelagringsregler för flera rutter separat, vilket visas i följande exempel:

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true

http://{default}/path/:
    type: upstream
    upstream: php:php
    cache:
        enabled: false

http://{default}/path/more/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
```

Exemplet ovan cachelagrar följande vägar:

- `http://{default}/`
- `http://{default}/path/more/`
- `http://{default}/path/more/etc/`

Och följande vägar är **not** cachelagrad:

- `http://{default}/path/`
- `http://{default}/path/etc/`

>[!NOTE]
>
>Reguljära uttryck i flöden är **not** stöds.

## Cachevaraktighet

Cachevaraktigheten bestäms av `Cache-Control` svarshuvud. Om nej `Cache-Control` -huvudet finns i svaret, `default_ttl` används.

## Cachenyckel

För att bestämma hur ett svar ska cachelagras, skapar Adobe Commerce en cachenyckel som är beroende av flera faktorer och lagrar det svar som är associerat med den här nyckeln. När en begäran levereras med samma cachenyckel återanvänds svaret. Dess syfte liknar HTTP [`Vary` header](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.44).

Parametrarna `headers` och `cookies` kan du ändra den här cachenyckeln.

Standardvärdet för de här tangenterna är följande:

```yaml
cache:
    enabled: true
    headers: ["Accept-Language", "Accept"]
    cookies: ["*"]
```

## Cacheattribut

### `enabled`

När inställt på `true`, aktivera cacheminnet för den här vägen. När inställt på `false`, inaktiverar du cacheminnet för den här vägen.

### `headers`

Definierar vilka värden cachenyckeln måste vara beroende av.

Om `headers` är följande:

```yaml
cache:
    enabled: true
    headers: ["Accept"]
```

Sedan cachelagrar Adobe Commerce olika svar för varje värde i `Accept` HTTP-huvud.

### `cookies`

The `cookies` -tangenten definierar vilka värden cachenyckeln måste vara beroende av.

Exempel:

```yaml
cache:
    enabled: true
    cookies: ["value"]
```

Cachenyckeln beror på värdet på `value` cookie i begäran.

Det finns ett specialfall om `cookies` har nyckeln `["*"]` värde. Detta värde innebär att alla förfrågningar med en cookie-fil kringgår cacheminnet. Det här är standardvärdet.

>[!NOTE]
>
>Du kan inte använda jokertecken i cookie-namnet. Använd ett exakt cookie-namn eller matcha alla cookies med en asterisk (`*`). Till exempel: `SESS*` eller `~SESS` är för närvarande **not** giltiga värden.

Cookies har följande begränsningar:

- Du kan ange maximalt **50 kakor** i systemet. I annat fall genereras ett `Unable to send the cookie. Maximum number of cookies would be exceeded` undantag.
- Den maximala cookie-storleken är **4 096 byte**. I annat fall genereras ett `Unable to send the cookie. Size of '%name' is %size bytes` undantag.

### `default_ttl`

Om svaret inte har en `Cache-Control` sidhuvud, `default_ttl` -tangenten används för att definiera cachevaraktigheten i sekunder. Standardvärdet är `0`, vilket betyder att inget cachelagras.
