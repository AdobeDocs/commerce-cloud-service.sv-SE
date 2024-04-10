---
title: Utvecklingsöversikt
description: Förbered dig för lokal utveckling med ett Adobe Commerce-projekt för molninfrastruktur.
role: Developer
feature: Cloud, Install
topic: Development
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: d4452d7d-d3dc-4f8d-8bd7-76f05d89f545
source-git-commit: 99272d08a11f850a79e8e24857b7072d1946f374
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Utvecklingsöversikt

Adobe Commerce i molnbaserade miljöer **Skrivskyddad**, inklusive alla Starter-miljöer och alla Pro-integrerings-, staging- och produktionsmiljöer. I en lokal utvecklingsmiljö kan du skriva och testa kod innan du skickar den till en integreringsmiljö för ytterligare testning och driftsättning till Förproduktion och Produktion.

Innan du förbereder din lokala arbetsyta bör du kontrollera att du har [autentiseringsuppgifter](../../get-started/prepare-workspace.md). Lokal utveckling kräver installation av PHP och Composer såvida du inte väljer att använda [Cloud Docker for Commerce](#docker-environment).

## Obligatoriska paket

Adobe Commerce i molninfrastruktur använder Composer för att hantera beroenden och uppgraderingar för projekt. För lokal utveckling måste du installera de PHP- och Composer-versioner som är kompatibla med ditt Cloud-projekt. Om du till exempel använder [!DNL Commerce] 2.4.7-molnmallen [`.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/2.4.7/.magento.app.yaml) konfigurationsfilen använder **PHP 8.3** och **Composer 2.7.2**.

Composer installerar nödvändiga bibliotek och beroenden för ditt projekt i `vendor` katalog. Följande Composer-filer som krävs finns i projektets rotkatalog:

- `composer.json`—Använd `composer.json` fil för att hantera produktinstallationer och uppgraderingar.
- `composer.lock`—The `composer.lock` filen lagrar en uppsättning exakta versionsberoenden som uppfyller versionsbegränsningarna för varje paket i projektets beroendeträd.

**Vanliga kommandon:**

| Kommando | Beskrivning |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `composer update` | Uppdateringar av de senaste versionerna av beroendena som visas i `composer.json` -fil. Detta uppdaterar `composer.lock` -fil. |
| `composer install` | Läser `composer.lock` fil för att hämta beroenden. Det är en god vana att hålla en uppdaterad kopia av `composer.lock` i projektarkivet. |

{style="table-layout:auto"}

När du lägger till, implementerar och skickar den uppdaterade koden körs distributionsprocessen automatiskt i `composer install` under [byggfas](../deploy/process.md#build-phase-build-phase).

### Cloud-metapaket

Adobe Commerce i molninfrastrukturen använder ett metapaket som kräver `magento/product-enterprise-edition`. Använd följande begränsningssyntax för att hämta de senaste uppdateringarna för den senaste versionen av Commerce:

```text
>=current_version <next_version
```

Om du till exempel vill använda den senaste versionen av Adobe Commerce 2.4.7 anger du `2.4.7` som den&quot;aktuella&quot; versionen och `2.4.8` som nästa version i `composer.json` fil:

```text
"magento/magento-cloud-metapackage": ">=2.4.7 <2.4.8"
```

Huvudpaketen i det här metapaketet är följande:

- **vendor/magento/ece-tools**—The `ece-tools` paketet är kompatibelt med Adobe Commerce version 2.1.4 och senare för att ge dig en mängd funktioner du kan använda för att hantera din Adobe Commerce i molninfrastrukturprojekt. Det innehåller skript och Adobe Commerce på molninfrastrukturskommandon som är utformade för att hantera koden och automatiskt bygga och driftsätta dina projekt. Se [`ece-tools` paketöversikt](../dev-tools/package-overview.md).
- **vendor/magento/product-enterprise-edition**—Det här metapaketet kräver programkomponenter som moduler, ramverk, teman med mera.
- **vendor/fast2/magento2**- Den här modulen hanterar Snabbt CDN och tjänster för Pro Staging and Production och Starter Production. Se [Snabba tjänster](/help/cloud-guide/cdn/fastly.md#fastly-cdn-module-for-magento-2).
- **vendor/magento/module-paypal-on-boarding**- Den här modulen erbjuder PayPal-betalningsgateway-utcheckning genom att ansluta till ditt PayPal-handelskonto. Se [PayPal On-Boarding-verktyg](../store/paypal.md).

>[!TIP]
>
>Se [Molnpaket för Adobe Commerce](/help/cloud-guide/release-notes/cloud-packages.md) i _Versionsinformation för Commerce_ för en lista över beroenden och tredjepartslicenser.

## Dockningsmiljö

Du kan använda verktyget Cloud Docker for Commerce för att emulera Adobe Commerce i molninfrastruktursproduktions- och utvecklingsmiljöer för lokal utveckling. PHP och Composer behöver inte installeras lokalt i molndockningsprogrammet för Commerce.

- [Lokal utveckling med Cloud Docker](https://developer.adobe.com/commerce/cloud-tools/docker/setup/) på Adobe Developer webbplats
- [Dockningsarkitektur och vanliga kommandon](../dev-tools/cloud-docker.md)
- [Versionsinformation om Cloud Docker](../release-notes/cloud-docker.md)

>[!TIP]
>
>Mer information om hur du använder Git-baserade värdtjänster med Adobe Commerce för molninfrastruktur finns i [Integreringar](../integrations/overview.md).
