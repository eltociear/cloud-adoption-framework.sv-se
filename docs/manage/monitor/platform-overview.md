---
title: 'Övervaknings guide för molnet: översikt över Monitoring Platforms'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Välj när Azure Monitor eller System Center Operations Manager ska användas i Microsoft Azure.
author: mgoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 668710d38fe6d3aa03761580f530f484133df792
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72547260"
---
# <a name="cloud-monitoring-guide-monitoring-platforms-overview"></a>Övervaknings guide för molnet: översikt över Monitoring Platforms

Microsoft tillhandahåller ett antal övervaknings funktioner från två produkter: System Center Operations Manager som har utformats lokalt och sedan utökats till molnet och Azure Monitor, som har utformats för molnet, men som även kan övervaka lokala system . Dessa två erbjudanden levererar grundläggande övervaknings tjänster, t. ex. avisering, service drift tids spårning, övervakning av program och infrastruktur hälsa, diagnostik och analys.

Många organisationer använder de senaste metoderna för DevOps rörlighet och moln innovationer för att hantera sina heterogena-miljöer. De är ännu bekymrade över sin förmåga att fatta lämpliga och ansvariga beslut om hur du övervakar arbets belastningarna.

Den här artikeln innehåller en översikt över våra övervaknings plattformar som hjälper dig att förstå hur båda levererar grundläggande övervaknings funktioner.

## <a name="story-of-system-center-operations-manager"></a>Berättelse i System Center Operations Manager

I 2000 angav vi åtgärds hanterings fältet med Microsoft Operations Manager (MOM) 2000. I 2007 introducerade vi en ny version av produkten med namnet System Center Operations Manager. Den har flyttats bortom enkel övervakning av en Windows Server och koncentrerats på robust, fullständig tjänst och program övervakning, inklusive heterogena-plattformar, nätverks enheter och andra program-eller tjänst beroenden. Det är en etablerad övervaknings plattform i företags klass för lokala miljöer i samma klass som IBM Tivoli eller HP Operations Manager i branschen. Den har växt för att stödja övervakning av beräknings-och plattforms resurser som körs i Azure, Amazon Web Services (AWS) och andra moln leverantörer.

## <a name="story-of-azure-monitor"></a>Berättelse i Azure Monitor

När Azure släpptes i 2010 tillhandahölls övervakning av moln tjänster med Azure-diagnostik-agenten, som tillhandahöll ett sätt att samla in diagnostikdata från Azure-resurser. Den här funktionen betraktades som ett allmänt övervaknings verktyg snarare än en övervaknings plattform i företags klass.  

Application Insights har introducerats för att växla till förändringar i branschen där spridning av moln-, mobil-och IoT-enheter växer och införandet av DevOps-metoder. Den har utvecklats från övervakning av program prestanda i Operations Manager till en tjänst i Azure, där den ger omfattande övervakning av webb program som har skrivits på flera olika språk. I 2015 har förhands granskningen av Application Insights för Visual Studio annonser ATS och senare beskrevs den precis som Application Insights. Den samlar in information om program prestanda, begär Anden och undantag och spårningar.

I 2015 gjordes Azure Operational Insights allmänt tillgänglig. Den levererade tjänsten Log Analytics Analysis som samlar in och sökte efter data från datorer i Azure, lokalt eller i andra moln miljöer och är anslutna till System Center Operations Manager. Intelligence-paket erbjöds som levererade olika förpaketerade hanterings-och övervaknings konfigurationer som innehöll en samling frågor och analys logik, visualiseringar och data insamlings regler för sådana scenarier som säkerhets granskning, hälsa utvärderingar och aviserings hantering. Senare är Azure Operational Insights känt som Log Analytics.  

I 2016 annonserades förhands granskningen av Azure Monitor. Det tillhandahöll ett gemensamt ramverk för att samla in plattforms mått, resurs-diagnostikloggar och aktivitets logg händelser på prenumerations nivå från alla Azure-tjänster som har börjat använda ramverket. Tidigare hade varje Azure-tjänst sin egen övervaknings metod.

På Microsoft antändnings konferens i 2018 presenterade vi att Azure Monitor varumärket har utökats för att omfatta flera olika tjänster som ursprungligen utvecklades med oberoende funktioner:

