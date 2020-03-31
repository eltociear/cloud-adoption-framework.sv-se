---
title: Granska dina nätverks alternativ
description: Använd ramverket för moln införande för Azure för att lära dig att identifiera de nätverksfunktioner som din landnings zon behöver för att stödja Azure-arbetsbelastningar.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 38a9476014b45f4230df6f76b1762249d8a988db
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433887"
---
<!-- cSpell:ignore paas NVAs VPNs -->

# <a name="review-your-network-options"></a>Granska dina nätverks alternativ

Att designa och implementera funktioner i Azure-nätverk är en viktig del av molnimplementeringen. Du måste fatta designbeslut för nätverket för att korrekt stödja arbetsbelastningar och tjänster som kommer att finnas i molnet. Azures nätverksprodukter och tjänster har stöd för många olika nätverksfunktioner. Strukturen för dessa tjänster och nätverksarkitekturen beror på organisationens arbetsbelastning, styrningen och behovet av anslutningar.

## <a name="identify-workload-networking-requirements"></a>Identifiera nätverkskrav för arbetsbelastning

Som del av utvärderingen och förberedelsen av landningszonen måste du identifiera de nätverksfunktioner som din landningszon måste ha stöd för. Processen förutsätter att du bedömer var och ett av de program och tjänster som utgör arbetsbelastningarna för att fastställa deras nätverksanslutningskrav. När du har identifierat och dokumenterat dessa krav kan du skapa principer för din landnings zon för att kontrollera tillåtna nätverksresurser och konfigurationer utifrån dina arbetsbelastningsbehov.

För varje program eller tjänst som du distribuerar till din landningszonmiljö använder du följande beslutsträd som utgångspunkt för att hjälpa dig att avgöra vilka nätverksverktyg eller tjänster som ska användas:

![Beslutsträd för nätverkstjänster i Azure](../../_images/ready/network-decision-tree.png)

### <a name="key-questions"></a>Viktiga frågor

Besvara följande frågor om dina arbetsbelastningar för att skapa ett beslutsunderlag baserat på beslutsträdet för Azure-nätverkstjänster:

