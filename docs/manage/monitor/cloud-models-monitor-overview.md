---
title: 'Övervaknings guide för molnet: övervaknings strategi för moln distributions modeller'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Välj när Azure Monitor eller System Center Operations Manager ska användas i Microsoft Azure
author: MGoedtel
ms.author: magoedte
ms.date: 10/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 81bb5775f2d83a0784e360440b52112427acf243
ms.sourcegitcommit: 50788e12bb744dd44da14184b3e884f9bddab828
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/18/2019
ms.locfileid: "74160259"
---
# <a name="cloud-monitoring-guide-monitoring-strategy-for-cloud-deployment-models"></a>Övervaknings guide för molnet: övervaknings strategi för moln distributions modeller

Den här artikeln innehåller vår rekommenderade övervaknings strategi för varje moln distributions modell, baserat på följande kriterier:

- Du måste underhålla ditt åtagande att Operations Manager eller en annan företags övervaknings plattform, eftersom den är integrerad med IT-arbetsprocesser, kunskap och expertis, eller att vissa funktioner inte är tillgängliga ännu i Azure Monitor.
- Du måste övervaka arbets belastningar både lokalt och i det offentliga molnet, eller bara i molnet.
- Din strategi för moln migrering innehåller en modern IT-verksamhet och flyttar till våra moln övervaknings tjänster och-lösningar.
- Du kan ha kritiska system som är gapped eller fysiskt isolerade, eller som finns i ett privat moln eller på fysisk maskin vara, och dessa system måste övervakas.

Vår strategi omfattar stöd för övervakning av infrastruktur (beräknings-, lagrings-och Server arbets belastningar), program (slutanvändare, undantag och klient) och nätverks resurser. Det ger ett komplett, service-orienterad övervaknings perspektiv.

## <a name="azure-cloud-monitoring"></a>Azure Cloud Monitoring

Azure Monitor är Azure Native Platform service som tillhandahåller en enda källa för övervakning av Azure-resurser. Den är utformad för moln lösningar som:

- Bygger på Azure.
- Stöd för en affärs kapacitet som baseras på virtuella dator arbets belastningar eller komplexa arkitekturer som använder mikrotjänster och andra plattforms resurser.

Den övervakar alla skikt i stacken och börjar med klient tjänster, till exempel Azure Active Directory Domain Services och händelser på prenumerations nivå och Azure Service Health.

Den övervakar också infrastruktur resurser, till exempel virtuella datorer, lagring och nätverks resurser. Det översta lagret övervakar ditt program.

Genom att övervaka var och en av dessa beroenden och samla in rätt signaler som varje kan generera, får du lämplighet för program och den nyckel infrastruktur du behöver.

Vår rekommenderade metod för att övervaka varje skikt i stacken sammanfattas i följande tabell:

<!-- markdownlint-disable MD033 -->

