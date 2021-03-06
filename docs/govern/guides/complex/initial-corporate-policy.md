---
title: 'Komplex företags styrning: ursprunglig företags policy'
description: Använd ramverket för moln införande för Azure för att definiera inledande styrnings position, tidiga risker, initiala princip satser och tidiga tvångs processer.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 327cbac3de0641b0fc4e8baf1c621dce7d5bc356
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434436"
---
# <a name="governance-guide-for-complex-enterprises-initial-corporate-policy-behind-the-governance-strategy"></a>Styrnings guide för komplexa företag: första företags principen bakom styrnings strategin

Följande företags policy definierar den inledande styrnings positionen, som är start punkten för den här guiden. Den här artikeln definierar tidiga risker, inledande princip-instruktioner och tidiga processer för att genomdriva princip satser.

> [!NOTE]
>Företags principen är inte ett tekniskt dokument, men det ger många tekniska beslut. Styrnings MVP: en som beskrivs i [översikten](./index.md) i slut änden härleds från den här principen. Innan du implementerar en styrnings MVP bör din organisation utveckla en företags policy utifrån dina egna mål och affärs risker.

## <a name="cloud-governance-team"></a>Team för moln styrning

INFORMATIONS gruppen hölls nyligen ett möte med IT-styrningen för att förstå historiken för personliga data och verksamhets kritiska principer och granska effekterna av att ändra dessa principer. INFORMATIONS gruppen diskuterade även den övergripande potentialen för molnet för IT och företaget.

Efter mötet har två medlemmar i IT-styrningen behörighet att undersöka och stödja moln planerings ansträngningar. Chefen för IT-styrningen har identifierat behovet av styrning och en möjlighet att begränsa skuggan IT-chef. Med detta föddes moln styrnings teamet. Under de kommande månaderna kommer de att ärva en rensning av många misstag som gjorts under utforskningen i molnet från ett styrnings perspektiv. Detta tar dem till moniker för _Cloud-förmyndare komponenter_. I senare iterationer visar den här guiden hur deras roller förändras över tid.

[!INCLUDE [business-risk](../../../../includes/business-risks.md)]

## <a name="tolerance-indicators"></a>Tolerans indikatorer

Den aktuella risk toleransen är hög och riskbenägenhet för investeringar i moln styrning är låg. Därför fungerar tolerans indikatorerna som ett tidig varnings system för att utlösa investeringen av tid och energi. Om följande indikatorer observeras är det klokt att gå över till styrnings strategin.

- **Cost Management:** Distributions skalan överskrider 1 000 till gångar till molnet, eller månads kostnaden överskrider $10 000 USD per månad.
- **Identitets bas linje:** Inkludering av program med äldre eller tredje parts Multi-Factor Authentication-krav.
- **Säkerhets bas linje:** Inkludering av skyddade data i definierade moln införande planer.
- **Resurs konsekvens:** Inkludering av alla verksamhets kritiska program i definierade moln implementerings planer.

[!INCLUDE [policy-statements](../../../../includes/policy-statements.md)]

## <a name="next-steps"></a>Nästa steg

Den här företags policyn förbereder moln styrnings teamet för att implementera styrnings-MVP, som är grunden för införande. Nästa steg är att implementera denna MVP.

> [!div class="nextstepaction"]
> [Metod tips förklaras](./prescriptive-guidance.md)
