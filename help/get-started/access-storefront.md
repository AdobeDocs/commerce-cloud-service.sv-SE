---
title: Öppna Commerce Admin-panelen
description: Lär dig hur du kommer åt din Commerce Admin-panel.
recommendations: noDisplay, catalog
exl-id: 9a8a0a49-b108-48bd-b413-ec9431370c06
source-git-commit: 85ff1283f773823ff2c6e6ab8f391fd5b4aa00e4
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Öppna Commerce Admin-panelen

Användare som har administratörsbehörighet för Commerce Admin-panelen kan lägga till användare, konfigurera butikstjänster, slutföra butiksinstallation och anpassningsarbete och mycket annat.

För ett nytt projekt är det första steget efter att du har fått välkomstmeddelandet att skydda administratörsåtkomst till projektet genom att ändra lösenordet på licensägarkontot. Standardanvändarnamnet för det här kontot är licensägarens e-postadress.

Du kan skicka en begäran om lösenordsändring på något av följande sätt:

- Leta upp det välkomstmeddelande som skickas till e-postadressen till licensägaren och följ länken och ändra lösenordet.

- Kopiera butikens URL från [[!DNL Cloud Console]](../cloud-guide/project/overview.md) i en webbläsare. Lägg sedan till `/admin` till slutet av URL:en för att öppna inloggningssidan. Klicka på **Har du glömt lösenordet?** om du vill skicka en begäran om lösenordsändring till licensägarens e-postadress.

När du har skickat begäran om lösenordsändring kan du kontrollera om det finns ett meddelande om lösenordsåterställning i e-postmeddelandet. Om du inte får e-postmeddelandet kontrollerar du din skräppostmapp.

>[!TIP]
>
>Om lösenordsåterställningen misslyckas eller du inte kan logga in på Admin-panelen, kan en användare med administratörsåtkomst ansluta till projektet med SSH och lägga till en administratörsanvändare med `admin:user:create` CLI-kommando. Se [Skapa, redigera eller låsa upp ett administratörskonto](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) i _Installationsguide_.
