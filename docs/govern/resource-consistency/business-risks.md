---
title: Resurs konsekvens affärs risker
description: Använd ramverket för moln införande för Azure för att förstå typisk kund införande av en resurs konsekvens i en strategi för moln styrning.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3eff0f6130adc35d8c087d385d42b06e141f3c64
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433502"
---
# <a name="resource-consistency-motivations-and-business-risks"></a>Resultat av resurs konsekvens och affärs risker

Den här artikeln beskriver orsakerna till att kunderna vanligt vis antar en resurs konsekvens i en strategi för moln styrning. Det innehåller också några exempel på potentiella affärs risker som kan användas för att köra princip satser.

<!-- markdownlint-disable MD026 -->

## <a name="resource-consistency-relevancy"></a>Resurs konsekvens relevanta

När det gäller att distribuera resurser och arbets belastningar erbjuder molnet ökad flexibilitet och flexibilitet i de flesta traditionella lokala data Center. De här potentiella molnbaserade fördelarna är dock också kopplade till potentiella hanterings nack delar som allvarligt kan äventyra framgången av ditt moln. Vilka resurser har du distribuerat? Vilka team äger olika resurser? Har du tillräckligt med resurser som stöder en arbets belastning? Hur vet du om arbets belastningarna är felfria?

Resurs konsekvens är avgörande för att säkerställa att resurser distribueras, uppdateras och konfigureras konsekvent på ett repeterbart sätt och att avbrott i tjänsten minimeras och åtgärdas i så liten tid som möjligt.

Syftet med resurs konsekvensen är att identifiera och minska affärs riskerna som rör drifts aspekterna av moln distributionen. Resurs konsekvens omfattar övervakning av program, arbets belastningar och till gångens prestanda. Den innehåller också de uppgifter som krävs för att uppfylla skalnings kraven, tillhandahålla funktioner för haveri beredskap, minimera prestanda Serviceavtal (SLA) överträdelser, och förebyggande av dessa SLA-överträdelser via automatiserad reparation.

Inledande test distributioner kanske inte behöver mycket mer än att införa vissa markör namn och tagga standarder som stöd för dina resurs konsekvens behov. I takt med att ditt moln antas och du distribuerar mer komplicerade och verksamhets kritiska till gångar, ökar behovet av att investera i disciplinen för resurs konsekvens snabbt.

## <a name="business-risk"></a>Affärs risk

Ämnes gruppen för resurs konsekvens försöker hantera kärn drifts affärs risker. Arbeta med dina affärs-och IT-team för att identifiera dessa risker och övervaka var och en av dem efter relevans när du planerar för och implementerar dina moln distributioner.

Riskerna varierar mellan olika organisationer, men följande fungerar som vanliga risker som du kan använda som utgångs punkt för diskussioner i din moln styrnings grupp:

- **Onödig drifts kostnad.** Föråldrade eller oanvända resurser eller resurser som överetablerats under tider med låg efter frågan, Lägg till onödiga drifts kostnader.
- **Underetablerad resurser.** Resurser som upplever högre än förväntad efter frågan kan leda till avbrott i verksamheten eftersom moln resurser är överbelastade på begäran.
- **Hanterings ineffektivitet.** Brist på konsekvent namngivning och taggning av metadata som är kopplade till resurser kan leda till IT-personal där de inte kan hitta resurser för hanterings uppgifter eller identifiera ägarskaps-och redovisningsinformation som rör till gångar. Detta resulterar i en ineffektiv hantering av kostnader som kan öka kostnaderna och minska IT-svars tiden till avbrott i tjänsten eller andra drift problem.
- **Affärs avbrott.** Avbrott i tjänsten som resulterar i överträdelser av organisationens etablerade service nivå avtal (service avtal) kan leda till förlust av affärs-eller andra ekonomiska konsekvenser för ditt företag.

## <a name="next-steps"></a>Nästa steg

Använd [moln hanterings mal len](./template.md)för att dokumentera affärs risker som sannolikt kommer att introduceras av den aktuella moln implementerings planen.

När en förståelse av realistiska affärs risker har upprättats är nästa steg att dokumentera affärs toleransen för risker och indikatorer och viktiga mått för att övervaka den toleransen.

> [!div class="nextstepaction"]
> [Förstå indikatorer, mått och risk tolerans](./metrics-tolerance.md)
