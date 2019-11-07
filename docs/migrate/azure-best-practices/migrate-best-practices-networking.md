---
title: Metodtips för att konfigurera nätverk för arbetsbelastningar som migrerats till Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: När du har migrerat till Azure kan du få metodtips om nätverk för migrerade arbetsbelastningar.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/04/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: a7f119dcfd2b7cdfc71b8a4c6f913448cd98e763
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753608"
---
# <a name="best-practices-to-set-up-networking-for-workloads-migrated-to-azure"></a>Metodtips för att konfigurera nätverk för arbetsbelastningar som migrerats till Azure

När du planerar och utformar din migrering är ett av de viktigaste stegen, utöver själva migreringen, utformningen och implementeringen av Azure-nätverk. Den här artikeln innehåller metodtips för nätverk när du migrerar till IaaS- och PaaS-implementeringar i Azure.

> [!IMPORTANT]
> De metodtips och åsikter som beskrivs i den här artikeln baseras på de tillgängliga funktionerna i Azure-plattformen och -tjänsten när den skrevs. Funktioner förändras över tid. Vissa rekommendationer kan kanske inte tillämpas på din distribution så välj vad som passar dig bäst.

## <a name="design-virtual-networks"></a>Utforma virtuella nätverk

Azure tillhandahåller virtuella nätverk:

