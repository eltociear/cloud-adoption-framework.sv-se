---
title: Styrningsguide för komplexa företag
description: Styrningsguide för komplexa företag
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 2485aa48a8af05fdf945f39523439743f30977c6
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76805752"
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

1. Definiera en hanteringsgrupp för varje affärsenhet med en detaljerad hierarki som återspeglar det geografiska området först och sedan miljötypen (till exempel produktionsmiljö eller icke-produktionsmiljö).
2. Skapa en prenumeration för produktionsmiljön och en som inte är avsedd för produktionsmiljön för varje unik kombination med en diskret affärsenhet eller ett geografiskt område. Att skapa flera prenumerationer kräver noggrant övervägande. Mer information finns i guiden [Prenumerationsbeslut](../../../decision-guides/subscriptions/index.md).
3. Tillämpa [konsekvent terminologi](../../../ready/azure-best-practices/naming-and-tagging.md) på varje nivå i den här grupperingshierarkin.
4. Resursgrupper bör distribueras på ett sätt som tar hänsyn till innehållets livslängd. Resurser som utvecklas tillsammans, hanteras tillsammans och dras tillbaka tillsammans tillhör samma resursgrupp. Mer information om metodtips för att använda resursgrupper finns [här](../../../decision-guides/resource-consistency/index.md).
5. [Valet av region](../../../decision-guides/regions/index.md) är otroligt viktigt. Du måste se till att nätverk, övervakning och granskning är tillgängligt för redundans/återställning och att [nödvändiga SKU:er är tillgängliga i de önskade regionerna](https://azure.microsoft.com/global-infrastructure/services).

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

Nu när du är bekant med styrnings-MVP och de kommande styrningsändringarna kan du läsa den relaterade berättelsen för att få ytterligare sammanhang.

> [!div class="nextstepaction"]
> [Läs den stödjande berättelsen](./narrative.md)
