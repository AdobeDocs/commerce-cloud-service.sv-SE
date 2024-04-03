---
title: ADMIN-variabler
description: Se en lista över miljövariabler som används vid installation av Adobe Commerce i molninfrastruktur.
feature: Cloud, Configuration, Install, Roles/Permissions
role: Developer
exl-id: 2829a9dc-40bb-4665-886e-a56d98468fc1
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Administratörsvariabler

Användare som har administratörsbehörighet för Adobe Commerce i molninfrastrukturprojekt kan använda följande projektmiljövariabler för att åsidosätta konfigurationsinställningarna för administratörskontot för att få åtkomst till administratörsgränssnittet.

## Administratörsreferenser

Du kan åsidosätta administratörens inloggningsuppgifter under Commerce-installation med ADMIN-variablerna i följande tabell.

Om du vill ändra värdena efter installationen ansluter du till miljön med SSH och använder Adobe Commerce CLI [`admin:user` kommando](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) för att skapa eller redigera administratörens användaruppgifter.

| Variabel | Standard | Beskrivning |
| -------------- | --------------------------- | ----------- |
| `ADMIN_USERNAME` | Licensägarens e-postadress | Ett användarnamn för den administrativa användaren med möjlighet att skapa andra användare, inklusive administrativa användare. |
| `ADMIN_EMAIL` |                             | E-postadress till administratören. Den här adressen används för att skicka meddelanden om återställning av lösenord. |
| `ADMIN_PASSWORD` |                             | Lösenord för den administrativa användaren. När projektet skapas skapas ett slumpmässigt lösenord och ett e-postmeddelande skickas till licensägaren. När projektet skapades bör licensägaren redan ha ändrat lösenordet. Kontakta licensägaren för det uppdaterade lösenordet. |
| `ADMIN_LOCALE` | `en_US` | Det standardspråk som används av administratören. |

## Admin-URL

Använd följande miljövariabel för att skydda åtkomsten till ditt administratörsgränssnitt. Om det här värdet anges åsidosätts standardwebbadressen under installationen.

`ADMIN_URL`- Den relativa URL-adressen för åtkomst till Admin-gränssnittet. Standardwebbadressen är `/admin`. Av säkerhetsskäl rekommenderar Adobe att du ändrar standardvärdet till en unik, anpassad Admin-URL som inte är enkel att gissa sig till.

### Ändra Admin-URL

Adobe rekommenderar att du ändrar miljönivåvariabeln för Admin URL efter installationen. Konfigurera den här inställningen av säkerhetsskäl innan den förgrenas från klonade `master` miljö. Alla förgreningar som har skapats från `master` gren ärver miljönivåvariablerna och deras värden.

Använd `magento-cloud variable:update` för att uppdatera variabelvärdet. (Med `variable:set` -kommandot har tagits bort och är inte tillgängligt.) I följande exempel uppdateras ADMIN_URL till `newAdmin_A8v10`:

```bash
magento-cloud variable:update ADMIN_URL --value newAdmin_A8v10 -e master
```

>[!NOTE]
>
>The `ADMIN_URL` värdet accepterar bokstäver (a-z eller A-Z), siffror (0-9) och understreck (_) för en anpassad administratörssökväg. Blanksteg och andra tecken är **not** accepterad.

**Om du vill ändra URL:en använder du[!DNL Cloud Console]**:

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Välj ett projekt i _Alla projekt_ lista.

1. I projektöversikten markerar du miljön och klickar på konfigurationsikonen.

   ![Projektkonfiguration](../../assets/icon-configure.png){width="36"}

1. Välj **Variabel** -fliken.

1. Klicka **Skapa variabel**.

1. Ange följande:

   - **Variabelnamn** = `ADMIN_URL`
   - **value** = Ny URL. Ange till exempel Admin URL till `magento_A8v10`.

   Som standard `Available during runtime` och `Make inheritable` är markerade.

1. Klicka **Skapa variabel** och vänta tills distributionen är klar. Den här knappen visas bara när de obligatoriska fälten innehåller värden.
