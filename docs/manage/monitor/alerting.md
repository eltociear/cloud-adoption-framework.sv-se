---
title: Guide för moln övervakning – avisering
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Välj när Azure Monitor eller System Center Operations Manager ska användas i Microsoft Azure
author: MGoedtel
ms.author: magoedte
ms.date: 06/26/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 0157cf5c50cd676478b28889b565c7f3f6952e32
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548601"
---
# <a name="cloud-monitoring-guide-alerting"></a>Övervaknings guide för molnet: avisering

För år har IT-organisationerna fått problem med att bekämpa en aviserings utmattning som skapats av de övervaknings verktyg som distribueras i företaget. Många system genererar en stor mängd aviseringar ofta som meningslösa, medan andra är relevanta, men antingen förbises eller ignoreras. Det innebär att IT-och utvecklarnas åtgärder har fått problem att uppfylla den utlovade kvaliteten på service nivån för interna eller externa kunder. Det är viktigt att förstå statusen för din infrastruktur och dina program för att säkerställa tillförlitligheten. Du behöver snabbt identifiera orsaker, minimera tjänstens försämring och avbrott, eller minska risken för eller minska antalet incidenter.

## <a name="successful-alerting-strategy"></a>Aviserings strategin har slutförts

*Du kan inte åtgärda det du inte vet är brutet.*

Avisering om vad som är viktigt för dig. Den är underfixerad genom att samla in och mäta rätt mått och loggar. Du behöver också ett övervaknings verktyg som kan lagra, aggregera, visualisera, analysera och initiera ett automatiserat svar när villkoren är uppfyllda. Att förbättra bevarandet av dina tjänster och program kan bara utföras om du är helt medveten om dess sammansättning. Du kan mappa sammansättningen till en detaljerad övervaknings konfiguration som ska användas av övervaknings plattformen. Detta inkluderar tillstånden för förutsägbara fel (symptomen är inte orsaken till felet) som är meningsfull för aviseringen.

Tänk på följande principer för att avgöra om ett symtom är en lämplig kandidat för aviseringar:

- **Spelar det någon roll?** Är problemet symptomatic av ett reellt problem eller problem som påverkar programmets övergripande hälso tillstånd? Är du till exempel försiktig om processor användningen är hög på resursen? Eller att en viss SQL-fråga som körs på en SQL Database-instans på den resursen förbrukar hög processor användning under en varaktig period? Eftersom processor användnings villkoret är ett verkligt problem bör du varna det. Men du behöver inte meddela teamet, eftersom det inte hjälper dig att peka på vad som orsakar tillståndet på den första platsen. Aviseringar och meddelanden om användnings problemet för SQL-frågekörning är både relevanta och åtgärds bara.
- **Är det brådskande?** Är problemet verkligt och behöver det ha brådskande uppmärksamhet? I så fall bör teamet som ansvarar omedelbart meddelas.
- **Påverkas dina kunder?** Påverkas användare av tjänsten eller programmet på grund av problemet?
- **Påverkas andra beroende system?** Finns det varningar från beroenden som är relaterade till varandra, och som kan korreleras för att undvika att meddela olika lag att de fungerar på samma problem?

Ställ frågor när du börjar utveckla en övervaknings konfiguration. Testa och validera antaganden i en miljö som inte är produktion och distribuera sedan till produktion. Övervakning av konfigurationer härleds från kända fellägen, test resultatet av simulerade haverier och erfarenhet från olika medlemmar i teamet.

När du har lanserat övervaknings konfigurationen kan du lära dig mer om vad som fungerar och vad som inte är det. Överväg hög varnings volym, problem som inte kan åtgärdas genom övervakning, men som har observerats av slutanvändarna, och vilka var de bästa åtgärderna som skulle vidtas som en del av den här utvärderingen. Identifiera ändringar som implementeras för att förbättra tjänst leveransen som en del av en pågående, kontinuerlig övervaknings förbättrings process. Det är inte bara att utvärdera aviserings bruset eller uteblivna aviseringar, men också effektiviteten för hur du övervakar arbets belastningen. Det rör sig om effektiviteten hos aviserings principerna, processen och den övergripande kulturen för att avgöra om du har förbättrats.

