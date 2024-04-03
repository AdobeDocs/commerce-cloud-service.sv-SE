---
title: Konfigurera RabbitMQ-tjänst
description: Lär dig hur du aktiverar tjänsten RabbitMQ för att hantera meddelandeköer för Adobe Commerce i molninfrastruktur.
feature: Cloud, Services
exl-id: 85794b8f-2260-4a6e-b5a6-a1b4c356594e
source-git-commit: d4c36b084094846cfad69adc2bffd567a58fab26
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Konfigurera [!DNL RabbitMQ] service

The [MQF (Message Queue Framework)](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework.html) är ett system i Adobe Commerce som tillåter [modul](https://glossary.magento.com/module) för att publicera meddelanden till köer. Det definierar också de konsumenter som tar emot meddelandena asynkront.

MQF använder [RabbitMQ](https://www.rabbitmq.com/) som meddelandeförmedlare, som tillhandahåller en skalbar plattform för att skicka och ta emot meddelanden. Den innehåller även en mekanism för att lagra olevererade meddelanden. [!DNL RabbitMQ] baseras på specifikationen Advanced Message Queuing Protocol (AMQP) 0.9.1.

>[!WARNING]
>
>Om du föredrar att använda en befintlig AMQP-baserad tjänst, som [!DNL RabbitMQ], i stället för att förlita dig på Adobe Commerce i molninfrastrukturen för att skapa den åt dig, ska du använda [`QUEUE_CONFIGURATION`](../environment/variables-deploy.md#queue_configuration) systemvariabel för att ansluta den till din plats.

{{service-instruction}}

**Aktivera RabbitMQ**:

1. Lägg till önskat namn, typ och diskvärde (i MB) i `.magento/services.yaml` tillsammans med den installerade RabbitMQ-versionen.

   ```yaml
   rabbitmq:
       type: rabbitmq:<version>
       disk: 1024
   ```

1. Konfigurera relationerna i `.magento.app.yaml` -fil.

   ```yaml
   relationships:
       rabbitmq: "rabbitmq:rabbitmq"
   ```

1. Lägg till, implementera och push-överföra kodändringar.

   ```bash
   git add .magento/services.yaml .magento.app.yaml
   ```

   ```bash
   git commit -m "Enable RabbitMQ service"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. [Verifiera tjänstrelationerna](services-yaml.md#service-relationships).

{{service-change-tip}}

## Anslut till RabbitMQ för felsökning

I felsökningssyfte är det praktiskt att ansluta direkt till en tjänstinstans på något av följande sätt:

- Anslut från din lokala utvecklingsmiljö
- Anslut från programmet
- Anslut från ditt PHP-program

### Anslut från din lokala utvecklingsmiljö

1. Logga in på `magento-cloud` CLI och projekt:

   ```bash
   magento-cloud login
   ```

1. Kolla in miljön med RabbitMQ installerat och konfigurerat.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. Använd SSH för att ansluta till molnmiljön:

   ```bash
   magento-cloud ssh
   ```

1. Hämta anslutningsinformation och inloggningsuppgifter för RabbitMQ från [$MAGENTO_CLOUD_RELATIONSHIPS](../application/properties.md#relationships) variabel:

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   eller

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   I svaret hittar du information om RabbitMQ, till exempel:

   ```json
   {
      "rabbitmq" : [
         {
            "password" : "guest",
            "ip" : "246.0.129.2",
            "scheme" : "amqp",
            "port" : 5672,
            "host" : "rabbitmq.internal",
            "username" : "guest"
         }
      ]
   }
   ```

1. Aktivera lokal portvidarebefordran till RabbitMQ.

   ```bash
   ssh -L <port-number>:rabbitmq.internal:<port-number> <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

   Ett exempel på hur du får åtkomst till RabbitMQ webbgränssnitt för hantering på `http://localhost:15672` är:

   ```bash
   ssh -L 15672:rabbitmq.internal:15672 <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

1. När sessionen är öppen kan du starta en valfri RabbitMQ-klient från den lokala arbetsstationen som är konfigurerad för att ansluta till `localhost:<portnumber>` med hjälp av portnummer, användarnamn och lösenordsinformation från variabeln MAGENTO_CLOUD_RELATIONSHIPS.

### Anslut från programmet

Installera en klient, till exempel för att ansluta till RabbitMQ som körs i ett program [amqp-utils](https://github.com/dougbarth/amqp-utils), som ett projektberoende i `.magento.app.yaml` -fil.

Exempel:

```yaml
dependencies:
    ruby:
        amqp-utils: "0.5.1"
```

När du loggar in på PHP-behållaren anger du `amqp-` tillgängliga för att hantera köer.

### Anslut från ditt PHP-program

Om du vill ansluta till RabbitMQ med ditt PHP-program lägger du till en PHP [bibliotek](https://glossary.magento.com/library) till källträdet.
