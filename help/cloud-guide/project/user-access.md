---
title: Hantera användaråtkomst
description: Lär dig hur du hanterar användaråtkomst till Adobe Commerce i molninfrastrukturprojekt och -miljöer.
role: Admin
feature: Cloud, Roles/Permissions
last-substantial-update: 2023-06-27T00:00:00Z
topic: Security
exl-id: 3357a3ea-bf86-4a65-95d1-6b24f1152248
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 0%

---

# Hantera användaråtkomst

Adobe Commerce-projekt om molninfrastruktur använder rollbaserad åtkomst. Det finns två tillgängliga roller på projektnivå:

- **Projektadministratör**—Skriva åtkomst till alla projektmiljöer och hantera användare, push-kod och uppdatera projektinställningar.
- **Projektvisningsprogram**—Åtkomst endast för visning till alla projektmiljöer.

Projektvisningsprogram kan inte utföra åtgärder i någon miljö, men du kan ge projektvisningsprogram skrivåtkomst till en viss miljötyp.

Åtkomst på miljönivå baseras på miljötypen: produktion, staging och utveckling. Bevilja en användare _visningsprogram_ behörighet att _utveckling_ miljöer innebär att de kan visa **alla** projektmiljöer. I följande tabell klargörs vilka möjligheter som ges för varje behörighetsnivå:

| Behörighetsnivå | Åtkomst | SSH-åtkomst |
| ------------------ | ----------- | :----------: |
| **Administratör** | Utföra administratörsuppgifter, t.ex. ändra inställningar, push-kod, utföra uppgifter och grenhantering, inklusive sammanfogning med den överordnade miljön | Ja |
| **Medarbetare** | Kodning och förgreningar i miljön - det går inte att ändra inställningar eller utföra åtgärder | Ja |
| **Visningsprogram** | Åtkomst endast för visning till miljötypen | Nej |
| **Ingen åtkomst** | Ingen åtkomst till miljötypen | Nej |

{style="table-layout:auto"}

Med hjälp av `magento-cloud` CLI eller [!DNL Cloud Console].

>[!BEGINSHADEBOX]

**Förutsättningar:**

