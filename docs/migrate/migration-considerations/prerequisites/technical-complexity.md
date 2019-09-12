---
title: 'Förbered dig för teknisk komplexitet: smidig förändringsledning'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Förbered dig för teknisk komplexitet: smidig förändringsledning'
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 7895094ea0297f725ae4f0451989055cb1afab93
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70825359"
---
# <a name="prepare-for-technical-complexity-agile-change-management"></a>Förbered dig för teknisk komplexitet: smidig förändringsledning

När ett helt datacenter avetableras och återskapas med en enda kodrad är det svårt för traditionella processer att hänga med. Vägledningen i Ramverk för molnimplementering bygger på metoder som Hantering av IT-tjänster (ITSM), Open Group Architecture Framework (TOGAF) med mera. För att säkerställa förändringarnas rörlighet och svarstider omvandlar det här ramverket dessa metoder så att de passar flexibla metodsystem DevOps-metoder.

När du övergår till en dynamisk modell där flexibilitet och iteration står i centrum hanteras teknisk komplexitet och förändringsledning annorlunda än i traditionella vattenfallsmodeller som fokuserar på en linjär serie migreringssteg. Den här artikeln beskriver en övergripande metod för förändringsledning i samband med en dynamisk migrering. När du har läst den här artikeln kommer du att ha utvecklat en kännedom om olika nivåer av förändringsledning och dokumentation som ingår i en stegvis migreringsmetod. Vidare utbildning och beslut krävs för att välja och implementera dynamiska metoder baserat på denna förståelse. Syftet med artikeln är att förbereda molnarkitekter för ett enklare samtal med projektledningen för att förklara det allmänna förändringsledningsbegreppet i denna metod.

## <a name="addressing-technical-complexity"></a>Hantera teknisk komplexitet

När du ändrar tekniska system medför komplexitet och beroenden risker. Molnbaserad migrering är inget undantag. När tusentals&mdash;eller tiotusentals&mdash;tillgångar flyttas till molnet förstärks dessa risker. Det kan ta flera år att identifiera och kartlägga alla beroenden i en stor digital egendom. Det är få företag som klarar av en så lång analyscykel. För att avväga behovet av arkitekturanalys och företagsacceleration fokuserar Ramverk för molnimplementering på en INVEST-modell för hantering av produktuppgifter. I följande avsnitt sammanfattas den här typen av modell.

## <a name="invest-in-workloads"></a>INVEST för arbetsbelastningar

Termen _arbetsbelastning_ förekommer i hela Ramverk för molnimplementering. En arbetsbelastning är en programfunktionsenhet som kan migreras till molnet. Det kan vara ett helt program, ett lager i ett program eller en programsamling. Definitionen är flexibel och kan ändras vid olika migreringsfaser. Ramverk för molnimplementering använder begreppet _invest_ för att definiera en arbetsbelastning.

INVEST är en vanlig akronym i många dynamiska metoder för att skriva användarberättelser eller produktuppgifter, eftersom båda är utdata från dynamiska projekthanteringsverktyg. Den mätbara enheten för utdata i en migrering är en migrerad arbetsbelastning. Ramverk för molnimplementering anpassar begreppet INVEST lite för att definiera arbetsbelastningar:

- **Independent (Oberoende):** En arbetsbelastning får inte ha några otillgängliga beroenden. För att en arbetsbelastning ska betraktas som migrerad bör alla beroenden vara tillgängliga och ingå i migreringen.
- **Negotiable (Förhandlingsbar):** När vidare identifiering utförs ändras definitionen av en arbetsbelastning. Arkitekterna som planerar migreringen kan förhandla faktorer som berör beroenden. Exempel på förhandlingspunkter är förlansering av funktioner, att göra funktioner tillgängliga på ett hybridnätverk eller samling av alla beroenden i en enda lansering.
- **Valuable:** Värdet i en arbetsbelastning mäts av möjligheten att ge användare åtkomst till en produktionsarbetsbelastning.
- **Estimable (Uppskattningsbar):** Beroenden, tillgångar, migreringstid, prestanda och molnkostnader bör gå att uppskatta och beräkna inför migreringen.
- **Small (Liten):** Målet är att samla arbetsbelastningarna i en enda spurt. Detta är dock inte alltid möjligt. I stället uppmuntras team att planera spurtar och versioner för att minimera den tid som krävs för att flytta en arbetsbelastning till produktion.
- **Testbar:** Det bör alltid finnas ett definierat sätt att testa eller verifiera att migreringen av en arbetsbelastning har slutförts.

Den här förkortningen är inte avsedd som en stel pekpinne men kan vägleda definitionen av begreppet _arbetsbelastning_.

## <a name="migration-backlog-aligning-business-priorities-and-timing"></a>Migreringsuppgifter: Justera verksamhetsprioriteter och tidsramar

