---
title: Konfigurera utgående e-post
description: Lär dig hur du aktiverar utgående e-post för Adobe Commerce i molninfrastruktur.
exl-id: 814fe2a9-15bf-4bcb-a8de-ae288fd7f284
source-git-commit: 59f82d891bb7b1953c1e19b4c1d0a272defb89c1
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Konfigurera utgående e-post

Du kan aktivera och inaktivera utgående e-post för varje miljö från [!DNL Cloud Console] eller från kommandoraden. Aktivera utgående e-post för integrering och staging-miljöer för att skicka tvåfaktorsautentisering eller återställa lösenordsmeddelanden för användare av Cloud-projekt.

Som standard är utgående e-post aktiverat i produktions- och mellanlagringsmiljöer. Men [!UICONTROL Enable outgoing emails] kan vara inaktiverat i miljöinställningarna tills du ställer in `enable_smtp` -egenskapen via [kommandorad](#enable-emails-in-the-cli) eller [Cloud Console](outgoing-emails.md#enable-emails-in-the-cloud-console).

Uppdaterar [!UICONTROL enable_smtp] egenskapsvärde efter [kommandorad](#enable-emails-in-the-cli) ändrar även [!UICONTROL Enable outgoing emails] ange ett värde för den här miljön på molnkonsolen.

{{redeploy-warning}}

## Aktivera e-post i molnkonsolen

Använd **[!UICONTROL Outgoing emails]** växla i _Konfigurera miljö_ för att aktivera eller inaktivera e-postsupport.

Om utgående e-post måste inaktiveras eller återaktiveras i Pro Production- eller Staging-miljöer kan du skicka en [Adobe Commerce Support](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

>[!TIP]
>
>Status för utgående e-post kanske inte återspeglas för Pro-miljöer på molnkonsolen. Använd i stället [kommandorad](#enable-emails-in-the-cli) för att aktivera och testa utgående e-postmeddelanden.

**Hantera e-postsupport från[!DNL Cloud Console]**:

1. Logga in på [[!DNL Cloud Console]](https://console.adobecommerce.com).
1. Välj ett projekt i _Alla projekt_ lista.
1. Klicka på konfigurationsikonen i det övre högra hörnet på projektkontrollpanelen.
1. Klicka **[!UICONTROL Environments]** och väljer en specifik miljö i listan.
1. Om du vill aktivera eller inaktivera utgående e-post växlar du _Aktivera utgående e-post_ **På** eller **Av**.

   ![Aktivera konfiguration för utgående e-post](../../assets/outgoing-emails.png)

När du har ändrat inställningen byggs och distribueras miljön med den nya konfigurationen.

## Aktivera e-post i CLI

Du kan ändra e-postkonfigurationen för en aktiv miljö med `magento-cloud` CLI `environment:info` för att ange `enable_smtp` -egenskap. Aktivera SMTP-uppdateringar för `MAGENTO_CLOUD_SMTP_HOST` miljövariabel med IP-adressen för SMTP-värden för att skicka e-post.

**Hantera e-postsupport från kommandoraden**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Kontrollera miljöns inställning för utgående e-post.

   ```bash
   magento-cloud environment:info -e <environment-id> | grep enable_smtp
   ```

1. Ändra konfigurationen för e-postsupport genom att ställa in `enable_smtp` miljövariabel till `true` eller `false`.

   ```bash
   magento-cloud environment:info --refresh -e <environment-id> enable_smtp true
   ```

   Vänta på att miljön ska byggas och distribueras.

1. Använd en SSH för att logga in i fjärrmiljön.

1. Verifiera att e-postmeddelandet fungerar. Skicka ett test-e-postmeddelande till en adress som du kan kontrollera.

   ```bash
   php -r 'mail("mail@example.com", "test message", "just testing", "From: tester@example.com");'
   ```

1. Kontrollera att e-postmeddelandet har hämtats av SendGrid.

   ```bash
   grep mail@example.com /var/log/mail.log
   ```
