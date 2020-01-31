---
title: Exempel på finansiella resultat
description: Exempel på finansiella resultat
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: 43cd9dd0d155849c8ed5dda277252e445507f6d8
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806857"
---
# <a name="examples-of-fiscal-outcomes"></a>Exempel på finansiella resultat

På den högsta nivån består räkenskaps samtal av tre grundläggande koncept:

- **Intäkter:** Kommer mer pengar att komma in i företaget som ett resultat av försäljningen av varor eller tjänster.
- **Kostnad:** Kommer mindre pengar att ägnas åt att skapa, marknadsföra, sälja eller leverera varor eller tjänster.
- **Vinst:** Även om de är ovanliga kan vissa transformeringar både öka intäkterna och minska kostnaderna. Detta är ett vinst resultat.

I resten av den här artikeln förklaras dessa räkenskaps resultat i samband med en moln omvandling.

> [!NOTE]
> Följande exempel är hypotetiska och bör inte anses vara en garanti för returer när du inför en moln strategi.

## <a name="revenue-outcomes"></a>Intäkts resultat

### <a name="new-revenue-streams"></a>Nya intäkts strömmar

Molnet kan hjälpa dig att skapa möjligheter att leverera nya produkter till kunder eller leverera befintliga produkter på ett nytt sätt. Nya intäkts strömmar är innovativa, företags och spännande för många personer i företags världen. Nya intäkts strömmar är också känslig för haveri och betraktas som många företag som ska vara höga risker. När intäkts-relaterade resultat föreslås, kommer det sannolikt att vara motstånd. Om du vill lägga till trovärdighet för dessa resultat kan du samar beta med en affärs ledare som är en beprövad innovatör. Validering av intäkts strömmen tidigt i processen hjälper till att undvika hindren från företaget.

- **Exempel:** Ett företag har Sälj böcker i över ett hundra år. En anställd i företaget inser att innehållet kan levereras elektroniskt. Medarbetaren skapar en enhet som kan säljas i pärmen, vilket gör att samma böcker kan hämtas direkt, med hjälp av $X i ny bok försäljning.

### <a name="revenue-increases"></a>Ökad intäkt

Med global skala och digital räckvidd kan molnet hjälpa företag att öka intäkter från befintliga intäkts strömmar. Den här typen av resultat kommer ofta från en justering med försäljnings-eller marknads ledarskap.

- **Exempel:** Ett företag som säljer widgetar kunde sälja fler widgetar, om säljarna säkert kan komma åt företagets digitala katalog och lager nivåer. Dessa data finns tyvärr bara i företagets ERP-system, som endast kan nås via en nätverksansluten enhet. Genom att skapa en tjänst fasad till ett gränssnitt med ERP och exponera katalog listan och icke-känsliga lager nivåer till ett program i molnet, skulle kunderna kunna få till gång till de data som de behöver, samtidigt som kunden är på plats. Att utöka lokala Active Directory att använda Azure Active Directory (Azure AD) och integrera rollbaserad åtkomst till programmet gör det möjligt för företaget att se till att data förblir säkra. Det här enkla projektet kan påverka intäkterna från en befintlig produkt linje med _x%_ .

### <a name="profit-increases"></a>Vinst ökningar

Sällan medför en enda insats samtidigt intäkter och lägre kostnader. Men när det sker kan du justera uttrycken från en eller flera av intäkterna med en eller flera av de kostnads resultat som behövs för att förmedla det önskade resultatet.

## <a name="cost-outcomes"></a>Kostnads resultat

### <a name="cost-reduction"></a>Kostnads minskning

Med molnbaserad data behandling kan du minska kapital kostnader för maskin-och program vara, konfigurera Data Center, köra Data Center på plats och så vidare. Kostnaderna för rack servrar, Round-of-ingångs elektricitet för ström och kylning, och IT-experter för att hantera infrastrukturen lägger upp snabbt. Om du stänger ett Data Center kan det minska kapital utgifts åtagandet. Detta kallas vanligt vis för att "komma ut från data Center Business". Kostnads nedsättning mäts vanligt vis i kronor i den aktuella budgeten, vilket kan omfatta en till fem år beroende på hur ekonomi chefen hanterar ekonomin.

