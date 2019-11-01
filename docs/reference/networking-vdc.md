---
title: 'Virtuella Data Center: ett nätverks perspektiv'
description: Lär dig hur du skapar ett virtuellt Data Center i Azure.
author: tracsman
ms.author: jonor
ms.date: 06/12/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: reference
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: cbd72c04c7d938aae41e20fae82a29b731f4b256
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/31/2019
ms.locfileid: "73240097"
---
# <a name="virtual-datacenters-a-network-perspective"></a>Virtuella Data Center: ett nätverks perspektiv

## <a name="overview"></a>Översikt

Migrering av lokala program till Azure ger organisationer fördelarna med en säker och kostnads effektiv infrastruktur, även om programmen migreras med minimala ändringar. För att få ut mesta möjliga flexibilitet med molnbaserad data behandling, måste företag utveckla sina arkitekturer för att dra nytta av Azure-funktionerna.

Microsoft Azure erbjuder storskaliga tjänster och infrastruktur med funktioner och tillförlitlighet i företags klass. Dessa tjänster och infrastruktur erbjuder många alternativ i hybrid anslutning så att kunderna kan välja att få åtkomst till dem via offentliga Internet eller via en privat Azure ExpressRoute-anslutning. Microsoft-partner tillhandahåller även förbättrade funktioner genom att erbjuda säkerhets tjänster och virtuella enheter som är optimerade för att köras i Azure.

Kunderna kan välja att få åtkomst till dessa moln tjänster antingen via Internet eller med Azure ExpressRoute, som tillhandahåller privat nätverks anslutning. Med Microsoft Azure-plattformen kan kunderna sömlöst utöka sin infrastruktur till molnet och bygga på flera nivåer. Microsoft-partner tillhandahåller även förbättrade funktioner genom att erbjuda säkerhets tjänster och virtuella enheter som är optimerade för att köras i Azure.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-the-virtual-datacenter"></a>Vad är det virtuella data centret?

Molnet var i grunden en plattform för att vara värd för offentliga program. Företag började förstå molnets värde och började flytta interna affärs program till molnet. De här typerna av program medförde ytterligare säkerhet, tillförlitlighet, prestanda och kostnads överväganden som kräver ytterligare flexibilitet i hur moln tjänster levererades. Detta förberedelse är ett sätt för nya infrastruktur-och nätverks tjänster som har utformats för att ge den här flexibiliteten, men även nya funktioner för skalning, haveri beredskap och andra överväganden.

Moln lösningar har först utformats för att vara värdar för enkla, relativt isolerade program i det offentliga spektrumet. Den här metoden fungerade bra under några få år. Sedan var fördelarna med moln lösningar uppenbara och flera storskaliga arbets belastningar fanns i molnet. Adressering av säkerhet, tillförlitlighet, prestanda och kostnader för distributioner i en eller flera regioner blev avgörande under hela livs cykeln för moln tjänsten.

I följande moln distributions diagram visas ett exempel på en säkerhets lucka i den **röda rutan**. Den **gula rutan** visar plats för optimering av virtuella nätverks enheter över arbets belastningar.

![0][0]

Ett virtuellt Data Center är ett koncept som är nödvändigt för skalning för att stödja företags arbets belastningar samtidigt som du kan balansera behovet av att lösa de problem som introducerades när du stöder storskaliga program i det offentliga molnet.

En implementering av ett virtuellt Data Center representerar inte bara program arbets belastningarna i molnet, utan även nätverk, säkerhet, hantering och infrastruktur (till exempel DNS-och katalog tjänster). Eftersom mer av ett företags arbets belastningar flyttas till Azure är det viktigt att tänka på den stödda infrastrukturen och de objekt som dessa arbets belastningar är placerade i. Att tänka på när resurser struktureras kan undvika spridningen av hundratals "arbets belastnings öar" som måste hanteras separat med oberoende data flöde, säkerhets modeller och utmaningar för efterlevnad.

Det virtuella Data Center konceptet är en uppsättning rekommendationer och metod tips för att implementera en samling separata men relaterade entiteter med vanliga stöd för funktioner, funktioner och infrastruktur. Genom att visa dina arbets belastningar via lins i ett virtuellt Data Center kan du utnyttja minskad kostnad på grund av skalbarhet, optimerad säkerhet genom komponent-och data flödes centralisering, samt enklare granskningar, hantering och efterlevnad.

> [!NOTE]
> Det är viktigt att förstå att ett virtuellt Data Center **inte** är en diskret Azure-produkt, men kombinationen av olika funktioner och funktioner för att uppfylla dina specifika krav. Ett virtuellt Data Center är ett sätt att tänka på dina arbets belastningar och Azure-användning för att maximera dina resurser och förmågor i molnet. Det är en modulär metod för att bygga upp IT-tjänster i Azure samtidigt som företagets organisatoriska roller och ansvars områden respekteras.

En implementering av virtuella Data Center kan hjälpa företag att få arbets belastningar och program till Azure i följande scenarier:

- Var värd för flera relaterade arbets belastningar.
- Migrera arbets belastningar från en lokal miljö till Azure.
- Implementera delade eller centraliserade säkerhets-och åtkomst krav i arbets belastningar.
- Blanda Azure DevOps och centralisera det för ett stort företag.

Nyckeln för att låsa upp fördelarna med ett virtuellt Data Center är en central hubb och eker-nätverkstopologi med en blandning av Azure-tjänster och-funktioner:

- [Azure Virtual Network][VNet],
- [Nätverks säkerhets grupper][network-security-groups],
- [Peering för virtuella nätverk][VNetPeering],
- [Användardefinierade vägar][user-defined-routes]och
- Azure Identity med [rollbaserad åtkomst kontroll (RBAC)][RBAC] och eventuellt [Azure-brandvägg][AzFW], [Azure DNS][DNS], Azure- [frontend][AFD]och [Azure Virtual WAN][vWAN].

## <a name="who-should-implement-a-virtual-datacenter"></a>Vem ska implementera ett virtuellt Data Center?

Alla Azure-kunder som har beslutat att använda molnet kan dra nytta av effektiviteten i att konfigurera en uppsättning resurser för vanlig användning av alla program. Beroende på omfattning kan även enskilda program dra nytta av de mönster och komponenter som används för att bygga en implementering av ett virtuellt Data Center.

Om din organisation har centraliserade team eller avdelningar för IT, nätverk, säkerhet eller efterlevnad kan du implementera ett virtuellt Data Center för att upprätthålla princip punkter, ansvars fördelning och se till att de underliggande komponenterna är enhetliga samtidigt som de ger program team som hög frihet och kontroll som passar dina behov.

Organisationer som vill DevOps kan också använda virtuella Data Center koncept för att tillhandahålla auktoriserade fickor för Azure-resurser och se till att de har total kontroll i gruppen (antingen prenumeration eller resurs grupp i en gemensam prenumeration), men Nätverks-och säkerhets gränser förblir kompatibla som definieras av en centraliserad princip i ett nav-VNet och en resurs grupp.

<!-- markdownlint-enable MD026 -->

## <a name="considerations-for-implementing-a-virtual-datacenter"></a>Överväganden för att implementera ett virtuellt Data Center

När du skapar en virtuell Data Center implementering finns det flera olika Pivot-frågor att tänka på:

### <a name="identity-and-directory-service"></a>Identitets-och katalog tjänst

Identitets-och katalog tjänster är en viktig aspekt av alla data Center, både lokalt och i molnet. Identiteten är relaterad till alla aspekter av åtkomst och auktorisering av tjänster inom en implementering av ett virtuellt Data Center. För att säkerställa att endast auktoriserade användare och processer får åtkomst till ditt Azure-konto och-resurser använder Azure flera typer av autentiseringsuppgifter för autentisering. Detta inkluderar lösen ord (för att få åtkomst till Azure-kontot), kryptografiska nycklar, digitala signaturer och certifikat. [Azure Multi-Factor Authentication][multi-factor-authentication] är ett extra säkerhets lager för att få åtkomst till Azure-tjänster. Multi-Factor Authentication ger stark autentisering med en rad enkla verifierings alternativ (telefonsamtal, SMS eller meddelande om mobilapp) och låter kunderna välja den metod som de föredrar.

