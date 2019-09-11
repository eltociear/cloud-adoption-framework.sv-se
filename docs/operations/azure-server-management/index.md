---
title: Översikt över Azures serverhanteringstjänster
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introduktion till Azures serverhanteringstjänster
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 4d1ada9d47e54f4b0d3828ce93b2d55f3eda8a34
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817221"
---
# <a name="overview-of-azure-server-management-services"></a>Översikt över Azures serverhanteringstjänster

Azures serverhanteringstjänster ger kunderna konsekventa funktioner som gör att de kan hantera sina servrar i stor skala. Tjänsterna omfattar både Linux- och Windows-operativsystemen och kan användas i produktion, utveckling och testmiljöer. Dessutom har de stöd för virtuella Azure IaaS-datorer, fysiska servrar och virtuella datorer som antingen körs lokalt eller i andra värdmiljöer. 

I diagrammet nedan ser du några av Azure-tjänsterna för serverhantering. 

![Diagram över Azure-driftsmodellen](./media/operations-diagram.png)

Riktlinjerna i det här avsnittet av Microsoft Cloud Adoption Framework är bra exempel på hur du kan distribuera serverhanteringstjänster i din miljö. Syftet med den här planen är att ge en snabb orientering kring tjänsterna, och att guida dig genom en inkrementell uppsättning hanteringssteg för alla miljöer oavsett storlek.

För enkelhetens skull har vi kategoriserat den här vägledningen i tre steg:

![De tre stegen för att komma igång med Azures programsvit för serverhantering](./media/operations-stages.png)

<!-- markdownlint-disable MD026 -->

## <a name="why-use-azure-management-services"></a>Varför ska man använda Azures hanteringstjänster?

Azures hanteringstjänster erbjuder följande fördelar:

- **Azure-internt.** Hanteringstjänsterna är inbyggda och integrerade i Azure Resource Manager. De förbättras ständigt med nya funktioner.
- **Windows och Linux**. Hanteringen sköts likadant på Windows- och Linux-datorer.
- **Hybrid.** Hanteringstjänsterna omfattar såväl virtuella Azure IaaS-datorer som fysiska och virtuella servrar som körs lokalt eller i andra värdmiljöer.
- **Säkerhet.** Microsoft ägnar stora resurser åt alla former av säkerhet. Den här investeringen skyddar inte bara Azure molninfrastrukturen, utan även den resulterande tekniken och expertisen när det gäller att skydda kundernas resurser oavsett var de finns.

## <a name="next-steps"></a>Nästa steg

Bekanta dig med de [verktyg och tjänster och den planering](./prerequisites.md) som krävs för att börja använda Azures programsvit för serverhantering.

> [!div class="nextstepaction"]
> [Verktyg och planering som krävs](./prerequisites.md)