Layer | Resurs | Omfång | Metod
---|---|---|----
Program | Ett webbaserat program som körs på .NET, .NET Core, Java, Java Script och Node. js-plattformen på en virtuell Azure-dator, Azure App Services, Azure Service Fabric, Azure Functions och Azure Cloud Services. | Övervaka ett Live-webbprogram för att automatiskt identifiera prestanda avvikelser, identifiera kod undantag och problem och samla in användar beteende analys. |  Azure Monitor (Application Insights).
Azure-resurser – plattform som en tjänst (PaaS) | Azure Database Services (till exempel SQL eller MySQL). | Azure Database för SQL prestanda mått. | Aktivera diagnostikloggning för att strömma SQL-data till Azure Monitor loggar.
Azure-resurser – infrastruktur som en tjänst (IaaS) | 1. Azure Storage<br/> 2. Azure Application Gateway<br/> 3. nätverks säkerhets grupper<br/> 4. Azure-Traffic Manager<br/> 5. Azure Virtual Machines<br/> 6. Azure Kubernetes service/Azure Container Instances | 1. kapacitet, tillgänglighet och prestanda.<br/> 2. prestanda-och diagnostikloggar (aktivitet, åtkomst, prestanda och brand vägg).<br/> 3. övervaka händelser när regler tillämpas och regel räknaren för hur många gånger en regel tillämpas på neka eller Tillåt.<br/> 4. övervaka slut punkts status tillgänglighet.<br/> 5. övervaka kapacitet, tillgänglighet och prestanda i ett operativ system för en gäst dator. Mappa program beroenden som finns på varje virtuell dator, inklusive synligheten för aktiva nätverks anslutningar mellan servrar, inkommande och utgående anslutnings fördröjning och portar i alla TCP-anslutna arkitektur.<br/> 6. övervaka kapacitet, tillgänglighet och prestanda för arbets belastningar som körs på behållare och behållar instanser. | 1. lagrings mått för Blob Storage.<br/> 2. Aktivera diagnostikloggning och konfigurera direkt uppspelning till Azure Monitor loggar.<br/> 3. Aktivera diagnostikloggning för nätverks säkerhets grupper och konfigurera direkt uppspelning till Azure Monitor loggar.<br/> 4. Aktivera diagnostikloggning för Traffic Manager slut punkter och konfigurera direkt uppspelning till Azure Monitor loggar.<br/> 5. Aktivera Azure Monitor for VMs.<br/> 6. Aktivera Azure Monitor för behållare.
Nätverk | Kommunikation mellan den virtuella datorn och en eller flera slut punkter (en annan virtuell dator, ett fullständigt kvalificerat domän namn, ett enhetligt resurs-ID eller en IPv4-adress). | Övervaka ändringar av tillgänglighet, svars tid och nätverks sto pol Ogin mellan den virtuella datorn och slut punkten. | Azure-Network Watcher.
Azure-prenumeration | Azure Service Health och grundläggande resurs hälsa. | <li> Administrativa åtgärder som utförs på en tjänst eller resurs.<br/><li> Tjänst hälsan med en Azure-tjänst är i ett försämrat eller otillgängligt tillstånd.<br/><li> Hälso problem har identifierats med en Azure-resurs från Azures tjänst perspektiv.<br/><li> Åtgärder som utförs med Azure autoskalning som indikerar ett fel eller undantag. <br/><li> Åtgärder som utförs med Azure Policy som indikerar att en tillåten eller nekad åtgärd utfördes.<br/><li> Registrera aviseringar som genererats av Azure Security Center. | Levereras i aktivitets loggen för övervakning och avisering med hjälp av Azure Resource Manager.
Azure-klientorganisation | Azure Active Directory || Aktivera diagnostikloggning och konfigurera direkt uppspelning till Azure Monitor loggar.

<!-- markdownlint-enable MD033 -->

## <a name="hybrid-cloud-monitoring"></a>Övervakning av hybrid moln

För många organisationer måste över gången till molnet gradvis närmas, där hybrid moln modellen är det vanligaste första steget i resan. Du väljer noggrant lämplig delmängd av program och infrastruktur för att påbörja migreringen, samtidigt som du undviker avbrott i verksamheten. Men eftersom vi erbjuder två övervaknings plattformar som har stöd för den här moln modellen kan besluts fattare vara osäker på vilket som är det bästa valet för att stödja verksamheten och drifts målen.

I det här avsnittet tar vi itu med osäkerheten genom att granska flera faktorer och erbjuda en förståelse för vilken plattform du bör tänka på.

Tänk på följande viktiga tekniska aspekter:

- Du måste samla in data från Azure-resurser som har stöd för arbets belastningen och vidarebefordra dem till dina befintliga lokala eller hanterade tjänst leverantörs verktyg.

- Du måste underhålla din aktuella investering i System Center Operations Manager och konfigurera den för att övervaka IaaS-och PaaS-resurser som körs i Azure. Alternativt, eftersom du övervakar två miljöer med olika egenskaper, baserat på dina krav, måste du bestämma hur integreringen med Azure Monitor stöder din strategi.

