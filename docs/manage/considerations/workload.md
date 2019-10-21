---
title: Arbets belastnings åtgärder – moln hantering och åtgärder
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Arbets belastnings åtgärder – moln hantering och åtgärder
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: f3b554f2453ffa825302680f3f0e4546f41cb3c7
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558030"
---
# <a name="workload-operations-in-cloud-management"></a>Arbets belastnings åtgärder i moln hantering

Vissa arbets belastningar är avgörande för att verksamheten ska lyckas. För dessa arbets belastningar räcker det inte med en hanterings bas linje för att uppfylla de affärs åtaganden som krävs för moln hantering. Plattforms åtgärder kan inte ens vara tillräckliga för att möta affärs åtaganden. Den här mycket viktiga del mängden av arbets belastningar kräver en specialiserad fokus på hur arbets belastnings funktionerna och hur de stöds.

I retur kan investeringen i arbets belastnings åtgärder leda till bättre prestanda, minska risken för affärs avbrott och snabbare återställning när systemfel uppstår. Den här artikeln beskriver en metod för att investera i fortsatta drift av dessa arbets belastningar med hög prioritet för att driva bättre affärs åtaganden.

## <a name="when-to-invest-in-workload-operations"></a>När du ska investera i arbets belastnings åtgärder

Pareto-princip (kallas även regeln 80/20) anger att 80% av effekterna kommer från 20% av orsakerna. När IT-portföljer får växa ekologiskt över tid, kan den här regeln ofta ses i en granskning av IT-portföljen. Beroende på vilken inverkan som kräver investering kan orsaken variera, men principen allmänt gäller:

- 80% av system felen tenderar att bli resultatet av 20% av de vanliga felen eller buggar
- 80% av affärs värde kan komma från 20% av arbets belastningarna i en portfölj
- 80% av ansträngningen att migrera till molnet kommer från 20% av de arbets belastningar som flyttas
- 80% av moln hanterings ansträngningarna kommer att stödja 20% av tjänst incidenterna eller fel biljetter
- 80% av affärs påverkan från avbrott kommer att komma från 20% av systemen som påverkas av ett avbrott

Arbets belastnings åtgärder bör endast tillämpas när moln implementerings strategin, affärs resultat och drifts mått är bra förstå. Detta är ett paradigm Skift från den klassiska vyn av det. Traditionellt sett antas det att alla arbets belastningar har samma grad av support och nödvändiga liknande prioritets nivåer.

Innan du investerar i djupgående arbets belastnings åtgärder bör både IT-avdelningen och verksamheten förstå affärs motiveringen och förväntningarna på ökad investering i moln hantering.

## <a name="start-with-the-data"></a>Börja med data

Arbets belastnings åtgärder börjar med en djupgående förståelse för arbets belastnings prestanda och support krav. Innan du investerar i arbets belastnings åtgärder måste teamet ha omfattande data om: arbets belastnings beroenden, program prestanda, databas diagnostik, telemetri för virtuella datorer och incident historik.

Dessa data dirigerar de insikter som driver arbets belastnings åtgärder.

## <a name="continued-observation"></a>Fortsatt observation

Inledande data och pågående telemetri kan hjälpa till att formulera och testa basreaktionsteorier om prestanda för en arbets belastning. Men pågående arbets belastnings åtgärder rotas i en fortsatt och utökat observation av arbets belastnings prestanda, med stor fokus på program-och data prestanda.

### <a name="testing-automation"></a>Testa automatisering

På program nivå är de första kraven för arbets belastnings åtgärder en investering i djup testning. För alla program som stöds genom arbets belastnings åtgärder bör en test plan upprättas och utföras regelbundet för att leverera funktionell och skala testningen i programmen.

Vanlig testning av telemetri ger omedelbar validering av olika Hypotheses om driften av arbets belastningen. Att förbättra operativa och arkitektur mönster kan utföras och testas, delta i dessa resultat ger tydliga konsekvens analyser för att hjälpa fortsatta investeringar.

### <a name="understand-releases"></a>Förstå versioner

Tydliga förståelsen av versions cykler och lanserings pipelines är ett viktigt element i arbets belastnings åtgärder.

