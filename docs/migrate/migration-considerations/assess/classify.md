---
title: Arbets belastnings klassificering före migrering
description: Klassificera dina arbets belastningar under en utvärdering av för migrering.
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 2378c3ba3e17a9c1408a07c65129dc853a83d8b2
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80432841"
---
# <a name="workload-classification-before-migration"></a>Arbets belastnings klassificering före migrering

Under varje iteration av migreringsprocessen migreras en eller flera arbets belastningar och befordras till produktion. Före någon av dessa migrerings aktiviteter är det viktigt att klassificera varje arbets belastning. Klassificeringen hjälper till att klargöra styrnings-, säkerhets-, drift-och data hanterings krav.

Följande vägledning bygger på de föreslagna taggnings kraven som beskrivs i [artikeln namnge och tagga standarder](../../../ready/azure-best-practices/naming-and-tagging.md#metadata-tags) genom att lägga till viktiga [funktioner](../../../manage/considerations/criticality.md#criticality-scale) och [styrnings](../../../govern/guides/complex/prescriptive-guidance.md#resource-tagging) element.

I den här artikeln föreslår vi särskilt att du lägger till allvarlighets grad och data känslighet i dina befintliga märknings standarder. Var och en av dessa data punkter hjälper andra team att förstå vilka arbets belastningar som kan kräva ytterligare uppmärksamhet eller support.

## <a name="data-sensitivity"></a>Data känslighet

Som beskrivs i artikeln om [data klassificering](../../../govern/policy-compliance/data-classification.md), mäter data klassificeringen den effekt som en data läcka har på företaget eller kunderna. Styrnings-och säkerhets teamen utnyttjar data känslighet eller data klassificering som en indikator för säkerhets risker. Under utvärderingen bör moln implementerings teamet utvärdera data klassificeringen för varje arbets belastning som är avsedd för migrering och dela denna klassificering med stöd team. Arbets belastningar som hanterar strikta offentliga data kanske inte påverkar support teamen. Men eftersom data flyttas vidare till "hög konfidentiell"-delen av spektrumet, kommer både styrnings-och säkerhets team att ha en fördelad andel som deltar i bedömningen av arbets belastningen.

Arbeta med dina säkerhets-och styrnings grupper så tidigt som möjligt för att definiera följande objekt:

- En tydlig process för att dela alla arbets belastningar i efter släpning med känsliga data.
- En förståelse för de styrnings krav och säkerhets bas linjer som krävs för olika nivåer av data känslighet.
- Eventuell påverkan på data känslighet kan ha på prenumerations design, hierarkier för hanterings grupper eller landnings zon krav.
- Eventuella krav för att testa data klassificeringen, som kan omfatta särskilda verktyg eller definierade klassificerings omfång.

## <a name="mission-criticality"></a>Verksamhets kritiskhet

Som beskrivs i artikeln om [belastnings kritiskan](../../../manage/considerations/criticality.md)är allvarlighets graden för en arbets belastning ett mått på hur betydligt verksamheten påverkas under ett avbrott. Den här data punkten hjälper drift hantering och säkerhets team att utvärdera risker avseende avbrott och överträdelser. Under utvärderingen bör moln implementerings teamet utvärdera uppdrags kritiskaheten för varje arbets belastning som är avsedd för migrering och dela denna klassificering med stöd team. "Låg" eller "ej stödda" arbets belastningar har troligen ingen effekt på stöd teamen. I takt med att arbets belastningar närmar sig klassificeringarna "verksamhets kritiska" eller "enhets kritiska" blir deras operativa beroenden tydligare.

Arbeta med dina säkerhets-och drift team så snart som möjligt för att definiera följande objekt:

- En tydlig process för att dela alla arbets belastningar i efter släpning med support krav.
- En förståelse för drift hanterings-och resurs konsekvens kraven för olika nivåer av allvarlighets grad.
- Eventuell påverkan på påverkan kan ha på prenumerations design, hierarkier för hanterings grupper eller landnings zon krav.
- Eventuella krav för att dokumentera kritiskhet, som kan omfatta särskilda trafik-eller användnings rapporter, finansiella analyser eller andra verktyg.

## <a name="next-steps"></a>Nästa steg

När arbets belastningarna klassificeras på rätt sätt är det mycket enklare att [Justera affärs prioriteringarna](./business-priorities.md).

> [!div class="nextstepaction"]
> [Rikta in affärsprioriteringar](./business-priorities.md)
