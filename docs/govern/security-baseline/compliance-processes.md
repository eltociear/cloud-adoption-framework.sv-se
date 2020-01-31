---
title: Principer för regelefterlevnad för säkerhets bas linjen
description: Principer för regelefterlevnad för säkerhets bas linjen
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: b725a4867ec7e55f6b9d53cdba31c0874d61c80c
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808931"
---
# <a name="security-baseline-policy-compliance-processes"></a>Principer för regelefterlevnad för säkerhets bas linjen

Den här artikeln beskriver en metod för att följa policyer som styr [säkerhets bas linjen](./index.md). Effektiv styrning av moln säkerhet börjar med återkommande manuella processer som har utformats för att identifiera sårbarheter och införa principer för att åtgärda dessa säkerhets risker. Detta kräver en regelbunden medverkan av moln styrnings teamet och intresserade affärs-och IT-intressenter för att granska och uppdatera principen och säkerställa efterlevnaden av policyn. Dessutom kan många pågående övervaknings-och verk ställnings processer automatiseras eller kompletteras med verktyg för att minska kostnaderna för styrning och tillåta snabbare svar på princip avvikelse.

## <a name="planning-review-and-reporting-processes"></a>Planering, granskning och rapportering av processer

De bästa säkerhets bas linje verktygen i molnet är bara lika bra som de processer och principer som de stöder. Följande är en uppsättning exempel processer som ofta ingår i säkerhets bas linje disciplinen. Använd de här exemplen som utgångs punkt när du planerar de processer som gör att du kan fortsätta att uppdatera säkerhets principer baserat på affärs förändringar och feedback från säkerhets-och IT-teamen som du kan använda för att sätta styrnings vägledning i praktiken.

**Inledande riskbedömning och planering:** Som en del av ditt första antagande av säkerhets bas linje disciplin, identifierar du viktiga affärs risker och toleranser relaterade till moln säkerhet. Använd den här informationen för att diskutera tekniska risker med medlemmar i dina IT-och säkerhets team och utveckla en bas linje uppsättning med säkerhets principer för att minimera riskerna för att skapa din första styrnings strategi.

**Distributions planering:** Innan du distribuerar en arbets belastning eller till gång utför du en säkerhets granskning för att identifiera eventuella nya risker och se till att alla krav för åtkomst och data säkerhets principer uppfylls.

**Distributions testning:** Som en del av distributions processen för alla arbets belastningar och till gångar kommer moln styrnings teamet i samarbete med företagets säkerhets team att kunna granska distributionen för att kontrol lera efterlevnaden av säkerhets principer.

**Årlig planering:** På årsbasis bör du utföra en övergripande granskning av strategin för säkerhets bas linjen. Utforska framtida företags prioriteringar och uppdaterade moln införande strategier för att identifiera potentiell risk ökning och andra nya säkerhets behov. Du kan också använda den här tiden för att granska de senaste metod tipsen för säkerhets bas linjer och integrera dem i principerna och gransknings processerna.

**Kvartals vis granskning och planering:** En gång i kvartalet utför en granskning av säkerhets gransknings data och incident rapporter för att identifiera eventuella ändringar som krävs i säkerhets principen. Som en del av den här processen granskar du det aktuella cybersäkerhet-landskapet för att proaktivt förutse nya hot och uppdatera principen efter behov. När granskningen är klar justerar du design vägledningen med den uppdaterade principen.

Den här planerings processen är också en lång tid att utvärdera det aktuella medlemskapet i moln styrnings teamet för kunskaps luckor som rör nya eller föränderliga principer och risker relaterade till säkerhet. Bjud in relevant IT-personal för att delta i granskningar och planering som antingen tillfälliga tekniska rådgivare eller permanenta medlemmar i teamet.

**Utbildning och utbildning:** En gång i månaden kan du erbjuda utbildning för att se till att IT-personal och utvecklare är uppdaterade på de senaste säkerhets princip kraven. Som en del av den här processen kan du granska och uppdatera dokumentation, vägledning eller andra utbildnings resurser för att se till att de är synkroniserade med de senaste företags princip uttrycken.

