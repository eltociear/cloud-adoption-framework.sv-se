---
title: Mått och indikatorer för konsekvens tolerans för resurs konsekvens
description: Använd ramverket för moln införande för Azure för att kvantifiera affärs risk toleransen som är relaterad till resurs konsekvens.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: def4d8a52dbff95a836549d68595f21d6d1244d8
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80429814"
---
<!-- cSpell:ignore MTBF MTTR -->

# <a name="resource-consistency-metrics-indicators-and-risk-tolerance"></a>Resurs konsekvens statistik, indikatorer och risk tolerans

I den här artikeln får du hjälp med att kvantifiera affärs risk toleransen när det gäller resurs konsekvens. Genom att definiera mått och indikatorer får du hjälp att skapa ett affärs ärende för att göra en investering som förfaller i disciplinen för resurs konsekvens.

## <a name="metrics"></a>Mått

Disciplinen för resurs konsekvens fokuserar på att adressera risker relaterade till drift hantering av moln distributioner. Som en del av din riskanalys vill du samla in data som är relaterade till din IT-verksamhet för att fastställa hur mycket risk du möter, och hur viktig investering i resurs konsekvensen är till dina planerade moln distributioner.

Varje organisation har olika drifts scenarier, men följande objekt visar användbara exempel på mått som du bör samla in när du utvärderar risk tolerans i disciplinen för resurs konsekvens:

- **Moln till gångar.** Totalt antal moln-distribuerade resurser.
- **Otaggade resurser.** Antal resurser utan obligatorisk redovisning, påverkan på verksamheten eller organisatoriska taggar.
- **Underutnyttjade till gångar.** Antal resurser där minnes-, processor-eller nätverks kapaciteten ständigt används.
- **Resurs uttömdning.** Antal resurser där minnes-, processor-eller nätverks kapacitet har förbruk ATS genom belastningen.
- **Resursens ålder.** Tid sedan resursen senast distribuerades eller ändrades.
- **Virtuella datorer i kritiskt tillstånd.** Antal distribuerade virtuella datorer där ett eller flera kritiska problem identifieras som måste åtgärdas för att återställa normala funktioner.
- **Aviseringar efter allvarlighets grad.** Totalt antal aviseringar på en distribuerad till gång, uppdelat efter allvarlighets grad.
- **Nätverks länkar som inte är felfria.** Antal resurser med problem med nätverks anslutningen.
- **Felaktiga tjänst slut punkter.** Antal problem med externa nätverks slut punkter.
- **Hälso incidenter i Cloud Provider service.** Antal avbrott eller prestanda incidenter som orsakas av moln leverantören.
- **Service nivå avtal.** Detta kan omfatta både Microsofts åtaganden för drift tid och anslutning av Azure-tjänster, samt åtaganden som görs av verksamheten till externa och interna kunder.
- **Tjänst tillgänglighet.** Procent andel faktiska drift tid för molnbaserade arbets belastningar jämfört med den förväntade drift tiden.
- **Mål för återställnings tid (RTO).** Den längsta acceptabla tiden som ett program kan vara otillgängligt efter en incident.
- **Återställnings punkt mål (återställnings punkt mål).** Maximal varaktighet för data förlust som är acceptabel under en katastrof. Om du till exempel lagrar data i en enda databas, utan replikering till andra databaser, och säkerhetskopierar varje timme kan du förlora upp till en timme med data.
- **Genomsnittlig tid för återställning (MTTR).** Genomsnittlig tid som krävs för att återställa en komponent efter ett haveri.
- **Genomsnittlig tid mellan haverier (MTBF).** Hur länge en komponent kan förväntas köras mellan avbrott. Det här måttet kan hjälpa dig att beräkna hur ofta en tjänst blir otillgänglig.
- **Säkerhets kopierings hälsa.** Antalet säkerhets kopieringar som aktivt synkroniseras.
- **Återställnings hälsa.** Antalet återställnings åtgärder som har utförts.

## <a name="risk-tolerance-indicators"></a>Risk tolerans indikatorer

Cloud Platforms erbjuder en bas linje uppsättning funktioner som gör det möjligt för distributions grupper att effektivt hantera små distributioner utan ytterligare planering eller processer. Det innebär att små utvecklings-/testnings-eller experiment-eller experiment-arbetsbelastningar som innehåller en relativt liten mängd molnbaserade till gångar representerar låg risk nivå och inte behöver mycket på vägen för en formell resurs konsekvens princip.