Migreringsuppgifterna låter dig spåra din portfölj med arbetsbelastningar som ska migreras på högsta nivå. Innan migreringen uppmuntras molnstrategiteamet och molnimplementeringsteamet att göra en granskning av den aktuella [digitala egendomen](../../../digital-estate/index.md) och komma överens om en prioriteringslista för arbetsbelastningar som ska migreras. Den här listan utgör grunden för den första listan med migreringsuppgifter.

Inledningsvis är det osannolikt att de migreringsuppgifterna uppfyller INVEST-kriterierna som beskrivs i föregående avsnitt. De fungerar istället som en logisk gruppering av tillgångar från en preliminär inventering och som platshållare för framtida arbete. Platshållarna är kanske inte tekniskt korrekta men de fungerar för att samordna med verksamheten.

![Relationen mellan loggarna för migrerings-, lanserings- och iterationsuppgifter som används under migreringsprocessen](../../../_images/migration/migrate-release-iteration-backlog-relationship.png)

*Loggarna för migrering-, lanserings- och iterationsuppgifter spårar olika aktivitetsnivåer under migreringsprocessen.*

I migreringsuppgifterna bör förändringsledningsteamet försöka inhämta följande information för alla arbetsbelastningar i planen. Dessa data bör minst vara tillgängliga för arbetsbelastningar som prioriteras för migrering under de kommande två eller tre lanseringarna.

### <a name="migration-backlog-data-points"></a>Datapunkter i migreringsuppgifter

- **Påverkan på verksamheten.** Förståelse av konsekvenserna för företaget om förväntade deadlines missas eller minskad funktioner under frysning.
- **Relativ affärsprioritet.** En rangordnad lista över arbetsbelastningar baserat på affärsprioriteringar.
- **Affärsbeslutägare.** Dokumentera den person som ansvarar för att fatta affärsbeslut om den här arbetsbelastningen.
- **Teknisk ägare.** Dokumentera den person som ansvarar för att fatta tekniska beslut om den här arbetsbelastningen.
- **Förväntade tidslinjer.** När migreringen ska vara slutförd.
- **Frysning av arbetsbelastningen.** Tidsperioder då arbetsbelastningen inte kan ändras.
- **Namn på arbetsbelastning.**
- **Första inventeringen.** Alla tillgångar som krävs för att tillhandahålla arbetsbelastningens funktioner, inklusive virtuella datorer, IT-enheter, data, program, distribueringspipelines med mera. Den här informationen är förmodligen felaktig.

## <a name="release-backlog-aligning-business-change-and-technical-coordination"></a>Lanseringsuppgifter: Justera affärsändringar och teknisk samordning

I samband med en migrering är en _version_ en aktivitet som distribuerar en eller flera arbetsbelastningar till produktion. En lansering täcker i allmänhet flera iterationer eller tekniska uppgifter. Den representerar en enda iteration av en affärsförändring. När en eller flera arbetsbelastningar har förberetts för produktionsbefordran sker en lansering. Beslut om att samla en lansering sker när de migrerade arbetsbelastningarna medför tillräckligt företagsvärde för att motivera att införa ändringen i en företagsmiljö. Versioner körs tillsammans med en [verksamhetsförändringsplan](../optimize/business-change-plan.md)när [företagstestningen](../optimize/business-test.md) har slutförts. Molnstrategiteamet ansvarar för att planera och se över körningen av en version för att säkerställa att den önskade affärsändringen lanseras.

En *uppgiftslista för lansering* är en framtidsplan som definierar en kommande lansering. Uppgiftslistan är knutpunkten mellan företagsförändringsledningen (*migreringsuppgifter*) och den tekniska förändringsledningen (*spurtuppgifter*). Lanseringsuppgifterna består av en lista med arbetsbelastningar från migreringsuppgifterna som anpassas till en specifik undergrupp av företagsuppgifter. Utformningen och inlämningen av lanseringsuppgifter till molnimplementeringsteamet utgör startpunkten för djupare analys och migreringsplanering. När molnimplementeringsteamet har kontrollerat den tekniska informationen som associeras med en lansering kan de besluta att anta lanseringen och etablera en lanseringstidsram baserat på den föreliggande informationen.

Med tanke på mängden analys som krävs för att godkänna en lansering bör molnstrategiteamet upprätthålla en löpande lista för de två till fyra nästa lanseringarna. Teamet bör också försöka kontrollera så mycket som möjligt av följande information innan en lansering definieras och lämnas in. Ett välorganiserat molnstrategiteam som kan underhålla de kommande fyra lanseringarna kan leda till avsevärt bättre precision och efterlevnad av de uppskattade tidsramarna.

### <a name="release-backlog-data-points"></a>Datapunkter i lanseringsuppgifter

