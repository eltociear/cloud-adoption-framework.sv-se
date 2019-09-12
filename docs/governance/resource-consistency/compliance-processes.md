---
title: Processer för efterlevnad av resurs konsekvens principer
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Processer för efterlevnad av resurs konsekvens principer
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 7abe4e31c9688c3f6621054e656d029de8362640
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70824267"
---
# <a name="resource-consistency-policy-compliance-processes"></a>Processer för efterlevnad av resurs konsekvens principer

Den här artikeln beskriver en metod för att följa regler som styr [resurs konsekvensen](./index.md). Effektiv styrning av resurs konsekvens i molnet börjar med återkommande manuella processer som har utformats för att identifiera Operational-ineffektivhet, förbättra hanteringen av distribuerade resurser och se till att verksamhets kritiska arbets belastningar har minimala störningar. Dessa manuella processer kompletteras med övervakning, automatisering och verktyg för att minska kostnaderna för styrningen och tillåta snabbare svar på princip avvikelsen.

## <a name="planning-review-and-reporting-processes"></a>Planering, granskning och rapportering av processer

Cloud Platforms tillhandahåller en uppsättning hanterings verktyg och funktioner som du kan använda för att organisera, etablera, skala och minimera stillestånds tid. Genom att använda dessa verktyg för att effektivt strukturera och hantera moln distributioner på ett sätt som gör det nödvändigt att åtgärda potentiella risker måste du tänka igenom processer och principer förutom att nära samar beta med IT-avdelningen och affärs intressenter.

Följande är en uppsättning exempel processer som ofta ingår i disciplinen för resurs konsekvens. Använd de här exemplen som en start punkt när du planerar de processer som gör att du kan fortsätta att uppdatera principen för resurs konsekvens baserat på affärs förändringar och feedback från utvecklingen och IT-teamen som du kan använda för att sätta igång vägledningen.

**Inledande riskbedömning och planering:** Som en del av ditt första antagande av resurs konsekvens disciplinen kan du identifiera de viktiga affärs riskerna och toleranserna som rör drift och IT-hantering. Använd den här informationen för att diskutera tekniska risker med medlemmar i dina IT-team och arbets belastnings ägare för att utveckla en bas linje uppsättning av resurs konsekvens principer som är utformade för att åtgärda dessa risker, och att etablera din inledande styrnings strategi.

**Distributions planering:** Innan du distribuerar en till gång kan du utföra en granskning för att identifiera eventuella nya drift risker. Upprätta resurs krav och förväntade demand-mönster och identifiera skalbarhets behov och potentiella möjligheter till optimering av användning. Se också till att säkerhets kopierings-och återställnings planer är på plats.

**Distributions testning:** Som en del av distributionen kommer moln styrnings teamet, i samarbete med dina moln drifts grupper, att vara ansvarig för att granska distributionen för att verifiera efterlevnad av resursens konsekvens policy.

**Årlig planering:** På årsbasis bör du utföra en övergripande granskning av strategin för resurs konsekvens. Utforska framtida företags expansions planer eller prioriteringar och uppdatera moln implementerings strategier för att identifiera potentiell risk ökning eller andra kommande resurs konsekvens behov. Använd även den här tiden för att granska de senaste bästa praxisen för moln resurs konsekvens och integrera dem i dina principer och gransknings processer.

**Kvartals vis granskning och planering:** En gång i kvartalet utför en granskning av drift data och incident rapporter för att identifiera eventuella ändringar som krävs i principen för resurs konsekvens. Som en del av den här processen granskar du förändringar i resursanvändningen och prestanda för att identifiera till gångar som kräver ökad eller minskning i resursallokeringen och identifierar eventuella arbets belastningar eller till gångar som är kandidater för pensionering.

Den här planerings processen är också en lämplig tidpunkt för att utvärdera det aktuella medlemskapet i moln styrnings teamet för kunskaps luckor som rör nya eller föränderliga principer och risker relaterade till resurs konsekvens som en disciplin. Bjud in relevant IT-personal för att delta i granskningar och planering som antingen tillfälliga tekniska rådgivare eller permanenta medlemmar i teamet.

