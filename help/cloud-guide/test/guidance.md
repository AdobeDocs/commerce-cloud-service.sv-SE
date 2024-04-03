---
title: Testvägledning
description: Läs om testningstyper och de bästa sätten att starta Adobe Commerce på molninfrastrukturen.
exl-id: 1d7897a2-af97-46ab-89c0-2ec54284190e
source-git-commit: aae285d85188bfadd73d5b4e1fea16afa5beb117
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Testvägledning

När du har konfigurerat och anpassat ditt Adobe Commerce i ett molninfrastrukturprojekt är det bäst att testa programmet noggrant innan du startar butikens webbplats. Testning hjälper till att hantera förväntningarna på klusterstorleken på rätt sätt och skalas för framtida affärsbehov.

## Funktionstestning

Under utvecklingen är det viktigt att du utför funktionstestning från början till slut på ditt Adobe Commerce i molninfrastrukturprojekt. Se följande riktlinjer för funktionstestning i Docker-miljön:

- **Programtestning**—Använd [Magento Functional Testing Framework (MFTF)](https://developer.adobe.com/commerce/cloud-tools/docker/test/application-testing/) för programtestning i Cloud Docker-miljön.

- **Kodtestning**—Använd [Testramverk för kodekering för PHP](https://developer.adobe.com/commerce/cloud-tools/docker/test/code-testing/) för validering av kod som är avsedd att bidra till molnpaketets databaser.

## Bästa tillvägagångssätt före lansering

Tänk på följande testtyper som en bra metod att utföra innan webbplatsen startas:

- **Lastprovning**- Utför ett belastningstest för att förstå systemets beteende under en förväntad belastning. Testa till exempel ett antal aktiva användare samtidigt i programmet, där varje användare utför ett visst antal transaktioner inom den angivna varaktigheten. Det här testet visar svarstiden för viktiga affärskritiska transaktioner, som databasen eller programserverfunktionen. Ett belastningstest kan hjälpa till att identifiera flaskhalsar.

- **Stresstest**- Utmana de övre gränserna för kapaciteten i systemet för att avgöra om systemet fungerar tillräckligt när den aktuella belastningen ligger långt över förväntat maxvärde.

- **Säkerhetsgenomsökning**—Adobe erbjuder en kostnadsfri [Verktyg för säkerhetsgenomsökning](../launch/overview.md#set-up-the-security-scan-tool) för era webbplatser.

- **Penetrationsprovning**- Är en godkänd simulerad cyberattack på ett datorsystem som är utformat för att utvärdera systemets säkerhet. Inpenetrationstestet hjälper till att identifiera svagheter eller sårbarheter, inklusive potentialen för obehöriga parter att få tillgång till systemfunktioner och data.

>[!WARNING]
>
>Kunderna får inte själva utföra säkerhetsbedömningar av AWS infrastruktur eller AWS tjänster. Om du upptäcker ett säkerhetsproblem i någon av de AWS-tjänster som ingår i säkerhetsutvärderingen, [kontakta AWS Security](mailto:aws-security@amazon.com) omedelbart. Se [AWS kundpolicyer för penetrationstestning](https://aws.amazon.com/security/penetration-testing/).
