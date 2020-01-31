---
title: Beslutsguide för regioner
description: Lär dig mer om hur du väljer region för molnplattformen.
author: doodlemania2
ms.author: dermar
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: aff6a3129bd93df434737a861f0b5f0daad24bcc
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806721"
---
# <a name="azure-regions"></a>Azure-regioner

Azure består av många regioner runtom i världen. Varje [Azure-region](https://azure.microsoft.com/global-infrastructure/regions) har särskilda egenskaper, som gör valet av region ytterst viktigt.

1. **Tillgängliga tjänster:** Vilka tjänster som distribueras till respektive region varierar beroende på olika faktorer. Välj en region för din arbetsbelastning som innehåller den tjänst du vill använda. Mer information om vilka tjänster som är tillgängliga i respektive region finns i [Produkttillgänglighet per region](https://azure.microsoft.com/global-infrastructure/services).
1. **Kapacitet:** Varje region har en maximal kapacitet. Även om detta oftast inte påverkar slutanvändaren, kan det påverka vilka typer av prenumerationer som kan distribuera vilka typer av tjänster och under vilka omständigheter. Detta skiljer sig från prenumerationskvoterna. Om du planerar en omfattande datacentermigrering till Azure kanske du vill kontakta ditt lokala Azure-team eller din kontoansvariga för att kontrollera att du kan distribuera i den skala som behövs.
1. **Villkor:** Distributionen av tjänster är begränsad i vissa regioner. Vissa regioner är till exempel bara tillgängliga som mål för säkerhetskopiering eller redundans. Andra begränsningar som är viktiga att notera är [krav på datasuveränitet](https://azure.microsoft.com/global-infrastructure/geographies).
1. **Suveränitet:** Vissa regioner är avsedda för specifika suveräna entiteter. Även om alla regioner är Azure-regioner, är dessa suveräna regioner helt isolerade från resten av Azure. De hanteras inte nödvändigtvis av Microsoft, och kan vara begränsade till särskilda typer av kunder. Dessa suveräna regioner är:
    1. [Azure Kina](https://azure.microsoft.com/global-infrastructure/china)
    1. [Azure Germany](https://azure.microsoft.com/global-infrastructure/germany) (håller på att ersättas med icke-suveräna Azure-regioner i Tyskland)
    1. [Azure för amerikanska myndigheter](https://azure.microsoft.com/global-infrastructure/government)
    1. Obs! Två regioner i [Australien](https://azure.microsoft.com/global-infrastructure/australia) hanteras av Microsoft, men är avsedda för den australiska regeringen och dess kunder och leverantörer, och har därför liknande klientbegränsningar som de andra suveräna molnen.

## <a name="operate-in-multiple-geographic-regions"></a>Arbeta i flera geografiska regioner

När företag arbetar i flera geografiska områden kan det innebära ytterligare komplexitet, samtidigt som det är nödvändigt för återhämtning. Dessa utmatningar tar sig i uttryck i fyra huvudsakliga former:

- Tillgångsdistribution
- Profiler för användaråtkomst
- Efterlevnadskrav
- Regional återhämtning

I takt med att vi tittar närmare på utmaningarna ovan kommer du att förstå hur viktigt valet av region är för din övergripande molnimplementeringsstrategi. Vi börjar med ett antal nätverksöverväganden.

## <a name="networking-considerations"></a>Nätverksöverväganden

En robust molndistribution kräver ett välfungerande nätverk som tar hänsyn till Azure-regioner. När du har granskat egenskaperna ovan vad gäller valet av region, måste nätverket distribueras. I det här avsnittet går vi inte igenom alla nätverksaspekter, utan fokuserar endast på några få:

- Azure-regioner distribueras i par. I händelse av ett oåterkalleligt fel i en region, är regionen associerad till en annan region inom samma politiska gränser *. Tänk på distributionen i associerade regioner som en primär och sekundär återhämtningsstrategi. \* Azure Brasilien är ett viktigt undantag där den associerade regionen är USA, södra centrala. Mer information finns här: [Azure-länkade regioner](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

  - Azure Storage stöder [geo-redundant lagring (GRS)](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs), vilket innebär att tre kopior av dina data lagras i den primära regionen och ytterligare tre kopior i den associerade regionen. Det går inte att ändra lagringspar för GRS.
  - Tjänster som är beroende av Azure Storage GRS kan dra nytta av funktionen för associerade regioner. För att göra det måste dina program och nätverket konfigureras med stöd för det.
  - Om du inte planerar att använda GRS för regional återhämtning, rekommenderar vi att du _inte_ använder den associerade regionen som sekundär region. I händelse av ett fel i en region, blir trycket på resurser i den associerade regionen stort när resurserna migreras. Genom att undvika detta hårda tryck kan du snabba upp återhämtningen genom att återställa till en alternativ plats.
  > [!WARNING]
  > Försök inte utnyttja Azure GRS för säkerhetskopiering eller återställning av virtuella datorer. Använd i stället [Azure Backup](https://azure.microsoft.com/services/backup) och [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery) tillsammans med [Azure-hanterade diskar](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview) för att stödja återhämtningen av dina IaaS-arbetsbelastningar.

- Azure Backup och Azure Site Recovery fungerar tillsammans med din nätverksdesign för att underlätta regional återhämtning för dina behov av IaaS- och datasäkerhetskopiering. Kontrollera att nätverket är optimerat så att dataöverföringarna sker i Microsofts stamnät och utnyttja [VNet-peering](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) om möjligt. Vissa större organisationer med globala distributioner kan i stället använda [ExpressRoute Premium](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) för att dirigera trafik mellan regioner, vilket kan innebära lägre regionala avgifter för utgående trafik.

- Azures resursgrupper är regionsspecifika konstruktioner. Det är normalt att resurser inom en resursgrupp sträcker sig över flera regioner. Om det uppstår problem i en region så misslyckas åtgärder i kontrollplanet i den berörda regionen, vilket är viktigt att komma ihåg, även om resurserna i andra regioner (i den aktuella resursgruppen) fortsätter fungera. Detta kan påverka både din nätverksdesign och din resursgruppsdesign.

- Många PaaS-tjänster i Azure har stöd för [tjänstslutpunkter](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) och [Private Link](https://docs.microsoft.com/azure/private-link/private-link-overview). Båda dessa lösningar påverkar dina nätverksstrategier avsevärt med avseende på regional återhämtning, migrering och styrning.

- Många PaaS-tjänster är beroende av egna regionala återhämtningslösningar. Med både Azure SQL Database och Cosmos DB kan du till exempel enkelt replikera till _x_ ytterligare regioner. Vissa tjänster är regionsoberoende, t.ex. Azure DNS. När du funderar på vilka tjänster du ska använda i implementeringen är det viktigt att du förstår redundansfunktionerna och återställningsstegen som krävs för respektive Azure-tjänst.

- Förutom att distribuera i flera regioner för att stödja haveriberedskap väljer många organisationer att distribuera i ett ”aktiv-aktiv”-mönster så att ingen redundans krävs. Detta har den extra fördelen med att tillhandahålla global belastningsutjämning, ytterligare feltolerans och bättre nätverksprestanda. För att kunna dra nytta av det här mönstret måste dina program ha stöd för körning av ”aktiv-aktiv” i flera regioner.

> [!WARNING]
> Azure-regioner är konstruktioner med hög tillgänglighet, och tjänsterna som körs i dem täcks av serviceavtal. Du bör dock undvika ett enda regionberoende för verksamhetskritiska program. Planera alltid för regionala fel och vidta återställnings- och riskreduceringsåtgärder.

När du har kommit fram till vilken nätverkstopologi som krävs måste du gå igenom ytterligare dokumentations- och processteg. Följande metod kan underlätta vid utvärdering av potentiella utmaningar och fastställa en allmän åtgärdsplan:

- Överväg en robustare implementering för beredskap och styrning.
- Gör en inventering av de berörda områdena. Sätt ihop en lista med de regioner och länder som påverkas.
- Dokumentera kraven på datasuveränitet. Har de länder som identifierats krav som påverkar datasuveräniteten?
- Dokumentera användarbasen. Kommer anställda, partner eller kunder i det identifierade landet att påverkas av molnmigreringen?
- Dokumentera datacenter och tillgångar. Finns det tillgångar i det identifierade landet som kan beröras av migreringsarbetet?
- Dokumentera krav på regional SKU-tillgänglighet och redundans.

Genomför ändringar i migreringsprocessen för att hantera den inledande inventeringen.

## <a name="document-complexity"></a>Dokumentkomplexitet

Följande tabell kan underlätta dokumentationen av resultaten från stegen ovan:

| Region        | Land/region     | Lokala anställda | Lokala externa användare   | Lokala datacenter eller tillgångar | Krav på datasuveränitet |
|---------------|-------------|-----------------|------------------------|-----------------------------|-------------------------------|
| Nordamerika | USA         | Ja             | Partners och kunder | Ja                         | Inga                            |
| Nordamerika | Kanada      | Inga              | Kunder              | Ja                         | Ja                           |
| Europa        | Tyskland     | Ja             | Partners och kunder | Nej – endast nätverk           | Ja                           |
| Asien och stillahavsområdet  | Sydkorea | Ja             | Partner               | Ja                         | Inga                            |

<!-- markdownlint-disable MD026 -->

## <a name="data-sovereignty-relevancy"></a>Relevans för datasuveränitet

Runt om i världen har statliga organisationer börjat fastställa krav på datasuveränitet, som exempelvis GDPR (dataskyddsförordningen). Krav på efterlevnad av denna typ kräver ofta lokalisering inom en specifik region eller till och med ett visst land för att skydda deras medborgare. I vissa fall måste data som rör kunder, anställda eller partners lagras i en molnplattform i samma region som slutanvändaren.

Att hantera denna utmaning har varit en bakomliggande motivering för molnmigrering för företag som opererar globalt. För att upprätthålla kraven på efterlevnad har vissa företag valt att distribuera duplicerade IT-tillgångar till molnleverantörer i regionen. I tabellen ovan är Tyskland ett bra exempel på det här scenariot. I detta exempel finns det kunder, partner och anställda i Tyskland, men inga befintliga IT-tillgångar. Företaget kan välja att distribuera en del tillgångar till ett datacenter i GDPR-området, potentiellt även Tyska Azure-datacenter. Förståelse av vilka data som berörs av GDPR hjälper teamet för molnimplementering att välja bäst metod för migrering i detta fall.

### <a name="why-is-the-location-of-end-users-relevant"></a>Varför har slutanvändarens placering betydelse?

Företag som arbetar med slutanvändare i flera länder har tagit fram tekniska lösningar för att hantera trafik från slutanvändare. I vissa fall inkluderar detta lokalisering av tillgångar. I andra scenarion kan företaget istället välja att implementera globala WAN-lösningar för att hantera olika användargrupper via nätverksfokuserade lösningar. I samtliga fall kan migreringsstrategin påverkas av dessa olika slutanvändares användningsprofiler.

Eftersom företaget hanterar anställda, partner och kunder i Tyskland men för tillfället inte har datacenter i det landet, är det troligt att företaget implementerat någon form av hyrd nätverkskapacitet för att dirigera trafik till datacenter i andra länder. Denna omdirigering utgör en betydande risk för den upplevda prestandan hos migrerade program. Att infoga ytterligare hopp i ett etablerat och finjusterat WAN kan skapa uppfattningen av att program underpresterar efter migreringen. Att hitta och korrigera dessa problem kan avsevärt försena ett projekt. I var och en av processerna nedan finns vägledning om hur du hanterar denna komplexitet för förutsättningar, utvärdering, migrering och optimering. Att förstå användarprofiler i varje land är avgörande för att hantera den här komplexiteten korrekt.

### <a name="why-is-the-location-of-datacenters-relevant"></a>Varför har datacentrens placering betydelse?

Placeringen av befintliga datacenter kan påverka migreringsstrategin. Följande är några av de vanligaste effekterna:

**Arkitekturbeslut:** Målregionen är ett av de första stegen vid utveckling av en migreringsstrategi. Detta påverkas ofta av de befintliga tillgångarnas placering. Dessutom kan de tillgängliga molntjänsterna och enhetskostnaden för dessa tjänster variera från ett område till ett annat. Därför påverkar placeringen av aktuella och framtida tillgångar arkitekturbeslut och kan även påverka budgetberäkningar.

**Beroenden mellan datacenter:** Baserat på data i tabellen ovan är det troligt att beroenden finns mellan de olika datacentren runt om i världen. I många organisationer som verkar på denna skala kan dessa beroenden vara odokumenterade eller så kan kunskapen vara bristfällig. De metoder som används för att utvärdera användarprofiler kan hjälpa till att hitta en del av dessa beroenden. Ytterligare steg bör dock vidtas under utvärderingsprocessen för att minska riskerna med denna komplexitet.

## <a name="implementing-the-general-approach"></a>Implementera den allmänna metoden

Denna metod drivs av kvantifierbar information. Följande metod kommer därför att följa en datadriven modell för hantering av komplexitet vid global migrering.

När omfånget för en migrering innehåller flera regioner bör följande beredskapsöverväganden utvärderas av teamet för molnimplementering:

- Datasuveränitet kan kräva lokalisering av vissa tillgångar, men det finns många tillgångar som kanske inte styrs av dessa begränsningar. Saker som loggning, rapportering, nätverksroutning, identitet och andra centrala IT-tjänster kan vara möjliga att hantera som delade tjänster över flera prenumerationer eller till och med flera regioner. Molnimplementeringsteamet bör utvärdera användningen av en delad tjänstmodell för dessa tjänster, på det sätt som beskrivs i [referensarkitekturen för en ”nav och eker”-topologi med delade tjänster](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)
- Vid införandet av flera instanser av liknande miljöer kan en miljöfabrik skapa konsekvens, förbättra styrningen och påskynda distributionen. [Styrningsguiden för komplexa företag](../../govern/guides/complex/index.md) fastställer en metod som skapar en miljö som skalar över flera regioner.

När teamet är nöjda med grundmetoden och beredskapen justerats finns det några datadrivna förutsättningar att tänka på:

- **Allmän identifiering:** Fyll i tabellen [Dokumentera komplexitet](#document-complexity) ovan.
- **Utför en användarprofilanalys för varje berört land:** Det är viktigt att förstå allmän routning av slutanvändare tidigt i migreringsprocessen. Att ändra globala hyrda nätverk och lägga till anslutningar som ExpressRoute till ett molndatacenter kan kräva månader av förseningar på grund av nätverket. Hantera detta så tidigt i processen som möjligt.
- **Inledande rationalisering av digitala tillgångar:** När komplexitet införs i migreringsstrategi ska en inledande rationalisering av digitala tillgångar genomföras. Se vägledningen för [rationalisering av digitala tillgångar](../../digital-estate/index.md) för hjälp.
  - **Ytterligare krav för digital egendom:** Ta fram taggningsprinciper som identifierar alla arbetsbelastningar som påverkas av krav på datasuveränitet. Dessa taggar ska påbörjas vid rationaliseringen av digitala tillgångar och följa med till de migrerade tillgångarna.
- **Utvärdera en nav- och ekermodell:** Distribuerade system delar ofta gemensamma beroenden. Dessa beroenden kan ofta hanteras genom implementeringen av en nav- och ekermodell. Även om en sådan modell inte faller inom omfattningen för migrering ska det flaggas för analys vid framtida itereringar av [Färdigprocesser](../../ready/index.md).
- **Prioritering av kvarvarande migreringsuppgifter:** När nätverksändringar krävs för att stödja produktionsdistributionen av en arbetsbelastning som har stöd för flera regioner är det viktigt att teamet för molnstrategi spårar och hanterar eskaleringar om dessa ändringar i nätverket. Stöd från den högre ledningen underlättar förändringen. Det är dock viktigare att det ger strategi-teamet möjlighet att omprioritera kvarvarande punkter för att säkerställa att globala arbetsbelastningar inte blockeras av nätverksändringar. Sådana arbetsbelastningar ska endast prioriteras efter att nätverksändringarna slutförts.

Dessa förutsättningar ger möjlighet att skapa processer som kan hantera denna komplexitet under genomförandet av migreringsstrategin.

## <a name="assess-process-changes"></a>Utvärdera processändringar

När du hanterar komplexitet relaterad till globala tillgångar och användare finns det några viktiga aktiviteter som bör läggas till i utvärderingen av alla kandidater för migrering. Alla dessa ändringar kommer att ge mer information om påverkan på globala användare och tillgångar med en datadriven metod.

### <a name="suggested-action-during-the-assess-process"></a>Föreslagna åtgärder under utvärderingsprocessen

**Utvärdera beroenden mellan datacenter:** [Verktygen för beroendevisualisering i Azure Migrate](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization) kan underlätta identifieringen av beroenden. Vi rekommenderar att du använder dessa verktyg innan du migrerar. När det gäller komplexitet på global nivå är det dock ett nödvändigt steg i utvärderingsprocessen. Genom [beroendegruppering](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies) kan visualiseringen underlätta identifieringen av IP-adresser och portar för alla tillgångar som krävs för att hantera arbetsbelastningen.

> [!IMPORTANT]
> Två viktiga kommentarer: Först så krävs en ämnesexpert med förståelse för tillgångsplacering och IP-adresscheman för att identifiera tillgångar som ligger i sekundära datacenter. Sedan är det viktigt att utvärdera både underordnade beroenden och klienter visuellt för att förstå dubbelriktade beroenden.

**Identifiera global användarpåverkan:** Data från de nödvändiga användarprofilanalyserna ska identifiera alla arbetsbelastningar som påverkas av globala användarprofiler. När en migreringskandidat är i listan över påverkade arbetsbelastningar bör arkitekten som förbereder migreringen rådgöra med experter på nätverk och drift för att validera nätverksroutning och prestandaförväntningar. Som minst bör arkitekturen inkludera en ExpressRoute-anslutning mellan närmaste nätverksdriftcenter (NOC) och Azure. [Referensarkitekturen för ExpressRoute](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/expressroute)-anslutningar kan vara till hjälp vid konfigurationen av anslutningen.

**Designa för efterlevnad:** Data från de nödvändiga användarprofilanalyserna ska identifiera alla arbetsbelastningar som påverkas av krav på datasuveränitet. Under arkitekturaktiviteterna i utvärderingsprocessen ska den tilldelade arkitekten rådfråga experter på efterlevnad för att förstå eventuella krav för migrering/distribution över flera regioner. Dessa krav kommer ha stor påverkan på designstrategierna. Referensarkitekturer för [webbprogram som används i flera regioner](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) och [N-nivåprogram som används i flera regioner](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) kan vara till hjälp vid designen.

> [!WARNING]
> När du använder någon av referensarkitekturerna ovan kan det vara nödvändigt att undanta vissa dataelement från replikeringsprocesser för att uppfylla krav på datasuveränitet. Det innebär ett extra steg i befordringsprocessen.

## <a name="migrate-process-changes"></a>Ändringar i migreringsprocessen

När ett program som ska distribueras till flera regioner migreras finns det vissa saker att ta hänsyn till. Dessa överväganden gäller design av Azure Site Recovery-valv, design av konfiguration/processerver, design av nätverksbandbredd och datasynkronisering.

### <a name="suggested-action-during-the-migrate-process"></a>Föreslagna åtgärder under migreringsprocessen

**Design av Azure Site Recovery-valv:** Azure Site Recovery är det rekommenderade verktyget för replikering i molnet och synkronisering av digitala tillgångar till Azure. Site Recovery replikerar data om tillgången till ett Site Recovery-valv som är kopplat till en viss prenumeration i en viss region och ett visst Azure-datacenter. Vid replikering till en andra region kan det krävas ett andra Site Recovery-valv.

**Design av konfiguration/processerver:** Site Recovery fungerar med en lokal instans av en konfigurations- och processerver som är kopplad till ett enskilt Site Recovery-valv. Detta innebär att en andra instans av dessa servrar kan behöva installeras i källdatacentret för att underlätta replikering.

**Design av nätverksbandbredd:** Under replikering och pågående synkronisering flyttas binärt data över nätverket från källdatacentret till Site Recovery-valvet i Azure-datacentret. Denna process förbrukar bandbredd. Duplicering av en arbetsbelastning till en andra region fördubblar den förbrukade bandbredden. När bandbredden är begränsad eller en arbetsbelastning innebär en stor mängd avvikelser för konfiguration och data kan det påverka den tid det tar att genomföra migreringen. Det kan dessutom påverka upplevelsen för användare eller program som fortfarande använder källdatacentrets bandbredd.

**Datasynkronisering:** Ofta utgör synkronisering av data den största förbrukaren av bandbredd. Som definierat i referensarkitekturer för [webbprogram som används i flera regioner](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) och [N-nivåprogram som används i flera regioner](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) krävs ofta synkronisering för att programmen ska hållas uppdaterade och funktionella. Om detta är det önskade operativa läget för programmet kan det vara klokt att slutföra en synkronisering mellan källdataplattformen och var och en av molnplattformarna innan du migrerar programmet och tillgångar på mellannivå.
**Datasynkronisering:** Ofta utgör synkronisering av data den största förbrukaren av bandbredd. Som definierat i referensarkitekturer för [webbprogram som används i flera regioner](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) och [N-nivåprogram som används i flera regioner](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) krävs ofta synkronisering för att programmen ska hållas uppdaterade och funktionella. Om detta är det önskade operativa läget för programmet kan det vara klokt att slutföra en synkronisering mellan källdataplattformen och var och en av molnplattformarna innan du migrerar programmet och tillgångar på mellannivå.

**Azure-till-Azure-haveriåterställning:** Ett annat alternativ kan minska komplexiteten ytterligare. Om tidslinjer och datasynkronisering närmar sig ett införande i två steg, kan [Azure-till-Azure-haveriåterställning](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-architecture) vara en acceptabel lösning. I detta scenario migreras arbetsbelastningen till det första Azure-datacentret med ett enda Site Recovery-valv och en konfiguration eller processerverdesign. När arbetsbelastningen testats kan den återställas till ett andra Azure-datacenter från de migrerade tillgångarna. Denna metod minskar påverkan på resurserna i det ursprungliga datacentret och utnyttjar de höga hastigheterna för dataöverföring mellan Azure-datacenter.

> [!NOTE]
> Den här metoden kan öka den kortsiktiga kostnaden för migrering eftersom det kan leda till ytterligare avgifter för utgående bandbredd.

## <a name="optimize-and-promote-process-changes"></a>Optimera och höja upp processändringar

Att hantera global komplexitet under optimeringen och befordran kan kräva dubbla ansträngningar i varje ytterligare region. När en enskild distribution är godtagbar kan duplicering av planer för verksamhetstestning och verksamhetsändring ändå krävas.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Föreslagna åtgärder i samband med optimering och befordran

**Optimering innan test:** Inledande automatisk testning kan identifiera möjliga optimeringsmöjligheter, precis som vid all migrering. När det gäller globala arbetsbelastningar är det viktigt att testa arbetsbelastningen i varje region oberoende av varandra, eftersom mindre konfigurationsändringar i nätverket eller Azure-datacenter kan påverka prestandan.

**Planer för verksamhetsändring:** I komplexa migreringsscenarier bör en verksamhetsförändringsplan skapas för att säkerställa en tydlig kommunikation kring ändringar i affärsprocesser, användarupplevelsen och tidsplanen för implementeringen av ändringarna. När det gäller global migrering bör planen innehålla överväganden för slutanvändare i varje berört område.

**Verksamhetstestning:** I samband med planen för verksamhetsförändringar kan verksamhetstestning krävas i varje region för att säkerställa tillräcklig prestanda och att de ändrade mönstren för nätverksroutning följs.

**Befordran av förhandsversion:** Ofta sker befordran som en enda aktivitet, med omdirigering av produktionstrafik till de migrerade arbetsbelastningarna. Globala versioner bör levereras i form av förhandsversioner (eller fördefinierade användargrupper). Det gör att teamet för molnstrategi och molnimplementering bättre kan observera prestandan och förstärka support för användare i varje område. Befordran av förhandsversionen styrs ofta på nätverksnivå genom att ändra routningen för specifika IP-adressintervall från den ursprungliga tillgången till den migrerade tillgången. När en specifik grupp slutanvändare migrerats kan nästa grupp dirigeras om.

**Optimering av förhandsversioner:** En av fördelarna med förhandsversioner är att det ger möjlighet till noggrannare observationer och ytterligare optimering av de distribuerade tillgångarna. Efter en kort tids användning av den första förhandsversionen föreslås ytterligare förbättringar av de migrerade tillgångarna, om så är möjligt med tanke på IT-driften.
