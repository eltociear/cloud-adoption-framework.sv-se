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
ms.openlocfilehash: c0ef1165fc416814e0563ec29c4ad5901a83b032
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683278"
---
# <a name="democratize-data"></a>Demokratisera identifieringen av-data

Kol, olja och mänsklig potential var de tre sekventiella till gångarna i hela den industriella revolutionen. Dessa till gångar skapade företag, skiftade marknader och slutligen ändrade länder. I den digitala ekonomin finns det tre lika viktiga till gångar: data, enheter och mänsklig potential. I var och en av dessa till gångar är det en bra innovation. I alla Innovations insatser är data den nya oljan.

I alla företag idag finns det data fickor som kan utnyttjas för att hitta och möta kund behovet snabbare. Processen för att vinna data för att öka innovationen har tyvärr länge varit kostsam och tids krävande. Många av de mest värdefulla lösningarna till kund behov är ouppfyllda eftersom rätt personer inte kan komma åt de data de behöver.

Democratization av data är en process för att hämta data till rätt hand för att öka innovationen. Den här processen kan ta flera former, men innehåller vanligt vis lösningar för inmatade eller integrerade rå data, centralisering av data, delning av data och data skydd. När det är klart kan experter runt företaget utnyttja data för att testa Hypotheses. I många fall kan moln antagande team [bygga med kund empati](./build.md) med enbart data, vilket resulterar i snabb påverkan på befintliga kund behov.

## <a name="process-of-democratizing-data"></a>Process för democratizing-data

I följande faser får du vägledning för de beslut och tillvägagångs sätt som krävs för att införa en lösning som demokratiserar sakernas data. Var och en av faserna kanske inte krävs för att bygga en speciell lösning. Var och en bör dock utvärderas när du bygger en lösning på en kund hypotes. Var och en är en unik metod för att skapa innovativa lösningar.

![Process för democratizing-data](../../_images/innovate/democratize-data.png)

### <a name="share-data"></a>Dela data

När du [bygger med kund empati](./build.md), fokuserar alla processer på ett kund behov över en teknisk lösning. Democratizing-data är inget undantag, så vi börjar med att dela data. För att demokratisera identifieringen av data måste den innehålla en lösning som delar data med en data konsument. Konsumenten av data kan vara en direkt kund eller en proxy som fattar beslut för kunder. Godkända data konsumenter kan analysera, gå över och rapportera om centraliserade data, utan support från IT-personal.

Många lyckade innovationer har lanserats som MVP: er som levererar manuella, data drivna processer för kundens räkning. I den här Concierge-modellen är en medarbetare data konsumenten. Den anställda använder data för att hjälpa kunden. Varje gången kunden engagerar det manuella stödet kan en hypotes testas och verifieras. Den här metoden är ofta ett kostnads effektivt sätt att testa en kundfokuserad hypotes innan man investerar mycket integrerade lösningar.

