---
title: '[!DNL Onboarding] till Commerce'
description: Gå till ditt molnkonto och konfigurera ett Adobe Commerce-projekt för molninfrastruktur.
role: Admin
recommendations: noDisplay, catalog
exl-id: c6b768d7-d835-4a8d-aad9-1c0324f7570d
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# [!DNL Onboarding] till Commerce

När Adobe har aktiverat en Commerce on cloud Infrastructure-prenumeration är det ursprungliga projektet och kodåtkomsten endast tillgänglig för den person som har angetts som licensägare (kontoägare).

Licensägaren är den person i företaget eller finansorganisationen som hanterar betalningar och andra affärsrelaterade transaktioner för Adobe Commerce på molninfrastrukturkontot. Den här personen fungerar som kontaktpunkt för Adobe. Om du måste ändra licensägaren för ditt konto måste du kontakta ditt Adobe-kontoteam.

För att snabbt kunna ta med dig ditt projekt, så att du kan börja utveckla webbplatsen för direktdistribution, måste du slutföra den nödvändiga installationen och [!DNL onboarding] uppgifter. Vanligtvis börjar licensägaren processen genom att skydda administratörsåtkomst och skapa användare av Technical Admin som kan hjälpa till med konfiguration, anpassning och utveckling.

## Registrera dig för ett molnkonto

Om du inte har något Adobe Commerce-konto för molninfrastruktur kontaktar du [Försäljning]. När du registrerar dig skapar Adobe ditt konto och skickar ett välkomstmeddelande med instruktioner om hur du kommer åt projektgränssnittet. E-postmeddelandet innehåller en länk så att du kan logga in på ditt konto och slutföra den första projektkonfigurationen.

### Cloud [!DNL Onboarding] UI

Adobe Commerce on cloud infrastructure Project page in the ([!DNL Onboarding] UI) finns en lista med kryssrutor för att komma igång med att konfigurera projekt och tjänster, fastställa åtkomst och komma igång med utveckling. Från OBUI kan du:

- Lägg till en teknisk administratör, en superanvändare som kan hantera ditt projekt och dina grenar
- Få tillgång till din projektmiljö, inklusive en länk till [!DNL Cloud Console]
- Slutför en checklista för snabbtest av användargodkännande (UAT) med länkar till ytterligare tester

**Öppna projektsidan**:

1. Logga in på [Adobe Commerce kundkonto](https://account.magento.com/customer/account/login).

1. På _Mitt konto_ klickar du på **[!UICONTROL Commerce]** om du vill visa projekten på ditt konto.

1. Klicka **Visa projektsida** i [Avsnittet Projekt](https://cloud.magento.com/cloud/project/).

1. Klicka på projektnamnet och öppna sidan Cloud Project ([!DNL Onboarding] UI).

   ![Projektsida för OBUI](../assets/onboarding-ui.png)

   Bläddra igenom portalen för att få användbar information och alternativ för att börja planera projektet, utveckla kod och förbereda för lansering av UAT och webbplats.

## Få åtkomst till projekt och lägg till användare

Licensägaren kan lägga till användarkonton för att ge åtkomst till kod, hantera grenar, ange biljetter och supportmiljöer. Dessa användarkonton kan omfatta intern utveckling, konsulter och lösningsspecialister.

Vanligtvis är den enda användare som licensägaren måste skapa _Teknisk administratör_. Den tekniska administratören behöver ett användarkonto med administratörsåtkomst för att skapa användarkonton för utvecklare, ange miljöbehörigheter och hantera alla grenar och miljöer. Den tekniska administratören kan vara utvecklare, konsult och [Adobe Solution Partner](https://business.adobe.com/products/magento/partners.html)eller dig själv.

Du kan skapa en teknisk administratör via projektportalen på [!DNL Cloud Console]eller från kommandoraden med `magento-cloud` CLI.

### Användarregistrering

Du kan bara lägga till registrerade användare i Adobe Commerce i projekt och miljöer för molninfrastruktur. Om du har en ny användare ber du dem att [kontoregistrering](https://account.magento.com/customer/account/login/) och ange den e-postadress som är kopplad till deras kontoprofil.

### Åtkomst till delat konto

Licensägaren kan konfigurera delad åtkomst för kontot. Med delad åtkomst kan betrodda medarbetare och tjänsteleverantörer använda Help center för att skicka och spåra supportärenden som rör din Adobe Commerce i molninfrastrukturprojekt. Instruktioner finns i [Delad åtkomst] artikel i hjälpcentret.

### [!DNL Cloud Console]

Du kan använda [[!DNL Cloud Console]](cloud-console.md) för att hantera ditt projekt, lägga till användarkonton och börja utveckla din butik. Licensägaren, den tekniska administratören och utvecklarna kan använda [!DNL Cloud Console] för att hantera alla miljöer och grenar, miljövariabler, miljöinställningar och vägar.

**Så här öppnar du[!DNL Cloud Console]**:

1. Logga in på [Mitt konto](https://account.magento.com/customer/account/login).

1. På _Mitt konto_ klickar du på **[!UICONTROL Commerce]** om du vill visa projekten på ditt konto.

1. Klicka på **Projekt** och välja ett projekt.

1. Klicka **Infrastrukturåtkomst** och klicka sedan på **Project Access (webbgränssnitt)**.

   ![Projektportal i molnet](../assets/obui-project-access.png)

## Registrera dig för status Adobe

Få uppdateringar om Adobe Commerce i molninfrastrukturens plattformsmiljöer och tillhörande tjänster från [Statussida].

Sidan innehåller en status för Adobe Commerce komponenter och tjänster följt av meddelanden om incidentrapporter, serviceuppgraderingar, planerade driftavbrott och planerat underhåll. Alla som arbetar med ditt projekt kan prenumerera på Adobe Commerce statuswebbplats för att få händelseaviseringar och uppdateringar via e-post eller Slack. Du kan anpassa din Adobe-statusprenumeration för att spåra specifika produkter efter regioner och händelser.

>[!TIP]
>
> Öppna den nya [!DNL Cloud Console] och visa projekt- och miljöaktiviteter.
>
>**Nästa steg**: [Logga in på Cl[!DNL ]molnkonsolen](cloud-console.md)

<!-- link definitions -->

[Försäljning]: https://business.adobe.com/products/magento/get-demo.html
[Delad åtkomst]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#shared-access
[Statussida]: https://status.adobe.com/products/503473