Alla stora företag behöver definiera en identitets hanterings process som beskriver hanteringen av enskilda identiteter, autentisering, auktorisering, roller och behörigheter inom eller över deras virtuella Data Center implementering. Målen för den här processen bör vara att öka säkerheten och produktiviteten samtidigt som du minskar kostnaderna, stillestånds tiden och repetitiva manuella uppgifter.

Företags organisationer kan kräva en krävande blandning av tjänster för olika affärs linjer och anställda har ofta olika roller när de är involverade i olika projekt. Ett virtuellt Data Center kräver ett utmärkt samarbete mellan olika team, var och en med olika roll definitioner, för att få system som kör med en bättre styrning. Matrisen med ansvar, åtkomst och rättigheter kan vara komplex. Identitets hantering i ett virtuellt Data Center implementeras via [Azure Active Directory (Azure AD)][azure-ad] och rollbaserad åtkomst kontroll (RBAC).

En katalog tjänst är en infrastruktur för delad information som söker, hanterar, administrerar och ordnar de dagliga objekten och nätverks resurserna. Dessa resurser kan omfatta volymer, mappar, filer, skrivare, användare, grupper, enheter och andra objekt. Varje resurs i nätverket betraktas som ett objekt av katalog servern. Information om en resurs lagras som en samling attribut som är associerade med resursen eller objektet.

Alla Microsoft Online Business Services förlitar sig på Azure Active Directory (Azure AD) för inloggning och andra identitets behov. Azure Active Directory är en omfattande molnlösning för identitets- och åtkomsthantering med hög tillgänglighet som kombinerar kärnkatalogstjänster, avancerad identitetsstyrning och programåtkomsthantering. Azure AD kan integreras med lokala Active Directory för att möjliggöra enkel inloggning för alla molnbaserade och lokalt värdbaserade program. Användarattribut för lokala Active Directory kan synkroniseras automatiskt till Azure AD.

En enda global administratör krävs inte för att tilldela alla behörigheter i en implementering av Virtual Data Center. I stället kan varje enskild avdelning, grupp av användare eller tjänster i katalog tjänsten ha de behörigheter som krävs för att hantera sina egna resurser inom en implementering av ett virtuellt Data Center. Strukturerings behörighet kräver balansering. För många behörigheter kan hindra prestanda effektiviteten och för få eller lösa behörigheter kan öka säkerhets riskerna. Azure rollbaserad åtkomst kontroll (RBAC) hjälper till att lösa det här problemet genom att erbjuda detaljerad åtkomst hantering för resurser i en implementering av Virtual Data Center.

#### <a name="security-infrastructure"></a>Säkerhets infrastruktur

Säkerhets infrastrukturen syftar på en uppdelning av trafiken i en virtuell Data Center implementerings aktuella virtuella nätverks segment. Den här infrastrukturen anger hur ingress och utgående ska kontrol leras i en implementering av Virtual Data Center. Azure baseras på en arkitektur för flera innehavare som förhindrar obehörig och oavsiktlig trafik mellan distributioner med hjälp av VNet-isolering, åtkomst kontrol listor (ACL: er), belastningsutjämnare, IP-filter och trafik flödes principer. NAT (Network Address Translation) separerar intern nätverks trafik från extern trafik.

Azure-infrastrukturen allokerar infrastruktur resurser till klient arbets belastningar och hanterar kommunikation till och från virtuella datorer (VM). Azure-hypervisorn använder minnes-och process separationer mellan virtuella datorer och dirigerar nätverks trafik på ett säkert sätt till gäst operativ systemets klienter.

#### <a name="connectivity-to-the-cloud"></a>Anslutning till molnet

En implementering av Virtual Data Center kräver anslutning till externa nätverk för att erbjuda tjänster till kunder, partner och interna användare. Detta behov av anslutning avser inte bara Internet, utan även för lokala nätverk och data Center.

Kunderna styr vilka tjänster som har åtkomst till och är tillgängliga från det offentliga Internet med hjälp av [Azure-brandväggen][AzFW] eller andra typer av virtuella nätverks installationer (NVA), anpassade routningsprinciperna med hjälp av [användardefinierade vägar][user-defined-routes]och nätverk filtrering med hjälp av [nätverks säkerhets grupper][network-security-groups]. Vi rekommenderar att alla resurser som är riktade mot Internet också skyddas av [Azure DDoS Protection standard][DDoS].

Företag kan behöva ansluta sin implementering av ett virtuellt Data Center till lokala data Center eller andra resurser. Den här anslutningen mellan Azure och lokala nätverk är en viktig aspekt när du utformar en effektiv arkitektur. Företag har två olika sätt att skapa denna sammanlänkning: överföring via Internet eller via privata direkta anslutningar.

En [**Azure plats-till-plats-VPN**][VPN] är en sammanlänknings tjänst via Internet mellan lokala nätverk och en virtuell Data Center implementering, upprättad genom säkra krypterade anslutningar (IPSec/IKE-tunnlar). Azure plats-till-plats-anslutningen är flexibel, snabb att skapa och kräver inte ytterligare inköp eftersom alla anslutningar ansluter via Internet.

För stora mängder VPN-anslutningar är [**Azure Virtual WAN**][vWAN] en nätverks tjänst som tillhandahåller optimerad och automatiserad anslutning från gren till gren via Azure. Med det virtuella WAN-nätverket kan du ansluta till konfigurera avdelnings enheter för att kommunicera med Azure. Anslutning och konfiguration kan göras antingen manuellt eller genom att använda prioriterade providers enheter via en virtuell WAN-partner. Med prioriterade Provider-enheter kan du enkelt använda, förenkla anslutning och konfigurations hantering. Med de inbyggda instrumentpanelerna i Azure WAN kan du snabbt felsöka problem och enkelt visa anslutningar mellan platser i hög skala.

[**ExpressRoute**][ExR] är en Azure-anslutbarhet som möjliggör privata anslutningar mellan en implementering av ett virtuellt Data Center och alla lokala nätverk. ExpressRoute-anslutningar går inte via det offentliga Internet och ger högre säkerhet, tillförlitlighet och högre hastighet (upp till 10 Gbit/s) tillsammans med konsekvent svars tid. ExpressRoute är användbart för implementeringar av virtuella Data Center, eftersom ExpressRoute-kunder kan få fördelar med efterlevnadsprinciper som är kopplade till privata anslutningar. Med [ExpressRoute Direct][ExRD]kan du ansluta direkt till Microsoft-routrar på 100 Gbit/s för kunder med större bandbredds behov.

Att distribuera ExpressRoute-anslutningar innebär vanligtvis att man registrerar sig hos en ExpressRoute-tjänstleverantör. För kunder som behöver starta snabbt, är det vanligt att först använda plats-till-plats-VPN för att upprätta anslutningar mellan en implementering av virtuella Data Center och lokala resurser och sedan migrera till ExpressRoute-anslutningen när den fysiska sammanlänkning med din tjänst leverantör har slutförts.

#### <a name="connectivity-within-the-cloud"></a>*Anslutning i molnet*

[Virtuella nätverk][VNet] och [VNet-peering][VNetPeering] är de grundläggande nätverks anslutnings tjänsterna i en implementering av Virtual Data Center. Ett VNet garanterar en naturlig gränser för isolering för virtuella Data Center resurser och VNet-peering möjliggör kommunikation mellan olika virtuella nätverk inom samma Azure-region eller till och med mellan regioner. Trafik kontroll i ett virtuellt nätverk och mellan virtuella nätverk måste matcha en uppsättning säkerhets regler som anges i åtkomst kontrol listor ([nätverks säkerhets grupper][network-security-groups]), [virtuella nätverks][NVA]installationer och anpassade routningstabeller ([användardefinierade vägar][user-defined-routes]).