**Utbildning och utbildning:** En gång i månaden kan du erbjuda utbildning för att se till att IT-personal och utvecklare är uppdaterade på de senaste resurs kraven och vägledningen för resurs konsekvens. Som en del av den här processen granskar och uppdaterar du all dokumentation eller andra utbildnings resurser för att se till att de är synkroniserade med de senaste företags princip uppgifterna.

**Granskningar av månads granskning och rapportering:** Varje månad bör du utföra en granskning på alla moln distributioner för att säkerställa att deras fortsatta anpassningar med principen för resurs konsekvens. Granska relaterade aktiviteter med IT-personal och identifiera eventuella kompatibilitetsproblem som inte redan hanteras som en del av den pågående övervaknings-och verk ställande processen. Resultatet av den här granskningen är en rapport för moln strategi teamet och varje moln antagande team för att kommunicera övergripande prestanda och leda till policy. Rapporten lagras också för granskning och juridiskt syfte.

## <a name="ongoing-monitoring-processes"></a>Pågående övervaknings processer

Avgöra om din strategi för resurs konsekvens styrningen lyckas beror på insyn i den aktuella och den tidigare statusen för din moln infrastruktur. Utan möjlighet att analysera relevanta mått och data i moln miljöns hälsa och aktivitet kan du inte identifiera ändringar i riskerna eller identifiera överträdelser av dina risk toleranser. De löpande styrnings processer som beskrivs ovan kräver kvalitets data för att säkerställa att principen kan ändras för att optimera moln resursanvändningen och förbättra prestandan för molnbaserade arbets belastningar.

Se till att IT-teamen har implementerat automatiska övervaknings system för din moln infrastruktur som samlar in relevanta loggdata som du behöver för att utvärdera risker. Se till att övervaka dessa system och se till att det går att upptäcka och minska risken för eventuella policy överträdelser och se till att din övervaknings strategi är i linje med dina operativa behov.

## <a name="violation-triggers-and-enforcement-actions"></a>Fel utlösare och tvingande åtgärder

Eftersom regelefterlevnad för resurs konsekvens kan leda till kritiska avbrott i tjänsten eller avsevärda kostnader för att överskrida riskerna, bör moln styrnings teamet ha insyn i incidenter som inte uppfyller kraven. Se till att IT-personalen har tydliga eskalering sökvägar för att rapportera de här problemen till de styrnings grupp medlemmar som är bäst lämpade att identifiera och kontrol lera att princip problemen begränsas när de upptäcks.

När överträdelser identifieras bör du vidta åtgärder för att justera med principen så snart som möjligt. IT-teamet kan automatisera de flesta fel utlösare med hjälp av verktygen som beskrivs i [resurs konsekvens verktygskedjan för Azure](toolchain.md).

Följande utlösare och tvingande åtgärder innehåller exempel som du kan referera till när du planerar att använda övervaknings data för att lösa princip överträdelser:

- **Överetablerad resurs har identifierats.** Resurser som har identifierats med mindre än 60% processor-eller minnes kapacitet ska automatiskt skala ned eller avetablera resurser för att minska kostnaderna.
- **Underetablerad resurs har identifierats.** Resurser som har identifierats med mer än 80% processor-eller minnes kapacitet bör automatiskt skala upp eller att etablering av ytterligare resurser för att ge ytterligare kapacitet.
- **Ingen Taggad resurs skapas.** Alla begär Anden om att skapa en resurs utan obligatoriska meta-taggar kommer att avvisas automatiskt.
- **Kritiskt resurs avbrott identifierat.** IT-personal meddelas på alla identifierade avbrott i verksamhets kritiska avbrott. Om avbrott inte kan matchas omedelbart, kommer personalen att eskalera problemet och meddela arbets belastnings ägare och moln styrnings teamet. Moln styrnings teamet spårar problemet fram till lösning och uppdaterings vägledning om princip revision är nödvändig för att förhindra framtida incidenter.

## <a name="next-steps"></a>Nästa steg

Använd [mallen för moln hantering](./template.md)för att dokumentera de processer och utlösare som överensstämmer med den aktuella moln implementerings planen.

Vägledning om hur du kör moln hanterings principer i justering med implementerings planer finns i artikeln om disciplin förbättringar.

> [!div class="nextstepaction"]
> [Disciplin förbättring av resurs konsekvens](./discipline-improvement.md)
