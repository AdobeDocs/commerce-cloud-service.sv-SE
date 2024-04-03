---
title: Teknikstack
description: Se vilken teknologi som utgör Commerce on Cloud-infrastrukturen.
feature: Cloud, Iaas, Paas
exl-id: e456db25-c44b-4053-b96d-517d3d1606d0
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# Teknikstack

Tänk dig Adobe Commerce i molninfrastrukturen som fem funktionella lager, vilket visas nedan:

![Molnhög](../../assets/CloudStack.svg)

1. [**Molninfrastruktur**](pro-architecture.md): Välj antingen Amazon Web Services (AWS) eller Microsoft Azure som en grund för din infrastruktur som en tjänst (IaaS) för dina Adobe Commerce i projekt för molninfrastrukturproffs.

   Adobe analyserar rutinmässigt användningen av din virtuella datorresurs (vCPU) och allokerar automatiskt resurser för att optimera din långtidsanvändning och minska risken för att överskrida din högsta årliga daggräns för vCPU. Om du förväntar dig ökad webbplatstrafik under en viss tidsperiod måste du fortsätta att öppna en supportanmälan för att [begär en tillfällig storlek](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-request-temporary-magento-upsize.html).

1. [**Plattform som tjänst**](cloud-architecture.md): Varje Adobe Commerce-projekt för molninfrastruktur tillhandahåller en plattformsintegreringsmiljö (PaaS) för utveckling, testning och integrering av tjänster.
1. [**Adobe Commerce**](../project/overview.md): Adobe Commerce i molninfrastruktur erbjuder en förprovisionerad infrastruktur som omfattar PHP, MySQL (MariaDB), Redis, [!DNL RabbitMQ]och de sökmotortekniker som stöds.
1. [**Resultatverktyg**](../monitor/new-relic-service.md): Med New Relic prestandaverktyg kan du felsöka, övervaka och hantera program och infrastrukturer genom att samla in, analysera och visa data från Adobe Commerce i molninfrastrukturprojekt.
1. [**CDN (Content Delivery Network), Brandvägg för webbaserade program ([!DNL WAF]) och Bildoptimering (IO)**](../cdn/fastly.md):

   * [Snabb CDN](../cdn/fastly.md#ddos-protection)—Tillhandahåller säkra CDN-tjänster med inbyggt skydd mot DDoS-attacker (Distributed Denial of Service) som [!DNL Ping of Death], [!DNL Smurf] och andra ICMP-baserade (Internet Control Message Protocol) översvämningsattacker.
   * [Brandvägg för webbaserade program (WAF)](../cdn/fastly-waf-service.md)—WAF-tjänsterna garanterar PCI-kompatibilitet för Adobe Commerce-butiker i produktionsmiljöer och WAF-principer som skyddar dina Adobe Commerce webbapplikationer från injektionsangrepp, skadlig inmatning, serveröverskridande skriptning, dataexfiltrering, HTTP-protokollöverträdelser och andra [[!DNL OWASP] De 10 viktigaste säkerhethoten](https://owasp.org/www-project-top-ten/).
   * [Bildoptimering (IO)](../cdn/fastly-image-optimization.md)- Ger redigering och optimering i realtid av bilder för snabbare bildleverans och enklare underhåll av uppsättningar bildkällor för responsiva webbapplikationer. I/O-funktionen avlastar snabbt bildbearbetning och storleksändring, vilket frigör servrar så att de kan bearbeta beställningar och konverteringar effektivt.

Monolitiska applikationer är resurskrävande och svåra att skala och fungerar snabbt. Med Cloud-infrastrukturen får Commerce-kunder oöverträffad tillgång till SaaS-baserade mikrotjänster som är avancerade, intelligenta och prestandaoptimerade. Se [Programvara och tjänster som stöds](cloud-architecture.md#supported-software-and-services).

Använd [Guiden Komma igång med Commerce](../../get-started/overview.md) för att konfigurera ditt nya Cloud-program och börja hantera dina [!DNL Commerce] i en molnbaserad miljö.