En förståelse för cykler kan förbereda för potentiella avbrott och tillåta teamet att proaktivt adressera alla versioner som kan producera en skadlig påverkan på verksamheten. Den här förståelsen gör det också möjligt för moln hanterings teamet att samar beta med implementerings team för att kontinuerligt förbättra kvaliteten på produkten och adressera buggar som kan påverka stabiliteten.

En viktig Beskrivning av lanserings pipeliner kan avsevärt förbättra RTO av en arbets belastning. I många fall är den snabbaste och mest exakta sökvägen till återställningen av ett program en versions pipeline. För program lager som bara ändras när en ny version sker kan det vara klokt att investera mer kraftigt i optimering av pipelinen, än att återställa programmet från traditionella säkerhets kopierings processer.

Även om en distributions pipeline kan vara den snabbaste sökvägen till återställning, kan det också vara den snabbaste sökvägen till reparation. När ett program har en snabb, effektiv och tillförlitlig versions pipeline, har moln hanterings teamet ett alternativ för att automatisera distributionen till en ny värd som en form av automatiserad reparation.

Det kan finnas många andra snabbare och mer effektiva mekanismer för reparation och återställning. Men när användningen av en befintlig pipeline kan möta affärs åtaganden och få till gång till befintliga DevOps-investeringar, kan det vara ett alternativ som är lämpligt.

### <a name="clearly-communicate-changes-to-the-workload"></a>Kommunicera tydligt ändringar i arbets belastningen

Att ändra till en arbets belastning är bland de största riskerna med arbets belastnings åtgärder. För arbets belastningar inom arbets belastnings drifts nivån för moln hantering bör moln hanterings teamet vara noggrant justerade med moln implementerings teamen för att förstå ändringar som kommer från varje version. Den här investeringen i proaktiv förståelse kommer att ha direkt påverkan på drifts stabiliteten.

## <a name="improve-outcomes"></a>Förbättra resultat

Pågående åtgärder förbättras vanligt vis på ett av två sätt. Investeringarna data och kommunikation i en arbets belastning ger förslag på förbättringar av en av två sökvägar: automatiserad reparation eller förbättrad system design

### <a name="technical-debt-resolution"></a>Teknisk skuld ande lösning

De bästa drift planerna för arbets belastningen kräver fortfarande reparationer. När moln hanterings gruppen är ansluten till att förstå implementerings åtgärder och-versioner, bör du regelbundet dela reparations kraven för att säkerställa att teknisk skuld och buggar är en kontinuerlig prioritet för utvecklings grupper.

### <a name="automate-remediation"></a>Automatisera reparationer

Om du använder Pareto-principen kommer 80% av negativ inverkan på verksamheten troligen från 20% av tjänste incidenterna. När dessa incidenter inte kan åtgärdas i normala utvecklings cykler kan investeringar i reparations automatisering avsevärt minska affärs avbrott.

### <a name="improved-system-design"></a>Förbättrad system design

I båda fallen (teknisk skuldsättnings lösning eller automatiserad åtgärd) är system fel den vanligaste orsaken till de flesta avbrott i systemet. Att följa några design principer kan ha störst påverkan på övergripande arbets belastnings åtgärder.

1. Skalbarhet: möjligheten för ett system att hantera ökad belastning.
2. Tillgänglighet: den andel av tiden som ett system är funktionellt och fungerar.
3. Återhämtning: möjligheten för ett system att återställa efter fel och fortsätta att fungera.
4. Hantering: drifts processer som håller ett system som körs i produktion.
5. Säkerhet: skydda program och data från hot.

[Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/guide/pillars) innehåller en metod för att utvärdera vissa arbets belastningar för att nå dessa pelare, i syfte att förbättra den övergripande verksamheten. Dessa pelare kan användas för både plattforms åtgärder och arbets belastnings åtgärder.

## <a name="next-steps"></a>Nästa steg

Med fullständig förståelse för hanterings metoden i moln implementerings ramverket är du nu väpnade att implementera moln hanterings principer. Mer information om hur du gör den här metoden i din drift miljö finns i [landnings sidan för](../index.md) implementerings livs cykelns hanterings fas.

> [!div class="nextstepaction"]
> [Använd den här metoden](../index.md)
