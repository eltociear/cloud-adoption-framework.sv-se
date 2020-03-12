---
title: Balansera konkurrerande prioriteringar
description: Identifiera strategier för att balansera konkurrerande prioriteringar
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/04/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: ba70687627e81b58eb76cd69838abf1ebcdb6489
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092990"
---
# <a name="balance-competing-priorities"></a>Balansera konkurrerande prioriteringar

Att kräva en digital omvandlings resa fungerar som en tvingande funktion för intressenter, i affärs-och teknik teamet. Sökvägen till framgång dirigeras ordentligt i organisationernas möjlighet att balansera konkurrerande prioriteringar.

I likhet med andra digitala transformationer, kommer moln införande att exponera konkurrerande prioriteringar under hela livs cykeln för införande. Liksom andra former av omvandling, kommer möjligheten att hitta balans i dessa prioriteringar att ha en betydande inverkan på affärs värdets realisering. Att balansera dessa konkurrerande prioriteringar kräver öppen (och ibland svåra) konversationer mellan intressenter (och vid tillfällen med enskilda deltagare).

Den här artikeln beskriver några av de konkurrerande prioriteringar som ofta diskuteras under körningen av varje metod. Vi hoppas att den här avancerade medvetenheten hjälper bättre att förbereda för dessa diskussioner när du utvecklar din strategi för moln införande.

![Översikt över moln införande livs cykel](../_images/caf-overview.png)

Följande avsnitt överensstämmer med flödet av moln implementeringens livs cykel som är synlig ovan. Men det är viktigt att Observera att moln införande är iterativt (inte en sekventiell process) dessa konkurrerande prioriteringar kommer att framställas (och ibland upprepas) vid olika tidpunkter längs din moln införande.

## <a name="general-theme-of-the-cloud-adoption-framework-approach"></a>Allmänt tema för moln införande Ramverks metod

Monolitisk-lösningar och avancerad planering är båda bygger på en serie antaganden som kan (eller inte) Visa sig vara korrekt med tiden. Att anta molnet är ofta en ny upplevelse för verksamheten och de tekniska teamen. Precis som med de flesta nya upplevelser eller inlärnings möjligheter är det en hög sannolikhet att dessa antaganden kommer att bli falska.

Följande beprövade Agile-principer för fördröjda tekniska beslut är den prioriterade metoden för de flesta vägledningar i det här ramverket. Den här metoden följer ett konsekvent mönster: upprätta en allmän slut för ande, flytta snabbt till den första implementeringen, testa och validera antaganden, omkopplare tidigt för att adressera antaganden. Den här typen av tillväxt tänkesätt maximerar inlärningen och minimerar risken för affärs värde. Men den här tänkesätt kräver en viss bekvämlighet med tvetydighet.

Ibland kan tvetydigheten vara scarier (eller mer farlig) än falskt antaganden. Även om det här ramverket lutar inlärnings-och adresserings problem under körningen, finns det många situationer som kräver att teamet lutar sig över analysbaserade eller antagandebaserade metoder. Följande avsnitt kommer att försöka illustrera minst ett "expanderat omfattnings exempel" i varje avsnitt för att illustrera tillfällen när en andra djupare iteration skulle vara värdefull.

## <a name="balance-during-strategy"></a>Balans under strategin

Kärn målet med strategi metodik är att utveckla anpassningar mellan intressenter. När den anpassade strategiska positionen har definierats kommer beteendet att drivas av alla metoder för att säkerställa att de tekniska besluten anpassar sig efter dina affärs resultat. Genom att gynna anpassningen av intressenter skapar du en gemensam uppsättning med konkurrerande prioriteringar: **djup på motivering** **och tid till företags påverkan**.

**Konkurrerande prioriteringar:**

- **Motiverings djup**: intressenter vill ofta ha en djup finansiell analys och fullständig affärs motivering för att vara bekväm att justera till en strategisk riktning. Den analys nivån kan tyvärr kräva en längre tids period för att tillåta insamling och analys av data.
- **Tiden för att påverka verksamheten**: i motsatt grad är intressenter ofta konto för att leverera affärs resultat inom bestämda tids ramar. Tids krävande analyser och bedömningar kan leda till risker innan det tekniska arbetet börjar.