- **Exempel #1:** Ett företags data Center förbrukar en stor del av den årliga IT-budgeten. DET väljer att genomföra en molnbaserad migrering och över gångar i data centret till infrastruktur som en tjänst (IaaS) lösningar, vilket skapar en kostnads nedsättning på tre år.
- **Exempel #2:** Ett Holding bolag förvärvade nyligen ett nytt företag. I anskaffningen anger villkoren att den nya entiteten ska tas bort från de aktuella data centren inom sex månader. Om du inte gör det kommer det att resultera i en fin på 1 000 000 USD per månad till företaget. Att flytta de digitala resurserna till molnet i en molnbaserad migrering kan göra det möjligt för en snabbt avställning av de gamla till gångarna.
- **Exempel #3:** Ett inkomst skatte företag som betjänar konsumenterna har 70 procent av sina årliga intäkter under de tre första månaderna av året. Resten av året är dess stora IT-investeringar relativt vilande. En molnbaserad migrering kan göra det möjligt att distribuera beräknings-/värd kapaciteten som krävs för dessa tre månader. Under de återstående nio månaderna skulle IaaS-kostnaderna minska avsevärt genom att minska beräknings utrymmet.

### <a name="example-coverdell"></a>Exempel: Coverdell

Coverdell moderniserar sin infrastruktur för att driva in besparingar av kostnader med Azure. Coverdell beslut om att investera i Azure och för att få en enhets nätverk för webbplatser, program, data och infrastruktur i den här miljön, ledde till mer kostnads besparingar än företaget skulle ha förväntat sig. Migreringen till en Azure-miljö eliminerar 54 000 USD i månads kostnader för samlokaliserings tjänster. Med företagets nya, Förenade infrastruktur, förväntas Coverdell att spara en beräknad 1 000 000 USD under de kommande två till tre åren.

> "Att få åtkomst till Azure Technology stack öppnar dörren för vissa skalbara, lättanvända och hög tillgängliga lösningar som är kostnads effektiva. Detta gör att våra arkitekter kan vara mycket mer kreativa med de lösningar de erbjuder. "  
> Ryan Sorensen  
> Direktör för program utveckling och företags arkitektur  
> Coverdell

### <a name="cost-avoidance"></a>Kostnads snedvridning

Att avsluta ett Data Center kan också ge kostnads undvikade kostnader genom att förhindra framtida uppdaterings cykler. En uppdaterings cykel är en process för att köpa ny maskin-och program vara för att ersätta åldrande lokala system. I Azure underhålls och uppdateras maskin vara och operativ system regelbundet, korrigeras och uppdateras utan extra kostnad för kunderna. Detta gör att en ekonomi chef kan ta bort planerade framtida utgifter från långsiktiga finansiella prognoser. Kostnads skatteundandragande mäts i dollar. Det skiljer sig från kostnads minskning, som i allmänhet fokuserar på en framtida budget som ännu inte har godkänts fullständigt.

- **Exempel:** Ett företags data Center är upp för en låne förnyelse på sex månader. Data centret har varit i tjänst i åtta år. För fyra år sedan har alla servrar uppdaterats och virtualiserats, vilket kostar företaget miljon tals dollar. Nästa år planerar företaget att uppdatera maskin varan och program varan igen. Genom att migrera till gångarna i data centret som en del av en molnbaserad migrering skulle du kunna undvika kostnads snedvridning genom att ta bort den planerade uppdateringen från nästa års prognostiserade budget. Det kan också medföra kostnads nedsättning genom att minska eller eliminera fastighets leasing kostnader.

### <a name="capital-expenses-vs-operating-expenses"></a>Kapital kostnader jämfört med drifts kostnader

