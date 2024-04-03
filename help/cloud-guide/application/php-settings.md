---
title: PHP-inställningar
description: Lär dig mer om de optimala PHP-inställningarna för konfiguration av Commerce-program i molninfrastrukturen.
feature: Cloud, Configuration, Extensions
exl-id: b4180265-f7a1-48e4-8c23-27835253e171
source-git-commit: 9b3772cf640ebc56063434e1aa8acb1ec51dc63c
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# PHP-inställningar

Du kan välja vilken [PHP-version](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) för att köra `.magento.app.yaml` fil:

```yaml
name: mymagento
type: php:<version>
```

>[!TIP]
>
>Om du uppgraderar till PHP 8.1 och senare tar du bort JSON från [`runtime: extensions:` property](properties.md#runtime) i `.magento.app.yaml` och distribuera om. JSON-tillägget installeras i molnmiljön sedan PHP 8.0.

## Konfigurera PHP

Du kan anpassa PHP-inställningarna för din miljö med en `php.ini` som läggs till i konfigurationen som hanteras av Adobe Commerce.

Lägg till `php.ini` till programmets rot (databasroten).

>[!TIP]
>
>Om du konfigurerar PHP-inställningar på ett felaktigt sätt kan det uppstå problem, så endast avancerade administratörer bör ange dessa alternativ.

### Öka PHP-minnesgränsen

Om du vill öka PHP-minnesgränsen lägger du till följande inställning i `php.ini` fil:

```ini
memory_limit = 1G
```

För felsökning ökar du värdet till 2G.

### Optimera konfigurationen för realpath_cache

Ange följande `realpath_cache` för att förbättra programmets prestanda.

```conf
;
; Increase realpath cache size
;
realpath_cache_size = 10M

;
; Increase realpath cache ttl
;
realpath_cache_ttl = 7200
```

Med de här inställningarna kan PHP-processer cachelagra sökvägar till filer i stället för att leta upp dem för varje sidinläsning. Se [Prestandajustering](https://www.php.net/manual/en/ini.core.php) i PHP-dokumentationen.

>[!NOTE]
>
>En lista över rekommenderade PHP-konfigurationsinställningar finns i [Nödvändiga PHP-inställningar](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html) i _Installationsguide_.

### Kontrollera anpassade PHP-inställningar

När du har tryckt in `php.ini` ändringar i molnmiljön kan du kontrollera att den anpassade PHP-konfigurationen har lagts till i din miljö. Använd till exempel SSH för att logga in i fjärrmiljön och visa filen med något som liknar följande:

```bash
cat /etc/php/<php-version>/fpm/php.ini
```

>[!WARNING]
>
>Om du använder Cloud Docker för Commerce för lokal utveckling, se [Dockningsbehållare](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#fpm-container) för information om hur du använder en anpassad `php.ini` i en Docker-miljö.

## Aktivera tillägg

Du kan aktivera eller inaktivera PHP-tillägg i dialogrutan `runtime:extension` -avsnitt. Dessutom blir de angivna tilläggen tillgängliga i Docker PHP-behållarna.

>[!IMPORTANT]
>
>Innan du aktiverar tillägg är det viktigt att du förstår att PHP-versionen måste vara kompatibel med det operativsystem som är värd för projektet. Din projektmiljö kan kräva att infrastrukturteamet uppgraderar operativsystemet innan du kan fortsätta.

Exempel i `.magento.app.yaml` fil:

```yaml
runtime:
    extensions:
        - sockets
        - sodium
        - ssh2
    disabled_extensions:
        - bcmath
        - bz2
        - calendar
        - exif
```

Använd SSH för att logga in i en miljö och lista PHP-tilläggen.

```bash
php -m
```

Mer information om ett specifikt PHP-tillägg finns i [PHP-tilläggslista](https://www.php.net/manual/en/extensions.alphabetical.php).

Följande tabell visar vilka PHP-tillägg som stöds när du distribuerar Adobe Commerce på molnplattformen.

| Standardtillägg | Installerade tillägg<br>som inte kan avinstalleras | Tillägg som kan installeras<br>och avinstalleras efter behov |
| ------------------ | --------------------- | --------------------- |
| `bcmath`<br>`bz2`<br>`calendar`<br>`exif`<br>`gd`<br>`gettext`<br> `intl`<br> `mysqli`<br> `openswoole`<br> `pcntl`<br> `pdo_mysql`<br> `soap`<br> `sockets`<br>  `sysvmsg`<br> `sysvsem`<br> `sysvshm`<br> `opcache`<br> `zip` | `ctype`<br> `curl`<br>`date`<br> `dom`<br> `fileinfo`<br> `filter`<br> `ftp`<br> `hash`<br> `iconv`<br> `json`<br> `mbstring`<br> `mysqlnd`<br> `openssl`<br> `pcre`<br> `pdo`<br> `pdo_sqlite`<br> `phar`<br>`posix`<br> `readline`<br> `session`<br> `sqlite3`<br> `tokenizer`<br> `xml`<br> `xmlreader`<br> `xmlwriter`<br> | `geoip`<br>`gmp`<br> `igbinary`<br> `imagick`<br> `imap`<br> `ioncube` <br>`ldap`<br> `mailparse`<br> `mcrypt`<br> `msgpack`<br> `mysqli`<br> `oauth`<br> `pdo_mysql`<br> `propro`<br> `pspell`<br> `raphf`<br> `recode`<br> `redis`<br> `shmop` `sockets`<br> `sodium`<br> `ssh2`<br>`tidy`<br> `xdebug`<br> `xmlrpc`<br> `xsl`<br> `yaml` |

PHP-modulkraven är knutna till Adobe Commerce-versionen. Se [PHP-krav](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html).

### Stöd för tillägg

För Pro-projekt krävs ytterligare stöd för följande tillägg:

- `sourceguardian`

Om du till exempel vill konfigurera PHP så att bara SourceGuardian-skyddade skript körs i alla miljöer måste följande alternativ anges i `php.ini` fil:

```ini
[SourceGuardian]
sourceguardian.restrict_unencoded = "1"
```

Se [avsnitt 3.5 i SourceGuardian-dokumentationen](https://sourceguardian.com/demofiles/files/SourceGuardian%20for%20Linux%20User%20Manual.pdf). _Det här är en länk till en PDF_.

[Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om du vill ha hjälp med att installera dessa PHP-tillägg i alla produktionsmiljöer och i Pro Staging-miljöer. Inkludera dina uppdaterade `.magento/services.yaml` fil, `.magento.app.yaml` med den uppdaterade PHP-versionen och eventuella ytterligare PHP-tillägg. Om du vill ändra en produktionsmiljö måste du ange minst 48 timmars varsel. Det kan ta upp till 48 timmar för molninfrastrukturteamet att uppdatera ditt projekt.

>[!WARNING]
>
>PHP kompilerad med felsökning stöds inte och sonden kan hamna i konflikt med [!DNL XDebug] eller [!DNL XHProf]. Inaktivera dessa tillägg när du aktiverar avsökningen. Avsökningen står i konflikt med vissa PHP-tillägg som [!DNL Pinba] eller IonCube.