- **Kräver dina arbetsbelastningar ett virtuellt nätverk?** Resurstypen hanterad plattform som en tjänst (PaaS) använder underliggande funktioner för plattformsnätverk som inte alltid kräver ett virtuellt nätverk. Om dina arbetsbelastningar inte kräver avancerade nätverksfunktioner och du inte behöver distribuera infrastruktur som en tjänst (IaaS)-resurser kan de inbyggda [standardnätverksfunktionerna som tillhandahålls av PaaS](../../decision-guides/software-defined-network/paas-only.md)-resurser uppfylla dina krav på arbetsbelastningsanslutning och trafikhantering.
- **Behöver dina arbetsbelastningar anslutning mellan virtuella nätverk och ditt lokala datacenter?** Azure tillhandahåller två lösningar för att upprätta hybrid nätverksfunktioner: Azure VPN Gateway och Azure ExpressRoute. [Azure VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) ansluter dina lokala nätverk till Azure via virtuella privata nätverk av typen plats-till-plats, ungefär på samma sätt som du konfigurerar och ansluter till ett fjärrkontor. VPN Gateway har en maximal bandbredd på 1,25 Gbit/s. [Azure ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) erbjuder högre tillförlitlighet och lägre latens genom att använda en privat anslutning mellan Azure och din lokala infrastruktur. Bandbreddsalternativen för ExpressRoute sträcker sig från 50 Mbit/s till 100 Gbit/s.
- **Behöver du inspektera och granska utgående trafik genom att använda lokala nätverksenheter?** För molnbaserade arbetsbelastningar [kan du använda Azure Firewall](https://docs.microsoft.com/azure/firewall/overview) eller en [molnbaserad virtuell nätverksinstallation (NVA)](https://azure.microsoft.com/solutions/network-appliances) från tredje part för att inspektera och granska trafik som går till eller kommer från det offentliga Internet. Många företags IT-säkerhetsprinciper kräver dock Internet-baserad utgående trafik för att röra sig genom centralt hanterade enheter i organisationens lokala miljö. [Tvingad tunneltrafik](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) stöder dessa scenarier. Alla hanterade tjänster har inte stöd för tvingad tunneltrafik. Tjänster och funktioner som [App Service Environment i Azure App Service](https://docs.microsoft.com/azure/app-service/environment/intro), [Azure-](https://docs.microsoft.com/azure/api-management/api-management-key-concepts)API Management [, Azure Kubernetes Service (AKS](https://docs.microsoft.com/azure/aks/intro-kubernetes)) [, hanterade instanser i Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index), [Azure Databricks](https://docs.microsoft.com/azure/azure-databricks/what-is-azure-databricks) och [AzureHDInsight](https://docs.microsoft.com/azure/hdinsight) har stöd för den här konfigurationen när tjänsten eller funktionen distribueras i ett virtuellt nätverk.
- **Behöver du ansluta flera virtuella nätverk?** Du kan använda [peering för virtuella nätverk](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) för att ansluta flera instanser av[Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview). Peering kan användas för anslutningar mellan prenumerationer och regioner. För scenarier där du tillhandahåller tjänster som delas över flera prenumerationer eller behöver hantera ett stort antal nätverks-peer-datorer, kan du överväga att använda en [hubb- och ekernätverkstopologi](../../decision-guides/software-defined-network/hub-spoke.md) eller [Azure Virtual WAN](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about). Det virtuella nätverkets peering tillhandahåller endast anslutning mellan två peer-anslutna nätverk. Som standard ger den inte transitiva anslutningar över flera peer-kopplingar.
- **Kommer dina arbetsbelastningar att vara tillgängliga via Internet?** Azure tillhandahåller tjänster som är utformade för att hjälpa dig att hantera och skydda extern åtkomst till dina program och tjänster:
  - [Azure Firewall](https://docs.microsoft.com/azure/firewall/overview)
  - [Nätverkstillämpningar](https://azure.microsoft.com/solutions/network-appliances)
  - [Azure Front Door Service](https://docs.microsoft.com/azure/frontdoor/front-door-overview)
  - [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway)
  - [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)
- **Behöver du stöd för anpassad DNS-hantering?** [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview) är en värdtjänst för DNS-domäner. Azure DNS tillhandahåller namnmatchning med hjälp av Azure-infrastrukturen. Om dina arbetsbelastningar kräver namnmatchning som går utöver de funktioner som tillhandahålls av Azure DNS kan du behöva distribuera extra lösningar. Om dina arbetsbelastningar också kräver Active Directory-tjänster bör du överväga att använda Azure [Active Directory Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/overview) för att förstärka Azure DNS-funktionerna. För fler funktioner kan du också [distribuera anpassade virtuella IaaS-datorer](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances) för att täcka dina behov.

## <a name="common-networking-scenarios"></a>Vanliga nätverksscenarier

Azure-nätverk består av flera produkter och tjänster som tillhandahåller olika nätverksfunktioner. Som en del av din designprocess för nätverk kan du jämföra arbetsbelastningskraven med nätverksscenarierna i följande tabell för att identifiera de Azure-verktyg eller -tjänster som du kan använda för att tillhandahålla följande nätverksfunktioner:

<!-- markdownlint-disable MD033 -->

| **Scenario** | **Nätverksprodukt eller -tjänst** |
| --- | --- |
| Nätverksinfrastrukturen måste kunna ansluta allt från virtuella datorer till inkommande VPN-anslutningar. | [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network) |
| Jag behöver kunna balansera inkommande och utgående anslutningar och förfrågningar till mina program och tjänster. | [Azure Load Balancer](https://docs.microsoft.com/azure/load-balancer) |
| Jag vill optimera leveransen från appserverfarmar samtidigt som jag förbättrar säkerheten med en brandvägg för webbappar. | [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway) <br/>[Azure Front Door Service](https://docs.microsoft.com/azure/frontdoor) |
| Jag behöver använda internet säkert och ansluta till Azure Virtual Networks med högpresterande VPN-gatewayer. | [Azure VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway) |
| Jag vill säkerställa hypersnabba DNS-svar och mycket hög tillgänglighet för alla mina domänbehov. | [Azure DNS](https://docs.microsoft.com/azure/dns) |
| Jag behöver leverera bandbreddsintensivt innehåll till kunder världen över snabbare, från program och lagrat innehåll till direktuppspelad video. | [Azure Content Delivery Network](https://docs.microsoft.com/azure/cdn) |
| Jag behöver skydda mina Azure-program från DDoS-attacker. | [Azure DDoS Protection](https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview) |
| Jag behöver fördela trafiken optimalt till tjänster i Azure-regioner globalt, samtidigt som jag får hög tillgänglighet och korta svarstider. | [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager)<br/>[Azure Front Door Service](https://docs.microsoft.com/azure/frontdoor) |
| Jag behöver lägga till anslutningar till privata nätverk och använda molntjänster från Microsoft direkt från företagsnätverket, precis som om de låg lokalt i mitt eget datacenter. | [Azure ExpressRoute](https://docs.microsoft.com/azure/expressroute) |
| Jag vill övervaka och diagnostisera villkor på nätverksscenarionivå. | [Azure Network Watcher](https://docs.microsoft.com/azure/network-watcher) |
| Jag behöver inbyggda brand Väggs funktioner, med inbyggd hög tillgänglighet, obegränsad moln skalbarhet och inget underhåll. | [Azure Firewall](https://docs.microsoft.com/azure/firewall) |
| Jag behöver ansluta företagskontor, detaljhandelsplatser och webbplatser säkert. | [Azure Virtual WAN](https://docs.microsoft.com/azure/virtual-wan) |
| Jag behöver en skalbar, säkerhetsförbättrad leveranspunkt för globala, mikrotjänstbaserade webbprogram. | [Azure Front Door Service](https://docs.microsoft.com/azure/frontdoor) |

<!-- markdownlint-enable MD033 -->

## <a name="choose-a-networking-architecture"></a>Välja en nätverksarkitektur

När du har identifierat de Azure Networking-tjänster som du behöver för att stödja dina arbetsbelastningar måste du också utforma arkitekturen som kombinerar dessa tjänster för att tillhandahålla din landningszons molnnätverksinfrastruktur. Molnimplementeringsramverket [Beslutsguide för programvarudefinierade nätverk](../../decision-guides/software-defined-network/index.md) innehåller information om några av de vanligaste nätverksarkitekturmönstren som används i Azure.

I följande tabell sammanfattas de huvudsakliga scenarier som dessa mönster stöder:

| **Scenario**                                                                                                                                                                                                                                                                                                                        | **Föreslagen nätverksarkitektur**                                                  |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| Alla Azure-värdbaserade arbets belastningar som distribueras till din landnings zon är helt PaaS-baserade, kräver inte ett virtuellt nätverk och är inte en del av en större moln implementerings ansträngning som innehåller IaaS-resurser.                                                                                                                        | [Endast PaaS](../../decision-guides/software-defined-network/paas-only.md)            |
| Dina Azure-värdbaserade arbetsbelastningar distribuerar IaaS-baserade resurser som virtuella datorer eller behöver annars ett virtuellt nätverk, men de behöver inte anslutas till din lokala miljö.                                                                                                                                          | [Molnbaserat](../../decision-guides/software-defined-network/cloud-native.md)      |
| Dina Azure-värdbaserade arbetsbelastningar kräver begränsad åtkomst till lokala resurser, men du är tvungen att hantera molnanslutningar som ej betrodda.                                                                                                                                                                                           | [Cloud DMZ](../../decision-guides/software-defined-network/cloud-dmz.md)            |
| Dina Azure-värdbaserade arbetsbelastningar kräver begränsad åtkomst till lokala resurser och du planerar att implementera äldre säkerhetsprinciper och säker anslutning mellan molnet och den lokala miljön.                                                                                                                         | [Hybrid](../../decision-guides/software-defined-network/hybrid.md)                  |
| Du behöver distribuera och hantera ett stort antal virtuella datorer och arbetsbelastningar, vilket kan överskrida gränserna för [Azure-prenumerationer](https://docs.microsoft.com/azure/azure-subscription-service-limits), du behöver dela tjänster över prenumerationer eller så behöver du en mer segmenterad struktur för roll, program eller behörighetsåtskillnad. | [Hubb och ekrar](../../decision-guides/software-defined-network/hub-spoke.md)        |
| Du har många avdelningskontor som behöver anslutas till varandra och till Azure.                                                                                                                                                                                                                                                       | [Azure Virtual WAN](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about) |

### <a name="azure-virtual-datacenter"></a>Azure Virtual Datacenter

Förutom att använda något av dessa arkitekturmönster kan du [konsultera Azure Virtual](../../reference/vdc.md) Data Center-vägledningen när du utformar din Azure-baserade moln infrastruktur, om företagets IT-grupp hanterar stora molnmiljöer. Azure Virtual Data Center ger en kombinerad lösning för nätverk, säkerhet, hantering och infrastruktur om organisationen uppfyller följande kriterier:

- Ditt företag måste uppfylla efterlevnadskrav som kräver centraliserad övervakning och granskningsfunktioner.
- Molntillgångarna består av över 10 000 virtuella IaaS-datorer eller PaaS-tjänster i motsvarande skala.
- Utvecklare och driftteam behöver flexibla distributionsfunktioner, samtidigt som företaget kräver gemensam princip- och styrningsefterlevnad och centraliserad IT-kontroll över kärntjänster.
- Din bransch är beroende av en komplex plattform som kräver djup expertis (till exempel branscher som ekonomi, olja och gas eller tillverkning).
- De befintliga IT-styrningsprinciperna kräver striktare paritet med befintliga funktioner, även tidigt i implementeringsprocessen.

## <a name="follow-azure-networking-best-practices"></a>Följ metodtips för Azure-nätverk

Som en del av din designprocess för nätverk kan du läsa följande artiklar:

- [Planering av virtuella nätverk](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Lär dig att planera virtuella datornätverk som baseras på dina krav på isolering, anslutningar och plats.
- [Metodtips för nätverkssäkerhet med Azure](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Lär dig om metodtips för Azure som kan hjälpa dig att förbättra nätverkssäkerheten.
- [Metodtips för nätverk när du migrerar arbetsbelastningar till Azure](https://docs.microsoft.com/azure/migrate/migrate-best-practices-networking?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Få ytterligare vägledning om hur du implementerar Azure-nätverk för att stödja IaaS-baserade och PaaS-baserade arbetsbelastningar.