**Minsta omfattning:** Att hitta den här balansen kräver diskussioner mellan intressenter tidigt i processen. Strategi metoden rekommenderar att du begränsar justerings omfånget under den här tidiga ansträngningen. I den föreslagna metoden fokuserar intressenter på att justera runt en uppsättning viktiga motivation, mätbara resultat och en övergripande affärs justering. Vi rekommenderar att intressenter sedan snabbt genomför ett litet antal inledande projekt eller pilot för att driva nödvändiga inlärnings möjligheter.

**Exempel på utökad omfattning:** Om den inledande företags analysen visar en hög risk för att verksamheten påverkas negativt kan intressenterna behöva sakta ned och bättre utvärdera en djupare analys under affärs skäl.

## <a name="balance-during-plan"></a>Saldo under plan

På samma sätt som strategi prioriteringarna, under planeringen måste du göra en avvägning: djup vid inledande planering kontra fördröjda tekniska beslut.

**Konkurrerande prioriteringar:**

- Det finns ofta ett stort antal antaganden **för den första planeringen** avseende teknisk implementering i molnet. I synnerhet när teamet har kunskaps luckor, påverkas miljön av identifierings luckor, eller så har arbets belastningarna inte några tydligt definierade arkitektur slut tillstånd. Alla dessa antaganden är vanliga i detaljerade moln implementerings planer. Experimentering, pilot och kvalitativ analys krävs för att ta bort dessa antaganden.
- **Fördröjda tekniska beslut** förutsätter att det senare ett tekniskt beslut kan fattas, desto mer exakta är beslutet. Följande principer för flexibel produkt planering bidrar till att fördröja tekniska beslut, så att de kan ske vid rätt tidpunkt med tillräckligt med information. Den här metoden resulterar dock i en mycket högre grad av tvetydighet i den första planen.

**Minsta omfattning:** Smidiga produkt utvecklings metoder rekommenderas för att köra en åtgärds fråga i hanterbara planer. Plan metoden rekommenderar följande steg för att uppnå saldot. Inventera den fullständiga digitala egendomen med hjälp av automatiserade identifierings verktyg, men Använd stegvisa rationalisering för att planera så långt som de kommande 1-3 månaderna av arbete. Se till att organisationens justering går snabbt. Skapa en färdighets beredskaps plan för det tilldelade teamet. Använd mallen för moln implementerings planer för att snabbt distribuera en första efter släpning.

**Exempel på utökad omfattning:** Vid ett tillfälle kan leverans av en moln implementerings plan svara på en tids känslig eller affärs händelse med hög påverkan. När du behöver flytta ett stort antal till gångar under en bestämd tids period, följer stegen ovan ofta en djupare planerings ansträngning. Nyckeln för att lyckas i dessa scenarier är att planera tillräckligt för att komma igång och sedan planera för hela engagemanget. Den här metoden minskar sannolikheten för planering av spärrning av affärs resultat.

## <a name="balance-during-ready"></a>Saldo under klart

När antagande team förbereds för sina första steg i molnet, finns det ofta konkurrerande prioriteringar mellan tiden för att vidta åtgärder och långsiktiga åtgärder. Teamet kanske är väl lämpade att leverera på den uppgift som är väl hanterad. Detta är nödvändigt i traditionella IT-miljöer, där utvecklingen av en plattform kräver fysiska till gångar och förvärvs cykler. Men när hela IT-plattformen definieras i kod, minskar traditionella utvecklings taktiker (t. ex. omstrukturering) behovet av bra hantering från början.

**Konkurrerande prioriteringar:**

