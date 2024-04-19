---
source-git-commit: 6d8c082d78259f8f7adb0fb7f11ff4fcdb234124
workflow-type: tm+mt
source-wordcount: '4030'
ht-degree: 0%

---
# ece-tools

<!-- The template to render with above values -->
**Version**: 2002.1.18

Referensen innehåller 34 kommandon som är tillgängliga via `ece-tools` kommandoradsverktyg.
Den inledande listan genereras automatiskt med `ece-tools list` på Adobe Commerce om molninfrastruktur.

>[!NOTE]
>
>Den här referensen genereras från programmets kodbas. Om du vill ändra innehållet kan du uppdatera källkoden för motsvarande kommandoimplementering i [kodbas](https://github.com/magento/magento-cloud-cli) arkivera och skicka in dina ändringar för granskning. Ett annat sätt är att _Ge oss feedback_ (hitta länken i det övre högra hörnet). Information om riktlinjer för bidrag finns i [Kodavgifter](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

## `_complete`

Internt kommando för att ge förslag på komplettering av skalet

```bash
ece-tools _complete [-s|--shell SHELL] [-i|--input INPUT] [-c|--current CURRENT] [-a|--api-version API-VERSION] [-S|--symfony SYMFONY]
```

### `--shell`, `-s`

Skaltypen (&quot;bash&quot;, &quot;fish&quot;, &quot;zsh&quot;)

- Kräver ett värde

### `--input`, `-i`

En array med indatatoken (t.ex. COMP_WORDS eller argv)

- Standard: `[]`
- Kräver ett värde

### `--current`, `-c`

Indexvärdet för den inmatningsarray där markören finns (t.ex. COMP_CWORD)

- Kräver ett värde

### `--api-version`, `-a`

API-versionen av det slutförda skriptet

- Kräver ett värde

### `--symfony`, `-S`

inaktuell

- Kräver ett värde

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `build`

Skapar program.

```bash
ece-tools build
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `completion`

Dumpa skriptet för gränssnittets slutförande

```bash
ece-tools completion [--debug] [--] [<shell>]
```


### `shell`

Gränssnittstypen (t.ex. &quot;bash&quot;), värdet för &quot;$SHELL&quot; env var, används om detta inte anges


### `--debug`

Avsluta felsökningsloggen

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `db-dump`

Skapar säkerhetskopiering av databaser.

```bash
ece-tools db-dump [-d|--remove-definers] [-a|--dump-directory DUMP-DIRECTORY] [--] [<databases>...]
```


### `databases`

Databaser för säkerhetskopiering. Tillgängliga värden: [försäljning av huvudofferter]. Om argumentvärdet inte anges skapas databassäkerhetskopior med hjälp av inloggningsuppgifterna som lagras i `MAGENTO_CLOUD_RELATIONSHIP` miljövariabel eller/och `stage.deploy.DATABASE_CONFIGURATION` -egenskapen i .magento.env.yaml-konfigurationsfilen.

- Standard: `[]`

- Array

### `--remove-definers`, `-d`

Ta bort definitioner från databasdumpen

- Standard: `false`
- Accepterar inte ett värde

### `--dump-directory`, `-a`

Använd alternativ katalog för att spara dumpen

- Kräver ett värde

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `deploy`

Distribuerar programmet.

```bash
ece-tools deploy
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `help`

Visa hjälp för ett kommando

```bash
ece-tools help [--format FORMAT] [--raw] [--] [<command_name>]
```


### `command_name`

Kommandonamnet

- Standard: `help`


### `--format`

Utdataformatet (txt, xml, json eller md)

- Standard: `txt`
- Kräver ett värde

### `--raw`

Hjälp för att skriva ut råformat

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `list`

Listkommandon

```bash
ece-tools list [--raw] [--format FORMAT] [--short] [--] [<namespace>]
```


### `namespace`

Namnutrymmets namn


### `--raw`

Utdata för kommandolista

- Standard: `false`
- Accepterar inte ett värde

### `--format`

Utdataformatet (txt, xml, json eller md)

- Standard: `txt`
- Kräver ett värde

### `--short`

Så här beskriver du inte kommandots argument

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `patch`

Använder anpassade patchar.

```bash
ece-tools patch
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `post-deploy`

Utför efter distributionsåtgärder.

```bash
ece-tools post-deploy
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `run`

Kör scenarier.

```bash
ece-tools run <scenario>...
```


### `scenario`

Scenario(er)

- Standard: `[]`

- Obligatoriskt
- Array

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `backup:list`

Visar en lista med säkerhetskopierade filer.

```bash
ece-tools backup:list
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `backup:restore`

Återställ viktiga konfigurationsfiler. Kör säkerhetskopiering:lista för att visa listan med säkerhetskopierade filer.

```bash
ece-tools backup:restore [-f|--force] [--file [FILE]]
```

### `--force`, `-f`

Skriv över befintliga filer under återställning av en säkerhetskopia

- Standard: `false`
- Accepterar inte ett värde

### `--file`

En specifik filåterställningssökväg

- Accepterar ett värde

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `build:generate`

Genererar alla filer som behövs för byggfasen.

```bash
ece-tools build:generate
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `build:transfer`

Överför genererade filer till init-katalogen.

```bash
ece-tools build:transfer
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `cloud:config:create`

Skapar en `.magento.env.yaml` fil med den angivna variabelkonfigurationen för bygge, distribution och efterdistribution. Skriver över befintliga `.magento,.env.yaml` -fil.

```bash
ece-tools cloud:config:create <configuration>
```


### `configuration`

Konfiguration i JSON-format

- Obligatoriskt

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `cloud:config:update`

Uppdaterar befintliga `.magento.env.yaml` fil med den angivna konfigurationen. Skapar `.magento.env.yaml` om filen inte finns.

```bash
ece-tools cloud:config:update <configuration>
```


### `configuration`

Konfiguration i JSON-format

- Obligatoriskt

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `cloud:config:validate`

Validerar `.magento.env.yaml` konfigurationsfil

```bash
ece-tools cloud:config:validate
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `config:dump`

Dumpa konfigurationen för statisk innehållsdistribution.

```bash
ece-tools config:dump
```


```bash
ece-tools dump
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `cron:disable`

Inaktivera alla Magento cron-processer och avsluta alla processer som körs.

```bash
ece-tools cron:disable
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `cron:enable`

Möjliggör Magento cron-processer.

```bash
ece-tools cron:enable
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `cron:kill`

Avslutar alla Magento cron-processer.

```bash
ece-tools cron:kill
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `cron:unlock`

Lås upp cron-jobb som fastnat i körläge.

```bash
ece-tools cron:unlock [--job-code [JOB-CODE]]
```

### `--job-code`

Upplås genom att krona jobbkoden.

- Standard: `[]`
- Accepterar flera värden

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `dev:generate:schema-error`

Skapar dist/error-codes.md från filen schema.error.yaml.

```bash
ece-tools dev:generate:schema-error
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `dev:git:update-composer`

Uppdaterar disposition för distribution från Git.

```bash
ece-tools dev:git:update-composer
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `env:config:show`

Visa miljövariabler för kodad molnkonfiguration.

```bash
ece-tools env:config:show [<variable>...]
```


### `variable`

Miljövariabler som ska visas, möjliga alternativ: tjänster, flöden, variabler

- Standard: `[]`

- Array

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `error:show`

Visar information om fel med fel-ID eller information om alla fel från den senaste distributionen.

```bash
ece-tools error:show [-j|--json] [--] [<error-code>]
```


### `error-code`

Felkod: Om kommandot inte skickas visas information om alla fel från den senaste distributionen


### `--json`, `-j`

Används för att få resultat i JSON-format

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `module:refresh`

Uppdaterar konfigurationen för att aktivera nya moduler.

```bash
ece-tools module:refresh
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `schema:generate`

Skapar schemafilen *.dist.

```bash
ece-tools schema:generate
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `wizard:ideal-state`

Verifierar det idealiska konfigurationstillståndet.

```bash
ece-tools wizard:ideal-state
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `wizard:master-slave`

Verifierar konfigurationen av master-slave.

```bash
ece-tools wizard:master-slave
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `wizard:scd-on-build`

Verifierar SCD vid konfiguration av bygge.

```bash
ece-tools wizard:scd-on-build
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `wizard:scd-on-demand`

Verifierar konfiguration av SCD vid behov.

```bash
ece-tools wizard:scd-on-demand
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `wizard:scd-on-deploy`

Verifierar SCD vid distributionskonfiguration.

```bash
ece-tools wizard:scd-on-deploy
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde


## `wizard:split-db-state`

Verifierar möjligheten att dela DB och om DB redan delats eller inte.

```bash
ece-tools wizard:split-db-state
```

### `--help`, `-h`

Visa hjälp för det angivna kommandot. När inget kommando anges visas hjälpen för listkommandot

- Standard: `false`
- Accepterar inte ett värde

### `--quiet`, `-q`

Skriv inget meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas utförlighet: 1 för normal utskrift, 2 för mer utförlig utskrift och 3 för felsökning

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--ansi`

Tvinga (eller inaktivera) ANSI-utdata

- Accepterar inte ett värde

### `--no-ansi`

Ignorera alternativet &quot;—ansi&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`, `-n`

Ställ inga interaktiva frågor

- Standard: `false`
- Accepterar inte ett värde

