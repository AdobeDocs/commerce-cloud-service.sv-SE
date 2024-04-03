---
title: SkickaGrid-e-posttjänst
description: Lär dig mer om e-posttjänsten SendGrid för Adobe Commerce i molninfrastrukturen och hur du kan testa din DNS-konfiguration.
exl-id: 30d3c780-603d-4cde-ab65-44f73c04f34d
source-git-commit: 7c22dc3b0e736043a3e176d2b7ae6c9dcbbf1eb5
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# SkickaGrid-e-posttjänst

Proxytjänsten SendGrid Simple Mail Transfer Protocol (SMTP) tillhandahåller utgående e-postautentisering och anseendeövervakning, inklusive stöd för:

* Alla utgående transaktionsmejl
* Dedikerade IP-adresser
* Domänregistrering, DKIM-signaturer (DomainKeys Identified Mail) för e-postdomänvalidering (endast för Pro Staging- och Production-miljöer)
* Anpassad domänregistrering (endast för Pro)
* Automatisk integrering för integreringsmiljöerna Starter och Pro. Proffsproduktions- och mellanlagringsmiljöer kräver manuell etablering och konfiguration under maskinvaruprovisioneringsprocessen för Infrastructure as a Service (IaaS)

SendGrid SMTP-proxyn är inte avsedd att användas som en allmän e-postserver för att ta emot inkommande e-post eller för användning med e-postmarknadsföringskampanjer.