Men eftersom storleken på din moln egendom ökar komplexiteten med att hantera dina till gångar blir det betydligt svårare. Med fler till gångar i molnet är möjligheten att identifiera ägarskapet för resurser och kontroll resurser användbart att vara avgörande för att minimera riskerna. Eftersom fler verksamhets kritiska arbets belastningar distribueras till molnet, blir tjänstens drift tid mer kritisk och toleransen för potentiella kostnader för tjänst avbrott minskar snabbt.

I det tidiga skedet av moln införande arbetar du med IT-avdelningen och affärs intressenterna för att identifiera [affärs risker](./business-risks.md) relaterade till resurs konsekvensen och avgör sedan en acceptabel bas linje för risk tolerans. Det här avsnittet av moln implementerings ramverket innehåller exempel, men detaljerade risker och bas linjer för ditt företag eller distributioner kan vara olika.

När du har en bas linje kan du fastställa de lägsta benchmark-värden som representerar en oacceptabel ökning av dina identifierade risker. Dessa riktmärken fungerar som utlösare för när du behöver vidta åtgärder för att åtgärda dessa risker. Nedan följer några exempel på hur drifts mått, till exempel de som beskrivs ovan, kan motivera en ökad investering i disciplinen för resurs konsekvens.

- **Tagga och namngivnings utlösare.** Ett företag med fler än _x_ resurser som saknar obligatorisk taggnings information eller som inte följer namngivnings standarder bör överväga att investera i resurs konsekvens disciplinen för att förfina dessa standarder och säkerställa konsekvent tillämpning av dem på molnbaserade till gångar.
- **Överetablerade resurser utlösare.** Om ett företag har mer än _x%_ av till gångar som regelbundet använder små mängder av sina tillgängliga minnes-, processor-eller nätverks funktioner, föreslås investeringen i disciplinen för resurs konsekvens för att hjälpa till att optimera resursernas användning för dessa objekt.
- **Utlösare av underetablerad resurser.** Om ett företag har mer än _x%_ av till gångar som regelbundet förbrukar de flesta av sina tillgängliga minnes-, processor-eller nätverksfunktioner, föreslås investeringen i disciplinen för resurs konsekvens för att säkerställa att dessa till gångar har de resurser som krävs för att förhindra avbrott i tjänsten.
- **Resurs ålders utlösare.** Ett företag med fler än _x_ resurser som inte har uppdaterats på över _y_ -månader kan dra nytta av investeringar i resurs konsekvens disciplinen som syftar till att säkerställa att aktiva resurser korrigeras och är felfria, samtidigt som du tar bort föråldrade eller outnyttjade till gångar.
- **Utlösare på service nivå avtal.** Ett företag som inte kan uppfylla sina service avtals avtal till sina externa kunder eller interna partner bör investera i distributions accelerations disciplinen för att minska system stillestånds tiden.
- **Utlösare för återställnings tid.** Om ett företag överskrider de tröskelvärden som krävs för återställnings tiden efter ett systemfel, bör det investera i att förbättra dess spridnings-och system design för att minska eller eliminera problem eller påverka enskilda komponenters drift stopp.
- **Hälso utlösare för virtuell dator.** Ett företag som har mer än _x%_ av de virtuella datorer som har ett kritiskt hälso problem bör investera i resurs konsekvens disciplinen för att identifiera problem och förbättra VM-stabiliteten.
- **Nätverks hälso utlösare.** Ett företag som har mer än _x%_ av nätverks under nät eller slut punkter som har anslutnings problem bör investera i resurs konsekvens disciplinen för att identifiera och lösa nätverks problem.
- **Utlösare för säkerhets kopiering.** Ett företag med _x%_ av verksamhets kritiska till gångar utan uppdaterade säkerhets kopior på plats skulle ha nytta av en ökad investering i disciplinen för resurs konsekvens för att säkerställa en konsekvent säkerhets kopierings strategi.
- **Säkerhets kopierings hälso utlösare.** Ett företag som har mer än _x%_ fel i återställnings åtgärder bör investera i resurs konsekvens disciplinen för att identifiera problem med säkerhets kopieringen och se till att viktiga resurser skyddas.

De exakta mått och utlösare som du använder för att mäta risk toleransen och nivån av investeringar i disciplinen för resurs konsekvens är specifika för din organisation, men exemplen ovan bör fungera som en användbar bas för diskussioner i din moln styrning Dela.

## <a name="next-steps"></a>Nästa steg

Använda [mallen för moln hantering](./template.md), dokument mått och tolerans indikatorer som överensstämmer med den aktuella moln implementerings planen.

Granska exempel på resurs konsekvens principer som utgångs punkt för att utveckla principer som åtgärdar specifika affärs risker som överensstämmer med dina moln implementerings planer.

> [!div class="nextstepaction"]
> [Granska exempel principer](./policy-statements.md)
