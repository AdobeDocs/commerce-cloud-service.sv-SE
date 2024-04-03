---
title: Anpassad VCL för att tillåta begäranden
description: Filtrera inkommande förfrågningar och tillåt åtkomst via IP-adress för Adobe Commerce-webbplatser genom att använda en lista med snabbkantsåtkomstlistor och anpassade VCL-fragment.
feature: Cloud, Configuration, Security
exl-id: a6ee958a-c3d3-47be-b2df-510707f551fc
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# Anpassad VCL för att tillåta begäranden

Du kan använda en snabbkantslista (ACL) med ett anpassat VCL-kodfragment för att filtrera inkommande begäranden och tillåta åtkomst via IP-adress. ACL-listan anger vilka IP-adresser som tillåts.

Skapa en tillåtelselista för att begränsa åtkomsten till mellanlagringsmiljön så att endast begäranden från angivna IP-adresser för interna utvecklare och godkända externa tjänster tillåts. Du kan också skapa en tillåtelselista för säker åtkomst till Admin i mellanlagrings- och produktionsmiljöer.

I följande exempel visas hur du använder ett anpassat VCL-fragment med en [ACL (Fast Access Control List)](https://docs.fastly.com/guides/access-control-lists/about-acls) för att säkra åtkomsten till Admin för Adobe Commerce i molninfrastrukturens projektmiljö. När du lägger till det anpassade VCL-fragmentet i molnmiljön tillåter snabbast endast begäranden från IP-adresser som ingår i åtkomstkontrollistan.

>[!TIP]
>
>I miljöer för mellanlagrings- och integreringsmiljöer som inte ska vara allmänt tillgängliga använder du alternativet för HTTP-åtkomstkontroll i [[!DNL Cloud Console]](../project/overview.md#access-the-project-web-interface) för att hantera åtkomst till hela webbplatsen via IP-adress.

**Förutsättningar:**


{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Lista över IP-adresser för klienter som ska inkluderas i tillåtelselista

## Skapa Edge ACL för att tillåta klient-IP-adresser

Edge ACL:er skapar IP-adresslistor för att hantera åtkomst till din webbplats. I det här exemplet skapar du en Edge ACL och lägger till listan över IP-adresser för klienter som har åtkomst till Admin för din projektmiljö.

{{admin-login-step}}

1. Klicka **Lager** > Inställningar > **Konfiguration** > **Avancerat** > **System**.

1. Expandera **Helsidescache** > **Snabb konfiguration** > **Kant-ACL**.

1. Skapa ACL-behållaren:

   - Klicka **Lägg till ACL**.

   - På *ACL-behållare* sida, ange en **ACL-namn**—`allowlist`.

   - Välj **Aktivera efter ändringen** för att driftsätta ändringarna i den version av snabbtjänstkonfigurationen som du redigerar.

   - Klicka **Överför** för att ansluta åtkomstkontrollistan till din snabbtjänstkonfiguration.

1. Lägg till listan över IP-adresser som kan få åtkomst till administratören:

   - Klicka på inställningsikonen för `allowlist` ACL.

   - Lägg till och spara *IP-värde* för varje klient-IP-adress.

   - Klicka **Avbryt** för att återgå till sidan för systemkonfiguration.

1. Klicka **Spara konfiguration**.

1. Uppdatera cacheminnet enligt meddelandet längst upp på sidan.

## Skapa ett anpassat VCL-fragment för att skydda administratörsåtkomsten

Följande anpassade VCL-kodfragment (JSON-format) visar logiken för att filtrera begäranden till administratören och tillåta åtkomst om klientens IP-adress matchar en adress i `allowlist` ACL.

```json
{
  "name": "allowlist",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ((req.url ~ \"^/admin\") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 \"Forbidden\"; }"
}
```

Före [skapa ett anpassat fragment](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-allowlist.html#add-the-custom-vcl-snippet) Granska värdena utifrån det här exemplet för att avgöra om du behöver göra några ändringar. Ange sedan varje värde i respektive fält, till exempel `type` till textfältet, `content` till fältet Innehåll.

- `name` — Namnet på VCL-fragmentet. I detta exempel `allowlist`.

- `priority` — Avgör när VCL-fragmentet körs. Prioriteten är `5` för att omedelbart köra och kontrollera om en Admin-begäran kommer från en tillåten IP-adress. Utdraget körs före något av de förvalda VCL-kodfragmenten för Magento (`magentomodule_*`) fick prioritet 50. Ange prioriteten för varje anpassat fragment som är högre eller lägre än 50, beroende på när du vill att fragmentet ska köras. Fragment med lägre prioritetsnummer körs först.

- `type` — Anger en plats där fragmentet ska infogas i den versionshanterade VCL-koden. Denna VCL är en `recv` fragmenttyp som lägger till fragmentkoden i `vcl_recv` underrutinen under standardkoden Fast VCL och ovanför eventuella objekt.

- `content` — Det VCL-kodfragment som ska köras. I det här exemplet filtrerar koden förfrågningar till administratören och ger åtkomst om klientens IP-adress matchar en adress i `allowlist` ACL. Om adressen inte matchar blockeras begäran med en `403 Forbidden` fel.

  Om URL:en för din administratör har ändrats ersätter du exempelvärdet `/admin` med URL:en för din miljö. Till exempel: `/company-admin`.

I kodexemplet är villkoret `!req.http.Fastly-FF` är viktigt när du använder [Origo Shielding](fastly-custom-cache-configuration.md#configure-back-ends-and-origin-shielding). Ta inte bort eller redigera den här koden.

När du har granskat och uppdaterat koden för din miljö använder du någon av följande metoder för att lägga till det anpassade VCL-fragmentet i din snabbtjänstkonfiguration:

- [Lägg till det anpassade VCL-fragmentet från administratören](#add-the-custom-vcl-snippet). Den här metoden rekommenderas om du har åtkomst till Admin. (Kräver [Snabb CDN-modul för Magento 2 version 1.2.58](fastly-configuration.md#upgrade) eller senare.)

- Spara JSON-kodexemplet till en fil (till exempel `allowlist.json`) och [ladda upp det med API:t Fast](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Använd den här metoden om du inte kan komma åt administratören.

## Lägg till anpassat VCL-fragment

{{admin-login-step}}

1. Klicka **Lager** > Inställningar > **Konfiguration** > **Avancerat** > **System**.

1. Expandera **Helsidescache** > **Snabb konfiguration** > **Anpassade VCL-kodfragment**.

1. Klicka **Skapa anpassat fragment**.

1. Lägg till VCL-fragmentvärden:

   - **Namn** — `allowlist`

   - **Typ** — `recv`

   - **Prioritet** — `5`

   - Lägg till **VCL** textutdrag:

     ```conf
     if ((req.url ~ "^/admin") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 "Forbidden";}
     ```

1. Klicka **Skapa** för att generera VCL-fragmentfilen med namnmönstret `type_priority_name.vcl`, till exempel `recv_5_allowlist.vcl`

1. När sidan har lästs in igen klickar du på **Ladda upp VCL snabbt** i *Snabb konfiguration* för att lägga till filen i snabbtjänstkonfigurationen.

1. När överföringen är klar uppdaterar du cacheminnet enligt meddelandet längst upp på sidan.

Snabbt validerar den uppdaterade versionen av VCL-koden under överföringsprocessen. Om valideringen misslyckas kan du åtgärda problemet genom att redigera det anpassade VCL-fragmentet. Ladda sedan upp VCL-filen igen.

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