- **Långsiktiga åtgärder:** Kunder kan ofta blockeras av en moln miljö som uppfyller funktions paritet med aktuella drift hanterings-, styrnings-och säkerhets system. I en aktuell studie av kunder är mer än 90% av kunderna som behövde stöd för att komma förbi den här tänkesätt. Den här blockeraren infogar månads fördröjning för att sakta in eller förhindra företags påverkan.
- **Tidpunkt för införande:** Molnbaserade verktyg som Azure Policy, Azure-ritningar och hanterings grupper gör det enkelt att omväga över IT-plattformen. Dessutom ger fördefinierade landnings zoner påstridigt-positioner för att påskynda distributionen till en miljö som redan uppfyller många av funktions paritets kraven. Tillsammans finns det möjligheter att påskynda tiden till marknaden, med minimal påverkan på långsiktiga åtgärder.

**Minsta omfattning:** Den färdiga metoden beskriver en direkt väg från snabba antagande till långsiktiga åtgärder. Den här metoden börjar med en grundläggande introduktion till de verktyg som gör det möjligt för omstrukturering av miljön. Baserat på dessa verktyg och miljö krav, är kunderna guidade att välja mellan fördefinierade landnings zoner (varje levererad med hjälp av infrastruktur som kod modeller). Koden kan sedan omstruktureras under moln implementeringen för att förbättra drift-, säkerhets-och hanterings postures.

**Exempel på utökad omfattning:** För team vars antagande plan kräver ett Mid-långsiktigt mål (inom 24 månader) som värd för **fler än 1 000-tillgångar (appar, infrastruktur eller data till gångar) i molnet**, föreslås en mer robust vy av landnings zoner. I dessa fall bör styr och hantera metoder beaktas under inledande landnings zon-konversationer. Den här djupare beräkningen lägger dock ofta till veckor eller månader i en moln implementerings plan. För att minimera påverkan på affärs resultat bör antagande teamet piloterar faktiska arbets belastningar i molnet parallellt med att skapa en mer vuxen landnings zon och en central arkitektur lösning.

## <a name="balance-during-migrate"></a>Saldo under migrering

Under migreringen är det vanligt att anta att arbets belastningarna kommer att revaras i molnet i den aktuella konfigurationen. Detta konkurrerar direkt med en framåtriktad vy för att bygga om alla arbets belastningar för att bättre utnyttja moln funktionerna. Sadly är två inte ömsesidigt uteslutande och kan vara kostnads fria när de hanteras via en gemensam process.

**Konkurrerande prioriteringar:**

- **Rehost:** Kunderna motsvarar ofta migrering till en _hiss och flyttar_ rörelserna för att replikera alla till gångar till molnet i den aktuella tillstånds konfigurationen. Detta resulterar i lite drift i IT-portföljen. Den här metoden är också det snabbaste sättet att dra tillbaka till gångar i ett befintligt Data Center.
- **Rearkitekt:** Att utnyttja arkitekturen för varje arbets belastning maximerar molnets värde för kostnad, prestanda och åtgärder. Den här metoden är dock mycket långsammare och kräver ofta åtkomst till varje programs käll kod.

**Minsta omfattning:** Vid planering i tidigt skedet använder du alternativet Rehost för att planera, med en tydlig förståelse för att det här alternativet är ett första affärs antagande och inte ett tekniskt beslut. I metoderna för migrering anropar antagande teamet detta antagande för varje migrerad arbets belastning. Den här metoden följer stegen i utvärdera, migrera, befordra för varje arbets belastning eller grupp eller arbets belastningar som skapar en migrerings fabrik. Under utvärderings fasen utvärderar antagande teamet tekniska anpassningar och arkitektur för varje arbets belastning. Utvärderings ansträngningen resulterar sällan i en ren hiss och Skift-metod, eftersom många av komponenterna i arkitekturen brukar väljas för omberäkning och modernisering.

**Exempel på utökad omfattning:** För verksamhets kritiska eller hög känslighets arbets belastningar, t. ex. en stordator eller ett mikrotjänstprogram på flera nivåer, kan en djupare bedömning av arbets belastningen krävas under utvärderings fasen. I dessa omarkitekturs situationer rekommenderar vi att kunderna använder Azures arkitektur granskning och Azure Architecture Framework för att förfina arbets belastnings kraven under utvärderingen.

## <a name="balance-during-innovate"></a>Saldo under innovation

Sant kundinriktad innovation skapar vanliga motstridiga prioriteringar mellan behovet av att leverera på en planerad funktions uppsättning och en kund empati utvecklings process.

