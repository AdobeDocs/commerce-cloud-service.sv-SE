---
title: Anpassad VCL för att snabbt kringgå cache
description: Felsök trafiken till den ursprungliga servern genom att skapa ett anpassat VCL-kodfragment som kringgår snabbcachen.
feature: Cloud, Configuration, Cache
exl-id: a2e9dc57-9b5e-4716-9965-a4324442ad00
source-git-commit: 7a181af2149eef7bfaed4dd4d256b8fa19ae1dda
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Anpassad VCL för att snabbt kringgå cache

Du kan skapa ett anpassat VCL-kodfragment som kringgår snabbcachen så att du kan felsöka begärandetrafik till den ursprungliga servern. Du kan till exempel skapa ett kodfragment som avgör om platsproblem orsakas av cachelagring eller om sidhuvuden ska felsökas.

Du kan konfigurera fragmentet så att det kringgår snabb cachelagring för begäranden från en viss IP-adress eller URL.

>[!NOTE]
>
>Innan du sammanfogar en anpassad VCL-konfiguration i en produktionsmiljö måste du testa koden i mellanlagringsmiljön.

**Förutsättningar:**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

**För att kringgå snabb cachelagring baserat på IP-adress eller URL**:

{{admin-login-step}}

1. Klicka **Lager** > Inställningar > **Konfiguration** > **Avancerat** > **System**.

1. Expandera **Helsidescache** > **Snabb konfiguration** > **Anpassade VCL-kodfragment**.

1. Klicka **Skapa anpassat fragment**.

1. Lägg till VCL-fragmentvärden:

   - **Namn** — `bypass_fastly`

   - **Typ** — `recv`

   - **Prioritet** — `5`

   - **VCL** textutdrag —

     Följande exempel kringgår Fastly för en specifik IP-adress:

     ```conf
     if (client.ip == "<Your IPv4 IP address>" || client.ip == "<Your IPv6 IP address>") {
       return(pass);
     }
     ```

     Följande exempel kringgår Snabbt för ett specifikt URL-mönster:

     ```conf
     if (req.url ~ "/media/feeds/GoogleShoppingHiVisNew.xml") {  return (pass);}
     ```

     Om du vill ha en exakt URL-matchning använder du `==` operatorn i stället för `~` -operator. Se [Snabb VCL-referens] för mer information.

1. Klicka **Skapa**.

   ![Skapa VCL-kodfragment med snabb åsidosättning](/help/assets/cdn/fastly-create-bypass-snippet.png)

1. När sidan har lästs in igen klickar du på **Ladda upp VCL snabbt** i *Snabb konfiguration* -avsnitt.

1. När överföringen är klar uppdaterar du cacheminnet enligt meddelandet längst upp på sidan.

   Validerar snabbt den uppdaterade VCL-versionen under överföringsprocessen. Om valideringen misslyckas kan du åtgärda eventuella problem genom att redigera det anpassade VCL-fragmentet. Ladda sedan upp VCL-filen igen.

När du har lagt till VCL-kodfragmentet kan du använda cURL-kommandon för att skicka begäranden till den ursprungliga servern från den angivna IP-adressen eller URL:en enligt följande exempel:

```bash
curl -svo /dev/null www.example.com/index.html
```

Kontrollera sedan svaret på felsökningsproblem med det ocachelagrade innehållet.

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}

<!--External link definitions-->

[Snabb VCL-referens]: https://docs.fastly.com/vcl/
