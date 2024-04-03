---
title: Brandväggsegenskap
description: Se exempel på hur du konfigurerar brandväggsegenskapen i konfigurationsfilen för Commerce-programmet.
feature: Cloud, Configuration, Security
exl-id: f169c008-c62a-41b7-a98d-cccd81c7291a
source-git-commit: 74d88560db3b65294673a1e1827f9cea098d707a
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# Brandväggsegenskap

>[!IMPORTANT]
>
>Endast startprojekt

För Starter-projekt finns `firewall` egenskapen lägger till en _utgående_ brandväggen till programmet. Den här brandväggen påverkar inte inkommande begäranden. Den definierar vilken `tcp` utgående förfrågningar kan _lämna_ en Adobe Commerce webbplats. Detta kallas för egresfiltrering. Den utgående brandväggen filtrerar det som kan gå ur - gå ut eller fly från webbplatsen. Genom att begränsa vad som kan kringgås läggs ett kraftfullt säkerhetsverktyg till på servern.

## Standardbegränsningsprinciper

Brandväggen innehåller två standardprinciper som styr utgående trafik: `allow` och `deny`. The `allow` policy _tillåter_ all utgående trafik som standard. Och `deny` policy _förnedrande_ all utgående trafik som standard. Men när du lägger till en regel åsidosätts standardprincipen och brandväggen blockeras **alla** utgående trafik tillåts inte av regeln.

För Starter-planer är standardprincipen inställd på `allow`. Med den här inställningen kan du vara säker på att all utgående trafik inte blockeras förrän du lägger till regler för utgående filtrering. Standardprincipen kan anges till `deny` på begäran.

**Så här kontrollerar du standardprofilen**:

```bash
magento-cloud p:curl --project PROJECT_ID /settings | grep -i outbound
```

Om du inte har begärt det `deny` för din profil bör kommandot visa din princip som `allow`:

```terminal
"outbound_restrictions_default_policy": "allow"
```

>[!NOTE]
>
>**Nyckeltagning**: När du lägger till en utgående regel blockerar du all utgående trafik förutom de domäner, IP-adresser eller portar som du lägger till i regeln. Därför är det viktigt att ha en fullständig utgående lista definierad och testad innan du lägger till den på produktionsplatsen.

## Brandväggsalternativ

Följande exempelkonfiguration i `.magento.app.yaml` filen visar alla `firewall` alternativ som du kan använda för att lägga till regler för urklippsfiltrering.

```yaml
firewall:
    outbound:
        - # Common accessed domains
            domains:
                - newrelic.com
                - fastly.com
                - magento.com
                - magentocommerce.com
                - google.com
            ports:
                - 80
                - 443
            protocol: tcp # Can be omitted from rules.

        - # Adobe Stock integration
            domains:
                - account.adobe.com
                - stock.adobe.com
                - console.adobe.io
            ports:
                - 80
                - 443

        - # Payment services
            domains:
                - braintreepayments.com
                - paypal.com
            ports:
                - 80
                - 443

        - # Shipping services
            domains:
                - ups.com
                - usps.com
                - fedex.com
                - dhl.com
            ports:
                - 80
                - 443

        - # Vertex Integrated Address Cleansing
            domains:
                - mgcsconnect.vertexsmb.com
            ports:
                - 80
                - 443

        - # New Relic networks
            ips:
                - 162.247.240.0/22 # US region accounts
                - 185.221.84.0/22 # EU region accounts
            ports:
                - 443

        - # New Relic endpoints
            domains:
                - collector.newrelic.com, # US region accounts
                - collector.eu01.nr-data.net # EU region accounts
            ports:
                - 443

        - # Fastly IP ranges
            ips:
                - 23.235.32.0/20
                - 43.249.72.0/22
                - 103.244.50.0/24
                - 103.245.222.0/23
                - 103.245.224.0/24
                - 104.156.80.0/20
                - 146.75.0.0/16
                - 151.101.0.0/16
                - 157.52.64.0/18
                - 167.82.0.0/17
                - 167.82.128.0/20
                - 167.82.160.0/20
                - 167.82.224.0/20
                - 172.111.64.0/18
                - 185.31.16.0/22
                - 199.27.72.0/21
                - 199.232.0.0/16
            ports:
                - 80
                - 443
```

## Regler för filtrering av ägg

Konfigurationer för utgående brandvägg består av regler. Du kan definiera så många regler du behöver. Kraven för reglerna är följande.

**Varje regel:**

- Måste börja med ett bindestreck (`-`). Om du lägger till en kommentar på samma rad blir det lättare att dokumentera och visuellt skilja en regel från nästa.
- Måste definiera minst ett av följande alternativ: `domains`, `ips`, eller `ports`.
- Måste använda `tcp` -protokoll. Eftersom det här är standardprotokollet för alla regler kan du utesluta det från regeln.
- Kan definiera `domains` eller `ips`, men inte båda i samma regel.
- Kan innehålla `yaml` kommentarer (`#`) och radbrytningar för att organisera vilka domäner, IP-adresser och portar som tillåts.

