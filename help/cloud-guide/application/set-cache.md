---
title: Ange cache för statiska filer
description: Lär dig hur du anger alternativ för cachelagring i [!DNL Commerce] programkonfigurationsfil.
feature: Cloud, Configuration, Cache, SCD
exl-id: ca6db004-47fc-45ea-b8db-c0ecc3c2136b
source-git-commit: eace5d84fa0915489bf562ccf79fde04f6b9d083
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Ange cache för statiska filer

TTL-värdet (time-to-live) för dina media och statiska filer anges i `.magento.app.yaml` konfigurationsfilen med `expires` -tangenten.

>[!NOTE]
>
>Innan du uppdaterar produktionsmiljön är det viktigt att du testar ändringarna i mellanlagringsmiljön. [Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om du vill ha hjälp med att uppdatera konfigurationen i dessa miljöer.

1. Ange TTL-tiden (i sekunder) i dialogrutan [`web` property](web-property.md) i `.magento.app.yaml` -fil. Du kan lägga till `expires` tangent under `locations` eller under `"/media"` och `"/static"`.

   Om du vill förhindra att cachen förfaller använder du `expires: -1` nyckelvärdepar. Se följande exempel:

   ```yaml
   # The configuration of app when it is exposed to the web.
   web:
     locations:
       "/media":
         ...
         expires: -1
   
       "/static":
         ...
         expires: -1
   ```

1. Lägg till, implementera och push-överföra kodändringar.

   ```bash
   git add -A && git commit -m "Set cache TTL for static files" && git push origin <branch-name>
   ```
