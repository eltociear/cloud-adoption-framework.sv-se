---
title: Benchmark-testa och ändra storlek på molntillgångar
description: Lär dig att mäta och optimera dina moln till gångar så att du kan hitta balansen mellan prestanda och kostnader.
author: BrianBlanchard
ms.author: brblanch
ms.date: 5/19/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b0b49d2785de8cee4c08395f6a2893436fd0aa9e
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092772"
---
# <a name="benchmark-and-resize-cloud-assets"></a>Benchmark-testa och ändra storlek på molntillgångar

Det är mycket viktigt att övervaka användning och utgifter för molninfrastrukturer. Organisationer betalar för de resurser de förbrukar över tid. När användningen överskrider avtalets trösklar kan det gå snabbt att få höga överförbrukningskostnader. Kostnadshanteringsrapporter hjälper till att övervaka utgifterna för att kunna analysera och följa molnanvändning, kostnader och trender. Med övertidsrapporter upptäcks avvikelser som skiljer sig från normala trender. Ineffektivitet i molnanvändning synliggörs i optimeringsrapporter. Se ineffektivitet i kostnadsanalysrapporterna.

I de traditionella IT-modellerna med lokala installationer är införskaffande av IT-system kostsamt och tidsödande. Processerna kräver ofta långdragna utvärderingsomgångar för kapitalutgifter och kan kräva en årlig planeringsprocess. Det är därför vanligt att köpa mer än vad som krävs. Det är också vanligt för IT-administratörer att tillhandahålla för mycket resurser för att förbereda för framtida behov.

I molnet eliminerar redovisnings- och etableringsmodellerna de tidsfördröjningar som leder till överköp. När en tillgång behöver ytterligare resurser kan den skalas upp eller ut nästan direkt. Detta innebär att tillgångar tryggt kan minskas i storlek för att minimera resurser och kostnader. Under benchmark-tester och optimering försöker teamet för molnimplementering att hitta balansen mellan prestanda och kostnader genom etablering av resurser så att de är av precis rätt storlek för att uppfylla produktionskraven.

<!-- markdownlint-disable MD026 -->

## <a name="should-assets-be-optimized-during-or-after-the-migration"></a>Ska tillgångar optimeras före eller efter migrering?

Ska tillgångar optimeras&mdash;före eller efter migrering? Det enkla svaret är *både* och. Men det är inte helt korrekt. För att förstå svaret tar vi två grundläggande scenarion för resursoptimering:

- **Planerad storleksförändring.** Ofta är en tillgång uppenbarligen för stor och underanvänd och bör storleksförändras under införandet. För att avgöra om en tillgång storleksförändrats korrekt i detta fall krävs användargodkännande efter migreringen. Om en avancerad användare inte upplever brister i prestanda eller funktionalitet under testning kan du dra slutsatsen att tillgången har rätt storlek.
- **Optimering.** I fall där behovet av optimering är oklart ska IT-team använda en datadriven metod för hantering av storleksförändring av resurser. Med hjälp av benchmarks för till gångens prestanda kan ett IT-team fatta sammanfattande beslut om lämplig storlek, tjänster, omfattning och arkitektur för en lösning. Sedan kan de storleksförändra och testa prestandateorier efter migreringen.

Använd underbyggda gissningar och experimentera med storleksförändring under migreringen. Verklig optimering av resurser kräver data baserat på verklig prestanda i en molnmiljö. För att genomföra en ordentlig optimering måste IT-teamet först implementera metoder för övervakning av prestanda och resursutnyttjande.

## <a name="benchmark-and-optimize-with-azure-cost-management"></a>Benchmark-testa och optimera med Azure Cost Management

[Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview) som licensierats av Cloudyn, ett dotterbolag till Microsoft, hanterar utgifter för molnet på ett transparent och korrekt sätt. Denna tjänst övervakar, benchmark-testar, tilldelar och optimerar molnkostnader.

Historiska data hjälper dig hantera kostnader genom att analysera användning och kostnader över tid för att identifiera trender som sedan används för att skapa prognoser för framtida utgifter. Cost Management innehåller även användbara rapporter för kostnadsprognoser. Kostnadsallokering hanterar kostnader genom att analysera kostnaderna baserat på taggningsprinciper. Använd kostnadsallokering för kostnadsrapporter/återbetalning för att visa resursanvändning och kopplade kostnader för att påverka förbrukningsbeteenden eller debitera klientkunder. Åtkomstkontroll hjälper till att hantera kostnader genom att se till att användare och team endast har åtkomst till de kostnadshanteringsdata som de behöver. Aviseringar kan hjälpa till att hantera kostnader genom automatiska meddelanden vid ovanliga utgifter eller för höga utgifter. Aviseringar kan även meddela andra intressenter automatiskt vid avvikelser i utgifter och risk för höga utgifter. Olika rapporter har stöd för aviseringar baserat på budget- och kostnadströsklar.

## <a name="improve-efficiency"></a>Förbättra effektiviteten

Bestäm optimal användning av virtuella datorer, identifiera virtuella datorer som inte används eller ta bort virtuella datorer som inte används och ej anslutna diskar med Cost Management. Med hjälp av informationen i rapporterna för storleksoptimering och ineffektivitet skapar du en plan för att minska storleken eller ta bort virtuella datorer som inte används.

## <a name="next-steps"></a>Nästa steg

När en arbetsbelastning testats och optimerats är det dags att [förbereda arbetsbelastningen för befordran](./ready.md).

> [!div class="nextstepaction"]
> [Förbereda en migrerad arbetsbelastning för produktionsanvändning](./ready.md)
