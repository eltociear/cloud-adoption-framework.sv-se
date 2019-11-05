---
title: 'Utveckling av moln: demokratisera identifieringen av data'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introduktion till Cloud innovation – demokratisera identifieringen av data
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: f854b103decc3b23f27a41d01a81b812d2bc3c3f
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565706"
---
# <a name="democratize-data"></a>Demokratisera data

Kol, olja och mänsklig potential var de tre sekventiella till gångarna under industrins revolution. Dessa till gångar skapade företag, skiftade marknader och slutligen ändrade länder. I den digitala ekonomin finns det tre lika viktiga till gångar: data, enheter och mänsklig potential. Var och en av dessa till gångar innehåller fantastiska möjligheter till innovation. För all innovation ansträngning i modern ansträngning är data den nya oljan.

I alla företag idag finns det data fickor som kan utnyttjas för att hitta och möta kund behovet mer effektivt. Processen för att vinna data för att öka innovationen har tyvärr länge varit kostsam och tids krävande. Många av de mest värdefulla lösningarna till kund behov är ouppfyllda eftersom rätt personer inte kan komma åt de data de behöver.

Democratization av data är en process för att hämta data till rätt hand för att öka innovationen. Den här processen kan ta flera formulär, men de omfattar vanligt vis lösningar för inmatade eller integrerade rå data, centralisering av data, delning av data och data skydd. När dessa metoder lyckas kan experter runt företaget använda data för att testa Hypotheses. I många fall kan moln antagande team [bygga med kund empati](./build.md) med enbart data och snabbt adressera befintliga kund behov.

## <a name="process-of-democratizing-data"></a>Process för democratizing-data

I följande faser beskrivs de beslut och tillvägagångs sätt som krävs för att införa en lösning som demokratiserar sakernas data. Alla faser behöver inte vara nödvändiga för att bygga en speciell lösning. Du bör dock utvärdera varje fas när du bygger en lösning på en kund hypotes. Var och en är en unik metod för att skapa innovativa lösningar.

![Process för democratizing-data](../../_images/innovate/democratize-data.png)

### <a name="share-data"></a>Dela data

När du [skapar med kund empati](./build.md)höjer alla processer kund behovet via en teknisk lösning. Eftersom democratizing-data inte är ett undantag börjar vi med att dela data. För att demokratisera identifieringen av data måste den innehålla en lösning som delar data med en data konsument. Data konsumenten kan vara en direkt kund eller en proxy som fattar beslut för kunder. Godkända data konsumenter kan analysera, undersöka och rapportera om centraliserade data, utan support från IT-personal.

Många lyckade innovationer har lanserats som minsta livskraftiga produkter (MVP) som levererar manuella, data drivna processer för kundens räkning. I den här Concierge-modellen är en medarbetare data konsumenten. Den anställda använder data för att hjälpa kunden. Varje gången kunden engagerar sig manuellt, kan en hypotes testas och verifieras. Den här metoden är ofta ett kostnads effektivt sätt att testa en kund fokuserad hypotes innan du investerar kraftigt i integrerade lösningar.

