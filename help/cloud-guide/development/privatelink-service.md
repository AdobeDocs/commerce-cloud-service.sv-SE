---
title: PrivateLink-tjänst
description: Lär dig hur du använder tjänsten PrivateLink för att upprätta en säker anslutning mellan en privat molnplattform och Adobe Commerce molnplattform i samma region.
feature: Cloud, Iaas, Security
exl-id: b25548b8-312b-4a74-b242-f4e2ac6cf945
source-git-commit: 5b52157c6c623bb4c765a2d545919df79d81f1da
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# PrivateLink-tjänst

Adobe Commerce i molninfrastrukturen har stöd för integrering med [AWS PrivateLink](https://aws.amazon.com/privatelink/) eller [Azure Private Link](https://learn.microsoft.com/en-us/azure/private-link/) service. Du kan använda PrivateLink för att upprätta säker, privat kommunikation mellan Adobe Commerce i molninfrastrukturmiljöer med tjänster och program som finns på externa system. Både Adobe Commerce-programmet och externa system måste vara tillgängliga via VPC-slutpunkter (Virtual Private Cloud) som konfigurerats på samma molnplattform (AWS eller Azure) inom samma molnregion.

>[!TIP]
>
>PrivateLink används bäst för att skydda anslutningar för icke-HTTP(S)-integreringar, som databaser eller filöverföringar. Om du tänker integrera ditt program med Adobe Commerce API:er kan du se hur du skapar en [Adobe API Mesh](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/) in _API-nät för Adobe Developer App Builder_.

## Funktioner och support

Integreringen av PrivateLink-tjänsten för Adobe Commerce i molninfrastrukturprojekt innehåller följande funktioner och support:

- En säker anslutning mellan en kund, VPC (Virtual Private Cloud) och Adobe VPC på samma molnplattform (AWS eller Azure) inom samma molnregion.
- Stöd för enkelriktad eller dubbelriktad kommunikation mellan slutpunktstjänster som finns på Adobe och kundens VPC:er.
- Tjänstaktivering:

   - Öppna nödvändiga portar i Adobe Commerce i molninfrastruktursmiljö
   - Upprätta den första anslutningen mellan kunden och Adobe VPC:er
   - Felsöka anslutningsproblem under aktivering

## Begränsningar

- Stöd för PrivateLink finns endast i Pro Production- och Staging-miljöer. Det är inte tillgängligt i lokala miljöer, integreringsmiljöer eller i Starter-projekt.
- Du kan inte upprätta SSH-anslutningar med PrivateLink. Se [Aktivera SSH-nycklar](secure-connections.md).
- Adobe Commerce support omfattar inte felsökning av AWS PrivateLink-problem utöver den initiala aktiveringen.
- Kunderna ansvarar för kostnaderna för att hantera sina egna VPC.
- Du kan inte använda HTTPS-protokollet (port 443) för att ansluta till Adobe Commerce i molninfrastrukturen via Azure Private Link på grund av [Insvepning med snabbt ursprung](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/faq/fastly-origin-cloaking-enablement-faq.html). Denna begränsning gäller inte AWS PrivateLink.
- PrivateDNS är inte tillgängligt.

## Anslutningstyper för PrivateLink

Det finns två typer av PrivateLink-anslutningar tillgängliga - vilket visas i följande nätverksdiagram - för att upprätta säker kommunikation mellan din butik och externa system som ligger utanför molnmiljön.

![PrivateLink-nätverksdiagram](../../assets/privatelink-architecture-diagram.png)

Välj en av de PrivateLink-anslutningstyper som passar bäst för din Adobe Commerce i molninfrastrukturmiljöer:

- **Enkelriktad PrivateLink**-Välj den här konfigurationen om du vill hämta data på ett säkert sätt från en Adobe Commerce i molninfrastrukturbutiken.
- **Dubbelriktad PrivateLink**-Välj den här konfigurationen för att upprätta säkra anslutningar till och från system utanför Adobe Commerce i molninfrastrukturmiljön. Dubbelriktat alternativ kräver två anslutningar:

   - En anslutning mellan kundens VPC och Adobe VPC
   - En anslutning mellan Adobe VPC och kundens VPC

>[!TIP]
>
>Kontakta nätverksadministratören eller molnplattformsleverantören för att få hjälp med att välja anslutningstypen PrivateLink eller hjälp med konfiguration och administration av VPC. Mer information finns i dokumentationen till PrivateLink för molnplattformen: [AWS PrivateLink](https://aws.amazon.com/privatelink/) eller [Azure Private Link](https://learn.microsoft.com/en-us/azure/private-link/).

## Begär aktivering av PrivateLink

>[!WARNING]
>
>Det kan ta upp till _fem_ arbetsdagar. Att tillhandahålla ofullständig eller felaktig information kan fördröja processen.

### Förutsättningar

![check](../../assets/fix.svg) Ett molnkonto (AWS eller Azure) i samma region som Adobe Commerce på molninfrastrukturinstansen.

![check](../../assets/fix.svg) En VPC i kundmiljön som är värd för tjänsterna som ska anslutas via PrivateLink. Läs AWS- eller Azure-dokumentationen om du behöver hjälp med VPC-installationen eller kontakta nätverksadministratören.

![check](../../assets/fix.svg) För dubbelriktade PrivateLink-anslutningar måste du skapa slutpunktstjänstkonfigurationen för ditt program eller din tjänst och skapa en slutpunkt i VPC-miljön innan du begär PrivateLink-aktivering. Se [Konfigurera för dubbelriktade PrivateLink-anslutningar](#set-up-for-bidirectional-privatelink-connections).

Samla in följande data som krävs för PrivateLink-aktivering:

- **Kontonummer för kundmolnet** (AWS eller Azure) - Måste finnas i samma region som Adobe Commerce på molninfrastrukturinstansen
- **Molnregion**—Ange den molnregion där kontot finns för verifieringsändamål
- **Tjänster och kommunikationsportar**—Adobe måste öppna portar för att aktivera tjänstkommunikation mellan VPC-datorer, till exempel SQL-port 3306, SFTP-port 222
- **Projekt-ID**- Ange Adobe Commerce för projekt-ID för molninfrastruktur. Du kan hämta projekt-ID och annan projektinformation med följande [Cloud CLI](../dev-tools/cloud-cli-overview.md) kommando: `magento-cloud project:info`
- **Anslutningstyp**—Ange enkelriktad eller dubbelriktad för anslutningstyp
- **Slutpunktstjänst**—För dubbelriktade PrivateLink-anslutningar anger du DNS-URL:en för VPC-slutpunktstjänsten som Adobe måste ansluta till, till exempel: `com.amazonaws.vpce.<cloud-region>.vpce-svc-<service-id>`
- **Tillgång till slutpunktstjänsten har beviljats**- Om du vill ansluta till en extern tjänst ger du slutpunktstjänsten åtkomst till följande AWS-kontokonto: `arn:aws:iam::402592597372:root`

  >[!WARNING]
  >
  >Om åtkomst till slutpunktstjänsten inte tillhandahålls är den dubbelriktade PrivateLink-anslutningen till tjänsten i din VPC **not** som försenar installationen.

#### Ytterligare krav som är specifika för aktivering av Azure Private Link

- Ange kluster-ID; med SSH loggar du in på fjärrkontrollen och använder kommandot: `cat /etc/platform_cluster`
- För att kunna ansluta en extern tjänst till ditt Adobe Commerce Pro-kluster behöver du:

   - En lista över portar i ditt Pro-kluster som ska visas för den nya externa privata slutpunkten
   - En lista över Azure-prenumerations-ID:n för privata slutpunktsanslutningar

- Om du vill ansluta ditt Adobe Commerce Pro-kluster till en extern tjänst behöver du:

   - En lista över resurs-ID:n för måltjänsterna. Tjänst-ID för extern privat länk ser ut ungefär så här:

  ```text
  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/privateLinkServices/{svcNameID}
  ```

### Arbetsflöde för aktivering

I följande arbetsflöde beskrivs aktiveringsprocessen för PrivateLink-integrering med Adobe Commerce i molninfrastrukturen.

1. **Kund** skickar en supportanmälan med begäran om PrivateLink-aktivering med ämnesraden `PrivateLink support for <company>`. Inkludera [data som krävs för aktivering](#prerequisites) i biljetten. Adobe använder supportbiljetten för att koordinera kommunikationen under aktiveringsprocessen.

1. **Adobe** ger åtkomst till slutpunktstjänsten i Adobe VPC via kundkontot.

   - Uppdatera slutpunktstjänstkonfigurationen för Adobe för att acceptera begäranden som initierats från kundens AWS- eller Azure-konto.
   - Uppdatera supportbiljetten för att ange tjänstnamnet för VPC-slutpunkten som Adobe ska ansluta till, till exempel `com.amazonaws.vpce.<cloud-region>.vpce-svc-<service-id>`.

1. **Kund** lägger till slutpunktstjänsten för Adobe i sitt molnkonto (AWS eller Azure), som utlöser en anslutningsbegäran till Adobe. Mer information finns i dokumentationen för molnplattformen:

   - För AWS, se [Acceptera och avvisa anslutningsbegäranden för gränssnittets slutpunkt].
   - För Azure, se [Hantera anslutningsbegäranden].

1. **Adobe** godkänner anslutningsbegäran.

1. Efter godkännande av anslutningsbegäran, **kunden** [verifierar anslutningen](#test-vpc-endpoint-service-connection) mellan deras VPC och Adobe VPC.

1. Ytterligare steg för att aktivera dubbelriktade anslutningar:

   - **Adobe** tillhandahåller kontots huvudnamn (rotanvändare för AWS- eller Azure-konton) i Adobe och begär åtkomst till kundens VPC-slutpunktstjänst.
   - **Kund** ger Adobe tillgång till slutpunktstjänsten i kundens VPC. Detta förutsätter att kontots huvudman på Adobe har åtkomst till `arn:aws:iam::402592597372:root`, enligt beskrivningen i **Tillgång till slutpunktstjänsten har beviljats** krav.

      - Uppdatera kundens slutpunktstjänstkonfiguration för att acceptera begäranden som initierats från Adobe-kontot. Mer information finns i dokumentationen för molnplattformen:

         - För AWS, se [Lägga till och ta bort behörigheter för slutpunktstjänsten].
         - För Azure, se [Hantera en privat slutpunktsanslutning]

      - Ange slutpunktstjänstens namn för kundens VPC för Adobe.

   - **Adobe** lägger till kundslutpunktstjänsten i Adobe-plattformskonto (AWS eller Azure), som utlöser en anslutningsbegäran till kundens VPC.
   - **Kund** godkänner anslutningsbegäran från Adobe för att slutföra konfigurationen.
   - **Kund** [verifierar anslutningen](#test-vpc-endpoint-service-connection) från Adobe VPC.

## Testa VPC-slutpunktsanslutning

Du kan använda Telnet-programmet för att testa anslutningen till VPC-slutpunktstjänsten.

**Testa anslutningen till VPC-slutpunktstjänsten**:

1. Från projektets rotkatalog **checka ut** Staging- eller produktionsmiljön som konfigurerats för åtkomst till PrivateLink-slutpunktstjänsten.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. Kör följande CURL-kommando:

   ```bash
   curl -v telnet://<endpoint-service-dns-url>:<port>/
   ```

   Exempel:

   ```terminal
   $ curl -v telnet://vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce.amazonaws.com:80 -vvv
   ```

   Exempel på lyckat svar:

   ```terminal
   * Rebuilt URL to: telnet://vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce.amazonaws.com:80
   * Connected to vpce-0088d56482571241d-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce. amazonaws.com (191.210.82.246) port 80 (#0)
   ```

   Samplingssvaret misslyckades:

   ```terminal
   Failed to connect to vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.ap-southeast-1.vpce.amazonaws.com port 80: Connection timed out
   * Closing connection 0
   ```

1. Kontrollera att tjänsten lyssnar på VM.

   ```bash
   netstat -na | grep <port>
   ```

1. Kontrollera paketflödet.

   ```bash
   tcpdump -i <ethernet-interface> -tt -nn port <destination-port> and host <source-host>
   ```

   Kontrollera följande interna inställningar för att säkerställa att konfigurationen är giltig:

   - Inställningar för slutpunkts- och slutpunktstjänster
   - NLB-inställningar (Network Load Balancer)
   - Målgrupperna i NLB och verifiera att de är felfria
   - URL för netcat/curl-slutpunkt från varje virtuell dator (visas ovan)

   I följande artiklar finns hjälp med att felsöka anslutningsproblem:

   - [AWS: Felsöka anslutningar till slutpunktstjänster]
   - [Amazon: Felsökning av anslutningsproblem med Azure Private Link]

   Om du inte kan åtgärda felen kan du uppdatera Adobe Commerce supportanmälan och be om hjälp med att upprätta anslutningen.

## Ändra konfiguration för PrivateLink

[Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om du vill ändra en befintlig PrivateLink-konfiguration. Du kan till exempel begära ändringar enligt följande:

- Ta bort PrivateLink-anslutningen från Adobe Commerce i molninfrastrukturen Pro Production eller Staging-miljön.
- Ändra kundens Cloud-plattformskontonummer för åtkomst till slutpunktstjänsten i Adobe.
- Lägg till eller ta bort PrivateLink-anslutningar från Adobe VPC till andra slutpunktstjänster som är tillgängliga i kundens VPC-miljö.

## Konfigurera för dubbelriktade PrivateLink-anslutningar

Kund-VPC måste ha följande resurser tillgängliga för stöd av dubbelriktade PrivateLink-anslutningar:

- En NLB (Network Load Balancer)
- En slutpunktstjänstkonfiguration som ger åtkomst till ett program eller en tjänst från kundens VPC
- An [gränssnittsslutpunkt] (AWS) eller [privat slutpunkt] (Azure) som gör att Adobe kan ansluta till slutpunktstjänster på din VPC

Om dessa resurser inte är tillgängliga i kundens VPC måste du logga in på ditt molnplattformskonto för att lägga till konfigurationen.

- Amazon VPC-konsol- `https://console.aws.amazon.com/vpc/`
- Azure-portal- `https://portal.azure.com`

Se dokumentationen för molnplattformen för konfigureringsinstruktioner för PrivateLink:

- **AWS PrivateLink-dokumentation**
   - [Skapa en utjämning för nätverksbelastning]
   - [Skapa en konfiguration för slutpunktstjänsten]
   - [Skapa en gränssnittsslutpunkt]
   - [Livscykel för gränssnittets slutpunkt]

- **Azure PrivateLink-dokumentation**
   - [Skapa en belastningsutjämnare]
   - [Arbetsflöde för Azure Private Link]

<!--Link definitions-->

[Acceptera och avvisa anslutningsbegäranden för gränssnittets slutpunkt]: https://docs.aws.amazon.com/vpc/latest/userguide/accept-reject-endpoint-requests.html
[Lägga till och ta bort behörigheter för slutpunktstjänsten]: https://docs.aws.amazon.com/vpc/latest/userguide/add-endpoint-service-permissions.html
[Amazon: Felsökning av anslutningsproblem med Azure Private Link]: https://docs.microsoft.com/en-us/azure/private-link/troubleshoot-private-link-connectivity
[AWS: Felsöka anslutningar till slutpunktstjänster]: https://aws.amazon.com/premiumsupport/knowledge-center/connect-endpoint-service-vpc/
[Arbetsflöde för Azure Private Link]: https://docs.microsoft.com/en-us/azure/private-link/private-link-service-overview#workflow
[Skapa en belastningsutjämnare]: https://docs.microsoft.com/en-us/azure/load-balancer/quickstart-load-balancer-standard-public-portal
[Skapa en utjämning för nätverksbelastning]: https://docs.aws.amazon.com/elasticloadbalancing/latest/network/create-network-load-balancer.html
[Skapa en konfiguration för slutpunktstjänsten]: https://docs.aws.amazon.com/vpc/latest/userguide/create-endpoint-service.html
[Skapa en gränssnittsslutpunkt]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#create-interface-endpoint
[interface endpoint lifecycle]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#vpce-interface-lifecycle
[gränssnittsslutpunkt]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html
[Hantera en privat slutpunktsanslutning]: https://docs.microsoft.com/en-us/azure/private-link/manage-private-endpoint
[Hantera anslutningsbegäranden]: https://docs.microsoft.com/en-us/azure/private-link/private-link-service-overview#manage-your-connection-requests
[privat slutpunkt]: https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview
