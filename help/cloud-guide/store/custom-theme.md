---
title: Eget tema
description: Lär dig hur du installerar ett anpassat tema med Adobe Commerce i molninfrastrukturen.
feature: Cloud, Themes
exl-id: f08134ab-daea-471d-a927-02531d36a809
source-git-commit: bb7a866b1896a8a43d01ad3f83dc655bcf383374
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Eget tema

Du kan installera ett eller flera teman som du kan använda för en eller alla dina butiker och webbplatser i ditt projekt. Teman innehåller flera statiska filer, bland annat bilder, teckensnitt, CSS, JavaScript, PHP med mera för att skapa butiker. Du kan lägga till temat genom att antingen extrahera dess kod till filsystemet eller använda Composer.

## Installera ett tema manuellt

Om du vill installera ett tema manuellt måste du ha temats kod i ett komprimerat arkiv eller i en katalogstruktur som liknar följande:

```text
<VendorName>
  ├── composer.json
      ├── etc
      │   └── view.xml
      ├── media
      ├── registration.php
      ├── theme.xml
      └── web
          ├── css
          │   └── source
          ├── fonts
          ├── images
          └── js
```

**Installera ett tema manuellt**:

1. Kopiera temats kod under `<Project root dir>/app/design/frontend` för ett butikstema eller `<Project root dir>/app/design/adminhtml` för ett administratörstema. Verifiera att den översta katalogen är `<VendorName>`annars installeras temat inte korrekt.

   ```bash
   cp -r ExampleTheme <project-root>/app/design/frontend
   ```

1. Bekräfta att temat har kopierats till rätt plats.

   * Tema: `ls <project-root>/app/design/frontend`
   * Administratörstema: `ls <project-root>/app/design/adminhtml`

   Ett exempel följer:

   ExampleTheme Adobe Commerce

1. Lägg till och implementera filer.

   ```bash
   git add -A && git commit -m "Add theme"
   ```

1. Skicka filerna till din gren.

   ```bash
   git push origin <branch name>
   ```

1. Vänta tills distributionen är klar.
1. Logga in på Admin.
1. Klicka **Innehåll** > Design > **Teman**.

   Temat visas i den högra rutan.

## Installera ett tema med Composer

Att installera ett tema med Composer är detsamma som att installera andra tillägg med Composer. Se [Installera, hantera och uppgradera moduler](extensions.md) för mer information.

Så här installerar du ett tema med Composer:

1. Köp temat från Commerce Marketplace.
1. Hämta temats disposition.
1. Byt till Adobe Commerce rotkatalog och ange kommandot:

   ```bash
   composer require <vendor>/<name>:<version>
   ```

   Exempel:

   ```bash
   composer require zero1/theme-fashionista-theme:1.0.0
   ```

1. Vänta på att beroenden ska uppdateras.
1. Ange följande kommandon:

   ```bash
   git add -A && git commit -m "Add theme"
   ```

   ```bash
   git push origin <branch name>
   ```

1. Logga in på Admin.
1. Klicka **Innehåll** > Design > **Teman**.

   Temat visas i den högra rutan.

## Flera teman

Om du använder flera teman, t.ex. olika teman per språkinställning, ska du granska `SCD_MATRIX` miljövariabel för anpassning av temadistribution. Se [bygg](../environment/variables-build.md#scd_matrix) eller [driftsätta](../environment/variables-deploy.md#scd_matrix) i [miljökonfiguration](../environment/configure-env-yaml.md).
