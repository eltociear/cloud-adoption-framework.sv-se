---
title: Hantera komplexiteten vid migrering av flera geografiska områden
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Hantera komplexiteten vid migrering av flera geografiska områden.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 2d834b9e7c3e661561dc44b8d3104ef819f0c6af
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025491"
---
# <a name="multiple-geographic-regions"></a>Flera geografiska områden

När företag verkar i flera geografiska områden kan det leda till ytterligare komplexitet i arbetet med molnmigrering. Denna komplexitet tar sig i huvudsak tre olika former: tillgångsdistribuering, profiler för användartillgång och efterlevnadskrav. Innan man tar itu med komplexiteter som rör flera områden är det viktigt att förstå omfånget av den potentiella komplexiteten.

## <a name="general-scope-expansion"></a>Allmän omfångsutökning

Följande metod kan underlätta vid utvärdering av potentiella utmaningar och fastställa en allmän åtgärdsplan:

- Överväg en robustare implementering för beredskap och styrning.
- Gör en inventering av de berörda områdena. Skapa en lista med de områden och länder som påverkas av molnmigreringen.
- Dokumentera krav på datasuveränitet: Har de länder som identifierats krav som påverkar datasuveräniteten?
- Dokumentera användarbasen: Kommer anställda, partner eller kunder i det identifierade landet att påverkas av molnmigreringen?
- Dokumentera datacenter och tillgångar: Finns det tillgångar i det identifierade landet som kan beröras av migreringsarbetet?

Genomför ändringar i migreringsprocessen för att hantera den inledande inventeringen.

### <a name="documenting-complexity"></a>Dokumentera komplexitet

Följande tabell kan underlätta dokumentationen av resultaten från stegen ovan:

|Region  |Country  |Lokala anställda  |Lokala externa användare  |Lokala datacenter eller tillgångar |Krav på datasuveränitet  |
|---------|---------|---------|---------|---------|---------|
|Nordamerika     |USA         |Ja         |Partners och kunder         |Ja         |Nej         |
|Nordamerika     |Kanada         |Nej         |Kunder         |Ja         |Ja         |
|Europa     |Tyskland         |Ja         |Partners och kunder         |Nej – endast nätverk         |Ja         |
|Asien och stillahavsområdet     |Sydkorea         |Ja         |Partner         |Ja         |Nej         |

<!-- markdownlint-disable MD026 -->

### <a name="why-is-data-sovereignty-relevant"></a>Varför är datasuveränitet relevant?

Runt om i världen har statliga organisationer börjat fastställa krav på datasuveränitet, som exempelvis GDPR (dataskyddsförordningen). Krav på efterlevnad av denna typ kräver ofta lokalisering inom en specifik region eller till och med ett visst land för att skydda deras medborgare. I vissa fall måste data som rör kunder, anställda eller partners lagras i en molnplattform i samma region som slutanvändaren.

Att hantera denna utmaning har varit en bakomliggande motivering för molnmigrering för företag som opererar globalt. För att upprätthålla kraven på efterlevnad har vissa företag valt att distribuera duplicerade IT-tillgångar till molnleverantörer i regionen. I exemplet ovan är Tyskland ett bra exempel på detta scenario. I detta exempel finns det kunder, partners och anställda i Tyskland, men inga befintliga IT-tillgångar. Företaget kan välja att distribuera en del tillgångar till ett datacenter i GDPR-området, potentiellt även Tyska Azure-datacenter. Förståelse av vilka data som berörs av GDPR hjälper teamet för molnimplementering att välja bäst metod för migrering i detta fall.

### <a name="why-is-the-location-of-end-users-relevant"></a>Varför har slutanvändarens placering betydelse?

Företag som arbetar med slutanvändare i flera länder har tagit fram tekniska lösningar för att hantera trafik från slutanvändare. I vissa fall inkluderar detta lokalisering av tillgångar. I andra scenarion kan företaget istället välja att implementera globala WAN-lösningar för att hantera olika användargrupper via nätverksfokuserade lösningar. I samtliga fall kan migreringsstrategin påverkas av dessa olika slutanvändares användningsprofiler.

Eftersom företaget hanterar anställda, partners och kunder i Tyskland men för tillfället inte har datacenter i det landet, är det troligt att företaget implementerat någon form av hyrd nätverkskapacitet för att dirigera trafik till datacenter i andra länder. Denna omdirigering utgör en betydande risk för den upplevda prestandan hos migrerade program. Att infoga ytterligare hopp i ett etablerat och finjusterat WAN kan skapa uppfattningen av att program underpresterar efter migreringen. Att hitta och korrigera dessa problem kan avsevärt försena ett projekt. I var och en av processerna nedan finns vägledning om hur du hanterar denna komplexitet för förutsättningar, utvärdering, migrering och optimering. Att förstå användarprofiler i varje land är avgörande för att hantera den här komplexiteten korrekt.

