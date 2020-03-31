---
title: Arbets belastnings åtgärder i moln hantering
description: Förstå en metod för att investera i fortsatta drift av dessa arbets belastningar med hög prioritet för att driva bättre affärs åtaganden.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 92453f3323a2479160bd7bd45e6ef5101c1d9f1b
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80430123"
---
# <a name="workload-operations-in-cloud-management"></a>Arbets belastnings åtgärder i moln hantering

Vissa arbets belastningar är avgörande för att verksamheten ska lyckas. För dessa arbets belastningar är en hanterings bas linje otillräcklig för att uppfylla de affärs åtaganden som krävs för moln hantering. Plattforms åtgärder kan inte ens vara tillräckliga för att möta affärs åtaganden. Den här mycket viktiga del mängden av arbets belastningar kräver en specialiserad fokus på hur arbets belastnings funktionerna och hur de stöds.

I retur kan investeringen i arbets belastnings åtgärder leda till bättre prestanda, minska risken för affärs avbrott och snabbare återställning när systemfel uppstår. Den här artikeln beskriver en metod för att investera i fortsatta drift av dessa arbets belastningar med hög prioritet för att driva bättre affärs åtaganden.

## <a name="when-to-invest-in-workload-operations"></a>När du ska investera i arbets belastnings åtgärder

_Pareto-principen_ (kallas även _regeln 80/20_) anger att 80 procent av effekterna kommer från 20 procent av orsakerna. När IT-portföljer får växa ekologiskt över tid, illustreras den här regeln ofta i en granskning av IT-portföljen. Beroende på vilken påverkan som kräver investering kan orsaken variera, men den allmänna principen är sann:

- 80 procent systemfel tenderar att bli resultatet av 20 procent av vanliga fel eller buggar.
- 80 procent av affärs värde kan komma från 20 procent av arbets belastningarna i en portfölj.
- 80 procent av ansträngningen för att migrera till molnet kommer från 20 procent av de arbets belastningar som flyttas.
- 80 procent av moln hanterings ansträngningarna kommer att stödja 20 procent av tjänst incidenterna eller fel biljetter.
- 80 procent av verksamhets påverkan från ett avbrott kommer att komma från 20 procent av de system som påverkas av avbrottet.

Arbets belastnings åtgärder bör endast tillämpas när moln implementerings strategin, företags resultatet och drifts måtten är bra förstå. Detta är ett paradigm Skift från den klassiska vyn av det. Traditionellt sett antas det att alla arbets belastningar har samma grad av support och nödvändiga liknande prioritets nivåer.

Innan de investerar i djupgående arbets belastnings åtgärder bör både IT och företaget förstå affärs motiveringen och förväntningarna på ökad investering i moln hantering.

## <a name="start-with-the-data"></a>Börja med data

Arbets belastnings åtgärder börjar med en djupgående förståelse för arbets belastnings prestanda och support krav. Innan gruppen investerar i arbets belastnings åtgärder måste den ha omfattande data om arbets belastnings beroenden, program prestanda, databas diagnostik, telemetri för virtuella datorer och incident historik.

Dessa data dirigerar de insikter som driver arbets belastnings åtgärder.

## <a name="continued-observation"></a>Fortsatt observation

Inledande data och pågående telemetri kan hjälpa dig att formulera och testa basreaktionsteorier om prestanda för en arbets belastning. Men pågående arbets belastnings åtgärder rotas i en fortsatt och utökat observation av arbets belastnings prestanda, med stor fokus på program-och data prestanda.

### <a name="test-the-automation"></a>Testa automatiseringen

På program nivå är de första kraven för arbets belastnings åtgärder en investering i djup testning. För alla program som stöds genom arbets belastnings åtgärder bör en testplan upprättas och köras regelbundet för att leverera funktionella och skalade tester i programmen.

Vanlig testning av telemetri kan ge omedelbar verifiering av olika Hypotheses om driften av arbets belastningen. Bättre drift-och arkitektur mönster kan utföras och testas. De resulterande deltarna ger en tydlig effekt analys för att hjälpa fortsatta investeringar.

### <a name="understand-releases"></a>Förstå versioner

En tydlig förståelse av lanserings cykler och lanserings pipelines är ett viktigt element i arbets belastnings åtgärder.

