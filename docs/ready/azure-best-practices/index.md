---
title: Metodtips för Azure-beredskap
description: Lär dig hur du tillhandahåller metodtips och ytterligare vägledning som hjälper din grupp att upprätta och förbereda Azure-miljön.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 8d44d3981824c9599151391cd3b7e3550ac31cd6
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79093573"
---
# <a name="best-practices-for-azure-readiness"></a>Metodtips för Azure-beredskap

En stor del av molnberedskapen handlar om att förse personalen med de tekniska kunskaper som krävs för att påbörja en molnimplementering och förbereda din migreringsmålmiljö för de tillgångar och arbetsbelastningar som du ska flytta till molnet. Läs dessa regelverk och ytterligare vägledning som hjälper din grupp att förbereda din Azure-miljö.

## <a name="azure-fundamentals"></a>Grunderna i Azure

Organisera och distribuera dina tillgångar i Azure-miljön.

- [Grundläggande koncept för Azure](../considerations/fundamental-concepts.md). Lär dig viktiga begrepp och termer som används i Azure samt hur begreppen är relaterade till varandra.
- [Rekommenderade regler för namngivning och etiketter](../azure-best-practices/naming-and-tagging.md). Läs detaljerade rekommendationer för att namnge och märka upp dina resurser. De här rekommendationerna är lämpliga när företag flyttar till molnet.
- [Skalning med flera Azure-prenumerationer](../azure-best-practices/scaling-subscriptions.md). Förstå strategier för skalning med flera Azure-prenumerationer.
- [Organisera dina resurser i Azure-hanteringsgrupper](https://docs.microsoft.com/azure/governance/management-groups/?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Lär dig hur Azure-hanteringsgrupper kan hantera resurser, roller, principer och distribution över flera prenumerationer.
- [Skapa konsekventa hybridmoln](../considerations/hybrid-consistency.md). Skapa hybridmolnlösningar som tillhandahåller fördelarna med molnskapande samtidigt som många av fördelarna med lokal hantering bibehålls.

## <a name="networking"></a>Nätverk

Förbered din molnnätverksinfrastruktur för dina arbetsbelastningar.

- [Nätverksbeslut](../considerations/networking-options.md). Välj de nätverkstjänster, verktyg och arkitekturer som stöder för krav som din organisations arbetsbelastning, styrning och anslutningskrav.
- [Planering av virtuella nätverk](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Planera virtuella datornätverk som baseras på dina krav på isolering, anslutningar och plats.
- [Metodtips för nätverkssäkerhet](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Läs om metodtips för att hantera vanliga säkerhetsproblem för nätverk med inbyggda Azure-funktioner.
- [Perimeternätverk](./perimeter-networks.md). Möjliggör säkra anslutningar mellan dina molnnätverk och lokala eller fysiska datacenternätverk, tillsammans med en anslutning till och från Internet.
- [Nätverkstopologi med nav och ekrar](./hub-spoke-network-topology.md). Hantera effektivt vanlig kommunikation eller säkerhetskrav för komplicerade arbetsbelastningar och hantera potentiella begränsningar med Azure-prenumerationer.

## <a name="identity-and-access-control"></a>Identitets- och åtkomstkontroll

Utforma din infrastruktur för identiteter och åtkomstkontroll för att öka effektiviteten i säkerheten för och hanteringen av dina arbetsbelastningar.

- [Metodtips för identitetshantering och åtkomstkontroll i Azure](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Lär dig metodtips för identitetshantering och åtkomstkontroll med hjälp av inbyggda Azure-funktioner.
- [Metodtips för rollbaserad åtkomstkontroll](../considerations/roles.md). Möjliggör detaljerad och gruppbaserad åtkomsthantering för resurser som har organiserats efter användarroller.
- [Skydda privilegierad åtkomst för hybrid- och molndistributioner i Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Säkerställ att din organisations administrativa åtkomst och behöriga konton är säkra i molnet och lokalt.

## <a name="storage"></a>Storage

- [Riktlinjer för Azure Storage](../considerations/storage-options.md). Välj den Azure Storage-lösning som passar för ditt användningsfall.
- [Guide till Azure Storage-säkerhet](https://docs.microsoft.com/azure/storage/blobs/security-recommendations?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Läs mer om säkerhetsfunktionerna i Azure Storage.

## <a name="databases"></a>Databaser

- [Välj rätt SQL Server-alternativ i Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Välj den PaaS- eller IaaS-lösning som stöder SQL Server-arbetsbelastningar på bästa sätt.
- [Metodtips för databassäkerhet](https://docs.microsoft.com/azure/security/azure-database-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Metodtips för databassäkerhet på Azure-plattformen.
- [Välj rätt datalager](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview). Välj rätt datalager för att uppfylla dina krav. Hundratals implementeringar är tillgängliga bland från SQL- och NoSQL-databaser. Datalager kategoriseras ofta genom hur de strukturerar data och vilka typer av åtgärder som de stöder. Den här artikeln beskriver flera vanliga lagringsmodeller.

## <a name="cost-management"></a>Kostnadshantering

- [Spåra kostnader för affärsenheter, miljöer och projekt](./track-costs.md). Läs om metodtips för att skapa rätt mekanismer för kostnadsspårning.
- [Optimera din molninvestering med Azure Cost Management](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Implementera en strategi för kostnadshantering och lär dig mer om de verktyg som finns tillgängliga för att hantera kostnadsutmaningar.
- [Skapa och hantera budgetar](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Lär dig att skapa och hantera budgetar med Azure Cost Management.
- [Exportera kostnadsdata](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-export-acm-data?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Lär dig att exportera kostnadsdata med Azure Cost Management.
- [Optimera kostnader baserat på rekommendationer](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Lär dig att identifiera underutnyttjade resurser och minska kostnaderna med Azure Cost Management och Azure Advisor.
- [Övervaka användning och utgifter med hjälp av kostnadsaviseringar](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Lär dig att använda Cost Management-aviseringar när du övervakar din användning och dina utgifter i Azure.
