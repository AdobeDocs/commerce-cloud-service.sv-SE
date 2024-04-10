---
source-git-commit: 99272d08a11f850a79e8e24857b7072d1946f374
workflow-type: tm+mt
source-wordcount: '21442'
ht-degree: 0%

---
# magento-cloud (Adobe Commerce on cloud infrastructure)

<!-- The template to render with above values -->
**Version**: 1.46.1

Den här referensen innehåller 119 kommandon som är tillgängliga via `magento-cloud` kommandoradsverktyg.
Den inledande listan genereras automatiskt med `magento-cloud list` på Adobe Commerce om molninfrastruktur.

>[!NOTE]
>
>Den här referensen genereras från programmets kodbas. Om du vill ändra innehållet kan du uppdatera källkoden för motsvarande kommandoimplementering i [kodbas](https://github.com/magento/magento-cloud-cli) arkivera och skicka in dina ändringar för granskning. Ett annat sätt är att _Ge oss feedback_ (hitta länken i det övre högra hörnet). Information om riktlinjer för bidrag finns i [Kodavgifter](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

## `clear-cache`

Rensa CLI-cachen

```bash
magento-cloud cc
```

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `decode`

Avkoda en kodad sträng som MAGENTO_CLOUD_VARIABLES

```bash
magento-cloud decode [-P|--property PROPERTY] [--] <value>
```


### `value`

Variabelvärdet som ska avkodas

- Obligatoriskt

### `--property`, `-P`

Den egenskap som ska visas i variabeln

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `docs`

Öppna onlinedokumentationen

```bash
magento-cloud docs [--browser BROWSER] [--pipe] [--] [<search>]...
```


### `search`

Sökord

- Standard: `[]`

- Array

### `--browser`

Webbläsaren som ska användas för att öppna URL-adressen. Ange 0 som ingen.

- Kräver ett värde

### `--pipe`

Skriv ut URL-adressen som ska stoppas.

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `help`

Visar hjälp för ett kommando

```bash
magento-cloud help [--format FORMAT] [--raw] [--] [<command_name>]
```


### `command_name`

Kommandonamnet

- Standard: `help`


### `--format`

Utdataformatet (txt, json eller md)

- Standard: `txt`
- Kräver ett värde

### `--raw`

Hjälp för att skriva ut råformat

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `list`

Visar kommandon

```bash
magento-cloud list [--raw] [--format FORMAT] [--all] [--] [<namespace>]
```


### `command`

Kommandot som ska köras

- Obligatoriskt

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

### `--all`

Visa alla kommandon, även dolda

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `multi`

Kör ett kommando i flera projekt

```bash
magento-cloud multi [-p|--projects PROJECTS] [--continue] [--sort SORT] [--reverse] [--] <cmd> (<cmd>)...
```


### `cmd`

Kommandot som ska köras

- Standard: `[]`

- Obligatoriskt
- Array

### `--projects`, `-p`

En lista med projekt-ID:n, avgränsade med kommatecken och/eller blanksteg

- Kräver ett värde

### `--continue`

Fortsätt köra kommandon även om ett undantag påträffas

- Standard: `false`
- Accepterar inte ett värde

### `--sort`

En egenskap som listan med projektalternativ ska sorteras efter

- Standard: `title`
- Kräver ett värde

### `--reverse`

Invertera ordningen för projektalternativ

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `web`

Öppna projektet i webbgränssnittet

```bash
magento-cloud web [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--browser`

Webbläsaren som ska användas för att öppna URL-adressen. Ange 0 som ingen.

- Kräver ett värde

### `--pipe`

Skriv ut URL-adressen som ska stoppas.

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `activity:cancel`

Avbryt en aktivitet

```bash
magento-cloud activity:cancel [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

Aktivitets-ID. Standardvärdet är den senaste avbrutna aktiviteten.


### `--type`, `-t`

Filtrera efter typ (när du väljer en standardaktivitet). Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg. Tecknen % och * kan användas som jokertecken för typen, t.ex. &#39;%var%&#39; för att välja variabelrelaterade aktiviteter.

- Standard: `[]`
- Kräver ett värde

### `--exclude-type`, `-x`

Exkludera efter typ (när du väljer en standardaktivitet). Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg. Tecknen % och * kan användas som jokertecken för att utesluta typer.

- Standard: `[]`
- Kräver ett värde

### `--all`, `-a`

Kontrollera senaste aktiviteter i alla miljöer (när du väljer en standardaktivitet)

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `activity:get`

Visa detaljerad information om en enskild aktivitet

```bash
magento-cloud activity:get [-P|--property PROPERTY] [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<id>]
```


### `id`

Aktivitets-ID. Standardvärdet är den senaste aktiviteten.


### `--property`, `-P`

Egenskapen som ska visas

- Kräver ett värde

### `--type`, `-t`

Filtrera efter typ (när du väljer en standardaktivitet). Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg. Tecknen % och * kan användas som jokertecken för typen, t.ex. &#39;%var%&#39; för att välja variabelrelaterade aktiviteter.

- Standard: `[]`
- Kräver ett värde

### `--exclude-type`, `-x`

Exkludera efter typ (när du väljer en standardaktivitet). Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg. Tecknen % och * kan användas som jokertecken för att utesluta typer.

- Standard: `[]`
- Kräver ett värde

### `--state`

Filtrera efter läge (när du väljer en standardaktivitet): in_progress, pending, complete eller canceled. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--result`

Filtrera efter resultat (när du väljer en standardaktivitet): slutförd eller misslyckad

- Kräver ett värde

### `--incomplete`, `-i`

Inkludera endast ofullständiga aktiviteter (när du väljer en standardaktivitet). Det här är en förkortning för \&lt;info>—state=in_progress,pending\&lt;/info>

- Standard: `false`
- Accepterar inte ett värde

### `--all`, `-a`

Kontrollera senaste aktiviteter i alla miljöer (när du väljer en standardaktivitet)

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `activity:list`

Hämta en lista över aktiviteter för en miljö eller ett projekt

```bash
magento-cloud activities [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--type`, `-t`

Filtrera aktiviteter efter typ Värden kan delas upp med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg. Den första delen av aktivitetsnamnet kan utelämnas, t.ex. &quot;cron&quot; kan välja aktiviteter av typen &quot;environment.cron&quot;. Tecknen % och * kan användas som jokertecken, t.ex. &#39;%var%&#39; för att välja variabelrelaterade aktiviteter.

- Standard: `[]`
- Kräver ett värde

### `--exclude-type`, `-x`

Uteslut aktiviteter efter typ. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg. Den första delen av aktivitetsnamnet kan utelämnas, t.ex. kan &quot;cron&quot; utesluta aktiviteter av typen &quot;environment.cron&quot;. Tecknen % och * kan användas som jokertecken för att utesluta typer.

- Standard: `[]`
- Kräver ett värde

### `--limit`

Begränsa antalet resultat som visas

- Standard: `10`
- Kräver ett värde

### `--start`

Endast aktiviteter som skapats före detta datum listas

- Kräver ett värde

### `--state`

Filtrera aktiviteter efter tillstånd: in_progress, pending, complete eller canceled. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--result`

Filtrera aktiviteter efter resultat: lyckade eller misslyckade

- Kräver ett värde

### `--incomplete`, `-i`

Endast lista ofullständiga aktiviteter

- Standard: `false`
- Accepterar inte ett värde

### `--all`, `-a`

Visa aktiviteter i alla miljöer

- Standard: `false`
- Accepterar inte ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: id*, created*, description*, progress*, state*, result*, complete, environment, type (* = default columns). Tecknet&quot;+&quot; kan användas som platshållare för standardkolumnerna. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `activity:log`

Visa loggen för en aktivitet

```bash
magento-cloud activity:log [--refresh REFRESH] [-t|--timestamps] [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

Aktivitets-ID. Standardvärdet är den senaste aktiviteten.


### `--refresh`

Intervall för aktivitetsuppdatering (sekunder). Ange 0 om du vill inaktivera uppdatering.

- Standard: `3`
- Kräver ett värde

### `--timestamps`, `-t`

Visa en tidsstämpel bredvid varje meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--type`

Filtrera efter typ (när du väljer en standardaktivitet). Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg. Tecknen % och * kan användas som jokertecken för typen, t.ex. &#39;%var%&#39; för att välja variabelrelaterade aktiviteter.

- Standard: `[]`
- Kräver ett värde

### `--exclude-type`, `-x`

Exkludera efter typ (när du väljer en standardaktivitet). Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg. Tecknen % och * kan användas som jokertecken för att utesluta typer.

- Standard: `[]`
- Kräver ett värde

### `--state`

Filtrera efter läge (när du väljer en standardaktivitet): in_progress, pending, complete eller canceled. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--result`

Filtrera efter resultat (när du väljer en standardaktivitet): slutförd eller misslyckad

- Kräver ett värde

### `--incomplete`, `-i`

Inkludera endast ofullständiga aktiviteter (när du väljer en standardaktivitet). Det här är en förkortning för \&lt;info>—state=in_progress,pending\&lt;/info>

- Standard: `false`
- Accepterar inte ett värde

### `--all`, `-a`

Kontrollera senaste aktiviteter i alla miljöer (när du väljer en standardaktivitet)

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `app:config-get`

Visa konfigurationen för ett program

```bash
magento-cloud app:config-get [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

### `--property`, `-P`

Den konfigurationsegenskap som ska visas

- Kräver ett värde

### `--refresh`

Om cachen ska uppdateras

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--identity-file`, `-i`

[Inaktuellt alternativ, används inte längre]

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `app:list`

Visa program i projektet

```bash
magento-cloud apps [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Om cachen ska uppdateras

- Standard: `false`
- Accepterar inte ett värde

### `--pipe`

Skriv endast ut en lista med programnamn

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: namn*, typ*, disk, sökväg, storlek (* = standardkolumner). Tecknet&quot;+&quot; kan användas som platshållare för standardkolumnerna. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `auth:api-token-login`

Logga in på Magento Cloud med en API-token

```bash
magento-cloud auth:api-token-login
```

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `auth:browser-login`

Logga in på Magento Cloud via en webbläsare

```bash
magento-cloud login [-f|--force] [--browser BROWSER] [--pipe]
```

### `--force`, `-f`

Logga in igen, även om du redan är inloggad

- Standard: `false`
- Accepterar inte ett värde

### `--browser`

Webbläsaren som ska användas för att öppna URL-adressen. Ange 0 som ingen.

- Kräver ett värde

### `--pipe`

Skriv ut URL-adressen som ska stoppas.

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `auth:info`

Visa din kontoinformation

```bash
magento-cloud auth:info [--no-auto-login] [-P|--property PROPERTY] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--] [<property>]
```


### `property`

Kontoegenskapen som ska visas


### `--no-auto-login`

Hoppar över automatisk inloggning. Inget skrivs ut om det inte loggas in och avslutningskoden blir 0, förutsatt att inga andra fel inträffar.

- Standard: `false`
- Accepterar inte ett värde

### `--property`, `-P`

Den kontoegenskap som ska visas (alternativ syntax)

- Kräver ett värde

### `--refresh`

Om cachen ska uppdateras

- Standard: `false`
- Accepterar inte ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `auth:logout`

Logga ut från Magento Cloud

```bash
magento-cloud logout [-a|--all] [--other]
```

### `--all`, `-a`

Logga ut från alla lokala sessioner

- Standard: `false`
- Accepterar inte ett värde

### `--other`

Logga ut från andra lokala sessioner

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `blackfire:setup`

Konfigurera Blackfire.io-integrering för projektet

```bash
magento-cloud blackfire:setup [--server_id SERVER_ID] [--server_token SERVER_TOKEN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--server_id`

Server-ID

- Kräver ett värde

### `--server_token`

Servertoken

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `certificate:add`

Lägg till ett SSL-certifikat i projektet

```bash
magento-cloud certificate:add [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--cert`

Sökvägen till certifikatfilen

- Kräver ett värde

### `--key`

Sökvägen till certifikatets privata nyckelfil

- Kräver ett värde

### `--chain`

Sökvägen till certifikatkedjefilen

- Standard: `[]`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `certificate:delete`

Ta bort ett certifikat från projektet

```bash
magento-cloud certificate:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <id>
```


### `id`

Certifikat-ID (eller början av det)

- Obligatoriskt

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `certificate:get`

Visa ett certifikat

```bash
magento-cloud certificate:get [-P|--property PROPERTY] [--date-fmt DATE-FMT] [-p|--project PROJECT] [--] <id>
```


### `id`

Certifikat-ID (eller början av det)

- Obligatoriskt

### `--property`, `-P`

Certifikategenskapen som ska visas

- Kräver ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `certificate:list`

Visa projektcertifikat

```bash
magento-cloud certificates [--domain DOMAIN] [--exclude-domain EXCLUDE-DOMAIN] [--issuer ISSUER] [--only-auto] [--no-auto] [--ignore-expiry] [--only-expired] [--no-expired] [--pipe-domains] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--domain`

Filtrera efter domännamn (skiftlägesokänslig sökning)

- Kräver ett värde

### `--exclude-domain`

Uteslut certifikat, matcha efter domännamn (skiftlägesokänslig sökning)

- Kräver ett värde

### `--issuer`

Filtrera efter utfärdare

- Kräver ett värde

### `--only-auto`

Visa endast automatiskt tilldelade certifikat

- Standard: `false`
- Accepterar inte ett värde

### `--no-auto`

Visa endast manuellt tillagda certifikat

- Standard: `false`
- Accepterar inte ett värde

### `--ignore-expiry`

Visa både utgångna och ej utgångna certifikat

- Standard: `false`
- Accepterar inte ett värde

### `--only-expired`

Visa endast utgångna certifikat

- Standard: `false`
- Accepterar inte ett värde

### `--no-expired`

Visa endast certifikat som inte har upphört att gälla (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--pipe-domains`

Returnera endast en lista med domännamn som omfattas av certifikaten

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: skapad, domäner, förfallodatum, id, utfärdare. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `commit:get`

Visa implementeringsinformation

```bash
magento-cloud commit:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<commit>]
```


### `commit`

Verkställ SHA. Detta kan även acceptera suffixen &quot;HEAD&quot; och cirkumflex (^) eller tilde (~) för överordnade implementeringar.

- Standard: `HEAD`


### `--property`, `-P`

Den implementeringsegenskap som ska visas.

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `commit:list`

Listimplementeringar

```bash
magento-cloud commits [--limit LIMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<commit>]
```


### `commit`

Den första Git-implementeringen av SHA. Detta kan även acceptera suffixen &quot;HEAD&quot; och cirkumflex (^) eller tilde (~) för överordnade implementeringar.


### `--limit`

Antalet implementeringar som ska visas.

- Standard: `10`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: författare, datum, SHA, sammanfattning. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `db:dump`

Skapa en lokal dump av fjärrdatabasen

```bash
magento-cloud db:dump [--schema SCHEMA] [-f|--file FILE] [-d|--directory DIRECTORY] [-z|--gzip] [-t|--timestamp] [-o|--stdout] [--table TABLE] [--exclude-table EXCLUDE-TABLE] [--schema-only] [--charset CHARSET] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

### `--schema`

Schemat som ska dumpas. Uteslut att använda standardschemat (vanligen&quot;main&quot;).

- Kräver ett värde

### `--file`, `-f`

Ett anpassat filnamn för dumpen

- Kräver ett värde

### `--directory`, `-d`

En anpassad katalog för dumpen

- Kräver ett värde

### `--gzip`, `-z`

Komprimera dumpen med gzip

- Standard: `false`
- Accepterar inte ett värde

### `--timestamp`, `-t`

Lägg till en tidsstämpel i dumpfilnamnet

- Standard: `false`
- Accepterar inte ett värde

### `--stdout`, `-o`

Utdata till STDOUT i stället för en fil

- Standard: `false`
- Accepterar inte ett värde

### `--table`

Tabell som ska inkluderas

- Standard: `[]`
- Kräver ett värde

### `--exclude-table`

Tabell(er) som ska uteslutas

- Standard: `[]`
- Kräver ett värde

### `--schema-only`

Dumpa endast scheman, inga data

- Standard: `false`
- Accepterar inte ett värde

### `--charset`

Teckenuppsättningens kodning för dumpen

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--relationship`, `-r`

Den tjänstrelation som ska användas

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `db:size`

Beräkna diskanvändningen för en databas

```bash
magento-cloud db:size [-B|--bytes] [-C|--cleanup] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-i|--identity-file IDENTITY-FILE]
```

### `--bytes`, `-B`

Visa storlekar i byte.

- Standard: `false`
- Accepterar inte ett värde

### `--cleanup`, `-C`

Kontrollera om tabeller kan rensas och visa rekommendationer (endast InnoDb).

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--relationship`, `-r`

Den tjänstrelation som ska användas

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: max, percent_used, used. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `db:sql`

Kör SQL på fjärrdatabasen

```bash
magento-cloud sql [--raw] [--schema SCHEMA] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [--] [<query>]
```


### `query`

En SQL-sats som ska köras


### `--raw`

Producera råa, icke-tabulära utdata

- Standard: `false`
- Accepterar inte ett värde

### `--schema`

Schemat som ska användas. Uteslut att använda standardschemat (vanligen&quot;main&quot;). Skicka en tom sträng för att inte använda något schema.

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--relationship`, `-r`

Den tjänstrelation som ska användas

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `domain:add`

Lägg till en ny domän i projektet

```bash
magento-cloud domain:add [--cert CERT] [--key KEY] [--chain CHAIN] [--attach ATTACH] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Domännamnet

- Obligatoriskt

### `--cert`

Sökvägen till certifikatfilen för domänen

- Kräver ett värde

### `--key`

Sökvägen till den privata nyckelfilen för det angivna certifikatet.

- Kräver ett värde

### `--chain`

Sökvägen till certifikatkedjefilen eller -filerna för det angivna certifikatet

- Standard: `[]`
- Kräver ett värde

### `--attach`

Den produktionsdomän som den här ersätter i miljöns vägar. Krävs för icke-produktionsmiljöer.

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `domain:delete`

Ta bort en domän från projektet

```bash
magento-cloud domain:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Domännamnet

- Obligatoriskt

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `domain:get`

Visa detaljerad information om en domän

```bash
magento-cloud domain:get [-P|--property PROPERTY] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<name>]
```


### `name`

Domännamnet


### `--property`, `-P`

Domänegenskapen som ska visas

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `domain:list`

Hämta en lista över alla domäner

```bash
magento-cloud domains [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: name*, ssl*, created_at*, registered_name, replace_for, type, updated_at (* = standardkolumner). Tecknet&quot;+&quot; kan användas som platshållare för standardkolumnerna. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `domain:update`

Uppdatera en domän

```bash
magento-cloud domain:update [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Domännamnet

- Obligatoriskt

### `--cert`

Sökvägen till certifikatfilen för domänen

- Kräver ett värde

### `--key`

Sökvägen till den privata nyckelfilen för det angivna certifikatet.

- Kräver ett värde

### `--chain`

Sökvägen till certifikatkedjefilen eller -filerna för det angivna certifikatet

- Standard: `[]`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:activate`

Aktivera en miljö

```bash
magento-cloud environment:activate [--parent PARENT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```


### `environment`

Den eller de miljöer som ska aktiveras

- Standard: `[]`

- Array

### `--parent`

Ange en ny överordnad miljö innan du aktiverar

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:branch`

Gren och miljön

```bash
magento-cloud branch [--title TITLE] [--type TYPE] [--no-clone-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>] [<parent>]
```


### `id`

Den nya miljöns ID (filialnamn)


### `parent`

Den nya miljöns överordnade


### `--title`

Den nya miljöns titel

- Kräver ett värde

### `--type`

Den nya miljöns typ

- Kräver ett värde

### `--no-clone-parent`

Klona inte den överordnade miljöns data

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:checkout`

Kolla in en miljö

```bash
magento-cloud checkout [-i|--identity-file IDENTITY-FILE] [--] [<id>]
```


### `id`

ID för miljön som ska checkas ut. Exempel: &quot;sprint2&quot;


### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:delete`

Ta bort en eller flera miljöer

```bash
magento-cloud environment:delete [--delete-branch] [--no-delete-branch] [--type TYPE] [-t|--only-type ONLY-TYPE] [--exclude EXCLUDE] [--exclude-type EXCLUDE-TYPE] [--inactive] [--merged] [--allow-delete-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```


### `environment`

Den eller de miljöer som ska tas bort. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`

- Array

### `--delete-branch`

Ta bort Git-grenar för inaktiva miljöer, utan bekräftelse

- Standard: `false`
- Accepterar inte ett värde

### `--no-delete-branch`

Ta inte bort Git-grenar (inaktiva miljöer)

- Standard: `false`
- Accepterar inte ett värde

### `--type`

Ta bort alla miljöer av en typ (som läggs till andra markerade) Värden kan delas upp med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--only-type`, `-t`

Endast borttagningsmiljöer av en viss typ Värden kan delas upp med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--exclude`

Miljö(er) som inte ska tas bort. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--exclude-type`

Miljötyper som inte ska tas bort kan delas upp med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--inactive`

Ta bort alla inaktiva miljöer (lägga till andra markerade)

- Standard: `false`
- Accepterar inte ett värde

### `--merged`

Ta bort alla sammanfogade miljöer (lägga till andra markerade)

- Standard: `false`
- Accepterar inte ett värde

### `--allow-delete-parent`

Tillåt att miljöer med underordnade tas bort

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:http-access`

Uppdatera HTTP-åtkomstinställningar för en miljö

```bash
magento-cloud httpaccess [--access ACCESS] [--auth AUTH] [--enabled ENABLED] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--access`

Åtkomstbegränsning i formatet &quot;permission:address&quot;. Använd 0 för att rensa alla adresser.

- Standard: `[]`
- Kräver ett värde

### `--auth`

HTTP Basic-autentiseringsuppgifter i formatet &quot;username:password&quot;. Använd 0 för att rensa alla autentiseringsuppgifter.

- Standard: `[]`
- Kräver ett värde

### `--enabled`

Anger om åtkomstkontroll ska aktiveras: 1 för att aktivera, 0 för att inaktivera

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:info`

Läs eller ange egenskaper för en miljö

```bash
magento-cloud environment:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```


### `property`

Egenskapens namn


### `value`

Ange ett nytt värde för egenskapen


### `--refresh`

Om cachen ska uppdateras

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:init`

Initiera en miljö från en offentlig Git-databas

```bash
magento-cloud environment:init [--profile PROFILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <url>
```


### `url`

En URL till en Git-databas

- Obligatoriskt

### `--profile`

Profilens namn

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:list`

Få en lista över miljöer

```bash
magento-cloud environments [-I|--no-inactive] [--pipe] [--refresh REFRESH] [--sort SORT] [--reverse] [--type TYPE] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--no-inactive`, `-I`

Visa inte inaktiva miljöer

- Standard: `false`
- Accepterar inte ett värde

### `--pipe`

Skriv ut en enkel lista över miljö-ID:n.

- Standard: `false`
- Accepterar inte ett värde

### `--refresh`

Anger om listan ska uppdateras.

- Standard: `1`
- Kräver ett värde

### `--sort`

En egenskap som ska sorteras efter

- Standard: `title`
- Kräver ett värde

### `--reverse`

Sortera i omvänd ordning (fallande)

- Standard: `false`
- Accepterar inte ett värde

### `--type`

Filtrera listan efter miljötyp(er). Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: id*, title*, status*, type*, created, machine_name, updated (* = default columns). Tecknet&quot;+&quot; kan användas som platshållare för standardkolumnerna. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:logs`

Läs en miljös loggar

```bash
magento-cloud log [--lines LINES] [--tail] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [--] [<type>]
```


### `type`

Loggtypen, t.ex. &quot;access&quot; eller &quot;error&quot;


### `--lines`

Antalet rader som ska visas

- Standard: `100`
- Kräver ett värde

### `--tail`

Avsluta loggen kontinuerligt

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--worker`

Ett arbetarnamn

- Kräver ett värde

### `--instance`, `-I`

Ett instans-ID

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:merge`

Sammanfoga en miljö

```bash
magento-cloud merge [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```


### `environment`

Den miljö som ska sammanfogas


### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:pause`

Pausa en miljö

```bash
magento-cloud environment:pause [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:push`

Kodning i en miljö

```bash
magento-cloud push [--target TARGET] [-f|--force] [--force-with-lease] [-u|--set-upstream] [--activate] [--parent PARENT] [--type TYPE] [--no-clone-parent] [-W|--no-wait] [--wait] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-i|--identity-file IDENTITY-FILE] [--] [<source>]
```


### `source`

Källreferens: ett grennamn eller en implementerad hash

- Standard: `HEAD`


### `--target`

Målgrenens namn. Standardvärdet är den aktuella grenen.

- Kräver ett värde

### `--force`, `-f`

Tillåt icke-snabba framåtriktade uppdateringar

- Standard: `false`
- Accepterar inte ett värde

### `--force-with-lease`

Tillåt icke-snabba framåtriktade uppdateringar om fjärrspårningsgrenen är uppdaterad

- Standard: `false`
- Accepterar inte ett värde

### `--set-upstream`, `-u`

Ange målmiljön som den överordnade för källgrenen. Detta anger även målprojektet som fjärrplats för den lokala databasen.

- Standard: `false`
- Accepterar inte ett värde

### `--activate`

Aktivera miljön innan du trycker

- Standard: `false`
- Accepterar inte ett värde

### `--parent`

Ange den nya miljön som överordnad (används endast med —activate)

- Kräver ett värde

### `--type`

Ange miljötypen (används endast med —activate )

- Kräver ett värde

### `--no-clone-parent`

Klona inte den överordnade grenens data (används endast med —activate)

- Standard: `false`
- Accepterar inte ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:redeploy`

Distribuera om en miljö

```bash
magento-cloud redeploy [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:relationships`

Visa en miljös relationer

```bash
magento-cloud relationships [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<environment>]
```


### `environment`

Miljön


### `--property`, `-P`

Den relationsegenskap som ska visas

- Kräver ett värde

### `--refresh`

Om relationerna ska uppdateras

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:resume`

Återuppta en pausad miljö

```bash
magento-cloud environment:resume [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:scp`

Kopiera filer till och från en miljö med scp

```bash
magento-cloud scp [-r|--recursive] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE] [--] [<files>]...
```


### `files`

Filer att kopiera. Använd prefixet remote: för att definiera fjärrplatser.

- Standard: `[]`

- Array

### `--recursive`, `-r`

Kopiera hela kataloger rekursivt

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--worker`

Ett arbetarnamn

- Kräver ett värde

### `--instance`, `-I`

Ett instans-ID

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:ssh`

SSH till den aktuella miljön

```bash
magento-cloud ssh [--pipe] [--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE] [--] [<cmd>]...
```


### `cmd`

Ett kommando som körs i miljön.

- Standard: `[]`

- Array

### `--pipe`

Skriv bara ut SSH-URL:en.

- Standard: `false`
- Accepterar inte ett värde

### `--all`

Skriv ut alla SSH-URL:er (för alla program).

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--worker`

Ett arbetarnamn

- Kräver ett värde

### `--instance`, `-I`

Ett instans-ID

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:synchronize`

Synkronisera en miljös kod och/eller data från dess överordnade

```bash
magento-cloud sync [--rebase] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<synchronize>]...
```


### `synchronize`

Synkronisera: &quot;kod&quot;, &quot;data&quot; eller både och

- Standard: `[]`

- Array

### `--rebase`

Synkronisera kod genom att basera om i stället för att sammanfoga

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:url`

Hämta offentliga URL:er för en miljö

```bash
magento-cloud url [-1|--primary] [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--primary`, `-1`

Returnera bara URL:en för den primära vägen

- Standard: `false`
- Accepterar inte ett värde

### `--browser`

Webbläsaren som ska användas för att öppna URL-adressen. Ange 0 som ingen.

- Kräver ett värde

### `--pipe`

Skriv ut URL-adressen som ska stoppas.

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `environment:xdebug`

Öppna en tunnel för Xdebug i miljön

```bash
magento-cloud xdebug [--port PORT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--port`

Den lokala porten

- Standard: `9000`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--worker`

Ett arbetarnamn

- Kräver ett värde

### `--instance`, `-I`

Ett instans-ID

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `integration:activity:get`

Visa detaljerad information om en enskild integreringsaktivitet

```bash
magento-cloud integration:activity:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<integration>] [<activity>]
```


### `integration`

Ett integrerings-ID. Lämna tomt om du vill välja från en lista.


### `activity`

Aktivitets-ID. Som standard används den senaste integreringsaktiviteten.


### `--property`, `-P`

Egenskapen som ska visas

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

[Inaktuellt alternativ, används inte]

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `integration:activity:list`

Få en lista över aktiviteter för en integrering

```bash
magento-cloud int:act [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```


### `id`

Ett integrerings-ID. Lämna tomt om du vill välja från en lista.


### `--type`

Filtrera aktiviteter efter typ. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--exclude-type`, `-x`

Uteslut aktiviteter efter typ. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg. Tecknen % och * kan användas som jokertecken för att utesluta typer.

- Standard: `[]`
- Kräver ett värde

### `--limit`

Begränsa antalet resultat som visas

- Standard: `10`
- Kräver ett värde

### `--start`

Endast aktiviteter som skapats före detta datum listas

- Kräver ett värde

### `--state`

Filtrera aktiviteter efter stat. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--result`

Filtrera aktiviteter efter resultat

- Kräver ett värde

### `--incomplete`, `-i`

Endast lista ofullständiga aktiviteter

- Standard: `false`
- Accepterar inte ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: id*, created*, description*, type*, state*, result*, complete (* = default columns). Tecknet&quot;+&quot; kan användas som platshållare för standardkolumnerna. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

[Inaktuellt alternativ, används inte]

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `integration:activity:log`

Visa loggen för en integreringsaktivitet

```bash
magento-cloud integration:activity:log [-t|--timestamps] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<integration>] [<activity>]
```


### `integration`

Ett integrerings-ID. Lämna tomt om du vill välja från en lista.


### `activity`

Aktivitets-ID. Som standard används den senaste integreringsaktiviteten.


### `--timestamps`, `-t`

Visa en tidsstämpel bredvid varje meddelande

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

[Inaktuellt alternativ, används inte]

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `integration:add`

Lägg till en integrering i projektet

```bash
magento-cloud integration:add [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

### `--type`

Integrationstypen (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webkrok&#39;, &#39;health.email&#39;, &#39;health.pageruty&#39;, &#39;health.slack&#39;, &#39;health.webkrok&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;splunk&#39;, &#39;sumologic&#39;, &#39;syslog&#39;)

- Kräver ett värde

### `--base-url`

Bas-URL:en för serverinstallationen

- Kräver ett värde

### `--bitbucket-url`

Bas-URL:en för Bitbucket Server-installationen

- Kräver ett värde

### `--username`

Användarnamnet för Bitbucket Server

- Kräver ett värde

### `--token`

En token för autentisering eller åtkomst för integreringen

- Kräver ett värde

### `--key`

En Bitbucket OAuth-konsumentnyckel

- Kräver ett värde

### `--secret`

En Bitbucket OAuth-konsumenthemlighet

- Kräver ett värde

### `--license-key`

Licensnyckeln för New Relic Logs

- Kräver ett värde

### `--server-project`

Projektet (t.ex. &#39;namespace/repo&#39;)

- Kräver ett värde

### `--repository`

Den databas som ska spåras (t.ex. &#39;ägare/databas&#39;)

- Kräver ett värde

### `--build-merge-requests`

GitLab: skapa sammanfogningsbegäranden som miljöer

- Standard: `true`
- Kräver ett värde

### `--build-pull-requests`

Bygg upp alla förfrågningar som en miljö

- Standard: `true`
- Kräver ett värde

### `--build-draft-pull-requests`

Bygg släppbegäranden

- Standard: `true`
- Kräver ett värde

### `--build-pull-requests-post-merge`

Skapa pull-begäranden baserat på deras status efter sammanfogning

- Standard: `false`
- Kräver ett värde

### `--build-wip-merge-requests`

GitLab: skapa WIP-sammanslagningsbegäranden

- Standard: `true`
- Kräver ett värde

### `--merge-requests-clone-parent-data`

GitLab: klondata för sammanslagningsbegäranden

- Standard: `true`
- Kräver ett värde

### `--pull-requests-clone-parent-data`

Klona den överordnade miljöns data för pull-begäranden

- Standard: `true`
- Kräver ett värde

### `--resync-pull-requests`

Synkronisera miljödata för pull-begäran på nytt vid varje bygge

- Standard: `false`
- Kräver ett värde

### `--fetch-branches`

Hämta alla grenar från fjärrkontrollen (som inaktiva miljöer)

- Standard: `true`
- Kräver ett värde

### `--prune-branches`

Ta bort grenar som inte finns på fjärrkontrollen

- Standard: `true`
- Kräver ett värde

### `--resources-init`

De resurser som ska användas när en ny tjänst initieras (&#39;minimum&#39;, &#39;default&#39;, &#39;manual&#39;, &#39;parent&#39;)

- Kräver ett värde

### `--url`

Integreringens URL- eller API-slutpunkt

- Kräver ett värde

### `--shared-key`

Webkrok: den delade hemliga nyckeln för JWS

- Kräver ett värde

### `--file`

Namnet på en lokal fil som innehåller skriptet som ska överföras

- Kräver ett värde

### `--events`

En lista över händelser som ska hanteras, t.ex. environment.push

- Standard: `*`
- Kräver ett värde

### `--states`

En lista över lägen att agera på, t.ex. väntande, in_progress, slutfört

- Standard: `complete`
- Kräver ett värde

### `--environments`

De miljö-ID som ska inkluderas

- Standard: `*`
- Kräver ett värde

### `--excluded-environments`

De miljö-ID:n som ska uteslutas

- Standard: `[]`
- Kräver ett värde

### `--from-address`

[Valfritt] Anpassad avsändaradress för varningsmeddelanden

- Kräver ett värde

### `--recipients`

Mottagarens e-postadress(er)

- Standard: `[]`
- Kräver ett värde

### `--channel`

Kanalen Slack

- Kräver ett värde

### `--routing-key`

PagerDuty-routningsnyckeln

- Kräver ett värde

### `--category`

Kategorin Sumo Logic, som används för filtrering

- Kräver ett värde

### `--index`

Splunk-index

- Kräver ett värde

### `--sourcetype`

Källtypen för Splunk-händelsen

- Kräver ett värde

### `--protocol`

Syslog-transportprotokoll (&#39;tcp&#39;, &#39;udp&#39;, &#39;tls&#39;)

- Standard: `tls`
- Kräver ett värde

### `--syslog-host`

Syslog relay/collector host

- Kräver ett värde

### `--syslog-port`

Syslog-relä/insamlarport

- Kräver ett värde

### `--facility`

Syslog-funktion

- Standard: `1`
- Kräver ett värde

### `--message-format`

Syslog-meddelandeformat (&#39;rfc3164&#39; eller &#39;rfc5424&#39;)

- Standard: `rfc5424`
- Kräver ett värde

### `--auth-mode`

Autentiseringsläge (prefix eller Structure_data)

- Standard: `prefix`
- Kräver ett värde

### `--auth-token`

Autentiseringstoken

- Kräver ett värde

### `--verify-tls`

Om HTTPS-certifikatverifiering ska vara aktiverat (rekommenderas)

- Standard: `true`
- Kräver ett värde

### `--header`

HTTP-huvud(n) som ska användas vid POST-begäranden. Avgränsa namn och värden med kolon (:).

- Standard: `[]`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `integration:delete`

Ta bort en integrering från ett projekt

```bash
magento-cloud integration:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

Integrations-ID. Lämna tomt om du vill välja från en lista.


### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `integration:get`

Visa information om en integrering

```bash
magento-cloud integration:get [-P|--property [PROPERTY]] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<id>]
```


### `id`

Ett integrerings-ID. Lämna tomt om du vill välja från en lista.


### `--property`, `-P`

Den integrationsegenskap som ska visas

- Accepterar ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `integration:list`

Visa en lista över projektintegrering(ar)

```bash
magento-cloud integrations [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: id, sammanfattning, typ. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `integration:update`

Uppdatera en integrering

```bash
magento-cloud integration:update [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

ID för den integrering som ska uppdateras


### `--type`

Integrationstypen (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webkrok&#39;, &#39;health.email&#39;, &#39;health.pageruty&#39;, &#39;health.slack&#39;, &#39;health.webkrok&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;splunk&#39;, &#39;sumologic&#39;, &#39;syslog&#39;)

- Kräver ett värde

### `--base-url`

Bas-URL:en för serverinstallationen

- Kräver ett värde

### `--bitbucket-url`

Bas-URL:en för Bitbucket Server-installationen

- Kräver ett värde

### `--username`

Användarnamnet för Bitbucket Server

- Kräver ett värde

### `--token`

En token för autentisering eller åtkomst för integreringen

- Kräver ett värde

### `--key`

En Bitbucket OAuth-konsumentnyckel

- Kräver ett värde

### `--secret`

En Bitbucket OAuth-konsumenthemlighet

- Kräver ett värde

### `--license-key`

Licensnyckeln för New Relic Logs

- Kräver ett värde

### `--server-project`

Projektet (t.ex. &#39;namespace/repo&#39;)

- Kräver ett värde

### `--repository`

Den databas som ska spåras (t.ex. &#39;ägare/databas&#39;)

- Kräver ett värde

### `--build-merge-requests`

GitLab: skapa sammanfogningsbegäranden som miljöer

- Standard: `true`
- Kräver ett värde

### `--build-pull-requests`

Bygg upp alla förfrågningar som en miljö

- Standard: `true`
- Kräver ett värde

### `--build-draft-pull-requests`

Bygg släppbegäranden

- Standard: `true`
- Kräver ett värde

### `--build-pull-requests-post-merge`

Skapa pull-begäranden baserat på deras status efter sammanfogning

- Standard: `false`
- Kräver ett värde

### `--build-wip-merge-requests`

GitLab: skapa WIP-sammanslagningsbegäranden

- Standard: `true`
- Kräver ett värde

### `--merge-requests-clone-parent-data`

GitLab: klondata för sammanslagningsbegäranden

- Standard: `true`
- Kräver ett värde

### `--pull-requests-clone-parent-data`

Klona den överordnade miljöns data för pull-begäranden

- Standard: `true`
- Kräver ett värde

### `--resync-pull-requests`

Synkronisera miljödata för pull-begäran på nytt vid varje bygge

- Standard: `false`
- Kräver ett värde

### `--fetch-branches`

Hämta alla grenar från fjärrkontrollen (som inaktiva miljöer)

- Standard: `true`
- Kräver ett värde

### `--prune-branches`

Ta bort grenar som inte finns på fjärrkontrollen

- Standard: `true`
- Kräver ett värde

### `--resources-init`

De resurser som ska användas när en ny tjänst initieras (&#39;minimum&#39;, &#39;default&#39;, &#39;manual&#39;, &#39;parent&#39;)

- Kräver ett värde

### `--url`

Integreringens URL- eller API-slutpunkt

- Kräver ett värde

### `--shared-key`

Webkrok: den delade hemliga nyckeln för JWS

- Kräver ett värde

### `--file`

Namnet på en lokal fil som innehåller skriptet som ska överföras

- Kräver ett värde

### `--events`

En lista över händelser som ska hanteras, t.ex. environment.push

- Standard: `*`
- Kräver ett värde

### `--states`

En lista över lägen att agera på, t.ex. väntande, in_progress, slutfört

- Standard: `complete`
- Kräver ett värde

### `--environments`

De miljö-ID som ska inkluderas

- Standard: `*`
- Kräver ett värde

### `--excluded-environments`

De miljö-ID:n som ska uteslutas

- Standard: `[]`
- Kräver ett värde

### `--from-address`

[Valfritt] Anpassad avsändaradress för varningsmeddelanden

- Kräver ett värde

### `--recipients`

Mottagarens e-postadress(er)

- Standard: `[]`
- Kräver ett värde

### `--channel`

Kanalen Slack

- Kräver ett värde

### `--routing-key`

PagerDuty-routningsnyckeln

- Kräver ett värde

### `--category`

Kategorin Sumo Logic, som används för filtrering

- Kräver ett värde

### `--index`

Splunk-index

- Kräver ett värde

### `--sourcetype`

Källtypen för Splunk-händelsen

- Kräver ett värde

### `--protocol`

Syslog-transportprotokoll (&#39;tcp&#39;, &#39;udp&#39;, &#39;tls&#39;)

- Standard: `tls`
- Kräver ett värde

### `--syslog-host`

Syslog relay/collector host

- Kräver ett värde

### `--syslog-port`

Syslog-relä/insamlarport

- Kräver ett värde

### `--facility`

Syslog-funktion

- Standard: `1`
- Kräver ett värde

### `--message-format`

Syslog-meddelandeformat (&#39;rfc3164&#39; eller &#39;rfc5424&#39;)

- Standard: `rfc5424`
- Kräver ett värde

### `--auth-mode`

Autentiseringsläge (prefix eller Structure_data)

- Standard: `prefix`
- Kräver ett värde

### `--auth-token`

Autentiseringstoken

- Kräver ett värde

### `--verify-tls`

Om HTTPS-certifikatverifiering ska vara aktiverat (rekommenderas)

- Standard: `true`
- Kräver ett värde

### `--header`

HTTP-huvud(n) som ska användas vid POST-begäranden. Avgränsa namn och värden med kolon (:).

- Standard: `[]`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `integration:validate`

Validera en befintlig integrering

```bash
magento-cloud integration:validate [-p|--project PROJECT] [--] [<id>]
```


### `id`

Ett integrerings-ID. Lämna tomt om du vill välja från en lista.


### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `local:build`

Bygg det aktuella projektet lokalt

```bash
magento-cloud build [-a|--abslinks] [-s|--source SOURCE] [-d|--destination DESTINATION] [-c|--copy] [--clone] [--run-deploy-hooks] [--no-clean] [--no-archive] [--no-backup] [--no-cache] [--no-build-hooks] [--no-deps] [--working-copy] [--concurrency CONCURRENCY] [--lock] [--] [<app>]...
```


### `app`

Ange vilka program som ska byggas

- Standard: `[]`

- Array

### `--abslinks`, `-a`

Använd absoluta länkar

- Standard: `false`
- Accepterar inte ett värde

### `--source`, `-s`

Källkatalogen. Standardvärdet är projektets aktuella rot.

- Kräver ett värde

### `--destination`, `-d`

Det mål som webbroten för varje program ska länkas till. Standard: _www

- Kräver ett värde

### `--copy`, `-c`

Kopiera till en byggkatalog i stället för att länka från källan

- Standard: `false`
- Accepterar inte ett värde

### `--clone`

Använd Git för att klona HEAD till byggkatalogen

- Standard: `false`
- Accepterar inte ett värde

### `--run-deploy-hooks`

Kör hookar för driftsättning och/eller post_deploy

- Standard: `false`
- Accepterar inte ett värde

### `--no-clean`

Ta inte bort gamla byggen

- Standard: `false`
- Accepterar inte ett värde

### `--no-archive`

Skapa eller använd inte ett byggarkiv

- Standard: `false`
- Accepterar inte ett värde

### `--no-backup`

Säkerhetskopiera inte föregående version

- Standard: `false`
- Accepterar inte ett värde

### `--no-cache`

Inaktivera cachelagring

- Standard: `false`
- Accepterar inte ett värde

### `--no-build-hooks`

Kör inte kopplingar efter bygget

- Standard: `false`
- Accepterar inte ett värde

### `--no-deps`

Installera inte byggberoenden lokalt

- Standard: `false`
- Accepterar inte ett värde

### `--working-copy`

Dra: använd git för att klona en databas för varje Drupal-modul i stället för att bara hämta en version

- Standard: `false`
- Accepterar inte ett värde

### `--concurrency`

Dra: ange antalet samtidiga projekt som ska bearbetas samtidigt

- Standard: `4`
- Kräver ett värde

### `--lock`

Dra: skapa eller uppdatera en låsfil (endast tillgänglig med Drush version 7+)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `local:dir`

Hitta den lokala projektroten

```bash
magento-cloud dir [<subdir>]
```


### `subdir`

Den underkatalog som ska hittas (&#39;local&#39;, &#39;web&#39; eller &#39;shared&#39;)


### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `metrics:all`

Visa mått för processor, disk och minne för en miljö

```bash
magento-cloud metrics [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Visa storlekar i byte

- Standard: `false`
- Accepterar inte ett värde

### `--range`, `-r`

Tidsintervall. Mätvärden läses in för den här varaktigheten till sluttiden (—to). Du kan ange enheter: timmar (h), minuter (m) eller sekunder (s). Minimum \&lt;comment>5 m\&lt;/comment>, max \&lt;comment>8h\&lt;/comment> eller mer (beroende på projektet), standard \&lt;comment>10 m\&lt;/comment>.

- Kräver ett värde

### `--interval`, `-i`

Tidsintervallet. Standardvärdet är en division av intervallet. Du kan ange enheter: timmar (h), minuter (m) eller sekunder (s). Minimum \&lt;comment>1 m\&lt;/comment>.

- Kräver ett värde

### `--to`

Sluttiden. Standardvärdet är nu.

- Kräver ett värde

### `--latest`, `-1`

Visa endast den senaste enskilda datapunkten

- Standard: `false`
- Accepterar inte ett värde

### `--service`, `-s`

Filtrera efter tjänst- eller programnamn Tecknen % eller * kan användas som jokertecken.

- Standard: `[]`
- Kräver ett värde

### `--type`

Filtrera efter tjänsttyp (if —service tillhandahålls inte). Versionen är inte obligatorisk. Tecknen % och * kan användas som jokertecken.

- Standard: `[]`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: tidsstämpel*, tjänst*, cpu_percent*, mem_percent*, disc_percent*, tmp_disk_percent*, cpu_limit, cpu_used, disc_limit, disc_used, inodes_limit, inodes_percent, inodes_used, mem_limit, mem_used, tmp_disk_limit, tmp_disk_used, tmmmmmmtmp_used p_inodes_limit, tmp_inodes_percent, tmp_inodes_used, type (* = standardkolumner). Tecknet&quot;+&quot; kan användas som platshållare för standardkolumnerna. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `metrics:cpu`

Visa processoranvändning i en miljö

```bash
magento-cloud cpu [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--range`, `-r`

Tidsintervall. Mätvärden läses in för den här varaktigheten till sluttiden (—to). Du kan ange enheter: timmar (h), minuter (m) eller sekunder (s). Minimum \&lt;comment>5 m\&lt;/comment>, max \&lt;comment>8h\&lt;/comment> eller mer (beroende på projektet), standard \&lt;comment>10 m\&lt;/comment>.

- Kräver ett värde

### `--interval`, `-i`

Tidsintervallet. Standardvärdet är en division av intervallet. Du kan ange enheter: timmar (h), minuter (m) eller sekunder (s). Minimum \&lt;comment>1 m\&lt;/comment>.

- Kräver ett värde

### `--to`

Sluttiden. Standardvärdet är nu.

- Kräver ett värde

### `--latest`, `-1`

Visa endast den senaste enskilda datapunkten

- Standard: `false`
- Accepterar inte ett värde

### `--service`, `-s`

Filtrera efter tjänst- eller programnamn Tecknen % eller * kan användas som jokertecken.

- Standard: `[]`
- Kräver ett värde

### `--type`

Filtrera efter tjänsttyp (if —service tillhandahålls inte). Versionen är inte obligatorisk. Tecknen % och * kan användas som jokertecken.

- Standard: `[]`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: tidsstämpel*, tjänst*, använd*, gräns*, procent*, typ (* = standardkolumner). Tecknet&quot;+&quot; kan användas som platshållare för standardkolumnerna. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `metrics:disk-usage`

Visa diskanvändning i en miljö

```bash
magento-cloud disk [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [--tmp] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Visa storlekar i byte

- Standard: `false`
- Accepterar inte ett värde

### `--range`, `-r`

Tidsintervall. Mätvärden läses in för den här varaktigheten till sluttiden (—to). Du kan ange enheter: timmar (h), minuter (m) eller sekunder (s). Minimum \&lt;comment>5 m\&lt;/comment>, max \&lt;comment>8h\&lt;/comment> eller mer (beroende på projektet), standard \&lt;comment>10 m\&lt;/comment>.

- Kräver ett värde

### `--interval`, `-i`

Tidsintervallet. Standardvärdet är en division av intervallet. Du kan ange enheter: timmar (h), minuter (m) eller sekunder (s). Minimum \&lt;comment>1 m\&lt;/comment>.

- Kräver ett värde

### `--to`

Sluttiden. Standardvärdet är nu.

- Kräver ett värde

### `--latest`, `-1`

Visa endast den senaste enskilda datapunkten

- Standard: `false`
- Accepterar inte ett värde

### `--service`, `-s`

Filtrera efter tjänst- eller programnamn Tecknen % eller * kan användas som jokertecken.

- Standard: `[]`
- Kräver ett värde

### `--type`

Filtrera efter tjänsttyp (if —service tillhandahålls inte). Versionen är inte obligatorisk. Tecknen % och * kan användas som jokertecken.

- Standard: `[]`
- Kräver ett värde

### `--tmp`

Rapportera tillfällig diskanvändning (visar kolumner: tidsstämpel, tjänst, tmp_used, tmp_limit, tmp_percent, tmp_ipercent)

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: tidsstämpel*, tjänst*, använd*, gräns*, procent*, ipercent*, tmp_percent*, ilimit, iused, tmp_ilimit, tmp_ipercent, tmp_iused, tmp_limit, tmp_used, type (* = standardkolumner). Tecknet&quot;+&quot; kan användas som platshållare för standardkolumnerna. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `metrics:memory`

Visa minnesanvändning i en miljö

```bash
magento-cloud mem [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--bytes`, `-B`

Visa storlekar i byte

- Standard: `false`
- Accepterar inte ett värde

### `--range`, `-r`

Tidsintervall. Mätvärden läses in för den här varaktigheten till sluttiden (—to). Du kan ange enheter: timmar (h), minuter (m) eller sekunder (s). Minimum \&lt;comment>5 m\&lt;/comment>, max \&lt;comment>8h\&lt;/comment> eller mer (beroende på projektet), standard \&lt;comment>10 m\&lt;/comment>.

- Kräver ett värde

### `--interval`, `-i`

Tidsintervallet. Standardvärdet är en division av intervallet. Du kan ange enheter: timmar (h), minuter (m) eller sekunder (s). Minimum \&lt;comment>1 m\&lt;/comment>.

- Kräver ett värde

### `--to`

Sluttiden. Standardvärdet är nu.

- Kräver ett värde

### `--latest`, `-1`

Visa endast den senaste enskilda datapunkten

- Standard: `false`
- Accepterar inte ett värde

### `--service`, `-s`

Filtrera efter tjänst- eller programnamn Tecknen % eller * kan användas som jokertecken.

- Standard: `[]`
- Kräver ett värde

### `--type`

Filtrera efter tjänsttyp (if —service tillhandahålls inte). Versionen är inte obligatorisk. Tecknen % och * kan användas som jokertecken.

- Standard: `[]`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: tidsstämpel*, tjänst*, använd*, gräns*, procent*, typ (* = standardkolumner). Tecknet&quot;+&quot; kan användas som platshållare för standardkolumnerna. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `mount:download`

Hämta filer från en montering med hjälp av synkronisering

```bash
magento-cloud mount:download [-a|--all] [-m|--mount MOUNT] [--target TARGET] [--source-path] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--all`, `-a`

Hämta från alla monteringar

- Standard: `false`
- Accepterar inte ett värde

### `--mount`, `-m`

Monteringen (som en apprelativ sökväg)

- Kräver ett värde

### `--target`

Katalogen som filerna ska hämtas till. Om —all används läggs monteringssökvägen till

- Kräver ett värde

### `--source-path`

Använd monteringens källsökväg (i stället för monteringssökvägen) som en underkatalog till målet, när —all används

- Standard: `false`
- Accepterar inte ett värde

### `--delete`

Om överflödiga filer ska tas bort i målkatalogen

- Standard: `false`
- Accepterar inte ett värde

### `--exclude`

Fil(er) som ska uteslutas från nedladdningen (mönster)

- Standard: `[]`
- Kräver ett värde

### `--include`

Fil(er) som inte ska uteslutas (mönster)

- Standard: `[]`
- Kräver ett värde

### `--refresh`

Om cachen ska uppdateras

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--worker`

Ett arbetarnamn

- Kräver ett värde

### `--instance`, `-I`

Ett instans-ID

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `mount:list`

Få en lista över monteringar

```bash
magento-cloud mounts [--paths] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

### `--paths`

Utdata endast för monteringsbanor (en per rad)

- Standard: `false`
- Accepterar inte ett värde

### `--refresh`

Om cachen ska uppdateras

- Standard: `false`
- Accepterar inte ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: definition, sökväg. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--worker`

Ett arbetarnamn

- Kräver ett värde

### `--instance`, `-I`

Ett instans-ID

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `mount:size`

Kontrollera diskanvändning av monteringar

```bash
magento-cloud mount:size [-B|--bytes] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

### `--bytes`, `-B`

Visa storlekar i byte

- Standard: `false`
- Accepterar inte ett värde

### `--refresh`

Uppdatera cachen

- Standard: `false`
- Accepterar inte ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: available, max, monts, percent_used, sizes, used. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--worker`

Ett arbetarnamn

- Kräver ett värde

### `--instance`, `-I`

Ett instans-ID

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `mount:upload`

Överför filer till en plats med hjälp av synkronisering

```bash
magento-cloud mount:upload [--source SOURCE] [-m|--mount MOUNT] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [-i|--identity-file IDENTITY-FILE]
```

### `--source`

En katalog som innehåller filer som ska överföras

- Kräver ett värde

### `--mount`, `-m`

Monteringen (som en apprelativ sökväg)

- Kräver ett värde

### `--delete`

Om överflödiga filer ska tas bort i monteringen

- Standard: `false`
- Accepterar inte ett värde

### `--exclude`

Fil(er) som ska uteslutas från överföringen (mönster)

- Standard: `[]`
- Kräver ett värde

### `--include`

Fil(er) som inte ska uteslutas (mönster)

- Standard: `[]`
- Kräver ett värde

### `--refresh`

Om cachen ska uppdateras

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--worker`

Ett arbetarnamn

- Kräver ett värde

### `--instance`, `-I`

Ett instans-ID

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `operation:list`

Visa körningsåtgärder i en miljö

```bash
magento-cloud ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--full`

Begränsa inte längden på det kommando som ska visas. Standardgränsen är 24 rader.

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--worker`

Ett arbetarnamn

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: service*, name*, start*, role, stop (* = standardkolumner). Tecknet&quot;+&quot; kan användas som platshållare för standardkolumnerna. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `operation:run`

Köra en åtgärd i miljön

```bash
magento-cloud operation:run [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-W|--no-wait] [--wait] [--] [<operation>]
```


### `operation`

Åtgärdsnamnet


### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--worker`

Ett arbetarnamn

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `project:clear-build-cache`

Rensa ett projekts byggcache

```bash
magento-cloud project:clear-build-cache [-p|--project PROJECT]
```

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `project:get`

Klona ett projekt lokalt

```bash
magento-cloud get [-e|--environment ENVIRONMENT] [--depth DEPTH] [--build] [-p|--project PROJECT] [-i|--identity-file IDENTITY-FILE] [--] [<project>] [<directory>]
```


### `project`

Projekt-ID


### `directory`

Katalogen som ska klonas. Standardvärdet är projekttiteln


### `--environment`, `-e`

Det miljö-ID som ska klonas. Standardvärdet är projektets standardinställning eller den första tillgängliga miljön

- Kräver ett värde

### `--depth`

Skapa en grund klon: begränsa antalet implementeringar i historiken

- Kräver ett värde

### `--build`

Bygg projektet efter kloning

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `project:info`

Läsa eller ange egenskaper för ett projekt

```bash
magento-cloud project:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```


### `property`

Egenskapens namn


### `value`

Ange ett nytt värde för egenskapen


### `--refresh`

Om cachen ska uppdateras

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `project:list`

Hämta en lista över alla aktiva projekt

```bash
magento-cloud projects [--pipe] [--region REGION] [--title TITLE] [--my] [--refresh REFRESH] [--sort SORT] [--reverse] [--page PAGE] [-c|--count COUNT] [--format FORMAT] [--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

### `--pipe`

Skriv ut en enkel lista med projekt-ID:n. Inaktiverar sidnumrering.

- Standard: `false`
- Accepterar inte ett värde

### `--region`

Filtrera efter region (exakt matchning)

- Kräver ett värde

### `--title`

Filtrera efter titel (skiftlägesokänslig sökning)

- Kräver ett värde

### `--my`

Visa endast de projekt du äger

- Standard: `false`
- Accepterar inte ett värde

### `--refresh`

Om listan ska uppdateras

- Standard: `1`
- Kräver ett värde

### `--sort`

En egenskap som ska sorteras efter

- Standard: `title`
- Kräver ett värde

### `--reverse`

Sortera i omvänd ordning (fallande)

- Standard: `false`
- Accepterar inte ett värde

### `--page`

Sidnummer. Detta aktiverar sidnumrering, trots konfiguration eller —count. Ignoreras om —pipe har angetts.

- Kräver ett värde

### `--count`, `-c`

Antalet projekt som ska visas per sida. Använd 0 för att inaktivera sidnumrering. Ignoreras om —page har angetts.

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`

Kolumner att visa. Tillgängliga kolumner: id*, title*, region*, created_at, organization_id, organization_label, organization_name, status (* = standardkolumner). Tecknet&quot;+&quot; kan användas som platshållare för standardkolumnerna. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `project:set-remote`

Ange fjärrprojektet för den aktuella Git-databasen

```bash
magento-cloud set-remote [<project>]
```


### `project`

Projekt-ID


### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `repo:cat`

Läsa en fil i projektdatabasen

```bash
magento-cloud repo:cat [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] <path>
```


### `path`

Sökvägen till filen

- Obligatoriskt

### `--commit`, `-c`

Verkställ SHA. Detta kan även acceptera suffixen &quot;HEAD&quot; och cirkumflex (^) eller tilde (~) för överordnade implementeringar.

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `repo:ls`

Visa filer i projektdatabasen

```bash
magento-cloud repo:ls [-d|--directories] [-f|--files] [--git-style] [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```


### `path`

Sökvägen till en underkatalog


### `--directories`, `-d`

Visa endast kataloger

- Standard: `false`
- Accepterar inte ett värde

### `--files`, `-f`

Visa endast filer

- Standard: `false`
- Accepterar inte ett värde

### `--git-style`

Formatutdata som liknar &quot;git ls-tree&quot;

- Standard: `false`
- Accepterar inte ett värde

### `--commit`, `-c`

Verkställ SHA. Detta kan även acceptera suffixen &quot;HEAD&quot; och cirkumflex (^) eller tilde (~) för överordnade implementeringar.

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `repo:read`

Läsa en katalog eller fil i projektdatabasen

```bash
magento-cloud read [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```


### `path`

Sökvägen till katalogen eller filen


### `--commit`, `-c`

Verkställ SHA. Detta kan även acceptera suffixen &quot;HEAD&quot; och cirkumflex (^) eller tilde (~) för överordnade implementeringar.

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `route:get`

Visa detaljerad information om ett flöde

```bash
magento-cloud route:get [--id ID] [-1|--primary] [-P|--property PROPERTY] [--refresh] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<route>]
```


### `route`

Vägets ursprungliga URL


### `--id`

Ett rutt-ID att välja

- Kräver ett värde

### `--primary`, `-1`

Välj primärt flöde

- Standard: `false`
- Accepterar inte ett värde

### `--property`, `-P`

Egenskapen som ska visas

- Kräver ett värde

### `--refresh`

Kringgå cacheminnet för vägar

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

[Inaktuellt alternativ, används inte längre]

- Kräver ett värde

### `--identity-file`, `-i`

[Inaktuellt alternativ, används inte längre]

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `route:list`

Visa alla vägar för en miljö

```bash
magento-cloud routes [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<environment>]
```


### `environment`

Miljö-ID


### `--refresh`

Kringgå cacheminnet för vägar

- Standard: `false`
- Accepterar inte ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: flöde*, typ*, till*, url (* = standardkolumner). Tecknet&quot;+&quot; kan användas som platshållare för standardkolumnerna. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `self:install`

Installera eller uppdatera CLI-konfigurationsfiler

```bash
magento-cloud self:install [--shell-type SHELL-TYPE]
```

### `--shell-type`

Gränssnittstypen för automatisk komplettering (bash eller zsh)

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `self:update`

Uppdatera CLI till den senaste versionen

```bash
magento-cloud update [--no-major] [--unstable] [--manifest MANIFEST] [--current-version CURRENT-VERSION] [--timeout TIMEOUT]
```

### `--no-major`

Uppdatera endast mellan mindre versioner eller korrigeringsversioner

- Standard: `false`
- Accepterar inte ett värde

### `--unstable`

Uppdatera till en ny instabil version, om en sådan finns

- Standard: `false`
- Accepterar inte ett värde

### `--manifest`

Åsidosätt manifestfilens plats

- Kräver ett värde

### `--current-version`

Åsidosätt den aktuella versionen

- Kräver ett värde

### `--timeout`

En timeout för versionskontrollen

- Standard: `30`
- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `service:list`

Visa tjänster i projektet

```bash
magento-cloud services [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Om cachen ska uppdateras

- Standard: `false`
- Accepterar inte ett värde

### `--pipe`

Skriv endast ut en lista med tjänstnamn

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: disk, namn, storlek, typ. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `service:mongo:dump`

Skapa en binär arkivdump av data från MongoDB

```bash
magento-cloud mongodump [-c|--collection COLLECTION] [-z|--gzip] [-o|--stdout] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

Samlingen som ska dumpas

- Kräver ett värde

### `--gzip`, `-z`

Komprimera dumpen med gzip

- Standard: `false`
- Accepterar inte ett värde

### `--stdout`, `-o`

Utdata till STDOUT i stället för en fil

- Standard: `false`
- Accepterar inte ett värde

### `--relationship`, `-r`

Den tjänstrelation som ska användas

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `service:mongo:export`

Exportera data från MongoDB

```bash
magento-cloud mongoexport [-c|--collection COLLECTION] [--jsonArray] [--type TYPE] [-f|--fields FIELDS] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

Samlingen som ska exporteras

- Kräver ett värde

### `--jsonArray`

Exportera data som en enda JSON-array

- Standard: `false`
- Accepterar inte ett värde

### `--type`

Exporttyp, t.ex. &quot;csv&quot;

- Kräver ett värde

### `--fields`, `-f`

De fält som ska exporteras

- Standard: `[]`
- Kräver ett värde

### `--relationship`, `-r`

Den tjänstrelation som ska användas

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `service:mongo:restore`

Återställa en binär arkivdump av data till MongoDB

```bash
magento-cloud mongorestore [-c|--collection COLLECTION] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--collection`, `-c`

Samlingen som ska återställas

- Kräver ett värde

### `--relationship`, `-r`

Den tjänstrelation som ska användas

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `service:mongo:shell`

Använd MongoDB-skalet

```bash
magento-cloud mongo [--eval EVAL] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--eval`

Skicka ett JavaScript-fragment till skalet

- Kräver ett värde

### `--relationship`, `-r`

Den tjänstrelation som ska användas

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `service:redis-cli`

Åtkomst till Redis CLI

```bash
magento-cloud redis [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--] [<args>]
```


### `args`

Argument som ska läggas till i Redis-kommandot


### `--relationship`, `-r`

Den tjänstrelation som ska användas

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `snapshot:create`

Ta en ögonblicksbild av en miljö

```bash
magento-cloud backup [--live] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```


### `environment`

Miljön


### `--live`

Live-säkerhetskopiering: stoppa inte miljön. Om detta anges kommer miljön att vara igång och öppen för anslutningar under säkerhetskopieringen. Detta minskar driftstoppen och riskerar att data säkerhetskopieras i ett inkonsekvent tillstånd.

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `snapshot:delete`

Ta bort en ögonblicksbild av miljön

```bash
magento-cloud snapshot:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>]
```


### `id`

ID för ögonblicksbilden. Krävs i icke-interaktivt läge.


### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `snapshot:get`

Visa en ögonblicksbild av en miljö

```bash
magento-cloud snapshot:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<id>]
```


### `id`

ID för ögonblicksbilden. Standardvärdet är den senaste.


### `--property`, `-P`

Egenskapen som ska visas.

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `snapshot:list`

Visa tillgängliga ögonblicksbilder av en miljö

```bash
magento-cloud snapshots [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `snapshot:restore`

Återställ en ögonblicksbild av miljön

```bash
magento-cloud snapshot:restore [--target TARGET] [--branch-from BRANCH-FROM] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<snapshot>]
```


### `snapshot`

Namnet på ögonblicksbilden. Standardvärdet är den senaste


### `--target`

Den miljö som ska återställas till. Standardvärdet är ögonblicksbildens aktuella miljö

- Kräver ett värde

### `--branch-from`

Om —target inte finns än, anger detta den överordnade för den nya miljön

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `source-operation:list`

Visa källåtgärder i en miljö

```bash
magento-cloud source-ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--full`

Begränsa inte längden på det kommando som ska visas. Standardgränsen är 24 rader.

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: app, command, operation. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `source-operation:run`

Köra en källåtgärd

```bash
magento-cloud source-operation:run [--variable VARIABLE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<operation>]
```


### `operation`

Åtgärdsnamnet


### `--variable`

En variabel som ska anges under operationen i formatet \&lt;info>type:name=value\&lt;/info>

- Standard: `[]`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `ssh-cert:load`

Generera ett SSH-certifikat

```bash
magento-cloud ssh-cert:load [--refresh-only] [--new] [--new-key]
```

### `--refresh-only`

Uppdatera bara certifikatet om det behövs (skriv inte SSH-konfigurationen)

- Standard: `false`
- Accepterar inte ett värde

### `--new`

Tvinga certifikatet att uppdateras

- Standard: `false`
- Accepterar inte ett värde

### `--new-key`

[Föråldrat] Använd —new i stället

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `ssh-key:add`

Lägg till en ny SSH-nyckel

```bash
magento-cloud ssh-key:add [--name NAME] [--] [<path>]
```


### `path`

Sökvägen till en befintlig offentlig SSH-nyckel


### `--name`

Ett namn som identifierar nyckeln

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `ssh-key:delete`

Ta bort en SSH-nyckel

```bash
magento-cloud ssh-key:delete [<id>]
```


### `id`

ID:t för SSH-nyckeln som ska tas bort


### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `ssh-key:list`

Hämta en lista med SSH-nycklar i ditt konto

```bash
magento-cloud ssh-keys [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: id*, title*, path*, fingeravtryck (* = standardkolumner). Tecknet&quot;+&quot; kan användas som platshållare för standardkolumnerna. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `subscription:info`

Läs eller ändra prenumerationsegenskaper

```bash
magento-cloud subscription:info [-s|--id ID] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<property>] [<value>]
```


### `property`

Egenskapens namn


### `value`

Ange ett nytt värde för egenskapen


### `--id`, `-s`

Prenumerations-ID

- Kräver ett värde

### `--date-fmt`

Datumformatet (som en PHP-datumformatsträng)

- Standard: `c`
- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `tunnel:close`

Stäng SSH-tunnlar

```bash
magento-cloud tunnel:close [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--all`, `-a`

Stäng alla tunnlar

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `tunnel:info`

Visa relationsinformation för SSH-tunnlar

```bash
magento-cloud tunnel:info [-P|--property PROPERTY] [-c|--encode] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

### `--property`, `-P`

Den relationsegenskap som ska visas

- Kräver ett värde

### `--encode`, `-c`

Utdata som base64-kodad JSON

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `tunnel:list`

Lista SSH-tunnlar

```bash
magento-cloud tunnels [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--all`, `-a`

Visa alla tunnlar

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: port*, projekt*, miljö*, app*, relation*, url (* = standardkolumner). Tecknet&quot;+&quot; kan användas som platshållare för standardkolumnerna. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `tunnel:open`

Öppna SSH-tunnlar i en apps relationer

```bash
magento-cloud tunnel:open [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

### `--gateway-ports`, `-g`

Tillåt att fjärrvärdar ansluter till lokala vidarebefordrade portar

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `tunnel:single`

Öppna en SSH-tunnel till en apprelation

```bash
magento-cloud tunnel:single [--port PORT] [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [-i|--identity-file IDENTITY-FILE]
```

### `--port`

Den lokala porten

- Kräver ett värde

### `--gateway-ports`, `-g`

Tillåt att fjärrvärdar ansluter till lokala vidarebefordrade portar

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--app`, `-A`

Namnet på fjärrprogrammet

- Kräver ett värde

### `--relationship`, `-r`

Den tjänstrelation som ska användas

- Kräver ett värde

### `--identity-file`, `-i`

En SSH-identitet (privat nyckel) som ska användas

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `user:add`

Lägg till en användare i projektet

```bash
magento-cloud user:add [-r|--role ROLE] [--force-invite] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```


### `email`

Användarens e-postadress


### `--role`, `-r`

Användarens projektroll (admin eller viewer) eller miljötypsroll (t.ex. &#39;staging:contributor&#39; eller &#39;production:viewer&#39;). Om du vill ta bort en användare från en miljötyp anger du rollen som none. Tecknen % och * kan användas som jokertecken för miljötypen, t.ex. %:viewer, för att ge användaren rollen &#39;viewer&#39; för alla typer. Rollen kan förkortas, t.ex. &#39;production:v&#39;.

- Standard: `[]`
- Kräver ett värde

### `--force-invite`

Skicka en inbjudan, även om en inbjudan redan har skickats

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `user:delete`

Ta bort en användare från projektet

```bash
magento-cloud user:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <email>
```


### `email`

Användarens e-postadress

- Obligatoriskt

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `user:get`

Visa en användares roll

```bash
magento-cloud user:get [-l|--level LEVEL] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [-r|--role ROLE] [--] [<email>]
```


### `email`

Användarens e-postadress


### `--level`, `-l`

Rollnivån (&#39;project&#39; eller &#39;environment&#39;)

- Kräver ett värde

### `--pipe`

Utdata för rollen till stdout (efter att du har gjort några ändringar)

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--role`, `-r`

[Inaktuell: använd användare:uppdatera för att ändra en användares roll(er)]

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `user:list`

Visa projektanvändare

```bash
magento-cloud users [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: e-post*, namn*, roll*, id*, beviljad_at, uppdaterad_at (* = standardkolumner). Tecknet&quot;+&quot; kan användas som platshållare för standardkolumnerna. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `user:update`

Uppdatera användarroller i ett projekt

```bash
magento-cloud user:update [-r|--role ROLE] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```


### `email`

Användarens e-postadress


### `--role`, `-r`

Användarens projektroll (admin eller viewer) eller miljötypsroll (t.ex. &#39;staging:contributor&#39; eller &#39;production:viewer&#39;). Om du vill ta bort en användare från en miljötyp anger du rollen som none. Tecknen % och * kan användas som jokertecken för miljötypen, t.ex. %:viewer, för att ge användaren rollen &#39;viewer&#39; för alla typer. Rollen kan förkortas, t.ex. &#39;production:v&#39;.

- Standard: `[]`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `variable:create`

Skapa en variabel

```bash
magento-cloud variable:create [-u|--update] [-l|--level LEVEL] [--name NAME] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--prefix PREFIX] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<name>]
```


### `name`

Variabelnamnet


### `--update`, `-u`

Uppdatera variabeln om den redan finns

- Standard: `false`
- Accepterar inte ett värde

### `--level`, `-l`

Den nivå som variabeln (&#39;project&#39; eller &#39;environment&#39;) ska anges på

- Kräver ett värde

### `--name`

Variabelnamnet

- Kräver ett värde

### `--value`

Variabelns värde

- Kräver ett värde

### `--json`

Om variabelvärdet är JSON-formaterat

- Standard: `false`
- Kräver ett värde

### `--sensitive`

Om variabelvärdet är känsligt

- Standard: `false`
- Kräver ett värde

### `--prefix`

Variabelnamnets prefix som kan avgöra dess typ, t.ex. &#39;env&#39;. Gäller endast om namnet inte redan innehåller ett prefix. (t.ex. &#39;none&#39; eller &#39;env:&#39;)

- Standard: `none`
- Kräver ett värde

### `--enabled`

Om variabeln ska aktiveras i miljön

- Standard: `true`
- Kräver ett värde

### `--inheritable`

Om variabeln kan ärvas av underordnade miljöer

- Standard: `true`
- Kräver ett värde

### `--visible-build`

Om variabeln ska vara synlig vid byggtillfället

- Kräver ett värde

### `--visible-runtime`

Om variabeln ska vara synlig vid körning

- Standard: `true`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `variable:delete`

Ta bort en variabel

```bash
magento-cloud variable:delete [-l|--level LEVEL] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Variabelnamnet

- Obligatoriskt

### `--level`, `-l`

Variabelnivån (&#39;project&#39;, &#39;environment&#39;, &#39;p&#39; eller &#39;e&#39;)

- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `variable:get`

Visa en variabel

```bash
magento-cloud vget [-P|--property PROPERTY] [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--pipe] [--] [<name>]
```


### `name`

Variabelns namn


### `--property`, `-P`

Visa en enskild variabelegenskap

- Kräver ett värde

### `--level`, `-l`

Variabelnivån (&#39;project&#39;, &#39;environment&#39;, &#39;p&#39; eller &#39;e&#39;)

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--pipe`

[Inaktuellt alternativ] Utdata endast för variabelvärdet

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `variable:list`

Listvariabler

```bash
magento-cloud variables [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

### `--level`, `-l`

Variabelnivån (&#39;project&#39;, &#39;environment&#39;, &#39;p&#39; eller &#39;e&#39;)

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: is_enabled, level, name, value. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `variable:update`

Uppdatera en variabel

```bash
magento-cloud variable:update [--allow-no-change] [-l|--level LEVEL] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```


### `name`

Variabelnamnet

- Obligatoriskt

### `--allow-no-change`

Returnera lyckade (noll avslutningskod) om inga ändringar har angetts

- Standard: `false`
- Accepterar inte ett värde

### `--level`, `-l`

Variabelnivån (&#39;project&#39;, &#39;environment&#39;, &#39;p&#39; eller &#39;e&#39;)

- Kräver ett värde

### `--value`

Variabelns värde

- Kräver ett värde

### `--json`

Om variabelvärdet är JSON-formaterat

- Standard: `false`
- Kräver ett värde

### `--sensitive`

Om variabelvärdet är känsligt

- Standard: `false`
- Kräver ett värde

### `--enabled`

Om variabeln ska aktiveras i miljön

- Standard: `true`
- Kräver ett värde

### `--inheritable`

Om variabeln kan ärvas av underordnade miljöer

- Standard: `true`
- Kräver ett värde

### `--visible-build`

Om variabeln ska vara synlig vid byggtillfället

- Kräver ett värde

### `--visible-runtime`

Om variabeln ska vara synlig vid körning

- Standard: `true`
- Kräver ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--no-wait`, `-W`

Vänta inte tills åtgärden har slutförts

- Standard: `false`
- Accepterar inte ett värde

### `--wait`

Vänta tills åtgärden har slutförts (standard)

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde


## `worker:list`

Hämta en lista över alla distribuerade arbetare

```bash
magento-cloud workers [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

### `--refresh`

Om cachen ska uppdateras

- Standard: `false`
- Accepterar inte ett värde

### `--pipe`

Skriv endast ut en lista med arbetarnamn

- Standard: `false`
- Accepterar inte ett värde

### `--project`, `-p`

Projekt-ID eller URL

- Kräver ett värde

### `--environment`, `-e`

Händelse-ID. Använd &quot;.&quot; för att välja projektets standardmiljö.

- Kräver ett värde

### `--format`

Utdataformatet: table, csv, tsv eller plain

- Standard: `table`
- Kräver ett värde

### `--columns`, `-c`

Kolumner att visa. Tillgängliga kolumner: kommandon, namn, typ. Tecknen % och * kan användas som jokertecken. Värdena kan delas med kommatecken (t.ex. &quot;a,b,c&quot;) och/eller blanksteg.

- Standard: `[]`
- Kräver ett värde

### `--no-header`

Skriv inte ut tabellrubriken

- Standard: `false`
- Accepterar inte ett värde

### `--help`, `-h`

Visa det här hjälpmeddelandet

- Standard: `false`
- Accepterar inte ett värde

### `--verbose`, `-v|-vv|-vvv`

Öka meddelandenas exakthet

- Standard: `false`
- Accepterar inte ett värde

### `--version`, `-V`

Visa den här programversionen

- Standard: `false`
- Accepterar inte ett värde

### `--yes`, `-y`

Svara&quot;ja&quot; på bekräftelsefrågor; acceptera standardvärdet för andra frågor; inaktivera interaktion

- Standard: `false`
- Accepterar inte ett värde

### `--no-interaction`

Ställ inga interaktiva frågor. Acceptera standardvärdena. Motsvarar användning av miljövariabeln: \&lt;comment>MAGENTO_CLOUD_CLI_NO_INTERACTION=1\&lt;/comment>

- Standard: `false`
- Accepterar inte ett värde