- En registrerad användare hos en Adobe ID. En användare måste [register för ett Adobe-konto](https://account.adobe.com) och sedan [initiera sitt molnkonto](https://console.adobecommerce.com) innan du kan lägga till dem i ett Cloud-projekt.
- En användare som har tilldelats **Administratör** rollen inte kan hantera användare med `magento-cloud` CLI. Endast användare som har tilldelats **Kontoägare** kan hantera användare.

>[!ENDSHADEBOX]

## Hantera användare med CLI

Använd `magento-cloud` CLI för att hantera användare och integrera med automatiserade system:

- `magento-cloud user:add`-lägg till en användare i projektet
- `magento-cloud user:delete`-ta bort en användare
- `magento-cloud user:list [users]`-lista projektanvändare
- `magento-cloud user:role`-visa eller ändra användarrollen
- `magento-cloud user:update`-uppdatera användarroll i ett projekt

I följande exempel används `magento-cloud` CLI för att lägga till en användare, konfigurera roller, ändra projekttilldelningar och tilldela användarroller.

**Lägga till en användare och tilldela roller**:

1. Använd `magento-cloud` CLI för att lägga till användaren.

   ```bash
   magento-cloud user:add
   ```

   >[!IMPORTANT]
   >
   >Användaren måste ha en Adobe ID; se [krav](#add-users-and-manage-access).

1. Följ anvisningarna: ange användarens e-postadress, ange projekt- och miljörollerna och lägg till användaren.

   > Exempeluppmaningar

   ```terminal
   Enter the user's email address: alice@example.com
   
   Email address: alice@example.com
   
   The user's project role can be admin (a) or viewer (v).
   
   Project role (default: viewer) [a/v]: viewer
   
   The user's environment type role(s) can be admin (a), viewer (v), contributor (c) or none (n).
   
   Role on type development (default: none) [a/v/c/n]: none
   Role on type production (default: none) [a/v/c/n]: admin
   Role on type staging (default: none) [a/v/c/n]: admin
   
   Adding the user alice@example.com to (project_id):
   Project role: viewer
     Role on type production: admin
     Role on type staging: admin
   
   Are you sure you want to add this user? [Y/n] y
   Adding the user to the project
   ```

   När du har lagt till användaren skickar Adobe ett e-postmeddelande till den angivna adressen med instruktioner om hur du får åtkomst till Adobe Commerce i molninfrastrukturprojektet.

### Visa en användares projektroll

```bash
magento-cloud user:get alice@example.com
```

>Exempelsvar:

```terminal
Current role(s) of User (alice@example.com) on Production (project_id):
  Project role: admin
```

### Lägga till en användare i flera miljöer

Lägga till en användare som `viewer` på en `Production` miljö, och som `contributor` på en `Integration` miljö:

```bash
magento-cloud user:add alice@example.com -r production:v -r integration:c
```

### Uppdatera behörigheter för användarmiljö

Så här uppdaterar du användarmiljöbehörigheter till `admin` på `Production` miljö:

```bash
magento-cloud user:update alice@example.com -r production:a
```

## Hantera användare från [!DNL Cloud Console]

Du kan använda [[!DNL Cloud Console]](../../get-started/cloud-console.md) för att lägga till behörigheter och använda _Redigera_ om du vill ändra behörigheter för en befintlig användare.

>[!IMPORTANT]
>
>Användaren måste ha en Adobe ID; se [krav](#add-users-and-manage-access).

### Lägg till en användare i projektet

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com/).

1. Välj ett projekt i _Alla projekt_ lista.

1. Klicka på konfigurationsikonen i det övre högra hörnet på projektkontrollpanelen.

1. Under _Projektinställningar_, klicka **[!UICONTROL Access]**.

1. I _Åtkomst_ visa, klicka **[!UICONTROL Add]**.

1. Slutför _[!UICONTROL Add User]_formulär:

   - Ange användarens e-postadress.

   - **[!UICONTROL Project admin]**—Ge administratörsbehörighet till alla inställningar och miljötyper.

   - **[!UICONTROL Environment types and permissions]**—ger åtkomst och särskilda behörighetsnivåer till vissa miljötyper. _Ingen åtkomst_, _Administratör_ (ändra inställningar, köra åtgärd, sammanfoga kod), _Medarbetare_ (push-kod), eller _Visningsprogram_ (endast visa).

   >[!TIP]
   >
   >Endast en **Projektadministratör** kan hantera användare i alla miljöer. Ge en användare åtkomst till **Åtkomst** flik, annan **Projektadministratör** eller **Kontoägare** måste tilldela användaren **Projektadministratör** roll.

1. Klicka på **[!UICONTROL Add User]**.

1. Distribuera om alla miljöer för att tillämpa ändringarna när du har lagt till användare. När du lägger till en användare aktiveras inte distributionen automatiskt. Omdistribution är ett viktigt steg för att se till att användaren kan komma åt en miljö med SSH.

När du har lagt till användaren skickar Adobe ett e-postmeddelande till den angivna adressen med instruktioner om hur du får åtkomst till Adobe Commerce i molninfrastrukturprojektet.

## Krav för användarautentisering

För ökad säkerhet tillhandahåller Adobe multifaktorautentisering (MFA) på projektnivå för att kräva tvåfaktorsautentisering (TFA) för SSH-åtkomst till Adobe Commerce i källkod och miljöer för molninfrastrukturprojekt. Se [Aktivera MFA för SSH](multi-factor-authentication.md).

När användningen av MFA är aktiverad i ett Adobe Commerce-projekt för molninfrastruktur måste alla användare med SSH-åtkomst till en miljö i det projektet aktivera TFA på sina Adobe Commerce-konton för molninfrastruktur. För automatiserade processer kan du skapa en datoranvändare och en API-token som autentiseras från kommandoraden.

När du har lagt till en användare i ett Cloud-projekt ber du användaren att granska säkerhetsinställningarna för kontot och lägga till följande säkerhetskonfigurationer efter behov:

- **Aktivera TFA**- Uppfyll säkerhets- och efterlevnadsstandarder genom att konfigurera tvåfaktorsautentisering. Projekt konfigurerade med [MFA-kontroll](multi-factor-authentication.md) kräver TFA på konton där SSH används för att få tillgång till projekten.

- **Aktivera SSH-nycklar**- Användare som behöver åtkomst till Adobe Commerce i molninfrastrukturens källkodsarkiv måste aktivera SSH-nycklar på sitt konto. Se [Säkra anslutningar](../development/secure-connections.md).

- **Skapa en API-token**—Användare måste generera en API-token som används för SSH-åtkomst till en miljö. Du behöver en token för att aktivera autentiseringsarbetsflöden för automatiserade processer.

  I projekt där MFA-tvång är aktiverat måste du använda API-token för att autentisera SSH-åtkomstbegäranden från automatiserade konton. Med denna token kan automatiserade processer kringgå autentiseringsarbetsflöden som kräver TFA.

### Aktivera TFA för molnkonton

Adobe Commerce i molninfrastrukturen stöder TFA med något av följande program:

- [Google Authenticator (Android/iPhone)](https://support.google.com/accounts/answer/1066447?hl=en)
- [Authy (Android/iPhone)](https://authy.com/features/)
- [FreeOTP (Android)](https://play.google.com/store/apps/details?id=org.fedorahosted.freeotp)
- [GAuth Authenticator (Firefox OS, desktop, others)](https://github.com/gbraad-apps/gauth)

Instruktioner för hur du installerar autentiseringsprogrammet och aktiverar TFA finns på _Kontoinställningar_ sidan i [!DNL Cloud Console].

**Aktivera TFA på ditt användarkonto**:

1. Logga in på [ditt konto](https://console.adobecommerce.com).

1. Klicka på i den övre högra kontomenyn **[!UICONTROL My Profile]**.

1. På _Säkerhet_ flik, klicka **[!UICONTROL Set up application]**.

1. Om du inte har något godkänt autentiseringsprogram på din mobila enhet kan du installera ett med hjälp av de länkade instruktionerna.

1. Lägg till ditt Adobe Commerce-konto i molninfrastrukturen i autentiseringsprogrammet.

   - Öppna autentiseringsprogrammet på din mobila enhet. Lägg sedan till installationskoden i programmet.

   - I [!UICONTROL **[!UICONTROL TFA set up - Application]**] skriver du TFA-koden från din mobila enhet på sidan **[!UICONTROL Application verification code]** fält.

   - Klicka på **[!UICONTROL Verify and save]**.

     Om koden är giltig skickar Adobe ett meddelande till kontots e-postadress som bekräftar att kontot nu har TFA.

1. Valfritt. Aktivera _Betrodd webbläsare_ inställningar för att cachelagra autentiseringskoden i webbläsaren i 30 dagar.

   Den här konfigurationen minskar antalet autentiseringsproblem vid projektinloggning.

1. Klicka **Spara** eller **Hoppa över**.

1. Spara återställningskoderna.

   - På _TFA-konfiguration - återställning_ kodar, kopiera och spara återställningskoderna så att du kan logga in på ditt Adobe Commerce i molninfrastrukturprojekt när du inte har tillgång till din mobila enhet eller autentiseringsapplikation.

   - Kopiera återställningskoderna till en annan plats eller skriv ned dem om du skulle förlora åtkomsten till enheten eller autentiseringsprogrammet.

   - Klicka **Spara** för att spara koderna på ditt konto så att du kan visa och hantera dem från säkerhetsinställningarna för ditt konto.

     >[!WARNING]
     >
     >Om du förlorar åtkomsten till ett konto med TFA och inte har återställningskodlistan, måste du kontakta projektadministratören eller [Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) för att återställa TFA-programmet.

1. När du är klar med TFA-inställningarna klickar du på **Spara** för att uppdatera ditt konto.

1. Autentisera din aktuella session med TFA.

   - Logga ut från ditt konto.
   - Logga in med ditt användarnamn och lösenord.
   - Ange TFA-koden för `accounts.magento.cloud` från autentiseringsprogrammet på din mobila enhet.

### Hantera TFA-konfiguration och återställningskoder

Du kan hantera TFA-konfigurationen för ett Adobe Commerce-konto för molninfrastruktur från _Säkerhet_ i _Min profil_ sida.

1. Logga in på [ditt konto](https://console.adobecommerce.com).

1. Klicka på i den övre högra kontomenyn **[!UICONTROL My Profile]**.

1. På _Min profil_ klickar du på **[!UICONTROL Security]** -fliken.

1. Använd de tillgängliga länkarna för att uppdatera TFA-inställningarna för ditt Adobe Commerce-konto för molninfrastruktur:

   - Inaktivera TFA
   - Återställ autentiseringsprogrammet
   - Lägga till eller ta bort betrodda webbläsare
   - Visa eller uppdatera TFA-återställningskoder på ditt konto

### Skapa en API-token

En API-token kan bytas ut mot en OAuth 2-åtkomsttoken, som sedan kan användas för att autentisera begäranden.

I projekt där användningen av MFA är aktiverad måste du ha en API-token för att aktivera SSH-åtkomst för datoranvändare och automatiserade processer.

>[!IMPORTANT]
>
>Protect API-tokenvärden för ditt konto. Visa inte värdet i kodexempel, skärmdumpar eller osäker kommunikation mellan klient och server. Visa inte heller värdet i källkod som lagras i offentliga databaser.

**Skapa en API-token**:

1. Logga in på [ditt konto](https://console.adobecommerce.com).

1. Klicka på i den övre högra kontomenyn **[!UICONTROL My Profile]**.

1. På _Min profil_ klickar du på **[!UICONTROL API tokens]** -fliken.

1. Klicka **[!UICONTROL Create API token]** och ange ett namn, till exempel, som matchar datoranvändaren eller den automatiska process som använder API-token.

   ![API-token](../../assets/api-token-name.png)

1. Klicka på **[!UICONTROL Create API token]**.
