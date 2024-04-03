---
title: Blockera skräppost
description: Blockera spam från webbplatsen med hjälp av Fastly Edge-ordlistan och ett anpassat VCL-kodfragment.
feature: Cloud, Configuration, Security
exl-id: 665bac93-75db-424f-be2c-531830d0e59a
source-git-commit: 7a181af2149eef7bfaed4dd4d256b8fa19ae1dda
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# Blockera skräppost

I följande exempel visas hur du konfigurerar [Ordlista för fast kant](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api) med ett anpassat VCL-kodfragment för att blockera spam från din Adobe Commerce-webbplats för molninfrastruktur.

>[!NOTE]
>
>Vi rekommenderar att du lägger till anpassade VCL-konfigurationer i en mellanlagringsmiljö där du kan testa dem innan du kör dem mot produktionsmiljön.

**Förutsättningar:**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Granska webbplatsloggarna för falska hänvisnings-URL:er och gör en lista över domäner som ska blockeras.

## Skapa en hänvisare blockeringslista

Med Edge Dictionaries skapas nyckelvärdepar som är tillgängliga för VCL-funktioner under VCL-fragmentbearbetning. I det här exemplet skapar du en kantordlista med en lista över referenswebbplatser som ska blockeras.

{{admin-login-step}}

1. Klicka **Lager** > **Inställningar** > **Konfiguration** > **Avancerat** > **System**.

1. Expandera **Helsidescache** > **Snabb konfiguration** > **Edge-ordlistor**.

1. Skapa ordlistebehållaren:

   - Klicka **Lägg till behållare**.

   - På *Behållare* sida, ange en **Ordlistenamn**—`referrer_blocklist`.

   - Välj **Aktivera efter ändringen** för att driftsätta ändringarna i den version av snabbtjänstkonfigurationen som du redigerar.

   - Klicka **Överför** för att koppla ordboken till din snabbtjänstkonfiguration.

1. Lägg till listan med domännamn som ska blockeras i `referrer_blocklist` ordlista:

   - Klicka på inställningsikonen för `referrer_blocklist` ordbok.

   - Lägg till och spara nyckelvärdepar i den nya ordlistan. I det här exemplet **Nyckel** är domännamnet för en referens-URL som ska blockeras och **Värde** är `true`.

     ![Lägg till felaktiga referensordlisteobjekt](../../assets/cdn/fastly-referrer-blocklist-dictionary.png)

   - Klicka **Avbryt** för att återgå till sidan för systemkonfiguration.

1. Klicka **Spara konfiguration**.

1. Uppdatera cacheminnet enligt meddelandet längst upp på sidan.

Mer information om Edge-ordlistor finns i [Skapa och använda Edge-ordlistor](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api) och [anpassade VCL-fragment](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api#custom-vcl-examples) i Snabbas dokumentation.

## Skapa ett anpassat VCL-fragment för att blockera spam från referensen

I följande anpassade VCL-kodfragment (JSON-format) visas logiken för att kontrollera och blockera begäranden. VCL-fragmentet hämtar värddatorn för en referenswebbplats till ett sidhuvud och jämför sedan värdnamnet med listan med URL:er i `referrer_blocklist` ordbok. Om värdnamnet matchar blockeras begäran med en `403 Forbidden` fel.

```json
{
  "name": "block_bad_referrer",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "set req.http.Referer-Host = regsub(req.http.Referer, \"^https?:\/\/?([^:\/s]+).*$\", \"\\1\"); if (table.lookup(referrer_blocklist, req.http.Referer-Host)) { error 403 \"Forbidden\"; }"
}
```

Innan du skapar ett fragment baserat på det här exemplet ska du granska värdena för att avgöra om du behöver göra några ändringar:

- `name` — Namnet på VCL-fragmentet. I det här exemplet använde vi `block_bad_referrer`.

- `dynamic` — Värdet 0 anger att [reguljärt fragment](https://docs.fastly.com/en/guides/using-regular-vcl-snippets) för att överföra till den versionshanterade videobandboken för snabbkonfigurationen.

- `priority` — Avgör när VCL-fragmentet körs. Prioriteten är `5` om du vill köra den här kodfragmentkoden före något av de förvalda VCL-kodfragmenten för Magento (`magentomodule_*`) fick prioritet 50. Ange prioriteten för varje anpassat fragment som är högre eller lägre än 50, beroende på när du vill att fragmentet ska köras. Fragment med lägre prioritetsnummer körs först.

- `type` — Anger en plats där fragmentet ska infogas i VCL-versionen. I det här exemplet är VCL-fragmentet en `recv` kodfragment. När fragmentet infogas i VCL-versionen läggs det till i `vcl_recv` subrutin, under standardkoden Fast VCL och ovanför eventuella objekt.

- `content` — Det VCL-kodfragment som ska köras på en rad, utan radbrytningar.

När du har granskat och uppdaterat koden för din miljö använder du någon av följande metoder för att lägga till det anpassade VCL-fragmentet i din snabbtjänstkonfiguration:

- [Lägg till det anpassade VCL-fragmentet från administratören](#add-the-custom-vcl-snippet). Den här metoden rekommenderas om du har åtkomst till Admin. (Kräver [Snabbt version 1.2.58](fastly-configuration.md#upgrade) eller senare.)

- Spara JSON-kodexemplet till en fil (till exempel `allowlist.json`) och [ladda upp det med API:t Fast](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Använd den här metoden om du inte kan komma åt administratören.

## Lägg till anpassat VCL-fragment

{{admin-login-step}}

1. Klicka **Lager** > Inställningar > **Konfiguration** > **Avancerat** > **System**.

1. Expandera **Helsidescache** > **Snabb konfiguration** > **Anpassade VCL-kodfragment**.

1. Klicka **Skapa anpassat fragment**.

1. Lägg till VCL-fragmentvärden:

   - **Namn** — `block_bad_referrer`

   - **Typ** — `recv`

   - **Prioritet** — `5`

   - **VCL** textutdrag —

     ```conf
     set req.http.Referer-Host = regsub(req.http.Referer,
     "^https?://?([^:/\s]+).*$", "1");
     if (table.lookup(referrer_blocklist, req.http.Referer-Host)) {
       error 403 "Forbidden";
     }
     ```

1. Klicka **Skapa**.

   ![Skapa VCL-kodfragment för anpassat referensblock](/help/assets/cdn/fastly-create-referrer-block-snippet.png)

1. När sidan har lästs in igen klickar du på **Ladda upp VCL snabbt** i *Snabb konfiguration* -avsnitt.

1. När överföringen är klar uppdaterar du cacheminnet enligt meddelandet längst upp på sidan.

Validerar snabbt den uppdaterade VCL-versionen under överföringsprocessen. Om valideringen misslyckas kan du åtgärda eventuella problem genom att redigera det anpassade VCL-fragmentet. Ladda sedan upp VCL-filen igen.

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