Ett samarbete mellan molnstrategiteamet och molnimplementeringsteamet lägger till följande datapunkter för arbetsbelastningarna i lanseringsuppgifterna:

- **Förfinat lager.** Verifiering av nödvändiga till gångar som ska migreras. Dessa verifieras ofta via loggning eller övervakning av data på värd-, nätverks- eller operativsystemnivå för att bilda en korrekt förståelse för nätverket och maskinvarans beroende för varje tillgång under normal belastning.
- **Användningsmönster.** En förståelse av slutanvändarnas användningsmönster. Dessa mönster innehåller ofta en analys av geografisk distribution för slutanvändare, nätverksvägar, säsongsbundna användningstoppar, användnings toppar i dag/per timme och slutanvändarsammansättning (interna jämfört med externa).
- **Prestandaförväntningar.** Analys av tillgängliga dataflöden för loggdata, sidvisningar, nätverksvägar och andra prestandadata som krävs för att replikera slutanvändarupplevelsen.
- **Beroenden.** Analys av mönster för nätverkstrafik och programanvändning för att identifiera eventuella ytterligare arbetsbelastningsberoenden som räknas med i sekvenseringen och miljöberedskapen. Ta inte med en arbetsbelastning i en lansering förrän något av följande villkor kan uppfyllas:
  - Alla beroende arbetsbelastningar har migrerats.
  - Nätverks- och säkerhetskonfigurationerna har implementerats för att ge arbetsbelastningen åtkomst till alla beroenden i förhållande till befintliga prestandaförväntningar.
- **Önskat förhållningssätt till databasmigrering.** På nivån för migreringsuppgifter övervägs endast det förväntade migreringsprojektet vid analys. Till exempel, om verksamhetsresultatet är att lämna ett befintligt datacenter förväntas alla migreringar att vara värdbytesscenarier i migreringsuppgifterna. I lanseringsuppgifterna bör molnstrategiteamet och molnimplementeringsteamet utvärdera det långsiktiga värdet i ytterligare funktioner, modernisering och fortsatta investeringar i utveckling för att utreda om en modernare metod vore lämplig.
- **Verksamhetstestkriterier.** När en arbetsbelastning har lagts till i migreringsuppgifterna bör teamen komma överens om testkriterier. I vissa fall kan testkriterierna begränsas till ett prestandatest med en definierad grupp betrodda användare. För statistisk validering bör dock ett automatiserat prestandatest användas. Den befintliga programinstansen har vanligtvis inga automatiserade testfunktioner. Om detta visar sig vara korrekt är det inte ovanligt att molnarkitekterna arbetare med betrodda användare för att skapa ett belastningstest som baslinje för den befintliga lösningen som kan användas som riktmärke under migreringen.

### <a name="release-backlog-cadence"></a>Takt för lanseringsuppgifter

Lanseringarna sker regelbundet i inarbetade migreringar. Molnimplementeringsteamets takt normaliseras vanligtvis till att ta fram en lansering för varje två till fyra upprepningar (vanligtvis en eller två månader). Detta bör dock ske naturligt. En artificiell lanseringstakt kan skada molnimplementeringsteamets förmåga att uppnå ett konsekvent genomflöde.

För att stabilisera inverkan på företaget bör molnstrategiteamet etablera en månatlig lanseringsprocess med företaget så att regelbunden dialog bibehålls men de bör även skapa en förväntning om att det kommer att ta flera månader innan en regelbunden lanseringstakt kan förutsägas.

## <a name="sprint-or-iteration-backlog-aligning-technical-change-and-effort"></a>Spring- eller iterationsuppgifter: Anpassa teknisk ändring och tekniska projekt

En *spring-* eller *iteration* är en konsekvent och tidsbegränsad arbetsenhet. I migreringsprocessen mäts detta ofta i steg om två veckor. Det är dock inte omöjligt att ha iterationer på en till fyra veckor. När du skapar tidsbegränsade iterationer tvingas konsekventa intervall vilket möjliggör mer regelbunden justering av planer baserat på ny information. Under en given spurt ingår vanligtvis utvärderings-, migrerings- och arbetsbelastningsoptimeringsuppgifter som definieras i migreringsuppgifterna. De här arbetsenheterna bör spåras och hanteras i samma projektledningsverktyg som migrerings- och lanseringsuppgifterna så att alla nivåer av förändringsledningen är konsekvent.

*Sprintuppgifter* eller *iterationsuppgifter* består av tekniska uppgifter som ska slutföras i en enda spurt eller iteration för migrering av individuella tillgångar. Arbetet bör härledas från listan med arbetsbelastningar som migreras. När du använder verktyg som Azure DevOps (tidigare Visual Studio Online) för projekthantering är uppgifterna i en spurt underordnade produktuppgifterna i loggen med lanseringsuppgifterna och migreringsuppgifterna. En sådan överordnad-underordnad relation förtydligar på alla nivåer i förändringsledningen.