Både System Center Operations Manager och Azure Monitor stöd för aviseringar baserat på statiska eller jämna dynamiska tröskelvärden och åtgärder som ställts in ovanpå dem. Exempel är aviseringar för e-post, SMS och röst samtal för enkla meddelanden. Båda dessa tjänster har även stöd för ITSM-integrering, för att automatisera skapandet av incident poster och eskalera till rätt support team, eller andra aviserings hanterings system som använder en webhook.

När det är möjligt kan du använda någon av flera tjänster för att automatisera återställnings åtgärder. Detta omfattar System Center Orchestrator, Azure Automation, Azure Logic Apps eller automatisk skalning när det gäller elastiska arbets belastningar. När du meddelar ansvariga team är den vanligaste åtgärden för aviseringar, och det kan också vara lämpligt att automatisera korrigerande åtgärder. Detta kan hjälpa dig att effektivisera hela incident hanterings processen. Att automatisera dessa återställnings uppgifter kan också minska risken för mänskligt fel.

## <a name="azure-monitor-alerting"></a>Azure Monitor avisering

Om du använder Azure Monitor exklusivt gäller följande rikt linjer. Följ dessa rikt linjer när du överväger hastighet, kostnad och lagrings volym i Azure Monitor.

Det finns sex databaser som lagrar övervaknings data, beroende på vilken funktion och konfiguration du använder.

- **Azure Monitor mått databas.** En databas för tids serier används främst för Azure Monitor plattforms mått, men har även Application Insights Mät data som speglas i den. Information som anger den här databasen har snabbast aviserings tider.

- **Application Insights loggar lager.** En databas som lagrar de flesta Application Insights telemetri i logg formuläret.

- **Azure Monitor loggar lager.** Det primära arkivet för Azure-loggdata. Andra verktyg kan dirigera data till den och kan analyseras i Azure Monitor loggar. Logg aviserings frågor har högre latens på grund av inmatning och indexering. Den här fördröjningen är vanligt vis 5-10 minuter, men kan vara högre under vissa omständigheter.

- **Aktivitets logg lager.** Används för alla aktivitets logg-och tjänst hälso händelser. Dedikerad avisering är möjlig. Innehåller händelser på prenumerations nivå som inträffar för objekt i din prenumeration, som du ser från utsidan av dessa objekt. Till exempel när en princip har angetts eller om en resurs används eller tas bort.

- **Azure Storage.** General-Purpose Storage som stöds av Azure-diagnostik och andra övervaknings verktyg. Det är ett billigt alternativ för långsiktig kvarhållning av övervakning av telemetri. Aviseringar stöds inte från data som lagras i den här tjänsten.

- **Event Hubs.** Används vanligt vis för att strömma data till lokala eller andra partner övervaknings-/ITSM-verktyg.

Det finns fyra typer av aviseringar i Azure Monitor, som är något knutna till lagrings platsen som data lagras i.

- [Mått-varning](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric). Aviseringar om data i Azure Monitor Metrics-databasen. Aviseringar inträffar när ett övervakat värde korsar en användardefinierad tröskel och sedan igen när det återgår till "normal" tillstånd.

- [Avisering om logg fråga](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log-query). Tillgängligt för aviseringar om innehåll i Application Insights eller Azure-loggfiler. Kan även aviseringar baserat på frågor över arbets ytor.

- [Aktivitets logg avisering](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log). Aviseringar om objekt i aktivitets logg arkivet, med undantag för Service Health data.

- [Service Health avisering](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log-service-notifications?toc=%2fazure%2fservice-health%2ftoc.json). En särskild typ av avisering, bara för Service Health problem som kommer från aktivitets logg arkivet.

### <a name="alerting-through-partner-tools"></a>Avisering via partner verktyg

