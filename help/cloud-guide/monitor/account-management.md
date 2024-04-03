---
title: New Relic Kontohantering
description: Lär dig hur du får tillgång till ditt New Relic-konto och hanterar åtkomst, integrering och verktygshantering för ditt Adobe Commerce i molninfrastrukturprojekt.
feature: Cloud, Observability
role: Admin
exl-id: ee639e2e-4074-4384-8f68-152bc3bac93b
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# New Relic kontohantering

När Adobe tillhandahåller ditt molninfrastrukturprojekt får licensägaren ett e-postmeddelande från New Relic med uppgifter och instruktioner för hur man får åtkomst till New Relic-kontot. Om du inte fått e-postmeddelandet kan du återställa New Relic-lösenordet med hjälp av e-postadressen till licensägaren.

## Hantera användaråtkomst

Ett New Relic-konto kan bara ha en person tilldelad rollen Ägare. Om du måste ändra kontoägaren tilldelar du den aktuella ägaren administratörsrollen och tilldelar sedan rollen Ägare till en annan användare. Se [Uppdatera kontoägaren](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/) i _New Relic-dokumentation_ för instruktioner.

Riktlinjer för hantering av åtkomst till New Relic:

- Projektägare och administratörer kan lägga till och ta bort användare från New Relic-kontot.
- Skapa inte fler än fem fullständiga behörigheter **Användare**.
- Ge endast fullständig åtkomst till användare som strikt kräver åtkomst till hela funktionsuppsättningen.
- Det finns ingen specifik vägledning om kostnadsfria **Begränsad** -användare.

>[!TIP]
>
>Innan du tilldelar ägarrollen till en användare kontrollerar du att användaren finns på New Relic-kontot för Adobe Commerce i molninfrastrukturen. Om du måste lägga till användaren i det kontot och en befintlig kontoägare eller administratör inte kan hjälpa till, kan alla användare som har åtkomst till [Adobe partnerskap Ägarkonto](https://account.newrelic.com/accounts/1311131/users) för New Relic kan lägga till användare för kundens räkning.

Lägg till minst en **Administratör** användare till ditt New Relic-konto som kan hantera all åtkomst, alla integreringar och all verktygsanvändning.

**Få åtkomst till användarhantering i New Relic**:

1. Logga in på [New Relic](https://login.newrelic.com/login).

1. Välj ditt användarnamn i den nedre vänstra navigeringen.

1. Klicka **[!UICONTROL Administration]** och välj något av följande i listan:

   - **[!UICONTROL User management]** för att lägga till en användare och hantera aktiva användare och väntande inbjudningar.

   - **[!UICONTROL Access management]** för att hantera användargrupper, roller och konton.

Se [Användarhantering](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-user-management/user-management-ui-and-tasks/) i _New Relic_ dokumentation.

## Konfigurera New Relic för Starter-miljön

>[!NOTE]
>
>**Pro-miljöer** är förkonfigurerade för att använda New Relic-tjänster och kan hoppa över instruktioner om aktivering och anslutning. Om New Relic APM inte är installerat i miljö för förproduktion och produktion, eller om New Relic infrastruktur inte är tillgänglig i produktionsmiljön, [skicka en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) för att begära installation.

För Starter-miljöer måste du kontrollera `.magento.app.yaml` filen för att verifiera att `runtime` innehåller New Relic-tillägget. Om tillägget inte har konfigurerats lägger du till följande:

> `.magento.app.yaml`

```yaml
runtime:
    extensions:
        - newrelic
```

### Använd licensnyckel

Om du vill ansluta en molnmiljö till New Relic lägger du till New Relic licensnyckel i miljön.

- För **Pro-projekt** lägger Adobe till licensnyckeln i din produktions- och mellanlagringsmiljö under provisioneringsprocessen. Du kan logga in på [New Relic](https://login.newrelic.com/login) för att verifiera anslutningen mellan din Adobe Commerce på molninfrastruktursajt och New Relic.

- För **Startprojekt** har du en licensnyckel för New Relic som har stöd för upp till _tre_ miljöer. Du måste lägga till nyckeln i dina miljökonfigurationer manuellt. Startmiljöer är inte förprovisionerade för att använda New Relic-tjänsten.

I Starter-miljöer aktiverar du integreringen av New Relic genom att lägga till New Relic-licensnyckeln i miljökonfigurationen. Lägg till nyckeln i miljö för förproduktion och produktion och en annan miljö som du väljer. Endast licensnyckeln för New Relic krävs för konfigurationen. Mer information om ytterligare konfigurationsalternativ finns i [New Relic Reporting](https://experienceleague.adobe.com/docs/commerce-admin/config/general/new-relic-reporting.html) ämne i _Adobe Commerce Användarhandbok_.

{{redeploy-warning}}

>[!PREREQUISITES]
>
>- Inloggningsuppgifter för Adobe Commerce-kontosidan eller för den New Relic-licens som är kopplad till ditt projekt
>- [Åtkomst på administratörsnivå](../project/user-access.md) till Starter-miljöerna för att konfigurera
>- Autentiseringsuppgifter för åtkomst till [Administratör](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions.html) för miljön

**Konfigurera New Relic för Starter-miljöer**:

1. Hitta din licensnyckel för New Relic från [!DNL Cloud Console] eller Cloud CLI.

   **[!DNL Cloud Console]method**:

   - Öppna ditt molnprojekt [kontosida](https://accounts.magento.cloud/user).

   - På _Projekt_ finns i ditt projekt.

   - Klicka **Visa detaljer** för information om projektinfrastruktur.

   - Expandera **New Relic Service** för att visa licensnyckeln.

   - Kopiera licensnyckeln.

   **CLI-metod i molnet**:

   ```bash
   magento-cloud subscription:info services.newrelic
   ```

1. Lägg till licensnyckeln för New Relic i en miljö med `magento-cloud` CLI.

   - Byt till den miljö som behöver licensnyckeln.
   - Uppdatera variabelvärdet med följande `magento-cloud` CLI-kommando:

     ```bash
     magento-cloud variable:update php:newrelic.license --value <newrelic-license-key>
     ```

   Om du vill kan du lägga till det från [Commerce Admin](https://experienceleague.adobe.com/docs/commerce-admin/start/reporting/new-relic-reporting.html#step-3%3A-configure-your-store).

1. Logga in på [New Relic](https://login.newrelic.com/login) för att verifiera att du kan visa data från Adobe Commerce-miljön. Se [Undersök prestanda](investigate-performance.md).

### Ta bort licensnyckel

Du kan bara använda din licensnyckel för New Relic i tre aktiva miljöer. Om nyckeln används i tre miljöer måste du ta bort nyckeln från en av miljöerna innan du kan lägga till den i en annan miljö.

**Ta bort en licensnyckel från en miljö**:

1. Visa miljövariabler.

   ```bash
   magento-cloud variable:list
   ```

   Exempelsvar:

   ```terminal
    +----------------------+-------------+----------------------+---------+
    | Name                 | Level       | Value                | Enabled |
    +----------------------+-------------+----------------------+---------+
    | php:newrelic.license | environment | newrelic-license-key | true    |
    +----------------------+-------------+----------------------+---------+
   ```

   >[!WARNING]
   >
   >Om du lade till licensnyckeln som _projekt_ måste du ta bort den variabeln på projektnivå. En projektvariabel lägger till licensen i _var_ en gren som kan förbruka eller överskrida licensgränsen har skapats. Så här listar du projektvariabler: `magento-cloud variable:list --level project`

1. Ta bort licensvariabeln.

   ```bash
   magento-cloud variable:delete php:newrelic.license
   ```
