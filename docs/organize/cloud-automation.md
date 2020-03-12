---
title: Moln automatiserings funktioner
description: Använd ramverket för moln införande för Azure för att förstå bildande av moln automatiserings funktioner för att påskynda införande och innovation.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: f519425d83691db0b55ea6aa9d84b7371f632ac0
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79093923"
---
# <a name="cloud-automation-capabilities"></a>Moln automatiserings funktioner

Under moln implementeringen kommer Cloud Automation-funktionerna att kunna låsa upp potentialen hos DevOps och en moln intern metod. Expertis i vart och ett av dessa områden kan påskynda införande och innovation.

## <a name="possible-sources-for-cloud-automation-expertise"></a>Möjliga källor för moln automatiserings expert

De kunskaper som krävs för att tillhandahålla moln automatiserings funktioner kan tillhandahållas av:

- DevOps-tekniker
- Utvecklare med expert kunskaper om DevOps och infrastruktur
- IT-tekniker med DevOps och automatiserings expert

Dessa ämnes experter kan tillhandahålla funktioner i andra områden, till exempel moln införande, moln styrning eller moln plattform. När de visar kunskaper om automatisering av komplexa arbets belastningar kan du rekrytera dessa experter för att leverera ett Automation-värde.

## <a name="mindset"></a>Tänkesätt

Innan du får en grupp medlem i den här gruppen bör de Visa tre viktiga egenskaper:

- Expertis i en moln plattform med särskild tonvikt på DevOps och automatisering.
- En tillväxt tänkesätt eller öppenhet för att ändra hur den fungerar idag.
- En önskan att påskynda företags förändringar och ta bort traditionell IT-hindren.

## <a name="key-responsibilities"></a>Viktiga ansvars områden

Den främsta avgiften för moln automatisering är att äga och gå över till lösnings katalogen. Lösnings katalogen är en samling med färdiga lösningar eller automatiserings mallar. Dessa lösningar kan snabbt distribuera olika plattformar efter behov för att stödja arbets belastningar som krävs. Dessa lösningar är Bygg stenar som påskyndar moln införande och minskar tiden till marknaden under migreringen eller innovationen.

Exempel på lösningar i katalogen är:

- Ett skript för att distribuera ett program i behållare
- En Resource Manager-mall för att distribuera ett SQL HA AO-kluster
- Exempel kod för att bygga en distributions pipeline med Azure DevOps
- En Azure DevTest Labs instans av företags-ERP i utvecklings syfte
- Automatisk distribution av en självbetjänings miljö som ofta begärs av företags användare

Lösningarna i lösnings katalogen är inte distributions pipeliner för en arbets belastning. I stället kan du använda Automation-skript i katalogen för att snabbt skapa en distributions pipeline. Du kan också använda en lösning i katalogen för att snabbt etablera plattforms komponenter för att stödja arbets belastnings uppgifter som automatisk distribution, manuell distribution eller migrering.

Följande uppgifter utförs vanligt vis av Cloud Automation med jämna mellanrum:

### <a name="strategic-tasks"></a>Strategiska uppgifter

- Beakta
  - [affärs resultat](../strategy/business-outcomes/index.md)
  - [finansiella modeller](../strategy/financial-models.md)
  - [motivation för moln införande](../strategy/motivations.md)
  - [affärs risker](../govern/policy-compliance/risk-tolerance.md)
  - [rationalisering av den digitala fastigheten](../digital-estate/index.md)
- Övervaka implementerings planer och framsteg mot den [prioriterade migreringen](../migrate/migration-considerations/assess/release-iteration-backlog.md).
- Identifiera möjligheter att påskynda moln användningen, minska arbetet med automatisering och förbättra säkerheten, stabiliteten och konsekvensen.
- Prioritera en efter släpning av lösningar för den lösnings katalog som ger flest värde för andra strategiska indata.

### <a name="technical-tasks"></a>Tekniska uppgifter

- Granska eller utveckla lösningar baserat på prioriterad efter släpning.
- Se till att lösningar överensstämmer med plattforms kraven.
- Se till att lösningarna appliceras konsekvent och uppfyller befintliga styrnings-och efterlevnads krav.
- Skapa och validera lösningar i katalogen.
- Granska versions planer för källor med nya automatiserings möjligheter.

## <a name="meeting-cadence"></a>Mötes takt

Cloud Automation är en arbets grupp. Det förväntar sig att deltagarna genomför en stor del av sina dagliga scheman till moln automatiserings arbete. Bidragen är inte begränsade till möten och feedback-cykler.

Moln automatiserings teamet bör justera aktiviteter med andra funktioner. Den här justeringen kan resultera i en överliggande anslutning. För att säkerställa att Cloud Automation har tillräckligt med tid för att hantera lösnings katalogen bör du gå igenom Mötes cadences för att maximera samarbetet och minimera avbrott i utvecklings aktiviteter.

## <a name="next-steps"></a>Nästa steg

När de viktigaste moln funktionerna justeras kan de kollektiva teamerna hjälpa till att [utveckla nödvändiga tekniska kunskaper](./suggested-skills.md).

> [!div class="nextstepaction"]
> [Skapa tekniska kunskaper](./suggested-skills.md)