De primära verktygen för att dela data direkt med data konsumenter, inkluderar självbetjänings rapportering eller inbäddade data i andra upplevelser med hjälp av verktyg som [Power BI](https://docs.microsoft.com/power-bi).

> [!NOTE]
> Innan du delar data är det viktigt att vara medveten om följande avsnitt. Att dela data kan kräva styrning för att ge skydd för delade data. Ytterligare data kan spridas över flera moln och kan kräva centralisering. Mycket data kan till och med finnas i program som kräver insamling av data innan de delas.

### <a name="govern-data"></a>Styr data

Att dela data kan snabbt producera en MVP som kan användas i kund konversationer. Data är dock enbart data. För att göra det nödvändigt att dela data i en användbar kunskap är det ofta nödvändigt att göra lite mer. När en hypotes har verifierats genom data delning är nästa fas i utvecklingen ofta data styrning.

Data styrning är ett brett ämne som kan kräva att det är ett eget dedikerat ramverk. Detta ligger utanför omfånget för [moln införande ramverket](../../index.md). Det finns dock några aspekter av data styrning som bör beaktas, så snart som kund hypotesen verifieras. Här följer några exempel på dessa frågor:

- **Är de delade data känsliga?** [Data bör klassificeras](../../govern/policy-compliance/data-classification.md) före all offentlig delning för att skydda kundernas och företagets intresse.
- **Om data är känsliga, har de skyddats?** Skydd av känsliga data bör vara ett krav för alla democratized-data. Exempel arbets belastningen som fokuserar på att [skydda data lösningar](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/securing-data-solutions.md) är några referenser för att skydda data.
- **Är Data Catalog?** Att samla in information om de data som delas kommer att hjälpa till med långsiktig data hantering. Verktyg för att dokumentera data, som Azure Data Catalog, kan göra den här processen mycket enklare i molnet. Vägledning om [anteckningen av data](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-annotate) och [dokumentation av data källor](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-documentation) kan påskynda processen.

När democratization av data är viktigt för en kundfokuserad hypotes, bör styrning av delade data ligga någonstans i versions planen för att skydda kunder, data konsumenter och företaget.

### <a name="centralize-data"></a>Centralisera data

När data störs i en IT-miljö kan möjligheter till förnyad IT vara mycket begränsat, kostsamma och tids krävande. Molnet ger nya möjligheter att centralisera data över olika data silor. När centralisering av flera data källor krävs för att [bygga med kund empati](./build.md) kan molnet påskynda testningen av Hypotheses.

> [!CAUTION]
> Centralisering av data är en gemensam risk punkt i innovations processen. När data centralisering är en [teknisk insamling](./build.md#reduce-complexity-and-delay-technical-spikes), i stället för en källa till kund värde, rekommenderar vi att du fördröjer centralisering tills kunden hypotesen har verifierats.

Om centralisering av data krävs är det första steget att definiera lämpligt data lager för de centraliserade data. Den här metoden är att upprätta ett informations lager i molnet. Detta skalbara alternativ kommer att tillhandahålla en central plats för alla data. Den här typen av lösning är tillgänglig i OLAP-eller Big data-alternativ (Online Analytical Processing).

Referens arkitekturerna för [OLAP-](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-analytical-processing) och [Big data](https://docs.microsoft.com/azure/architecture/data-guide/big-data) -lösningar kan hjälpa dig att välja den mest relevanta lösningen i Azure. Om en hybrid lösning krävs kan referens arkitekturen för att [utöka lokala data](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/hybrid-on-premises-and-cloud) också hjälpa till att påskynda lösnings utvecklingen.

> [!IMPORTANT]
> Beroende på kundens behov och den justerade lösningen kan en enklare lösning vara tillräckligt. Moln arkitekten bör utmana teamet för att överväga lägre kostnads lösningar som kan leda till en snabbare verifiering av kund hypotesen, särskilt under en tidig utveckling. I avsnittet om att samla in data nedan visas några scenarier som kan tillkomma för en annan lösning.

### <a name="collect-data"></a>Samla in data

När data behöver centraliseras för att leverera ett kund behov är det mycket troligt att data måste samlas in från olika källor och flyttas till det centraliserade data lagret. Det finns två primära former för data insamling: integrering och inmatning. Var och en har olika sätt att samla in data.

**Integrera:** Befintliga data som finns i ett befintligt data lager kan integreras i det centraliserade data lagret med hjälp av traditionella metoder för data förflyttning. Detta är särskilt vanligt för scenarier som involverar data lagring i molnet. Dessa tekniker består av att extrahera data från det befintliga data lagret. Sedan läser du in data i det centrala data lagret. Vid någon tidpunkt i den här processen omvandlas data ofta för att vara mer användbara och relevanta i den centrala butiken.

Molnbaserade verktyg har omvandla dessa tekniker till verktyg för att betala per användning, vilket minskar barriären för inmatning av data insamling och centralisering. Verktyg som data migration service och Data Factory är två vanliga exempel i Azure. Referens arkitekturen för [Data Factory med ett OLAP-datalager](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/etl) ger ett exempel på en sådan lösning.

**Intag:** Vissa data är inte i något befintligt data lager. När dessa tillfälliga data är en primär källa för innovation bör alternativa metoder beaktas. Tillfälliga data finns i en rad olika befintliga källor, till exempel program, API: er, data strömmar, IoT-enheter, blockchain, program-cache, medie innehåll eller till och med flata filer.

Dessa olika typer av data kan integreras i ett centralt data lager på en OLAP-eller Big data-lösning. För tidiga iterationer av bygg-och-process-rutiner kan dock en online-lösning för transaktions bearbetning (OLTP) vara mer än tillräckliga för att verifiera en kund hypotes. OLTP-lösningar är inte den högsta kvalitets lösningen för eventuella rapporterings scenarier. Men när du [skapar med kund empati](./build.md) fokuserar du på kund behovet av att prioritera tekniska verktyg. När kunden hypotesen har validerats i skala kan en mer lämplig plattform behövas. Referens arkitekturen på [OLTP-data lager](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-transaction-processing) kan hjälpa till att avgöra vilket data lager som passar bäst för din lösning.

**Virtualisering:** Integrering och inmatning av data kan ibland sakta innovationer. När en lösning för datavirtualisering redan är tillgänglig kan detta vara en mer relevant metod. Inmatning och integrering kan både duplicera lagrings-/utvecklings krav, lägga till data svars tider, öka attack ytan, injicera kvalitets problem och förbättra styrnings arbetet. Datavirtualizering är ett mer modernt alternativ som lämnar ursprungliga data på en enda plats och skapar direkt-eller cachelagrade frågor för källdata.

SQL Server 2017 och Azure SQL Data Warehouse både support [PolyBase](/sql/relational-databases/polybase/polybase-guide) , som är den metod för datavirtualisering som oftast används i Azure.

## <a name="next-steps"></a>Nästa steg

Med en strategi för democratizing-data på plats är nästa steg att utvärdera metoder för att [engagera kunder genom appar](./apps.md).

> [!div class="nextstepaction"]
> [Engagera kunder via appar](./apps.md)