## <a name="virtual-datacenter-overview"></a>Översikt över Virtual Data Center

### <a name="topology"></a>Topologi

*Hubb och eker* är en modell för att utforma nätverk sto pol Ogin för en implementering av ett virtuellt Data Center.

![1][1]

Som du ser kan två typer av nav och eker-design användas i Azure. För kommunikation, delade resurser och centraliserad säkerhets princip (VNet-hubb i diagrammet) eller en virtuell WAN-typ (virtuellt WAN-nätverk i diagrammet) för storskalig kommunikation mellan gren-till-gren och gren-till-Azure.

En hubb är den centrala nätverks zonen som styr och kontrollerar inkommande eller utgående trafik mellan olika zoner: Internet, lokalt och ekrar. NAV-och eker-topologin ger IT-avdelningen ett effektivt sätt att tillämpa säkerhets principer på en central plats. Det minskar också risken för felaktig konfiguration och exponering.

Hubben innehåller ofta de gemensamma tjänst komponenter som används av ekrarna. Följande exempel är gemensamma centrala tjänster:

- Windows Active Directory-infrastrukturen, som krävs för användarautentisering av tredje part som kommer åt från ej betrodda nätverk innan de får åtkomst till arbets belastningarna i ekern. Det inkluderar relaterade Active Directory Federation Services (AD FS).
- En DNS-tjänst för att matcha namn på arbetsbelastningen i ekrarna, för att komma åt resurser lokalt och på Internet om [Azure DNS][DNS] inte används.
- En PKI (Public Key Infrastructure) för att implementera enkel inloggning på arbetsbelastningar.
- Flödeskontroll av TCP- och UDP-trafik mellan ekrarnas nätverkszoner och Internet.
- Flödeskontroll mellan ekrar och lokalt.
- Vid behov, flödeskontroll mellan två ekrar.

Det virtuella data centret minskar den totala kostnaden genom att använda infrastrukturen för delad hubb mellan flera ekrar.

Rollen för varje eker kan vara värd för olika typer av arbetsbelastningar. Ekrarna ger också en modulär metod för upprepningsbara distributioner av samma arbetsbelastningar. Exempel på detta är utveckling och testning, testning av användargodkännande, förproduktion och produktion. Ekrarna kan också särskilja och aktivera olika grupper i din organisation. Ett exempel är Azure DevOps-grupper. I en eker är det möjligt att distribuera en grundläggande arbetsbelastning eller komplexa arbetsbelastningar på flera nivåer med trafikkontroll mellan nivåerna.

#### <a name="subscription-limits-and-multiple-hubs"></a>Prenumerationsbegränsningar och flera hubbar

I Azure distribueras alla komponenter, oavsett typ, i en Azure-prenumeration. Isolering av Azure-komponenter i olika Azure-prenumerationer kan uppfylla kraven för olika LOBs, till exempel att ställa in differentierade nivåer av åtkomst och auktorisering.

En enda implementering av ett virtuellt Data Center kan skala upp till ett stort antal ekrar, även om det finns plattforms gränser, precis som med varje IT-system. Hubb distributionen är bunden till en enskild Azure-prenumeration, som har begränsningar och begränsningar (till exempel maximalt antal VNet-peers). mer information finns i [Azure-prenumerationer och tjänst begränsningar, kvoter och begränsningar][limits] för mer information. I fall där gränser kan vara ett problem kan arkitekturen skalas upp ytterligare genom att modellen utökas från en enda hubb till ett kluster med hubb och ekrar. Flera hubbar i en eller flera Azure-regioner kan sammankopplas med VNet-peering, ExpressRoute, virtuella WAN-nätverk eller VPN för plats till plats.

![2][2]

Introduktionen av flera hubbar ökar systemets kostnads-och hanterings ansträngning. Det skulle endast motiveras av skalbarhet, system gränser eller redundans och regional replikering för slut användar prestanda eller haveri beredskap. I scenarier som kräver flera hubbar bör alla hubbar sträva efter att erbjuda samma uppsättning tjänster för drifts skull.

#### <a name="interconnection-between-spokes"></a>Samtrafik mellan ekrar

I en enda eker är det möjligt att implementera komplexa arbets belastningar på flera nivåer. Konfigurationer med flera nivåer kan implementeras med undernät (en för varje nivå) i samma VNet och filtrera flödena med hjälp av nätverks säkerhets grupper.

En arkitekt kan vilja distribuera en arbetsbelastning på flera nivåer i flera virtuella nätverk. Med peering av virtuella nätverk kan ekrar ansluta till andra ekrar i samma hubb eller olika hubbar. Ett typiskt exempel på det här scenariot är fallet där program bearbetnings servrar finns i en eker eller ett virtuellt nätverk. Databasen distribueras i ett annat eker-eller virtuellt nätverk. I det här fallet är det enkelt att koppla ekrarna med peering av virtuella nätverk och därmed undvika att överföras via hubben. En noggrann arkitektur och säkerhets granskning bör utföras för att se till att kringgå navet inte kringgår viktiga säkerhets-och gransknings punkter som bara finns i hubben.

![3][3]

Ekrar kan också vara sammankopplade till en eker som fungerar som hubb. Den här metoden skapar en hierarki på två nivåer: ekern på den högre nivån (nivå 0) blir hubb för nedre ekrar (nivå 1) i hierarkin. Ekrarna för en virtuell Data Center implementering krävs för att vidarebefordra trafiken till den centrala hubben så att trafiken kan överföras till målet i antingen det lokala nätverket eller det offentliga Internet. En arkitektur med två nivåer av hubbar introducerar komplex routning som tar bort fördelarna med en enkel hubb-eker-relation.

Även om Azure tillåter komplexa topologier, är en av de viktigaste principerna för det virtuella Data Center konceptet repeterbarhet och enkelhet. För att minimera hanterings ansträngningen är den enkla nav eker-designen den virtuella Data Center referens arkitekturen som vi rekommenderar.

### <a name="components"></a>Komponenter

Ett virtuellt Data Center består av fyra grundläggande komponent typer: **infrastruktur**, **perimeternätverk**, **arbets belastningar**och **övervakning**.

Varje komponent typ består av olika Azure-funktioner och Azure-resurser. Din implementering av Virtual Data Center består av instanser av flera typer av komponenter och flera varianter av samma komponent typ. Du kan till exempel ha många olika, logiskt åtskilda arbets belastnings instanser som representerar olika program. Du använder dessa olika komponent typer och instanser för att slutligen bygga ett virtuellt Data Center.

![4][4]

Föregående övergripande koncept arkitektur i ett virtuellt Data Center visar olika komponent typer som används i olika zoner i topologin hubb-ekrar. Diagrammet visar infrastruktur komponenter i olika delar av arkitekturen.

Som bra praxis i allmänhet bör åtkomst rättigheter och behörigheter vara gruppbaserade. Att hantera grupper i stället för enskilda användare fören klar underhållet av åtkomst principer genom att tillhandahålla ett konsekvent sätt att hantera dem i olika grupper och hjälper till att minimera konfigurations fel. Genom att tilldela och ta bort användare till och från lämpliga grupper kan du se till att en speciell användares privilegier hålls aktuell.

Varje roll grupp måste ha ett unikt prefix i sina namn. Det här prefixet gör det enkelt att identifiera vilken grupp som är associerad med vilken arbets belastning. Till exempel kan en arbets belastning som är värd för en autentiseringstjänst ha grupper med namnet **AuthServiceNetOps**, **AuthServiceSecOps**, **AuthServiceDevOps**och **AuthServiceInfraOps**. Centraliserade roller eller roller som inte är relaterade till en speciell tjänst kan föregås av **Corp**. Ett exempel är **CorpNetOps**.

