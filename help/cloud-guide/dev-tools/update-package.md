---
title: Uppdatera ECE-verktygspaketet
description: Lär dig hur du uppgraderar ECE-verktygspaketet för att dra nytta av de senaste korrigeringarna och funktionerna som används i Adobe Commerce för molninfrastruktur.
feature: Cloud, Upgrade
exl-id: 7cce45eb-ae53-4468-b16d-4f4d3422ac52
source-git-commit: 513bc5b52f046ffd98005d80f34725b7f60b38bd
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# Uppdatera ECE-verktygspaketet

En uppdatering av `ece-tools` uppdaterar även det andra [Cloud Tools Suite for Commerce-paket](../release-notes/cloud-tools-suite.md), som är beroenden för `ece-tools`. Därför måste du använda en version av Adobe Commerce i molninfrastruktur som har stöd för `ece-tools` paket.

{{ece-tools-package}}

**Förutsättningar**:

- Innan du uppdaterar `ece-tools`, granska [Versionsinformation om Cloud Tools Suite för Commerce](../release-notes/cloud-tools-suite.md).
- Om du uppdaterar från `ece-tools` 2002.0.22 eller tidigare till 2002.1.0, recension [Bakåtkompatibla ändringar](../release-notes/backward-incompatible-changes.md) och göra nödvändiga ändringar i ditt Adobe Commerce i molninfrastrukturprojekt.
- Granska [Uppgraderingar och korrigeringar](../development/commerce-version.md#upgrade-from-older-versions) för att fastställa vilka versioner av ECE-verktygen som är kompatibla med din Adobe Commerce för molninfrastrukturprojekt.

{{upgrade-tip}}

**Uppdatera `ece-tools` package**:

1. Utför en uppdatering med Composer på din lokala arbetsstation.

   ```bash
   composer update magento/ece-tools --with-dependencies
   ```

   >[!NOTE]
   >
   >Om du inte kan uppdatera bortom `ece-tools` version 2002.0.8, se [Uppgradera projekt till ECE-verktygspaket](install-package.md).

1. Lägg till, implementera och push-ändra kod.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Update magento/ece-tools"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Efter testvalideringen sammanfogar du den här grenen med integreringsgrenen.
