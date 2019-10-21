---
title: Skydda och återställa moln hantering och åtgärder
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Skydda och återställa moln hantering och åtgärder
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: ab00e80297dc85aa028550faef8ff1a66f098c22
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557523"
---
# <a name="protect-and-recover-in-cloud-management"></a>Skydda och återställa i moln hantering

När kraven för [inventering och synlighet](./inventory.md) och [operativa](./operational-compliance.md) krav har uppfyllts kan moln hanterings team se fram emot och förbereda sig för att få en arbets belastnings risk. När du planerar för moln hantering måste teamet börja med ett antagande om att något kommer att Miss förväntas.

Ingen teknisk lösning kan konsekvent erbjuda ett service avtal på 100% drift tid. Lösningar med de mest redundanta arkitekturerna är anspråk på att leverera "sex nior" eller 99,9999% drift tid. Men även om en "sex nior"-lösning går nere i 31,6 sekunder under ett och samma år. Sadly-lösningar garanterar sällan den stora, kontinuerliga operativa investeringen som krävs för att uppnå "sex nior" av drift tid.

Förberedelsen för ett avbrott gör att teamet kan upptäcka fel tidigare och återställa snabbare. Fokus för den här disciplinen är på nästa steg som inträffar efter det att systemet Miss lyckas. Hur skyddar du arbets belastningar så att de kan återställas snabbt när ett avbrott inträffar.

## <a name="translating-protection-and-recovery-conversations"></a>Översättning av skydds-och återställnings konversationer

Arbets belastningarna som är verksamhets krävande för verksamheten består av program, data, virtuella datorer och andra till gångar. Var och en av dessa till gångar kan kräva en annan metod för skydd och återställning. Den viktigaste aspekten av denna disciplin är att skapa ett konsekvent åtagande inom hanterings bas linjen, för att tillhandahålla en start punkt under affärs diskussioner.

Varje till gång som har stöd för en viss arbets belastning bör minst ha en grund metod med ett tydligt åtagande för hastighet på återställningen (återställnings tid eller RTO) och risken för data förlust (återställnings punkt mål eller återställnings punkter).

### <a name="recovery-time-objectives-rto"></a>Mål för återställnings tid (RTO)

När en olycka inträffar är RTO den tid det tar att återställa ett visst system till för katastrof tillstånd. För varje arbets belastning omfattar det den tid som krävs för att återställa minimi kraven för de virtuella datorerna och apparna. Den innehåller också den tid som krävs för att återställa data som krävs av programmen.

I affärs villkor representerar RTO den tid som affärs processen kommer att vara ur drift. För verksamhets kritiska arbets belastningar bör den här variabeln vara relativt låg, vilket gör det möjligt för affärs processerna att återupptas snabbt. För arbets belastningar med lägre prioritet kanske en standard nivå av RTO inte har en märkbar inverkan på företagets prestanda.

Hanterings bas linjen bör upprätta ett standard mål för återställnings tid för arbets belastningar som inte är verksamhets kritiska. Företaget kan sedan använda denna bas linje som ett sätt att motivera ytterligare investeringar i återställnings tider.

### <a name="recovery-point-objectives-rpo"></a>Återställnings punkt mål (återställnings punkt mål)

I de flesta moln hanterings system samlas data regelbundet in och lagras i en viss form av data skydd. Senaste gången som data samlades in kallas en återställnings punkt. När ett system Miss lyckas kan det bara återställas till den senaste återställnings punkten.

Om ett system har ett återställnings punkt mål mätt i timmar eller dagar skulle ett systemfel leda till förlust av data för dessa timmar eller dagar mellan den senaste återställnings punkten och avbrottet. En nyställning på 1 dag skulle leda till att alla transaktioner på den dag som ledde till ett haveri bryts.

För verksamhets kritiska system kan en återställning på några minuter eller sekunder vara mer lämplig för att undvika förlust av intäkter. Men en kortare återställning leder vanligt vis till en ökning av de totala hanterings kostnaderna.

