---
title: Versionsinformation om Cloud Tools Suite
description: Läs om de senaste förbättringarna av Cloud Tools Suite för Adobe Commerce.
feature: Cloud, Release Notes
exl-id: 6a652e93-46a2-4590-97fc-fb5d114ece9a
source-git-commit: 40c0d4ca6b70d7cea988209e7e3c8b7e3cd3522e
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Versionsinformation om Commerce Cloud Tools Suite

Den här versionsinformationen innehåller information om de senaste förbättringarna av Cloud Tools Suite for Commerce-paketen som är utformade för att distribuera och hantera Adobe Commerce-installationer och uppgraderingar på molnplattformen.

| Versionsinformation | Version | Beskrivning | Källa |
| ----------------- |-----------| ---------------------------------------- | --------------------------- |
| [`ece-tools` package](ece-tools-package.md) | 2002.1.18 | En uppsättning skript och verktyg som utformats för att hantera och driftsätta Cloud-projekt | [`magento/ece-tools`](https://github.com/magento/ece-tools/tree/2002.1) |
| [Cloud Patches for Commerce](cloud-patches.md) | 1.0.26 | En uppsättning patchar som förbättrar integreringen av alla Adobe Commerce-versioner med molnmiljöer. Paketet innehåller Adobe Commerce patchar och tillgängliga snabbkorrigeringar som tillämpas när du använder `ece-tools` för att distribuera | [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches/tree/1.0.1) |
| [Cloud Docker for Commerce](cloud-docker.md) | 1.3.7 | Funktions- och konfigurationsfiler för Docker-bilder som ska distribuera Adobe Commerce till en lokal molnmiljö | [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker/tree/1.0) |
| [Cloud Components of Commerce](cloud-components.md) | 1.0.14 | Utökad Adobe Commerce-funktionalitet för webbplatser i molninfrastrukturen | [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components/tree/1.0.2) |

När du uppdaterar till ECE-Tools 2002.1.0 eller senare, uppdateras du automatiskt till de senaste versionerna av de andra paketen, som är beroenden för `ece-tools` paket. Se [Cloud-metapaket](../development/overview.md#cloud-metapackage) för en lista över beroenden.
