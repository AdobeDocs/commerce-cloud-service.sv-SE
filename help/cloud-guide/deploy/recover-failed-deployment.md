---
title: Återställning efter komponentfel
description: Lär dig hur du kan återställa en komponent som inte kan distribueras korrekt i Adobe Commerce i molninfrastrukturen.
feature: Cloud, Deploy
exl-id: 4855be0c-6883-4ab1-a364-316d10e97250
source-git-commit: b44d97f82ef09288807c648010202422c9ac04eb
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Återställning efter komponentfel

I det här avsnittet beskrivs hur du återställer om en komponent inte kan distribueras på rätt sätt. Typiska exempel är komponenter som har beroenden som inte uppfylls av din fjärrmiljö, till exempel inkompatibla PHP-versioner.

Du kan återställa efter en misslyckad distribution på något av följande sätt:

- [Återställa en säkerhetskopia](../storage/snapshots.md#restore-a-snapshot)
- Rensa projekt och kod från tidigare ändringar och omdistribuera

## Rensa, ta bort och omdistribuera

Om du vill rensa upp från den tidigare distributionen identifierar du komponenten som lades till eller uppdaterades och tar sedan bort den. Logga först in på fjärrmiljön och rensa innehållet i `var` katalog. Ta sedan bort komponenten från `composer.json` och distribuera om miljön.

**Så här rensar du `var` kataloger**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Använd SSH för att logga in i fjärrmiljön.

   ```bash
   magento-cloud ssh
   ```

1. Rensa `var` kataloger.

   ```shell
   rm -rf var/*
   ```

1. Logga ut.

**Ta bort komponenten**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Rensa cachen.

   ```bash
   composer clear-cache
   ```

1. Ta bort komponenten från `composer.json` -fil.

   ```bash
   composer remove <component-name>:<version>
   ```

   Om följande meddelande visas behöver du inte göra något mer:

   ```terminal
   Package "<name>:<version>" listed for update is not installed. Ignoring.
   ```

1. Vänta medan beroendena uppdateras.

1. Lägg till, implementera och push-ändra kod.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "<message>"
   ```

   ```bash
   git push origin <environment-ID>
   ```

{{redeploy-warning}}

Läs mer om återställning av en miljö utan säkerhetskopiering i [Återställa en miljö](../development/restore-environment.md).

{{stuck-deployment-tip}}