- Azure-resurser kommunicerar privat, direkt och säkert med varandra via virtuella nätverk.
- Du kan konfigurera slutpunktsanslutningar på virtuella nätverk för virtuella datorer och tjänster som behöver anslutning till Internet.
- Ett virtuellt nätverk är en logisk isolering av Azure-molnet som är dedikerad till din prenumeration.
- Du kan implementera flera virtuella nätverk i varje Azure-prenumeration och Azure-region.
- Varje virtuellt nätverk isoleras från andra virtuella nätverk.
- Virtuella nätverk kan innehålla privata och offentliga IP-adresser som definieras i [RFC 1918](https://tools.ietf.org/html/rfc1918), uttryckt i CIDR-format. Offentliga IP-adresser som anges i ett virtuellt nätverks adressutrymme är inte direkt tillgängliga från Internet.
- Virtuella nätverk kan ansluta till varandra med hjälp av VNet-peering. Anslutna virtuella nätverk kan finnas i samma eller olika regioner. Resurser i ett VNet kan därför ansluta till resurser i andra virtuella nätverk.
- Azure dirigerar trafik mellan undernät inom ett virtuellt nätverk, anslutna virtuella nätverk, lokala nätverk och Internet, som standard.

När du planerar din topologi för det virtuella nätverket bör du fundera på hur du vill organisera IP-adressutrymme, implementera ett nav- och ekernätverk, segmentera virtuella nätverk i undernät, konfigurera DNS och implementera Azure-åtkomstzoner.

## <a name="best-practice-plan-ip-addressing"></a>Bästa praxis: planera IP-adressering

När du skapar virtuella nätverk som en del av migreringen är det viktigt att planera det virtuella nätverkets IP-adressutrymme.

- Du bör tilldela ett adressutrymme som inte är större än CIDR-intervallet på /16 för varje virtuellt nätverk. Virtuella nätverk tillåter att IP-adresser med 65536 används och om du tilldelar ett mindre prefix än /16 går IP-adresserna förlorade. Det är viktigt att inte slösa IP-adresser även om de ligger i de privata intervall som definieras av RFC 1918.
- Det virtuella nätverkets adressutrymme bör inte överlappa de lokala nätverksintervallen.
- Network Address Translation (NAT) bör inte användas.
- Överlappande adresser kan leda till att nätverk inte kan anslutas och att routning inte fungerar som det ska. Om nätverket överlappar måste du ändra dess utformning eller använda Network Address Translation (NAT).

**Läs mer:**

- [Få en översikt](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) över virtuella Azure-nätverk.
- Läs [vanliga frågor och svar](https://docs.microsoft.com/azure/virtual-network/virtual-networks-faq) om nätverk.
- [Lär dig](https://docs.microsoft.com/azure/azure-subscription-service-limits?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) mer om nätverksbegränsningar.

## <a name="best-practice-implement-a-hub-and-spoke-network-topology"></a>Bästa praxis: implementera en nätverkstopologi för nav och ekrar

En hubb- och eker-nätverkstopologi är ett sätt att isolera arbetsbelastningar samtidigt som man delar tjänster som identitet och säkerhet.

- Hubben är ett virtuellt Azure-nätverk som fungerar som en central punkt för anslutningen.
- Ekrarna är virtuella nätverk som ansluter till det virtuella hubbnätverket med VNet-peering.
- Delade tjänster distribueras i hubben medan individuella arbetsbelastningar distribueras som ekrar.

Tänk också på följande:

- Implementeringen av en hub-spoke-topologi i Azure centraliserar gemensamma tjänster, till exempel anslutningar till lokala nätverk, brandväggar och isolering mellan virtuella nätverk. Det virtuella hubbnätverket tillhandahåller en central anslutningspunkt för lokala nätverk och en värd för tjänster som används av arbetsbelastningar som använder virtuella ekernätverk som värd.
- En hubb-och ekerkonfiguration används vanligtvis av större företag. Mindre företag bör överväga en enklare design för att undvika kostnader och komplexitet.
- Ekrar kan användas för att isolera arbetsbelastningar eftersom varje virtuellt eker-nätverk hanteras separat från andra ekrar. Varje arbetsbelastning kan innehålla flera nivåer, med flera undernät som är anslutna via Azure-lastbalanserare.
- Virtuella nätverk med hubbar och ekrar kan implementeras i olika resursgrupper och även i olika prenumerationer. När du använder virtuella peer-nätverk med olika prenumerationer kan prenumerationerna associeras med samma eller olika Azure Active Directory-klienter (Azure AD). Det möjliggör en decentraliserad hantering av varje arbetsbelastning, samtidigt som tjänster i det virtuella hubbnätverket delas.

![Förändringsledning](./media/migrate-best-practices-networking/hub-spoke.png)
*Hubb och eker*

**Läs mer:**

- [Läs mer om](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) en hubb- och ekertopologi.
- Få nätverksrekommendationer för att köra virtuella Azure-datorer med [Windows](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/windows-vm) och [Linux](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/linux-vm).
- [Läs mer om](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) VNet-peering (virtuella nätverk).

## <a name="best-practice-design-subnets"></a>Bästa praxis: utforma undernät

För att skapa en isolering inom ett virtuellt undernät ska du segmentera det i ett eller flera undernät och allokera en del av det virtuella nätverkets adressutrymme till varje undernät.

- Du kan skapa flera undernät i varje virtuella nätverk.
- Som standard dirigerar Azure trafik mellan alla undernät inom ett virtuellt nätverk.
- Undernätbesluten baseras på dina tekniska och organisatoriska krav.
- Du skapar undernät med CIDR-notation.
- När du bestämmer nätverksintervall för undernät är det viktigt att observera att Azure kvarhåller fem IP-adresser från varje undernät som inte kan användas. Om du till exempel skapar det minsta tillgängliga undernätet på/29 (med åtta IP-adresser) kvarhåller Azure fem adresser, så att du bara har tre användbara adresser som kan tilldelas till värdar i undernätet.
- I de flesta fall använder du/28 som det minsta under nätet.

**Exempel:**

Tabellen visar ett exempel på ett virtuellt nätverk med ett adressutrymme på 10.245.16.0/20 segmenterat i undernät för en planerad migrering.

**Undernät** | **CIDR** | **Adresser** | **Använd**
--- | --- | --- | ---
DEV-FE-EUS2 | 10.245.16.0/22 | 1019 | Virtuella datorer på klientsida/webbnivå
DEV-APP-EUS2 | 10.245.20.0/22 | 1019 | Virtuella datorer på appnivå
DEV-DB-EUS2 | 10.245.24.0/23 | 507 | Virtuella databasdatorer

**Läs mer:**

- [Lär dig](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#segmentation) mer om att utforma undernät.
- [Läs](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure) hur ett fiktivt företag (Contoso) förberedde sin nätverksinfrastruktur för migrering.

## <a name="best-practice-set-up-a-dns-server"></a>Bästa praxis: Konfigurera en DNS-Server

Azure lägger till en DNS-server som standard när du distribuerar ett virtuellt nätverk. På så sätt kan du snabbt bygga virtuella nätverk och distribuera resurser. Den här DNS-servern tillhandahåller dock endast tjänster till resurserna i det virtuella nätverket. Om du vill ansluta flera virtuella nätverk till varandra eller ansluta till en lokal server från virtuella nätverk behöver du ytterligare namnmatchningsfunktioner. Du kan till exempel behöva Active Directory för att matcha DNS-namn mellan virtuella nätverk. För att göra detta distribuerar du din egen anpassade DNS-server i Azure.

- DNS-servrar i ett virtuellt nätverk kan vidarebefordra DNS-frågor till de rekursiva matcharna i Azure. På så sätt kan du matcha värdnamn i det virtuella nätverket. En domänkontrollant som körs i Azure kan till exempel svara på DNS-frågor för sina egna domäner och vidarebefordra alla andra frågor till Azure.
- DNS-vidarebefordring gör det möjligt för virtuella datorer att se såväl dina lokala resurser (via domänkontrollanten) som Azure-tillhandahållna värdnamn (med hjälp av vidarebefordraren). Åtkomst till de rekursiva matcharna i Azure tillhandahålls med den virtuella IP-adressen 168.63.129.16.
- DNS-vidarebefordring möjliggör även DNS-matchning mellan virtuella nätverk och gör det möjligt för lokala datorer att lösa värdnamn som tillhandahålls av Azure.
  - För att lösa ett värdnamn för en virtuell dator måste den virtuella DNS-servern finnas i samma virtuella nätverk och konfigureras för att vidarebefordra värdnamnfrågor till Azure.
  - Eftersom DNS-suffixet skiljer sig i varje virtuella nätverk kan du använda regler för villkorlig vidarebefordran för att skicka DNS-frågor till rätt virtuella nätverk för matchning.
- När du använder dina egna DNS-servrar kan du ange flera DNS-servrar för varje virtuella nätverk. Du kan också ange flera DNS-servrar per nätverksgränssnitt (för Azure Resource Manager) eller per molntjänst (för den klassiska distributionsmodellen).
- DNS-servrar som angetts för ett nätverksgränssnitt eller en molntjänst prioriteras framför DNS-servrar som angetts för det virtuella nätverket.
- I Azure Resource Manager-distributionsmodellen kan du ange DNS-servrar för ett virtuellt nätverk och ett nätverksgränssnitt. Den rekommenderade metoden är att endast använda inställningen på virtuella nätverk.

    ![DNS-servrar](./media/migrate-best-practices-networking/dns2.png) *DNS-servrar för virtuella nätverk*

**Läs mer:**

- [Lär dig](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure) mer om namnmatchning när du använder en egen DNS-server.
- [Läs mer om](../../ready/azure-best-practices/naming-and-tagging.md) namngivningsregler och begränsningar för DNS.

## <a name="best-practice-set-up-availability-zones"></a>Bästa praxis: Konfigurera tillgänglighets zoner

Tillgänglighetszoner ökar hög tillgänglighet för att skydda dina appar och data från datacenterfel.

- Tillgänglighetszoner är unika fysiska platser inom en Azure-region.
- Varje zon utgörs av ett eller flera datacenter som är utrustade med oberoende kraft, kylning och nätverk.
- För att säkerställa återhämtning finns det minst tre separata zoner i alla aktiverade regioner.
- Den fysiska avgränsningen av tillgänglighetszonerna inom en region skyddar program och data mot datacenterfel.
- Zonredundanta tjänster replikerar dina program och data över tillgänglighetszoner för att skydda mot enskilda felpunkter. - - Med tillgänglighetszonerna kan Azure erbjuda branschens bästa serviceavtal med en drifttid på 99,99 % för virtuella datorer.

    ![Tillgänglighetszon](./media/migrate-best-practices-networking/availability-zone.png) *Tillgänglighetszon*

- Du kan planera och bygga hög tillgänglighet i din migrationsarkitektur genom att placera beräknings-, lagrings-, nätverks- och dataresurser inom en zon och replikera dem i andra zoner. Azuretjänster som har stöd för tillgänglighetszoner kan delas in i två kategorier:
  - Zonindelade Services: du kopplar en resurs till en speciell zon. Till exempel virtuella datorer, hanterade diskar, IP-adresser).
  - Zoner – redundanta tjänster: resursen replikeras automatiskt mellan zoner. Till exempel, zonredundant lagring, Azure SQL Database.
- Du kan distribuera en standardiserad Azure-belastning som utjämnas med internetriktade arbetsbelastningar eller appnivåer för att skapa en zonindelad feltolerans.

    ![Belastningsutjämnare](./media/migrate-best-practices-networking/load-balancer.png) *Belastningsutjämnare*

**Läs mer:**

- [Få en översikt](https://docs.microsoft.com/azure/availability-zones/az-overview) över tillgänglighetszoner.

## <a name="design-hybrid-cloud-networking"></a>Utforma hybridmolnnätverk

Vid en lyckad migrering är det viktigt att ansluta lokala företagsnätverk till Azure. Detta skapar ett så kallat hybridmolnnätverk, där tjänsterna tillhandahålls från Azuremolnet till företagsanvändare. Det finns två alternativ för att skapa den här typen av nätverk:

- **VPN för plats-till-plats:** Du upprättar en plats-till-plats-anslutning mellan din kompatibla lokala VPN-enhet och en Azure VPN-gateway som har distribuerats i ett VNet. Alla auktoriserade lokala resurser kan komma åt virtuella nätverk. Plats-till-platskommunikation skickas via en krypterad tunnel via Internet.
- **Azure-ExpressRoute:** Du upprättar en Azure ExpressRoute-anslutning mellan ditt lokala nätverk och Azure via en ExpressRoute-partner. Den här anslutningen är privat och trafiken går inte via Internet.

**Läs mer:**

- [Lär dig](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/vpn) mer om nätverk med hybridmoln.

## <a name="best-practice-implement-a-highly-available-site-to-site-vpn"></a>Bästa praxis: implementera en plats-till-plats-VPN med hög tillgänglighet

Om du vill implementera en plats-till-plats-VPN skapar du en VPN-gateway i Azure.

- En VPN-gateway är en speciell typ av VNet-gateway som skickar krypterad trafik mellan ett virtuellt Azure-nätverk och en lokal plats via det offentliga Internet.
- En VPN-gateway kan också skicka krypterad trafik mellan Azure virtuella nätverk över Microsoft-nätverket.
- Varje virtuellt nätverk kan ha bara en VPN-gateway.
- Du kan skapa flera anslutningar till samma VPN-gateway. När du skapar flera anslutningar delar alla VPN-tunnlar på den tillgängliga bandbredden.
- Varje Azure VPN-gateway består av två instanser i en aktiv-standby-konfiguration.
  - När det utförs ett planerat underhåll eller uppstår ett oplanerat avbrott för en aktiv instans inträffar redundans och standby-instansen tar över automatiskt. Plats-till-platsanslutningen eller anslutningen mellan virtuella nätverk återupptas.
  - Växlingen leder till ett kort avbrott.
  - Vid ett planerat underhåll återställs anslutningen inom 10 till 15 sekunder.
  - Vid ett oplanerat avbrott tar det lite längre tid att återställa anslutningen. I värsta fall kan det ta en till en och en halv minut.
  - P2S VPN-klientanslutningar till gatewayen kopplas från och användarna måste ansluta på nytt från klientdatorerna.

När du konfigurerar ett plats-till-plats-VPN gör du följande:

- Du behöver ett virtuellt nätverk vars adressintervall inte överlappar med det lokala nätverket som VPN-anslutningen ska ansluta till.
- Du skapar ett gateway-undernät i nätverket.
- Du skapar en VPN-gateway, anger Gateway-typ (VPN) och om gatewayen är principbaserad eller routningsbaserad. En Route-baserad VPN anses vara mer kapabel och kan granskas i framtiden.
- Du skapar en lokal nätverksgateway lokalt och konfigurerar den lokala VPN-enheten.
- Du skapar en redundant plats-till-plats-VPN-anslutning mellan den virtuella nätverksgatewayen och den lokala enheten. Med routningsbaserad VPN kan du antingen använda aktiv-passiv eller aktiv-aktiv anslutning till Azure. Routningsbaserad stöder dessutom både plats-till-plats-anslutning (från valfri dator) och punkt-till-plats-anslutning (from en enda dator) samtidigt.
- Välj den gateway-SKU som du vill använda. Detta beror på arbetsbelastningskrav, dataflöden, funktioner och serviceavtal.
- BGP (Border Gateway Protocol) är en valfri funktion som du kan använda med Azure ExpressRoute och routningsbaserade VPN-gatewayer för att sprida dina lokala BGP-vägar till dina virtuella nätverk.

![VPN](./media/migrate-best-practices-networking/vpn.png)
*Plats-till-plats-VPN*

**Läs mer:**

- [Se](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) kompatibla lokala VPN-enheter.
- [Få en översikt](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) över VPN-gatewayer.
- [Lär dig mer](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-highlyavailable) om VPN-anslutningar med hög tillgänglighet.
- [Lär dig](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) mer om att planera och utforma en VPN-gateway.
- [Se](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsku) VPN gateway-inställningar.
- [Se](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#gwsku) gateway-SKU:er.
- [Läs om](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-bgp-overview) hur du konfigurerar BGP med Azure VPN-gatewayer.

### <a name="best-practice-configure-a-gateway-for-vpn-gateways"></a>Bästa praxis: Konfigurera en gateway för VPN-gatewayer

När du skapar en VPN-gateway i Azure måste du använda ett särskilt undernät med namnet GatewaySubnet. När du skapar det här undernätet bör du följa dessa metodtips:

- Prefixlängden för gateway-undernätet får ha en maximal prefixlängd på 29 (till exempel 10.119.255.248/29). Den aktuella rekommendationen är att du använder prefixlängden 27 (till exempel 10.119.255.224/27).
- När du definierar adressutrymmet för gateway-undernätet använder du den sista delen av det virtuella nätverkets adressutrymme.
- När du använder Azure GatewaySubnet ska du aldrig distribuera virtuella datorer eller andra enheter som Application Gateway till gateway-undernätet.
- Tilldela inte en nätverkssäkerhetsgrupp (NSG) till det här undernätet. Det får gatewayen att sluta fungera.

**Läs mer:**

- [Använd det här verktyget](https://gallery.technet.microsoft.com/scriptcenter/Address-prefix-calculator-a94b6eed) för att fastställa IP-adressutrymmet.

## <a name="best-practice-implement-azure-virtual-wan-for-branch-offices"></a>Bästa praxis: implementera Azure Virtual WAN för avdelnings kontor

För flera VPN-anslutningar är Azure Virtual WAN en nätverkstjänst som tillhandahåller optimerade och automatiserade anslutningar mellan olika platser via Azure.

- Med Virtual WAN kan du ansluta och konfigurera platsspecifika enheter så att de kommunicerar med Azure. Detta kan göras manuellt eller med enheter från önskad leverantör via en Virtual WAN-partner.
- Leverantörsenheter är enkla att använda, ansluta och hantera.
- Med de inbyggda instrumentpanelerna i Azure WAN kan du snabbt felsöka problem och enkelt visa anslutningar mellan platser i hög skala.

**Läs mer:** 
[Läs mer om](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about) Azure Virtual WAN.

### <a name="best-practice-implement-expressroute-for-mission-critical-connections"></a>Bästa praxis: implementera ExpressRoute för verksamhets kritiska anslutningar

Azure ExpressRoute-tjänsten utökar din lokala infrastruktur till Microsoft Cloud genom att skapa privata anslutningar mellan virtuella Azure-datacenter och lokala nätverk.

- ExpressRoute-anslutningar kan befinna sig över ett valfritt-till-valfritt-nätverk (IP-VPN), ett Ethernet-nätverk från punkt till punkt eller via en anslutningsleverantör. De går inte via det offentliga Internet.
- ExpressRoute-anslutningar ger högre säkerhet, tillförlitlighet och högre hastigheter (upp till 10 Gbit/s), tillsammans med konsekvent svarstid.
- ExpressRoute är användbart för virtuella datacentra eftersom kunder kan få fördelar med efterlevnadsprinciper som är kopplade till privata anslutningar.
- Med ExpressRoute Direct kan du ansluta direkt till Microsoft-routrar på 100G bps för större bandbredd.
- ExpressRoute använder BGP för att utväxla vägar mellan lokala nätverk, Azure-instanser och offentliga Microsoft-adresser.

Att distribuera ExpressRoute-anslutningar innebär vanligtvis att man registrerar sig hos en ExpressRoute-tjänstleverantör. Det är vanligt att först använda plats-till-plats-VPN för att skapa en anslutning mellan det virtuella datacentret och den lokala resursen. Sedan migrerar man till en ExpressRoute-anslutning när en fysisk anslutning till din tjänsteleverantör är etablerad.

**Läs mer:**

- [Läs en översikt](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) över ExpressRoute.
- [Lär dig mer](https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about) om ExpressRoute Direct.

### <a name="best-practice-optimize-expressroute-routing-with-bgp-communities"></a>Bästa praxis: optimera ExpressRoute-routning med BGP-communities

När du har flera ExpressRoute-kretsar måste ha du mer än en sökväg för att ansluta till Microsoft. Därför kan en icke-optimal routning inträffa – vilket innebär att din trafik får en längre sökväg till Microsoft och Microsoft till nätverket. Ju längre nätverkssökvägen är, desto längre svarstid. Svarstiden har direkt inverkan på programmens prestanda och användarupplevelse.

**Exempel:**

Låt oss titta på ett exempel:

- Anta att du har två kontor i USA, ett i Los Angeles och ett i New York.
- Ditt kontor ansluts i ett WAN (Wide Area Network), som kan vara antingen ditt eget stamnät eller leverantörens IP VPN.
- Du har två ExpressRoute-kretsar, en i USA, västra och en i USA, östra som även är anslutna i WAN-nätverket. Naturligtvis har du två sökvägar för att ansluta till Microsoft-nätverket.

**Problem:**

Anta nu att du har Azure-distribution (t.ex. Azure App Service) i både ”USA, västra” och ”USA, östra”.

- Du vill att användarna på varje kontor ska ha tillgång till sina närmaste Azure-tjänster.
- Därför vill du ansluta användarna i Los Angeles till Azure västra USA och användarna i New York till Azure östra USA.
- Detta fungerar för användarna på östkusten men inte för dem på västkusten. Problemet är följande:
  - På varje ExpressRoute-krets annonserar vi både prefixet i Azure för USA, östra (23.100.0.0/16) och prefixet i Azure för USA, västra (13.100.0.0/16).
  - Om du inte vet vilket prefix som är från vilken region behandlas inte prefixen på olika sätt.
  - Ditt WAN-nätverk kan anta att båda prefixen är närmare USA, östra än USA, västra. Därför dirigeras användare från båda kontor till ExpressRoute-kretsen i östra USA, vilket ger en bättre upplevelse för användare i Los Angeles-kontoret.

Ej optimerad anslutning för ![VPN](./media/migrate-best-practices-networking/bgp1.png)
*BGP-communities*

**Lösning:**

För att optimera routningen för båda kontoren måste du veta vilket prefix som är från Azure i USA, västra och vilket som är från Azure i USA, östra. Du kan koda informationen genom att använda BGP Community-värden.

- Du tilldelar ett unikt BGP Community-värde för varje Azure-region, t.ex. Till exempel ”12076:51004” för USA, östra och ”12076:51006” för USA, västra.
- Nu när det är klart vilket prefix som tillhör vilken Azure-region kan du konfigurera en prioriterad ExpressRoute-krets.
- Eftersom du använder BGP till att utbyta routningsinformation kan du påverka routningen med hjälp av BGP:s lokala inställningar.
- I vårt exempel kan du tilldela ett högre lokalt inställningsvärde för 13.100.0.0/16 i USA, västra än i USA, östra och på samma sätt ett högre lokalt inställningsvärde för 23.100.0.0/16 i USA, östra än i USA, västra.
- Den här konfigurationen säkerställer att användare i Los Angeles ansluter till Azure USA, västra med hjälp av den västra kretsen och användare New York ansluter till Azure USA, östra med hjälp av den östra kretsen. Routning är optimerad på båda sidorna.

Optimerad anslutning för ![VPN](./media/migrate-best-practices-networking/bgp2.png)
*BGP-communities*

**Läs mer:**

- [Lär dig](https://docs.microsoft.com/azure/expressroute/expressroute-optimize-routing) mer om att optimera routning.

## <a name="secure-vnets"></a>Säker virtuella nätverk

Ansvaret för att skydda virtuella nätverk delas mellan Microsoft och dig. Microsoft tillhandahåller många nätverksfunktioner, samt tjänster som hjälper till att hålla resurserna säkra. När du utformar säkerheten för virtuella nätverk bör du följa rekommenderade metoder för att implementera ett perimeternätverk, använda filtrerings- och säkerhetsgrupper, skydda åtkomsten till resurser och IP-adresser samt implementera sårbarhetsskydd.

**Läs mer:**

- [Få en översikt över](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices) metodtips för nätverkssäkerhet.
- [Lär dig](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#security) utforma säkra nätverk.

## <a name="best-practice-implement-an-azure-perimeter-network"></a>Bästa praxis: implementera ett Azure-perimeternätverk

Även om Microsoft investerar mycket i att skydda molninfrastrukturen måste du också skydda dina molntjänster och resursgrupper. En säkerhetsmetod med flera lager ger det bästa skyddet. Att upprätta ett perimeternätverk är en viktig del av den försvarsstrategin.

- Ett perimeternätverk skyddar interna nätverks resurser från ett ej betrott nätverk.
- Det är det yttersta skiktet som exponeras mot Internet. Den ligger vanligtvis mellan Internet och företagsinfrastrukturen, ofta med en viss typ av skydd på båda sidor.
- I en typisk nätverkstopologi för företag är kärninfrastrukturen kraftigt förstärkt vid perimetern med flera lager av säkerhetsanordningar. Gränserna för varje lager består av enheter och principtillämpningspunkter.
- Varje lager kan innehålla en kombination av nätverkssäkerhetslösningar som omfattar brandväggar, skydd mot Denial of service (DoS), intrångsidentifiering/intrångsskyddsystem (ID/IP-adresser) och VPN-enheter.
- Principtillämpning i perimeternätverket kan använda brandväggsprinciper, åtkomstkontrollistor (ACL:er) eller en speciell routning.
- Eftersom inkommande trafik kommer från Internet, fångas den upp och hanteras av en kombination av försvarslösningar som blockerar attacker och skadlig trafik, samtidigt som giltiga begäranden släpps in i nätverket.
- Inkommande trafik kan dirigeras direkt till resurser i perimeternätverket. Nätverksresursen för perimeternätverket kan sedan kommunicera med andra resurser djupare i nätverket och flytta trafiken framåt i nätverket efter verifieringen.

Följande bild visar ett exempel på ett enkelt undernätsperimeternätverk i ett företagsnätverk med två säkerhetsgränser.

*Nätverksdistribution av ![VPN](./media/migrate-best-practices-networking/perimeter.png)
-perimeter*

**Läs mer:**

- [Lär dig](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) mer om att distribuera ett perimeternätverk mellan Azure och ditt lokala datacenter.

## <a name="best-practice-filter-vnet-traffic-with-nsgs"></a>Bästa praxis: filtrera VNet-trafik med NSG: er

Nätverkssäkerhetsgrupper (NSG) innehåller flera inkommande och utgående säkerhetsregler som filtrerar trafik som går till och från resurser. Filtrering kan bero på källan och målets IP-adress, port och protokoll.

- En nätverkssäkerhetsgrupp innehåller säkerhetsregler som tillåter eller nekar inkommande nätverkstrafik till, eller utgående nätverkstrafik från, flera typer av Azure-resurser. För varje regel kan du ange källa och mål, port och protokoll.
- Nätverkssäkerhetsgruppens regler utvärderas utifrån prioritet baserat på 5 tuppel information (källa, källport, mål, målport och protokoll) för att tillåta eller neka trafik.
- En flödespost skapas för befintliga anslutningar. Kommunikation tillåts eller nekas baserat på flödespostens anslutningsstatus.
- Tack vare flödesposten kan nätverkssäkerhetsgruppen vara tillståndskänslig. Om du till exempel anger en utgående säkerhetsregel till en adress via port 80, behöver du inte ange en inkommande säkerhetsregel för svar på utgående trafik. Du behöver bara ange en inkommande säkerhetsregel om kommunikationen initieras externt.
- Även det motsatta gäller. Om inkommande trafik tillåts via en port, behöver du inte ange en utgående säkerhetsregel för svar på trafik via porten.
- Befintliga anslutningar avbryts inte när du tar bort en säkerhetsregel som aktiverade flödet. Trafikflöden avbryts när anslutningar har stoppats och ingen trafik passerar i endera riktning under minst ett par minuter.
- När du skapar NSG:er skapar du så få som möjligt men så många som behövs.

### <a name="best-practice-secure-northsouth-and-eastwest-traffic"></a>Bästa praxis: skydda Nord-/Syd-och östra/västra trafik

När du skyddar virtuella nätverk är det viktigt att tänka på angreppsvektorer.

- Att endast använda undernätverksgrupper förenklar din miljö, men skyddar endast trafiken i undernätet. Detta kallas nord-/sydtrafik.
- Trafik mellan virtuella datorer i samma undernät kallas öst-/västtrafik.
- Det är viktigt att använda båda former av skydd så att om en hackare får åtkomst utifrån stoppas de när de försöker ansluta med datorer som finns i samma undernät.

### <a name="use-service-tags-on-nsgs"></a>Använda tjänsttaggar på nätverkssäkerhetsgrupper

En tjänsttagg representerar en grupp med IP-adressprefix. Genom att använda en tjänsttagg kan du minimera komplexiteten när du skapar nätverkssäkerhetsgruppsregler.

- Du kan använda tjänsttaggar i stället för specifika IP-adresser när du skapar regler.
- Microsoft hanterar adressprefix som omfattas av tjänsttaggen och uppdaterar automatiskt tjänsttaggen när adresserna ändras.
- Du kan inte skapa egna tjänsttaggar och du kan inte heller ange vilka IP-adresser som ska finnas i en tagg.

Tjänsttaggar avlastar det manuella arbetet med att tilldela en regel till grupper av Azure-tjänster. Om du till exempel vill tillåta ett virtuellt undernät som innehåller webbservrar som har åtkomst till en Azure SQL Database kan du skapa en regel för utgående trafik till port 1433 **och** använda SQL tjänsttaggen.

- Den här **Sql**-taggen beskriver adressprefixen för tjänsterna Azure SQL Database och Azure SQL Data Warehouse.
- Om du anger **Sql** som värde tillåts eller nekas trafik till Sql.
- Om du bara vill tillåta åtkomst till **Sql** i en viss region anger du regionen. Om du till exempel vill tillåta åtkomst endast till Azure SQL Database i regionen östra USA anger du **Sql.EastUS** som tjänsttagg.
- Taggen representerar tjänsten, men inte specifika instanser av tjänsten. Taggen kan till exempel representera tjänsten Azure SQL Database, men representerar inte en specifik SQL-databas eller -server.
- Alla adressprefix som representeras av den här taggen är också representerade av taggen **Internet**.

**Läs mer:**

- [Läs mer om](https://docs.microsoft.com/azure/virtual-network/security-overview) nätverkssäkerhetsgrupper.
- [Granska](https://docs.microsoft.com/azure/virtual-network/security-overview#service-tags) tjänsttaggarna som är tillgängliga för nätverkssäkerhetsgrupper.

## <a name="best-practice-use-application-security-groups"></a>Bästa praxis: använda program säkerhets grupper

Med programsäkerhetsgrupper kan du konfigurera nätverkssäkerhet som ett naturligt tillägg av en appstruktur.

- Du kan gruppera virtuella datorer och definiera nätverkssäkerhetsprinciper baserat på programsäkerhetsgrupper.
- Programsäkerhetsgrupper gör att du kan återanvända din säkerhetsprincip i stor skala utan manuellt underhåll av explicita IP-adresser.
- Programsäkerhetsgrupper hanterar komplexiteten med explicita IP-adresser och flera regeluppsättningar så att du kan fokusera på affärslogik.

**Exempel:**

![Programsäkerhetsgrupp](./media/migrate-best-practices-networking/asg.png)
*Exempel på programsäkerhetsgrupp*

**Nätverksgränssnitt** | **Programsäkerhetsgrupp**
--- | ---
NIC1 | AsgWeb
NIC2 | AsgWeb
NIC3 | AsgLogic
NIC4 | AsgDb

- I vårt exempel tillhör varje nätverksgränssnitt bara en programsäkerhetsgrupp, men i själva verket kan ett gränssnitt tillhöra flera grupper i enlighet med Azures gränser.
- Inget av nätverksgränssnitten har en associerad nätverkssäkerhetsgrupp. NSG1 är associerat med båda undernäten och innehåller följande regler.

<!--markdownlint-disable MD033 -->

**Regelnamn** | **Syfte** | **Detaljer**
--- | --- | ---
Allow-HTTP-Inbound-Internet | Den här regeln krävs för att tillåta trafik från Internet till webbservrarna. Inkommande trafik från Internet nekas av standardsäkerhetsregeln DenyAllInbound. Därför krävs ingen ytterligare regel för programsäkerhetsgruppen AsgLogic eller AsgDb. | Prioritet: 100<br/><br/> Källa: Internet<br/><br/> Källport: *<br/><br/> Mål: AsgWeb<br/><br/> Målport: 80<br/><br/> Protokoll: TCP<br/><br/> Åtkomst: Tillåt.
Deny-Database-All | Standardsäkerhetsregeln AllowVNetInBound tillåter all kommunikation mellan resurser i samma virtuella nätverk. Därför krävs den här regeln för att neka trafik från alla resurser. | Prioritet: 120<br/><br/> Källa: *<br/><br/> Källport: *<br/><br/> Mål: AsgDb<br/><br/> Målport: 1433<br/><br/> Protokoll: alla<br/><br/> Åtkomst: neka.
Allow-Database-BusinessLogic | Tillåt trafik från programsäkerhetsgruppen AsgLogic till programsäkerhetsgruppen AsgDb. Prioriteten för den här regeln är högre än regeln Deny-Database-All och bearbetas före den regeln så att trafik från programsäkerhetsgruppen AsgLogic tillåts, medan all annan trafik blockeras. | Prioritet: 110<br/><br/> Källa: AsgLogic<br/><br/> Källport: *<br/><br/> Mål: AsgDb<br/><br/> Målport: 1433<br/><br/> Protokoll: TCP<br/><br/> Åtkomst: Tillåt.

<!--markdownlint-enable MD033 -->

- Reglerna som definierar en programsäkerhetsgrupp som källan eller målet tillämpas bara på nätverksgränssnitt som är medlemmar i programsäkerhetsgruppen. Om nätverksgränssnittet inte är medlem i en programsäkerhetsgrupp tillämpas inte regeln på nätverksgränssnittet, även om nätverkssäkerhetsgruppen är associerad med undernätet.

**Läs mer:**

- [Lär dig mer om](https://docs.microsoft.com/azure/virtual-network/security-overview#application-security-groups) programsäkerhetsgrupper.

### <a name="best-practice-secure-access-to-paas-using-vnet-service-endpoints"></a>Bästa praxis: säker åtkomst till PaaS med hjälp av VNet-tjänstens slut punkter

Med tjänstslutpunkter för Virtual Network får du ett utökat privat adressutrymme för det virtuella nätverket och identiteten för ditt VNet till Azure-tjänsterna, via en direktanslutning.

- Med slutpunkter kan du skydda dina kritiska Azure-tjänstresurser till endast dina virtuella nätverk. Trafik från ditt VNet till Azure-tjänsten förblir alltid på Microsoft Azure-stamnätverket.
- Privat adressutrymme för virtuella nätverk kan överlappa och kan därför inte användas för att unikt identifiera trafik från ditt virtuella nätverk.
- När tjänstslutpunkter aktiveras på ditt VNet kan du skydda Azure-tjänstresurser på ditt VNet genom att lägga till en regel för virtuellt nätverk för dina tjänstresurser. Detta ger bättre säkerhet genom att helt ta bort åtkomst till offentlig Internetåtkomst för resurser och endast tillåta nätverk från ditt virtuella nätverk.

![Tjänstslutpunkter](./media/migrate-best-practices-networking/endpoint.png)
*Tjänstslutpunkter*

**Läs mer:**

- [Läs mer om](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) tjänstslutpunkter för virtuella nätverk.

## <a name="best-practice-control-public-ip-addresses"></a>Bästa praxis: kontrol lera offentliga IP-adresser

Offentliga IP-adresser i Azure kan associeras med virtuella datorer, belastningsutjämnare, programgatewayer och VPN-gatewayer.

- Offentliga IP-adresser gör det möjligt för Internet-resurser att kommunicera ingående till Azure-resurser och Azure-resurser att kommunicera utgående till Internet.
- Offentliga IP-adresser skapas med en Basic- eller standard-SKU som har flera skillnader. Standard-SKU:er kan tilldelas till vilken tjänst som helst, men de brukar konfigureras på virtuella datorer, belastningsutjämnare och programgatewayer.
- Det är viktigt att observera att en grundläggande offentlig IP-adress inte automatiskt har en nätverkssäkerhetsgrupp konfigurerad. Du måste konfigurera din egen och tilldela regler för att kontrollera åtkomst. Standard-SKU IP-adresser har en nätverkssäkerhetsgrupp och regler tilldelade som standard.
- Det rekommenderas att virtuella datorer inte konfigureras med en offentlig IP-adress.
  - Om du behöver en öppen port bör den bara vara för webbtjänster, till exempel port 80 eller 443.
  - Standardportarna för fjärrhantering, till exempel SSH (22) och RDP (3389) bör vara inställda på neka med hjälp av nätverkssäkerhetsgrupper, tillsammans med alla andra portar.
- En bättre metod är att publicera virtuella datorer bakom en Azure Load Balancer eller Application Gateway. Om åtkomst till fjärrhanteringsportar behövs kan du använda åtkomst till virtuella datorer med just-in-time i Azure Security Center.

**Läs mer:**

- [Offentliga IP-adresser i Azure](https://docs.microsoft.com/azure/virtual-network/virtual-network-ip-addresses-overview-arm#public-ip-addresses)
- [Hantera åtkomst till virtuella datorer med just-in-Time](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)

## <a name="take-advantage-of-azure-security-features-for-networking"></a>Dra nytta av Azures säkerhetsfunktioner för nätverk

Azure har plattformsäkerhetsfunktioner som är enkla att använda och ger omfattande motåtgärder för vanliga nätverksattacker. Detta omfattar Azure Firewall, brandväggen för webbaserade program och Network Watcher.

## <a name="best-practice-deploy-azure-firewall"></a>Bästa praxis: Distribuera Azure-brandväggen

Azure Firewall är en hanterad molnbaserad nätverkssäkerhetstjänst som skyddar dina resurser på virtuella nätverk. Det är en helt tillståndskänslig hanterad brandvägg med inbyggd hög tillgänglighet och obegränsad molnskalbarhet.

*Azure Firewall* för ![tjänstslutpunkter](./media/migrate-best-practices-networking/firewall.png)


- Azure Firewall kan centralt skapa, framtvinga och logga principer för tillämpning och nätverksanslutning över prenumerationer och virtuella nätverk.
- Azure Firewall använder en statisk offentlig IP-adress för din virtuella nätverksresurser som tillåter att externa brandväggar identifierar trafik som kommer från ditt virtuella nätverk.
- Azure Firewall är helt integrerad med Azure Monitor för loggning och analys.
- Vi rekommenderar att du använder FQDN-taggar när du skapar regler för Azure Firewall.
  - En FQDN-tagg representerar en grupp med FQDN:er som är associerade med välkända Microsoft-tjänster.
  - Du kan använda en FQDN-tagg för att tillåta nödvändig utgående nätverkstrafik genom brandväggen.
- Om du till exempel vill tillåta nätverkstrafik från Windows Update manuellt genom brandväggen måste du skapa flera programregler. Med FQDN-taggar skapar du en programregel och inkluderar Windows Update-taggen. Med den här regeln på plats kan nätverkstrafik till Microsoft Windows Update-slutpunkter flöda genom brandväggen.

**Läs mer:**

- [Få en översikt](https://docs.microsoft.com/azure/firewall/overview) över Azure Firewall.
- [Lär dig](https://docs.microsoft.com/azure/firewall/fqdn-tags) mer om FQDN-taggar.

## <a name="best-practice-deploy-a-web-application-firewall-waf"></a>Bästa praxis: Distribuera en brand vägg för webbaserade program (WAF)

Webbprogram blir i allt större utsträckning föremål för attacker där kända svagheter i programmen utnyttjas. SQL-inmatningsattacker och skriptangrepp mellan webbplatser är vanliga. Det kan vara svårt att förhindra sådana attacker i programkoden och kräver ofta omfattande underhåll, korrigeringar och övervakning av flera skikt i programtopologin. Med en centraliserad brandvägg för webbaserade program blir det enklare att hantera säkerheten och programadministratörer får bättre möjligheter skydda mot hot och intrång. En brandvägg för webbprogram kan reagera snabbare på säkerhetshot genom att korrigera kända sårbarheter centralt istället för att skydda individuella webbprogram. Befintliga programgatewayer kan enkelt konverteras till en Application Gateway med brandväggen för webbprogram.

Brandväggen för webbaserade program (WAF) är en funktion i Azure Application Gateway.

- Brandväggen för webbaserade program tillhandahåller ett centraliserat skydd för dina webbprogram mot vanliga sårbarheter och hot.
- Brandväggen för webbaserade program skyddar utan att ändra serverdelskoden.
- Skyddar flera webbprogram samtidigt bakom en programgateway.
- Brandväggen för webbaserade program kan integreras med Azure Security Center.
- Du kan anpassa regler och regelgrupper för brandväggen för webbaserade program så att de passar dina appkrav.
- Vi rekommenderar att du använder en brandvägg för webbaserade program framför alla program som är riktade mot webben, inklusive program på virtuella Azure-datorer eller som Azure App Service.

**Läs mer:**

- [Läs mer om](https://docs.microsoft.com/azure/application-gateway/waf-overview) brandvägg för webbaserade program.
- [Granska](https://docs.microsoft.com/azure/application-gateway/application-gateway-waf-configuration) begränsningar och undantag för brandväggen för webbaserade program.

## <a name="best-practice-implement-azure-network-watcher"></a>Bästa praxis: implementera Azure Network Watcher

Azure Network Watcher innehåller verktyg för att övervaka resurser och kommunikation i ett virtuellt Azure-nätverk. Du kan till exempel övervaka kommunikation mellan en virtuell dator och en slutpunkt, till exempel en annan virtuell dator eller FQDN, visa resurser och resursrelationer i ett virtuellt nätverk eller diagnostisera problem hos nätverkstrafiken.

![Network Watcher](./media/migrate-best-practices-networking/network-watcher.png)
*Network Watcher*

- Med Network Watcher kan du övervaka och diagnostisera nätverksproblem utan att du behöver logga in på dina virtuella datorer.
- Du kan lösa ut infångade paket genom att ställa in aviseringar och få åtkomst till prestandainformation i realtid på paketnivå. När du ser ett problem kan du undersöka i detalj.
- Vi rekommenderar att du använder Network Watcher för att granska flödesloggar för nätverkssäkerhetsgrupper.
  - Med Network Watchers flödesloggar för nätverkssäkerhetsgrupp kan du visa information om inkommande och utgående IP-trafik via en nätverkssäkerhetsgrupp.
  - Flödesloggar skrivs i JSON-format.
  - Flödes loggar visar utgående och inkommande flöden per regel, det nätverksgränssnitt (NIC) som flödet använder, 5-tupel information om flödet (käll-/mål-IP, käll-/målport och protokoll) och om trafiken tilläts eller nekades.

**Läs mer:**

- [Få en översikt](https://docs.microsoft.com/azure/network-watcher) över Network Watcher.
- [Läs mer](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) om flödesloggar för nätverkssäkerhetsgrupper.

## <a name="use-partner-tools-in-the-azure-marketplace"></a>Använd partnerlösningar från Azure Marketplace

För mer komplexa nätverkstopologier kan du använda säkerhetsprodukter från Microsoft-partners, särskilt virtuella nätverks installationer (NVA).

- En virtuell nätverksinstallation är en virtuell dator som utför en nätverksfunktion, till exempel en brandvägg, WAN-optimering eller annan nätverksfunktion.
- NVA stärker säkerheten och nätverksfunktionerna på virtuella nätverk. De kan distribueras för att tillhandahålla brandväggar med hög tillgänglighet, skydd mot intrång, intrångsidentifiering, brandväggar för webbaserade program (WAF), WAN-optimering, routning, belastningsutjämning, VPN, certifikathantering, Active Directory och multifaktorautentisering.
- NVA är tillgängligt från flera leverantörer på [Azure Marketplace.](https://azuremarketplace.microsoft.com)

## <a name="best-practice-implement-firewalls-and-nvas-in-hub-networks"></a>Bästa praxis: implementera brand väggar och NVA i hubb nätverk

I hubben hanteras perimeternätverket (med åtkomst till Internet) normalt via en Azure-brandvägg, en brandväggsgrupp eller en brandvägg för webbaserade program (WAF). Ta följande jämförelser som exempel.

<!--markdownlint-disable MD033 -->

**Brandväggstyp** | **Detaljer**
--- | ---
Brandvägg för webbaserade program | Webbprogram är vanliga och tenderar att drabbas av sårbarheter och potentiella hot.<br/><br/> Brandväggar för webbaserade program är utformade för att identifiera attacker mot webbprogram (HTTP/HTTPS) mer specifikt än en vanlig brandvägg.<br/><br/> Jämfört med traditionell brandväggsteknik har brandväggar för webbaserade program specifika funktioner som skyddar inre webbservrar mot hot.
Azure Firewall | Azure Firewall använder likt NVA-brandväggsgrupper en gemensam administrationsmekanism och en uppsättning säkerhetsregler som skyddar arbetsbelastningar i ekernätverk och kontrollerar åtkomst till lokala nätverk.<br/><br/> Azure Firewall har inbyggd skalbarhet.
NVA-brandväggar | NVA-brandväggsgrupper använder likt Azure Firewall en gemensam administrationsmekanism och en uppsättning säkerhetsregler som skyddar arbetsbelastningar i ekernätverk och kontrollerar åtkomst till lokala nätverk.<br/><br/> NVA-brandväggar kan skalas manuellt bakom en belastningsutjämnare.<br/><br/> Även om en NVA-brandvägg har mindre specialiserad programvara än en brandvägg för webbaserade program, har den ett bredare programdefinitionsområde för att filtrera och inspektera all typ av ingående och utgående trafik.<br/><br/> Om du vill använda NVA kan du hitta dem på Azure Marketplace.

<!--markdownlint-enable MD033 -->

Vi rekommenderar att du använder en Azure Firewall (eller NVA) för trafik som kommer från Internet och en annan för trafik som kommer från lokala nätverk.

- Att bara ha ett brandväggssystem är en säkerhetsrisk, eftersom det inte ger någon säkerhetsperimeter mellan de två uppsättningarna med nätverkstrafik.
- När separata brandväggslager används minskas komplexiteten för kontroll av säkerhetsregler och tydliggör vilka regler som motsvarar respektive inkommande nätverksbegäran.

**Läs mer:**

- [Lär dig](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) mer om att använda NVA i ett virtuellt Azure-nätverk.

## <a name="next-steps"></a>Nästa steg

Läs andra metodtips:

- [Metodtips](./migrate-best-practices-security-management.md) för säkerhet och hantering efter migrering.
- [Metodtips](./migrate-best-practices-costs.md) för kostnadshantering efter migrering.
