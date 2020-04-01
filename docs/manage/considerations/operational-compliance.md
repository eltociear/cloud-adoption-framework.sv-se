---
title: Operationell kompatibilitet i moln hantering
description: Använd ramverket för moln införande för Azure för att lära dig hur du upprätthåller efterlevnaden av operativa åtaganden.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: e693ba20984c46a8eae4497220e75c01d64abcbb
ms.sourcegitcommit: da7ebd67a0ebf29361f093f00e10217b212a2eb2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/01/2020
ms.locfileid: "80527650"
---
# <a name="operational-compliance-in-cloud-management"></a>Operationell kompatibilitet i moln hantering

Operativa krav bygger på [inventerings-och Synlighets](./inventory.md)disciplin. Som det första åtgärds bara steget i moln hantering fokuserar denna disciplin på regelbunden granskning av telemetri och reparations åtgärder (både proaktiv och reaktiv reparation). Den här disciplinen är hörn för att upprätthålla balansen mellan säkerhet, styrning, prestanda och kostnad.

## <a name="components-of-operations-compliance"></a>Komponenter i Operations-kompatibilitet

Att upprätthålla efterlevnaden av operativa åtaganden kräver analys, automatisering och mänsklig reparation. Effektiva operativa krav kräver konsekvens i några kritiska processer:

- Resurskonsekvens
- Miljö konsekvens
- Konsekvens av resurs konfiguration
- Uppdatera konsekvens
- Reparations automatisering

### <a name="resource-consistency"></a>Resurskonsekvens

Det mest effektiva steget som ett moln hanterings team kan vidta mot operativa krav är att upprätta konsekvens i resurs organisation och taggning. När resurser är konsekvent organiserade och taggade blir alla andra operativa uppgifter enklare. Mer detaljerad information om resurs konsekvens finns i [styrnings fasen](../../govern/index.md) i livs cykeln för moln införande. De [inledande styrnings bas artiklarna](../../govern/initial-foundation.md) visar hur du börjar utveckla resurs konsekvens.

### <a name="environment-consistency"></a>Miljö konsekvens

Att etablera konsekventa miljöer, eller landnings zoner, är nästa viktiga steg för att följa operativa krav. När landnings zoner är konsekventa och tillämpas via automatiserade verktyg, är det betydligt mindre komplicerat att diagnostisera och lösa drift problem. Mer detaljerad information om miljö konsekvens finns i den [färdiga fasen](../../ready/index.md) i moln införande livs cykel. Övningarna i den här fasen hjälper till att bygga en upprepnings bar process för att definiera och förväntar sig en konsekvent, kod-första metod för utveckling av molnbaserade miljöer.

### <a name="resource-configuration-consistency"></a>Konsekvens av resurs konfiguration

I takt med att det bygger på styrning och beredskaps metoder bör moln hantering omfatta processer för pågående övervakning och utvärdering av efterlevnad av resurs konsekvens krav. När arbets belastningar ändras eller nya versioner antas är det viktigt att moln hanterings processer utvärderar eventuella konfigurations ändringar, vilket inte är enkelt reglerat genom automatisering.

När inkonsekvenser upptäcks åtgärdas vissa efter konsekvens i uppdateringar och andra kan åtgärdas automatiskt.

### <a name="update-consistency"></a>Uppdatera konsekvens

Stabilitet i tillvägagångs sättet kan leda till mer stabila åtgärder. Men vissa ändringar krävs i moln hanterings processer. I synnerhet är regelbundna korrigeringar och prestanda ändringar nödvändiga för att minska avbrott och kontrol lera kostnader.

Ett av de många värdena i en vuxen moln hanterings metod är att fokusera på att stabilisera och kontrol lera nödvändig förändring.

Alla moln hanterings bas linjer bör innehålla ett sätt att schemalägga, kontrol lera och eventuellt automatisera nödvändiga uppdateringar. Dessa uppdateringar bör omfatta minst en korrigering, men det kan också omfatta prestanda, storlek och andra aspekter av uppdaterings till gångar.

### <a name="remediation-automation"></a>Reparations automatisering

Som en förbättrad bas linje för moln hantering kan vissa arbets belastningar ha nytta av automatiserad reparation. När en arbets belastning ofta stöter på problem som inte kan lösas via kod eller arkitektoniska ändringar kan automatiserad reparation hjälpa till att minska belastningen på moln hantering och öka användarnas tillfredsställelse.

Många skulle att att alla problem som är tillräckligt stora för att automatisera ska lösas genom lösning av teknisk skuld. När en långsiktig lösning är försiktig bör det vara standard alternativet. Vissa affärs scenarier gör det dock svårt att motivera stora investeringar vid upplösningen av den tekniska skulden. När en sådan lösning inte kan motiveras, men reparation är en gemensam och kostsam börda, är automatiserad reparation nästa bästa lösning.

## <a name="next-steps"></a>Nästa steg

[Skydd och återställning](./protect.md) är följande områden som du bör tänka på i en moln hanterings bas linje.

> [!div class="nextstepaction"]
> [Skydda och återställa](./protect.md)
