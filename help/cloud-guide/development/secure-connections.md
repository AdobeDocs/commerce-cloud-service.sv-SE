---
title: Säkra anslutningar
description: Lär dig hur du använder SSH-nycklar i ditt Adobe Commerce i molninfrastrukturprojekt och loggar in på fjärrmiljöer.
role: Developer
feature: Cloud, Security
topic: Security
exl-id: b5780e8e-e3da-4b10-8ca3-2778085acd4a
source-git-commit: 13e76d3e9829155995acbb72d947be3041579298
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 0%

---

# Säkra anslutningar till fjärrmiljöer

Secure Shell (SSH) är ett vanligt protokoll som används för att logga in på fjärrservrar och -system på ett säkert sätt. Du kan använda SSH för att komma åt fjärrmiljöer för att hantera Adobe Commerce-programmet och komma åt fjärrmiljöloggar. Adobe har endast stöd för säkra FTP-anslutningar (sFTP) med din offentliga SSH-nyckel. FTP-anslutningar stöds inte.

## Generera ett SSH-nyckelpar

Skapa ett SSH-nyckelpar på alla datorer och arbetsytor som kräver åtkomst till projektets källkod och miljöer. Med SSH-nyckeln kan du ansluta till GitHub för att hantera källkod och ansluta till molnservrar utan att kontinuerligt behöva ange ditt användarnamn och lösenord. Se [Ansluter till GitHub med SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) om du vill ha mer information om hur du skapar ett SSH-nyckelpar.

- The _publik nyckel_ är säkert att tillhandahålla för åtkomst till en plats, SSH och sFTP.
- The _privat nyckel_ förblir privat på arbetsstationen.

>[!CAUTION]
>
>**Dela aldrig din privata nyckel.** Lägg inte till den i en biljett, kopiera den till en chatt eller bifoga den till e-postmeddelanden.

## Lägg till en offentlig SSH-nyckel till ditt konto

När du har lagt till din offentliga SSH-nyckel till ditt Adobe Commerce-konto för molninfrastruktur ska du distribuera om alla aktiva miljöer på ditt konto för att installera nyckeln.

Du kan lägga till SSH-nycklar till ditt konto på något av följande sätt: Cloud CLI eller [!DNL Cloud Console].

>[!BEGINTABS]

>[!TAB CLI]

### Lägg till din SSH-nyckel med hjälp av CLI för molnet

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Logga in på ditt projekt:

   ```bash
   magento-cloud login
   ```

1. Lägg till den offentliga nyckeln.

   ```bash
   magento-cloud ssh-key:add ~/.ssh/id_rsa.pub
   ```

>[!TIP]
>
>Du kan visa och ta bort SSH-nycklar med CLI-kommandona i molnet `ssh-key:list` och `ssh-key:delete`.

>[!TAB Konsol]

### Lägg till din SSH-nyckel med [!DNL Cloud Console]

**Lägga till en SSH-nyckel i ett nytt projekt**:

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Klicka på **[!UICONTROL No SSH key]**. Den här ikonen finns till höger om kommandofältet och är synlig när projektet inte innehåller någon SSH-nyckel.

1. Kopiera och klistra in innehållet i den offentliga SSH-nyckeln i **Offentlig nyckel** fält.

1. Följ återstående instruktioner.

**Lägga till en SSH-nyckel i din molnprofil**:

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Klicka på i den övre högra kontomenyn **Min profil**.

1. I _SSH-nycklar_ visa, klicka **Lägg till offentlig nyckel**.

1. I _Lägg till en SSH-nyckel_ formulär, ge din nyckel en **Titel** och klistra in den offentliga SSH-nyckeln i **Nyckel** fält.

1. Klicka **Spara**.

>[!ENDTABS]

## Ansluta till en fjärrmiljö

Du kan ansluta till en fjärrmiljö med `magento-cloud` CLI eller ett SSH-kommando. The `magento-cloud` CLI-kommandon kan bara användas i integreringsmiljöer för Starter och Pro.

### Använda CLI i molnet

**Logga in i en fjärrintegreringsmiljö**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Lista miljöerna i det projektet.

   ```bash
   magento-cloud environment:list -p <project-ID>
   ```

1. Använd SSH för att logga in i fjärrmiljön.

   ```bash
   magento-cloud ssh -p <project-ID> -e <environment-ID>
   ```

### Använda ett SSH-kommando

The [!DNL Cloud Console] innehåller en lista med kommandon för webb- och SSH-åtkomst för varje miljö.

**Kopiera SSH-kommandot**:

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com).

1. Välj ett projekt i _Alla projekt_ lista.

1. Välj en miljö.

1. Klicka på **[!UICONTROL SSH]**.

