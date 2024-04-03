---
title: Brandvägg för webbaserade program (WAF)
description: Lär dig hur tjänsten Fast WAF identifierar, loggar och blockerar trafik för skadliga förfrågningar innan den kan skada Adobe Commerce nätverk eller webbplatser.
feature: Cloud, Configuration, Security
exl-id: 40bfe983-7f32-4155-ae77-7cd18866f6e2
source-git-commit: 6b01bf91c3bf63ba268d0f8e10e19db4cb355997
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# Brandvägg för webbaserade program (WAF)

Tjänsten WAF (web application firewall) för Adobe Commerce i molninfrastruktur tillhandahålls av Fastly och identifierar, loggar och blockerar trafik för skadliga förfrågningar innan den kan skada dina webbplatser eller ditt nätverk. Tjänsten WAF är endast tillgänglig i produktionsmiljöer.

Tjänsten WAF ger följande fördelar:

- **PCI-kompatibilitet**—WAF-aktivering säkerställer att Adobe Commerce storefront i produktionsmiljöer uppfyller PCI DSS 6.6-säkerhetskraven.
- **Standardprincip för WAF**- Standardprincipen för WAF, som konfigurerats och underhålls av Fastly, innehåller en samling säkerhetsregler som är skräddarsydda för att skydda dina Adobe Commerce webbapplikationer från en mängd olika attacker, inklusive injektionsangrepp, skadliga indata, serveröverskridande skriptning, dataexfiltrering, HTTP-protokollöverträdelser och andra [OWASP Top Ten](https://owasp.org/www-project-top-ten/) säkerhetshot.
- **WAF-introduktion och -aktivering**—Adobe distribuerar och aktiverar standardprincipen för WAF i produktionsmiljön inom 2 till 3 veckor efter det att etableringen är klar.
- **Drifts- och underhållsstöd**—
   - Adobe och Konfigurera och hantera snabbt loggar och aviseringar för tjänsten WAF.
   - Adobe gör kundsupportärenden relaterade till WAF-servicefrågor som blockerar legitim trafik som Priority 1-frågor.
   - Automatiserade uppgraderingar till WAF-versionen säkerställer omedelbar täckning för nya eller kommande utnyttjanden. Se [Underhåll och uppgraderingar av WAF](#waf-maintenance-and-updates).

>[!TIP]
>
>Mer information om hur du underhåller PCI-kompatibiliteten för din Adobe Commerce i molninfrastrukturbutiker finns i [PCI-kompatibilitet](https://business.adobe.com/products/magento/pci-compliance.html).

## Aktivera WAF

Adobe aktiverar WAF-tjänsten på nya konton inom 2 till 3 veckor efter det att etableringen är klar. WAF implementeras via tjänsten Fast CDN. Du behöver inte installera eller underhålla någon maskin- eller programvara.

>[!NOTE]
>
>Innan du kan använda WAF-tjänsten måste all extern trafik till ditt Adobe Commerce i molninfrastrukturprojekt gå via tjänsten Snabbt. Se [Konfigurera snabbt](fastly-configuration.md).

## Så här fungerar det

WAF-tjänsten integreras med Fast och använder cachelogiken i tjänsten Fast CDN för att filtrera trafiken på de snabbt globala noderna. Vi aktiverar tjänsten WAF i produktionsmiljön med en standardprincip för WAF baserad på [ModSecurity Rules från Trustwave SpiderLabs](https://github.com/owasp-modsecurity/ModSecurity) och OWASP De 10 viktigaste säkerhetshot.

WAF-tjänsten filtrerar HTTP- och HTTPS-trafik (GET- och POST-förfrågningar) mot WAF-regeluppsättningen och blockerar trafik som är skadlig eller som inte följer specifika regler. Tjänsten filtrerar endast ursprunglig trafik som försöker uppdatera cachen. Därför stoppar vi de flesta attackerna på snabbcachen och skyddar era urkunder från skadliga attacker. Genom att endast bearbeta ursprungstrafik bevarar WAF-tjänsten cacheprestanda, vilket innebär att endast uppskattningsvis 1,5 millisekunder till 20 millisekunder fördröjning för varje begäran som inte cache-lagras.

## Felsöka blockerade begäranden

När WAF-tjänsten är aktiverad filtreras all webb- och administratörstrafik mot WAF-reglerna och blockerar alla webbförfrågningar som utlöser en regel. När en begäran blockeras ser den begärande en standardinställning `403 Forbidden` felsida som innehåller ett referens-ID för blockeringshändelsen.

![WAF-felsida](../../assets/cdn/fastly-waf-403-error.png)

Du kan anpassa den här felsvarssidan från Admin. Se [Anpassa svarssidan för WAF](fastly-custom-response.md#customize-the-waf-error-page).

Om Adobe Commerce administratörssida eller butik returnerar en `403 Forbidden` felsida som svar på en giltig URL-begäran, skicka en [Adobe Commerce Support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). Kopiera referens-ID:t från felsvarssidan och klistra in det i biljettbeskrivningen.

## Underhåll och uppdateringar av WAF

Underhåller och uppdaterar snabbt WAF-reglerna baserat på regeluppdateringar från kommersiella tredje parter, snabbforskning och öppna källor. Uppdaterar snabbt de publicerade reglerna till en policy efter behov eller när ändringar av reglerna är tillgängliga från deras respektive källor. Fast kan också lägga till regler som matchar de publicerade klasserna av regler i WAF-instansen för alla tjänster när WAF-tjänsten har aktiverats. Uppdateringarna säkerställer omedelbar täckning för nya eller föränderliga explosioner.

Hantera uppdateringsprocessen i Adobe och Snabbt för att säkerställa att nya eller ändrade WAF-regler fungerar effektivt i produktionsmiljön innan uppdateringarna distribueras i blockeringsläge.

## Begränsningar

Standardtjänsten för WAF som drivs av Fastly stöder inte följande funktioner:

- Skydd mot skadlig kod eller robotskydd - Överväg att använda [åtkomstkontrollistor](./fastly-vcl-allowlist.md) eller en tredjepartstjänst.
- Hastighetsbegränsning - Se [Hastighetsbegränsning](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/RATE-LIMITING.md) i Snabbt-dokumentationen eller se [Hastighetsbegränsning](https://developer.adobe.com/commerce/webapi/get-started/rate-limiting/) i _Commerce Web API_ säkerhetssektion.
- Konfigurera en slutpunkt för loggning för kund - se [PrivateLink-tjänst](../development/privatelink-service.md) som ett alternativ.

Även om du inte kan blockera eller tillåta trafik baserat på IP-adresser i tjänsten WAF kan du lägga till åtkomstkontrollistor (ACL) och anpassade VCL-fragment till tjänsten Snabbt för att ange IP-adresser och VCL-logik för att blockera eller tillåta trafik. Se [Anpassade VCL-fragment snabbt](fastly-vcl-custom-snippets.md).

Filtrering för TCP-, UDP- eller ICMP-begäranden stöds inte av WAF-tjänsten. Den här funktionen tillhandahålls dock av det inbyggda DDoS-skyddet som ingår i tjänsten Fast CDN. Se [DDoS-skydd](fastly.md#ddos-protection).
