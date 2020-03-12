---
title: Molnövervakningsguide
description: Läs om Azure Monitor, System Center Operations Manager och den rekommenderade strategin för övervakning av molndistributionsmodellerna.
author: MGoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 4303a51a1a6df47e07e22f3de87639230f4a4c71
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79091433"
---
# <a name="cloud-monitoring-guide-introduction"></a>Molnövervakningsguide: Introduktion

Molnet ändrar i grunden det sätt på vilket företag anskaffar och använder teknikresurser. Tidigare ägde och ansvarade företagen för alla tekniknivåer, från infrastruktur till programvara. Nu gör molnet att företag kan etablera och förbruka resurser efter behov.

Molnet ger nästan obegränsad flexibilitet när det gäller utformningsalternativ, men företagen efterfrågar ofta beprövade och enhetliga metoder vid övergången till molntekniker. Alla företag har olika mål och tidslinjer för molnimplementeringen, vilket gör det i stort sett omöjligt att ha en enhetlig implementeringsmodell som passar alla.

![Diagram med strategier för molnanvändning](./media/monitoring-management-guidance-cloud-and-on-premises/introduction-cloud-adoption.png)

Den här digitala omvandlingen gör det även möjligt att modernisera infrastruktur, arbetsbelastningar och program. Beroende på affärsstrategi och mål är en hybridmolnmodell en sannolik del av migreringsresan från lokalt till helt fungerande i molnet. Under den här resan är IT-teamets utmaning att snabbt realisera ett värde ur molnanvändningen. IT-teamet måste dessutom lära sig att effektivt övervaka de program och tjänster som migreras till Azure och fortsätta att leverera en effektiv IT-drift/DevOps.

Intressenter vill kunna använda molnbaserade, SaaS-verktyg (programvara som en tjänst) för övervakning och hantering. De måste förstå vad tjänster och lösningar levererar för att kunna få en heltäckande insyn, minska kostnaderna och fokusera mindre på infrastruktur och underhåll av traditionella programvarubaserade IT-verktyg.

IT-teamet föredrar dock ofta att använda verktyg som det redan gjorts betydande investeringar i. Med de här verktygen kan de övervaka processer i båda molnmiljöerna, även om målet är att gå över till en SaaS-baserad drift. IT-avdelningen föredrar detta, inte bara för att det tar tid, kräver planering, resurser och finansiering för att byta. Det beror också på en viss förvirring kring vilka produkter eller Azure-tjänster som är lämpliga att använda under övergången.

Målet med den här guiden är att vara en detaljerad referens som hjälper företagets IT-chefer, affärsbeslutsfattare, arkitekter och apputvecklare att förstå följande:

* Azures övervakningsplattformar med en översikt över och jämförelse av deras funktioner.
* Bästa möjliga lösning för övervakning av hybridbaserade, privata och Azure-interna arbetsbelastningar.
* Rekommenderad övervakningsmetod både för infrastrukturer och program, från slutpunkt till slutpunkt. I metoden ingår distribuerbara lösningar för att migrera sådana vanliga arbetsbelastningar till Azure.

Den här guiden är inte en vägledning för att använda eller konfigurera enskilda tjänster och lösningar i Azure, men den refererar till sådana källor när de är tillgängliga eller lämpliga att använda. När du har läst den kommer du att veta hur du framgångsrikt kör en arbetsbelastning enligt rekommenderade metoder och mönster.

Om du inte är bekant med Azure Monitor och System Center Operations Manager och vill få en bättre förståelse om vad som gör dem unika och hur de fungerar jämfört med varandra, kan du läsa [Översikt över våra övervakningsplattformar](./platform-overview.md).

## <a name="audience"></a>Målgrupp

Guiden är särskilt användbar för företagsadministratörer, IT-driftteam, ansvariga för IT-säkerhet och efterlevnad, programarkitekter, ansvariga för arbetsbelastningsutveckling och arbetsbelastningsåtgärder.

## <a name="how-this-guide-is-structured"></a>Guidens struktur

Den här artikeln ingår i en serie. Följande artiklar är avsedda att läsas tillsammans, i följande ordning:

* Introduktion (den här artikeln)
* [Övervakningsstrategi för molndistributionsmodeller](./cloud-models-monitor-overview.md)
* [Samla in rätt data](./data-collection.md)
* [Aviseringar](./alerting.md)

## <a name="products-and-services"></a>Produkter och tjänster

Det finns några program och tjänster som hjälper dig att övervaka och hantera olika resurser i Azure, företagets nätverk eller andra molnleverantörer. De är:

* System Center Operations Manager
* Azure Monitor, som nu innehåller Log Analytics och Application Insights
* Azure Policy och Azure Blueprints
* Azure Automation
* Azure Logic Apps
* Azure Event Hubs

Den första versionen av guiden beskriver våra nuvarande övervakningsplattformar: Azure Monitor och System Center Operations Manager. Den beskriver också vår rekommenderade strategi för övervakning av de olika molndistributionsmodellerna. Även den första uppsättningen övervakningsrekommendationer ingår, med bland annat datainsamling och avisering.

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Övervakningsstrategi för molndistributionsmodeller](./cloud-models-monitor-overview.md)