Innan du diskuterar kostnads resultat är det viktigt att förstå de två primära kostnads alternativen: kapital kostnader och drifts kostnader.

Följande villkor hjälper dig att förstå skillnaderna mellan kapital utgifter och drifts kostnader under affärs diskussioner om en omvandlings resa.

- **Kapitalet** är det belopp och de till gångar som ägs av en verksamhet för att bidra till ett särskilt ändamål, till exempel att öka Server kapaciteten eller skapa ett program.
- **Kapital utgifter** genererar förmåner under en lång period. Dessa utgifter är vanligt vis icke-återkommande och resulterar i förvärv av permanent till gångar. Att skapa ett program kan kvalificeras som kapital utgifter.
- **Drifts kostnader** är kontinuerliga kostnader för att göra affärer. Användning av moln tjänster i en modell där du betalar per användning kan kvalificeras som drifts kostnader.
- **Till gångar** är ekonomiska resurser som kan ägas eller kontrol leras för att producera värde. Servrar, data sjöar och program kan betraktas som till gångar.
- **Avskrivning** är en minskning av värdet för en till gång över tid. Avskrivningen är mer relevant för kapital kostnaden jämfört med en konversation om drifts kostnader, så att kostnaden för en till gång fördelas över de perioder som de används i. Om du till exempel skapar ett program i år men det förväntas ha en genomsnittlig hållbarhets tid på fem år (till exempel de flesta kommersiella appar), skulle kostnaden för dev-teamet och nödvändiga verktyg som krävs för att skapa och distribuera kodbasen att skrivas av jämnt över fem årtal.
- **Värdering** är processen att uppskatta hur mycket ett företag är värt. I de flesta branscher baseras värderingen på företagets möjlighet att generera intäkter och vinster, samtidigt som du respekterar de drifts kostnader som krävs för att skapa de varor som utgör intäkterna. I vissa branscher, till exempel detalj handel, eller i vissa typer av transaktioner, t. ex. privat egendom, till gångar och avskrivning kan en stor del av företagets värderingar spelas upp.

Det är ofta ett säkert val som flera chefer, inklusive chefs chef, den bästa användningen av kapitalet för att växa företaget i önskad riktning. Att ge informations gruppen ett sätt att konvertera Contentious för kapitalutgifter till tydliga ansvar för drifts kostnader kan vara ett attraktivt resultat. I många branscher söker ekonomi cheferna (ekonomi chefer) aktivt på sätt som bättre kopplar skatte ansvars kostnaderna till kostnaden för sålda varor.

Innan du associerar en omvandlings resa med den här typen av kapital kontra konvertering av drifts kostnader är det klokt att möta medlemmarna i ekonomi-eller informations chefs teamen för att se vilken kostnads struktur som företaget föredrar. I vissa organisationer är det mycket *oönskat* att minska kapital utgifterna till förmån för drifts kostnader. Som tidigare nämnts visas den här metoden ibland i detalj handels-, företags-och privata aktie bolag som placerar högre värde på traditionella till gångs redovisnings modeller, vilket innebär ett litet värde på IP. Den visas också i organisationer som hade negativ erfarenhet när de har förflyttat IT-personal eller andra funktioner tidigare.

Om en modell för drifts kostnader är önskvärd kan följande exempel vara ett livskraftigt affärs resultat:

- **Exempel:** Företagets data Center skriver för närvarande till _x USD_ per år under de kommande tre åren. Vi förväntas kräva ytterligare _y-USD_ för att uppdatera maskin varan nästa år. Vi kan omvandla kapital utgifterna till en modell för drifts kostnader till en jämn pris på _ö USD_ per månad, vilket ger bättre hantering av och ansvar för drifts kostnaderna för teknik.

## <a name="next-steps"></a>Nästa steg

Lär dig mer om [smidiga resultat](./agility-outcomes.md).

> [!div class="nextstepaction"]
> [Smidiga resultat](./agility-outcomes.md)