>[!TIP]
>
>Information om SendGrid för ditt konto finns i [Gränssnitt för introduktion](https://cloud.magento.com) och väljer **Projektinformation** > **Värdinformation** -fliken.

## Aktivera eller inaktivera e-post

Som standard är utgående e-post aktiverad i Pro Production- och Staging-miljöer. The [!UICONTROL Outgoing emails] kan visas i miljöinställningarna oavsett status tills du anger `enable_smtp` -egenskap. Du kan aktivera utgående e-postmeddelanden för andra miljöer för att skicka autentiseringsmeddelanden i två nivåer till användare av Cloud-projekt. Se [Konfigurera e-postmeddelanden för testning](outgoing-emails.md).

## Kontrollpanel för SendGrid

Alla Cloud-projekt hanteras under ett centralt konto, så bara supporten har tillgång till kontrollpanelen SendGrid. SendGrid innehåller inga funktioner för begränsning av underkonto.

Om du vill granska aktivitetsloggarna för leveransstatus eller en lista över e-postadresser som studsat, avvisats eller blockerats, [skicka en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). Supportteamet **inte** hämta aktivitetsloggar som är äldre än 30 dagar.

Om det är möjligt kan du inkludera följande information i din begäran:

* e-postadresser som påverkas
* den aktuella tidsramen (endast under de senaste 30 dagarna)
* e-postmeddelandets ämne

## Identifierad post för DomainKeys (DKIM)

DKIM är en teknik för e-postautentisering som gör det möjligt för internetleverantörer att identifiera både giltiga och falska avsändaradresser, en teknik som ofta används vid nätfiske och e-postbedrägerier. DKIM förlitar sig på en domänägare som hanterar DNS-posterna. När du använder DKIM använder avsändarservern en privat nyckel för att signera meddelandena. Domänägaren lägger också till en DKIM-post, som är en ändrad `TXT` till avsändardomänens DNS-poster. Detta `TXT` posten innehåller en offentlig nyckel som mottagarens e-postservrar använder för att verifiera signaturen för ett meddelande. Kryptografiproceduren för den offentliga nyckeln DKIM gör det möjligt för mottagarna att verifiera en avsändares äkthet. Se [DKIM-poster förklaras](https://docs.sendgrid.com/ui/account-and-settings/dkim-records).

>[!WARNING]
>
>Stöd för SendGrid DKIM-signaturer och domänautentisering är bara tillgängligt för Pro-projekt och inte för Starter. Därför är det troligt att utgående transaktionsmejl flaggas av skräppostfilter. Om du använder DKIM förbättras leveransfrekvensen som en autentiserad e-postavsändare. Om du vill förbättra leveransfrekvensen för meddelanden kan du uppgradera från Starter till Pro eller använda en egen SMTP-server eller e-postleverantör. Se [Konfigurera e-postanslutningar](https://experienceleague.adobe.com/docs/commerce-admin/systems/communications/email-communications.html) i _Administratörssystemguide_.

### Avsändare och domänautentisering

För att SendGrid ska kunna skicka transaktionsmeddelanden för din räkning från Pro Production- eller Staging-miljöer måste du konfigurera dina DNS-inställningar så att de inkluderar de tre DNS-posterna för SendGrid-underdomänen. Varje SendGrid-konto tilldelas ett unikt `TXT` post som används för att autentisera utgående e-post.

**Aktivera domänautentisering**:

1. Skicka en [supportbiljett](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) som begär att DKIM ska aktiveras för en specifik domän (**Proffsmiljöer för mellanlagring och produktion**).
1. Uppdatera din DNS-konfiguration med `TXT` och `CNAME` poster som du har fått i supportanmälan.

**Exempel `TXT` post med konto-ID**:

```text
v=spf1 include:u17504801.wl.sendgrid.net -all
```

**Exempel `CNAME` poster**:

| Domän | Punkter till | Posttyp |
| ---------- | ---------- | ------------- |
| em.emaildomain.com | uxxxxxx.wl.sendgrid.net | CNAME |
| s1._domainkey.emaildomain.com | s1.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |
| s2._domainkey.emaildomain.com | s2.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |

### DKIM-signaturer och automatiserad säkerhet

Du kan välja mellan automatiserad och manuell säkerhet när du skapar en autentiserad domän. Om du väljer automatiserad säkerhet hanterar SendGrid dina DKIM- och SPF-poster automatiskt. När du lägger till en ny dedikerad sändande IP-adress till ditt konto uppdaterar SendGrid dina DNS-inställningar och DKIM-signatur omedelbart. Om du stänger av automatisk säkerhet ansvarar du för att uppdatera din DKIM-signatur när du vill ändra den sändande domänen.

**Exempel på automatiserad säkerhet aktiverat**:

```text
subdomain.mydomain.com. | CNAME | uxxxxxx.wl.sendgrid.net
s1._domainkey.mydomain.com. | CNAME | s1.domainkey.uxxxxxx.wl.sendgrid.net
s2._domainkey.mydomain.com. | CNAME | s2.domainkey.uxxxxxx.wl.sendgrid.net
```

**Exempel på automatisk säkerhet inaktiverat**:

```text
me12345.mydomain.com | MX | mx.sendgrid.net
me12345.mydomain.com | TXT | v=spf1 include:sendgrid.net ~all
m1._mydomain.com | TXT | k=rsa; t=s; p=<public-key>
```

När domänautentisering har konfigurerats hanterar SendGrid automatiskt SPF- (Security Policy Framework) och DKIM-poster åt dig. Efter SendGrid innehåller `CNAME` poster som du vill lägga till i dina DNS-poster kan du lägga till dedikerade IP-adresser och göra andra kontouppdateringar utan att du behöver hantera dina SPF-poster manuellt. Se [Automatisk säkerhet och din DKIM-signatur](https://docs.sendgrid.com/ui/account-and-settings/dkim-records#automated-security-and-your-dkim-signature).

Så här testar du DNS-konfigurationen:

```terminal
dig CNAME em.domain_name
dig CNAME s1._domainkey.domain_name
dig CNAME s2._domainkey.domain_name
```

## Tröskelvärde för transaktionsmeddelanden

Tröskelvärdet för transaktionella e-postmeddelanden avser antalet transaktionsmeddelanden som du kan skicka från Pro-miljöer under en viss tidsperiod, till exempel 12 000 e-postmeddelanden per månad från icke-produktionsmiljöer. Tröskelvärdet är utformat för att skydda mot att skicka skräppost och eventuellt skada ditt e-postrykte.

Det finns inga strikta gränser för hur många e-postmeddelanden som kan skickas i produktionsmiljön, så länge poängen Sender Reputation är över 95 %. Anseendet påverkas av antalet avvisade eller avvisade e-postmeddelanden och om DNS-baserade skräppostregister har flaggat din domän som en potentiell skräppostkälla. Se [E-postmeddelanden skickas inte när SendGrid-krediter överskrids på Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/emails-not-being-sent-sendgrid-credits-exceeded.html) i _Knowledge Base för Commerce Support_.

**Kontrollera om det maximala antalet krediter har överskridits**:

1. Byt till din projektkatalog på din lokala arbetsstation.

1. Använd SSH för att logga in i fjärrmiljön.

   ```bash
   magento-cloud ssh
   ```

1. Kontrollera `/var/log/mail.log` for `authentication failed : Maxium credits exceeded` poster.

   Om du ser `authentication failed` loggposter och **E-postavsändarens rykte** är minst 95, du kan [Skicka in en Adobe Commerce-supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) för att begära en ökning av kredittilldelningen.

### E-postavsändarens rykte

Ett e-postrykte är en poäng som tilldelats av en Internet-leverantör (ISP) till ett företag som skickar e-postmeddelanden. Ju högre poäng, desto troligare är det att en Internet-leverantör levererar meddelanden till en mottagares inkorg. Om poängen ligger under en viss nivå kan Internet-leverantören dirigera meddelanden till mottagarnas skräppostmapp eller till och med avvisa meddelanden helt. Anseendepoängen bestäms av flera faktorer, som ett 30-dagars genomsnitt av dina IP-adresser, jämfört med andra IP-adresser och andelen skräppost. Se [5 sätt att kontrollera ditt rykte](https://sendgrid.com/blog/5-ways-check-sending-reputation/).