En hanterings bas linje bör fokusera på den längsta acceptabla återställningen för att minimera kostnaderna. Moln hanterings teamet kan sedan öka återställningen av vissa plattformar eller arbets belastningar, vilket skulle motivera mer investering.

## <a name="protect-and-recover-workloads"></a>Skydda och återställa arbets belastningar

De flesta av arbets belastningarna i en IT-miljö stöder en mycket liten affärs-eller teknisk process. System som inte har en system påverkan på verksamheten garanterar inte ofta de ökade investeringar som krävs för att återställa data snabbt eller minimera data förlust. Genom att upprätta en bas linje kan företaget tydligt förstå vilken nivå av återställnings support som kan erbjudas till en konsekvent, hanterbar pris punkt. Detta hjälper affärs intressenterna att utvärdera värdet av en ökad investering i återställningen.

För de flesta moln hanterings team ger en förbättrad bas linje med specifika återställnings-/RTO-åtaganden för olika till gångar den mest fördelaktig sökvägen till ömsesidiga affärs åtaganden. I följande avsnitt beskrivs några vanliga utökade bas linjer som ger verksamheten möjlighet att enkelt lägga till skydds-och återställnings funktioner genom en upprepnings bar process.

### <a name="protect-and-recover-data"></a>Skydda och återställa data

Data är utan tvekan den värdefulla till gången i den digitala ekonomin. Möjligheten att skydda och återställa data på ett mer effektivt sätt är den vanligaste utökade bas linjen. För de data som ger en produktions arbets belastning kan förlust av data direkt likställas med förlust av intäkter eller förlust av lönsamhet. Det rekommenderas vanligt vis att moln hanterings team erbjuder en nivå av utökad hanterings bas linje som stöder gemensamma data plattformar.

Innan du implementerar plattforms åtgärder är det vanligt att moln hanterings grupper har stöd för bättre drift av plattform som en tjänst data plattform. Det är till exempel enkelt för ett moln hanterings team att genomdriva en högre frekvens av säkerhets kopiering eller multi-region-replikering för Azure SQL-eller Cosmo DB-lösningar. På så sätt kan utvecklings teamet enkelt förbättra nyproduktionen genom att helt enkelt ställa av sina data plattformar.

Den här processen kommer att tas i detalj igen i [plattforms åtgärds disciplinen](./platform.md).

### <a name="protect-and-recover-vms"></a>Skydda och återställa virtuella datorer

De flesta arbets belastningar har vissa beroenden på virtuella datorer. De virtuella datorerna är värdar för olika aspekter av lösningen. För att arbets belastningen ska stödja en affärs process efter ett systemfel måste ett antal virtuella datorer återställas snabbt.

Varje minut på de virtuella datorerna kan likställas med förlorade intäkter eller lägre lönsamhet. När stillestånds tiden på VM: ar har direkt påverkan på verksamhetens räkenskaps prestanda är RTO mycket viktigt. Virtuella datorer kan återställas snabbare med replikering till en sekundär plats och automatisk återställning, men den här modellen kallas snabb och varm återställnings modell. Med det högsta läget för återställning kan virtuella datorer replikeras till en helt funktionell, sekundär plats. Den här dyrare metoden kallas en hög tillgänglighets modell eller snabb återställnings modell.

Var och en av modellerna ovan minskar återställnings tiden, vilket resulterar i en snabbare återställning av affärs processens funktioner. Varje modell leder dock också till betydligt ökad moln hanterings kostnader.

Den här processen kommer att flyttas igen i detalj, i [disciplinen för arbets belastnings åtgärder](./workload.md).

## <a name="next-steps"></a>Nästa steg

När den här hanterings bas linje komponenten är uppfylld kan teamet gå vidare för att undvika avbrott med [plattforms åtgärder](./platform.md) och [arbets belastnings åtgärder](./workload.md).

> [!div class="nextstepaction"]
> [Plattforms åtgärder](./platform.md) 
> [arbets belastnings åtgärder](./workload.md)