**Konkurrerande prioriteringar:**

- Funktions fokus: de första planerna för innovation bygger på befintliga funktioner för digital egendom och molnet för att leverera en uppsättning funktioner som uppfyller ett kund behov. Det är enkelt att tillåta att planera den tekniska implementeringen, vilket leder till en funktion som fokuserar på utvecklings arbete. Den här metoden leder ofta till tillfälliga från intressenter, men minskar sannolikheten för att du ska kunna driva innovation som påverkar kund beteenden.
- Kund empati: de första planerna är en viktig del av arbets sidan i utvecklingen och bör ingå i vanlig rapportering. Att lära sig, mäta och utveckla med kund empati är dock ett mer exakt mått på framgång i en Innovations ansträngning. Att fokusera på kundernas över-funktioner är mer sannolikt att leda till både kortsiktig och långsiktig kund nöjdhet och inverkan på företaget.

**Minsta omfattning:** Den förnyade metoden visar hur du integrerar strategi och planer genom affärs värdes konsensus. Guiden introducerar sedan molnbaserade verktyg som kan påskynda varje ämnes område av innovation, som tillhör bästa praxis för implementering. Slutligen visar avsnittet process förbättringar olika metoder för att skapa kund empati, samtidigt som det rör sig om planer och strategier i molnets införande resa. Den här metoden fokuserar på att leverera innovation med hjälp av så lite teknik som möjligt.

**Exempel på utökad omfattning:** Ibland kan en innovation vara beroende av verksamhets kritiska arbets belastningar med hög känslighet. När "kunden" är en intern användare kan utvecklings ansträngningen vara både verksamhets kritisk och hög känslighet under det tidigaste antalet iterationer. I dessa scenarier rekommenderar vi att implementerings team utnyttjar Azures arkitektur granskning och Azure Architecture Framework för att utvärdera avancerad arkitektur design tidigt i processen.

## <a name="balance-during-govern"></a>Saldo under styrning

Användningen av moln styrning är en konstant balans mellan två konkurrerande prioriteringar: hastighet/flexibilitet och en väl styrd miljö. Moln styrnings teamet fokuserar på att utvärdera och minimera risker för verksamheten genom enhetliga kontroller och minimerande förändringar. Antagande teamet fokuserar på att driva affärs resultat, vilket kräver nya risker och som skapar ändringar.

**Konkurrerande prioriteringar:**

- Välstyrt: varje kontroll som är avsedd för att minimera risken, något som är aspekt av ändrings-eller begränsnings design alternativen. Kontrollen är nödvändig för en väl styrd miljö. Men när kontroller är utformade och distribuerade i isolering kan de vara lika skadliga som de risker som de är avsedda att förhindra.
- Hastighet/flexibilitet: hastighet och flexibilitet är grundläggande affärs krav i den digitala ekonomin. Båda kräver möjlighet att styra ändringar med minimala Blocker för innovation eller införande. När ändringar drivs i isolering av styrning, genererar den nya risker som kan skada verksamheten på oönskade sätt.

**Minsta omfattning:** Metoden styrd innebär att varken styrning eller antagande bör inträffa i isoleringen. Den här metoden börjar med en förståelse för styrnings discipliner och en konversation kring affärs risker, principer och processer. Som aktiv medlem i hela molnet, kan styrnings teamet implementera en minsta uppsättning guardrails för att lösa de konkreta riskerna i moln implementerings planen. Med tiden kan styrnings teamet omstrukturera och expandera dessa guardrails för att möta nya risker. Den här metoden maximerar inlärningen och innovationen och minimerar risken.

**Exempel på utökad omfattning:** När affärs risken är hög, särskilt tidigt i antagandet, kan moln styrnings gruppen behövas för att påskynda expansionen av styrnings implementeringar. Samma vägledning och övningar kan användas för att lägga till den här högre styrnings nivån, men tids inställningen kan behöva påskyndas. I vissa fall kan ett avancerat tillstånd för styrning även krävas under distributionen av de första landnings zonerna.