### <a name="why-is-the-location-of-datacenters-relevant"></a>Varför har datacentrens placering betydelse?

Placeringen av befintliga datacenter kan påverka migreringsstrategin. Följande är några av de vanligaste effekterna:

**Arkitekturbeslut:** Målregion/plats är ett av de första stegen vid utveckling av en migreringsstrategi. Detta påverkas ofta av de befintliga tillgångarnas placering. Dessutom kan de tillgängliga molntjänsterna och enhetskostnaden för dessa tjänster variera från ett område till ett annat. Därför påverkar placeringen av aktuella och framtida tillgångar arkitekturbeslut och kan även påverka budgetberäkningar.

**Beroenden mellan datacenter:** Baserat på data i tabellen ovan är det troligt att beroenden finns mellan de olika datacentren runt om i världen. I många organisationer som verkar på denna skala kan dessa beroenden vara odokumenterade eller så kan kunskapen vara bristfällig. De metoder som används för att utvärdera användarprofiler kan hjälpa till att hitta en del av dessa beroenden. Ytterligare steg bör dock vidtas under utvärderingsprocessen för att minska riskerna med denna komplexitet.

## <a name="implementing-the-general-approach"></a>Implementera den allmänna metoden

Denna metod drivs av kvantifierbar information. Följande metod kommer därför att följa en datadriven modell för hantering av komplexitet vid global migrering.

## <a name="suggested-prerequisites"></a>Föreslagna förutsättningar

Teamet för molnimplementering bör börja med migreringen av en enkel arbetsbelastning enligt [Guide för Azure-migrering](../azure-migration-guide/index.md) innan försök görs att hantera migreringen globalt. Detta säkerställer att teamet känner till den allmänna processen för molnmigrering innan de försöker sig på en komplex migrering.

När omfånget för en migrering innehåller flera regioner bör följande beredskapsöverväganden utvärderas av teamet för molnimplementering:

- Datasuveränitet kan kräva lokalisering av vissa till gångar, men det finns många till gångar som kanske inte styrs av dessa begränsningar. Saker som loggning, rapportering, nätverksroutning, identitet och andra centrala IT-tjänster kan vara möjliga att hantera som delade tjänster över flera prenumerationer eller till och med flera regioner. Teamet för molnimplementering bör utvärderar en modell för delade tjänster för dessa tjänster, enligt beskrivningen i [referensarkitektur för en nav- och eker-topologi med delade tjänster](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)
- Vid införandet av flera instanser av liknande miljöer kan en miljöfabrik skapa konsekvens, förbättra styrningen och påskynda distributionen. [Styrningsresa för stora företag](../../govern/guides/complex/index.md) fastställer en metod som skapar en miljöfabrik som skalar över flera regioner.

När teamet är nöjda med grundmetoden och beredskapen justerats finns det några datadrivna förutsättningar att tänka på:

