---
title: Standardguide för styrning av företag
description: Följ ett fiktivt standardföretag genom olika styrningsstadier som definierar en MVP (minimum viable product) som bygger på regelverk.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 26aaf3285d5e68a5add2e91a213a6dfd29c1ca25
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434338"
---
# <a name="standard-enterprise-governance-guide"></a>Standardguide för styrning av företag

## <a name="overview-of-best-practices"></a>Översikt över metodtips

Den här styrningsguiden följer ett fiktivt företag under de olika stegen för styrningsmognad. Den är baserad på verkliga kundupplevelser. Metodtipsen är baserade på det fiktiva företagets begränsningar och behov.

Som en snabb startpunkt definierar den här översikten MVP-kraven (Minimum Viable Product) för styrning baserat på bästa praxis. Den innehåller även länkar till några styrningsförbättringar som lägger till ytterligare bästa praxis allt eftersom nya affärsrisker eller tekniska risker uppstår.

> [!WARNING]
> Denna MVP är en baslinjestartpunkt som baseras på en uppsättning antaganden. Även den här minimala uppsättningen med bästa praxis baseras på företagspolicyer som drivs av unika affärsrisker och risktoleranser. Om du vill se om dessa antaganden gäller dig kan du läsa den [längre berättelsen](./narrative.md) som efterföljer den här artikeln.

### <a name="governance-best-practices"></a>Metodtips för styrning

Dessa metodtips kan fungera som utgångspunkt för en snabb och konsekvent riskhantering i dina prenumerationer.

### <a name="resource-organization"></a>Resursorganisering

Följande diagram visar MVP-styrningshierarkin för att organisera resurser.

![Diagram över resursorganisering](../../../_images/govern/resource-organization.png)

Varje program bör distribueras i korrekt område i hierarkin för hanteringsgrupp, prenumeration och resursgrupp. Under distributionsplaneringen skapar teamet för molnstyrning nödvändiga noder i hierarkin för att stödja molnimplementeringsteamen.

1. En hanteringsgrupp för varje typ av miljö (såsom produktion, utveckling och testning).
2. Två prenumerationer, en för produktionsarbetsbelastningar och en annan för icke-produktionsarbetsbelastningar.
3. [Konsekvent terminologi](../../../ready/azure-best-practices/naming-and-tagging.md) ska tillämpas på varje nivå i den här grupperingshierarkin.
4. Resursgrupper bör distribueras på ett sätt som tar hänsyn till innehållets livslängd: allt som utvecklas tillsammans hanteras tillsammans och dras tillbaka tillsammans. Mer information om metodtips för resursgrupper finns [här](../../../decision-guides/resource-consistency/index.md).
5. [Valet av region](../../../migrate/azure-best-practices/multiple-regions.md) är otroligt viktigt. Du måste se till att nätverk, övervakning och granskning är tillgängligt för redundans/återställning och att [nödvändiga SKU:er är tillgängliga i de önskade regionerna](https://azure.microsoft.com/global-infrastructure/services).

Här är ett exempel på hur det här mönstret används:

![Exempel på resursorganisering för ett medelstort företag](../../../_images/govern/mid-market-resource-organization.png)

Dessa mönster ger utrymme för tillväxt utan att göra hierarkin onödigt komplicerad.

[!INCLUDE [governance-of-resources](../../../../includes/caf-governance-of-resources.md)]

## <a name="iterative-governance-improvements"></a>Iterativa styrningsförbättringar

När denna MVP har distribuerats kan ytterligare styrningslager snabbt införlivas i miljön. Här följer några metoder för att förbättra MVP:n för att uppfylla specifika affärsbehov:

- [Säkerhetsbaslinje för skyddade data](./security-baseline-improvement.md)
- [Resurskonfigurationer för verksamhetskritiska program](./resource-consistency-improvement.md)
- [Kontroller för kostnadshantering](./cost-management-improvement.md)
- [Kontroller för utveckling med flera moln](./multicloud-improvement.md)

<!-- markdownlint-disable MD026 -->

## <a name="what-does-this-guidance-provide"></a>Vad får jag med den här vägledningen?

I MVP:n etableras metoder och verktyg från området [Distributionsacceleration](../../deployment-acceleration/index.md) för att snabbt tillämpa företagspolicy. I synnerhet använder MVP:n Azure Blueprints, Azure Policy och Azure-hanteringsgrupper för att tillämpa några grundläggande företagspolicyer, enligt definitionen i berättelsen för den här fiktiva företaget. Dessa företagsprinciper tillämpas med hjälp av Resource Manager-mallar och Azure-principer för att upprätta en liten baslinje för identitet och säkerhet.

![Exempel på en MVP för inkrementell styrnings](../../../_images/govern/governance-mvp.png)

## <a name="incremental-improvement-of-governance-practices"></a>Inkrementell förbättring av styrningsmetoder

Över tid används den här styrnings-MVP:n för att förbättra styrningsmetoderna. När implementeringen ökar så ökar även affärsriskerna. Olika områden i Cloud Adoption Framework-styrningsmodellen kommer att ändras för att hantera de riskerna. Senare artiklar i den här serien behandlar den inkrementella förbättring av företagspolicy som påverkar det fiktiva företaget. Förbättringarna sker över tre områden:

- Kostnadshantering, allt eftersom implementeringen ökar.
- Säkerhetsbaslinje, när skyddade data distribueras.
- Resurskonsekvens, när IT-avdelningen börjar stödja verksamhetskritiska arbetsbelastningar.

![Exempel på en MVP för inkrementell styrnings](../../../_images/govern/governance-improvement.png)

## <a name="next-steps"></a>Nästa steg

Nu när du är bekant med styrnings-MVP och har en uppfattning om vilka styrningsförbättringar du bör göra kan du läsa den relaterade berättelsen för att få ytterligare sammanhang.

> [!div class="nextstepaction"]
> [Läs den stödjande berättelsen](./narrative.md)
