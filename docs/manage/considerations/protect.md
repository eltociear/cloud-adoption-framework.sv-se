---
title: Skydda och återställa moln hantering och åtgärder
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Skydda och återställa moln hantering och åtgärder
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 356d6c463e97553cb56d132c4f94e812a5b1c656
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73752791"
---
# <a name="protect-and-recover-in-cloud-management"></a>Skydda och återställa i moln hantering

Efter att de har uppfyllt kraven för [inventering och synlighet](./inventory.md) och [operativa](./operational-compliance.md)krav kan moln hanterings team förutse och förbereda för en potentiell arbets belastnings störning. När de planerar för moln hantering måste teamen börja med ett antagande om att något kommer att Miss förväntas.

Ingen teknisk lösning kan konsekvent erbjuda ett SLA för 100 procents drift tid. Lösningar med de mest redundanta arkitekturerna är anspråk på att leverera "sex nior" eller 99,9999 procent drift tid. Men även om en "sex nior"-lösning går nere i 31,6 sekunder under ett och samma år. Sadly är det sällsynt för en lösning att motivera en stor, kontinuerlig drifts investering som krävs för att uppnå "sex nior" av drift tid.

Förberedelse för ett avbrott gör det möjligt för teamet att upptäcka fel snart och återställa snabbare. Fokus för den här disciplinen finns på de steg som kommer direkt efter ett system som Miss lyckas. Hur skyddar du arbets belastningar så att de kan återställas snabbt när ett avbrott uppstår?

## <a name="translate-protection-and-recovery-conversations"></a>Översätt skydds-och återställnings konversationer

Arbets belastningarna som Power Business-åtgärder består av program, data, virtuella datorer och andra till gångar. Var och en av dessa till gångar kan kräva en annan metod för skydd och återställning. Den viktigaste aspekten av denna disciplin är att upprätta ett konsekvent åtagande inom hanterings bas linjen, vilket kan ge en start punkt under affärs diskussioner.

Som minst bör varje till gång som har stöd för en viss arbets belastning ha en bas linje med ett tydligt åtagande för hastighet på återställnings tiden (återställnings mål, eller RTO) och risken för data förlust (återställnings punkt mål eller återställnings punkter).

### <a name="recovery-time-objectives-rto"></a>Mål för återställnings tid (RTO)

När haveriet inträffar är ett återställnings tids mål den tid det tar att återställa systemet till dess för katastrof tillstånd. För varje arbets belastning omfattar det den tid som krävs för att återställa minimi kraven för de virtuella datorerna och apparna. Den innehåller också den tid som krävs för att återställa de data som krävs av programmen.

I affärs villkor representerar RTO den tid som affärs processen kommer att vara ur drift. För verksamhets kritiska arbets belastningar bör den här variabeln vara relativt låg, vilket gör det möjligt för affärs processerna att återupptas snabbt. För arbets belastningar med lägre prioritet kanske en standard nivå av RTO inte har en märkbar inverkan på företagets prestanda.

Hanterings bas linjen bör upprätta en standard RTO för arbets belastningar som inte är verksamhets kritiska. Företaget kan sedan använda denna bas linje som ett sätt att motivera ytterligare investeringar i återställnings tider.

### <a name="recovery-point-objectives-rpo"></a>Återställnings punkt mål (återställnings punkt mål)

I de flesta moln hanterings system samlas data regelbundet in och lagras i en viss form av data skydd. Senaste gången som data samlades in kallas en återställnings punkt. När ett system Miss lyckas kan det bara återställas till den senaste återställnings punkten.

Om ett system har ett återställnings punkt mål som mäts i timmar eller dagar skulle ett systemfel leda till förlust av data för dessa timmar eller dagar mellan den senaste återställnings punkten och avbrottet. En engångs transaktion skulle teoretiskt leda till förlust av alla transaktioner under den dag som ledde till problemet.

För verksamhets kritiska system kan en återställning som mäts på minuter eller sekunder vara mer lämplig att använda för att undvika förlust av intäkter. Men en kortare återställning leder vanligt vis till en ökning av de totala hanterings kostnaderna.

