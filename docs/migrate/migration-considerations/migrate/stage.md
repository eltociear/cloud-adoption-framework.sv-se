---
title: Mellanlagring av aktiviteter under en migrering
description: Använd ramverket för moln införande för Azure för att förstå mellanlagrings aktiviteter och associerade slut produkter som behövs vid en migrering.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: f6d45943ac8545083ce8d31215488b433a3ad00b
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80432465"
---
# <a name="understand-staging-activities-during-a-migration"></a>Förstå mellanlagringsaktiviteter under en migrering

Som det beskrivs i artikeln om upphöjningsmodeller är *mellanlagring* den punkt då tillgångarna har migrerats till molnet. De är dock ännu inte redo att upphöjas till produktion. Detta är ofta det sista steget i migreringsprocessen under en migrering. Efter mellanlagringen hanteras arbetsbelastningen av IT-avdelningen eller molndriftsteamet för att förbereda den för produktionsanvändning.

## <a name="deliverables"></a>Leverabler

Mellanlagrade tillgångar är kanske inte redo för användning i produktion. Det finns flera kontroller vad gäller produktionsberedskap som bör slutföras innan den här fasen kan anses vara färdig. Följande är en lista över leverabler som ofta associeras med slutförandet av tillgångsmellanlagring.

- **Automatiserad testning.** Alla automatiserade tester som är tillgängliga för validering av arbetsbelastningars prestanda bör köras innan mellanlagringsprocessen avslutas. När tillgångarna har lämnat mellanlagringen avslutas synkronisering med det ursprungliga källsystemet. Därför är det svårare att omdistribuera de replikerade tillgångarna efter att tillgångarna har mellanlagrats för optimering.
- **Migreringsdokumentation.** De flesta migreringsverktyg kan generera en automatiserad rapport över de tillgångar som migreras. Innan mellanlagringsaktiviteten avslutas bör alla migrerade tillgångar dokumenteras för tydlighetens skull.
- **Konfigurationsdokumentation.** Ändringar som görs i en tillgång (under reparation, replikering eller mellanlagring) bör dokumenteras för driftsberedskapens skull.
- **Dokumentation om kvarvarande uppgifter.** Kvarvarande uppgifter för migrering bör uppdateras så att de speglar arbetsbelastningen och mellanlagrade tillgångar.

## <a name="next-steps"></a>Nästa steg

När mellanlagrade tillgångar har testats och dokumenterats kan du gå vidare till [optimeringsaktiviteter](../optimize/index.md).

> [!div class="nextstepaction"]
> [Optimera migrerade arbetsbelastningar](../optimize/index.md)