Många organisationer använder en variant av följande grupper för att ge en större uppdelning av roller:

- Den centrala IT-gruppen, **Corp,** har ägande rätt att kontrol lera infrastruktur komponenter. Exempel är nätverk och säkerhet. Gruppen måste ha rollen deltagare i prenumerationen, kontrollen av hubben och nätverks deltagar rättigheter i ekrarna. Stora organisationer delar ofta upp dessa hanterings ansvars områden mellan flera team. Exempel är en nätverks åtgärd **CorpNetOps** -grupp med exklusiv fokus på nätverk och en säkerhets åtgärd **CorpSecOps** grupp som ansvarar för brand Väggs-och säkerhets principer. I det här fallet måste två olika grupper skapas för tilldelning av dessa anpassade roller.
- Gruppen dev-test, **AppDevOps,** har ansvaret för att distribuera appar eller tjänste arbets belastningar. Den här gruppen använder rollen som virtuell dator deltagare för IaaS-distributioner eller en eller flera PaaS-deltagares roller. Se [inbyggda roller för Azure-resurser][Roles]. Utvecklings-och test teamet kan dessutom behöva insyn i säkerhets principer (nätverks säkerhets grupper) och routningsprinciperna (användardefinierade vägar) inuti hubben eller en viss eker. Förutom rollen som deltagare för arbets belastningar behöver den här gruppen även rollen som nätverks läsare.
- Drift-och underhålls gruppen, **CorpInfraOps** eller **AppInfraOps,** har ansvaret för att hantera arbets belastningar i produktionen. Den här gruppen måste vara en prenumerations deltagare för arbets belastningar i alla produktions prenumerationer. Vissa organisationer kan också utvärdera om de behöver en ytterligare grupp för eskalering av support med rollen prenumerations deltagare i produktion och den centrala Hub-prenumerationen. Den ytterligare gruppen åtgärdar potentiella konfigurations problem i produktions miljön.

Ett virtuellt Data Center har utformats så att grupper som skapats för den centrala IT-gruppen, hanterar hubben, har motsvarande grupper på arbets belastnings nivå. Förutom att hantera nav resurser, kan den centrala IT-gruppen kontrol lera åtkomsten till och toppnivå för prenumerationen. Arbets belastnings grupper kan också styra resurser och behörigheter för sitt VNet oberoende av det centrala.

Ett virtuellt Data Center är partitionerat för att på ett säkert sätt vara värd för flera projekt på olika verksamhets rader. Alla projekt kräver olika isolerade miljöer (dev, UAT, produktion). Separata Azure-prenumerationer för var och en av dessa miljöer tillhandahåller naturlig isolering.

![5][5]

Föregående diagram visar förhållandet mellan en organisations projekt, användare och grupper och de miljöer där Azure-komponenterna distribueras.

Normalt är en miljö (eller-nivå) ett system där flera program distribueras och körs. Stora företag använder en utvecklings miljö (där ändringar görs och testas) och en produktions miljö (vad slutanvändarna använder). Dessa miljöer är åtskilda, ofta med flera mellanlagrings miljöer mellan dem för att tillåta stegvis distribution (distribution), testning och återställning om det uppstår problem. Distributions arkitekturer varierar kraftigt, men vanligt vis är den grundläggande processen för utveckling (utveckling) och slut vid produktion (PROD) fortfarande.

En gemensam arkitektur för dessa typer av miljöer med flera nivåer består av Azure-DevOps för utveckling och testning, UAT för mellanlagring och produktions miljöer. Organisationer kan utnyttja en eller flera Azure AD-klienter för att definiera åtkomst och rättigheter till dessa miljöer. Föregående diagram visar ett fall där två olika Azure AD-klienter används: ett för Azure-DevOps och UAT och den andra exklusivt för produktion.

Förekomsten av olika Azure AD-klienter använder separationen mellan miljöer. Samma grupp med användare, till exempel den centrala IT, måste autentiseras med hjälp av en annan URI för att få åtkomst till en annan Azure AD-klient för att ändra rollerna eller behörigheterna för antingen Azure-DevOps eller produktions miljöerna i ett projekt. Förekomsten av olika användarautentisering för att få åtkomst till olika miljöer minskar eventuella avbrott och andra problem som orsakas av mänskliga fel.

#### <a name="component-type-infrastructure"></a>Komponent typ: infrastruktur

Den här komponent typen är där det mesta av den stödda infrastrukturen finns. Det är också här som dina centraliserade IT-, säkerhets-och Compliance-team tillbringar det mesta av sin tid.

![6][6]

Infrastruktur komponenter ger en samman koppling för de olika komponenterna i en virtuell Data Center implementering och finns både i hubben och i ekrar. Ansvaret för att hantera och underhålla infrastruktur komponenter tilldelas vanligt vis till centrala IT-eller säkerhets teamet.

En av de viktigaste uppgifterna i IT-infrastrukturens team är att garantera konsekvensen av IP-adressens scheman i hela företaget. Det privata IP-adressutrymmet som tilldelas till en virtuell Data Center implementering måste vara konsekvent och inte överlappa med privata IP-adresser som tilldelats till dina lokala nätverk.

NAT på lokala Edge-routrar eller i Azure-miljöer kan undvika konflikter i IP-adresser, men det lägger till komplikationer i infrastruktur komponenterna. Enkel hantering är en av de viktigaste målen i det virtuella data centret, så att använda NAT för att hantera IP-problem är inte en rekommenderad lösning.

Infrastruktur komponenter har följande funktioner:

