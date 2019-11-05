---
title: Etablera granskning av driftslämplighet
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vägledning om operativa grunderna
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 4fa02d8b81e4f1b0afcd5cf5fb932c52fc3c1ea6
ms.sourcegitcommit: 74c1eb00a3bfad1b24f43e75ae0340688e7aec48
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/28/2019
ms.locfileid: "72979928"
---
# <a name="establish-an-operational-fitness-review"></a>Etablera granskning av driftslämplighet

I takt med att ditt företag börjar arbeta med arbets belastningar i Azure är nästa steg att upprätta en process för *utvärdering av drifts förmåga*. Med den här processen räknas, implementeras och upprepas de icke- *funktionella kraven* för dessa arbets belastningar. Icke-funktionella krav är relaterade till tjänstens förväntade drift beteende.

Det finns fem viktiga kategorier av icke-funktionella krav, som kallas för [pelare för program kvalitet](https://docs.microsoft.com/azure/architecture/guide/pillars):

- Skalbarhet
- Tillgänglighet
- Återhämtning, inklusive affärs kontinuitet och haveri beredskap
- Hantering
- Säkerhet

En process för granskning av operativa krav garanterar att dina verksamhets kritiska arbets belastningar uppfyller förväntningarna för din verksamhet med avseende på kvalitets pelaren.

Skapa en process för verksamhets vårds granskning för att helt förstå de problem som uppstår när du kör arbets belastningar i en produktions miljö och hur du kan åtgärda och lösa problemen. Den här artikeln beskriver en övergripande process för att få en verksamhets vårds recension som ditt företag kan använda för att uppnå det här målet.

## <a name="operational-fitness-at-microsoft"></a>Drifts lämplighet hos Microsoft

Från början har många team i Microsoft varit inblandade i utvecklingen av Azure-plattformen. Det är svårt att garantera kvalitet och konsekvens för ett projekt av sådan storlek och komplexitet. Du behöver en robust process för att räkna upp och implementera grundläggande icke-funktionella krav regelbundet.

De processer som Microsoft följer utgör grunden för de processer som beskrivs i den här artikeln.

## <a name="understand-the-problem"></a>Förstå problemet

När du lärde dig att [komma igång](../getting-started/migrate.md)är det första steget i företagets digitala omvandling att identifiera de affärs problem som ska lösas genom att anta Azure. Nästa steg är att fastställa en lösning på hög nivå för problemet, till exempel migrera en arbets belastning till molnet eller anpassa en befintlig lokal tjänst för att inkludera moln funktioner. Slutligen kan du utforma och implementera lösningen.

Under den här processen är fokus ofta att fokusera på funktionerna i tjänsten: den uppsättning _funktions_ krav som du vill att tjänsten ska utföra. En produkt leverans tjänst kräver till exempel funktioner för att fastställa käll-och mål platser för produkten, spåra produkten under leverans och skicka meddelanden till kunden.

De _funktioner_ som inte fungerar, är däremot relaterade till egenskaper som tjänstens [tillgänglighet](https://docs.microsoft.com/azure/architecture/checklist/availability), [återhämtning](https://docs.microsoft.com/azure/architecture/resiliency)och [skalbarhet](https://docs.microsoft.com/azure/architecture/checklist/scalability). Dessa egenskaper skiljer sig från funktions kraven eftersom de inte direkt påverkar den slutliga funktionen för en viss funktion i tjänsten. Men inte funktions kraven relaterar till tjänstens prestanda och kontinuitet.

Du kan ange vissa krav som inte fungerar i enlighet med ett service avtal (SLA). Du kan till exempel uttrycka tjänste kontinuiteten i procent av tillgängligheten: "tillgänglig 99,99% av tiden". Andra ej fungerande krav kan vara svårare att definiera och kan ändras när produktions behoven förändras. En kundorienterad tjänst kan till exempel påverka förväntade data flödes krav efter en överspänning av popularitet.

> [!NOTE]
> Mer information om återhämtnings kraven finns i [utforma pålitliga Azure-program](https://docs.microsoft.com/azure/architecture/reliability#define-requirements). Artikeln innehåller förklaringar av begrepp som återställnings punkt mål (återställnings punkt mål), återställnings tids mål (RTO) och service avtal.

## <a name="process-for-operational-fitness-review"></a>Process för översyn av drifts förmåga

Nyckeln för att upprätthålla prestanda och kontinuitet för ett företags tjänster är att implementera en process för drifts-och tränings granskning.

![En översikt över processen för översyn av drifts förmåga](../_images/manage/ofr-flow.png)

Processen har två faser på hög nivå. I krav *fasen*upprättas kraven och mappas till stöd för tjänster. Den här fasen inträffar sällan: kanske varje år eller när nya åtgärder införs. Utdata från krav fasen används i *flödes fasen*. Flödes fasen förekommer oftare, till exempel varje månad.

### <a name="prerequisites-phase"></a>Krav fas

Stegen i den här fasen fångar upp kraven för att utföra en regelbunden granskning av de viktiga tjänsterna.

1. **Identifiera kritiska affärs åtgärder**. Identifiera företagets verksamhets kritiska affärs åtgärder. Affärs åtgärder är oberoende av alla stöd tjänster. Med andra ord representerar affärs åtgärder de faktiska aktiviteter som företaget behöver utföra och som stöds av en uppsättning IT-tjänster.

    Termen *verksamhets kritisk* (eller *verksamhets kritisk*) återspeglar en allvarlig påverkan på verksamheten om åtgärden störs. En online-detaljist kan till exempel ha en affärs åtgärd, till exempel "göra det möjligt för en kund att lägga till ett objekt i en Shopping vagn" eller "bearbeta en kredit korts betalning". Om någon av dessa åtgärder Miss lyckas kan en kund inte slutföra transaktionen och företaget kan inte realisera försäljning.

1. **Mappa åtgärder till tjänster**. Mappa kritiska affärs åtgärder till de tjänster som stöder dem. I shopping-shopping-exemplet kan flera tjänster delta, inklusive en inventering av lager hanterings tjänster och en shopping vagns tjänst. För att kunna bearbeta en kredit korts betalning kan en lokal betalnings tjänst samverka med en tredje part, tjänsten för betalnings bearbetning.

1. **Analysera tjänst beroenden**. De flesta affärs åtgärder kräver samordning mellan flera stöd tjänster. Det är viktigt att förstå beroenden mellan tjänsterna och flödet av verksamhets kritiska transaktioner genom dessa tjänster.

    Överväg även beroenden mellan lokala tjänster och Azure-tjänster. I shopping-shopping-exemplet kan inventeringen av lager hanterings tjänsten finnas lokalt och mata in data som anges av anställda från ett fysiskt lager. Det kan dock lagra data från andra platser i en Azure-tjänst, till exempel [Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-introduction)eller en databas, till exempel [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).

Utdata från dessa aktiviteter är en uppsättning *styrkorts mått* för tjänst åtgärder. Styrkortet mäter kriterier som tillgänglighet, skalbarhet och haveri beredskap. Styrkortets mått uttrycker de operativa villkor som du förväntar dig att tjänsten ska uppfylla. Dessa mått kan uttryckas på alla nivåer av granularitet som är lämpliga för tjänst åtgärden.

Styrkortet bör uttryckas i enkla termer för att under lätta en meningsfull diskussion mellan företagets ägare och teknik. Ett styrkorts Mät värde för skalbarhet kan till exempel vara färgkodat på ett enkelt sätt. Grönt innebär att de definierade villkoren uppfylls, gult innebär att det inte går att uppfylla de definierade kriterierna, men aktivt implementera en planerad åtgärd och rött innebär att det inte går att uppfylla de definierade kriterierna utan någon plan eller åtgärd.

Det är viktigt att betona att dessa mått bör vara direkt reflekterar affärs behoven.

### <a name="service-review-phase"></a>Tjänst – gransknings fas

Tjänsten för granskning av tjänster är kärnan i den operativa tränings granskningen. Det omfattar följande steg:

1. **Mät tjänst mått**. Använd styrkortets mått för att övervaka tjänsterna för att säkerställa att tjänsterna uppfyller affärs förväntningarna. Tjänst övervakning är viktigt. Om du inte kan övervaka en uppsättning tjänster med avseende på de funktioner som inte fungerar, bör du överväga att motsvarande styrkorts mått är röda. I det här fallet är det första steget för reparation att implementera lämplig tjänst övervakning. Om företaget till exempel förväntar sig att en tjänst ska fungera med 99,99% tillgänglighet, men det inte finns någon produktions telemetri på plats för att mäta tillgänglighet, förutsätter vi att du inte uppfyller kravet.

2. **Planera reparation**. För varje tjänst åtgärd där måtten unders tiger ett acceptabelt tröskelvärde bestämmer du kostnaden för att åtgärda tjänsten för att vidta åtgärder på en acceptabel nivå. Om kostnaden för att åtgärda tjänsten är större än den förväntade intäkten av tjänsten kan du gå vidare för att ta hänsyn till de immateriella kostnaderna, till exempel kund upplevelse. Om kunderna till exempel har svårt att placera en lyckad beställning med hjälp av tjänsten kan de välja en konkurrent i stället.

3. **Implementera reparation**. När företags ägarna och teknik teamet samtycker till en plan implementerar du den. Rapportera status för implementeringen när du granskar styrkortets mått.

Den här processen är iterativ och det är idealiskt att ditt företag har ett team avsett för IT. Det här teamet bör uppfylla regelbundet för att granska befintliga reparations projekt, inleda den grundläggande granskningen av nya arbets belastningar och spåra företagets övergripande styrkort. Teamet bör även ha befogenhet att hålla reparations teamen beroende av om de ligger bakom schemat eller inte uppfyller måtten.

## <a name="structure-of-the-review-team"></a>Gransknings teamets struktur

Teamet som ansvarar för den operativa tränings granskningen består av följande roller:

- **Företags ägare**: ger kunskap om verksamheten för att identifiera och prioritera varje verksamhets kritisk affärs åtgärd. Den här rollen Jämför även minsknings kostnaderna med påverkan på verksamheten och bedriver det slutliga beslutet om reparation.

- **Affärs**rådgivare: delar upp affärs åtgärder i diskret-delar och mappar dessa delar till tjänster och infrastruktur, oavsett om de finns lokalt eller i molnet. Rollen kräver djupgående kunskap om den teknik som är kopplad till varje affärs åtgärd.

- **Tekniker ägare**: implementerar de tjänster som är kopplade till affärs åtgärden. Dessa personer kan delta i utformningen, implementeringen och distributionen av lösningar för problem som inte är av en funktion som inte kan hanteras av gransknings teamet.

- **Tjänste ägare**: driver företagets program och tjänster. Dessa personer samlar in loggnings-och användnings data för dessa program och tjänster. Dessa data används både för att identifiera problem och för att verifiera korrigeringar när de har distribuerats.

## <a name="review-meeting"></a>Granska möte

Vi rekommenderar att ditt gransknings team uppfyller vanliga villkor. Teamet kan till exempel mötas per månad och sedan rapportera status och mått till chefens ledarskaps period.

Anpassa informationen om processen och mötet så att den passar just dina behov. Vi rekommenderar följande uppgifter som utgångs punkt:

1. Företagets ägare och affärs rådgivare räknar upp och avgör de funktions krav som ställs för varje affärs åtgärd, med inmatat från tekniker och tjänst ägare. Granska och verifiera prioritet för affärs åtgärder som har identifierats tidigare. Tilldela en prioritet i den befintliga listan för nya affärs åtgärder.

2. Teknik-och tjänst ägarna mappar affärs verksamhetens aktuella tillstånd till motsvarande lokala tjänster och moln tjänster. Mappningen är en lista över komponenterna i varje tjänst, orienterade som ett beroende träd. Tjänste ägarnas tekniker och tjänster avgör sedan de kritiska Sök vägarna i trädet.

3. Teknik-och tjänst ägarna granskar det aktuella läget för drifts loggning och övervakning av de tjänster som anges i föregående steg. Robust loggning och övervakning är kritiskt: de identifierar tjänst komponenter som bidrar till att det inte går att uppfylla icke-funktionella krav. Om det inte finns tillräckligt med loggning och övervakning på plats måste teamet placera dem på plats genom att skapa och implementera en plan.

4. Teamet skapar styrkorts mått för nya affärs åtgärder. Styrkortet består av listan över komponent komponenter för varje tjänst som identifieras i steg 2. Det är justerat med de infunktionella kraven och innehåller ett mått på hur väl varje komponent uppfyller kraven.

5. För komponenter som inte uppfyller kraven, utformar teamet en hög nivå lösning och tilldelar en teknisk ägare. I detta läge upprättar företags ägaren och affärs advokaten en budget för reparations arbetet, baserat på den förväntade intäkterna från affärs verksamheten.

6. Slutligen genomför teamet en granskning av det pågående reparations arbetet. Varje styrkorts mått för pågående arbete granskas mot de förväntade kriterierna. För komponenter som uppfyller mått villkoren visar tjänst ägaren loggnings-och övervaknings data för att bekräfta att villkoren är uppfyllda. För de komponenter som inte uppfyller Mät värdena förklarar varje ingenjörs ägare de problem som förhindrar att villkor uppfylls och presenterar nya design funktioner för reparation.

## <a name="recommended-resources"></a>Rekommenderade resurser

- [Pelare för program kvalitet](https://docs.microsoft.com/azure/architecture/guide/pillars).
    I det här avsnittet i guiden Azure Application arkitektur beskrivs de fem pelaren för program kvalitet: skalbarhet, tillgänglighet, återhämtning, hantering och säkerhet.
- [Tio design principer för Azure-program](https://docs.microsoft.com/azure/architecture/guide/design-principles).
    Det här avsnittet i guiden Azure Application arkitektur beskriver en uppsättning design principer för att göra programmet mer skalbart, elastiskt och hanterbart.
- [Utforma elastiska program för Azure](https://docs.microsoft.com/azure/architecture/resiliency).
    Den här guiden börjar med en definition av termen _återhämtning_ och relaterade begrepp. Sedan beskriver den en process för att uppnå återhämtning genom att använda en strukturerad metod under ett programs livs längd, från design och implementering till distribution och drift.
- [Design mönster för molnet](https://docs.microsoft.com/azure/architecture/patterns).
    De här design mönstren är användbara för teknik grupper när du skapar program i grund stenarna för program varu kvalitet.
