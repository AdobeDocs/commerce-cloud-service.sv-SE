---
title: Lägg till webbplatskarta och sökrobotar
description: Lär dig hur du lägger till webbplatskartor och sökrobotar i Adobe Commerce i molninfrastruktur.
feature: Cloud, Configuration, Search, Site Navigation
exl-id: b98f43fa-1878-466d-8ea0-1e7207af8b60
source-git-commit: ee1db75c73c086e0ea54e1a7591ca7f2b4d2b36d
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Lägg till webbplatskarta och sökrobotar

Ett försök att generera och skriva `sitemap.xml` till rotkatalogen resulterar i följande fel:

```terminal
Please make sure that "/" is writable by the web-server.
```

Med Adobe Commerce i molninfrastrukturen kan du bara skriva till specifika kataloger, som `var`, `pub/media`, `pub/static`, eller `app/etc`. När du genererar `sitemap.xml` med hjälp av administrationspanelen måste du ange `/media/` bana.

Du behöver inte generera en `robots.txt` eftersom den genererar `robots.txt` on demand-innehåll och lagrar det i databasen. Du kan visa innehållet i webbläsaren med `<domain.your.project>/robots.txt` eller `<domain.your.project>/robots` länk.

Detta kräver ECE-Tools version 2002.0.12 och senare med en uppdaterad `.magento.app.yaml` -fil. Se ett exempel på de här reglerna i [magento-cloud-databas](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml#L43-L49).

**Generera en `sitemap.xml` i version 2.2 och senare**:

1. Gå till Admin.
1. På _Marknadsföring_ meny, klicka **Webbplatskarta** i _SEO &amp; Search_ -avsnitt.
1. I _Webbplatskarta_ visa, klicka **Lägg till platskarta**.
1. I _Ny webbplatskarta_ ange följande värden:

   - **Filnamn**:`sitemap.xml`
   - **Bana**:`/media/`

1. Klicka **Spara och generera**. Den nya webbplatskartan blir tillgänglig på _Webbplatskarta_ rutnät.
1. Klicka på banan i _Link for Google_ kolumn.

**Lägga till innehåll i `robots.txt` fil**:

1. Gå till Admin.
1. På _Innehåll_ meny, klicka **Konfiguration** i _Design_ -avsnitt.
1. I _Designkonfiguration_ visa, klicka **Redigera** för webbplatsen i _Åtgärd_ kolumn.
1. I _Huvudwebbplats_ visa, klicka **Sökmotorrobotar**.
1. Uppdatera **Redigera anpassad instruktion för robots.txt** fält.
1. Klicka **Spara konfiguration**.
1. Verifiera `<domain.your.project>/robots.txt` fil eller `<domain.your.project>/robots` URL i webbläsaren.

>[!NOTE]
>
>Om `<domain.your.project>/robots.txt` filen genererar en `404 error`, [Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) för att ta bort omdirigeringen från `/robots.txt` till `/media/robots.txt`.

## Skriv om med snabbVCL-kodfragment

Om du har olika domäner och behöver separata webbplatskartor kan du skapa en VCL för att dirigera till rätt platskarta. Generera `sitemap.xml` på administrationspanelen enligt beskrivningen ovan och skapa sedan ett anpassat Fast VCL-kodfragment för att hantera omdirigeringen. Se [Anpassade VCL-fragment snabbt](../cdn/fastly-vcl-custom-snippets.md).

>[!NOTE]
>
> Du kan överföra anpassade VCL-kodfragment från administratörsgränssnittet eller med hjälp av API:t Snabb. Se [Exempel och självstudiekurser för anpassade VCL-kodfragment](../cdn/fastly-vcl-custom-snippets.md#example-vcl-snippet-code).

### Använd ett fast VCL-fragment för omdirigering

Skapa ett anpassat VCL-fragment som skriver om sökvägen för `sitemap.xml` till `/media/sitemap.xml` med `type` och `content` nyckelvärdepar.

```json
{
  "name": "sitemapxml_rewrite",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path ~ \"^/?sitemap.xml$\" ) { set req.url = \"/media/sitemap.xml\"; }"
}
```

I följande exempel visas hur du skriver om sökvägen för `robots.txt` och `sitemap.xml` till `/media/robots.txt` och `/media/sitemap.xml`

```json
{
  "name": "sitemaprobots_rewrite",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path ~ \"^/?sitemap.xml$\" ) { set req.url = \"/media/sitemap.xml\"; } else if (req.url.path ~ \"^/?robots.txt$\") { set req.url = \"/media/robots.txt\";}"
}
```

**Så här använder du ett fast VCL-fragment för en viss domänomdirigering**:

Skapa en `pub/media/domain_robots.txt` fil, där domänen är `domain.com`och använder nästa VCL-kodfragment:

```json
{
  "name": "domain_robots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }}"
}
```

VCL-utdragsvägar `http://domain.com/robots.txt` och presenterar `pub/media/domain_robots.txt` -fil.

Konfigurera en omdirigering för `robots.txt` och `sitemap.xml` i ett enskilt fragment, skapa `pub/media/domain_robots.txt` och `pub/media/domain_sitemap.xml` filer, där domänen är `domain.com` och använda nästa VCL-kodfragment:

```json
{
  "name": "domain_sitemaprobots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }} else if ( req.url.path == \"/sitemap.xml\" ) { if ( req.http.host ~ \"(domain).com$\" ) {  set req.url = \"/media/\" re.group.1 \"_sitemap.xml\"; }}"
}
```

I `sitemap` admin config, du måste ange filens plats med `pub/media/` i stället för `/`.

### Konfigurera indexering med sökmotor

Aktivera `robots.txt` anpassning måste du aktivera **Indexering med sökmotorer är aktiverat för`<environment-name>`** i projektinställningarna.

![Använd [!DNL Cloud Console] för att hantera miljöer](../../assets/robots-indexing-by-search-engine.png)

>[!NOTE]
>
>Om du använder PWA Studio och inte kan komma åt din konfigurerade `robots.txt` fil, lägga till `robots.txt` till [Namn på framsida, Tillåtelselista](https://github.com/magento/magento2-upward-connector#front-name-allowlist) på **Lager** > Konfiguration > **Allmänt** > **Webb** > Konfiguration av UPWARD PWA.