Om du använder en extern aviserings lösning kan du skicka så mycket som du kan via Azure Event Hubs, eftersom det är den snabbaste sökvägen från Azure Monitor. Du måste betala för inmatning till Event Hub. Om kostnad är ett problem och hastigheten inte är det kan du använda Azure Storage som ett billigare alternativ. Se bara till att dina övervaknings-eller ITSM-verktyg kan läsa Azure Storage för att extrahera data.

Azure Monitor innehåller stöd för integrering med andra övervaknings plattformar och ITSM program vara som ServiceNow. Du kan använda Azure-aviseringar och fortfarande utlösa åtgärder utanför Azure, enligt vad som krävs av din incident hantering eller DevOps process. Om du vill varna i Azure Monitor och automatisera svaret kan du initiera automatiserade åtgärder med hjälp av Azure Functions, Azure Logic Apps eller Azure Automation, baserat på ditt scenario och dina krav.

### <a name="specialized-azure-monitoring-offerings"></a>Specialiserade Azure Monitoring-erbjudanden

[Hanterings lösningar](https://docs.microsoft.com/azure/azure-monitor/insights/solutions-inventory) lagrar vanligt vis sina data i Azure logs-butiken. De två undantagen är Azure Monitor for VMs och Azure Monitor för behållare. I följande tabell beskrivs aviserings upplevelsen baserat på den specifika data typen och var den lagras.

Lösning| Datatyp | Aviserings beteende
:---|:---|:---
Azure Monitor för containrar | Beräknade genomsnitts prestanda data från noder och poddar skrivs till mått lagret. | Skapa mått aviseringar om du vill bli aviserad utifrån variationen av uppmätta användnings prestanda, sammanställt över tid.
|| Beräknade prestanda data som använder percentiler från noder, styrenheter, behållare och poddar skrivs till logg lagret. Behållar loggar och inventerings information skrivs också till logg lagret. | Skapa logg fråga aviseringar om du vill få en avisering utifrån variationen av uppmätt användning från kluster och behållare. Aviseringar för logg frågor kan också konfigureras baserat på antal Pod-faser och antal status noder.
Azure Monitor för virtuella datorer | Hälso kriterier är mått som skrivs till mått lagret. | Aviseringar genereras när hälso tillståndet ändras från felfritt till ohälsosamt tillstånd. Stöder endast åtgärds grupper som kon figurer ATS för att skicka SMS eller e-postmeddelanden.
|| Kart-och gäst operativ systemets prestanda logg data skrivs till logg lagret. | Skapa aviseringar för logg frågor.

### <a name="fastest-speed-driven-by-cost"></a>Snabbast hastighet driven genom kostnad

Svars tiden är ett av de mest kritiska besluten som påverkar aviseringen och snabb lösning av problem som påverkar din tjänst. Om du behöver aviseringar i nära real tid under fem minuter ska du först utvärdera om du har eller kan få aviseringar på din telemetri där den lagras som standard. I allmänhet är den här strategin också alternativet billigaste, eftersom verktyget som du använder redan skickar data till den platsen.

Det här är några viktiga fotnoter till den här regeln.

**Gäst operativ systemets telemetri** har ett antal sökvägar för att komma in i systemet.

- Det snabbaste sättet att varna för dessa data är att importera det som anpassade mått. Gör detta med hjälp av Azure-diagnostik-tillägget och Använd sedan en måtta-avisering. Anpassade mått är dock för närvarande en för hands version och är [dyrare än andra alternativ](https://azure.microsoft.com/pricing/details/monitor).

- Metoden billigaste men långsammast är att skicka den till Azure-loggfilerna Kusto Store. Att köra Log Analytics-agenten på den virtuella datorn är det bästa sättet att hämta alla gäst operativ system mått och logga data i det här arkivet.

- Du kan skicka till båda butikerna genom att köra både tillägget och agenten på samma virtuella dator. Sedan kan du snabbt varna dig, men även använda gäst operativ systemets data som en del av mer komplexa sökningar i kombination med annan telemetri.

**Importera data från lokala platser.** Om du försöker fråga och övervaka på datorer som körs i Azure och lokalt kan du använda Log Analytics-agenten för att samla in gäst operativ system data. Sedan kan du använda en funktion som kallas [loggar till mått](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric-logs) för att effektivisera dessa mått till mått lagret. Den här metoden åsidosätter delar av inmatnings processen i Azure logs-butiken och är därmed tillgänglig tidigare i mått databasen.

### <a name="minimize-alerts"></a>Minimera aviseringar

Om du använder en lösning som Azure Monitor for VMs och hittar standard hälso kriterier som övervakar att prestanda användningen godkänns, ska du inte skapa överlappande mått eller logg fråga aviseringar baserat på samma prestanda räknare.

Om du inte använder Azure Monitor for VMs kan du utforska följande funktioner för att göra jobbet att skapa aviseringar och hantera meddelanden enklare:

> [!NOTE]
> Dessa funktioner gäller endast för mått aviseringar. det vill säga aviseringar som baseras på data som skickas till Azure Monitor Metric-databasen. De gäller inte för andra typer av aviseringar. Som tidigare nämnts är det primära målet för mått aviseringar hastigheten. Om du får en avisering på mindre än 5 minuter inte är primärt, kan du använda en logg fråga i stället.

- [Dynamiska tröskelvärden](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-dynamic-thresholds). Dynamiska tröskelvärden tittar på resursens aktivitet under en tids period och skapar det övre och nedre tröskelvärdet för "normala beteende". När det mått som övervakas faller utanför dessa tröskelvärden får du en avisering.

- [Multisign-aviseringar](https://azure.microsoft.com/blog/monitor-at-scale-in-azure-monitor-with-multi-resource-metric-alerts). Du kan skapa en mått avisering som använder kombinationen av två olika indata från två olika resurs typer. Om du till exempel vill utlösa en avisering när CPU: n för en virtuell dator är över 90 procent och antalet meddelanden i en viss Azure Service Bus Queue som den virtuella datorn överskrider en viss mängd, kan du göra det utan att skapa en logg fråga. Detta fungerar bara för två signaler. Om du har en mer komplex fråga matar du in dina mått data i Azure Monitor logg lager och använder en logg fråga.

- [Aviseringar via multiresurs](https://azure.microsoft.com/blog/monitor-at-scale-in-azure-monitor-with-multi-resource-metric-alerts). Azure Monitor tillåter en enda måtta varnings regel som gäller för alla VM-resurser. Med den här funktionen kan du spara tid eftersom du inte behöver skapa enskilda aviseringar för varje virtuell dator. Prissättningen för den här typen av avisering är samma. Om du har skapat 50 aviseringar för övervakning av CPU-användning för 50-datorer eller 1 avisering som övervakar CPU-användningen för alla virtuella datorer i 50, kostar det samma belopp. Du kan även använda dessa typer av aviseringar i kombination med dynamiska tröskelvärden.

De här funktionerna används tillsammans och sparar tid genom att minimera aviserings aviseringar och hantering av underliggande aviseringar.

### <a name="alerts-limitations"></a>Aviserings begränsningar

Se till att du noterar [begränsningarna](https://docs.microsoft.com/azure/azure-subscription-service-limits#azure-monitor-limits) för hur många aviseringar som kan skapas. Vissa begränsningar (men inte alla) kan ökas genom att supporten anropas.

### <a name="best-query-experience"></a>Bästa fråge upplevelse

Om du letar efter trender i alla dina data är det klokt att importera alla dina data till Azure-loggar, om de inte redan finns i Application Insights. Du kan skapa frågor i båda arbets ytorna så att du inte behöver flytta data mellan dem. Du kan också importera aktivitets loggen och Service Health data till Log Analytics-arbetsytan. Du betalar för denna inmatning och lagring, men du får alla dina data på en plats för analys och frågor. Det ger dig också möjlighet att skapa komplexa frågevillkor och aviseringar.
