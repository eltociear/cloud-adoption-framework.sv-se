---
title: Översikt över Azures serverhanteringstjänster
description: Introduktion till Azures serverhanteringstjänster
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: d83b84ca63043646591c4e2f5b3e5f82fc53c102
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808064"
---
# <a name="overview-of-azure-server-management-services"></a>Översikt över Azures serverhanteringstjänster

Azures serverhanteringstjänster ger konsekventa funktioner för att hantera servrar i stor skala. Dessa tjänster fungerar med både Linux- och Windows-operativsystem. De kan användas i produktions-, utvecklings- och testningsmiljöer. Serverhanteringstjänsterna har stöd för virtuella Azure IaaS-datorer, fysiska servrar och virtuella datorer som körs lokalt eller i andra värdmiljöer.

I diagrammet nedan ser du några av Azure-tjänsterna för serverhantering: ![Diagram över Azure-driftsmodellen](./media/operations-diagram.png)

Det här avsnittet av Microsoft Cloud Adoption Framework innehåller bra exempel på hur du kan distribuera serverhanteringstjänster i din miljö. Den här planen ger en snabb orientering kring tjänsterna och guidar dig genom en inkrementell uppsättning hanteringssteg för alla miljöer oavsett storlek.

För enkelhetens skull har vi kategoriserat den här vägledningen i tre steg:

![De tre stegen för att komma igång med Azures programsvit för serverhantering](./media/operations-stages.png)

<!-- markdownlint-disable MD026 -->

## <a name="why-use-azure-server-management-services"></a>Varför ska jag använda Azures serverhanteringstjänster?

Azures serverhanteringstjänster erbjuder följande fördelar:

- **Ingår i Azure:** Serverhanteringstjänsterna är inbyggda och integrerade i Azure Resource Manager. De förbättras ständigt med nya funktioner.
- **Windows och Linux:** Hanteringen sköts likadant på Windows- och Linux-datorer.
- **Hybrid:** Serverhanteringstjänsterna omfattar såväl virtuella Azure IaaS-datorer som fysiska och virtuella servrar som körs lokalt eller i andra värdmiljöer.
- **Säkerhet:** Microsoft ägnar stora resurser åt alla former av säkerhet. Den här investeringen skyddar inte bara Azure-infrastrukturen, utan även den resulterande tekniken och expertisen när det gäller att skydda kundernas resurser oavsett var de finns.

## <a name="next-steps"></a>Nästa steg

Bekanta dig med de [verktyg och tjänster och den planering](./prerequisites.md) som krävs för att börja använda Azures programsvit för serverhantering.

> [!div class="nextstepaction"]
> [Verktyg och planering som krävs](./prerequisites.md)
