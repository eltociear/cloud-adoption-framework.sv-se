---
title: 'Program varu definitions nätverk: hubb och eker'
description: Använd ramverket för moln införande för Azure för att lära dig hur hubb och eker-nätverk ordnar nätverks infrastrukturen i flera anslutna virtuella nätverk.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 9138a686aedd3ba54352280b557b6ac622df6a46
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77708588"
---
# <a name="software-defined-networking-hub-and-spoke"></a>Program varu definitions nätverk: hubb och eker

NAV-och eker-nätverks modellen organiserar din Azure-baserade moln nätverks infrastruktur i flera anslutna virtuella nätverk. Med den här modellen kan du effektivt hantera vanliga kommunikations-eller säkerhets krav och hantera potentiella prenumerations begränsningar.

I Hubbs-och eker-modellen är _hubben_ ett virtuellt nätverk som fungerar som en central plats för att hantera externa anslutningar och värd tjänster som används av flera arbets belastningar. _Ekrarna_ är virtuella nätverk som är värdar för arbets belastningar och ansluter till den centrala hubben via [peering av virtuella nätverk](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

All trafik som passerar in i eller ut ur arbets belastnings ekerns nätverk dirigeras via hubb nätverket där det kan dirigeras, inspekteras eller hanteras på annat sätt av centralt hanterade IT-regler eller processer.

Den här modellen syftar till att åtgärda följande problem:

- **Kostnads besparingar och hanterings effektivitet.** Att centralisera tjänster som kan delas av flera arbets belastningar, till exempel virtuella nätverks installationer (NVA) och DNS-servrar, på en och samma plats gör det möjligt för IT att minimera redundanta resurser och hanterings ansträngning över flera arbets belastningar.
- **Begränsningar för prenumerationer överkommer.** Stora molnbaserade arbets belastningar kan kräva användning av fler resurser än vad som tillåts inom en enda Azure-prenumeration (se [prenumerations gränser](https://docs.microsoft.com/azure/azure-subscription-service-limits)). Med peer-anslutning av arbetsbelastningar i virtuella nätverk från olika prenumerationer till en central hubb löser du dessa problem.
- **Separering av problem.** Möjlighet att distribuera enskilda arbets belastningar mellan centrala IT-team och arbets belastnings team.

I följande diagram visas ett exempel på hubb och eker-arkitektur, inklusive centralt hanterade hybrid anslutningar.

![Hubb och eker nätverks arkitektur](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/images/hub-spoke.png)

Hubben och eker-arkitekturen används ofta tillsammans med hybrid nätverks arkitekturen, vilket ger en centralt hanterad anslutning till din lokala miljö som delas mellan flera arbets belastningar. I det här scenariot passerar all trafik som överförs mellan arbets belastningarna och lokala platser genom hubben där den kan hanteras och skyddas.

## <a name="hub-and-spoke-assumptions"></a>Antaganden för nav och ekrar

Om du implementerar en hubb och eker-arkitektur för virtuella nätverk förutsätts följande:

- Moln distributionerna omfattar arbets belastningar som finns i separata arbets miljöer, till exempel utveckling, testning och produktion, som alla förlitar sig på en uppsättning vanliga tjänster, till exempel DNS-eller katalog tjänster.
- Dina arbets belastningar behöver inte kommunicera med varandra, men de har vanliga krav för extern kommunikation och delade tjänster.
- Arbets belastningarna kräver fler resurser än vad som är tillgängligt i en enda Azure-prenumeration.
- Du måste ange arbets belastnings team med delegerade hanterings rättigheter över sina egna resurser samtidigt som du behåller den centrala säkerhets kontrollen över extern anslutning.

## <a name="global-hub-and-spoke"></a>Global hubb och eker

Hubbs-och eker-arkitekturer implementeras ofta med virtuella nätverk som distribueras till samma Azure-region för att minimera svars tiden mellan nätverk. Stora organisationer med global räckvidd kan dock behöva distribuera arbets belastningar i flera regioner för tillgänglighet, haveri beredskap eller myndighets krav. NAV-och eker-modellen kan använda Azures [globala virtuella nätverk som peering](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) för att utöka centraliserad hantering och delade tjänster mellan regioner och stödja arbets belastningar som distribueras över hela världen.

## <a name="learn-more"></a>Läs mer

Exempel på hur du implementerar Hubbs-och eker-nätverk i Azure finns i följande exempel på webbplatsen för Azure Reference arkitekturer:

- [Implementera en nätverkstopologi för nav och ekrar i Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
- [Implementera en nätverkstopologi med nav och ekrar med delade tjänster i Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)