De primära verktygen för att dela data direkt med data konsumenter är självbetjänings rapportering eller data som är inbäddade i andra upplevelser, med hjälp av verktyg som [Power BI](https://docs.microsoft.com/power-bi).

> [!NOTE]
> Se till att du har läst följande avsnitt innan du delar data. Att dela data kan kräva styrning för att ge skydd för delade data. Dessa data kan också spridas över flera moln och kan kräva centralisering. Mycket data kan till och med finnas i program som kräver data insamling innan du kan dela den.

### <a name="govern-data"></a>Styr data

Genom att dela data kan du snabbt skapa en MVP som du kan använda i kund samtal. Men för att kunna aktivera delade data i användbar och användbar kunskap, krävs en bit som är mer allmänt nödvändig. När en hypotes har verifierats genom data delning är nästa fas i utvecklingen vanligt vis data styrning.

Data styrning är ett brett ämne som kan kräva att det är ett eget dedikerat ramverk. Den graden av granularitet ligger utanför omfattningen av [moln införande ramverket](../../index.md). Det finns dock flera aspekter av data styrning som du bör ta hänsyn till när kund hypotesen verifieras. Exempel:

- **Är de delade data känsliga?** [Data bör klassificeras](../../govern/policy-compliance/data-classification.md) före all offentlig delning för att skydda kundernas och företagets intresse.
- **Om data är känsliga, har de skyddats?** Skydd av känsliga data bör vara ett krav för alla democratized-data. Exempel arbets belastningen som fokuserar på att [skydda data lösningar](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/securing-data-solutions) är några referenser för att skydda data.
- **Är data katalogiserade?** Att samla in information om de data som delas kommer att hjälpa till med långsiktig data hantering. Verktyg för att dokumentera data, som Azure Data Catalog, kan göra den här processen mycket enklare i molnet. Vägledning om [anteckningen av data](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-annotate) och [dokumentation av data källor](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-documentation) kan påskynda processen.

När democratization av data är viktigt för en kundfokuserad hypotes, se till att styrningen av delade data ligger någonstans i publicerings planen. Detta hjälper till att skydda kunder, data konsumenter och företaget.

### <a name="centralize-data"></a>Centralisera data

När data störs i en IT-miljö kan möjligheter till innovation vara mycket begränsat, dyrt och tids krävande. Molnet ger nya möjligheter att centralisera data över datasilor. När centralisering av flera data källor krävs för att [bygga med kund empati](./build.md)kan molnet påskynda testningen av Hypotheses.

> [!CAUTION]
> Centralisering av data representerar en risk punkt i innovations processen. När data centralisering är en [teknisk insamling](./build.md#reduce-complexity-and-delay-technical-spikes) (i stället för en källa till kund värde) rekommenderar vi att du fördröjer centralisering tills Kundens Hypotheses har verifierats.

Om centralisering av data krävs bör du först definiera lämpligt data lager för de centraliserade data. Det är en bra idé att upprätta ett informations lager i molnet. Detta skalbara alternativ är en central plats för alla dina data. Den här typen av lösning är tillgänglig i OLAP-eller Big data-alternativ (Online Analytical Processing).

Referens arkitekturerna för [OLAP-](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-analytical-processing) och [Big data](https://docs.microsoft.com/azure/architecture/data-guide/big-data) -lösningar kan hjälpa dig att välja den mest relevanta lösningen i Azure. Om en hybrid lösning krävs kan referens arkitekturen för att [utöka lokala data](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/hybrid-on-premises-and-cloud) också hjälpa till att påskynda lösnings utvecklingen.

> [!IMPORTANT]
> Beroende på kundens behov och den justerade lösningen kan en enklare metod vara tillräckligt. Moln arkitekten bör utmana teamet för att överväga lägre kostnads lösningar som kan leda till en snabbare verifiering av kund hypotesen, särskilt under en tidig utveckling. I följande avsnitt om insamling av data beskrivs några scenarier som kan föreslå en annan lösning för din situation.

### <a name="collect-data"></a>Samla in data

När du behöver data som ska centraliseras för att tillgodose ett kund behov, är det mycket troligt att du också måste samla in data från olika källor och flytta dem till det centraliserade data lagret. Det finns två primära former för data insamling: *integrering* och *inmatning*.

**Integrering:** Data som finns i ett befintligt data lager kan integreras i det centraliserade data lagret med hjälp av traditionella metoder för data förflyttning. Detta är särskilt vanligt för scenarier som involverar data lagring i molnet. Dessa tekniker innebär att extrahera data från det befintliga data lagret och sedan läsa in dem i det centrala data lagret. Vid någon tidpunkt i den här processen omvandlas data vanligt vis till att vara mer användbara och relevanta i den centrala butiken.

Molnbaserade verktyg har inaktiverat dessa tekniker i verktyg för att betala per användning, vilket minskar barriären för inmatning av data insamling och centralisering. Verktyg som data migration service och Data Factory är två exempel i Azure. Referens arkitekturen för [Data Factory med ett OLAP-datalager](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/etl) är ett exempel på en sådan lösning.

Inmatning **:** Vissa data finns inte i ett befintligt data lager. När dessa tillfälliga data är en primär källa till innovation bör du överväga andra metoder. Tillfälliga data finns i en mängd olika befintliga källor, t. ex. program, API: er, data strömmar, IoT-enheter, en blockchain, ett programcache, i medie innehåll eller till och med i flata filer.

Du kan integrera dessa olika typer av data i ett centralt data lager på en OLAP-eller Big data-lösning. För tidiga iterationer av processen build – plan – lära kan en OLTP-lösning (online transaktionell bearbetning) dock vara mer än tillräckliga för att verifiera en kund hypotes. OLTP-lösningar är inte den bästa kvalitets lösningen för eventuella rapporterings scenarier. Men när du [skapar med kund empati](./build.md)är det mer viktigt att fokusera på kundernas behov än på tekniska verktyg. När kunden hypotesen har validerats i skala kan en mer lämplig plattform behövas. Referens arkitekturen på [OLTP-data lager](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-transaction-processing) kan hjälpa dig att avgöra vilket data lager som passar bäst för din lösning.

**Virtualisering:** Integrering och inmatning av data kan ibland sakta innovationer. När en lösning för datavirtualizering redan är tillgänglig, kan det innebära en mer rimlig metod. Inmatning och integrering kan både medföra dubbla lagrings-och utvecklings krav, lägga till data svars tid, öka attack ytan, utlösa kvalitets problem och förbättra styrnings arbetet. Datavirtualizering är ett mer modernt alternativ som lämnar ursprungliga data på en enda plats och skapar direkt-eller cachelagrade frågor för källdata.

SQL Server 2017 och Azure SQL Data Warehouse både support [PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) , som är den metod för datavirtualisering som oftast används i Azure.

## <a name="next-steps"></a>Nästa steg

Med en strategi för democratizing-data på plats, ska du gå vidare till utvärdera metoder för att [engagera kunder genom appar](./apps.md).

> [!div class="nextstepaction"]
> [Engagera kunder via appar](./apps.md)