- [**Identitets-och katalog tjänster**][azure-ad]. Åtkomst till varje resurs typ i Azure styrs av en identitet som lagras i en katalog tjänst. Katalog tjänsten lagrar inte bara listan över användare, utan även åtkomst rättigheterna till resurser i en enskild Azure-prenumeration. Dessa tjänster kan endast finnas i molnet, eller så kan de synkroniseras med den lokala identiteten som lagras i Active Directory.
- [**Virtual Network**][VPN]. Virtuella nätverk är en av huvud komponenterna i det virtuella data centret och gör att du kan skapa en bindning för trafik isolering på Azure-plattformen. En Virtual Network består av ett eller flera virtuella nätverks segment, vart och ett med ett visst IP-nätverksprefix (ett undernät). Virtual Network definierar ett internt perimeter-området där IaaS virtuella datorer och PaaS-tjänster kan upprätta privat kommunikation. Virtuella datorer (och PaaS-tjänster) i ett virtuellt nätverk kan inte kommunicera direkt med virtuella datorer (och PaaS-tjänster) i ett annat virtuellt nätverk, även om båda virtuella nätverken har skapats av samma kund, under samma prenumeration. Isolering är en kritisk egenskap som garanterar att kunders virtuella datorer och kommunikation förblir privata i ett virtuellt nätverk.
- [**Användardefinierade vägar**][user-defined-routes]. Trafik i ett virtuellt nätverk dirigeras som standard baserat på tabellen system routning. En användardefinierad väg är en anpassad routningstabell som nätverks administratörer kan koppla till ett eller flera undernät för att skriva över beteendet för system vägvals tabellen och definiera en kommunikations Sök väg inom ett virtuellt nätverk. Förekomst av användardefinierade vägar garanterar att utgående trafik från eker-överföringen via vissa anpassade virtuella datorer eller virtuella nätverks apparater och belastningsutjämnare finns i både hubben och ekrarna.
- [**Nätverks säkerhets grupper**][network-security-groups]. En nätverks säkerhets grupp är en lista över säkerhets regler som fungerar som trafik filtrering på IP-källor, IP-adresser, protokoll, IP-källport och IP-mål portar. Nätverks säkerhets gruppen kan tillämpas på ett undernät, ett virtuellt NIC-kort som är kopplat till en virtuell Azure-dator eller både och. Nätverks säkerhets grupperna är nödvändiga för att implementera en korrekt flödes kontroll i hubben och i ekrarna. Den säkerhets nivå som ges av nätverks säkerhets gruppen är en funktion för vilka portar du öppnar och för vilket syfte. Kunderna bör tillämpa ytterligare filter per virtuell dator med värdbaserade brand väggar som program varan iptables eller Windows-brandväggen.
- [**DNS**][DNS]. Namn matchningen för resurser i virtuella nätverk för en virtuell Data Center implementering tillhandahålls via DNS. Azure tillhandahåller DNS-tjänster för både [offentlig][DNS] och [privat][PrivateDNS] namn matchning. Privata zoner ger namn matchning både i ett virtuellt nätverk och mellan virtuella nätverk. Du kan ha privata zoner som inte bara sträcker sig över virtuella nätverk i samma region, utan även mellan regioner och prenumerationer. För offentlig lösning tillhandahåller Azure DNS en värd tjänst för DNS-domäner som ger namn matchning med hjälp av Microsoft Azure-infrastrukturen. Genom att använda Azure som värd för dina domäner kan du hantera dina DNS-poster med samma autentiseringsuppgifter, API:er, verktyg och fakturering som för dina andra Azure-tjänster.
- [**Prenumerations**][SubMgmt] -och [**resurs grupps hantering**][RGMgmt]. En prenumeration definierar en naturlig gränser för att skapa flera grupper av resurser i Azure. Resurser i en prenumeration monteras tillsammans i logiska behållare som kallas resurs grupper. Resurs gruppen representerar en logisk grupp för att organisera resurserna för en virtuell Data Center implementering.
- [**RBAC**][RBAC]. Via RBAC är det möjligt att mappa organisations rollen tillsammans med rättigheter för att få åtkomst till specifika Azure-resurser, så att du kan begränsa användare till endast en viss del av åtgärder. Med RBAC kan du bevilja åtkomst genom att tilldela lämplig roll till användare, grupper och program inom relevant omfattning. Omfånget för en roll tilldelning kan vara en Azure-prenumeration, en resurs grupp eller en enskild resurs. RBAC tillåter arv av behörigheter. En roll som tilldelas till en överordnad omfattning ger också åtkomst till de underordnade objekten i den. Med RBAC kan du åtskilja uppgifter och ge endast åtkomst till användare som de behöver för att utföra sina jobb. Använd exempelvis RBAC för att låta en medarbetare hantera virtuella datorer i en prenumeration, medan en annan kan hantera SQL-databaser inom samma prenumeration.
- [**VNet-peering**][VNetPeering]. Den grundläggande funktionen som används för att skapa en infrastruktur i ett virtuellt Data Center är VNet-peering, en mekanism som ansluter två virtuella nätverk (virtuella nätverk) i samma region via Azure datacenter-nätverket eller med Azure World-Wide-stamnät över regioner .

#### <a name="component-type-perimeter-networks"></a>Komponent typ: perimeternätverk

[Nätverks][DMZ] komponenter i perimeternätverket möjliggör nätverks anslutning mellan dina lokala eller fysiska data Center nätverk, tillsammans med alla anslutningar till och från Internet. Det är också där dina nätverks-och säkerhets team ofta tillbringar det mesta av tiden.

Inkommande paket ska flöda genom säkerhetsenheterna i hubben innan de når backend-servrarna i ekrarna. Exempel är brand väggar, ID: n och IP-adresser. Innan de lämnar nätverket bör Internet-baserade paket från arbets belastningarna också flöda genom säkerhetsenheterna i perimeternätverket. Syftet med det här flödet är principtillämpning, inspektion och granskning.

Nätverks komponenter i perimeternätverket innehåller följande funktioner:

- [Virtuella nätverk][VNet], [användardefinierade vägar][user-defined-routes] och [nätverkssäkerhetsgrupper][network-security-groups]
- [Virtuella nätverks enheter][NVA]
- [Azure Load Balancer][ALB]
- [Azure Application Gateway][AppGW] med [brand vägg för webbaserade program (WAF)][AppGWWAF]
- [Offentliga IP-adresser][PIP]
- [Azure-front dörr][AFD] med [brand vägg för webbaserade program (WAF)][AFDWAF]
- [Azure Firewall][AzFW]

Vanligt vis har centrala IT-och säkerhets team ansvar för krav definition och drift av perimeternätverket.

![7][7]

Föregående diagram visar verk ställandet av två perimeter med åtkomst till Internet och ett lokalt nätverk, både Resident i DMZ-hubben. I DMZ-hubben kan perimeternätverket på Internet skala upp till stöd för ett stort antal LOBs, med hjälp av flera grupper av brand väggar för webbaserade program (WAF) eller Azure-brandväggar. I hubben tillåter även anslutning via VPN eller ExpressRoute vid behov.

[**Virtuella nätverk**][VNet]. Hubben bygger vanligt vis på ett virtuellt nätverk med flera undernät som är värdar för de olika typerna av tjänster som filtrerar och inspekterar trafik till eller från Internet via NVA, WAF och Azure Application Gateway-instanser.

[**Användardefinierade vägar**][user-defined-routes] Med hjälp av användardefinierade vägar kan kunder distribuera brand väggar, ID: n/IP-adresser och andra virtuella apparater och dirigera nätverks trafik genom dessa säkerhetsanordningar för tillämpning, granskning och inspektion av säkerhets gräns principen. Användardefinierade vägar kan skapas både i hubben och i ekrarna för att garantera att trafiktransiter via de speciella anpassade virtuella datorerna, virtuella nätverks installationer och belastningsutjämnare som används av en virtuell Data Center implementering. För att garantera att trafik som genereras från virtuella datorer som finns i eker-överföringarna till rätt virtuella enheter måste en användardefinierad väg anges i under näten i ekern genom att ange IP-adressen för den interna belastningsutjämnaren som nästa hopp. Den interna belastningsutjämnaren distribuerar den interna trafiken till de virtuella datorerna (belastningsutjämnarens serverdelspool).

[**Azure-brandväggen**][AzFW] är en hanterad, molnbaserad nätverks säkerhets tjänst som skyddar dina Azure Virtual Network-resurser. Det är en fullständigt tillstånds känslig brand vägg som en tjänst med inbyggd hög tillgänglighet och obegränsad moln skalbarhet. Du kan centralt skapa, framtvinga och logga principer för tillämpning och nätverksanslutning över prenumerationer och virtuella nätverk. Azure Firewall använder en statisk offentlig IP-adress för dina virtuella nätverksresurser. Det gör att externa brandväggar kan identifiera trafiken från ditt virtuella nätverk. Tjänsten är helt integrerad med Azure Monitor för loggning och analys.

[**Virtuella nätverks enheter**][NVA]. I hubben hanteras perimeternätverket med åtkomst till Internet normalt via en Azure Firewall-instans eller en grupp med brand väggar eller brand vägg för webbaserade program (WAF).

Många webbprogram används ofta i olika LOB:er. Dessa webbprogram tenderar att drabbas av sårbarheter och potentiella hot. Brand väggar för webb program är en särskild typ av produkt som används för att identifiera attacker mot webb program, HTTP/HTTPS, i större djup än en allmän brand vägg. Jämfört med tradition Firewall Technology har WAF en uppsättning funktioner för att skydda interna webb servrar mot hot.

En Azure Firewall-eller NVA-brandvägg använder båda ett gemensamt administrations plan med en uppsättning säkerhets regler för att skydda de arbets belastningar som finns i ekrarna och kontrol lera åtkomsten till lokala nätverk. Azure-brandväggen har inbyggd skalbarhet, medan NVA-brandväggar kan skalas manuellt bakom en belastningsutjämnare. Vanligt vis har en brand Väggs grupp mindre specialiserad program vara jämfört med en WAF, men har en bredare programdefinition för att filtrera och inspektera alla typer av trafik i utgående och ingångs händelser. Om en NVA metod används kan de hittas och distribueras från Azure Marketplace.

