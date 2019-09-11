---
title: Metodtips för Azure-beredskap
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introduktion till metodtips för Azure-beredskap
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: f1d4423e230d2eeff524a864f163e0cb13dc065b
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818275"
---
# <a name="best-practices-for-azure-readiness"></a>Metodtips för Azure-beredskap

En stor del av molnberedskapen handlar om att förse personalen med de tekniska kunskaper som krävs för att påbörja en molnimplementering och förbereda din migreringsmålmiljö för de tillgångar och arbetsbelastningar som du ska flytta till molnet. Följande avsnitt innehåller metodtips och ytterligare vägledning som hjälper din grupp att upprätta och förbereda Azure-miljön.

## <a name="azure-fundamentals"></a>Grunderna i Azure

Använd följande riktlinjer när du ordnar och distribuerar dina tillgångar i Azure-miljön:

- [Grundläggande koncept för Azure](../considerations/fundamental-concepts.md). Läs om grundläggande koncept och termer som används i Azure. Lär dig också hur dessa koncept är relaterade till varandra.
- [Rekommenderade regler för namngivning och etiketter](../considerations/name-and-tag.md). Läs detaljerade rekommendationer för att namnge och märka upp dina resurser. De här rekommendationerna är lämpliga när företag flyttar till molnet.
- [Skalning med flera Azure-prenumerationer](../considerations/scaling-subscriptions.md). Förstå strategier för skalning med flera Azure-prenumerationer.
- [Organisera dina resurser i Azure-hanteringsgrupper](https://docs.microsoft.com/azure/governance/management-groups/?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Lär dig hur Azure-hanteringsgrupper kan hantera resurser, roller, principer och distribution över flera prenumerationer.
- [Skapa konsekventa hybridmoln](../../infrastructure/misc/hybrid-consistency.md). Skapa hybridmolnlösningar som tillhandahåller fördelarna med molnskapande samtidigt som många av fördelarna med lokal hantering bibehålls.

## <a name="networking"></a>Nätverk

Använd följande riktlinjer när du ska förbereda din molnnätverksinfrastruktur för dina arbetsbelastningar:

- [Nätverksbeslut](../considerations/network-decisions.md). Välj de nätverkstjänster, verktyg och arkitekturer som stöder för krav som din organisations arbetsbelastning, styrning och anslutningskrav.
- [Planering av virtuella nätverk](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Lär dig att planera virtuella datornätverk som baseras på dina krav på isolering, anslutningar och plats.
- [Metodtips för nätverkssäkerhet](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Läs om metodtips för att hantera vanliga säkerhetsproblem i nätverk med inbyggda Azure-funktioner.
- [Perimeternätverk](./perimeter-networks.md). Perimeternätverk, som även kallas för DMZ:er, ger säkra anslutningar mellan dina molnnätverk och lokala eller fysiska datacenternätverk, tillsammans med någon anslutning till och från internet.
- [Nätverkstopologi med nav och ekrar](./hub-spoke-network-topology.md). Nav och ekrar är en nätverksmodell för effektiv hantering av vanlig kommunikation och säkerhetskrav för komplicerade arbetsbelastningar. Dessutom hanteras potentiella begränsningar för Azure-prenumerationer.

## <a name="identity-and-access-control"></a>Identitets- och åtkomstkontroll

Använd följande riktlinjer när du utformar din infrastruktur för identiteter och åtkomstkontroll för att öka effektiviteten i säkerheten för och hanteringen av dina arbetsbelastningar:

- [Metodtips för identitetshantering och åtkomstkontroll i Azure](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Lär dig metodtips för identitetshantering och åtkomstkontroll med hjälp av inbyggda Azure-funktioner.
- [Metodtips för rollbaserad åtkomstkontroll](./roles.md). Azures rollbaserade åtkomstkontroll (RBAC) erbjuder detaljerad gruppbaserad åtkomsthantering för resurser som har organiserats efter användarroller.
- [Skydda privilegierad åtkomst för hybrid- och molndistributioner i Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Använd Azure Active Directory till att säkerställa att din organisations administrativa åtkomst och administratörskonton är säkra både i molnmiljön och lokalt.

## <a name="storage"></a>Storage

- [Riktlinjer för Azure Storage](../considerations/storage-guidance.md). Välj den Azure Storage-lösning som passar för ditt användningsfall.
- [Guide till Azure Storage-säkerhet](https://docs.microsoft.com/azure/storage/common/storage-security-guide?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Läs mer om säkerhetsfunktionerna i Azure Storage.

## <a name="databases"></a>Databaser

- [Välj rätt SQL Server-alternativ i Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Välj den PaaS- eller IaaS-lösning som stöder SQL Server-arbetsbelastningar på bästa sätt.
- [Metodtips för databassäkerhet](https://docs.microsoft.com/azure/security/azure-database-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Metodtips för databassäkerhet på Azure-plattformen.
- [Välj rätt datalager](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview). Att välja rätt datalager för dina behov är ett viktigt beslut. Det finns hundratals implementeringar att välja bland från SQL- och NoSQL-databaser. Datalager kategoriseras ofta genom hur de strukturerar data och vilka typer av åtgärder som de stöder. Den här artikeln beskriver flera av de vanligaste lagringsmodellerna.

## <a name="cost-management"></a>Kostnadshantering

- [Spåra kostnader för affärsenheter, miljöer och projekt](./track-costs.md). Läs om metodtips för att skapa rätt mekanismer för kostnadsspårning.
- [Optimera din molninvestering med Azure Cost Management](https://docs.microsoft.com/azure/cost-management/cost-mgt-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Implementera en strategi för kostnadshantering och lär dig mer om de verktyg som finns tillgängliga för att hantera kostnadsutmaningar.
- [Skapa och hantera budgetar](https://docs.microsoft.com/azure/cost-management/tutorial-acm-create-budgets?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Lär dig att skapa och hantera budgetar med Azure Cost Management.
- [Exportera kostnadsdata](https://docs.microsoft.com/azure/cost-management/tutorial-export-acm-data?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Lär dig att skapa och hantera exporterade data med Azure Cost Management.
- [Optimera kostnader baserat på rekommendationer](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Lär dig att identifiera underutnyttjade resurser och vidta åtgärder för att minska kostnaderna med Azure Cost Management och Azure Advisor.
- [Övervaka användning och utgifter med hjälp av kostnadsaviseringar](https://docs.microsoft.com/azure/cost-management/cost-mgt-alerts-monitor-usage-spending?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Lär dig att använda Cost Management-aviseringar när du övervakar din användning och dina utgifter i Azure.
