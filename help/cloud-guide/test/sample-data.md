---
title: Exempeldata
description: Lär dig hur du installerar exempeldata med Adobe Commerce i molninfrastrukturen.
exl-id: 517e549f-15ba-47b3-9236-a1c4d24c917d
source-git-commit: 8a0523f1714b6ea41887e99b5c31294cf5e5255e
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Exempeldata

Om du behöver exempeldata när du utvecklar din butik kan du installera exempeldata. Dessa data simulerar en aktiv Adobe Commerce-butik med kunder, produkter och andra data. Dessa exempeldata fungerar bäst med en ny installation av Adobe Commerce i en molninfrastruktursmall.

Det bästa sättet är att installera exempeldata i utvecklings- och integreringsmiljöer. Om du använder exempeldata i Förproduktion eller Produktion måste du [ta bort](#reset-or-uninstall-sample-data) informationen och produkterna innan du går live.

## Installera exempeldata

Så här installerar du exempeldata:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. I roten anger du följande kommando för att lägga till exempeldata:

   ```bash
   ./bin/magento sampledata:deploy
   ```

1. Vänta på att komponenter ska uppdateras.

1. Verkställ och skicka ändringarna:

   ```bash
   git add -A && git commit -m "Install sample data"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Vänta på att projektet ska distribueras.

1. Kontrollera att installationen lyckades genom att gå till din butikssida i integreringsmiljön. Du kan hitta URL-länken till butiken via [!DNL Cloud Console].

1. Ta en ögonblicksbild av din miljö:

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

Du kan börja testa din utveckling med livedata!

## Återställ eller avinstallera exempeldata

Du kan återställa eller ta bort exempeldata enligt samma procedur som du använde för att installera exempeldata:

- Ta bort exempeldata: `./bin/magento sampledata:remove`
- Återställ exempeldata: `./bin/magento sampledata:reset`