- Som en del av din modernisering-strategi för att standardisera på ett enda verktyg för att minska kostnaderna och komplexiteten måste du genomföra Azure Monitor för att övervaka resurserna i Azure och i företags nätverket.

I följande tabell sammanfattas de krav som Azure Monitor och System Center Operations Manager stöd för att övervaka hybrid moln modellen baserat på en gemensam uppsättning villkor.

<!-- markdownlint-disable MD033 -->

|Krav | Azure Monitor | Operations Manager |
|:--|:---|:---|
|Infrastruktur krav | Nej | Ja<br> Kräver minst en hanterings Server och en SQL-Server som värd för den operativa databasen och informationslager för rapportering databasen. Komplexiteten ökar när hög tillgänglighet och haveri beredskap krävs, och det finns datorer på flera platser, ej betrodda system och andra komplexa design överväganden.|
|Begränsad anslutning-inget Internet<br> eller isolerat nätverk | Nej | Ja |
|Begränsad anslutning – styrd Internet åtkomst | Ja | Ja |
|Begränsad anslutning – ofta frånkopplad | Ja | Ja |
|Konfigurerbar hälso övervakning | Nej | Ja |
| Tillgänglighets test för webb program (isolerat nätverk) | Ja, begränsad<br> Azure Monitor har begränsat stöd i det här avsnittet och kräver anpassade brand Väggs undantag. | Ja |
| Tillgänglighets test för webb program (globalt distribuerat) | Nej | Ja |
|Övervaka VM-arbetsbelastningar | Ja, begränsad<br> Kan samla in IIS-och SQL Server fel loggar, Windows-händelser och prestanda räknare. Kräver att du skapar anpassade frågor, aviseringar och visualiseringar. | Ja<br> Stöder övervakning av de flesta Server arbets belastningar med tillgängliga hanterings paket. Kräver antingen Log Analytics Windows-agent eller Operations Manager agent på den virtuella datorn som rapporterar tillbaka till hanterings gruppen på företags nätverket.|
|Övervaka Azure-IaaS | Ja | Ja<br> Har stöd för övervakning av det mesta av infrastrukturen från företags nätverket. Spårar tillgänglighets tillstånd, mått och aviseringar för virtuella Azure-datorer, SQL och lagring via Azures hanterings paket.|
|Övervaka Azure-PaaS | Ja | Ja, begränsad<br> Baserat på vad som stöds i Azures hanterings paket. |
|Övervakning av Azure-tjänst | Ja<br> | Ja<br> Även om det inte finns någon inbyggd övervakning av Azure Service Health som tillhandahålls idag via ett hanterings paket kan du skapa anpassade arbets flöden för att fråga aviseringar om Azure-tjänstehälsa. Använd Azure-REST API för att få aviseringar via dina befintliga meddelanden.|
|Övervakning av moderna webb program | Ja | Nej |
|Övervakning av äldre webb program | Ja, begränsad, varierar beroende på SDK<br> Har stöd för övervakning av äldre versioner av .NET och Java-webbprogram. | Ja, begränsad |
|Övervaka Azure Kubernetes service-behållare | Ja | Nej |
|Övervaka Docker-eller Windows-behållare | Ja | Nej |
|Övervakning av nätverks prestanda | Ja | Ja, begränsad<br> Stöder tillgänglighets kontroller och samlar in grundläggande statistik från nätverks enheter med hjälp av Simple Network Management Protocol (SNMP) från företags nätverket.|
|Interaktiv data analys | Ja | Nej<br> Förlita dig på SQL Server Reporting Services konserverade eller anpassade rapporter, visualiserings lösningar från tredje part eller en anpassad Power BI implementering. Det finns skalnings-och prestanda begränsningar med Operations Manager data lagret. Integrera med Azure Monitor-loggar som ett alternativ för data agg regerings krav. Du uppnår integrering genom att konfigurera Log Analytics anslutningen.|
|Diagnostik från slut punkt till slut punkt, rotor Saks analys och problemlösnings tid | Ja | Ja, begränsad<br> Har stöd för diagnostik och fel sökning från slut punkt till slut punkt för lokal infrastruktur och program. Använder andra System Center-komponenter eller partner lösningar.|
|Interaktiva visualiseringar (instrument paneler) | Ja | Ja, begränsad<br> Tillhandahåller viktiga instrument paneler med sin HTML5-webb konsol eller en avancerad upplevelse från partner lösningar, till exempel i kvadrat-och Savision. |
|Integrering med IT-eller DevOps-verktyg | Ja | Ja, begränsad |