**Granskningar av månads granskning och rapportering:** Varje månad bör du utföra en granskning på alla moln distributioner för att säkerställa att de fortsätter att vara i konflikt med säkerhets principen. Granska säkerhetsrelaterade aktiviteter med IT-personal och identifiera eventuella kompatibilitetsproblem som inte redan hanteras som en del av den pågående övervaknings-och tvångs processen. Resultatet av den här granskningen är en rapport för moln strategi teamet och varje moln antagande team för att kommunicera den övergripande efterlevnaden av principen. Rapporten lagras också för granskning och juridiskt syfte.

## <a name="ongoing-monitoring-processes"></a>Pågående övervaknings processer

Avgöra om din strategi för säkerhets styrningen lyckas beror på insyn i den aktuella och den tidigare statusen för din moln infrastruktur. Utan möjlighet att analysera relevanta mått och data för moln resursernas säkerhets hälsa och aktivitet kan du inte identifiera ändringar i riskerna eller identifiera överträdelser av dina risk toleranser. De löpande styrnings processer som beskrivs ovan kräver kvalitets data för att säkerställa att principen kan ändras för att bättre skydda infrastrukturen mot att ändra hot och säkerhets krav.

Se till att dina säkerhets-och IT-team har implementerat automatiska övervaknings system för din moln infrastruktur som samlar in relevanta loggdata som du behöver för att utvärdera risken. Var proaktivt i övervakningen av dessa system för att säkerställa att det går att identifiera och åtgärda eventuella policy överträdelser, och se till att din övervaknings strategi är i linje med säkerhets behoven.

## <a name="violation-triggers-and-enforcement-actions"></a>Fel utlösare och tvingande åtgärder

Eftersom inkompatibilitet i säkerhet kan leda till kritiska risker och data exponering och störningar i tjänsten, bör moln styrnings teamet ha insyn i allvarliga princip överträdelser. Se till att IT-personalen har tydliga eskalering sökvägar för rapportering av säkerhets problem till styrnings grupps medlemmar som är bäst lämpade att identifiera och kontrol lera att princip problemen begränsas.

När överträdelser identifieras bör du vidta åtgärder för att justera med principen så snart som möjligt. IT-teamet kan automatisera de flesta fel utlösare med hjälp av verktygen som beskrivs i [säkerhets bas linjen verktygskedjan för Azure](./toolchain.md).

Följande utlösare och tvingande åtgärder innehåller exempel som du kan referera till när du planerar att använda övervaknings data för att lösa princip överträdelser:

- **Ökning av attacker har upptäckts.** Om en resurs upplever en 25% ökning av Brute Force eller DDoS-attacker kan du diskutera med IT-säkerhetspersonalen och arbets belastnings ägaren för att fastställa lösningar. Spåra problem-och uppdaterings vägledning om princip revision är nödvändig för att förhindra framtida incidenter.
- **Oklassificerade data har identifierats.** Alla data källor utan en lämplig sekretess-, säkerhets-eller affärs påverkans klassificering har extern åtkomst nekade tills klassificeringen tillämpas av data ägaren och lämplig nivå för data skydd tillämpas.
- **Ett säkerhets hälso problem har identifierats.** Inaktivera åtkomst till virtuella datorer som har känd åtkomst eller sårbarheter för skadlig kod identifierade tills lämpliga korrigeringar eller säkerhets program kan installeras. Uppdatera princip vägledning för att identifiera eventuella nyligen identifierade hot.
- **Ett nätverks problem har identifierats.** Åtkomst till alla resurser som inte uttryckligen tillåts av nätverks åtkomst principerna bör utlösa en avisering till IT-säkerhetspersonalen och relevant arbets belastnings ägare. Spåra problem-och uppdaterings vägledning om princip revision krävs för att minimera framtida incidenter.

## <a name="next-steps"></a>Nästa steg

Använd [mallen för moln hantering](./template.md)för att dokumentera de processer och utlösare som överensstämmer med den aktuella moln implementerings planen.

Vägledning om hur du kör moln hanterings principer i justering med implementerings planer finns i artikeln om disciplin förbättringar.

> [!div class="nextstepaction"]
> [Förbättringar av säkerhets bas linje disciplin](./discipline-improvement.md)
