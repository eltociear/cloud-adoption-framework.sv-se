---
title: Operationell kompatibilitet – moln hantering och åtgärder
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Operationell kompatibilitet – moln hantering och åtgärder
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: bb6e4584da87d992f85b6ce90e21081c9c19d7c3
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72682534"
---
# <a name="operational-compliance-in-cloud-management"></a>Operationell kompatibilitet i moln hantering

Operativa krav bygger på [inventerings-och Synlighets](./inventory.md)disciplin, som det första åtgärds bara steget i moln hantering. Denna disciplin fokuserar på regelbunden granskning av telemetri och reparations åtgärder (både proaktiv och reaktiv reparation). Den här disciplinen är hörn för att upprätthålla balansen mellan säkerhet, styrning, prestanda och kostnad.

## <a name="components-of-operations-compliance"></a>Komponenter i Operations-kompatibilitet

Att upprätthålla efterlevnaden av operativa åtaganden kräver analys, automatisering och mänsklig reparation. Effektiva operativa krav kräver konsekvens i några kritiska processer:

1. Resurskonsekvens
2. Miljö konsekvens
3. Konsekvens av resurs konfiguration
4. Uppdatera konsekvens
5. Reparations automatisering

### <a name="resource-consistency"></a>Resurskonsekvens

Det mest effektiva steget som ett moln hanterings team kan vidta för att uppnå operativa krav är att upprätta konsekvens i resurs organisation och taggning. När resurser är konsekvent organiserade och taggade blir alla andra operativa uppgifter enklare. Mer detaljerad information om resurs konsekvens finns i [styrnings fasen](../../govern/index.md) i livs cykeln för moln införande. De [inledande styrnings bas artiklarna](../../govern/initial-foundation.md) demonstrerar exempel på sätt att börja utveckla resurs konsekvens.

### <a name="environment-consistency"></a>Miljö konsekvens

Konsekventa miljöer, eller landnings zoner, är nästa viktiga steg för att följa operativa krav. När landnings zoner är konsekventa och tillämpas via automatiserade verktyg, är det betydligt mindre komplicerat att diagnostisera och lösa drift problem. Mer detaljerad information om miljö konsekvens finns i den [färdiga fasen](../../ready/index.md) i moln införande livs cykel. Övningarna i den fasen upprättar en upprepnings bar process för att definiera och förväntar sig en konsekvent, kod-första metod för utveckling av molnbaserade miljöer.

### <a name="resource-configuration-consistency"></a>Konsekvens av resurs konfiguration

Utveckling av styrning och beredskaps metoder, moln hantering bör omfatta processer för pågående övervakning och utvärdering av efterlevnad av resurs konsekvens krav. När arbets belastningar ändras eller nya versioner antas är det viktigt att moln hanterings processer utvärderar eventuella konfigurations ändringar, vilket inte enkelt kan regleras via automatiserade medel.

När inkonsekvenser upptäcks åtgärdas vissa av konsekvens i uppdateringar och andra kan åtgärdas automatiskt.

### <a name="update-consistency"></a>Uppdatera konsekvens

Stabilitet kan leda till stabila åtgärder. Men vissa ändringar krävs i moln hanterings processer. I synnerhet är regelbundna korrigeringar och prestanda ändringar nödvändiga för att minska avbrott och kontrol lera kostnader.

Ett av de många värdena i en vuxen moln hanterings metod är att stabilisera och kontrol lera nödvändig förändring.

Alla moln hanterings bas linjer bör innehålla ett sätt att schemalägga, kontrol lera och eventuellt automatisera nödvändiga uppdateringar. Dessa uppdateringar bör omfatta minst en korrigering, men det kan också omfatta prestanda, storlek och andra aspekter av uppdaterings till gångar.

### <a name="remediation-automation"></a>Reparations automatisering

Som en förbättrad bas linje för moln hantering kan vissa arbets belastningar ha nytta av automatiserad reparation. När en arbets belastning ofta påträffar problem som inte kan lösas via kod eller arkitektoniska ändringar kan reparations automatisering minska belastningen på moln hantering och öka användarnas belåtenhet.

Många skulle att att alla problem, som är tillräckligt stora för att automatisera, ska lösas genom lösning av teknisk skuld. När långsiktig upplösning är försiktig bör det vara standard alternativet. Det finns dock ett antal affärs scenarier som gör det svårt att motivera stora investeringar för att lösa tekniska skulder. När teknisk återställnings lösning inte är motiverad, men reparation är en gemensam och kostsam börda, är den automatiserade reparationen nästa bästa lösning.

## <a name="next-steps"></a>Nästa steg

[Skydd och återställning](./protect.md) är följande områden som du bör tänka på i en moln hanterings bas linje.

> [!div class="nextstepaction"]
> [Skydda och återställa](./protect.md)
