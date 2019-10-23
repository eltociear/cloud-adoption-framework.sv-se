---
title: Molnövervakningsguide
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Översikt över Azure Monitor och System Center Operations Manager
author: MGoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: e816420e99bfb712db3ad8064b4c077df3edfcee
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548186"
---
# <a name="cloud-monitoring-guide-introduction"></a>Molnövervakningsguide: Introduktion

Molnet innebär en stor förändring när det gäller hur företag förvärvar och använder teknikresurser. Tidigare ägde och ansvarade företagen för alla tekniknivåer, från infrastruktur till programvara. Nu gör molnet att företag kan etablera och förbruka resurser efter behov.

Molnet erbjuder nästan obegränsad flexibilitet när det gäller utformningsalternativ, men företagen efterfrågar ofta beprövade och enhetliga metoder vid övergången till molntekniker. Alla företag har olika mål och tidslinjer för molnimplementeringen, vilket gör det i stort sett omöjligt att ha en enhetlig implementeringsmodell som passar alla.

![Diagram med strategier för molnanvändning](./media/monitoring-management-guidance-cloud-and-on-premises/introduction-cloud-adoption.png)

Den här digitala omvandlingen gör det även möjligt att modernisera infrastruktur, arbetsbelastningar och program. Beroende på affärsstrategi och mål är en hybridmolnmodell en sannolik del av migreringsresan från lokalt till helt fungerande i molnet. Under den här resan är IT-teamets utmaning att snabbt realisera ett värde ur molnanvändningen. IT-teamet måste dessutom lära sig att effektivt övervaka de appar och tjänster som migreras till Azure och fortsätta att leverera en effektiv IT-drift/DevOps.

Intressenter vill kunna använda molnbaserade, SaaS-verktyg (programvara som en tjänst) för övervakning och hantering. De måste förstå vad våra tjänster och lösningar levererar för att kunna få en heltäckande insyn, minska kostnaderna och fokusera mindre på infrastruktur och underhåll av traditionella programvarubaserade IT-verktyg.

IT-teamet föredrar dock ofta att använda verktyg som det redan gjorts betydande investeringar i. I de här verktygen kan IT övervaka processer i båda molnmiljöerna, även om målet är att gå över till en SaaS-baserad drift. Det här valet beror inte bara på att det tar tid att planera resurser och finansiering för att byta. Det beror också på en viss förvirring kring vilka produkter eller Azure-tjänster som är lämpliga att använda under övergången.

Målet med den här guiden är att vara en detaljerad referens som hjälper företagets IT-chefer, affärsbeslutsfattare, arkitekter och apputvecklare att förstå följande:

* Azures övervakningsplattformar med en översikt över och jämförelse av deras funktioner.
* Bästa möjliga lösning för övervakning av hybridbaserade, privata och Azure-interna arbetsbelastningar.
* Rekommenderad övervakningsmetod både för infrastrukturer och appar som helhet, från slutpunkt till slutpunkt. I det här ingår distributionsbara lösningar för sådana vanliga arbetsbelastningar som migreras till Azure.

Den här guiden är inte en instruktionsguide för att använda eller konfigurera enskilda tjänster och lösningar i Azure, men vi refererar till sådana källor när de är tillgängliga eller lämpliga att använda. När du har läst den här guiden kommer du att förstå hur du framgångsrikt kör en arbetsbelastning enligt rekommenderade metoder och mönster.

Om du inte är bekant med Azure Monitor och System Center Operations Manager och vill få en bättre förståelse om vad som gör dem unika och hur de fungerar jämfört med varandra kan du läsa [Översikten över våra övervakningsplattformar](./platform-overview.md).

## <a name="audience"></a>Målgrupp

Guiden är särskilt användbar för företagsadministratörer, IT-driftteamet, ansvariga för IT-säkerhet och efterlevnad, apparkitekter, ansvariga för arbetsbelastningsutveckling och arbetsbelastningsåtgärder.

## <a name="how-this-guide-is-structured"></a>Guidens struktur

Den här artikeln ingår i en serie. Följande artiklar är avsedda att läsas tillsammans, i följande ordning:

* Introduktion (den här artikeln)
* [Övervakningsstrategi för molndistributionsmodeller](./cloud-models-monitor-overview.md)
* [Samla in rätt data](./data-collection.md)
* [Aviseringar](./alerting.md)

## <a name="products-and-services"></a>Produkter och tjänster

Ett urval av programvara och tjänster är tillgängliga för att övervaka och hantera en mängd olika resurser i Azure, företagets nätverk eller andra molnleverantörer. De är:

* System Center Operations Manager
* Azure Monitor, som nu innehåller Log Analytics och Application Insights
* Azure Policy och Azure Blueprints
* Azure Automation
* Azure Logic Apps
* Azure Event Hubs

Den första versionen av guiden omfattar våra aktuella övervakningsplattformar – Azure Monitor och System Center Operations Manager – och ger en översikt över vår rekommenderade strategi för övervakning av molndistributionsmodellerna. Även den första uppsättningen övervakningsrekommendationer ingår, med bland annat datainsamling och avisering.

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Övervakningsstrategi för molndistributionsmodeller](./cloud-models-monitor-overview.md)
