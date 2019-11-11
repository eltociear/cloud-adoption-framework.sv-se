---
title: Bästa praxis för Azure-migrering
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introduktion till bästa praxis för Azure-migrering
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 1519adff06d600b9829c9b7ff3ca82a0aa5a0160
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753376"
---
# <a name="azure-migration-best-practices"></a>Bästa praxis för Azure-migrering

Azure innehåller flera verktyg som underlättar genomförandet av migrering. Det här avsnittet av Cloud Adoption Framework är utformat för att hjälpa läsarna att implementera dessa verktyg i linje med bästa praxis för migrering. Denna bästa praxis överensstämmer med en av processerna i den Cloud Adoption Framework-migreringsmodell som visas nedan.

Expandera valfri process i innehållsförteckningen till vänster om du vill se den bästa praxis som vanligtvis krävs under den processen.

![Cloud Adoption Framework-migreringsmodellen](../../_images/operational-transformation-migrate.png)

> [!NOTE]
> Planering för digital egendom och tillgångsutvärdering representerar två olika nivåer av migreringsplanering och -utvärdering:
>
> - **Planering för digital egendom:** Du planerar eller rationaliserar den digitala egendomen under planering för att upprätta en övergripande uppgiftslista för migrering. Dock baseras den här planen på vissa antaganden och detaljer som behöver valideras innan en arbetsbelastning kan migreras.
> - **Tillgångsutvärdering:** Du utvärderar en arbetsbelastnings enskilda tillgångar innan arbetsbelastningen migreras för att utvärdera kompatibiliteten med molnet och för att förstå arkitektur- och storleksbegränsningar. Den här processen validerar inledande antaganden och ger den information som behövs för att migrera enskilda tillgångar.