Använd en uppsättning Azure-brandväggar (eller NVA) för trafik som kommer från Internet och en annan för trafik som kommer från lokal. Att bara ha ett brandväggssystem är en säkerhetsrisk, eftersom det inte ger någon säkerhetsperimeter mellan de två uppsättningarna med nätverkstrafik. Genom att använda separata brand Väggs lager minskar du komplexiteten vid kontroll av säkerhets regler och gör det tydligt vilka regler som motsvarar vilken inkommande nätverksbegäran som begärs.

Vi rekommenderar att du använder en uppsättning Azure Firewall-instanser, eller NVA, för trafik som kommer från Internet. Använd en annan för trafik som kommer från lokala platser. Att bara använda en uppsättning brand väggar för båda är en säkerhets risk eftersom den inte ger någon säkerhetsperimeter mellan de två uppsättningarna nätverks trafik. Genom att använda separata brand Väggs lager minskar du komplexiteten vid kontroll av säkerhets regler och gör det tydligt vilka regler som motsvarar vilken inkommande nätverksbegäran som begärs.

[**Azure Load Balancer**][ALB] erbjuder en Layer 4-tjänst med hög tillgänglighet (TCP, UDP) som kan distribuera inkommande trafik mellan tjänst instanser som definierats i en belastningsutjämnad uppsättning. Trafik som skickas till belastningsutjämnaren från front-end-slutpunkter (offentliga IP-slutpunkter eller privata IP-slutpunkter) kan distribueras om med eller utan adress översättning till en uppsättning backend-IP-adresspool (exempel är virtuella nätverks enheter eller virtuella datorer).

Azure Load Balancer kan avsöka hälso tillståndet för de olika Server instanserna och när en instans inte svarar på en avsökning slutar belastningsutjämnaren att skicka trafik till den felaktiga instansen. I ett virtuellt Data Center distribueras en extern belastningsutjämnare till hubben och ekrarna. I hubben används belastningsutjämnaren för att effektivt dirigera trafik till tjänster i ekrar, och i ekrar används belastnings utjämning för att hantera program trafik.

[**Azure**][AFD] -AFD (Azure-frontend) är Microsofts hög tillgängliga och skalbara plattform för webb programs acceleration, global HTTP-load balancer, program skydd och Content Delivery Network. Genom att köra på fler än 100 platser på kanten av Microsofts globala nätverk kan du använda AFD för att bygga, driva och skala ut ditt dynamiska webb program och statiskt innehåll. AFD tillhandahåller ditt program med slutanvändarens prestanda i världs klass, enhetlig regional/stämplad underhålls automatisering, BCDR Automation, enhetlig klient/användar information, cachelagring och service insikter. Plattformen erbjuder prestanda, tillförlitlighet och support service avtal, certifieringar för regelefterlevnad och gransknings bara säkerhets metoder som utvecklats, drivs och stöds internt av Azure.

[**Application Gateway**][AppGW] Microsoft Azure Application Gateway är en dedikerad virtuell installation som tillhandahåller program leverans kontroll (ADC) som en tjänst som erbjuder olika Layer 7 belastnings Utjämnings funktioner för ditt program. Du kan optimera webb server gruppens produktivitet genom att avlasta processor intensiva SSL-avslutning till Application Gateway. Här finns även andra layer 7-routningsfunktioner, till exempel resursallokeringsdistribution av inkommande trafik, cookiebaserad sessionstillhörighet, URL-sökvägsbaserad routning och möjligheten att vara värd för flera webbplatser bakom en enda Application Gateway. En brandvägg för webbaserade program (WAF) ingår också som en del av programgatewayens WAF SKU. Den här SKU:n skyddar webbprogram mot vanliga säkerhetsrisker och sårbarheter på webben. Application Gateway kan konfigureras som internetuppkopplad gateway, endast intern gateway eller en kombination av båda.

[**Offentliga IP-adresser**][PIP]. Med vissa Azure-funktioner kan du associera tjänstens slut punkter till en offentlig IP-adress, så att din resurs kan nås från Internet. Den här slutpunkten använder Network Address Translation (NAT) för att dirigera trafik till den interna adressen och porten i det virtuella Azure-nätverket. Den här vägen är det primära sättet för extern trafik att skickas till det virtuella nätverket. Du kan konfigurera offentliga IP-adresser för att avgöra vilken trafik som skickas och hur och var den översätts till det virtuella nätverket.

[**Azure DDoS Protection standard**][DDoS] ger ytterligare funktioner för minskning av de [grundläggande tjänst][DDoS] nivåer som är specifika för Azure Virtual Network-resurser. DDoS Protection standard är enkelt att aktivera och kräver inga programändringar. Skydds principer är justerade genom dedikerad trafik övervakning och Machine Learning-algoritmer. Principer tillämpas på offentliga IP-adresser som är kopplade till resurser som har distribuerats i virtuella nätverk. Exempel är Azure Load Balancer, Azure Application Gateway och Azure Service Fabric-instanser. Telemetri i real tid är tillgängligt via Azure Monitor vyer under ett angrepp och för historik. Program skikts skydd kan läggas till via brand väggen för webbaserade Azure Application Gateway. Skydd finns för offentliga IP-adresser med IPv4-protokoll i Azure.

#### <a name="component-type-monitoring"></a>Komponent typ: övervakning

Övervaknings komponenter ger synlighet och aviseringar från alla andra typer av komponenter. Alla team bör ha åtkomst till övervakning för de komponenter och tjänster som de har åtkomst till. Om du har en central supportavdelning eller drift team, kräver de integrerad åtkomst till de data som tillhandahålls av dessa komponenter.

Azure erbjuder olika typer av loggnings-och övervaknings tjänster för att spåra beteendet för Azure-värdbaserade resurser. Styrning och kontroll av arbets belastningar i Azure baseras inte bara på insamling av loggdata, utan även på möjlighet att utlösa åtgärder baserat på enskilda rapporterade händelser.

[**Azure Monitor**][Monitor]. Azure innehåller flera tjänster som utför en specifik roll eller aktivitet individuellt i övervakningsutrymmet. Tillsammans levererar dessa tjänster en heltäckande lösning för att samla in, analysera och agera utifrån telemetrin från dina program och de Azure-resurser som stöder dem. De kan också användas för att övervaka kritiska lokala resurser så att du får en hybridövervakningsmiljö. Det första steget i att utveckla en fullständig övervakningsstrategi för ditt program är att förstå de verktyg och data som är tillgängliga.

Det finns två huvud typer av loggar i Azure:

- [Azure aktivitets loggen][ActLog], som tidigare kallades **operativa loggar**, ger inblick i de åtgärder som utfördes på resurserna i Azure-prenumerationen. Dessa loggar rapporterar kontroll Plans händelser för dina prenumerationer. Varje Azure-resurs skapar gransknings loggar.

- [Azure Monitor diagnostikloggar][DiagLog] loggar genereras av en resurs som ger omfattande, frekventa data om driften av resursen. Innehållet i dessa loggar varierar beroende på resurs typ.

![9][9]

Det är viktigt att spåra loggar för nätverks säkerhets grupper, särskilt den här informationen:

- [Händelse loggar][nsg-log] innehåller information om vilka regler för nätverks säkerhets grupper som tillämpas på virtuella datorer och instans roller baserade på Mac-adress.
- [Räknar loggar][nsg-log] spår hur många gånger varje regel för nätverks säkerhets grupper kördes för att neka eller tillåta trafik.

Alla loggar kan lagras i Azure Storage-konton för gransknings-, statisk analys-eller säkerhets kopierings syfte. När du lagrar loggarna på ett Azure Storage-konto kan kunder använda olika typer av ramverk för att hämta, prepa, analysera och visualisera dessa data för att rapportera status och hälsa för moln resurser.