För varje regel används följande egenskaper:

### `domains`

The `domains` tillåter en lista med fullständigt kvalificerade domännamn (FQDN).

Om en regel definierar `domains` men inte `ports`tillåter brandväggen domänförfrågningar på alla portar.

### `ips`

The `ips` tillåter en lista med IP-adresser i CIDR-notationen. Du kan ange enskilda IP-adresser eller intervall med IP-adresser.

Lägg till `/32` CIDR-prefix till slutet av din IP-adress:

```terminal
172.217.11.174/32  # google.com
```

Använd kommandot [IP-intervall till CIDR](https://ipaddressguide.com/cidr) kalkylator.

Om en regel definierar `ips` men inte `ports`tillåter brandväggen IP-begäranden på alla portar.

### `ports`

The `ports` kan användas med en lista över portar mellan 1 och 65535. För de flesta regler i exemplet, portar `80` och `443` tillåter både HTTP- och HTTPS-begäranden. Men för New Relic tillåter reglerna bara åtkomst till domäner och IP-adresser på port `443`, vilket rekommenderas i New Relic-dokumentationen för [Nätverkstrafik](https://docs.newrelic.com/docs/new-relic-solutions/get-started/networks/#agents).

Om en regel bara definierar `ports`tillåter brandväggen åtkomst till alla domäner och IP-adresser för de definierade portarna.

>[!NOTE]
>
>Port `25`, den SMTP-port som ska skicka e-post blockeras alltid, utan undantag.

### `protocol`

Som vi nämnt är TCP standard och endast tillåtet protokoll för regler. UDP och dess portar tillåts inte. Därför kan du utelämna `protocol` från alla regler. Om du vill ta med den ändå måste du ange värdet till `tcp`, vilket visas i exemplets första regel.

## Söker efter domännamn som ska tillåtas

Använd följande kommando för att tolka serverns `dns.log` och visa en lista över alla DNS-begäranden som din plats har loggat:

```shell
awk '($5 ~/query/)' /var/log/dns.log | awk '{print $6}' | sort | uniq -c | sort -rn
```

Det här kommandot visar även DNS-begäranden som har gjorts men blockerats av reglerna för filtrering av urkunder. Utdata visar inte vilka domäner som blockerades, bara de som begärdes. Utdata visar inte begäranden som gjorts med en IP-adress.

```terminal
Example output:

97 magento.com
93 magentocommerce.com
88 google.com
70 metadata.google.internal.0
70 metadata.google.internal
65 newrelic.com
56 fastly.com
17 mcprod-0vunku5xn24ip.ap-4.magentosite.cloud
6 advancedreporting.rjmetrics.com
```

Domäner är, till skillnad från IP-adresser, vanligtvis mer specifika och säkra för offresfiltrering. Om du till exempel lägger till en IP-adress för en tjänst som använder ett CDN, tillåter du IP-adressen för CDN, som kan användas av hundratals eller tusentals andra domäner. Med en IP-adress kan du tillåta utgående åtkomst till tusentals andra servrar.

## Testa regler för gruppfiltrering

När du har samlat in och konfigurerat åtkomstregler för de domäner och IP-adresser som din webbplats behöver är det dags att trycka och testa.

Så här testar du regler för filtrering av utgångar:

1. Skapa ett gränssnittsskript för `curl` -kommandon för att komma åt domänerna och IP-adresserna i reglerna. Inkludera kommandon som testar åtkomst till domäner och IP-adresser som ska blockeras.

1. Konfigurera en `post_deploy` krok i din `.magento.app.yaml` fil som ska köra skriptet.

1. Tryck `firewall` konfiguration och testskript för `integration` gren.

1. Undersök `post_deploy` från `curl` kommandon.

1. Förfina `firewall` regler, uppdatera `curl` skript, implementera, push och upprepa.

### `curl` skriptexempel

```shell
# curl-tests-for-egress-filtering.sh

# Use the -v option to display connection details

# Check domain access
curl -v newrelic.com
curl -v fastly.com
curl -v magento.com
curl -v magentocommerce.com
curl -v google.com
curl -v account.adobe.com
curl -v stock.adobe.com
curl -v console.adobe.io
curl -v braintreepayments.com
curl -v paypal.com
curl -v ups.com
curl -v usps.com
curl -v fedex.com
curl -v dhl.com
curl -v devdocs.magento.com

# Check domain denials
curl -v amazon.com
curl -v facebook.com
curl -v twitter.com

# IP address access
...

# IP address denials
...
```

### `post_deploy` exempel

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: "php ./vendor/bin/ece-tools run scenario/deploy.xml\n"
    post_deploy: |
        set -e
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
        echo "[$(date)] post-deploy hook end"
        ./curl-tests-for-egress-filtering.sh
        echo "[$(date)] curl finished"
```
