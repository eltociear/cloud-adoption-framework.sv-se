---
title: Standardguide för styrning av företag
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Standardguide för styrning av företag
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 82467948ae3141ef1f961ab07a503be485a1bc6f
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/11/2019
ms.locfileid: "70908463"
---
# <a name="standard-enterprise-governance-guide"></a>Standardguide för styrning av företag

## <a name="overview-of-best-practices"></a>Översikt över metodtips

Den här styrningsguiden följer ett fiktivt företag under de olika stegen för styrningsmognad. Den är baserad på verkliga kundupplevelser. De rekommenderade metoderna baseras på det fiktiva företagets begränsningar och behov.

Som en snabb startpunkt definierar den här översikten MVP-kraven (Minimum Viable Product) för styrning baserat på förebyggande vägledning. Den innehåller även länkar till några styrningsförbättringar som lägger till ytterligare rekommenderade metoder allt eftersom nya affärsrisker eller tekniska risker uppstår.

> [!WARNING]
> Denna MVP är en baslinjestartpunkt som baseras på en uppsättning antaganden. Även den här minimala uppsättningen med bästa praxis baseras på företagspolicyer som drivs av unika affärsrisker och risktoleranser. Om du vill se om dessa antaganden gäller dig kan du läsa den [längre berättelsen](./narrative.md) som efterföljer den här artikeln.

### <a name="governance-best-practices"></a>Metodtips för styrning

Dessa metodtips kan fungera som utgångspunkt för en snabb och konsekvent riskhantering i dina prenumerationer.

### <a name="resource-organization"></a>Resursorganisering

Följande diagram visar MVP-styrningshierarkin för att organisera resurser.

![Diagram över resursorganisering](../../../_images/governance/resource-organization.png)

Varje program bör distribueras i korrekt område i hierarkin för hanteringsgrupp, prenumeration och resursgrupp. Under distributionsplaneringen skapar teamet för molnstyrning nödvändiga noder i hierarkin för att stödja molnimplementeringsteamen.

1. En hanteringsgrupp för varje typ av miljö (såsom produktion, utveckling och testning).
2. Två prenumerationer, en för produktion och en annan för icke-produktion.
3. Lämpliga resursgrupper med RBAC tillämpad i dessa prenumerationer.
4. [Konsekvent terminologi](../../../ready/considerations/name-and-tag.md) ska tillämpas på varje nivå i den här grupperingshierarkin.

Här är ett exempel på hur det här mönstret används:

![Exempel på resursorganisering för ett medelstort företag](../../../_images/governance/mid-market-resource-organization.png)

Dessa mönster ger utrymme för tillväxt utan att göra hierarkin onödigt komplicerad.

[!INCLUDE [governance-of-resources](../../../../includes/caf-governance-of-resources.md)]

## <a name="iterative-governance-improvements"></a>Iterativa styrningsförbättringar

När denna MVP har distribuerats kan ytterligare styrningslager snabbt införlivas i miljön. Här följer några metoder för att förbättra MVP:n för att uppfylla specifika affärsbehov:

- [Säkerhetsbaslinje för skyddade data](./security-baseline-evolution.md)
- [Resurskonfigurationer för verksamhetskritiska program](./resource-consistency-evolution.md)
- [Kontroller för kostnadshantering](./cost-management-evolution.md)
- [Kontroller för utveckling med flera moln](./multicloud-evolution.md)

<!-- markdownlint-disable MD026 -->

## <a name="what-does-this-guidance-provide"></a>Vad får jag med den här vägledningen?

I MVP:n etableras metoder och verktyg från området [Distributionsacceleration](../../deployment-acceleration/index.md) för att snabbt tillämpa företagspolicy. I synnerhet använder MVP:n Azure Blueprints, Azure Policy och Azure-hanteringsgrupper för att tillämpa några grundläggande företagspolicyer, enligt definitionen i berättelsen för den här fiktiva företaget. Dessa företagsprinciper tillämpas med hjälp av Resource Manager-mallar och Azure-principer för att upprätta en liten baslinje för identitet och säkerhet.

![Exempel på en MVP för inkrementell styrnings](../../../_images/governance/governance-mvp.png)

## <a name="incremental-improvement-of-governance-practices"></a>Inkrementell förbättring av styrningsmetoder

Över tid används den här styrnings-MVP:n för att förbättra styrningsmetoderna. När implementeringen ökar så ökar även affärsriskerna. Olika områden i Cloud Adoption Framework-styrningsmodellen kommer att ändras för att hantera de riskerna. Senare artiklar i den här serien behandlar den inkrementella förbättring av företagspolicy som påverkar det fiktiva företaget. Förbättringarna sker över tre områden:

- Kostnadshantering, allt eftersom implementeringen ökar.
- Säkerhetsbaslinje, när skyddade data distribueras.
- Resurskonsekvens, när IT-avdelningen börjar stödja verksamhetskritiska arbetsbelastningar.

![Exempel på en MVP för inkrementell styrnings](../../../_images/governance/governance-evolution.png)

## <a name="next-steps"></a>Nästa steg

Nu när du är bekant med styrnings-MVP och har en uppfattning om vilka styrningsförbättringar som bör följas kan du läsa följande stödjande berättelse för att få ytterligare kontext.

> [!div class="nextstepaction"]
> [Läs den stödjande berättelsen](./narrative.md)
