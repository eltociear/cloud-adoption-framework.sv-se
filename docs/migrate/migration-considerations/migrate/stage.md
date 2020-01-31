---
title: Förstå mellanlagringsaktiviteter under en migrering
description: Förstå mellanlagringsaktiviteter under en migrering
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: c8dcc71cd47253bbc59e885a085802d78323c5fd
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76801995"
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
