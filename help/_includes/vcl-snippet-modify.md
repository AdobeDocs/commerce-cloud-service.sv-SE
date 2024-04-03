---
source-git-commit: 2d902a3926c6bbc6a9dc8afcbd667eddeaf3be7e
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---
# Inkludera fil för snabb ändring av anpassad VCL

## Ändra det anpassade VCL-fragmentet

1. [Logga in](/help/get-started/onboarding.md#access-your-admin-panel) till administratören.

1. Klicka **Lager** > **Inställningar** > **Konfiguration** > **Avancerat** > **System**.

1. Expandera **Helsidescache** > **Snabb konfiguration** > **Anpassade VCL-kodfragment**.

   ![Hantera anpassade VCL-fragment](/help/assets/cdn/fastly-manage-snippets.png)

1. I _Åtgärd_ klickar du på inställningsikonen bredvid det fragment som ska redigeras.

1. När sidan har lästs in igen klickar du på **Ladda upp VCL snabbt** i _Snabb konfiguration_ -avsnitt.

1. När överföringen är klar uppdaterar du cacheminnet enligt meddelandet längst upp på sidan.

>[!WARNING]
>
>The _Anpassade VCL-fragment_ I gränssnittsalternativet visas endast de fragment som har lagts till via Adobe Commerce Admin. Om du lägger till fragment med API:t Snabb använder du API:t för att [hantera dem](/help/cloud-guide/cdn/fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api).