- De ursprungliga **Azure Monitor** funktionerna i att samla in plattforms mått, Resource Diagnostics-loggar och aktivitets loggar för Azures plattforms resurser.
- **Application Insights** för program övervakning.
- **Log Analytics** som primär plats för insamling och analys av loggdata.
- En ny **enhetlig aviserings tjänst** som sammanställer aviserings metoder från var och en av de andra tjänsterna ovan.  
- **Azure Network Watcher** för att övervaka, diagnostisera och visa mått för resurser i ett virtuellt Azure-nätverk.

## <a name="the-story-of-operations-management-suite-oms"></a>Artikeln om Operations Management Suite (OMS)

Från 2015 till och med den 2018 april är Operations Management Suite (OMS) en databunt av följande Azure-hanterings tjänster i licens syfte:

- Application Insights
- Azure Automatisering
- Azure Backup
- Operational Insights (senare den ommärkes Log Analytics)
- Webbplatsåterställning

Funktionerna i de tjänster som var en del av OMS ändrades inte när OMS skulle upphöra, de justerades under Azure Monitor.

## <a name="infrastructure-requirements"></a>Infrastruktur krav

### <a name="operations-manager"></a>Operations Manager

Operations Manager kräver betydande infrastruktur och underhåll för att stödja en hanterings grupp, vilket är en grundläggande enhet med funktioner. Som minst består en hanterings grupp av en eller flera hanterings servrar, en SQL Server som är värd för driften och informationslager för rapportering databasen och agenter. Designen av en hanterings grupp är beroende av ett antal faktorer, till exempel omfattningen av arbets belastningar som ska övervakas och hur många enheter eller datorer som har stöd för arbets belastningarna. Om du behöver hög tillgänglighet och plats återhämtning, som ofta är fallet med Enterprise Monitoring Platforms, kan infrastruktur krav och tillhör ande underhåll öka dramatiskt.

![Diagram över Operations Manager hanterings grupp](./media/monitoring-management-guidance-cloud-and-on-premises/operations-manager-management-group-optimized.svg)

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor är en SaaS-tjänst där all infrastruktur som stöder den körs i Azure och hanteras av Microsoft. Den är utformad för att utföra övervakning, analys och diagnostik i skala och är tillgänglig i alla nationella moln. Kärn delar av infrastrukturen (insamlare, mått och loggar och-analys) som krävs för att stödja Azure Monitor underhålls av Microsoft.  

![Diagram över Azure Monitor](./media/monitoring-management-guidance-cloud-and-on-premises/azure-monitor-greyed-optimized.svg)

## <a name="data-collection"></a>Datainsamling

### <a name="operations-manager"></a>Operations Manager

#### <a name="agents"></a>Agenter

