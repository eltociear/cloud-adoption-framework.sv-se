---
title: Beslutsguide för programvarudefinierade nätverk
description: Använd Cloud Adoption Framework för Azure för att lära dig hur programvarudefinierade nätverk tillhandahåller centralt hanterade virtuella nätverk via programvara.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: a07130e8d7ac201f7519658ea84e3ff9df33ecbb
ms.sourcegitcommit: 25cd1b3f218d0644f911737a6d5fd259461b2458
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/24/2020
ms.locfileid: "80225742"
---
# <a name="software-defined-networking-decision-guide"></a>Beslutsguide för programvarudefinierade nätverk

Programvarudefinierade nätverk (SDN) är en nätverksarkitektur som utformats för att möjliggöra virtualiserade nätverksfunktioner som kan hanteras, konfigureras och ändras centralt via programvara. SDN gör det möjligt att skapa molnbaserade nätverk med hjälp av de virtualiserade motsvarigheterna till fysiska routrar, brandväggar och andra nätverksenheter som används i lokala nätverk. SDN är viktigt för att skapa säkra virtuella nätverk på offentliga molnplattformar såsom Azure.

## <a name="networking-decision-guide"></a>Beslutsguide för nätverk

![Nätverksalternativ ordnade från minst till mest komplext, inriktat med direktlänkar nedan](../../_images/decision-guides/decision-guide-software-defined-network.png)

Hoppa till: [Endast PaaS](./paas-only.md) | [Molnbaserat](./cloud-native.md) | [Moln-DMZ](./cloud-dmz.md) [Hybrid](./hybrid.md) | [Nav och eker-modell](./hub-spoke.md) | [Läs mer](#learn-more)

SDN har flera alternativ med olika typer av prissättning och komplexitet. Ovanstående upptäcktsguide innehåller en referens för att snabbt anpassa dessa alternativ så att de bäst passar specifika företag och teknikstrategier.

Brytpunkten i den här guiden beror på flera viktiga beslut som ditt team för molnstrategi har fattat innan beslut tas om nätverksarkitektur. Det viktigaste bland dessa är beslut som rör din [definition av digital egendom](../../digital-estate/index.md) och [prenumerationsdesign](../subscriptions/index.md) (vilket även kan kräva feedback från beslut som fattats gällande dina strategier för redovisning och globala marknader för moln).

Små distributioner i en enskild region med färre än 1 000 virtuella datorer är mindre benägna att påverkas avsevärt av den här brytpunkten. Däremot kan stora implementeringsprojekt med fler än 1 000 virtuella datorer, flera affärsenheter eller flera geopolitiska marknader påverkas avsevärt av ditt SDN-beslut och den här nyckelbrytpunkten.

## <a name="choose-the-right-virtual-networking-architectures"></a>Välja rätt arkitekturer för virtuella nätverk

Det här avsnittet utökar beslutsguiden för att hjälpa dig välja rätt arkitekturer för virtuella nätverk.

Det finns många sätt att implementera SDN-tekniker för att skapa molnbaserade virtuella nätverk. Hur du strukturerar de virtuella nätverk som används i migreringen och hur dessa nätverk interagerar med din befintliga IT-infrastruktur beror på en kombination av arbetsbelastningskraven och styrningskraven.

När du planerar vilken arkitektur för virtuella nätverk eller kombination av arkitektur som du vill välja vid planeringen av molnmigrering bör du överväga följande frågor för att avgöra vad so passar organisationen bäst:

| Fråga | Endast PaaS | Molnbaserat | DMZ i molnet | Hybrid | Nav och ekrar |
|-----|-----|-----|-----|-----|-----|
| Kommer din arbetsbelastning endast använda PaaS-tjänster och inte kräva nätverksfunktioner utöver dem som tillhandahålls av själva tjänsterna? | Ja | Inga | Inga | Inga | Inga |
| Kräver arbetsbelastningen integrering med lokala program? | Inga | Inga | Ja | Ja | Ja |
| Har du upprättat mogna säkerhetsprinciper och säkra anslutningar mellan dina lokala nätverk och molnbaserade nätverk? | Inga | Inga | Inga | Ja | Ja |
| Kräver arbetsbelastningen autentiseringstjänster som inte stöds via molnidentitetstjänster eller behöver du direkt åtkomst till lokala domänkontrollanter? | Inga | Inga | Inga | Ja | Ja |
| Kommer du att behöva distribuera och hantera många virtuella datorer och arbetsbelastningar? | Inga | Inga | Inga | Inga | Ja |
| Kommer du behöva tillhandahålla centraliserad hantering och lokal anslutning och samtidigt delegera kontroll av resurser till enskilda arbetsbelastningsteam? | Inga | Inga | Inga | Inga | Ja |

## <a name="virtual-networking-architectures"></a>Arkitekturer för virtuella nätverk

Lär dig mer om de primära programvarudefinierade nätverksarkitekturerna:

- **[Endast PaaS](./paas-only.md):** De flesta PaaS-produkter (plattform som en tjänst) stödjer en begränsad uppsättning inbyggda nätverksfunktioner och kräver kanske inte ett uttryckligt definierat programvarudefinierat nätverk för att stödja arbetsbelastningskrav.
- **[Molnbaserat](./cloud-native.md):** En molnbaserad arkitektur stöder molnbaserade arbetsbelastningar med hjälp av virtuella nätverk som bygger på molnplattformens standardmässiga programvarudefinierade nätverksfunktioner utan beroende av lokala eller andra externa resurser.
- **[Moln-DMZ](./cloud-dmz.md):** Stöder begränsad anslutning mellan dina lokala nätverk och molnbaserade nätverk. Skyddas genom implementeringen av en demilitariserad zon som strikt kontrollerar trafik mellan de två miljöerna.
- **[Hybrid](./hybrid.md):** Nätverksarkitekturen för hybridmoln gör att virtuella nätverk i betrodda molnmiljöer kan komma åt dina lokala resurser och vice versa.
- **[Nav och ekrar](./hub-spoke.md):** Med nav och ekrar-arkitekturen kan du centralt hantera externa anslutningar och delade tjänster, isolera enskilda arbetsbelastningar och lösa potentiella prenumerationsbegränsningar.

## <a name="learn-more"></a>Läs mer

Mer information om programvarudefinierade nätverk i Azure finns här:

- [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview). I Azure tillhandahålls den grundläggande SDN-funktionen av Azure Virtual Network, som fungerar som en molnbaserad motsvarighet till fysiska lokala nätverk. Virtuella nätverk kan även fungera som en standardmässig isoleringsgräns mellan resurser på plattformen.
- [Metodtips för nätverkssäkerhet med Azure](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices). Rekommendationer från Azure Security-teamet om hur du konfigurerar virtuella nätverk för att minimera säkerhetsrisker.

## <a name="next-steps"></a>Nästa steg

Programvarudefinierade nätverk är bara en av huvudkomponenterna för infrastruktur som kräver arkitektoniska beslut under en process för att implementera moln. Gå till [översikten över beslutsguider](../index.md) om vill veta mer om alternativa mönster eller modeller som används vid utformningsbeslut för andra typer av infrastrukturer.

> [!div class="nextstepaction"]
> [Beslutsguider för arkitektur](../index.md)