<!-- markdownlint-enable MD033 -->

### <a name="collect-and-stream-monitoring-data-to-third-party-or-on-premises-tools"></a>Samla in och strömma övervaknings data till tredje part eller lokala verktyg

Om du vill samla in mått och loggar från Azure-infrastrukturen och plattforms resurser måste du aktivera Azure-diagnostik loggar för dessa resurser. Med virtuella Azure-datorer kan du dessutom samla in mått och loggar från gäst operativ systemet genom att aktivera Azure-diagnostik tillägget. Om du vill vidarebefordra diagnostikdata som skickas från dina Azure-resurser till dina lokala verktyg eller hanterade tjänst leverantörer konfigurerar du [Event Hubs](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-logs-stream-event-hubs) att strömma data till dem.

### <a name="monitor-with-system-center-operations-manager"></a>Övervaka med System Center Operations Manager

Även om System Center Operations Manager ursprungligen konstruerades som en lokal lösning för övervakning av program, arbets belastningar och infrastruktur komponenter som körs i din IT-miljö, har den utvecklats för att omfatta moln övervakning trådlösa. Den integreras med Azure, Office 365 och Amazon Web Services (AWS). Den kan övervaka över dessa olika miljöer med hanterings paket som är utformade och uppdaterade för att stödja dem.  

För kunder som har gjort betydande investeringar i Operations Manager för att uppnå omfattande övervakning som är nära integrerad med deras Hantering av IT-tjänster (ITSM) processer och verktyg, eller för kunder som är nya i Azure, är det lättare att fråga följande några

- Kan Operations Manager fortsätta att leverera värde och gör det till affärs idé?
- Har funktionerna i Operations Manager rätt plats för IT-organisationen?
- Ger integrering av Operations Manager med Azure Monitor den kostnads effektiva och heltäckande övervaknings lösning som vi behöver?

Om du redan har investerat i Operations Manager behöver du inte fokusera på att planera en migrering för att ersätta den direkt. Med Azure eller andra moln leverantörer som finns som tillägg till ditt eget lokala nätverk kan Operations Manager övervaka de virtuella gäst datorerna och Azure-resurserna som om de var i företags nätverket. Den här metoden kräver en tillförlitlig nätverks anslutning mellan nätverket och det virtuella Azure-nätverket som har tillräckligt med bandbredd.

Du behöver följande för att övervaka arbets belastningarna som körs i Azure:

