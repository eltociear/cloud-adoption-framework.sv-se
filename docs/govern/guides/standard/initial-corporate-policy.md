---
title: 'Standard styrnings guide för företag: Första företags principen bakom styrnings strategin'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Standard styrnings guide för företag: Första företags principen bakom styrnings strategin'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 5e269e623f22fa976f85c75c130ef0b19e4e9620
ms.sourcegitcommit: 945198179ec215fb264e6270369d561cb146d548
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/04/2019
ms.locfileid: "71967537"
---
# <a name="standard-enterprise-governance-guide-initial-corporate-policy-behind-the-governance-strategy"></a>Standard styrnings guide för företag: Första företags principen bakom styrnings strategin

Följande företags policy definierar en inledande styrnings position, som är start punkten för den här guiden. Den här artikeln definierar tidiga risker, inledande princip-instruktioner och tidiga processer för att genomdriva princip satser.

> [!NOTE]
>Företags principen är inte ett tekniskt dokument, men det ger många tekniska beslut. Styrnings MVP: en som beskrivs i [översikten](./index.md) i slut änden härleds från den här principen. Innan du implementerar en styrnings MVP bör din organisation utveckla en företags policy utifrån dina egna mål och affärs risker.

## <a name="cloud-governance-team"></a>Team för moln styrning

I den här berättelsen består gruppen moln styrning av två system administratörer som har identifierat behovet av styrning. Under de kommande månaderna kommer de att ärva jobbet för att rensa ut styrningen av företagets moln närvaro, som ger dem titeln för _Cloud förmyndare komponenter_. I efterföljande iterationer kommer den här rubriken förmodligen att ändras.

[!INCLUDE [business-risk](../../../../includes/business-risks.md)]

## <a name="tolerance-indicators"></a>Tolerans indikatorer

Den aktuella toleransen för risk är hög och riskbenägenhet för investeringar i moln styrning är låg. Därför fungerar tolerans indikatorerna som ett tidig varnings system för att utlösa mer tid och energi. Om och när följande indikatorer observeras bör du iterativt förbättra styrnings strategin.

- **Cost Management:** Distributions skalan överskrider förinställda gränser för antalet resurser eller månads kostnaden.
- **Säkerhets bas linje:** Inkludering av skyddade data i definierade moln införande planer.
- **Resurs konsekvens:** Inkludering av alla verksamhets kritiska program i definierade moln implementerings planer.

[!INCLUDE [policy-statements](../../../../includes/policy-statements.md)]

## <a name="next-steps"></a>Nästa steg

Den här företags policyn förbereder moln styrnings teamet för att implementera styrnings-MVP, som är grunden för införande. Nästa steg är att implementera denna MVP.

> [!div class="nextstepaction"]
> [Vägledning förklaring](./prescriptive-guidance.md)
