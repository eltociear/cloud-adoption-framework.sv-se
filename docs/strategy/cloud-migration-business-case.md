---
title: Utforma en affärsmotivering för molnmigrering
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Att tänka på när du skapar en affärs justering för molnbaserad migrering.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: d545b977a4c98692ba8503d5512b8cb0d0b7dd0d
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224185"
---
# <a name="build-a-business-justification-for-cloud-migration"></a>Utforma en affärsmotivering för molnmigrering

Genom att migrera molnet kan du generera en ny avkastning på investeringen (ROI) från moln omvandlings ansträngningar. Men att utveckla en tydlig affärs motivering med materiella, relevanta kostnader och returer kan vara en komplicerad process. Den här artikeln hjälper dig att tänka på vilka data du behöver för att skapa en finansiell modell som anpassas med molnets migrerings resultat. Först ska vi dispel några myths om migrering av molnet, så att din organisation kan undvika några vanliga misstag.

## <a name="dispelling-cloud-migration-myths"></a>Dispelling Cloud migration myths

**Myten Molnet är alltid billigare.** Det är vanligt att ett Data Center i molnet alltid är billigare än att fungera lokalt. Detta antagande kan vanligt vis vara sant, men det är inte alltid fallet. Ibland är moln drifts kostnaderna högre. Dessa högre kostnader orsakas ofta av dåliga kostnads styrning, feljusterade system arkitekturer, process duplicering, ovanlig-systemkonfigurationer eller högre personalkostnader. Lyckligt vis kan du minska många av de här problemen för att skapa en tidig ROI. Genom att följa rikt linjerna för [att skapa affärs skäl](#building-the-business-justification) kan du identifiera och undvika dessa fel justeringar. Dispelling de andra Myths som beskrivs här kan hjälpa dig.

**Myten Allt ska gå in i molnet.** Vissa affärs drivande faktorer kan i själva verket leda till att du väljer en hybrid lösning. Innan du slutför en affärs modell är det smart att slutföra en första rundad kvantitativ analys, enligt beskrivningen i artiklar om [digital egendom](../digital-estate/5-rs-of-rationalization.md). Mer information om de enskilda kvantitativa driv rutiner som ingår i rationalisering finns i [5 RS-rationalisering](../digital-estate/5-rs-of-rationalization.md). Antingen kommer metoden att använda lätt erhållna inventerings data och en kort kvantitativ analys för att identifiera arbets belastningar eller program som kan leda till högre kostnader i molnet. Dessa metoder kan också identifiera beroenden eller trafik mönster som skulle kräva en hybrid lösning.

**Myten Att spegla min lokala miljö hjälper mig att spara pengar i molnet.** Under planeringen av den digitala fastigheten är den inte av för företag att upptäcka outnyttjad kapacitet på över 50% av den etablerade miljön. Om till gångar är etablerade i molnet för att matcha den aktuella etableringen är det svårt att realisera kostnads besparingarna. Överväg att minska storleken på de distribuerade till gångarna så att de överensstämmer med användnings mönster i stället för att använda mönster.

**Myten Server kostnader driver affärs ärenden för molnbaserad migrering.** Detta antagande är ibland sant. För vissa företag är det viktigt att minska löpande kapital kostnader som är relaterade till servrar. Men det beror på flera faktorer. Företag med en fem års till åtta års uppdaterings cykel är osannolika att se snabba returer vid deras moln migrering. Företag med standardiserade eller framtvingade uppdaterings cykler kan snabbt nå en Bryt punkt. I båda fallen kan andra utgifter vara de finansiella utlösare som motiverar migreringen. Här följer några exempel på kostnader som ofta förbises när företag använder en endast Server-eller endast VM-vy av kostnader:

- Kostnaderna för program vara för virtualisering, servrar och mellanprogram kan vara omfattande. Moln leverantörer eliminerar några av dessa kostnader. Två exempel på en moln leverantör som minskar kostnaderna för virtualisering är [Azure Hybrid-förmån](https://azure.microsoft.com/pricing/hybrid-benefit/#services) och [Azures boknings](https://azure.microsoft.com/reservations) program.
- Affärs förluster som orsakas av avbrott kan snabbt överskrida maskinvaru-eller program varu kostnader. Om det aktuella data centret är instabilt arbetar du med verksamheten för att kvantifiera effekten av avbrott i förhållande till affärs möjlighets kostnader eller faktiska verksamhets kostnader.
- Miljö kostnader kan också vara betydande. För den genomsnittliga amerikanska familjen är en start den största investeringen och den högsta kostnaden i budgeten. Samma sak gäller ofta för data Center. Kostnader för fastighets-, anläggningar-och-verktyg utgör en rättvis del av de lokala kostnaderna. När data Center har dragits tillbaka kan dessa funktioner återanvändas, eller så kan ditt företag eventuellt släppas från dessa kostnader helt och hållet.

**Myten En modell för drifts utgifter är bättre än en kapital utgifts modell.** Som förklaras i artikeln [räkenskaps resultat](./business-outcomes/fiscal-outcomes.md) kan en modell för drifts kostnader vara en bra sak. Men vissa branscher visar drifts utgifter negativt. Här följer några exempel på hur du utlöser en tätt integrerad integrering med ekonomi-och affär senheter om drift utgifts konversationen:

- När ett företag ser kapital till gångar som en driv rutin för företags värdering kan avdrag av kapital kostnader vara ett negativt resultat. Även om det inte är en universell standard visas den här sentiment vanligt vis i detalj handels-, tillverknings-och bygg branschen.
- Ett privat eget kapital företag eller ett företag som söker kapital inflöde kan anse att drifts kostnader ökar som ett negativt resultat.
- Om ett företag fokuserar mycket på att förbättra försäljnings marginalerna eller minska kostnaderna för sålda varor (KSV) kan drifts kostnader vara negativa.

Företag är mer sannolika att se drift kostnader som mer fördelaktig än kapital kostnader. Den här metoden kan till exempel vara väl mottagen av företag som försöker förbättra kassa flödet, minska kapital investeringar eller minska till gångs anläggningar.

Innan du anger en affärs justering som fokuserar på en konvertering från kapitalkostnader till drifts kostnader, bör du förstå vilken som passar din verksamhet bättre. Redovisning och anskaffning kan ofta hjälpa till att justera meddelandet mot finansiella mål.

**Myten Att flytta till molnet är som att vända en växel.** Migreringar är en manuellt intensiv teknisk omvandling. När du utvecklar en affärs justering, särskilt motiveringar som är tids känsliga, bör du tänka på följande aspekter som kan öka tiden det tar att migrera till gångar:

- **Bandbredds begränsningar:** Mängden bandbredd mellan det aktuella data centret och moln leverantören kommer att köra tids linjer under migreringen.
- **Testa tids linjer:** Testa program med verksamheten för att säkerställa beredskap och prestanda kan ta lång tid. Det är viktigt att justera privilegierade användare och testnings processer.
- **Tids linjer för migrering:** Hur lång tid och ansträngning som krävs för att implementera migreringen kan öka kostnaderna och orsaka förseningar. Tilldelning av medarbetare eller avtals slutande partners kan också försena processen. Planen bör redovisas för dessa allokeringar.

Tekniska och kulturella hinder kan göra moln införande långsamt. När tiden är en viktig aspekt av affärs justeringen är den bästa minskningen lämplig. Under planeringen kan två metoder hjälpa till att minska tids linje riskerna:

- Investera tid och energi i förståelse för tekniska antaganden. Även om trycket för att gå snabbt kan vara högt, är det viktigt att kontona för realistiska tids linjer.
- Om kulturella eller andra hinder uppstår har de mer allvarliga effekter än tekniska begränsningar. Moln införande skapar ändringar, vilket ger önskad omvandling. Tyvärr kan man ibland göra en ökad förändring och kan behöva ytterligare support för att kunna anpassas till planen. Identifiera viktiga personer i teamet som är i motsats att ändra och engagera dem tidigt.

För att maximera beredskap och minska riskerna med tids linjen förbereder du bransch intressenter genom att justera affärs värdens och affärs resultaten ordentligt. Hjälp dessa intressenter att förstå de ändringar som kommer att komma med omvandlingen. Var klar och ange realistiska förväntningar från början. När människor eller tekniker saktar ned processen blir det enklare att registrera Executive-support.

## <a name="building-the-business-justification"></a>Skapa affärs justeringen

Följande process definierar en metod för att utveckla affärs justeringen för moln migreringar. Mer information om beräkningar och ekonomiska villkor finns i artikeln om [finansiella modeller](./financial-models.md).

På den högsta nivån är formeln för affärs justering enkel. Men de diskreta data punkterna som krävs för att fylla formeln kan vara svåra att justera. På en grundläggande nivå fokuserar affärs justeringen på avkastningen på investeringen (ROI) som är associerad med den föreslagna tekniska ändringen. Den allmänna formeln för ROI är:

![AVKASTNINGen är lika med (vinst från investering minus kostnad för investering) dividerat med kostnaden för investeringen](../_images/strategy/formula-roi.png)

Vi kan packa upp den här ekvationen för att få en migrering som är speciell för formlerna för indatavärdena på höger sida av ekvationen. I de återstående avsnitten i den här artikeln finns några saker att tänka på när du tar hänsyn till detta.

## <a name="migration-specific-initial-investment"></a>Migrering-bestämd första investering

- Moln leverantörer som Azure-erbjudande kalkylatorer för att beräkna moln investeringar. [Pris Kalkylatorn för Azure](https://azure.microsoft.com/pricing) är ett exempel.
- Vissa moln leverantörer tillhandahåller även kostnads förändrings kalkylatorer. [Kostnaden för total ägande kostnad (TCO) för Azure](https://azure.com/tco) är ett exempel.
- Om du vill ha mer förfinade kostnads strukturer bör du överväga att [Planera en digital fastighets planering](../digital-estate/index.md) .
- Uppskatta kostnaden för migrering.
- Uppskatta kostnaden för förväntade utbildnings möjligheter. [Microsoft Learn](/learn) kan hjälpa till att minska kostnaderna.
- På vissa företag kan den tid som investerats av befintliga personal medlemmar behöva tas med i de ursprungliga kostnaderna. Kontakta ekonomi kontoret om du behöver hjälp.
- Diskutera eventuella ytterligare kostnader eller kostnader för kostnads börda med ekonomi kontoret för validering.

## <a name="migration-specific-revenue-deltas"></a>Migrering – speciella intäkts delta

Den här aspekten är ofta överblickad av grund som skapar en affärs justering för migrering. I vissa områden kan molnet minska kostnaderna. Men det slutliga målet för en transformering är att ge bättre resultat över tid. Ta hänsyn till de efterföljande effekterna för att förstå förbättringar av långsiktiga intäkter. Vilka nya tekniker kommer att vara tillgängliga för ditt företag när migreringen inte kan användas idag? Vilka projekt eller affärs mål blockeras av beroenden i tidigare teknologier? Vilka program är spärrade, väntande stora kapital utgifter för teknik?

När du har funderat på vilka affärs möjligheter som är låsta av molnet kan du arbeta med företaget för att beräkna intäkts ökningar som kan komma från dessa affärs möjligheter.

## <a name="migration-specific-cost-deltas"></a>Migrering – vissa kostnads delta

Beräkna eventuella ändringar av kostnader som kommer från den föreslagna migreringen. I artikeln [finans modeller](./financial-models.md) finns mer information om olika typer av kostnads delta. Moln leverantörer erbjuder ofta verktyg för beräkning av kostnads beräkningar. [Kostnaden för total ägande kostnad (TCO) för Azure](https://azure.com/tco) är ett exempel.

Andra exempel på kostnader som kan minskas med en molnbaserad migrering:

- Data Center terminering eller minskning (miljö kostnader)
- Minskad strömförbrukning (miljö kostnader)
- Rack avslutning (återställning av fysisk till gång)
- Undvikande av maskin varu uppdatering (kostnads snedvridning)
- Undvika förnyelse av program vara (drift kostnads minskning eller kostnads snedvridning)
- Leverantörs konsolidering (drift kostnads minskning och eventuell mjuk kostnads nedsättning)

## <a name="when-roi-results-are-surprising"></a>När ROI-resultat är överraskande

Om ROI för en molnbaserad migrering inte matchar dina förväntningar kanske du vill gå tillbaka till de vanliga myths som anges i början av den här artikeln.

Men det är viktigt att förstå att det inte alltid är möjligt att spara pengar. Vissa program kostar mer att arbeta i molnet än lokalt. Dessa program kan märkbart snedställa resultat i en analys.

När ROI unders tiger 20% bör du överväga en [plan för digital fastighets planering](../digital-estate/index.md) , med särskild uppmärksamhet på [rationalisering](../digital-estate/rationalize.md). Under kvantitativ analys granskar du varje program för att hitta arbets belastningar som skevar resultaten. Det kan vara klokt att ta bort arbets belastningarna från planen. Om användnings data är tillgängliga bör du överväga att minska storleken på de virtuella datorerna så att de matchar användningen.

Om AVKASTNINGen fortfarande är feljusterad kan du söka efter hjälp från din Microsoft-representant eller [engagera en erfaren partner](https://azure.microsoft.com/migration/support).

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Skapa en finans modell för moln omvandling](./financial-models.md)
