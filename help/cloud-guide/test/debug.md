---
title: Konfigurera [!DNL Xdebug]
description: Lär dig hur du konfigurerar Xdebug-tillägget för felsökning av din Adobe Commerce när du utvecklar projekt för molninfrastruktur.
exl-id: bf2d32d8-fab7-439e-8df3-b039e53009d4
source-git-commit: 751456f50e7b017b47c2ff43e008c2d04a558d96
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 0%

---

# Konfigurera Xdebug

[!DNL Xdebug] är ett tillägg till felsökning av PHP. Även om du kan använda en annan utvecklingsmiljö förklarar följande hur du konfigurerar [!DNL Xdebug] och [!DNL PhpStorm] för att felsöka i din lokala miljö.

>[!NOTE]
>
>Du kan konfigurera [!DNL Xdebug] för att köras i Cloud Docker-miljön för lokal felsökning utan att ändra din projektkonfiguration för Adobe Commerce för molninfrastruktur. Se [Konfigurera Xdebug för Docker](https://developer.adobe.com/commerce/cloud-tools/docker/test/configure-xdebug/).

Aktivera [!DNL Xdebug]måste du konfigurera en fil i Git-databasen, konfigurera din IDE och konfigurera portvidarebefordran. Du kan konfigurera vissa inställningar i `magento.app.yaml` -fil. Efter redigering kan du föra Git-ändringarna över alla Starter-miljöer och Pro-integreringsmiljöer för att aktivera [!DNL Xdebug]. [!DNL Xdebug] finns redan i Pro Staging &amp; Production-miljöer.

När konfigurationen är klar kan du felsöka CLI-kommandon, webbförfrågningar och kod. Kom ihåg att alla molninfrastrukturmiljöer är skrivskyddade. Klona koden i den lokala utvecklingsmiljön för att utföra felsökningen. Proffsens miljö för mellanlagring och produktion finns på [ytterligare instruktioner](#debug-for-pro-staging-and-production) for [!DNL Xdebug].

## Krav

Köra och använda [!DNL Xdebug]behöver du SSH-URL:en för miljön. Du kan hitta informationen via [[!DNL Cloud Console]](../project/overview.md) eller [!DNL Cloud Onboarding UI].

## Konfigurera Xdebug

Konfigurera [!DNL Xdebug]gör du så här:

- [Arbeta i en gren för att överföra filuppdateringar](#get-started-with-a-branch)
- [Aktivera [!DNL Xdebug] för miljöer](#enable-xdebug-in-your-environment)
- [Konfigurera din IDE](#configure-phpstorm)
- [Konfigurera portvidarebefordran](#set-up-port-forwarding)

### Kom igång med en gren

Lägg till [!DNL Xdebug]rekommenderar Adobe att arbeta i [en utvecklingsgren](../dev-tools/cloud-cli-overview.md#create-an-environment-branch).

### Aktivera Xdebug i miljön

Du kan aktivera [!DNL Xdebug] direkt till alla Starter-miljöer och Pro-integreringsmiljöer. Det här konfigurationssteget krävs inte för Pro Production &amp; Staging-miljöer. Se [Debug for Pro Staging and Production](#debug-for-pro-staging-and-production).

Aktivera [!DNL Xdebug] för ditt projekt, lägg till `xdebug` till `runtime:extensions` i `.magento.app.yaml` -fil.

**Aktivera Xdebug**:

1. Öppna `.magento.app.yaml` i en textredigerare.

1. I `runtime` avsnitt, under `extensions`, lägga till `xdebug`. Exempel:

   ```yaml
   runtime:
       extensions:
           - redis
           - xsl
           - newrelic
           - sodium
           - xdebug
   ```

1. Spara ändringarna i `.magento.app.yaml` och avsluta textredigeraren.

1. Lägg till, implementera och kör ändringarna för att omdistribuera miljön.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Add xdebug"
   ```

   ```bash
   git push origin <environment-ID>
   ```

Vid driftsättning i Starter-miljöer och i Pro-integreringsmiljöer [!DNL Xdebug] är nu tillgängligt. Fortsätt konfigurera IDE. Information om PhpStorm finns på [Konfigurera PhpStorm](#configure-phpstorm).

### Konfigurera PhpStorm

The [PhpStorm](https://www.jetbrains.com/phpstorm/) IDE måste konfigureras för att fungera korrekt med [!DNL Xdebug].

**Så här konfigurerar du PhpStorm att arbeta med Xdebug**:

1. I PhpStorm-projektet öppnar du **Inställningar** -panelen.

   - _macOS_—Select **PhpStorm** > **Inställningar**.
   - _Windows/Linux_—Select **Fil** > **Inställningar**.

1. I _Inställningar_ panel, expandera och leta upp **Språk och ramar** > **PHP** > **Servrar** -avsnitt.

1. Klicka på **+** för att lägga till en serverkonfiguration. Projektnamnet är grått högst upp.

1. [Valfritt] Konfigurera följande inställningar för den nya serverkonfigurationen. Se [Ingen felsökningsserver har konfigurerats](https://www.jetbrains.com/help/phpstorm/troubleshooting-php-debugging.html#no-debug-server-is-configured) i _PHPStorm_ dokumentation.

   - **Namn**—Ange samma som värdnamnet. Detta värde måste matcha värdet för `PHP_IDE_CONFIG` variabel i [Felsöka CLI-kommandon](#debug-cli-commands) för att använda CLI för felsökning.
   - **Värd**—Ange värdnamnet.
   - **Port**—Enter `443`.
   - **Felsökning**—Select `Xdebug`.

1. Välj **Använda banmappningar**. I _Fil/katalog_ -rutan, roten för projektet för `serverName` visas.

1. I **Absolut sökväg på servern** klickar du på **Redigera** och lägga till en inställning baserad på miljön.

   - För alla Starter-miljöer och Pro-integreringsmiljöer är fjärrsökvägen `/app`.
   - För Pro Staging- och Production-miljöer:

      - Produktion: `/app/<project_code>/`
      - Mellanlagring:  `/app/<project_code>_stg/`

1. Ändra [!DNL Xdebug] port till 9000 i **Språk och ramar** > **PHP** > **Felsök** > **Xdebug** > **Felsökningsport** -panelen.

1. Klicka **Använd**.

### Konfigurera portvidarebefordran

Mappa `XDEBUG` anslutning från servern till ditt lokala system. För att kunna utföra alla typer av felsökning måste du vidarebefordra port 9000 från din Adobe Commerce på molninfrastrukturservern till din lokala dator. Se något av följande avsnitt:

- [Portvidarebefordran på Mac eller UNIX](#port-forwarding-on-mac-or-unix)
- [Portvidarebefordran i Windows](#port-forwarding-on-windows)

#### Portvidarebefordran på Mac eller UNIX®

**Konfigurera portvidarebefordran på en Mac eller i en UNIX®-miljö**:

1. Öppna en terminal.

1. Använd SSH för att upprätta anslutningen.

   ```bash
   ssh -R 9000:localhost:9000 <ssh url>
   ```

   Använd `-v` (utförligt) så att när en socket är ansluten till porten som vidarebefordras visas den i terminalen.

   Om ett fel av typen&quot;Det gick inte att ansluta&quot; eller&quot;det gick inte att lyssna på porten på fjärrservern&quot; visas, kan det finnas en annan aktiv SSH-session som är beständig på servern och som upptar port 9000. Om den anslutningen inte används kan du avsluta den.

**Felsöka anslutningen**:

1. Använd SSH för att logga in på fjärrintegrerings-, mellanlagrings- eller produktionsmiljön.

1. Visa en lista över SSH-sessioner: `who`

1. Visa befintliga SSH-sessioner per användare. Var noga med att inte påverka andra användare än dig själv!

   - integration: användarnamn liknar `dd2q5ct7mhgus`
   - Mellanlagring: användarnamn liknar `dd2q5ct7mhgus_stg`
   - Produktion: användarnamn liknar `dd2q5ct7mhgus`

1. För en användarsession som är äldre än din finns pseudoterminalvärdet (PTS), som `pts/0`.

1. Avsluta process-ID (PID) som motsvarar PTS-värdet.

   ```bash
   ps aux | grep ssh
   kill <PID>
   ```

   Exempelsvar:

   ```terminal
   dd2q5ct7mhgus        5504  0.0  0.0  82612  3664 ?      S    18:45   0:00 sshd: dd2q5ct7mhgus@pts/0
   ```

   Om du vill avsluta anslutningen anger du ett avslutskommando med process-ID (PID).

   ```bash
   kill 3664
   ```

#### Portvidarebefordran i Windows

Om du vill konfigurera portvidarebefordran (SSH-tunnling) på Windows måste du konfigurera Windows-terminalprogrammet. I det här exemplet beskrivs hur du skapar en SSH-tunnel med [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html). Du kan använda andra program som Cygwin. Mer information om andra program finns i leverantörsdokumentationen som medföljer dessa program.

**Konfigurera en SSH-tunnel i Windows med Putty**:

1. Hämta om du inte redan har gjort det [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

1. Starta Putty.

1. Klicka på i kategorirutan **Session**.

1. Ange följande information:

   - **Värdnamn (eller IP-adress)** fält: Ange [SSH-URL](../development/secure-connections.md#connect-to-a-remote-environment) för din molnserver
   - **Port** fält: Retur `22`

   ![Konfigurera Putty](../../assets/xdebug/putty-session.png)

1. I _Kategori_ ruta, klicka **Anslutning** > **SSH** > **Tunnlar**.

1. Ange följande information:

   - **Källport** fält: Retur `9000`
   - **Mål** fält: Retur `127.0.0.1:9000`
   - Klicka **Fjärr**

1. Klicka **Lägg till**.

   ![Skapa en SSH-tunnel i Putty](../../assets/xdebug/putty-tunnels.png)

1. I _Kategori_ ruta, klicka **Session**.

1. I **Sparade sessioner** anger du ett namn för den här SSH-tunneln.

1. Klicka **Spara**.

   ![Spara SSH-tunneln](../../assets/xdebug/putty-session-save.png)

1. Om du vill testa SSH-tunneln klickar du på **Läs in** och sedan klicka **Öppna**.

   Om ett &quot;Det går inte att ansluta&quot;-fel visas kontrollerar du följande:

   - Alla mjuka inställningar är korrekta
   - Du kör Putty på den dator där din privata Adobe Commerce på SSH-nycklar för molninfrastruktur finns

## SSH-åtkomst till Xdebug-miljöer

För att starta felsökning, utföra inställningar med mera behöver du SSH-kommandona för att komma åt miljöerna. Du kan hämta den här informationen via [[!DNL Cloud Console]](../development/secure-connections.md#use-an-ssh-command) och ditt projektkalkylblad.

För Starter-miljöer och Pro-integreringsmiljöer kan du använda följande `magento-cloud` CLI-kommando för SSH i dessa miljöer:

```bash
magento-cloud environment:ssh --pipe -e <environment-ID>
```

Används [!DNL Xdebug], SSH till miljön enligt följande:

```bash
ssh -R <xdebug listen port>:<host>:<xdebug listen port> <SSH-URL>
```

Exempel:

```bash
ssh -R 9000:localhost:9000 pwga8A0bhuk7o-mybranch@ssh.us.magentosite.cloud
```

## Debug for Pro Staging and Production

>[!NOTE]
>
>I Pro Staging &amp; Production-miljöer [!DNL Xdebug] är alltid tillgängligt eftersom dessa miljöer har särskilda inställningar för [!DNL Xdebug]. Alla vanliga webbförfrågningar dirigeras till en dedikerad PHP-process som inte har [!DNL Xdebug]. Därför behandlas dessa begäranden normalt och påverkas inte av prestandaförsämringar när [!DNL Xdebug] har lästs in. När en webbförfrågan skickas har den [!DNL Xdebug] den dirigeras till en separat PHP-process som har [!DNL Xdebug] inläst.

Används [!DNL Xdebug] i Pro-planens miljö för mellanlagring och produktion skapar du en separat SSH-tunnel och webbsession som bara du har tillgång till. Den här användningen skiljer sig från den vanliga åtkomsten, som bara ger dig åtkomst och inte till alla användare.

Du behöver följande:

- SSH-kommandon för åtkomst till miljöer. Du kan hämta den här informationen via [[!DNL Cloud Console]](../project/overview.md) eller [!DNL Cloud Onboarding UI].
- The `xdebug_key` värdet anges när du konfigurerar miljöer av typen Förproduktion och Pro.

  The `xdebug_key` kan hittas genom att använda SSH för att logga in på den primära noden och köra:

  ```bash
  cat /etc/platform/*/nginx.conf | grep xdebug.sock | head -n1
  ```

**Konfigurera en SSH-tunnel till en mellanlagrings- eller produktionsmiljö**:

1. Öppna en terminal.

1. Rensa alla SSH-sessioner för varje webbnod i klustret.

   ```bash
   ssh USERNAME@CLUSTER.ent.magento.cloud 'rm /run/platform/USERNAME/xdebug.sock'
   ```

1. Konfigurera SSH-tunneln för Xdebug för varje webbnod i klustret.

   ```bash
   ssh -R /run/platform/USERNAME/xdebug.sock:localhost:9000 -N USERNAME@CLUSTER.ent.magento.cloud
   ```

**Så här startar du felsökningen med URL:en för miljön**:

1. Aktivera fjärrfelsökning. Gå till webbplatsen i webbläsaren och lägg till följande till den URL där `KEY` är värde för `xdebug_key`.

   ```http
   ?XDEBUG_SESSION_START=KEY
   ```

   I det här steget anges den cookie som skickar webbläsarbegäranden till utlösaren [!DNL Xdebug].

1. Slutför felsökningen med [!DNL Xdebug].

1. När du är redo att avsluta sessionen använder du följande kommando för att ta bort cookien och avsluta felsökningen via webbläsaren där `KEY` är värde för `xdebug_key`.

   ```http
   ?XDEBUG_SESSION_STOP=KEY
   ```

   >[!NOTE]
   >
   >The `XDEBUG_SESSION_START` passerad av `POST` begäranden stöds inte.

## Felsöka CLI-kommandon

I det här avsnittet beskrivs CLI-kommandona för felsökning.

Så här felsöker du CLI-kommandon:

1. SSH in på den server som du vill felsöka med CLI-kommandon.

1. Skapa följande miljövariabler:

   ```bash
   export XDEBUG_CONFIG='PHPSTORM'
   ```

   ```bash
   export PHP_IDE_CONFIG="serverName=<name of the server that is configured in PHPSTORM>"
   ```

   Dessa variabler tas bort när SSH-sessionen avslutas.

1. Starta felsökning

   Kör CLI-kommandot för att felsöka i Starter-miljöer och i Pro-integreringsmiljöer.
Du kan lägga till körningsalternativ, till exempel:

   ```bash
   php -d xdebug.profiler_enable=On -d xdebug.max_nesting_level=9999 bin/magento cache:clean
   ```

   I Pro Staging- och Production-miljöer måste du ange sökvägen till [!DNL Xdebug] PHP-konfigurationsfil vid felsökning av CLI-kommandon, till exempel:

   ```bash
   php -c /etc/platform/USERNAME/php.xdebug.ini bin/magento cache:clean
   ```

## Felsöka webbförfrågningar

Följande steg hjälper dig att felsöka webbförfrågningar.

1. På _Tillägg_ meny, klicka **Felsök** för att aktivera.

1. Högerklicka, välj alternativmenyn och ställ in IDE-tangenten på **PHPSTORM**.

1. Installera [!DNL Xdebug] i webbläsaren. Konfigurera och aktivera den.

### Exempel: Chrome-inställning

I det här avsnittet beskrivs hur du använder [!DNL Xdebug] i Chrome med [!DNL Xdebug] Hjälptillägg. Mer information om [!DNL Xdebug] för andra webbläsare, se webbläsardokumentationen.

**Använda Xdebug Helper med Chrome**:

1. Skapa en [SSH-tunnel](#ssh-access-to-xdebug-environments) till molnservern.

1. Installera [Hjälptillägg för Xdebug](https://chromewebstore.google.com/detail/eadndfjplgieldjbigjakmdgkmoaaaoc) från Chrome Store.

1. Aktivera tillägget i Chrome enligt följande bild.

   ![Aktivera tillägget Xdebug i Chrome](../../assets/xdebug/enable-chrome-ext.png)

1. I Chrome högerklickar du på den gröna hjälpikonen i verktygsfältet i Chrome.

1. På popup-menyn klickar du på **Alternativ**.

1. Från _IDE-nyckel_ lista, klicka på **PhpStorm**.

1. Klicka **Spara**.

   ![Hjälpalternativ för Xdebug](../../assets/xdebug/helper-options.png)

1. Öppna ditt PhpStorm-projekt.

1. I det övre navigeringsfältet klickar du på **Börja lyssna** -ikon.

   Om navigeringsfältet inte visas klickar du på **Visa** > **Navigeringsfält**.

1. Dubbelklicka på den PHP-fil som ska testas i PHpStorm-navigeringsrutan.

## Felsöka lokal kod

På grund av skrivskyddade miljöer måste du hämta kod till den lokala arbetsstationen från en miljö eller en specifik Git-gren för att kunna utföra felsökning.

Det är upp till dig att välja metod. Du har följande alternativ:

- Checka ut kod från Git och kör `composer install`

  Den här metoden fungerar om inte `composer.json` refererar till paket i privata databaser som du inte har åtkomst till. Den här metoden leder till att hela Adobe Commerce-kodbasen hämtas.

- Kopiera `vendor`, `app`, `pub`, `lib`och `setup` kataloger

  Den här metoden gör att du får all kod som du kan testa. Beroende på hur många statiska resurser du har kan det resultera i en lång överföring med en stor mängd filer.

- Kopiera `vendor` endast katalog

  Eftersom större delen av koden finns i `vendor` den här metoden kommer troligen att resultera i bra testning, men testar inte hela kodbasen.

**Komprimera filer och kopiera dem till din lokala dator**:

1. Använd SSH för att logga in i fjärrmiljön.

1. Komprimera filerna.

   ```bash
   tar -czf /tmp/<file-name>.tgz <directory list>
   ```

   Om du till exempel vill komprimera `vendor` endast katalog:

   ```bash
   tar -czf /tmp/vendor.tgz vendor
   ```

1. I din lokala miljö använder du PhpStorm för att komprimera filerna.

   ```bash
   cd <phpstorm project root dir>
   ```

   ```bash
   rsync <SSH-URL>:/tmp/<file-name>.tgz .
   ```

   ```bash
   tar xzf <file-name>.tgz
   ```
