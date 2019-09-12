---
title: Perimeternätverk
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Perimeternätverk
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: cf5b641bb894c9784f01e4e9eaae545b6b38a30d
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70828544"
---
# <a name="perimeter-networks"></a>Perimeternätverk

[Perimeternätverk][perimeter-network] aktiverar säkra anslutningar mellan dina molnnätverk och lokala eller fysiska datacenternätverk, tillsammans med någon anslutning till och från Internet. De kallas även för demilitariserade zoner (DMZs).

För att perimeternätverket ska vara effektiva måste inkommande paket flöda genom säkerhetsenheter som finns i säkra undernät innan de når serverdelen. Exempel är brandväggen, identifieringssystem för intrång (ID) och system för skydd mot intrång (IPS). Innan de lämnar nätverket bör Internet-baserade paket från arbetsbelastningen också flöda genom säkerhetsenheterna i perimeternätverket. Syftet med det här flödet är principtillämpning, inspektion och granskning.

Perimeternätverket använder följande Azure-funktioner och -tjänster:

- [Virtuella nätverk][virtual-networks], [användardefinierade vägar][user-defined-routes] och [nätverkssäkerhetsgrupper][network-security-groups]
- [Virtuell nätverksutrustning][NVA]
- [Azure Load Balancer][ALB]
- [Azure Application Gateway][AppGW] och [brandvägg för webbaserade program][AppGWWAF] (WAF)
- [Offentliga IP-adresser][PIP]
- [Azure Front Door][AFD] med [brandvägg för webbaserade program][AFDWAF]
- [Azure Firewall][AzFW]

> [!NOTE]
> Referensarkitekturen för Azure innehåller exempelmallar som du kan använda för att implementera dina egna perimeternätverk:
>
> - [Implementera en DMZ mellan Azure och ditt lokala datacenter](/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid)
> - [Implementera en DMZ mellan Azure och Internet](/azure/architecture/reference-architectures/dmz/secure-vnet-dmz)

Vanligtvis ansvarar dina centrala IT- och säkerhetsteam för att definiera krav för att använda perimeternätverket.

![Exempel på nätverk med hubb och ekrar][7]

Föregående diagram visar ett exempel på ett [ hubb-och-ekernätverk](./hub-spoke-network-topology.md) som använder två perimeternätverk med åtkomst till Internet och ett lokalt nätverk. Båda perimeterna finns i DMZ-hubben. I DMZ-hubben kan perimeternätverket till Internet skala upp för att stödja många affärsapplikationer (LOBs) genom att använda flera grupper av WAF och Azure Firewall-instanser som skyddar de virtuella ekernätverken. Hubben tillåter också anslutning via VPN eller Azure-ExpressRoute efter behov.

## <a name="virtual-networks"></a>Virtuella nätverk

Perimeternätverk skapas vanligtvis med hjälp av [ett virtuellt][virtual-networks] nätverk med flera undernät som är värdar för de olika typerna av tjänster som filtrerar och inspekterar trafik till eller från Internet via instanser NVA, WAF och Azure Application Gateway.

## <a name="user-defined-routes"></a>Användardefinierade vägar

Genom att [använda användardefinierade vägar][user-defined-routes] kan kunder distribuera brandväggar, IDS/IPS och andra virtuella enheter. Kunderna kan sedan dirigera nätverkstrafik genom de här säkerhetsanordningarna för tillämpning, granskning och inspektion av säkerhetsgränser. Användardefinierade vägar kan skapas för att garantera att trafiken passerar genom de angivna anpassade virtuella datorerna, NVA:erna och belastningsutjämnare.

I ett hubb-och-ekernätverk som ser till att trafiken som skapas av virtuella datorer i ekrarna passerar genom rätt virtuella installationer i hubben behövs en användardefinierad väg i ekernätverkets undernät. Den här vägen anger klientdelens IP-adress för den interna belastningsutjämnaren som nästa hopp. Den interna belastningsutjämnaren distribuerar den interna trafiken till de virtuella datorerna (belastningsutjämnarens serverdelspool).

## <a name="azure-firewall"></a>Azure Firewall

[Azure Firewall][AzFW] är en hanterad, molnbaserad tjänst som skyddar dina Azure Virtual Network-resurser. Det är en helt tillståndskänslig hanterad brandvägg med inbyggd hög tillgänglighet och obegränsad molnskalbarhet. Du kan centralt skapa, framtvinga och logga principer för tillämpning och nätverksanslutning över prenumerationer och virtuella nätverk.

Azure Firewall använder en statisk offentlig IP-adress för dina virtuella nätverksresurser. Det gör att externa brandväggar kan identifiera trafiken från ditt virtuella nätverk. Tjänsten är helt integrerad med Azure Monitor för loggning och analys.

## <a name="network-virtual-appliances"></a>Virtuella nätverksinstallationer

Perimeternätverket med åtkomst till Internet hanteras normalt via en Azure Firewall-instans eller en brandväggsgrupp eller [brandväggar för webbaserade program][AFDWAF].

