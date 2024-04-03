---
title: Bästa tillvägagångssätt för att uppgradera ditt projekt
description: Se en lista över de bästa sätten att uppgradera dina projektfiler.
feature: Cloud, Best Practices, Upgrade
exl-id: 7d0a2627-e4c5-46b4-9e6c-24d20fa4f92f
source-git-commit: c61d711b1041ecf76ec6468cd225a34fd77c24b1
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Bästa tillvägagångssätt för att uppgradera ditt projekt

Följ vedertagna standarder för byggen och driftsättningen och använd [Uppgraderingar och patchar](../development/commerce-version.md) arbetsflöde för att uppgradera programmet. Använd följande riktlinjer för att planera uppgraderings- och efteruppgraderingsarbetet:

- **Säkerhetskopiera ditt projekt**-Innan du uppgraderar Adobe Commerce och eventuella tillägg från tredje part eller anpassade, bör du säkerhetskopiera databasen i integrerings-, mellanlagrings- och produktionsmiljöer. Se [Säkerhetskopiera databasen](../development/commerce-version.md#project-backup).

- **Kontrollera kompatibilitetsproblem**-

   - Kontrollera att alla anpassade teman är kompatibla med den nya Adobe Commerce-versionen

   - När du har uppgraderat tillägg från tredje part och anpassade tillägg använder du `magento-cloud local:build` för att validera Composer-beroenden före distributionen.

   - Granska versionsinformationen och tilläggsdokumentationen för Adobe Commerce för att kontrollera att du har implementerat de tillfälliga lösningar eller konfigurationsändringar som krävs för att åtgärda kända funktionsproblem och fel som gäller den uppgraderade Adobe Commerce-versionen och tillägg.

   - Kontrollera att de installerade tjänstversionerna är kompatibla med den nya Adobe Commerce-versionen och uppgradera tjänsterna efter behov. Se [Tjänster](../services/services-yaml.md).

   - Testa databasen för att åtgärda eventuella problem som uppstår vid uppdateringar av Adobe Commerce-versionen och tillägg.

   - Gör nödvändiga uppdateringar av miljöspecifika inställningar innan du distribuerar till fjärrmiljön.

   - Kontrollera att söktjänstversionen är kompatibel med PHP-klientversionen. Se [Konfigurera Elasticsearch](../services/elasticsearch.md) eller [Konfigurera OpenSearch](../services/opensearch.md).

- **Kontrollera databaskopplingar och tillgängligt lagringsutrymme i fjärrmiljöer**-

   - Använd SSH för att logga in på fjärrservern och verifiera anslutningen till MySQL-databasen. Se [Anslut till databasen](../services/mysql.md#connect-to-the-database).

   - Verifiera tillgängligt lagringsutrymme i fjärrmiljön-Använd `disk free` för att visa och hantera tillgängligt diskutrymme i dina molnmiljöer. Se [Hantera diskutrymme](../storage/manage-disk-space.md).

      - Kontrollera storleken på den uppgraderade databasen och verifiera att `services.yaml` filen har tillräckligt med ledigt diskutrymme.

      - Frigör diskutrymme - Rensa cacheminnet och rensa `/log` och `/tmp` kataloger före distribution.

- **Planera och utför en uppgradering på lokal miljö och i integreringsmiljöer innan den distribueras till mellanlagring**-Efter uppgraderingen testar du driftsättningen och löser eventuella problem.

- **Koppla kod till mellanlagring och sedan till produktion**-Testa och åtgärda eventuella problem i mellanlagringsmiljön innan du gör några ändringar i produktionsmiljön.

- **Slutföra efteruppgraderingar**-

   - Använd SSH för att logga in på fjärrservern och verifiera följande:

      - Kontrollera indexerarens status och indexera om det behövs. Se [Hantera indexerare](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/manage-indexers.html) i _Konfigurationsguide_.

      - Kontrollera `cron` loggar och `cron_schedule` i Adobe Commerce-databasen för att verifiera kronistatus och köra kron-jobb igen efter behov.
Se [Loggning](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html#logging) i _Konfigurationshandbok_.

   - Slutför UAT-testet (User Acceptance Testing UAT) efter uppgraderingen och åtgärda eventuella problem som rör uppgraderingar från tredje part och anpassade tillägg.