Stora företag bör redan ha förvärvat ett standard ramverk för övervakning av lokala system. De kan utöka detta ramverk för att integrera loggar som genereras av moln distributioner. Genom att använda [Azure Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-queries)kan organisationer behålla all loggning i molnet. Log Analytics implementeras som en molnbaserad tjänst. Så att du snabbt kan komma igång med minimal investering i infrastruktur tjänster. Log Analytics integreras också med System Center-komponenter som System Center Operations Manager för att utöka dina befintliga hanterings investeringar i molnet.

Log Analytics är en tjänst i Azure som hjälper till att samla in, korrelera, söka och agera på logg-och prestanda data som genereras av moln komponenter för operativ system, program och infrastruktur. Den ger kunderna real tids insikter med integrerad sökning och anpassade instrument paneler för att analysera alla poster över alla dina arbets belastningar i din implementering av Virtual Data Center.

[Azure Network Watcher][NetWatch] innehåller verktyg för att övervaka, diagnostisera och visa mått och aktivera eller inaktivera loggar för resurser i ett virtuellt Azure-nätverk. Det är en mångfacetterat-tjänst som gör det möjligt att använda följande funktioner:

- Övervaka kommunikation mellan en virtuell dator och en slut punkt.
- Visa resurser i ett virtuellt nätverk och deras relationer.
- Diagnostisera problem med nätverks trafik filtrering till eller från en virtuell dator.
- Diagnostisera problem med nätverks routning från en virtuell dator.
- Diagnostisera utgående anslutningar från en virtuell dator.
- Avbilda paket till och från en virtuell dator.
- Diagnostisera problem med en virtuell Azure-nätverksgateway och anslutningar.
- Bestäm relativ fördröjning mellan Azure-regioner och Internet leverantörer.
- Visa säkerhets regler för ett nätverks gränssnitt.
- Visa nätverks mått.
- Analysera trafik till eller från en nätverks säkerhets grupp.
- Visa diagnostikloggar för nätverks resurser.

[Övervakare av nätverksprestanda][NPM] -lösningen i Operations Management Suite kan ge detaljerad nätverks information från slut punkt till slut punkt. Den här informationen omfattar en enda vy över dina Azure-nätverk och lokala nätverk. Lösningen har olika Övervakare för ExpressRoute och offentliga tjänster.

#### <a name="component-type-workloads"></a>Komponent typ: arbets belastningar

Arbets belastnings komponenter är där dina faktiska program och tjänster finns. Det är också där dina program utvecklings team tillbringar det mesta av sin tid.

Arbets belastnings möjligheterna är oändliga. Följande är bara några av de möjliga arbets belastnings typerna:

**Interna LOB-program:** Branschspecifika program är dator program som är viktiga för pågående drift av ett företag. LOB-program har några gemensamma egenskaper:

- **Interaktivt efter typ:** Data har angetts och resultat eller rapporter returneras.
- **Data driven:** Data intensiva arbets belastningar med frekvent åtkomst till databaser eller andra lagrings enheter.
- **Integrerad:** Arbets belastningar erbjuder integration med andra system inom eller utanför organisationen.

**Kund riktade webbplatser (Internet eller internt)** : de flesta program som interagerar med Internet är webbplatser. Azure erbjuder funktioner för att köra en webbplats på en virtuell IaaS-dator eller från en [Azure Web Apps][WebApps] -plats (PaaS). Azure Web Apps stöd för integrering med virtuella nätverk som tillåter distribution av Web Apps i en eker-nätverks zon. Interna riktade webbplatser behöver inte exponera en offentlig Internet-slutpunkt eftersom resurserna är tillgängliga via privata adresser som inte är Internet-dirigerade från det privata virtuella nätverket.

**Big data och analys:** När data måste skalas upp till en stor volym kan det hända att databaser inte skalas upp på rätt sätt. Hadoop-tekniken erbjuder ett system för att köra distribuerade frågor parallellt på ett stort antal noder. Kunderna har möjlighet att köra data arbets belastningar i virtuella IaaS-datorer eller PaaS ([HDInsight][HDI]). HDInsight stöder distribution till ett location-baserat VNet, kan distribueras till ett kluster i en eker i ett virtuellt Data Center.

**Händelser och meddelanden:** [Azure Event Hubs][EventHubs] är en inmatnings tjänst för storskalig telemetri som samlar in, transformerar och lagrar miljon tals händelser. Som en distribuerad strömmande plattform erbjuder den låg latens och konfigurerbar tids kvarhållning, så att du kan mata in stora mängder telemetri i Azure och läsa dessa data från flera program. Med Event Hubs kan en enda data ström stödja både real tids-och batch-baserade pipeliner.

Du kan implementera en mycket tillförlitlig moln meddelande tjänst mellan program och tjänster via [Azure Service Bus][ServiceBus]. Den erbjuder asynkrona asynkrona meddelanden mellan klient och Server, strukturerade First-in-First-meddelanden (FIFO) och publicera och prenumerera-funktioner.

![10][10]

### <a name="making-a-virtual-datacenter-highly-available-multiple-virtual-datacenters"></a>Göra ett virtuellt Data Center tillgängligt med hög tillgänglighet: flera virtuella Data Center

Den här artikeln har hittills fokuserat på utformningen av ett enda virtuellt Data Center, som beskriver de grundläggande komponenterna och arkitekturen som bidrar till återhämtning. Azure-funktioner som Azure Load Balancer, NVA, tillgänglighets uppsättningar, skalnings uppsättningar, tillsammans med andra mekanismer bidrar till ett system som gör det möjligt att bygga fasta SLA-nivåer i dina produktions tjänster.

Men eftersom ett enda virtuellt Data Center vanligt vis implementeras inom en enda region kan det vara utsatt för alla större avbrott som påverkar hela regionen. Kunder som kräver hög service avtal måste skydda tjänsterna genom distributioner av samma projekt i två (eller flera) virtuella Data Center implementeringar placerade i olika regioner.

Förutom SLA-frågor finns det flera vanliga scenarier där distribution av flera virtuella Data Center implementeringar är meningsfullt:

- Regional eller global närvaro.
- Haveriberedskap.
- En mekanism för att avleda trafik mellan data Center.

#### <a name="regionalglobal-presence"></a>Regional/global närvaro

Azure-datacenter finns i flera regioner över hela världen. När du väljer flera Azure-datacenter måste kunderna överväga två relaterade faktorer: geografiska avstånd och svars tid. För att erbjuda den bästa användar upplevelsen kan du utvärdera det geografiska avståndet mellan varje Virtual Data Center-implementering samt avståndet mellan varje virtuell Data Center implementering och slutanvändarna.

Den region där de virtuella data centrets implementeringarna finns måste följa myndighets krav som fastställs av juridiska myndigheter som organisationen använder.

#### <a name="disaster-recovery"></a>Haveriberedskap

Utformningen av en katastrof återställnings plan beror på typerna av arbets belastningar och möjligheten att synkronisera status för dessa arbets belastningar mellan olika virtuella Data Center implementeringar. De flesta kunder vill ha en snabb failover-funktion, och detta kan kräva programdata-synkronisering mellan distributioner som kör flera virtuella Data Center implementeringar. Men vid utformning av katastrof återställnings planer är det viktigt att tänka på att de flesta program är känsliga för den svars tid som kan orsakas av den här datasynkroniseringen.

Synkronisering och pulsslags övervakning av program i olika Virtual Data Center-implementeringar kräver att de kommunicerar via nätverket. Två implementeringar i olika regioner kan anslutas via:

- VNet-peering – VNet-peering kan ansluta hubbar mellan regioner.
- ExpressRoute privata peering när hubbarna i varje Virtual Data Center-implementering är anslutna till samma ExpressRoute-krets.
- Flera ExpressRoute-kretsar som är anslutna via företagets stamnät och flera Virtual Data Center-implementeringar anslutna till ExpressRoute-kretsarna.
- Plats-till-plats-VPN-anslutningar mellan nav zonen i dina virtuella Data Center implementeringar i varje Azure-region.

