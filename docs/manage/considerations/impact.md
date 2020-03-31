---
title: Inverkan på verksamheten i moln hantering
description: Använd ramverket för moln införande för Azure för att lära dig hur du kan fastställa och förstå vilken effekt som uppstår eller prestanda försämringen kan ha på din verksamhet.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 3e7c74a1d2afa880a0bdec5215b2237e8261ec79
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80426362"
---
# <a name="business-impact-in-cloud-management"></a>Inverkan på verksamheten i moln hantering

Antag det bästa och Förbered dig för det värsta. I IT-hanteringen är det säkert att anta att de arbets belastningar som krävs för att stödja affärs åtgärder är tillgängliga och att de kommer att utföras inom överenskomna begränsningar, baserat på den valda allvarlighets graden. Men för att hantera investeringar är det viktigt att förstå hur verksamheten påverkar verksamheten när ett avbrott eller prestanda försämring sker. Den här prioriteten illustreras i följande diagram, som mappar potentiella affärs avbrott för specifika arbets belastningar till påverkan av drift störningar i en relativ värde skala.

![Påverkan av affärs avbrott](../../_images/manage/time-value-impact.png)

För att skapa en rättvis grund för jämförelsen av olika arbets belastningar i en portfölj, föreslås ett tids värdes mått. Tid/värde-måttet avbildar den skadliga effekten av ett avbrott i arbets belastningen. I allmänhet registreras denna påverkan som en direkt förlust av intäkter eller rörelse intäkter under en typisk avbrotts period. Mer specifikt beräknar det mängden förlorad intäkt för en tidsenhet. Det vanligaste värdet för tid/värde är *påverkan per timme*, som mäter förlust av drift intäkt per timme för avbrott.

Några metoder kan användas för att beräkna påverkan. Du kan använda något av alternativen i följande avsnitt för att uppnå liknande resultat. Det är viktigt att använda samma metod för varje arbets belastning när du beräknar skyddade förluster i en portfölj.

## <a name="start-with-estimates"></a>Börja med uppskattningar

Nuvarande drift modeller kan göra det svårt att fastställa en korrekt påverkan. Lyckligt vis behöver några system en mycket exakt förlust beräkning. I föregående steg, *klassificera kritiskhet*, föreslog vi att du startar alla arbets belastningar med ett standardvärde av *medelhög allvarlighets grad*. Mellanliggande arbets belastningar får vanligt vis en standard nivå för hantering av support med en relativt låg inverkan på drift kostnaden. Endast när en arbets belastning kräver ytterligare drift hanterings resurser kan du behöva en korrekt ekonomisk påverkan.

För alla standardiserade arbets belastningar fungerar företags påverkan som en prioriterings variabel när du återställer system under ett avbrott. Utanför dessa begränsade situationer skapar företags påverkan liten till ingen ändring i drifts hanterings upplevelsen.

## <a name="calculate-time"></a>Beräkna tid

Beroende på arbets Belastningens natur kan du beräkna förluster på olika sätt. För högpresterande transaktions system, till exempel en real tids handels plattform, kan förluster per millisekund vara betydande. Mindre system som används ofta, till exempel lön, kan inte användas varje timme. Oavsett om användnings frekvensen är hög eller låg är det viktigt att normalisera tids variabeln när du beräknar ekonomisk påverkan.

## <a name="calculate-total-impact"></a>Beräkna den totala påverkan

När du vill överväga ytterligare hanterings investeringar är det viktigt att affärs effekten är mer exakt. Följande tre metoder för att beräkna förluster beställs från de mest exakta till minst exakta:

- **Justerade förluster:** Om ditt företag har drabbats av en stor förlust händelse tidigare, till exempel en orkan eller annan natur katastrof kan en anspråks justering ha beräknat faktiska förluster under avbrottet. De här beräkningarna baseras på försäkrings bransch standarder för förlust beräkning och riskhantering. Genom att använda justerade förluster som det totala antalet förluster inom en bestämd tidsram kan det leda till hög noggrannhets projektion.

- **Historiska förluster:** Om din lokala miljö har lidit tidigare från avbrott till följd av infrastruktur instabilitet, kan det vara en bit svårare att beräkna förluster. Men du kan fortfarande använda de justerings formler som används internt. Om du vill beräkna historiska förluster kan du jämföra delta i försäljning, brutto intäkter och drifts kostnader över tre tids ramar: före, under och efter avbrott. Genom att undersöka dessa delta kan du identifiera korrekta förluster när inga andra data är tillgängliga.

- **Slutför förlust beräkning:** Om inga historiska data är tillgängliga kan du härleda ett värde för jämför ande förlust. I den här modellen fastställer du den genomsnittliga brutto intäkten per timme för affär senheten. När du är klar med att undvika investeringar i förlust, är det inte rimligt att anta att ett fullständigt system avbrott motsvarar 100 procent förlust av intäkter. Men du kan använda detta antagande som en grov grund för att jämföra förlust påverkar och prioritera investeringar.

Innan du gör vissa antaganden om potentiella förluster som är kopplade till arbets belastnings avbrott, är det en bra idé att arbeta med ekonomi avdelningen för att fastställa den bästa metoden för sådana beräkningar.

## <a name="calculate-workload-impact"></a>Beräkna arbets belastnings påverkan

När du beräknar förluster genom att använda historiska data kan du ha tillräckligt med information för att tydligt avgöra bidraget för varje arbets belastning till dessa förluster. Om du utför den här utvärderingen är partnerskap i verksamheten absolut viktiga. När den totala påverkan har beräknats måste påverkan vara tilldelad för varje arbets belastning. Den distributionen av påverkan bör komma från affärs intressenterna, som bör enas om den relativa och ackumulerade påverkan av varje arbets belastning. Därför bör ditt team be om feedback från affärs chefer för att validera justering. Sådan feedback är ofta detsamma som känslo och ämnes expert kunskaper. Det är viktigt att den här övningen representerar logik och övertygelse för de affärs intressenter som bör ha ett par i budgetallokeringen.

## <a name="use-the-template"></a>Använd mallen

Om du använder [arbets boken för Operations Management](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) för att planera för moln hantering kan du göra följande:

- Varje företag bör uppdatera varje arbets belastning i *exemplet* eller en *ren mall* med *tids-och värde påverkan* för varje arbets belastning. Som standard representerar *tid/värde-påverkan* de beräknade förluster per timme som associeras med ett avbrott i arbets belastningen.

## <a name="next-steps"></a>Nästa steg

När företaget har definierat påverkan kan du [Justera åtagandena](./commitment.md).

> [!div class="nextstepaction"]
> [Justera hanterings åtaganden med verksamheten](./commitment.md)