Inom en enda spurt eller iteration arbetar molnimplementeringsteamet med att leverera de tekniska uppgifterna det har åtagit sig och arbetar mot att migrera den definierade arbetsbelastningen. Detta är slutresultatet av förändringsledningsstrategin. När uppgifterna har slutförts kan de testas genom att kontrollera arbetsbelastningens produktionsberedskap i molnet.

### <a name="large-or-complex-sprint-structures"></a>Stora eller komplexa spurtstrukturer

För en liten migrering med ett fristående migreringsteam kan en enda spurt omfatta alla fyra faser i en migrering för en enskild arbetsbelastning (*utvärdering*, *migrering*, *optimering* och *säkerhets och hantering*). Oftast delas var och en av dessa processer av flera team i olika arbetsobjekt mellan olika spurter. Beroende på projekttyp, projektskala och roller kan dessa spurter utformas på olika sätt.

- **Migreringsfabrik.** Storskaliga migreringar kräver ibland en metod som påminner om en fabrik för körningsmodellen. I den här modellen allokeras olika team till körningen av en viss migreringsprocess (eller en delmängd av processen). När körningen är klar fylls uppgiftslistan för nästa team automatiskt med resultatet från det andra teamets spurt. Det här är en effektiv metod för storskalig migrering med värdbyte för många arbetsbelastningar med tusentals virtuella datorer som rör sig genom utvärderings-, arkitektur-, reparations- och migreringsfaser. Men för att den här metoden ska fungera måste en ny homogen miljö med strömlinjeformad ändringshantering och godkännandeprocesser finnas.
- **Migreringsvågor.** En annan metod som fungerar bra för stora migreringar är en vågmodell. I den här modellen är arbetsfördelningen inte lika tydlig. Team hanterar själva migreringsprocessen för individuella arbetsbelastningar själva. Varje spurt är dock olik de andra. I en spurt kanske teamet slutför en utvärdering och arkitektur. I en annan spurt slutför de kanske migreringen. I ännu en sprint kanske fokus ligger på optimering och produktionslansering. Med den här metoden kan en kärngrupp anpassa sig till arbetsbelastningarna och följa dem genom hela processen. När den här metoden används kan mångfalden av färdigheter och sammanhang minska teamets förmåga att arbeta snabbt vilket kan fördröja migreringen. Dessutom kan hinder under godkännandefaserna orsaka stora förseningar. Om du använder den här metoden är det viktigt att du har olika alternativ i lanseringsuppgifterna så att teamet kan fortsätta arbeta under blockerade perioder. Det är också viktigt att korsutbilda teammedlemmar så att deras färdigheter passar för temat för varje spurt.

### <a name="sprint-backlog-data-points"></a>Datapunkter i spurtuppgifter

Efter en spurt inhämtas och dokumenteras ändringarna i arbetsbelastningen vilket stänger förändringsledningscykeln. När det är klart bör som minst följande dokumenteras. Under hela körningen av spurten bör denna dokumentation skapas i fas med de tekniska uppgifterna.

- **Distribuerade tillgångar.** Alla tillgångar som distribueras till molnet som värd för arbetsbelastningen.
- **Åtgärder.** Eventuella ändringar i tillgångarna för att förbereda för migrering av molnet.
- **Konfiguration.** Vald konfiguration för alla distribuerade tillgångar, inklusive referenser till konfigurationsskript.
- **Distributionsmodell.** Metod som används för att distribuera till gången till molnet, inklusive referenser till eventuella distributionsskript eller verktyg.
- **Arkitektur.** Dokumentation av arkitekturen som distribueras till molnet.
- **Prestandamått.** Utdata från automatiserad testning eller affärstestning som utförs för att validera prestandan vid tidpunkten för distributionen.
- **Unika krav eller konfiguration.** Alla unika aspekter av distributionen, konfigurationen eller de tekniska krav som ställs för att kunna använda arbetsbelastningen.
- **Driftsgodkännande.** Programägare och ansvarig IT-teknikers godkännande som bekräftar att arbetsbelastningen är redo för drift.
- **Arkitekturgodkännande.** Godkännande från arbetsbelastningsägaren och molnimplementeringsteamet för att bekräfta eventuella arkitekturändringar som behövs som värd för varje tillgång.

## <a name="next-steps"></a>Nästa steg

När ändringshanteringsmetoderna har etablerats är det dags att hantera det sista förhandskravet, [granskningen av migreringsuppgifterna](./migration-backlog-review.md)

> [!div class="nextstepaction"]
> [Granskning av migreringsuppgifter](./migration-backlog-review.md)
