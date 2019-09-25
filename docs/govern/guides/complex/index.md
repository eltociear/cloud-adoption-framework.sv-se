---
title: Styrningsguide för komplexa företag
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Styrningsguide för komplexa företag
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 63b66858c023ff85e1ff6f8adc811540f3034e2d
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025974"
---
# <a name="governance-guide-for-complex-enterprises"></a>Styrningsguide för komplexa företag

## <a name="overview-of-best-practices"></a>Översikt över metodtips

Den här styrningsguiden följer ett fiktivt företag under de olika stegen för styrningsmognad. Den är baserad på verkliga kundupplevelser. Föreslagen bästa praxis baseras på det fiktiva företagets begränsningar och behov.

Som en snabb startpunkt definierar den här översikten MVP-kraven (Minimum Viable Product) för styrning baserat på bästa praxis. Den innehåller även länkar till några styrningsförbättringar som lägger till ytterligare bästa praxis allt eftersom nya affärsrisker eller tekniska risker uppstår.

> [!WARNING]
> Denna MVP är en baslinjestartpunkt som baseras på en uppsättning antaganden. Även den här minimala uppsättningen med bästa praxis baseras på företagspolicyer som drivs av unika affärsrisker och risktoleranser. Om du vill se om dessa antaganden gäller dig kan du läsa den [längre berättelsen](./narrative.md) som efterföljer den här artikeln.

### <a name="governance-best-practices"></a>Metodtips för styrning

Dessa metodtips kan fungera som utgångspunkt för en snabb och konsekvent riskhantering i flera Azure-prenumerationer.

### <a name="resource-organization"></a>Resursorganisering

Följande diagram visar MVP-styrningshierarkin för att organisera resurser.

![Diagram över resursorganisering](../../../_images/govern/resource-organization.png)

Varje program bör distribueras i korrekt område i hierarkin för hanteringsgrupp, prenumeration och resursgrupp. Under distributionsplaneringen skapar teamet för molnstyrning nödvändiga noder i hierarkin för att stödja molnimplementeringsteamen.

1. Definiera en hanteringsgrupp för varje affärsenhet med en detaljerad hierarki som återspeglar geografi och sedan miljötyp (till exempel produktion eller icke-produktion).
1. Skapa en prenumeration för varje unik kombination av affärsenhet, geografi, miljö och ”programkategorisering”.
1. Skapa en separat resursgrupp för varje program.
1. Tillämpa [konsekvent terminologi](../../../ready/considerations/naming-and-tagging.md) på varje nivå i den här grupperingshierarkin.

![Diagram över resursorganisering för stort företag](../../../_images/govern/large-enterprise-resource-organization.png)

Dessa mönster ger utrymme för tillväxt utan att göra hierarkin onödigt komplicerad.

[!INCLUDE [governance-of-resources](../../../../includes/caf-governance-of-resources.md)]

<!-- See comments for suggestion to possibly add here -->

## <a name="incremental-governance-improvements"></a>Inkrementella styrningsförbättringar

När denna MVP har distribuerats kan ytterligare styrningslager snabbt införlivas i miljön. Här följer några metoder för att förbättra MVP:n för att uppfylla specifika affärsbehov:

- [Säkerhetsbaslinje för skyddade data](./security-baseline-improvement.md)
- [Resurskonfigurationer för verksamhetskritiska program](./resource-consistency-improvement.md)
- [Kontroller för kostnadshantering](./cost-management-improvement.md)
- [Kontroller för inkrementell förbättring med flera moln](./multicloud-improvement.md)

<!-- markdownlint-disable MD026 -->

## <a name="what-does-this-guidance-provide"></a>Vad får jag med den här vägledningen?

I MVP:n etableras metoder och verktyg från området [Distributionsacceleration](../../deployment-acceleration/index.md) för att snabbt tillämpa företagspolicy. I synnerhet använder MVP:n Azure Blueprints, Azure Policy och Azure-hanteringsgrupper för att tillämpa några grundläggande företagspolicyer, enligt definitionen i berättelsen för den här fiktiva företaget. Dessa företagsprinciper tillämpas med hjälp av Azure Resource Manager-mallar och Azure-principer för att upprätta en liten baslinje för identitet och säkerhet.

![Exempel på en MVP för inkrementell styrnings](../../../_images/govern/governance-mvp.png)

## <a name="incremental-improvements-to-governance-practices"></a>Inkrementell förbättring av styrningsmetoder

Över tid används den här styrnings-MVP:n för att inkrementellt förbättra styrningsmetoderna. När implementeringen ökar så ökar även affärsriskerna. Olika områden i Cloud Adoption Framework-styrningsmodellen kommer att anpassas för att hantera de riskerna. Senare artiklar i den här serien behandlar ändringarna av företagspolicy som påverkar det fiktiva företaget. Ändringarna gäller fyra områden:

- Identitetsbaslinje, när migreringsberoenden ändras i berättelsen.
- Kostnadshantering, allt eftersom implementeringen ökar.
- Säkerhetsbaslinje, när skyddade data distribueras.
- Resurskonsekvens, när IT-avdelningen börjar stödja verksamhetskritiska arbetsbelastningar.

![Exempel på en MVP för inkrementell styrnings](../../../_images/govern/governance-improvement-large.png)

## <a name="next-steps"></a>Nästa steg

Nu när du är bekant med styrnings-MVP och de kommande styrningsändringarna kan du läsa följande stödjande berättelse för att få ytterligare kontext.

> [!div class="nextstepaction"]
> [Läs den stödjande berättelsen](./narrative.md)