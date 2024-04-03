---
title: "Logga in på [!DNL Cloud Console]"
description: Läs mer om [!DNL Cloud Console] för Adobe Commerce i molninfrastruktur.
recommendations: noDisplay, catalog
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: c19a36b6-e5e8-461c-a82c-68b7bf121999
source-git-commit: abe9aa36b907be8bdfdf42e6f28f1e1eac68fecf
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# Logga in på [!DNL Cloud Console]

The [!DNL Cloud Console] innehåller interaktiva metoder för att skapa, hantera och distribuera Commerce-kod. The [!DNL Cloud Console] är en modernare, användarvänlig upplevelse som lägger grunden till framtida förbättringar av gränssnittet.

[Logga in på [!DNL Cloud Console]](https://console.adobecommerce.com) för att visa projektlistan.

![Projektlista](../assets/ui-allprojects-list.png)

## Funktioner

Nya eller förbättrade funktioner:

- Tydlig översikt över projekt- och miljöegenskaper
- Aktivitetsström med sorterbar historik
- Manuell hantering av säkerhetskopiering och historik för startprojekt
- Förbättrade loggvyer
- Sorterbara listor
- Enkla formulär och vägledning för att lägga till integreringar
- WCAG-kompatibilitet (Web Content Accessibility Guidelines)

![[!DNL Cloud Console]](../assets/CloudConsole.svg)

De nya eller förbättrade funktionerna är följande:

| Funktion | Förbättringar |
| -------------- | ----------------------------------- |
| [Aktivitetsström](../cloud-guide/project/activity-stream.md) | Interagera med en sorterbar lista över pågående, väntande eller historiska åtgärder. Välj en aktivitet och visa loggar eller avbryt en pågående version. |
| [Projekt- och miljööversikter](../cloud-guide/project/overview.md#project-overview) | Öppna projektet och se en översikt över projektinformation och miljölista. I miljööversikten finns mer information om miljöstatus, programåtkomst och senaste aktiviteter. |
| [Integrationsblanketter](../cloud-guide/integrations/overview.md) | Använd enkla formulär och vägledning för att lägga till integreringar, som Bitbucket eller Slack. |
| [Projektlista](../cloud-guide/project/overview.md#cloud-console) | The _Alla projekt_ visar en lista över alla projekt som du har behörighet att komma åt. Klicka **[!UICONTROL Show filters]** och filtrera projektlistan efter typ, region eller plan. |
| [Alternativ för variabel synlighet](../cloud-guide/environment/variable-levels.md) | Begränsa synligheten för en variabel på projektnivå eller miljönivå under bygge eller körning. |

<!-- The following are features yet to be activated:
| **Apps and services topology** | The Apps & Services topology is visible on Project and Environment views. This interactive diagram allows you to select a service and view the relationship details, such as name, type, version, port, and more. Click **[!UICONTROL View details]** to access the overview and configuration panel for each service. | -->

## Konsolfrågor

**_Var hittar jag funktionen Fixeringar?_**?

För [!DNL Starter] projekt kallas nu funktionen för ögonblicksbilder _Säkerhetskopior_. Du kan skapa en manuell säkerhetskopia av [!DNL Starter] från [!DNL Cloud Console] eller skapa en ögonblicksbild från Cloud CLI. Du måste ha en administratörsroll för miljön.

Välj en miljö i projektnavigeringsfältet. Miljön måste vara aktiv. Välj **[!UICONTROL Backups]** -fliken. För närvarande är det här alternativet inte tillgängligt för Pro-miljöer.

**_Var finns listan över konfigurerade vägar för miljön?_**?

Du hittar listan över konfigurerade vägar på _Tjänster_ -flik för en miljö.

Välj en miljö i projektnavigeringsfältet. Välj **[!UICONTROL Services]** -fliken. The **Router** I visas de konfigurerade vägarna. Du kan för närvarande inte lägga till en väg från den nya [!DNL Cloud Console].

## Menyn Konto

I det övre högra hörnet finns din kontomeny. Klicka på nedpilen för menyn och välj **[!UICONTROL My Profile]**. I _Min profil_ kan du styra användarinformation och visningsinställningar, hantera [autentisering av säkerhet](../cloud-guide/project/user-access.md#user-authentication-requirements), [API-token](../cloud-guide/project/user-access.md#create-an-api-token)och [SSH-nycklar](../cloud-guide/development/secure-connections.md).