- [Hanterings paketet för Azure](https://www.microsoft.com/download/details.aspx?id=50013). Den samlar in prestanda mått som släpps av Azure-tjänster som Web-och Worker-roller, Application Insights tillgänglighets test (webbtest), Azure Service Bus och så vidare. Hanterings paketet använder Azure-REST API för att övervaka tillgänglighet och prestanda för dessa resurser. Vissa typer av Azure-tjänster har inga mått eller fördefinierade övervakare i hanterings paketet, men du kan fortfarande övervaka dem genom relationerna som definierats i Azures hanterings paket för identifierade tjänster.

- [Hanterings paketet för Azure SQL Database](https://www.microsoft.com/download/details.aspx?id=38829) övervaka tillgänglighet och prestanda för Azure SQL-databaser och Azure SQL Database-servrar med hjälp av Azure REST API-och T-SQL-frågor för att SQL Server systemvyer.

- För att övervaka gäst operativ system och arbets belastningar som körs på den virtuella datorn, t. ex. SQL Server, IIS eller Apache Tomcat, måste du hämta och importera det hanterings paket som stöder programmet, tjänsten och operativ systemet.

Kunskap definieras i hanterings paketet, som beskriver hur du övervakar enskilda beroenden och komponenter. Båda hanterings paketen i Azure kräver att du utför en uppsättning konfigurations steg i Azure och Operations Manager innan du kan börja övervaka resurserna.

På program nivå erbjuder Operations Manager grundläggande funktioner för övervakning av program prestanda för vissa äldre versioner av .NET och Java. Om vissa program i din hybrid moln miljö arbetar i ett offline-eller isolerat läge, så att de inte kan kommunicera med en offentlig moln tjänst, kan Operations Manager prestanda övervakning av program prestanda (APM) vara ett användbart alternativ för vissa begränsade scenarier. För program som inte körs på äldre plattformar men som är värdbaserade både lokalt och i alla offentliga moln som tillåter kommunikation via en brand vägg (antingen direkt eller via en proxyserver) till Azure använder du Azure Monitor Application Insights. Den här tjänsten erbjuder djupgående övervakning på kod nivå, med förstklassigt stöd för ASP.NET, ASP.NET Core, Java, Java Script och Node. js.

För alla webb program som kan nås externt bör du aktivera en typ av syntetisk transaktion som kallas [tillgänglighets övervakning]( https://docs.microsoft.com/azure/azure-monitor/app/monitor-web-app-availability). Det är viktigt att veta om ditt program eller en kritisk HTTP/HTTPS-slutpunkt som din app är beroende av är tillgänglig och svarar. Med Application Insights tillgänglighets övervakning kan du köra tester från flera Azure-datacenter och tillhandahålla insikter om hälso tillståndet för ditt program från ett globalt perspektiv.

Även om Operations Manager kan övervaka resurser som finns i Azure, finns det flera fördelar med att ta med Azure Monitor, eftersom dess starka skydd kan lösa begränsningarna i Operations Manager och kan upprätta en stark grund till stöd för eventuell migrering från den. Här går vi igenom var och en av dessa styrkor och svagheter, med vår rekommendation att inkludera Azure Monitor i din strategi för Hybrid övervakning.  

#### <a name="disadvantages-of-using-operations-manager-by-itself"></a>Nack delar med att använda Operations Manager av sig själv

- Analys av övervaknings data i Operations Manager utförs ofta med hjälp av fördefinierade vyer som tillhandahålls av hanterings paket som nås från-konsolen, från SQL Server Reporting Services-rapporter (SSRS) eller från anpassade vyer som slutanvändarna har skapat. Det går inte att utföra ad hoc-dataanalysen. Operations Manager rapportering är inflexibelt. Informations lagret som tillhandahåller långsiktig kvarhållning av övervaknings data skalar inte eller fungerar bra. Och expertis i skriva T-SQL-uttryck, utveckla en Power BI-lösning eller använda lösningar från tredje part krävs för att stödja kraven för de olika personer i IT-organisationen.

- Aviseringar i Operations Manager stöder inte komplexa uttryck eller innehåller korrelations logik. För att minska bruset grupperas aviseringar för att Visa relationerna mellan dem och för att identifiera deras orsaker.

#### <a name="advantages-of-using-operations-manager-with-azure-monitor"></a>Fördelar med att använda Operations Manager med Azure Monitor

- Azure Monitor är ett sätt att komma runt begränsningarna i Operations Manager. Den kompletterar Operations Manager informations lager databasen genom att samla in viktiga prestanda-och loggdata. Azure Monitor ger bättre analyser, prestanda (vid frågor mot stor data volym) och kvarhållning än Operations Manager data lagret.

  Med det Azure Monitor frågespråket kan du skapa mycket mer komplexa och avancerade frågor. Du kan köra frågor i flera terabyte data på några sekunder. Du kan snabbt transformera dina data till cirkel diagram, tids diagram och många andra visualiseringar. För att analysera dessa data är du inte längre begränsade genom att arbeta med Operations Manager rapporter som baseras på SQL Server Reporting Services, anpassade SQL-frågor eller andra lösningar.

- Du kan leverera en förbättrad aviserings upplevelse genom att implementera den Azure Monitor aviserings hanterings lösningen. Aviseringar som genereras i Operations Manager hanterings gruppen kan vidarebefordras till arbets ytan Azure Monitor loggar Analytics. Du kan konfigurera prenumerationen som ansvarar för vidarebefordran av aviseringar från Operations Manager till Azure Monitor loggar som endast vidarebefordrar vissa aviseringar. Du kan till exempel endast vidarebefordra aviseringar som uppfyller dina kriterier för frågor om stöd för problem hantering för trender och undersökning av rotor saken till fel eller problem, genom en enda ruta i glaset. Dessutom kan du korrelera andra loggdata från Application Insights eller andra källor, för att få insikter som hjälper dig att förbättra användar upplevelsen, öka drift tiden och minska tiden för att lösa incidenter.

- Du kan övervaka molnbaserad infrastruktur och program, från en enkel arkitektur eller flera nivåer i Azure, och du kan använda Operations Manager för att övervaka en lokal infrastruktur. Den här övervakningen omfattar en eller flera virtuella datorer, flera virtuella datorer som placerats i en tillgänglighets uppsättning eller en skalnings uppsättning för virtuella datorer, eller ett behållare som distribuerats till Azure Kubernetes service (AKS) som körs på Windows Server-eller Linux-behållare.

- Du kan använda System Center Operations Manager-hälsokontroll-lösningen för att proaktivt utvärdera riskerna och hälsan i din System Center Operations Manager hanterings grupp med jämna mellanrum. Den här lösningen kan ersätta eller komplettera alla anpassade funktioner som du har lagt till i hanterings gruppen.

- Med hjälp av kart funktionen i Azure Monitor for VMs kan du övervaka standard anslutnings mått från nätverks anslutningar mellan dina virtuella datorer i Azure och lokala virtuella datorer. Dessa mått omfattar svars tid, begär Anden per minut, trafik data flöde och länkar. Du kan identifiera misslyckade anslutningar, felsöka, utföra migrering av migrering, utföra säkerhets analyser och kontrol lera tjänstens övergripande arkitektur. Kartan kan automatiskt identifiera program komponenter i Windows-och Linux-system och mappa kommunikationen mellan tjänsterna. Den här automationen hjälper dig att identifiera anslutningar och beroenden som du kände till, planera och validera migrering till Azure och minimera spekulation under incident lösning.

- Med hjälp av Övervakare av nätverksprestanda kan du övervaka nätverks anslutningen mellan:
  - Företagets nätverk och Azure.
  - Verksamhets kritiska program på flera nivåer och mikrotjänster.
  - Användar platser och webbaserade program (HTTP/HTTPS).

Den här strategin ger insyn i nätverks lagret, utan behov av SNMP. Det kan också finnas i en interaktiv topologi, en hopp-och Hopps sto pol Ogin mellan käll-och mål slut punkten. Det är ett bättre alternativ än att försöka utföra samma resultat med nätverks övervakning i Operations Manager eller med andra verktyg för nätverks övervakning som används i din miljö.

### <a name="monitor-with-azure-monitor"></a>Övervaka med Azure Monitor

Även om en migrering till molnet visar flera utmaningar, innehåller den också ett antal affärs möjligheter. Det gör det möjligt för din organisation att migrera från ett eller flera lokala Enterprise Monitoring-verktyg till att inte bara minska kapital utgifter och drifts kostnader, utan även för att dra nytta av fördelarna som en moln övervaknings plattform som Azure Monitor kan leverera i moln skala. Undersök dina övervaknings-och aviserings krav, konfiguration av befintliga övervaknings verktyg och arbets belastningar som övergår till molnet. När du har slutfört din plan konfigurerar du Azure Monitor.

- Övervaka hybrid infrastrukturen och program, från en enkel eller flera nivåer där komponenter finns mellan Azure, andra moln leverantörer och företagets nätverk. Komponenterna kan innehålla en eller flera virtuella datorer, flera virtuella datorer som placerats i en tillgänglighets uppsättning eller en virtuell dators skalnings uppsättning eller ett behållar program som distribueras till Azure Kubernetes service (AKS) som körs på Windows Server-eller Linux-behållare.

- Aktivera Azure Monitor for VMs, Azure Monitor för behållare och Application Insights för att identifiera och diagnostisera problem mellan infrastruktur och program. För en mer omfattande analys och korrelation av data som samlas in från flera komponenter eller beroenden som stöder programmet måste du använda Azure Monitor loggar.

- Skapa smarta aviseringar som gäller för en central uppsättning program och tjänst komponenter, minska aviserings bruset med dynamiska tröskelvärden för komplexa signaler och Använd varnings agg regering baserat på Machine Learning-algoritmer för att snabbt identifiera problemet.

- Definiera ett bibliotek med frågor och instrument paneler för att stödja kraven för de olika personer i IT-organisationen.

- Definiera standarder och metoder för att aktivera övervakning över hybrid-och moln resurser, en övervaknings bas linje för varje resurs, tröskelvärden för aviseringar och så vidare.  

- Konfigurera rollbaserad åtkomst kontroll (RBAC) så att du endast beviljar användare och grupper den mängd åtkomst de behöver för att övervaka data från resurser som de ansvarar för att hantera.

- Inkludera automatisering och självbetjäning för att göra det möjligt för varje team att skapa, aktivera och finjustera deras övervakning och aviserings konfiguration efter behov.

## <a name="private-cloud-monitoring"></a>Övervakning av privata moln

Du kan få en helhets övervakning av Azure Stack med System Center Operations Manager. Mer specifikt kan du övervaka arbets belastningarna som körs i klienten, resurs nivån, på de virtuella datorerna och infrastrukturen som är värd för Azure Stack (fysiska servrar och nätverks växlar).

Du kan också få en helhets övervakning med en kombination av [infrastruktur övervaknings funktioner](https://docs.microsoft.com/azure/azure-stack/azure-stack-monitor-health) som ingår i Azure Stack. Dessa funktioner hjälper dig att Visa hälso tillstånd och aviseringar för en Azure Stack region och [tjänsten Azure Monitor](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-metrics-azure-data) i Azure Stack, som tillhandahåller infrastruktur mått och loggar på bas nivå för de flesta tjänster.

Om du redan har investerat i Operations Manager använder du Azure Stack hanterings paketet för att övervaka tillgängligheten och hälso tillståndet för Azure Stack distributioner, inklusive regioner, resurs leverantörer, uppdateringar, uppdaterings körningar, skalnings enheter, enhets noder, infrastruktur roller och deras instanser (logiska entiteter som består av maskin varu resurserna). Det här hanterings paketet använder REST-API: er för hälso-och uppdaterings resurs leverantörer för att kommunicera med Azure Stack. Om du vill övervaka fysiska servrar och lagrings enheter använder du OEM-leverantörens hanterings paket (till exempel, som tillhandahålls av Lenovo, Hewlett Packard eller Dell). Operations Manager kan internt övervaka nätverks växlarna för att samla in grundläggande statistik med hjälp av SNMP. Det går att övervaka klient arbets belastningarna med Azures hanterings paket genom att följa två grundläggande steg. Konfigurera den prenumeration som du vill övervaka och Lägg sedan till övervakarna för den prenumerationen.

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Samla in rätt data](./data-collection.md)