1. I _SSH_ klickar du på kopieringsknappen för att kopiera det fullständiga SSH-kommandot till Urklipp.

1. Öppna en terminal och klistra in SSH-kommandot för att skapa en anslutning.

   ```bash
   ssh abcdefg123abc-branch-a12b34c--mymagento@ssh.us-2.magento.cloud
   ```

>[!TIP]
>
>För Pro Staging- och Production-miljöer kan SSH-kommandot se ut så här:
>
>```bash
>ssh <node>.ent-<project-ID>-<environment>-<user-ID>@ssh.<region>.magento.com
>```

## sFTP

Adobe Commerce i molninfrastrukturen har stöd för åtkomst till dina miljöer med sFTP (säker FTP) med SSH-autentisering. Använd en klient som har stöd för SSH-nyckelautentisering för sFTP och använd den offentliga SSH-nyckeln. Den offentliga SSH-nyckeln måste läggas till i målmiljön. För Starter-miljöer och Pro-integreringsmiljöer kan du [lägga till det via [!DNL Cloud Console]](#add-your-ssh-key-using-the-project-web-interface).

Skrivskyddade sFTP-anslutningar är _not_ stöds; sFTP-åtkomst tillhandahålls med _skriva_ behörighet som standard.

När du konfigurerar sFTP använder du informationen från SSH-åtkomstmiljökommandot: `<project-id>-<environment-id>--<app-name>@ssh<cloud-host>`

- **Användarnamn**: Allt innehåll före `@` i SSH-åtkomstmålet.
- **Lösenord**: Du behöver inget lösenord för sFTP. sFTP-åtkomst använder SSH-nyckelautentisering.
- **Värd**: Allt innehåll efter `@` i SSH-åtkomsten.
- **Port**: 22, vilket är standardporten för SSH.
- **SSH** Privat nyckel: Ange vid behov platsen för din privata nyckel till sFTP-klienten. Som standard lagras privata nycklar i `~/.ssh` katalog.

Beroende på klienten kan ytterligare alternativ behövas för att slutföra SSH-autentiseringen för sFTP. Granska dokumentationen för den valda klienten.

För **Starter-miljöer och Pro-integreringsmiljöer** kanske du också vill överväga [lägga till en `mount`](../application/properties.md#mounts) för åtkomst till en viss katalog. Du skulle lägga till monteringen i `.magento.app.yaml` -fil. En lista över skrivbara kataloger finns på [Projektstruktur](../project/file-structure.md). Den här monteringspunkten fungerar bara i dessa miljöer.

För **Proffsmiljöer för staging och produktion** Om du inte har SSH-åtkomst till miljön måste du [skicka en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) begära sFTP-åtkomst och en monteringspunkt för åtkomst till den specifika mappen, t.ex. `pub/media`.

>[!NOTE]
>För Pro Staging and Production, om sFTP-anslutningen är för en _generisk_ användare som **not** måste vara [som lagts till i molnprojektet](../project/user-access.md)måste du [skicka en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) med **public** bifogad nyckel. **Ange aldrig din privata SSH-nyckel.**

## SSH-tunnel

Du kan använda SSH-tunnel för att ansluta till en tjänst från den lokala utvecklingsmiljön som om tjänsten var lokal. Konfigurera [SSH](#add-an-ssh-public-key-to-your-account).

Använd ett terminalprogram för att logga in och skicka ut kommandon.

```bash
magento-cloud login
```

Kontrollera om några tunnlar är öppna med.

```bash
magento-cloud tunnel:list
```

Om du vill bygga en tunnel måste du känna till [programnamn](../application/properties.md#name). Du kan kontrollera programnamnet med CLI:

```bash
magento-cloud apps
```

### Konfigurera SSH-tunneln

```bash
magento-cloud tunnel:open -e <environment-ID> --app <app-name>
```

Om du till exempel vill öppna en tunnel till `sprint5` gren i ett projekt med en app som heter `mymagento`, ange

```bash
magento-cloud tunnel:open -e sprint5 --app mymagento
```

Exempelsvar:

```terminal
SSH tunnel opened on port 30004 to relationship: redis
SSH tunnel opened on port 30005 to relationship: database
Logs are written to: /home/magento_user/.magento/tunnels.log

List tunnels with: magento-cloud tunnels
View tunnel details with: magento-cloud tunnel:info
Close tunnels with: magento-cloud tunnel:close
```

**Visa information om tunneln**:

```bash
magento-cloud tunnel:info -e <environment-ID>
```

### Anslut till tjänster

När du har skapat en SSH-tunnel kan du ansluta till tjänster som om de körs lokalt. Om du till exempel vill ansluta till databasen använder du följande kommando:

```bash
mysql --host=127.0.0.1 --user='<database-username>' --pass='<user-password>' --database='<name>' --port='<port>'
```
