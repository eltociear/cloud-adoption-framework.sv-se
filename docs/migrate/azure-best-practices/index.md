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
ms.openlocfilehash: e8a7ae0af3b64a6d7e04555fe64a6189d964b3ff
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70816575"
---
# <a name="azure-migration-best-practices"></a>Bästa praxis för Azure-migrering

Azure innehåller flera verktyg som underlättar genomförandet av migrering. Det här avsnittet av Cloud Adoption Framework är utformat för att hjälpa läsarna att implementera dessa verktyg i linje med bästa praxis för migrering. Denna bästa praxis överensstämmer med en av processerna i den Cloud Adoption Framework-migreringsmodell som visas nedan.

Expandera valfri process i innehållsförteckningen till vänster om du vill se den bästa praxis som vanligtvis krävs under den processen.

![Cloud Adoption Framework-migreringsmodellen](../../_images/operational-transformation-migrate.png)

> [!NOTE]
> Planering för digital egendom och tillgångsutvärdering representerar två olika nivåer av migreringsplanering och -utvärdering:
>
> - **Planering för digital egendom:** Du planerar eller rationaliserar den digitala egendomen under planering för att upprätta en övergripande uppgiftslista för migrering. Dock baseras den här planen på vissa antaganden och detaljer som behöver valideras innan en arbetsbelastning kan migreras.
> - **Tillgångsutvärdering:** Du utvärderar en arbetsbelastnings enskilda tillgångar före migrering av arbetsbelastningen i syfte att utvärdera kompatibilitet för molnet samt förstå arkitekturen och storleksbestämma begränsningar. Den här processen validerar inledande antaganden och ger den information som behövs för att migrera enskilda tillgångar.