För att minimera kostnaderna bör en hanterings bas linje fokusera på den längsta acceptabla återställningen. Moln hanterings teamet kan sedan öka återställningen av vissa plattformar eller arbets belastningar, vilket skulle motivera mer investering.

## <a name="protect-and-recover-workloads"></a>Skydda och återställa arbets belastningar

De flesta av arbets belastningarna i en IT-miljö stöder en enskild affärs-eller teknisk process. System som inte har en system påverkan på verksamheten garanterar inte ofta de ökade investeringar som krävs för att återställa snabbt eller minimera data förlust. Genom att upprätta en bas linje kan företaget tydligt förstå vilken nivå av återställnings support som kan erbjudas till en konsekvent, hanterbar pris punkt. Den här förståelsen hjälper affärs intressenter att utvärdera värdet av en ökad investering i återställningen.

För de flesta moln hanterings team ger en förbättrad bas linje med specifika återställnings-/RTO-åtaganden för olika till gångar den mest fördelaktig sökvägen till ömsesidiga affärs åtaganden. I följande avsnitt beskrivs några vanliga utökade bas linjer som ger verksamheten möjlighet att enkelt lägga till skydds-och återställnings funktioner genom en upprepnings bar process.

### <a name="protect-and-recover-data"></a>Skydda och återställa data

Data är utan tvekan den värdefulla till gången i den digitala ekonomin. Möjligheten att skydda och återställa data på ett mer effektivt sätt är den vanligaste utökade bas linjen. För de data som ger en produktions arbets belastning kan förlust av data direkt likställas med förlust av intäkter eller förlust av lönsamhet. Vi uppmuntrar vanligt vis moln hanterings grupper att erbjuda en nivå av utökad hanterings bas linje som stöder gemensamma data plattformar.

Innan moln hanterings grupper implementerar plattforms åtgärder är det vanligt att de har stöd för förbättrade åtgärder för en plattform som en tjänst (PaaS) data plattform. Det är till exempel enkelt för ett moln hanterings team att upprätthålla en högre frekvens av säkerhets kopierings-eller multiregion-replikering för Azure SQL Database-eller Azure Cosmos DB-lösningar. På så sätt kan utvecklings teamet enkelt förbättra återställnings möjligheterna genom att använda sina dataplattformar.

Mer information om den här processen finns i [plattforms åtgärds disciplin](./platform.md).

### <a name="protect-and-recover-vms"></a>Skydda och återställa virtuella datorer

De flesta arbets belastningar har vissa beroenden på virtuella datorer, vilka är värdar för olika aspekter av lösningen. För att arbets belastningen ska stödja en affärs process efter ett systemfel måste ett antal virtuella datorer återställas snabbt.

Varje minut på de virtuella datorerna kan leda till förlust av intäkter eller lägre lönsamhet. När den virtuella datorns stillestånds tid har direkt inverkan på verksamhetens räkenskaps prestanda är RTO mycket viktigt. Virtuella datorer kan återställas snabbare med hjälp av replikering till en sekundär plats och automatisk återställning, en modell som kallas snabb och varm återställnings modell. Med det högsta läget för återställning kan virtuella datorer replikeras till en helt funktionell, sekundär plats. Den här dyrare metoden kallas för hög tillgänglighet, eller frekvent frekvent återställnings modell.

Var och en av de föregående modellerna minskar RTO, vilket resulterar i en snabbare återställning av affärs processens funktioner. Varje modell leder dock också till betydligt ökad moln hanterings kostnader.

Mer information om den här processen finns i [disciplin för arbets belastnings åtgärder](./workload.md).

## <a name="next-steps"></a>Nästa steg

När den här hanterings bas linje komponenten är uppfylld kan teamet gå vidare för att undvika avbrott i [plattforms åtgärder](./platform.md) och [arbets belastnings åtgärder](./workload.md).

> [!div class="nextstepaction"]
> [Plattforms åtgärder](./platform.md)
> [arbets belastnings åtgärder](./workload.md)
