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
ms.openlocfilehash: 8fbdd20c435d4aed8a284174d813abc8d391171b
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022856"
---
# <a name="best-practices-to-set-up-networking-for-workloads-migrated-to-azure"></a>Bästa praxis för att konfigurera nätverk för arbetsbelastningar migreras till Azure

Som du planerar och utformar för migrering, förutom migrering, är en av de viktigaste stegen design och implementering av Azure-nätverk. Den här artikeln beskriver Metodtips för nätverk när du migrerar till IaaS och PaaS-implementeringar i Azure.

> [!IMPORTANT]
> Bästa praxis och yttranden som beskrivs i den här artikeln baseras på Azure-plattformen och bearbeta funktioner som är tillgängliga vid tidpunkten för skrivning. Funktioner och möjligheter ändras med tiden. Inte alla rekommendationer som kan tillämpas för din distribution, så Välj dem som fungerar för dig.

## <a name="design-virtual-networks"></a>Utforma virtuella nätverk

Azure ger virtuella nätverk (Vnet):

- Azure-resurser kommunicerar privat, direkt och säkert med varandra över virtuella nätverk.
- Du kan konfigurera slutpunkten anslutningar i virtuella nätverk för virtuella datorer och tjänster som kräver internet-kommunikation.
- Ett virtuellt nätverk är en logisk avgränsning av Azure-molnet som är dedikerad för din prenumeration.
- Du kan implementera flera virtuella nätverk inom varje Azure-prenumeration och Azure-region.
- Varje virtuellt nätverk är isolerat från andra virtuella nätverk.
- Virtuella nätverk kan innehålla privata och offentliga IP-adresser som definieras i [RFC 1918](https://tools.ietf.org/html/rfc1918), uttryckt i CIDR-format. Offentliga IP-adresser som anges i ett virtuellt nätverks adressutrymme är inte direkt tillgängliga från Internet.
- Virtuella nätverk kan ansluta till varandra med hjälp av VNet-peering. Anslutna virtuella nätverk kan vara i samma eller olika regioner. Därmed kan resurser i ett virtuellt nätverk ansluta till resurser i andra virtuella nätverk.
- Azure dirigerar trafik mellan undernät inom ett virtuellt nätverk, anslutna virtuella nätverk, lokala nätverk och Internet, som standard.

När du planerar din topologi för det virtuella nätverket bör du fundera på hur du vill organisera IP-adressutrymme, implementera ett nav- och ekernätverk, segmentera virtuella nätverk i undernät, konfigurera DNS och implementera Azure-åtkomstzoner.

## <a name="best-practice-plan-ip-addressing"></a>Metodtips: Planera IP-adress

När du skapar virtuella nätverk som en del av migreringen är det viktigt att planera det virtuella nätverkets IP-adressutrymme.

- Du bör tilldela ett adressutrymme som inte är större än ett CIDR-intervall för /16 för varje virtuellt nätverk. Virtuella nätverk kan användningen av 65536 IP-adresser och tilldela ett prefix som är mindre än/16 skulle leda till förlust av IP-adresser. Det är viktigt att inte slösa bort IP-adresser, även om de finns i de privata intervall som definieras av RFC 1918.
- Virtuella nätverkets adressutrymme får inte överlappa med lokala nätverksintervall.
- Network Address Translation (NAT) bör inte användas.
- Överlappande adresser kan orsaka nätverk som inte kan anslutas och routning som inte fungerar korrekt. Om nätverk överlappar behöver du ändra designen på nätverket eller använda network address translation (NAT).

**Lära sig mer:**

- [Få en översikt](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) av virtuella Azure-nätverk.
- [Läs](https://docs.microsoft.com/azure/virtual-network/virtual-networks-faq) nätverk vanliga frågor och svar.
- [Lär dig](https://docs.microsoft.com/azure/azure-subscription-service-limits?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) mer om nätverksbegränsningar.

## <a name="best-practice-implement-a-hub-and-spoke-network-topology"></a>Metodtips: Implementera en hubb- och eker-nätverkstopologi

En hubb- och eker-nätverkstopologi är ett sätt att isolera arbetsbelastningar samtidigt som man delar tjänster som identitet och säkerhet.

- Hubben är ett virtuellt Azure-nätverk som fungerar som en central punkt för anslutningen.
- Ekrarna är virtuella nätverk som ansluter till det virtuella hubbnätverket med hjälp av VNet-peering.
- Delade tjänster distribueras i hubben medan individuella arbetsbelastningar distribueras som ekrar.

Tänk också på följande:

- Implementera en topologi med nav och ekrar i Azure centraliserar vanliga tjänster, till exempel anslutningar till lokala nätverk, brandväggar och isolering mellan virtuella nätverk. Det virtuella hubbnätverket ger en central plats för anslutning till lokala nätverk och en plats för värd services användning av arbetsbelastningar som finns i virtuella ekernätverken.
- En konfiguration med nav och ekrar används vanligtvis av större företag. Mindre nätverk kan du välja en enklare design att spara på kostnaderna och komplexiteten.
- Virtuella nätverk ekrar kan användas till att isolera arbetsbelastningar, med varje eker som hanteras separat från andra ekrar. Varje arbetsbelastning kan innehålla flera nivåer och flera undernät som är anslutna med Azure-belastningsutjämnare.
- Virtuella nätverk med hubbar och ekrar kan implementeras i olika resursgrupper och även i olika prenumerationer. När du använder virtuella peer-nätverk med olika prenumerationer kan prenumerationerna associeras med samma eller olika Azure Active Directory-klienter (Azure AD). Det möjliggör en decentraliserad hantering av varje arbetsbelastning, samtidigt som tjänster i det virtuella hubbnätverket delas.

![Ändringshantering](./media/migrate-best-practices-networking/hub-spoke.png)
*topologi för NAV och ekrar*

**Lära sig mer:**

- [Läs mer om](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) en topologi med nav och ekrar.
- Få nätverksrekommendationer för att köra Azure [Windows](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/windows-vm) och [Linux](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/linux-vm) virtuella datorer.
- [Läs mer om](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) VNet-peering (virtuella nätverk).

## <a name="best-practice-design-subnets"></a>Metodtips: Utforma undernät

För att skapa en isolering inom ett virtuellt undernät ska du segmentera det i ett eller flera undernät och allokera en del av det virtuella nätverkets adressutrymme till varje undernät.

- Du kan skapa flera undernät inom varje virtuellt nätverk.
- Som standard nätverkstrafik Azure dirigerar mellan alla undernät i ett virtuellt nätverk.
- Undernät baserat på ditt beslut baserat på dina tekniska och organisatoriska krav.
- Du skapar undernät med CIDR-notering.
- När du bestämmer dig för nätverkets adressintervall för undernät, är det viktigt att notera att Azure behåller fem IP-adresser från varje undernät som inte får återanvändas. Till exempel om du skapar det minsta tillgängliga undernätet/29 (med åtta IP-adresser), behåller Azure fem adresser, så du behöver bara tre användbara adresser som kan tilldelas till värdar i undernätet.
- I de flesta fall rekommenderas att använda /28 som minsta undernät.

**Exempel:**

Tabellen visar ett exempel på ett virtuellt nätverk med ett adressutrymme på 10.245.16.0/20 segmenterat i undernät för en planerad migrering.

**Undernät** | **CIDR** | **Adresser** | **Använd**
--- | --- | --- | ---
DEV-FE-EUS2 | 10.245.16.0/22 | 1019 | Virtuella datorer på klientsida/webbnivå
DEV-APP-EUS2 | 10.245.20.0/22 | 1019 | App-nivå virtuella datorer
DEV-DB-EUS2 | 10.245.24.0/23 | 507 | Virtuella

**Lära sig mer:**

- [Lär dig](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#segmentation) mer om att utforma undernät.
- [Läs](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure) hur ett fiktivt företag (Contoso) förberedde sin nätverksinfrastruktur för migrering.

## <a name="best-practice-set-up-a-dns-server"></a>Metodtips: Konfigurera en DNS-server

Azure lägger till en DNS-server som standard när du distribuerar ett virtuellt nätverk. På så sätt kan du snabbt skapa virtuella nätverk och distribuera resurser. Den här DNS-servern tillhandahåller dock endast tjänster till resurserna på det virtuella nätverket. Om du vill ansluta flera virtuella nätverk tillsammans eller ansluta till en lokal server från virtuella nätverk behöver du ytterligare name resolution funktioner. Du kanske till exempel behöver Active Directory för DNS-namnmatchning mellan virtuella nätverk. Om du vill göra detta måste distribuera du dina egna anpassade DNS-server i Azure.

- DNS-servrar i ett virtuellt nätverk kan vidarebefordra DNS-frågor till de rekursiva matchare i Azure. På så sätt kan du matcha värdnamn inom det virtuella nätverket. Exempelvis kan en domänkontrollant som kör i Azure svara på DNS-frågor för egna domäner och vidarebefordra alla frågor till Azure.
- DNS-vidarebefordran kan virtuella datorer finns i både lokala resurser (via domänkontrollanten) och Azure-tillhandahållen värdnamn (med vidarebefordraren). Åtkomst till de rekursiva matchare i Azure anges med hjälp av den virtuella IP-adressen 168.63.129.16.
- Vidarebefordran av DNS kan du även gör DNS-matchning mellan virtuella nätverk, och att lokala datorer för att matcha värdnamn som tillhandahålls av Azure.
  - För att lösa ett VM-värdnamn, DNS-server-dator måste finnas i samma virtuella nätverk och konfigureras för att vidarebefordra värd-namnfrågor till Azure.
  - Eftersom DNS-suffix är olika i varje virtuellt nätverk kan använda du regler för villkorlig vidarebefordran för att skicka DNS-frågor till rätt VNet för matchning.
- När du använder en egen DNS-servrar, kan du ange flera DNS-servrar för varje virtuellt nätverk. Du kan också ange flera DNS-servrar per nätverksgränssnitt (för Azure Resource Manager) eller per molntjänst (för den klassiska distributionsmodellen).
- DNS-servrar som angetts för en nätverkstjänst för gränssnittet eller molnet företräde framför DNS-servrar som angetts för det virtuella nätverket.
- Du kan ange DNS-servrar för ett virtuellt nätverk och ett nätverksgränssnitt i Azure Resource Manager-distributionsmodellen, men den bästa metoden är att använda inställningen för endast virtuella nätverk.

    ![DNS-servrar](./media/migrate-best-practices-networking/dns2.png) *DNS-servrar för det virtuella nätverket*

**Lära sig mer:**

- [Lär dig mer om](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure) namnmatchning när du använder en egen DNS-server.
- [Läs mer om](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-subscriptions) namngivningsregler och begränsningar för DNS.

## <a name="best-practice-set-up-availability-zones"></a>Metodtips: Konfigurera tillgänglighetszoner

Tillgänglighetszoner ökar hög tillgänglighet för att skydda dina appar och data från datacenterfel.

- Tillgänglighetszoner är unika, fysiska platser inom en Azure-region.
- Varje zon består av en eller flera datacenter som är utrustade med oberoende kraft, kylning och nätverkstjänster.
- För att säkerställa återhämtning, finns det minst tre separata zoner i alla aktiverade regioner.
- Fysisk avgränsning av tillgänglighetszoner inom en region skyddar program och data mot datacenterproblem.
- Zonredundant tjänster replikera dina program och data i olika tillgänglighetszoner och skydda mot enskilda felpunkter. – Azure erbjuder ett serviceavtal på 99,99% drifttid för virtuella datorer med tillgänglighetszoner.

    ![Tillgänglighetszon](./media/migrate-best-practices-networking/availability-zone.png) *tillgänglighetszon*

- Du kan planera och skapa hög tillgänglighet i din migreringsarkitektur genom att samordna beräkning, lagring, nätverk och dataresurser inom en zon och replikera dem i andra zoner. Azuretjänster som har stöd för tillgänglighetszoner kan delas in i två kategorier:
  - Zonindelade tjänster: Du kan associera en resurs med en specifik zon. Till exempel virtuella datorer, hanterade diskar, IP-adresser).
  - Zonredundant lagring: Resursen replikeras automatiskt mellan zoner. Till exempel, zonredundant lagring, Azure SQL Database.
- Du kan distribuera en standard Azure belastningsutjämnade med internet-riktade arbetsbelastningar eller app-nivåerna för att ge feltolerans för zonindelade.

    ![Belastningsutjämnare](./media/migrate-best-practices-networking/load-balancer.png) *belastningsutjämnare*

**Lära sig mer:**

- [Få en översikt](https://docs.microsoft.com/azure/availability-zones/az-overview) av tillgänglighetszoner.

## <a name="design-hybrid-cloud-networking"></a>Design hybridmolnet nätverk

Det är viktigt att ansluta lokala företagets nätverk till Azure för en lyckad migrering. Detta skapar en ständig-anslutning kallas ett hybridmoln nätverk, där erbjuds från Azure cloud till företagsanvändare. Det finns två alternativ för att skapa den här typen av nätverk:

- **Plats-till-plats-VPN:** Du etablerar en plats-till-platsanslutning mellan den kompatibla lokala VPN-enheten och en Azure VPN Gateway som distribueras i ett virtuellt nätverk. Alla auktoriserade lokala resurser kan komma åt virtuella nätverk. Plats-till-platskommunikation skickas via en krypterad tunnel via Internet.
- **Azure ExpressRoute:** Du etablerar en Azure ExpressRoute mellan ditt lokala nätverk och Azure, via en ExpressRoute-partner. Den här anslutningen är privat och trafiken går inte via Internet.

**Lära sig mer:**

- [Lär dig](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/vpn) mer om nätverk med hybridmoln.

## <a name="best-practice-implement-a-highly-available-site-to-site-vpn"></a>Metodtips: Implementera en plats-till-plats-VPN med hög tillgänglighet

Om du vill implementera en plats-till-plats-VPN skapar du en VPN-gateway i Azure.

- En VPN-gateway är en viss typ av VNet-gateway som används för att skicka krypterad trafik mellan ett virtuellt Azure nätverk och en lokal plats via det offentliga Internet.
- Du kan också använda en VPN-gateway för att skicka krypterad trafik mellan virtuella Azure-nätverk över Microsoft-nätverket.
- Varje virtuellt nätverk kan bara ha en VPN-gateway.
- Du kan skapa flera anslutningar till samma VPN-gateway. När du skapar flera anslutningar, delar alla VPN-tunnlar den tillgängliga bandbredden.
- Varje Azure VPN-gateway består av två instanser i en aktiv-standby-konfiguration.
  - När det utförs ett planerat underhåll eller uppstår ett oplanerat avbrott för en aktiv instans inträffar redundans och standby-instansen tar över automatiskt. Plats-till-platsanslutningen eller anslutningen mellan virtuella nätverk återupptas.
  - Växlingen leder till ett kort avbrott.
  - Vid ett planerat underhåll återställs anslutningen inom 10 till 15 sekunder.
  - Vid ett oplanerat avbrott tar det lite längre tid att återställa anslutningen. I värsta fall kan det ta en till en och en halv minut.
  - P2S VPN-klientanslutningar till gatewayen kopplas från och användarna måste ansluta på nytt från klientdatorerna.

När du konfigurerar ett plats-till-plats-VPN gör du följande:

- Du behöver ett virtuellt nätverk vars adressintervall inte överlappar med det lokala nätverket som VPN-anslutningen ska ansluta till.
- Du skapar ett gateway-undernät i nätverket.
- Du skapar en VPN-gateway, ange gateway-typ (VPN) och om gatewayen är principbaserad eller routningsbaserad. En RouteBased VPN rekommenderas som mer kapacitet och framtidssäkrar.
- Du skapar en lokal nätverksgateway på plats och konfigurera den lokala VPN-enheten.
- Du skapar en växling vid fel plats-till-plats VPN-anslutning mellan VNet-gateway och den lokala enheten. Om du använder ruttbaserad VPN får aktivt-passivt eller aktiv-aktiv-anslutningar till Azure. Ruttbaserad också stöder både plats-till-plats (från valfri dator) och anslutningar för punkt-till-plats (från en enda dator) samtidigt.
- Du kan ange vilken gateway-SKU som du vill använda. Detta beror på din arbetsbelastningskraven, genomflöden, funktioner och serviceavtal.
- BGP (border gateway protocol) är en valfri funktion som du kan använda med Azure ExpressRoute och routningsbaserade VPN-gatewayer för att sprida lokala BGP-vägar till dina virtuella nätverk.

![VPN](./media/migrate-best-practices-networking/vpn.png)
*plats-till-plats-VPN*

**Lära sig mer:**

- [Granska](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) kompatibla lokala VPN-enheter.
- [Få en översikt](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) VPN-gatewayer.
- [Lär dig mer om](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-highlyavailable) VPN-anslutningar med hög tillgänglighet.
- [Lär dig mer om](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) planerar och utformar en VPN-gateway.
- [Granska](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsku) VPN gateway-inställningar.
- [Granska](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#gwsku) gateway SKU: er.
- [Läs om](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-bgp-overview) hur du konfigurerar BGP med Azure VPN-gatewayer.

### <a name="best-practice-configure-a-gateway-for-vpn-gateways"></a>Metodtips: Konfigurera en gateway för VPN-gatewayer

När du skapar en VPN-gateway i Azure måste du använda ett särskilt undernät med namnet GatewaySubnet. När du skapar det här undernätet Obs dessa metodtips:

- Prefixlängden för gateway-undernätet kan ha maximalt prefixlängden 29 (till exempel 10.119.255.248/29). Aktuella rekommendationen är att du använder prefixlängden 27 (till exempel 10.119.255.224/27).
- När du definierar adressutrymmet för gatewayundernätet kan använda den sista delen av virtuella nätverkets adressutrymme.
- När du använder Azure-GatewaySubnet, aldrig distribuera virtuella datorer eller andra enheter, till exempel Application Gateway till gateway-undernätet.
- Tilldela inte en nätverkssäkerhetsgrupp (NSG) till det här undernätet. Det gör att gatewayen slutar att fungera.

**Lära sig mer:**

- [Använd det här verktyget](https://gallery.technet.microsoft.com/scriptcenter/Address-prefix-calculator-a94b6eed) för att fastställa IP-adressutrymmet.

## <a name="best-practice-implement-azure-virtual-wan-for-branch-offices"></a>Metodtips: Implementera Azure Virtual WAN för avdelningskontor

För flera VPN-anslutningar är Azure Virtual WAN en nätverkstjänst som tillhandahåller optimerade och automatiserade anslutningar mellan olika platser via Azure.

- Med Virtual WAN kan du ansluta och konfigurera platsspecifika enheter så att de kommunicerar med Azure. Detta kan göras manuellt eller med enheter från önskad leverantör via en Virtual WAN-partner.
- Om du använder prioriterade providern enheter får enkel användning, anslutningar och konfiguration hantering.
- Azure WAN inbyggda instrumentpanelen innehåller omedelbara felsökning insikter som sparar tid och ger ett enkelt sätt att spåra storskaliga plats-till-plats-anslutning.

**Läs mer:** 
[Läs mer om](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about) Azure Virtual WAN.

### <a name="best-practice-implement-expressroute-for-mission-critical-connections"></a>Metodtips: Implementera ExpressRoute för verksamhetskritiska anslutningar

Azure ExpressRoute-tjänsten utökar din lokala infrastruktur till Microsoft Cloud genom att skapa privata anslutningar mellan virtuella Azure-datacenter och lokala nätverk.

- ExpressRoute-anslutningar kan befinna sig över ett valfritt-till-valfritt-nätverk (IP-VPN), ett Ethernet-nätverk från punkt till punkt eller via en anslutningsleverantör. De går inte via offentliga internet.
- ExpressRoute-anslutningar har högre säkerhet, tillförlitlighet och högre hastigheter (upp till 10 Gbit/s), tillsammans med konsekvent svarstid.
- ExpressRoute är användbart för virtuella datacenter som kunder kan få fördelarna med regler för efterlevnad som är associerade med privata anslutningar.
- Du kan ansluta direkt till Microsoft-routrarna vid 100Gbps för större bandbreddsbehov ExpressRoute Direct.
- ExpressRoute använder BGP för att utbyta vägar mellan lokala nätverk, Azure-instanser och Microsoft offentliga adresser.

Att distribuera ExpressRoute-anslutningar innebär vanligtvis att man registrerar sig hos en ExpressRoute-tjänstleverantör. Det är vanligt att först använda plats-till-plats-VPN för att skapa en anslutning mellan det virtuella datacentret och den lokala resursen. Sedan migrerar man till en ExpressRoute-anslutning när en fysisk anslutning till din tjänsteleverantör är etablerad.

**Läs mer:**

- [Läs en översikt](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) över ExpressRoute.
- [Lär dig mer](https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about) om ExpressRoute Direct.

### <a name="best-practice-optimize-expressroute-routing-with-bgp-communities"></a>Metodtips: Optimera ExpressRoute-routning med BGP-communityer

När du har flera ExpressRoute-kretsar måste ha du mer än en sökväg för att ansluta till Microsoft. Därför kan en icke-optimal routning inträffa – vilket innebär att din trafik får en längre sökväg till Microsoft och Microsoft till nätverket. Ju längre nätverkssökvägen är, desto längre svarstid. Svarstiden har direkt inverkan på programmens prestanda och användarupplevelse.

**Exempel:**

Låt oss titta på ett exempel:

- Anta att du har två kontor i USA, ett i Los Angeles och ett i New York.
- Dina kontor är anslutna i WAN, vilket kan vara antingen ditt eget stamnät eller leverantörens IP VPN.
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

För att optimera routningen för båda kontoren måste du veta vilket prefix som är från Azure i USA, västra och vilket som är från Azure i USA, östra. Du kan koda den här informationen med hjälp av BGP community-värden.

- Du tilldelar ett unikt BGP Community-värde för varje Azure-region, t.ex. Till exempel ”12076:51004” för USA, östra och ”12076:51006” för USA, västra.
- Nu när det är klart vilket prefix som tillhör vilken Azure-region kan du konfigurera en prioriterad ExpressRoute-krets.
- Eftersom du använder BGP till att utbyta routningsinformation kan du påverka routningen med hjälp av BGP:s lokala inställningar.
- I vårt exempel kan du tilldela ett högre lokalt inställningsvärde för 13.100.0.0/16 i USA, västra än i USA, östra och på samma sätt ett högre lokalt inställningsvärde för 23.100.0.0/16 i USA, östra än i USA, västra.
- Den här konfigurationen garanterar att när både sökvägar till Microsoft, användarna i Los Angeles ska ansluta till Azure i västra USA västra-krets och användarna New York ansluta till Azure i östra USA Öst-krets. Routning är optimerad på båda sidorna.

![VPN](./media/migrate-best-practices-networking/bgp2.png)
*BGP-communities optimerade anslutning*

**Läs mer:**

- [Lär dig](https://docs.microsoft.com/azure/expressroute/expressroute-optimize-routing) mer om att optimera routning.

## <a name="securing-vnets"></a>Skydda virtuella nätverk

Ansvaret för att skydda virtuella nätverk delas mellan Microsoft och dig. Microsoft tillhandahåller många nätverksfunktioner, samt tjänster som hjälper till att hålla resurserna säkra. När du utformar säkerheten för virtuella nätverk bör du följa rekommenderade metoder för att implementera ett perimeternätverk, använda filtrerings- och säkerhetsgrupper, skydda åtkomsten till resurser och IP-adresser samt implementera sårbarhetsskydd.

**Läs mer:**

- [Få en översikt](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices) bra metoder för nätverkssäkerhet.
- [Lär dig](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#security) utforma säkra nätverk.

## <a name="best-practice-implement-an-azure-perimeter-network"></a>Metodtips: Implementera ett Azure-perimeternätverk

Även om Microsoft investerar mycket i att skydda molninfrastrukturen måste du också skydda dina molntjänster och resursgrupper. En flerskiktiga strategi inom säkerhet ger det bästa skyddet. Sätta ett perimeternätverk är en viktig del av den defense-strategin.

- Ett perimeternätverk skyddar interna nätverksresurser från ett icke betrott nätverk.
- Det är den yttersta lagret som är exponerade mot internet. Den allmänt sitter mellan internet och företagsinfrastruktur, vanligtvis med någon form av skydd på båda sidorna.
- I en typisk företags-nätverkstopologi spikas kraftigt grundläggande infrastruktur på perimetrar med flera lager av säkerhetsenheter. Gränsen för varje nivå består av enheter och tillämpningspunkter för principen.
- Varje lager kan innehålla en kombination av microsoftbaserade nätverkssäkerhetslösningar med brandväggar, Denial of Service (DoS) förebygga, intrång identifiering/intrång protection system (IDS/IPS) och VPN-enheter.
- Genomförande av principer i perimeternätverket kan använda principer för brandväggen, åtkomstkontrollistor (ACL) eller specifika routning.
- När inkommande trafik anländer från internet, har det fångas upp och hanteras av en kombination av lösning för skydd för block attacker och skadlig trafik samtidigt som legitima begäranden till nätverket.
- Inkommande trafik kan vidarebefordra direkt till resurser i perimeternätverket. Nätverksresursen perimeternätverket kan sedan kommunicera med andra resurser som är djupare i nätverket, flytta vidarebefordra trafik till nätverk efter valideringen.

Följande bild visar ett exempel på ett enda undernät perimeternätverk i ett företagsnätverk, med två säkerhetsgränser.

![VPN](./media/migrate-best-practices-networking/perimeter.png)
*Perimeter nätverksdistribution*

**Lära sig mer:**

- [Lär dig](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) mer om att distribuera ett perimeternätverk mellan Azure och ditt lokala datacenter.

## <a name="best-practice-filter-vnet-traffic-with-nsgs"></a>Metodtips: Filtrera virtuell nätverkstrafik med NSG:er

Nätverkssäkerhetsgrupper (NSG) innehåller flera inkommande och utgående säkerhetsregler som filtrerar trafik som går till och från resurser. Filtrering kan vara av källa och mål-IP-adress, port och protokoll.

- Nätverkssäkerhetsgrupper innehåller säkerhetsregler som tillåter eller nekar inkommande trafik till (eller utgående nätverkstrafik från) flera typer av Azure-resurser. För varje regel kan du ange källa och mål, port och protokoll.
- NSG-reglerna utvärderas efter prioritet med fem-tuppel-information (källa, källport, mål, målport och protokoll) att tillåta eller neka trafik.
- En flödespost skapas för befintliga anslutningar. Kommunikation tillåts eller nekas baserat på flödespostens anslutningsstatus.
- En post i flödet kan en NSG tillståndskänsliga. Exempel: Om du anger en utgående säkerhetsregel till en adress via port 80, behöver du inte en inkommande säkerhetsregel att svara på utgående trafik. Du behöver bara ange en inkommande säkerhetsregel om kommunikationen initieras externt.
- Även det motsatta gäller. Om inkommande trafik tillåts via en port, behöver du inte ange en utgående Säkerhetsregel för svar på trafik via porten.
- Befintliga anslutningar avbryts inte när du tar bort en säkerhetsregel som aktiverats flödet. Trafikflöden avbryts när anslutningar har stoppats och ingen trafik flödar i båda riktningarna för minst ett par minuter.
- När du skapar NSG:er skapar du så få som möjligt men så många som behövs.

### <a name="best-practice-secure-northsouth-and-eastwest-traffic"></a>Metodtips: Skydda trafik nord/syd och öst/väst

När du skyddar virtuella nätverk är det viktigt att tänka på angreppsvektorer.

- Med hjälp av endast undernät NSG: er förenklar din miljö, men endast säkrar trafik till undernätet. Detta kallas för Nord-Syd trafik.
- Trafik mellan virtuella datorer i samma undernät kallas öst-/västtrafik.
- Det är viktigt att använda båda former av skydd så att om en hackare får åtkomst utifrån stoppas de när de försöker ansluta med datorer som finns i samma undernät.

### <a name="use-service-tags-on-nsgs"></a>Använda tjänsttaggar på nätverkssäkerhetsgrupper

En tjänsttagg representerar en grupp med IP-adressprefix. Med hjälp av en tjänsttagg hjälper till att minska komplexiteten när du skapar NSG-regler.

- Du kan använda servicetaggar i stället för specifika IP-adresser när du skapar regler.
- Microsoft hanterar adressprefix som är associerade med en tjänsttaggen och uppdaterar automatiskt tjänsttaggen när adresserna ändras.
- Du kan inte skapa egna tjänsttaggar eller ange vilka IP-adresser som ingår i en tagg.

Tjänsttaggar Ta manuellt arbete från tilldelning av en regel till grupper i Azure-tjänster. Till exempel om du vill tillåta ett virtuellt nätverk undernät som innehåller servrar för Webbåtkomst till en Azure SQL Database du kan skapa en regel för utgående trafik till port 1433, och använda den **Sql** servicetagg.

- Detta **Sql** taggen anger adressprefix för tjänsterna Azure SQL Database och Azure SQL Data Warehouse.
- Om du anger **Sql** som värde, trafik tillåts eller nekas till Sql.
- Om du bara vill tillåta åtkomst till **Sql** i en viss region kan du ange den regionen. Till exempel om du vill tillåta endast åtkomst till Azure SQL Database i regionen östra USA, du kan ange **Sql.EastUS** som tjänsttagg.
- Taggen representerar tjänsten, men inte specifika instanser av tjänsten. Till exempel taggen representerar tjänsten Azure SQL Database, men representerar inte en viss SQL-databas eller en server.
- Alla adressprefix som representeras av den här taggen är också representerade av taggen **Internet**.

**Lära sig mer:**

- [Läs mer om](https://docs.microsoft.com/azure/virtual-network/security-overview) NSG: er.
- [Granska](https://docs.microsoft.com/azure/virtual-network/security-overview#service-tags) tjänsttaggarna som är tillgängliga för nätverkssäkerhetsgrupper.

## <a name="best-practice-use-application-security-groups"></a>Metodtips: Använd programsäkerhetsgrupper

Med programsäkerhetsgrupper kan du konfigurera nätverkssäkerhet som ett naturligt tillägg av en appstruktur.

- Du kan gruppera virtuella datorer och definiera nätverkssäkerhetsprinciper baserat på programsäkerhetsgrupper.
- Programsäkerhetsgrupper kan du återanvända din säkerhetsprincip i stor skala utan manuellt underhåll av explicita IP-adresser.
- Programsäkerhetsgrupper hanterar komplexiteten med explicita IP-adresser och flera regeluppsättningar så att du kan fokusera på affärslogik.

**Exempel:**

![Programsäkerhetsgrupp](./media/migrate-best-practices-networking/asg.png)
*Exempel på programsäkerhetsgrupp*

**Nätverksgränssnitt** | **Programsäkerhetsgruppen**
--- | ---
NIC1 | AsgWeb
NIC2 | AsgWeb
NIC3 | AsgLogic
NIC4 | AsgDb

- Varje nätverksgränssnitt som hör till endast en programsäkerhetsgrupp i vårt exempel, men i själva verket ett gränssnitt kan tillhöra flera grupper, i enlighet med Azure-gränser.
- Ingen av nätverksgränssnitt har någon associerad NSG. NSG1 är kopplad till både undernät och innehåller följande regler.

<!--markdownlint-disable MD033 -->

**Regelnamn** | **Syfte** | **Detaljer**
--- | --- | ---
Allow-HTTP-Inbound-Internet | Tillåta trafik från internet till webbservrar. Inkommande trafik från Internet nekas av standardsäkerhetsregeln DenyAllInbound. Därför krävs ingen ytterligare regel för programsäkerhetsgruppen AsgLogic eller AsgDb. | Prioritet: 100<br/><br/> Källa: Internet<br/><br/> Källport: *<br/><br/> Mål: AsgWeb<br/><br/> Målport: 80<br/><br/> Protokoll: TCP<br/><br/> Åtkomst: Tillåt.
Deny-Database-All | Standardsäkerhetsregeln AllowVNetInBound tillåter all kommunikation mellan resurser i samma virtuella nätverk. Därför krävs den här regeln för att neka trafik från alla resurser. | Prioritet: 120<br/><br/> Källa: *<br/><br/> Källport: *<br/><br/> Mål: AsgDb<br/><br/> Målport: 1433<br/><br/> Protokoll: Alla<br/><br/> Åtkomst: Neka.
Allow-Database-BusinessLogic | Tillåt trafik från programsäkerhetsgruppen AsgLogic till programsäkerhetsgruppen AsgDb. Prioriteten för den här regeln är högre än regeln Deny-Database-All och bearbetas före den regeln så att trafik från programsäkerhetsgruppen AsgLogic tillåts, medan all annan trafik blockeras. | Prioritet: 110<br/><br/> Källa: AsgLogic<br/><br/> Källport: *<br/><br/> Mål: AsgDb<br/><br/> Målport: 1433<br/><br/> Protokoll: TCP<br/><br/> Åtkomst: Tillåt.

<!--markdownlint-enable MD033 -->

- Reglerna som definierar en programsäkerhetsgrupp som källan eller målet tillämpas bara på nätverksgränssnitt som är medlemmar i programsäkerhetsgruppen. Om nätverksgränssnittet inte är medlem i en programsäkerhetsgrupp tillämpas inte regeln på nätverksgränssnittet, även om nätverkssäkerhetsgruppen är associerad med undernätet.

**Lära sig mer:**

- [Lär dig mer om](https://docs.microsoft.com/azure/virtual-network/security-overview#application-security-groups) programsäkerhetsgrupper.

### <a name="best-practice-secure-access-to-paas-using-vnet-service-endpoints"></a>Metodtips: Säker åtkomst till PaaS med hjälp av tjänstslutpunkter för virtuella nätverk

Med tjänstslutpunkter för Virtual Network får du ett utökat privat adressutrymme för det virtuella nätverket och identiteten för ditt VNet till Azure-tjänsterna, via en direktanslutning.

- Slutpunkter kan du skydda dina kritiska Azure-resurser till dina virtuella nätverk endast. Trafik från ditt VNet till Azure-tjänsten förblir alltid på Microsoft Azure-stamnätverket.
- Privat adressutrymme för virtuellt nätverk kan finnas överlappande och därför användas inte för att identifiera trafik som kommer från ett virtuellt nätverk.
- När tjänstslutpunkter är aktiverade i ditt virtuella nätverk, kan du skydda Azure-tjänstresurser genom att lägga till en VNet-regel service-resurser. Detta ger bättre säkerhet genom att helt ta bort den offentliga Internetåtkomsten till resurser och tillåter trafik från ditt virtuella nätverk.

![Tjänstslutpunkter](./media/migrate-best-practices-networking/endpoint.png)
*tjänstens slutpunkter*

**Lära sig mer:**

- [Läs mer om](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) tjänstslutpunkter för virtuella nätverk.

## <a name="best-practice-control-public-ip-addresses"></a>Metodtips: Statiska offentliga IP-adresser

Offentliga IP-adresser i Azure kan associeras med virtuella datorer, belastningsutjämnare, programgatewayer och VPN-gatewayer.

- Offentliga IP-adresser gör det möjligt för Internet-resurser att kommunicera ingående till Azure-resurser och Azure-resurser att kommunicera utgående till Internet.
- Offentliga IP-adresser skapas med en Basic- eller standard-SKU som har flera skillnader. Standard-SKU:er kan tilldelas till vilken tjänst som helst, men de brukar konfigureras på virtuella datorer, belastningsutjämnare och programgatewayer.
- Det är viktigt att Observera att en grundläggande offentliga IP-adress inte har en NSG som konfigureras automatiskt. Du måste konfigurera en egen och tilldela regler för åtkomstkontroll. Standard-SKU-IP-adresser har en NSG och regler som tilldelas som standard.
- Som bästa praxis bör inte virtuella datorer konfigureras med en offentlig IP-adress.
  - Om du behöver en port som öppnas, ska det endast för webbtjänster, till exempel port 80 eller 443.
  - Standard remote hanteringsportar som SSH (22) och RDP (port 3389) ska anges för att neka, tillsammans med alla andra portar, med hjälp av NSG: er.
- En bättre metod är att placera virtuella datorer bakom en Azure load balancer eller application gateway. Om åtkomst till fjärranslutna hanteringsportar krävs, kan du använda åtkomst till just-in-time-virtuella datorer i Azure Security Center.

**Lära sig mer:**

- [Lär dig mer om](https://docs.microsoft.com/azure/virtual-network/virtual-network-ip-addresses-overview-arm#public-ip-addresses) offentliga IP-adresser i Azure.
- [Läs mer om](https://docs.microsoft.com/azure/security-center/security-center-just-in-time) Azure Security Center – Åtkomst till virtuella Just-in-Time-datorer.

## <a name="take-advantage-of-azure-security-features-for-networking"></a>Dra nytta av Azures säkerhetsfunktioner för nätverk

Azure har plattformsäkerhetsfunktioner som är enkla att använda och ger omfattande motåtgärder för vanliga nätverksattacker. Detta omfattar Azure Firewall, brandväggen för webbaserade program och Network Watcher.

## <a name="best-practice-deploy-azure-firewall"></a>Metodtips: Distribuera Azure Firewall

Azure Firewall är en hanterad molnbaserad nätverkssäkerhetstjänst som skyddar dina resurser på virtuella nätverk. Det är en helt tillståndskänslig hanterad brandvägg med inbyggd hög tillgänglighet och obegränsad molnskalbarhet.

*Azure Firewall* för ![tjänstslutpunkter](./media/migrate-best-practices-networking/firewall.png)


- Azure Firewall kan centralt skapa, framtvinga och logga principer för tillämpning och nätverksanslutning över prenumerationer och virtuella nätverk.
- Azure Firewall använder en statisk offentlig IP-adress för din virtuella nätverksresurser som tillåter att externa brandväggar identifierar trafik som kommer från ditt virtuella nätverk.
- Azure-brandväggen är helt integrerat med Azure Monitor för loggning och analyser.
- Som bästa praxis när du skapar brandväggsregler för Azure att använda FQDN-taggar för att skapa regler.
  - Ett FQDN-taggen representerar en grupp med FQDN: er som är associerade med välkända Microsoft-tjänster.
  - Du kan använda en FQDN-tagg för att tillåta nödvändiga utgående nätverkstrafik genom brandväggen.
- Om du vill tillåta manuellt Windows Update-nätverkstrafik via brandväggen, skulle du behöva skapa flera regler. Med hjälp av FQDN taggar, du skapar en regel för programmet och inkluderar uppdateringar för Windows-taggen. Med den här regeln är på plats kan nätverkstrafik till Microsoft Windows Update-slutpunkter flöda via brandväggen.

**Lära sig mer:**

- [Få en översikt](https://docs.microsoft.com/azure/firewall/overview) för Azure-brandväggen.
- [Lär dig](https://docs.microsoft.com/azure/firewall/fqdn-tags) mer om FQDN-taggar.

## <a name="best-practice-deploy-a-web-application-firewall-waf"></a>Metodtips: Distribuera en brandvägg för webbaserade program (WAF)

Webbprogram blir i allt större utsträckning föremål för attacker där kända svagheter i programmen utnyttjas. Kryphål omfattar SQL-inmatningsattacker och cross-site skriptattacker. Att förhindra sådana attacker i programkoden kan vara en utmaning och kan kräver ofta omfattande underhåll, korrigeringar och övervakning av flera skikt i programtopologin. En centraliserad brandvägg hjälper till att göra det mycket enklare säkerhetshantering och hjälper app-administratörer skydda mot intrång. En brandvägg för webbaserade program kan reagera på säkerhetshot snabbare genom att åtgärda kända säkerhetsrisker på en central plats i stället för att skydda enskilt webbprogram. Befintliga programgatewayer kan enkelt konverteras till en Application Gateway med brandväggen för webbprogram.

Brandväggen för webbaserade program (WAF) är en funktion i Azure Application Gateway.

- Brandväggen för webbaserade program tillhandahåller ett centraliserat skydd för dina webbprogram mot vanliga sårbarheter och hot.
- Brandväggen för webbaserade program skyddar utan att ändra serverdelskoden.
- Skyddar flera webbprogram samtidigt bakom en programgateway.
- Brandväggen för webbaserade program kan integreras med Azure Security Center.
- Du kan anpassa WAF-regler och regelgrupper som passar dina krav för appar.
- Som bästa praxis bör du använda en WAF framför i web-riktade appar, inklusive appar på Azure Virtual Machines eller som en Azure App Service.

**Lära sig mer:**

- [Lär dig mer om](https://docs.microsoft.com/azure/application-gateway/waf-overview) WAF.
- [Granska](https://docs.microsoft.com/azure/application-gateway/application-gateway-waf-configuration) begränsningar och undantag för brandväggen för webbaserade program.

## <a name="best-practice-implement-azure-network-watcher"></a>Metodtips: Implementera Azure Network Watcher

Azure Network Watcher innehåller verktyg för att övervaka resurser och kommunikation i ett virtuellt Azure-nätverk. Du kan till exempel övervaka kommunikation mellan en virtuell dator och en slutpunkt, t.ex en annan virtuell dator eller FQDN, samt visa resurser och resursrelationer i ett virtuellt nätverk, eller diagnostisera nätverksproblem trafik.

![Network Watcher](./media/migrate-best-practices-networking/network-watcher.png)
*Network Watcher*

- Med Network Watcher kan du övervaka och diagnostisera nätverksproblem utan att logga in på virtuella datorer.
- Du kan utlösa infångade paket genom att ställa in aviseringar och få åtkomst till prestandainformation i realtid på paketnivå. När du ser ett problem kan du undersöka i detalj.
- Vi rekommenderar att du använder Network Watcher för att granska flödesloggar för nätverkssäkerhetsgrupper.
  - Med Network Watchers flödesloggar för nätverkssäkerhetsgrupp kan du visa information om inkommande och utgående IP-trafik via en nätverkssäkerhetsgrupp.
  - Flödesloggar skrivs i JSON-format.
  - Flödes loggar visar utgående och inkommande flöden per regel, det nätverksgränssnitt (NIC) som flödet använder, 5-tupel information om flödet (käll-/mål-IP, käll-/målport och protokoll) och om trafiken tilläts eller nekades.

**Lära sig mer:**

- [Få en översikt](https://docs.microsoft.com/azure/network-watcher) i Network Watcher.
- [Läs mer](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) om NSG flow loggar.

## <a name="use-partner-tools-in-the-azure-marketplace"></a>Använda partner-verktygen i Azure Marketplace

Du kan använda säkerhetsprodukter från Microsofts partner i viss virtuella nätverksinstallationer (Nva) för mer avancerade nätverkstopologier.

- En NVA är en virtuell dator som utför en nätverksfunktion, till exempel en brandvägg, WAN-optimering eller annan nätverksfunktion.
- NVA stärker säkerheten och nätverksfunktionerna på virtuella nätverk. De kan distribueras för att tillhandahålla brandväggar med hög tillgänglighet, skydd mot intrång, intrångsidentifiering, brandväggar för webbaserade program (WAF), WAN-optimering, routning, belastningsutjämning, VPN, certifikathantering, Active Directory och multifaktorautentisering.
- NVA är tillgängligt från flera leverantörer på [Azure Marketplace.](https://azuremarketplace.microsoft.com)

## <a name="best-practice-implement-firewalls-and-nvas-in-hub-networks"></a>Metodtips: Implementera brandväggar och NVA i hubbnätverk

I hubben hanteras perimeternätverket (med åtkomst till Internet) normalt via en Azure-brandvägg, en brandväggsgrupp eller en brandvägg för webbaserade program (WAF). Ta följande jämförelser som exempel.

<!--markdownlint-disable MD033 -->

**Typ av brandvägg** | **Detaljer**
--- | ---
Brandvägg för webbaserade program | Webbprogram är vanliga och tenderar att drabbas av sårbarheter och potentiella hot.<br/><br/> Brandväggar för webbaserade program är utformade för att identifiera attacker mot webbprogram (HTTP/HTTPS) mer specifikt än en vanlig brandvägg.<br/><br/> Jämfört med traditionell brandväggsteknik har brandväggar för webbaserade program specifika funktioner som skyddar inre webbservrar mot hot.
Azure Firewall | Azure Firewall använder likt NVA-brandväggsgrupper en gemensam administrationsmekanism och en uppsättning säkerhetsregler som skyddar arbetsbelastningar i ekernätverk och kontrollerar åtkomst till lokala nätverk.<br/><br/> Azure Firewall har inbyggd skalbarhet.
NVA-brandväggar | Som Azure brandväggen NVA ha brandväggen servergrupper vanliga mekanism för administration och en uppsättning säkerhetsregler för att skydda arbetsbelastningar som finns i eker-nätverk och vill kontrollera åtkomsten till lokala nätverk.<br/><br/> NVA-brandväggar kan skalas manuellt bakom en belastningsutjämnare.<br/><br/> Även om en NVA-brandväggen har mindre särskild programvara än WAF har bredare omfång för programmet att filtrera och granska alla typer av trafik i ut- och ingångsanspråk.<br/><br/> Om du vill använda NVA som du hittar dem på Azure Marketplace.

<!--markdownlint-enable MD033 -->

Vi rekommenderar att du använder en uppsättning Azure brandväggar (eller nva: er) för trafik från internet och en annan för trafik som skickas på plats.

- Använda endast en uppsättning brandväggar för både utgör en säkerhetsrisk, eftersom det ger någon säkerhetsperimeter mellan de två uppsättningarna med nätverkstrafik.
- Med separat brandvägg lager minskar komplexiteten för kontroll av säkerhetsregler och det är tydligt vilka regler som motsvarar vilka inkommande nätverksbegäran.

**Lära sig mer:**

- [Lär dig mer om](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) med nva: er i ett virtuellt Azure nätverk.

## <a name="next-steps"></a>Nästa steg

Granska andra metodtips:

- [Bästa praxis](./migrate-best-practices-security-management.md) för säkerhet och hantering efter migreringen.
- [Bästa praxis](./migrate-best-practices-costs.md) för kostnadshantering efter migreringen.