Operations Manager samlar endast in data direkt från agenter som är installerade på [Windows-datorer](https://docs.microsoft.com//system-center/scom/plan-planning-agent-deployment?view=sc-om-1807#windows-agent). Den kan ta emot data från Operations Manager SDK, men det används vanligt vis för partner som utökar produkten med anpassade program, inte för att samla in övervaknings data. Den kan samla in data från andra källor, till exempel [Linux-datorer](https://docs.microsoft.com/system-center/scom/plan-planning-agent-deployment?view=sc-om-1807#linuxunix-agent) och nätverks enheter, genom att använda särskilda moduler som körs på Windows-agenten via fjärr anslutning till de här andra enheterna.

![Diagram över Operations Manager agent](./media/monitoring-management-guidance-cloud-and-on-premises/data-collection-opsman-agents-optimized.svg)

Operations Manager agenten kan samla in från flera data källor på den lokala datorn, till exempel händelse loggen, anpassade loggar och prestanda räknare. Det kan också köra skript som kan samla in data från den lokala datorn eller från externa källor. Du kan skriva anpassade skript för att samla in data som inte kan samlas in på annat sätt eller från en mängd olika fjärranslutna enheter som annars inte kan övervakas.

#### <a name="management-packs"></a>Hanteringspaket

Operations Manager utför all övervakning med arbets flöden (regler, övervakare och objekt identifieringar). Dessa paketeras tillsammans i ett [hanterings paket](https://docs.microsoft.com/system-center/scom/manage-overview-management-pack?view=sc-om-2019)och distribueras till agenter. Det finns hanterings paket för olika produkter och tjänster som innehåller fördefinierade regler och övervakare. Du kan också skapa egna hanterings paket för dina egna program och anpassade scenarier.

#### <a name="monitoring-configuration"></a>Övervaknings konfiguration

Hanterings paket kan innehålla hundratals regler, övervakare och regler för objekt identifiering. En agent kör alla dessa övervaknings inställningar från alla hanterings paket som gäller, vilket bestäms av identifierings regler. Varje instans av varje övervaknings inställning körs oberoende och fungerar omedelbart på de data som samlas in. Så här kan Operations Manager uppnå aviseringar i nära real tid och det aktuella hälso tillståndet för övervakade resurser.

En övervakare kan till exempel sampla en prestanda räknare med några minuters mellanrum. Om räknaren överskrider ett tröskelvärde anger den omedelbart hälso tillståndet för dess mål objekt, vilket omedelbart utlöser en avisering i hanterings gruppen. En schemalagd regel kan se till att en viss händelse skapas och direkt utlösa en avisering när händelsen skapas i den lokala händelse loggen.

Eftersom dessa övervaknings inställningar är isolerade från varandra och fungerar från enskilda data källor, Operations Manager har utmaningar som korrelerar data mellan flera källor. Det är också svårt att reagera på data när de har samlats in. Du kan köra arbets flöden som har åtkomst till Operations Manager databasen, men det här scenariot är inte gemensamt och används vanligt vis för ett begränsat antal arbets flöden för särskilda syften.

![Diagram över Operations Manager hanterings grupp](./media/monitoring-management-guidance-cloud-and-on-premises/operations-manager-management-group-optimized.svg)

### <a name="azure-monitor"></a>Azure Monitor

#### <a name="data-sources"></a>Datakällor

Azure Monitor samlar in data från en mängd olika källor, inklusive Azures infrastruktur-och plattforms resurser, agenter på Windows-och Linux-datorer och övervaknings data som samlas in i Azure Storage. Alla REST-klienter kan skriva logg data till Azure Monitor med hjälp av ett API och du kan definiera anpassade mått för dina webb program. Vissa mått data kan dirigeras till olika platser, beroende på dess användning. Du kan till exempel använda data för "snabb och möjlig"-avisering, eller för långsiktig trend analys som genomsöks tillsammans med andra loggdata.

#### <a name="monitoring-solutions-and-insights"></a>Övervaknings lösningar och insikter

Övervaknings lösningar använder logg plattformen i Azure Monitor för att tillhandahålla övervakning för ett visst program eller en viss tjänst. De definierar vanligt vis data insamling från agenter eller från Azure-tjänster och innehåller logg frågor och vyer för att analysera dessa data. De ger vanligt vis inga varnings regler, vilket innebär att du måste definiera egna aviserings villkor baserat på insamlade data.

Insikter, till exempel Azure Monitor för behållare och Azure Monitor for VMs, använder du loggar och mått plattform för Azure Monitor för att tillhandahålla en anpassad övervaknings upplevelse för ett program eller en tjänst i Azure Portal. De kan tillhandahålla hälso övervakning och aviserings villkor, förutom anpassad analys av insamlade data.

#### <a name="monitoring-configuration"></a>Övervaknings konfiguration

Azure Monitor separerar data insamling från åtgärder som vidtagits för dessa data, som stöder distribuerade mikrotjänster i en moln miljö. Den sammanställer data från flera källor till en gemensam data plattform och ger analys-, visualiserings-och aviserings funktioner baserat på insamlade data.

Alla data som samlas in av Azure Monitor lagras som antingen loggar eller mått och olika funktioner i övervakaren förlitar sig på antingen. Måtten innehåller numeriska värden i tids serier som lämpar sig väl för aviseringar i nära real tid och snabb identifiering av problem. Loggar innehåller text eller numeriska data och stöds av ett kraftfullt frågespråk som gör dem särskilt användbara för att utföra komplexa analyser.

Eftersom övervakaren separerar data insamling från åtgärder mot dessa data, kanske det inte går att tillhandahålla aviseringar i nära real tid i många fall. För att varna vid loggdata körs frågor på ett återkommande schema som definierats i aviseringen. Med det här beteendet kan Azure Monitor enkelt korrelera data från alla övervakade källor, och du kan analysera data interaktivt på flera olika sätt. Detta är särskilt användbart för att utföra rotor Saks analys och identifiera var felet kan uppstå.

## <a name="health-monitoring"></a>Hälsoövervakning

### <a name="operations-manager"></a>Operations Manager

Hanterings paket i Operations Manager innehåller en tjänst modell som beskriver komponenterna i det program som övervakas och deras relation. Övervakare identifierar det aktuella hälso tillståndet för varje komponent som baseras på data och skript på agenten. Hälso tillstånden samlas in så att du snabbt ser det sammanfattade hälso tillståndet för övervakade datorer och program.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor tillhandahåller inte en användar definierbar metod för att implementera en tjänst modell eller Övervakare som anger det aktuella hälso tillståndet för alla tjänst komponenter. Eftersom övervaknings lösningar baseras på standard funktionerna i Azure Monitor ger de inte övervakning på tillstånds nivå. Följande funktioner i Azure Monitor kan vara till hjälp:

- **Application Insights** skapar en sammansatt karta över ditt webb program och ger ett hälso tillstånd för varje program komponent eller beroende. Detta omfattar aviserings status och detaljerad information till mer detaljerad diagnostik för ditt program.

- **Azure Monitor for VMS** ger en hälso övervakning för virtuella gäst datorer i Azure, på samma sätt som Operations Manager, när du övervakar virtuella Windows-och Linux-datorer. Den utvärderar hälso tillståndet för viktiga operativ Systems komponenter från tillgänglighets-och prestanda perspektivet för att fastställa det aktuella hälso tillståndet. När den fastställer att den virtuella gäst datorn har drabbats av resursutnyttjande, disk utrymmes kapacitet eller ett problem som rör kärn funktioner i operativ systemet, genererar den en avisering för att få det här läget.

- **Azure Monitor for containers** övervakar prestanda och hälsa för Azure Kubernetes Services eller Azure Container instances. Den samlar in minnes-och processor mått från styrenheter, noder och behållare som är tillgängliga i Kubernetes via Metrics-API: et. Den samlar även in behållar loggar och inventerings data om behållare och avbildningar. Fördefinierade hälso kriterier som baseras på de prestanda data som samlas in hjälper dig att identifiera om det finns en resurs Flask hals eller kapacitets problem. Du kan också förstå den övergripande prestandan eller prestandan från en speciell Kubernetes objekt typ (pod, Node, Controller eller container).

## <a name="analyzing-data"></a>Analysera data

### <a name="operations-manager"></a>Operations Manager

Operations Manager innehåller fyra grundläggande sätt att analysera data när de har samlats in.

- Med **Hälsoutforskaren**kan du ta reda på vilka Övervakare som identifierar hälso tillstånds problem och granska kunskap om övervakaren och möjliga orsaker till åtgärder relaterade till den.

- **Vyer** är fördefinierade visualiseringar av insamlade data, till exempel diagram över prestanda data eller en lista över övervakade komponenter och deras aktuella hälso tillstånd. Diagramvyn visar tjänst modellen för ett program visuellt.

- Med **rapporter** kan du sammanfatta historiska data som lagras i Operations Manager data lagret. Du kan anpassa de data som vyer och rapporter baseras på. Det finns dock ingen funktion för att tillåta komplex eller interaktiv analys av insamlade data.

- **Operations Manager Command Shell**, som utökar Windows PowerShell med ytterligare en uppsättning cmdletar, kan fråga efter och visualisera insamlade data. Detta omfattar grafer och andra visualiseringar, internt med PowerShell eller med den Operations Manager HTML-baserade webb konsolen.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor har en kraftfull analys motor som gör det möjligt att interaktivt arbeta med loggdata och kombinera dem med andra övervaknings data för utveckling och annan data analys. Med vyer och instrument paneler kan du visualisera frågedata på olika sätt från Azure Portal och importera till Power BI. Övervaknings lösningar innehåller frågor och vyer för att presentera de data som de samlar in. Insikter som Application Insights, Azure Monitor for VMs och Azure Monitor för behållare innehåller anpassade visualiseringar som stöder interaktiva övervaknings scenarier.

## <a name="alerting"></a>Aviseringar

### <a name="operations-manager"></a>Operations Manager

Operations Manager skapar aviseringar som svar på fördefinierade händelser, när ett prestanda tröskelvärde uppfylls och när hälso tillståndet för en övervakad komponent ändras. Den innehåller fullständig hantering av aviseringar, så att du kan ställa in sin upplösning och tilldela dem till olika operatörer eller system tekniker. Du kan ange meddelande regler som anger vilka aviseringar som ska skicka proaktiva meddelanden.

Hanterings paketen innehåller olika fördefinierade varnings regler för olika kritiska villkor i det program som övervakas. Du kan finjustera reglerna eller skapa anpassade regler för de särskilda kraven i din miljö.

### <a name="azure-monitor"></a>Azure Monitor

Med Azure Monitor kan du skapa aviseringar baserat på ett mått som korsar ett tröskelvärde eller baserat på ett schemalagt frågeresultat. Aviseringar som baseras på mått kan uppnå nästan real tids resultat, medan schemalagda frågor har längre svars tid, beroende på hastigheten på data inhämtning och indexering. I stället för att begränsas till en viss agent kan du logga frågans aviseringar i Azure Monitor så att du kan analysera data över alla data som lagras i flera arbets ytor. Dessa aviseringar omfattar även data från en speciell Application Insights-app med hjälp av en fråga mellan arbets ytor.

Övervaknings lösningar kan innehålla aviserings regler, vanligt vis skapar du dem utifrån dina egna krav.

## <a name="workflows"></a>Arbetsflöden

### <a name="operations-manager"></a>Operations Manager

Hanterings paket i Operations Manager innehålla hundratals enskilda arbets flöden och bestämma både vilka data som ska samlas in och vilka åtgärder som ska utföras med dessa data. En regel kan till exempel sampla en prestanda räknare med några minuters mellanrum och lagra resultatet för analys. En övervakare kan sampla samma prestanda räknare och jämföra dess värde med ett tröskelvärde för att fastställa hälso tillståndet för ett övervakat objekt. En annan regel kan köra ett skript för att samla in och analysera vissa data på en agent dator och utlösa en avisering om det returnerade ett visst värde.

Arbets flöden i Operations Manager är oberoende av varandra, så analys över flera övervakade objekt är svårt. Dessa övervaknings scenarier måste baseras på data när de har samlats in, vilket är möjligt, men kan vara svårt, och är inte vanligt.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor separerar data insamling från åtgärder och analyser som vidtas från dessa data. Agenter och andra data källor skriver loggdata till en Log Analytics arbets yta och Metric-data till mått databasen, utan någon analys av dessa data eller kunskaper om hur de kan användas. Övervakaren utför aviseringar och andra åtgärder från lagrade data, vilket gör att du kan utföra analyser över data från alla källor.

## <a name="extending-base-platform"></a>Utöka bas plattform

### <a name="operations-manager"></a>Operations Manager

Operations Manager implementerar all övervaknings logik i ett hanterings paket, som du antingen skapar själv eller hämtar från oss eller en partner. När du installerar ett hanterings paket identifierar det automatiskt komponenter i programmet eller tjänsten på olika agenter och distribuerar lämpliga regler och övervakare. Hanterings paketet innehåller hälso definitioner, aviserings regler, prestanda-och händelse insamlings regler och vyer för att tillhandahålla fullständig övervakning som stöder infrastruktur tjänsten eller programmet.

Operations Manager SDK gör det möjligt för Operations Manager att integrera med övervaknings plattformar från tredje part eller ITSM-programvara. SDK används också av vissa partner hanterings paket för att ge stöd för övervakning av nätverks enheter och för att leverera anpassade presentations upplevelser som den fyrkantiga HTML5-instrument panelen eller integrering med Microsoft Office Visio.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor samlar in mått och loggar från Azure-resurser, med liten till ingen konfiguration. Övervaknings lösningar Lägg till logik för att övervaka ett program eller en tjänst, men fungerar fortfarande inom standard logg frågor och vyer i övervakaren. Insikter, till exempel Application Insights och Azure Monitor for VMs, använder övervaknings plattformen för data insamling och bearbetning och innehåller även ytterligare verktyg för att visualisera och analysera data. Du kan kombinera data som samlas in med hjälp av insikter med andra data, genom att använda Core Monitor-funktioner som logg frågor och aviseringar.

Övervakaren stöder flera metoder för att samla in övervaknings-eller hanterings data från Azure eller externa resurser. Du kan sedan extrahera och vidarebefordra data från mått-eller logg lager till dina ITSM eller övervaknings verktyg, eller utföra administrativa uppgifter med hjälp av Azure Monitor REST API.

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Övervaka distributions modeller för moln](./cloud-models-monitor-overview.md)