Många webbprogram används ofta i olika LOB:er. Dessa webbprogram tenderar att drabbas av sårbarheter och potentiella hot. En brandvägg för webbaserade program identifierar attacker mot webbprogram (HTTP/HTTPS) i större utsträckning än en allmän brandvägg. Jämfört med traditionell brandväggsteknik har brandväggar för webbaserade program specifika funktioner som skyddar inre webbservrar mot hot.

En Azure Firewall-instans och en [nätverksbrandvägg för virtuella datorer][NVA] använder ett gemensamt administrationsplan med en uppsättning säkerhetsregler för att skydda arbetsbelastningarna som finns i ekrarna och kontrollerar åtkomsten till lokala nätverk. Azure-brandväggen har inbyggd skalbarhet, medan NVA-brandväggar kan skalas manuellt bakom en belastningsutjämnare.

En brandväggsgrupp har vanligtvis mindre specialiserad programvara än en brandvägg för webbaserade program men den har ett bredare programdefinitionsområde för att filtrera och inspektera all typ av ingående och utgående trafik. Om du använder en NVA-metod kan du söka efter och distribuera programvaran från Azure Marketplace.

Använd en uppsättning Azure Firewall-instanser (eller NVA) för trafik som kommer från Internet och en annan uppsättning för trafik som kommer från lokala platser. Att bara ha en uppsättning med brandväggar är en säkerhetsrisk eftersom det inte ger någon säkerhetsperimeter mellan de två uppsättningarna med nätverkstrafik. När separata brandväggslager används minskas komplexiteten för kontroll av säkerhetsregler och tydliggör vilka regler som motsvarar respektive inkommande nätverksbegäran.

## <a name="azure-load-balancer"></a>Azure Load Balancer

[Azure Load Balancer][ALB] är en tjänst för hög tillgänglighet för Layer 4 (TCP/UDP) som kan distribuera inkommande trafik mellan tjänstinstanser som definierats i en belastningsutjämnad uppsättning. Trafik som skickas till belastningsutjämnaren från klientdelsslutpunkter (offentliga IP-slutpunkter eller privata IP-slutpunkter) kan distribueras om med eller utan adressöversättning till en grupp IP-adresser för serverdelen (t. ex. NVA eller virtuella datorer).

Azure Load Balancer kan också avsöka hälsotillståndet för de olika serverinstanserna. När en instans inte svarar på avsökningen slutar belastningsutjämnaren att skicka trafik till de ohälsosamma instanserna.

Som exempel på att använda ett hubb- och ekernätverk kan du distribuera en extern belastningsutjämnare till både hubbarna och ekrarna. I hubben dirigerar belastningsutjämnaren trafik effektivt till tjänster i ekrarna. I ekrarna hanterar belastningsutjämnarna programtrafik.

## <a name="azure-front-door-service"></a>Azure Front Door Service

[Azure Front Door Service][AFD] är Microsofts högtillgängliga och skalbara plattform för webbprogramacceleration och global HTTPS-belastningsutjämnare. Du kan använda Azures Front Door Service för att bygga, hantera och skala ut ditt dynamiska webbprogram och statiska innehåll. Den körs på över 100 platser på kanten av Microsofts globala nätverk.

Azure Front Door Service ger ditt program enhetlig regional/stämplad underhållsautomatisering, BCDR-automatisering, enhetlig klient-/användarinformation, cachelagring och tjänstinsikter. Plattformen erbjuder prestanda, tillförlitlighet och stöd för serviceavtal. Den erbjuder även certifieringar för regelefterlevnad och granskningsbara säkerhetsmetoder som utvecklas, drivs och stöds internt av Azure.

## <a name="application-gateway"></a>Application Gateway

[Azure Application Gateway][AppGW] är en dedikerad virtuell installation som tillhandahåller en hanterad ADC (Application Delivery Controller). Tjänsten erbjuder olika Layer 7-belastningsutjämningsfunktioner för ditt program.

Application Gateway gör det möjligt för dig att optimera webbservergruppens produktivitet genom att avlasta CPU-intensiv SSL-avslutning till Application Gateway. Här finns även andra layer 7-routningsfunktioner, till exempel resursallokeringsdistribution av inkommande trafik, cookiebaserad sessionstillhörighet, URL-sökvägsbaserad routning och möjligheten att vara värd för flera webbplatser bakom en enda Application Gateway.

Application Gateway WAF SKU:n innehåller en brandvägg för webbaserade program. Den här SKU:n skyddar webbprogram mot vanliga säkerhetsrisker och sårbarheter på webben. Application Gateway kan konfigureras som internetuppkopplad gateway, endast intern gateway eller en kombination av båda.

## <a name="public-ips"></a>Offentliga IP-adresser