Normalt är VNet-peering eller ExpressRoute-anslutningar den önskade typen av nätverks anslutning på grund av den högre bandbredden och konsekvent latens nivåer vid överföring via Microsofts stamnät.

Vi rekommenderar att kunderna kör tester för nätverks kvalificering för att kontrol lera svars tiden och bandbredden hos anslutningarna och bestämma om synkron eller asynkron datareplikering är lämplig baserat på resultatet. Det är också viktigt att väga de här resultaten med tanke på det optimala återställnings tids målet (RTO).

#### <a name="disaster-recovery-diverting-traffic-from-one-region-to-another"></a>Haveri beredskap: avleda trafik från en region till en annan

[Azure Traffic Manager][traffic-manager] kontrollerar regelbundet tjänst hälsan för offentliga slut punkter i olika Virtual Data Center-implementeringar och, om dessa slut punkter inte fungerar, dirigeras de automatiskt till det sekundära virtuella data centret med hjälp av Domain Name System ( DNS).

Eftersom den använder DNS är Traffic Manager bara för användning med offentliga Azure-slutpunkter. Tjänsten används vanligt vis för att styra eller leda till trafik till virtuella Azure-datorer och Web Apps i den felfria instansen av en virtuell Data Center implementering. Traffic Manager är elastisk även om en hel Azure-region slutar fungera och kan styra distributionen av användar trafik för tjänst slut punkter i olika virtuella Data Center baserat på flera kriterier. Till exempel om en tjänst Miss lyckas i en speciell implementering av ett virtuellt Data Center eller om du väljer den virtuella Data Center implementeringen med den lägsta nätverks fördröjningen.

### <a name="summary"></a>Sammanfattning

Ett virtuellt Data Center är en metod för att migrera data Center för att skapa en skalbar arkitektur i Azure som maximerar användningen av moln resurser, minskar kostnaderna och fören klar system styrningen. Ett virtuellt Data Center baseras på en nav-och eker-nätverkstopologi, vilket ger gemensamma delade tjänster i hubben och tillåter vissa program och arbets belastningar i ekrarna. Ett virtuellt Data Center matchar också strukturen för företags roller, där olika avdelningar, till exempel central IT, DevOps och drift och underhåll fungerar tillsammans samtidigt som de utför sina egna roller. Ett virtuellt Data Center uppfyller kraven för en överförings-och Shift-migrering, men ger också många fördelar för distribution av interna moln.

## <a name="references"></a>Referenser

Följande funktioner beskrivs i det här dokumentet. Följ länkarna om du vill veta mer.

<!-- markdownlint-disable MD033 -->

|Nätverksfunktioner|Belastningsutjämning|Anslutningsmöjlighet|
|-|-|-|
|[Azure Virtual Networks][VNet]</br>[Nätverkssäkerhetsgrupper][network-security-groups]</br>[Loggar för nätverks säkerhets grupper][nsg-log]</br>[Användardefinierade vägar][user-defined-routes]</br>[Virtuella nätverks enheter][NVA]</br>[offentliga IP-adresser][PIP]</br>[Azure-DDoS][DDoS]</br>[Azure Firewall][AzFW]</br>[Azure DNS][DNS]|[Azure Front Door][AFD]</br>[Azure Load Balancer (L3)][ALB]</br>[Application Gateway (L7)][AppGW]</br>[Brand vägg för webbaserade program] WAF</br>[Azure Traffic Manager][traffic-manager]</br></br></br></br></br> |[VNet-peering][VNetPeering]</br>[Virtuellt privat nätverk][VPN]</br>[Virtuellt WAN][vWAN]</br>[ExpressRoute][ExR]</br>[ExpressRoute Direct][ExRD]</br></br></br></br></br>

|Identitet</br>|Övervakning</br>|Bästa metoder</br>|
|-|-|-|
|[Azure Active Directory][azure-ad]</br>[Multi-Factor Authentication][multi-factor-authentication]</br>[Åtkomst kontroller för roll bas][RBAC]</br>[Standard roller för Azure AD][Roles]</br></br></br> |[Network Watcher][NetWatch]</br>[Azure Monitor][Monitor]</br>[Aktivitets loggar][ActLog]</br>[Diagnostikloggar][DiagLog]</br>[Microsoft Operations Management Suite][OMS]</br>[Övervakning av nätverksprestanda][NPM]|[Metod tips för perimeter-nätverk][DMZ]</br>[Prenumerations hantering][SubMgmt]</br>[Hantering av resurs grupper][RGMgmt]</br>[Begränsningar för Azure-prenumeration][limits] </br></br></br>|

|Andra Azure-tjänster|
|-|
|[Azure Web Apps][WebApps]</br>[HDInsight (Hadoop)][HDI]</br>[Event Hubs][EventHubs]</br>[Service Bus][ServiceBus]|

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Nästa steg

- Utforska [VNet-peering][VNetPeering], underfästnings teknik för virtuella Data Center Hub och ekrar.
- Implementera [Azure AD][azure-ad] för att komma igång med [RBAC][RBAC] -utforskning.
- Utveckla en prenumerations-och resurs hanterings modell och RBAC-modell för att uppfylla organisationens struktur, krav och principer. Den viktigaste aktiviteten är planering. I så stor utsträckning som möjligt, planera för organisations-, sammanslagnings-, nya produkt linjer och andra överväganden.

<!-- images -->

[0]: ../_images/vdc/networking-redundant-equipment.png "Exempel på komponentöverlappning"
[1]: ../_images/vdc/networking-vdc-high-level.png "Exempel på hög nivå av hubb och eker i en virtuell Data Center implementering"
[2]: ../_images/vdc/networking-hub-spokes-cluster.png "Kluster med hubbar och ekrar"
[3]: ../_images/vdc/networking-spoke-to-spoke.png "Eker-till-eker"
[4]: ../_images/vdc/networking-vdc-block-level-diagram.png "Diagram över block nivå för en virtuell Data Center implementering"
[5]: ../_images/vdc/networking-users-groups-subscriptions.png "Användare, grupper, prenumerationer och projekt"
[6]: ../_images/vdc/networking-infrastructure-high-level.png "Infrastrukturdiagram på hög nivå"
[7]: ../_images/vdc/networking-high-level-perimeter-networks.png "Infrastrukturdiagram på hög nivå"
[8]: ../_images/vdc/networking-vnet-peering-perimeter-networks.png "VNet-peering och perimeternätverk"
[9]: ../_images/vdc/networking-high-level-diagram-monitoring.png "Diagram på hög nivå för övervakning"
[10]: ../_images/vdc/networking-high-level-workloads.png "Diagram på hög nivå för arbetsbelastning"

<!-- links -->

[limits]: https://docs.microsoft.com/azure/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/role-based-access-control/built-in-roles
[VNet]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[network-security-groups]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg
[DNS]: https://docs.microsoft.com/azure/dns/dns-overview
[PrivateDNS]: https://docs.microsoft.com/azure/dns/private-dns-overview
[VNetPeering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview
[user-defined-routes]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview
[RBAC]: https://docs.microsoft.com/azure/role-based-access-control/overview
[multi-factor-authentication]: https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication
[azure-ad]: https://docs.microsoft.com/azure/active-directory/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction
[ExRD]: https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about
[vWAN]: https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[AzFW]: https://docs.microsoft.com/azure/firewall/overview
[SubMgmt]: /azure/architecture/cloud-adoption/appendix/azure-scaffold
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[DMZ]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[DDoS]: https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address
[AFD]: https://docs.microsoft.com/azure/frontdoor/front-door-overview
[AFDWAF]: https://docs.microsoft.com/azure/frontdoor/waf-overview
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[AppGWWAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
[Monitor]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/
[ActLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs
[DiagLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[nsg-log]: https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview
[NPM]: https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor
[NetWatch]: https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview
[WebApps]: https://docs.microsoft.com/azure/app-service/
[HDI]: https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[traffic-manager]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