- **Allmän identifiering:** Fyll i tabellen [Dokumentera komplexitet](#documenting-complexity) ovan.
- **Utför en användarprofilanalys för varje berört land:** Det är viktigt att förstå allmän routning av slutanvändare tidigt i migreringsprocessen. Att ändra globala hyrda nätverk och lägga till anslutningar som ExpressRoute till ett molndatacenter kan kräva månader av förseningar på grund av nätverket. Hantera detta så tidigt i processen som möjligt.
- **Inledande rationalisering av digitala tillgångar:** När komplexitet införs i migreringsstrategi ska en inledande rationalisering av digitala tillgångar genomföras. Se vägledningen för [rationalisering av digitala tillgångar](../../digital-estate/index.md) för hjälp.
  - **Ytterligare krav för digital egendom:** Ta fram taggningsprinciper som identifierar alla arbetsbelastningar som påverkas av krav på datasuveränitet. Dessa taggar ska påbörjas vid rationaliseringen av digitala tillgångar och följa med till de migrerade tillgångarna.
- **Utvärdera en nav- och ekermodell:** Distribuerade system delar ofta gemensamma beroenden. Dessa beroenden kan ofta hanteras genom implementeringen av en nav- och ekermodell. Även om en sådan modell inte faller inom omfattningen för migrering ska det flaggas för analys vid framtida itereringar av [Färdigprocesser](../../ready/index.md).
- **Prioritering av kvarvarande migreringsuppgifter:** När nätverksändringar krävs för att stödja produktionsdistributionen av en arbetsbelastning som har stöd för flera regioner är det viktigt att teamet för molnstrategi spårar och hanterar eskaleringar om dessa ändringar i nätverket. Stöd från den högre ledningen underlättar förändringen. Det är dock viktigare att det ger strategi-teamet möjlighet att omprioritera kvarvarande punkter för att säkerställa att globala arbetsbelastningar inte blockeras av nätverksändringar. Sådana arbetsbelastningar ska endast prioriteras efter att nätverksändringarna slutförts.

Dessa förutsättningar ger möjlighet att skapa processer som kan hantera denna komplexitet under genomförandet av migreringsstrategin.

## <a name="assess-process-changes"></a>Utvärdera ändringar i processen

När du hanterar komplexitet relaterad till globala tillgångar och användare finns det några viktiga aktiviteter som ska läggas till i utvärderingen av alla kandidater för migrering. Alla dessa ändringar kommer att ge mer information om påverkan på globala användare och tillgångar med en datadriven metod.

### <a name="suggested-action-during-the-assess-process"></a>Föreslagna åtgärder under utvärderingsprocessen

**Utvärdera beroenden mellan datacenter:** [Verktygen för beroendevisualisering i Azure Migrate](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization) kan underlätta identifieringen av beroenden. Att använda denna verktygsuppsättning innan migrering är ett bra allmänt regelverk. När det gäller komplexitet på global nivå är det dock ett nödvändigt steg i utvärderingsprocessen. Genom [beroendegruppering](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies) kan visualiseringen underlätta identifieringen av IP-adresser och portar för alla tillgångar som krävs för att hantera arbetsbelastningen.

> [!IMPORTANT]
> Två viktiga kommentarer: Först så krävs en ämnesexpert med förståelse för tillgångsplacering och IP-adresscheman för att identifiera tillgångar som ligger i sekundära datacenter. Sedan är det viktigt att utvärdera både underordnade beroenden och klienter visuellt för att förstå dubbelriktade beroenden.

**Identifiera global användarpåverkan:** Data från de nödvändiga användarprofilanalyserna ska identifiera alla arbetsbelastningar som påverkas av globala användarprofiler. När en migreringskandidat är i listan över påverkade arbetsbelastningar bör arkitekten som förbereder migreringen rådgöra med experter på nätverk och drift för att validera nätverksroutning och prestandaförväntningar. Som minst bör arkitekturen inkludera en ExpressRoute-anslutning mellan närmaste NOC och Azure. [Referensarkitekturen för ExpressRoute](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/expressroute)-anslutningar kan vara till hjälp vid konfigurationen av anslutningen.

**Designa för efterlevnad:** Data från de nödvändiga användarprofilanalyserna ska identifiera alla arbetsbelastningar som påverkas av krav på datasuveränitet. Under arkitekturaktiviteterna i utvärderingsprocessen ska den tilldelade arkitekten rådfråga experter på efterlevnad för att förstå eventuella krav för migrering/distribution över flera regioner. Dessa krav kommer ha stor påverkan på designstrategierna. Referensarkitekturer för [webbprogram som används i flera regioner](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) och [N-nivåprogram som används i flera regioner](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) kan vara till hjälp vid designen.

> [!WARNING]
> När du använder någon av referensarkitekturerna ovan kan det vara nödvändigt att undanta vissa dataelement från replikeringsprocesser för att uppfylla krav på datasuveränitet. Det innebär ett extra steg i befordringsprocessen.

## <a name="migrate-process-changes"></a>Ändringar i migreringsprocessen

Vid migrering av ett program som måste distribueras till olika regioner finns det några överväganden som teamet för molnimplementering måste ta hänsyn till. Dessa överväganden gäller design av Azure Site Recovery-valv, design av konfiguration/processerver, design av nätverksbandbredd och datasynkronisering.

### <a name="suggested-action-during-the-migrate-process"></a>Föreslagna åtgärder under migreringsprocessen

**Design av Azure Site Recovery-valv:** Azure Site Recovery är det rekommenderade verktyget för replikering i molnet och synkronisering av digitala tillgångar till Azure. Site Recovery replikerar data om tillgången till ett Site Recovery-valv som är kopplat till en viss prenumeration i en viss region och ett visst Azure-datacenter. Vid replikering till en andra region kan det krävas ett andra Site Recovery-valv.

**Design av konfiguration/processerver:** Site Recovery fungerar med en lokal instans av en konfigurations- och processerver som är kopplad till ett enskilt Site Recovery-valv. Detta innebär att en andra instans av dessa servrar kan behöva installeras i källdatacentret för att underlätta replikering.

**Design av nätverksbandbredd:** Under replikering och pågående synkronisering flyttas binärt data över nätverket från källdatacentret till Site Recovery-valvet i Azure-datacentret. Denna process förbrukar bandbredd. Duplicering av en arbetsbelastning till en andra region fördubblar den förbrukade bandbredden. När bandbredden är begränsad eller en arbetsbelastning innebär en stor mängd avvikelser för konfiguration och data kan det påverka den tid det tar att genomföra migreringen. Det kan dessutom påverka upplevelsen för användare eller program som fortfarande använder källdatacentrets bandbredd.

**Datasynkronisering:** Ofta utgör synkronisering av data den största förbrukaren av bandbredd. Som definierat i referensarkitekturer för [webbprogram som används i flera regioner](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) och [N-nivåprogram som används i flera regioner](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) krävs ofta synkronisering för att programmen ska hållas uppdaterade och funktionella. Om detta är det önskade operativa läget för programmet kan det vara klokt att slutföra en synkronisering mellan källdataplattformen och var och en av molnplattformarna innan du migrerar programmet och tillgångar på mellannivå.
**Datasynkronisering:** Ofta utgör synkronisering av data den största förbrukaren av bandbredd. Som definierat i referensarkitekturer för [webbprogram som används i flera regioner](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) och [N-nivåprogram som används i flera regioner](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) krävs ofta synkronisering för att programmen ska hållas uppdaterade och funktionella. Om detta är det önskade operativa läget för programmet kan det vara klokt att slutföra en synkronisering mellan källdataplattformen och var och en av molnplattformarna innan du migrerar programmet och tillgångar på mellannivå.

**Azure-till-Azure-haveriåterställning:** Det finns ett alternativ som kan minska komplexiteten ytterligare. Om tidslinjer och datasynkronisering närmar sig ett införande i två steg, kan [Azure-till-Azure-haveriåterställning](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-architecture) vara en acceptabel lösning. I detta scenario migreras arbetsbelastningen till det första Azure-datacentret med ett enda Site Recovery-valv och en konfiguration eller processerverdesign. När arbetsbelastningen testats kan den återställas till ett andra Azure-datacenter från de migrerade tillgångarna. Denna metod minskar påverkan på resurserna i det ursprungliga datacentret och utnyttjar de höga hastigheterna för dataöverföring mellan Azure-datacenter.

> [!NOTE]
> Den här metoden kan öka den kortsiktiga kostnaden för migrering eftersom det kan leda till ytterligare avgifter för utgående bandbredd.

## <a name="optimize-and-promote-process-changes"></a>Optimera och flytta upp processändringar

Att hantera global komplexitet under optimeringen och befordran kan kräva dubbla ansträngningar i varje ytterligare region. När en enskild distribution är godtagbar kan duplicering av planer för verksamhetstestning och verksamhetsändring ändå krävas.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Föreslagna åtgärder i samband med optimering och befordran

**Optimering innan test:** Inledande automatisk testning kan identifiera möjliga optimeringsmöjligheter, precis som vid all migrering. När det gäller globala arbetsbelastningar är det viktigt att testa arbetsbelastningen i varje region oberoende av varandra, eftersom mindre konfigurationsändringar i nätverket eller Azure-datacenter kan påverka prestandan.

**Planer för verksamhetsändring:** I ett scenario med komplex migrering rekommenderas att en verksamhetsförändringsplan skapas för att säkerställa en tydlig kommunikation om eventuella ändringar i affärsprocesser, användarupplevelser och tidpunkten för de ansträngningar som krävs för att genomföra ändringarna. När det gäller global migrering bör planen innehålla överväganden för slutanvändare i varje berört område.

**Verksamhetstestning:** I samband med planen för verksamhetsförändringar kan verksamhetstestning krävas i varje region för att säkerställa tillräcklig prestanda och att de ändrade mönstren för nätverksroutning följs.

**Befordran av förhandsversion:** Ofta sker befordran som en enda aktivitet, med omdirigering av produktionstrafik till de migrerade arbetsbelastningarna. Vid global publicering rekommenderas att befordran sker med förhandsversioner (eller fördefinierade grupper av användare). Det gör att teamet för molnstrategi och molnimplementering bättre kan observera prestandan och förstärka support för användare i varje område. Befordran av förhandsversionen styrs ofta på nätverksnivå genom att ändra routningen för specifika IP-adressintervall från den ursprungliga tillgången till den migrerade tillgången. När en specifik grupp slutanvändare migrerats kan nästa grupp dirigeras om.

**Optimering av förhandsversioner:** En av fördelarna med förhandsversioner är att det ger möjlighet till noggrannare observationer och ytterligare optimering av de distribuerade tillgångarna. Efter en kort tids användning av den första förhandsversionen föreslås ytterligare förbättringar av de migrerade tillgångarna, om så är möjligt med tanke på IT-driften.

## <a name="next-steps"></a>Nästa steg

En annan punkt som ger upphov till komplexitet och ofta är relaterad till förekomsten av flera olika regioner, är behovet av att förbereda migrering av [flera datacenter](./multiple-datacenters.md). Även om de delvis liknar varandra gäller denna komplexitet volymen av tillgångar som ska migreras när flera datacenter flyttas till molnet.

> [!div class="nextstepaction"]
> [Migrera flera datacenter](./multiple-datacenters.md)