Med vissa Azure-funktioner kan du associera tjänstslutpunkter till en [offentlig IP-adress][PIP] så att din resurs kan nås från Internet. Den här slutpunkten använder Network Address Translation (NAT) för att dirigera trafik till den interna adressen och porten i det virtuella Azure-nätverket. Den här vägen är det primära sättet för extern trafik att skickas till det virtuella nätverket. Du kan konfigurera offentliga IP-adresser för att avgöra vilken trafik som skickas och hur och var den översätts till det virtuella nätverket.

## <a name="azure-ddos-protection-standard"></a>Azure DDoS Protection Standard

[Azure DDoS Protection Standard][DDoS] ger skydd utöver [grundläggande tjänstnivåer][DDoS] som är specifikt för Azures virtuella nätverksresurser. DDoS Protection standard är enkelt att aktivera och kräver inga programändringar.

Du kan justera skyddsprinciperna genom dedikerad trafikövervakning och algoritmer för maskininlärning. Principer tillämpas på offentliga IP-adresser som är kopplade till resurser som har distribuerats i virtuella nätverk. Exempel är Azure Load Balancer, Azure Application Gateway och Azure Service Fabric-instanser.

Telemetri i realtid är tillgängligt via Azure Monitor-vyer, såväl under pågående angrepp som i efterhand. Du kan lägga till skydd på programnivå med Azure Application Gateway-brandvägg för webbaserade program. Skydd finns för offentliga IP-adresser med IPv4-protokoll i Azure.

<!-- images -->

[0]: ./images/network-redundant-equipment.png "Exempel på komponentöverlappning"
[1]: ./images/network-hub-spoke-high-level.png "Exempel på en hög nivå med hubb och eker"
[2]: ./images/network-hub-spokes-cluster.png "Kluster med hubbar och ekrar"
[3]: ./images/network-spoke-to-spoke.png "Eker-till-eker"
[4]: ./images/network-hub-spoke-block-level-diagram.png "Blocknivådiagram för hubb-eker"
[5]: ./images/network-users-groups-subsciptions.png "Användare, grupper, prenumerationer och projekt"
[6]: ./images/network-infrastructure-high-level.png "Infrastrukturdiagram på hög nivå"
[7]: ./images/network-highlevel-perimeter-networks.png "Infrastrukturdiagram på hög nivå"
[8]: ./images/network-vnet-peering-perimeter-neworks.png "VNet-peering och perimeternätverk"
[9]: ./images/network-high-level-diagram-monitoring.png "Diagram på hög nivå för övervakning"
[10]: ./images/network-high-level-workloads.png "Diagram på hög nivå för arbetsbelastning"

<!-- links -->

[Limits]: /azure/azure-subscription-service-limits
[Roles]: /azure/role-based-access-control/built-in-roles
[virtual-networks]: /azure/virtual-network/virtual-networks-overview
[network-security-groups]: /azure/virtual-network/virtual-networks-nsg
[DNS]: /azure/dns/dns-overview
[PrivateDNS]: /azure/dns/private-dns-overview
[VNetPeering]: /azure/virtual-network/virtual-network-peering-overview
[user-defined-routes]: /azure/virtual-network/virtual-networks-udr-overview
[RBAC]: /azure/role-based-access-control/overview
[azure-ad]: /azure/active-directory/active-directory-whatis
[VPN]: /azure/vpn-gateway/vpn-gateway-about-vpngateways
[ExR]: /azure/expressroute/expressroute-introduction
[ExRD]: /azure/expressroute/expressroute-erdirect-about
[vWAN]: /azure/virtual-wan/virtual-wan-about
[NVA]: /azure/architecture/reference-architectures/dmz/nva-ha
[AzFW]: /azure/firewall/overview
[SubMgmt]: /azure/architecture/cloud-adoption/appendix/azure-scaffold
[RGMgmt]: /azure/azure-resource-manager/resource-group-overview
[perimeter-network]: /azure/best-practices-network-security
[ALB]: /azure/load-balancer/load-balancer-overview
[DDoS]: /azure/virtual-network/ddos-protection-overview
[PIP]: /azure/virtual-network/virtual-network-public-ip-address
[AFD]: /azure/frontdoor/front-door-overview
[AFDWAF]: /azure/frontdoor/waf-overview
[AppGW]: /azure/application-gateway/application-gateway-introduction
[AppGWWAF]: /azure/application-gateway/application-gateway-web-application-firewall-overview
[Monitor]: /azure/monitoring-and-diagnostics/
[ActLog]: /azure/monitoring-and-diagnostics/monitoring-overview-activity-logs
[DiagLog]: /azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[nsg-log]: /azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: /azure/operations-management-suite/operations-management-suite-overview
[NPM]: /azure/log-analytics/log-analytics-network-performance-monitor
[NetWatch]: /azure/network-watcher/network-watcher-monitoring-overview
[WebApps]: /azure/app-service/
[HDI]: /azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: /azure/event-hubs/event-hubs-what-is-event-hubs
[ServiceBus]: /azure/service-bus-messaging/service-bus-messaging-overview
[traffic-manager]: /azure/traffic-manager/traffic-manager-overview