En förståelse för cykler kan förbereda för potentiella avbrott och tillåta teamet att proaktivt adressera eventuella versioner som kan producera en negativ påverkan på verksamheten. Den här förståelsen gör det också möjligt för moln hanterings teamet att samar beta med implementerings team för att kontinuerligt förbättra kvaliteten på produkten och åtgärda eventuella buggar som kan påverka stabiliteten.

En viktig Beskrivning av lanserings pipeliner kan avsevärt förbättra återställnings punkt målet för en arbets belastning. I många fall är den snabbaste och mest exakta sökvägen till återställningen av ett program en versions pipeline. För program lager som bara ändras när en ny version sker kan det vara klokt att investera mer kraftigt i optimering av pipelinen än att återställa programmet från traditionella säkerhets kopierings processer.

Även om en distributions pipeline kan vara den snabbaste sökvägen till återställning, kan det också vara den snabbaste sökvägen till reparation. När ett program har en snabb, effektiv och tillförlitlig versions pipeline, har moln hanterings teamet ett alternativ för att automatisera distributionen till en ny värd som en form av automatiserad reparation.

Det kan finnas många andra snabbare och mer effektiva mekanismer för reparation och återställning. Men när användningen av en befintlig pipeline kan möta affärs åtaganden och få till gång till befintliga DevOps-investeringar, kan den befintliga pipelinen vara ett lämpligt alternativ.

### <a name="clearly-communicate-changes-to-the-workload"></a>Kommunicera tydligt ändringar i arbets belastningen

Att ändra till en arbets belastning är bland de största riskerna med arbets belastnings åtgärder. För arbets belastningar inom arbets belastnings drifts nivån för moln hantering bör moln hanterings teamet noggrant anpassa sig till moln implementerings teamen för att förstå de ändringar som kommer från varje version. Den här investeringen i proaktiv förståelse kommer att ha en direkt, positiv inverkan på drifts stabiliteten.

## <a name="improve-outcomes"></a>Förbättra resultat

Investeringarna data och kommunikation i en arbets belastning ger förslag på förbättringar av pågående åtgärder på något av tre olika områden:

- Teknisk skuld ande lösning
- Automatiserad reparation
- Förbättrad system design

### <a name="technical-debt-resolution"></a>Teknisk skuld ande lösning

De bästa arbets belastnings planerna kräver fortfarande reparationer. När moln hanterings gruppen är ansluten till att förstå implementerings åtgärder och-versioner bör teamet också regelbundet dela reparations krav för att säkerställa att den tekniska skulden och buggar är en kontinuerlig prioritet för dina utvecklings grupper.

### <a name="automated-remediation"></a>Automatiserad reparation

Genom att använda Pareto-principen kan vi säga att 80 procent av negativ inverkan på verksamheten kommer att komma från 20 procent av tjänste incidenterna. När dessa incidenter inte kan åtgärdas i normala utvecklings cykler kan investeringar i reparations automatisering avsevärt minska affärs avbrott.

### <a name="improved-system-design"></a>Förbättrad system design

I fall av teknisk skuld ande lösning och automatiserad åtgärd är systemfel den vanligaste orsaken till de flesta avbrott i systemet. Du kan ha störst påverkan på övergripande arbets belastnings åtgärder genom att följa några design principer:

- **Skalbarhet:** Möjligheten för ett system att hantera ökad belastning.
- **Tillgänglighet:** Den procent andel av tiden som ett system fungerar och fungerar.
- **Återhämtning:** Möjligheten för ett system att återställa efter fel och fortsätta att fungera.
- **Hantering:** Drifts processer som håller ett system som körs i produktion.
- **Säkerhet:** Skydda program och data från hot.

För att förbättra de övergripande åtgärderna ger [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/guide/pillars) en metod för att utvärdera vissa arbets belastningar för att nå dessa pelare. Du kan använda pelaren för både plattforms åtgärder och arbets belastnings åtgärder.

## <a name="next-steps"></a>Nästa steg

Med fullständig förståelse för hanterings metoden i moln implementerings ramverket är du nu väpnade att implementera moln hanterings principer. Information om hur du gör den här metoden i din drift miljö finns i [Cloud Management i ramverket för moln införande](../index.md) i livs cykeln för införande.

> [!div class="nextstepaction"]
> [Använd den här metoden](../index.md)
