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

När Adobe har aktiverat en Commerce-prenumeration på en molninfrastruktur är det ursprungliga projektet och kodåtkomsten endast tillgänglig för den person som har angetts som licensägare (kontoägare).

Licensägaren är den person i företaget eller finansorganisationen som hanterar betalningar och andra affärsrelaterade transaktioner för Adobe Commerce på molninfrastrukturkontot. Den här personen fungerar som kontaktpunkt för Adobe. Om du måste ändra licensägaren för ditt konto måste du kontakta ditt Adobe-kontoteam.

Om du snabbt vill komma igång med ditt projekt, så att du kan börja utveckla webbplatsen för direktdistribution, måste du slutföra de nödvändiga inställningarna och [!DNL onboarding]-uppgifterna. Vanligtvis börjar licensägaren processen genom att skydda administratörsåtkomst och skapa användare av Technical Admin som kan hjälpa till med konfiguration, anpassning och utveckling.

## Registrera dig för ett molnkonto

Om du inte har något Adobe Commerce-konto för molninfrastruktur kontaktar du [Försäljning]. När du registrerar dig skapar Adobe ditt konto och skickar ett välkomstmeddelande med instruktioner om hur du kommer åt projektgränssnittet. E-postmeddelandet innehåller en länk så att du kan logga in på ditt konto och slutföra den första projektkonfigurationen.

### Användargränssnitt för [!DNL Onboarding] i molnet

På sidan Adobe Commerce om projekt för molninfrastruktur i ([!DNL Onboarding] användargränssnitt) finns en checklista för att komma igång med att konfigurera ditt projekt och dina tjänster, fastställa åtkomst och komma igång med utvecklingen. Från OBUI kan du:

- Lägg till en teknisk administratör, en superanvändare som kan hantera ditt projekt och dina grenar
- Få åtkomst till din projektmiljö, inklusive en länk till [!DNL Cloud Console]
- Slutför en checklista för snabbtest av användargodkännande (UAT) med länkar till ytterligare tester

**Så här öppnar du projektsidan**:

1. Logga in på ditt [Adobe Commerce-kundkonto](https://account.magento.com/customer/account/login).

1. På sidan _Mitt konto_ klickar du på fliken **[!UICONTROL Commerce]** för att visa projekten i ditt konto.

1. Klicka på **Visa projektsida** i avsnittet [Projekt](https://cloud.magento.com/cloud/project/).

1. Klicka på projektnamnet och öppna sidan för molnprojekt ([!DNL Onboarding] användargränssnitt).

   ![OBUI-projektsida](../assets/onboarding-ui.png)

   Bläddra igenom portalen för att få användbar information och alternativ för att börja planera projektet, utveckla kod och förbereda för lansering av UAT och webbplats.

## Få åtkomst till projekt och lägg till användare

Licensägaren kan lägga till användarkonton för att ge åtkomst till kod, hantera grenar, ange biljetter och supportmiljöer. Dessa användarkonton kan omfatta intern utveckling, konsulter och lösningsspecialister.

Vanligtvis är den enda användare som licensägaren måste skapa _Teknisk administratör_. Den tekniska administratören behöver ett användarkonto med administratörsåtkomst för att skapa användarkonton för utvecklare, ange miljöbehörigheter och hantera alla grenar och miljöer. Den tekniska administratören kan vara utvecklare, konsult, [Adobe Solution Partner](https://business.adobe.com/products/magento/partners.html) eller dig själv.

Du kan skapa en teknisk administratör via projektportalen, från [!DNL Cloud Console] eller från kommandoraden med hjälp av CLI:n för `magento-cloud`.

### Användarregistrering

Du kan bara lägga till registrerade användare i Adobe Commerce i projekt och miljöer för molninfrastruktur. Om du har en ny användare ber du dem att [registrera ett konto](https://account.magento.com/customer/account/login/) och ange den e-postadress som är kopplad till deras kontoprofil.

### Åtkomst till delat konto

Licensägaren kan konfigurera delad åtkomst för kontot. Med delad åtkomst kan betrodda medarbetare och tjänsteleverantörer använda Help center för att skicka och spåra supportärenden som rör din Adobe Commerce i molninfrastrukturprojekt. Instruktioner finns i artikeln [Delad åtkomst] i hjälpcentret.

### [!DNL Cloud Console]

Du kan använda [[!DNL Cloud Console]](cloud-console.md) för att hantera ditt projekt, lägga till användarkonton och börja utveckla din butik. Licensägaren, den tekniska administratörens användare och utvecklare kan använda [!DNL Cloud Console] för att hantera alla miljöer och grenar, miljövariabler, miljöinställningar och vägar.

**Så här kommer du åt[!DNL Cloud Console]**:

1. Logga in på [Mitt konto](https://account.magento.com/customer/account/login).

1. På sidan _Mitt konto_ klickar du på fliken **[!UICONTROL Commerce]** för att visa projekten i ditt konto.

1. Klicka på fliken **Projekt** och välj ett projekt.

1. Klicka på **Infrastrukturåtkomst** och sedan på **Projektåtkomst (webbgränssnitt)**.

   ![Projektportal i molnet](../assets/obui-project-access.png)

## Registrera dig för status Adobe

Hämta uppdateringar om Adobe Commerce för plattformsmiljöer för molninfrastruktur och relaterade tjänster från [statussidan].

Sidan innehåller en status för Adobe Commerce komponenter och tjänster följt av meddelanden om incidentrapporter, serviceuppgraderingar, planerade driftavbrott och planerat underhåll. Alla som arbetar med ditt projekt kan prenumerera på Adobe Commerce statuswebbplats för att få händelseaviseringar och uppdateringar via e-post eller Slack. Du kan anpassa din Adobe-statusprenumeration för att spåra specifika produkter efter regioner och händelser.

>[!TIP]
>
> Öppna den nya [!DNL Cloud Console] och visa projekt- och miljöaktiviteter.
>
>**Nästa steg**: [Logga in på Cl[!DNL ]molnkonsol](cloud-console.md)

<!-- link definitions -->

[Försäljning]: https://business.adobe.com/products/magento/get-demo.html
[Delad åtkomst]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#shared-access
[Statussida]: https://status.adobe.com/products/503473