## <a name="balance-during-manage"></a>Saldo under hantera

IT-affärsmodellen avseende drifts hantering har ständigt ökat under de senaste tio åren. När maskin varu underhållet flyttas ytterligare från det viktiga värdet för viktiga värden, har vyn i Operations Management även Skift ATS. När det gäller att leverera ett affärs värde är Operations Management Teams i konflikt med att balansera inget Ops/Low Ops vs breda investeringar.

**Konkurrerande prioriteringar:**

- Breda investeringar: investeringar på samma sätt som att undvika avbrott, snabb återställning och övervakning i miljön är den traditionella vyn av drift hantering. Den här metoden kan vara kostsam och samtidigt som de stödda produkterna tillhandahålls av moln leverantören.
- Inget Ops/Low Ops: utnyttja molnbaserade drift verktyg för att minimera återkommande och återkommande uppgifter som tidigare levererats av heltids anställda. Genom att minska dessa drifts beroenden i drifts hanterings modellen frigörs dessa anställda till att öka värdet. Den här metoden kan dessutom leda till subpar-åtgärder.

**Minsta omfattning:** Med hanterings metoden kan du upprätta en moln intern, hanterings bas linje utan Ops. Att bekräfta att ingen Ops-bas linje uppfyller alla affärs behov, arbetar med verksamheten för att definiera åtaganden och bättre anpassa investeringar. Expandera bas linjen för att möta vanliga behov för alla arbets belastningar. Aktivera sedan plattforms team eller speciella arbets belastnings team för att underhålla välhanterade lösningar i en väl hanterad miljö.

**Exempel på utökad omfattning:** I de flesta miljöer är en liten procent andel arbets belastningar vars affärs värde motiverar djupgående investeringar i driften. I dessa scenarier kan IT-teamet vilja använda Azures arkitektur granskning och Azure Architecture Framework för att hjälpa djupare drift.

## <a name="balance-during-organize"></a>Saldo under organisera

De konkurrerande prioriteringarna i den här artikeln är reflekterande av IT-enheter för att leverera på affärs behoven för hastighet och flexibilitet. Samma Skift visas i förändringar av organisations scheman (eller V-team strukturer) för att ge bättre stöd för affärs resultat. När IT-ledare återspeglar team strukturer, är två konkurrerande prioriteringar vanliga: centraliserad kontroll vs delegerad kontroll

**Konkurrerande prioriteringar:**

- Centraliserad kontroll: centralt styr drifts modeller fokuserar på centralisering av alla kontroller som krävs för att genomdriva fasta principer. I den här modellen fungerar den som en blockerare för innovation, hastighet och flexibilitet. Det kan dock vara en högre grad av stabilitet, efterlevnad och säkerhet.
- Delegerad kontroll: i den här distribuerade operativ modellen förutsätts att varje DevOps team eller affärs program team tillhandahåller egna kontroller, baserat på de lösningar som krävs för att leverera affärs mål. I den här modellen ger den guardrails för att hjälpa till att hålla teamet på vägen, men minimerar antalet framtvingade tekniska begränsningar när det är möjligt.

**Minsta omfattning:** De flesta organisationer kommer att gå igenom en naturlig uppsättning utvecklingar över tid. Metoden organisera beskriver de vanligaste utvecklings serierna. Den föreslagna vägledningen är för lag för att sträva efter att gå över till ett moln Center med hög expert struktur för att leverera delegerade kontroll metoder.

**Exempel på utökad omfattning:** Det finns många situationer som skulle utlösa behovet av centraliserad kontroll. Krav på efterlevnad av tredje part och temporär säkerhets exponering är två exempel på utlösare för centraliserad kontroll. I sådana fall finns det ofta ett behov av att fastställa begränsade principer och fasta och fasta kontroller. Men för att möjliggöra innovation och införande för att fortsätta, rekommenderar vi att centrala IT-team levererar kontrollerna baserat på allvarlighets grad och känslighet för varje arbets belastning. Att tillhandahålla miljöer med mindre kontroll, men en reducerad omfattning eller risk profil, ger flexibilitet även om kontroll krävs.
