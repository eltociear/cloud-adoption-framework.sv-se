---
title: Verksamhets kritiskhet – moln hantering och åtgärder
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Verksamhets kritiskhet – moln hantering och åtgärder
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: be5cc97c7b42eb79f0ec9721376524dc2710e2c4
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683622"
---
# <a name="business-impact-in-cloud-management"></a>Inverkan på verksamheten i moln hantering

Antag det bästa och Förbered dig för det värsta. I IT-hanteringen är det säkert att anta att de arbets belastningar som krävs för att stödja affärs åtgärder kommer att vara tillgängliga och att de kommer att utföras inom överenskomna villkor, baserat på den valda allvarlighets graden. Men för att hantera investeringar är det viktigt att förstå den påverkan som företaget upplever när ett avbrott eller prestanda försämring sker. Den här prioriteten illustreras i kurvan som illustrerar potentiella affärs avbrott i specifika arbets belastningar för att påverka driften av drift störningar i en relativ värde skala.

![Påverkan av affärs avbrott](../../_images/manage/time-value-impact.png)

För att skapa en rättvis grund för jämförelsen av olika arbets belastningar i en portfölj, föreslås ett tids/värde-mått. Tid/värde-måttet avbildar den skadliga effekten av ett avbrott i arbets belastningen. I allmänhet registreras denna påverkan som en direkt förlust av intäkter eller rörelse intäkter under en typisk avbrotts period. Mer specifikt, beräkna mängden förlorad intäkt för en tidsenhet. Det vanligaste värdet för tid/värde är "påverkan per timme", som mäter förlust av drift inkomster per timme för avbrott.

Det finns några metoder som kan användas för att beräkna påverkan. Något av alternativen i följande avsnitt kan utnyttjas med liknande resultat. Det är viktigt att använda samma metod för varje arbets belastning när du beräknar skyddade förluster i en portfölj.

## <a name="start-with-estimates"></a>Börja med uppskattningar

Nuvarande drift modeller kan göra det svårt att fastställa en korrekt påverkan. Lyckligt vis behöver några system en mycket exakt förlust beräkning. I föregående steg: klassificera kritiskhet föreslog du att alla arbets belastningar börjar med standardvärdet "medelhög allvarlighets grad". Mellanliggande arbets belastningar får vanligt vis en standard nivå för hantering av support med relativt låg drifts kostnad. Endast när en arbets belastning kräver ytterligare resurser för drift hantering skulle det krävas en korrekt ekonomisk påverkan.

För alla standardiserade arbets belastningar fungerar affärs påverkan som prioriterad variabel vid återställning av system under ett avbrott. Utanför dessa begränsade situationer kommer affärs påverkan att skapa liten till ingen ändring i drifts hanterings upplevelsen. 

## <a name="calculating-time"></a>Beräknar tid

Beroende på arbets Belastningens natur kan förluster beräknas annorlunda. För transaktions system med hög hastighet, som en real tids handels plattform, kan det uppstå förluster per millisekund. Mindre system som används ofta, som lön, kan inte användas varje timme. Oavsett om användnings frekvensen är hög eller låg är det viktigt att normalisera tids variabeln när du beräknar ekonomisk påverkan.

## <a name="calculating-total-impact"></a>Beräknar total påverkan

När ytterligare hanterings investeringar önskas är det viktigt att affärs effekten är mer exakt. På följande punkter kan du beräkna förluster, i den mest exakta (från mest exakta till minst exakta):

- **Justerade förluster:** Om företaget har drabbats av en stor förlust händelse tidigare, t. ex. en orkan eller annan natur katastrof kan en anspråks justering ha beräknat faktiska förluster under avbrottet. De här beräkningarna baseras på försäkrings bransch standarder för förlust beräkning och riskhantering. Genom att använda justerade förluster som det totala antalet förluster inom en bestämd tidsram kan det leda till hög noggrannhets projektion.

- **Historiska förluster:** Om den lokala miljön har lidit tidigare avbrott på grund av instabilitet i infrastrukturen, kan det vara lite svårare att beräkna förluster. Men-formelrna kan fortfarande användas internt. Om du vill beräkna historiska förlora, jämför du delta i försäljning, brutto intäkter och drifts kostnader över tre tids ramar: före, under och efter avbrott. Genom att undersöka dessa delta kan du identifiera korrekt förlorar om inga andra data är tillgängliga.

- **Slutför förlust beräkning:** Om inga historiska data är tillgängliga kan ett jämförelse förlust värde härledas. I den här modellen fastställer du den genomsnittliga brutto intäkten per timme för affär senheten. Under förutsättning att ett fullständigt system avbrott motsvarar 100% förlust av intäkter är ett dåligt antagande när du vill undvika investeringar i projekt förlust. Men det kan användas som en grov grund för att jämföra förlust påverkar och prioritera investeringar.

Innan du gör antaganden om förlust beräkningar arbetar du med din ekonomi avdelning för att fastställa den bästa metoden för att beräkna potentiella förluster som är kopplade till ett arbets belastnings avbrott.

## <a name="calculating-workload-impact"></a>Beräknar arbets belastnings påverkan

När historiska data används för att beräkna förluster kan det finnas tillräckligt med information för att tydligt avgöra påverkan av varje arbets belastning på dessa förluster. Den här utvärderingen är den plats där samarbetet med verksamheten är absolut viktigt. När en sammanlagd påverkan har beräknats måste påverkan vara för varje arbets belastning. Den distributionen av påverkan bör komma från affärs intressenterna, som bör enas om den relativa och ackumulerade påverkan av varje arbets belastning. Dessutom bör teamet be om feedback från affärs chefer för att validera justering. Slut resultatet är tyvärr lika delar av känslo och expert kunskaper om ämnen. Betydelsen av den här övningen är att den representerar logik och övertygelse för de affärs intressenter som bör ha ett par i budgetallokeringen.

## <a name="using-the-template"></a>Använda mallen

Följande steg gäller för läsare som använder [arbets boken för OPS-hantering](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) för att planera för moln hantering.

1. Varje arbets belastning i "exempel" eller "Rensa mall" bör uppdateras av verksamheten med "tids-/värde påverkan" för varje arbets belastning. Som standard representerar "tid/värde-påverkan" den beräknade förlusten per timme som är kopplad till ett avbrott i arbets belastningen.

## <a name="next-steps"></a>Nästa steg

När påverkan har definierats [kan åtagandena justeras](./commitment.md).

> [!div class="nextstepaction"]
> [Justera hanterings åtaganden med verksamheten](./commitment.md)
