---
title: Principer för regelefterlevnad för Cost Management
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Principer för regelefterlevnad för Cost Management
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 27d60d6b330bb1e651b68f4f7fa92509941f36ba
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026613"
---
# <a name="cost-management-policy-compliance-processes"></a>Principer för regelefterlevnad för Cost Management

Den här artikeln beskriver en metod för att skapa processer som har stöd för en [Cost Management](./index.md) styrnings disciplin. Effektiv styrning av moln kostnader börjar med återkommande manuella processer som har utformats för att stödja policy efterlevnad. Detta kräver regelbunden medverkan av moln styrnings teamet och intresserade affärs intressenter för att granska och uppdatera principen och säkerställa efterlevnad av principer. Dessutom kan många pågående övervaknings-och verk ställnings processer automatiseras eller kompletteras med verktyg för att minska kostnaderna för styrning och tillåta snabbare svar på princip avvikelse.

## <a name="planning-review-and-reporting-processes"></a>Planering, granskning och rapportering av processer

De bästa Cost Management verktygen i molnet är bara lika bra som de processer och principer som de stöder. Följande är en uppsättning exempel processer som ofta ingår i Cost Management disciplin. Använd de här exemplen som utgångs punkt när du planerar de processer som gör att du kan fortsätta att uppdatera kostnads policyn baserat på affärs förändringar och feedback från affärs teamen, beroende på kostnads styrnings vägledning.

**Inledande riskbedömning och planering:** Som en del av ditt första antagande av Cost Management-disciplinen kan du identifiera de viktiga affärs riskerna och toleranserna som rör moln kostnader. Använd den här informationen för att diskutera budget-och kostnads relaterade risker med medlemmar i dina affärs team och utveckla en grundläggande uppsättning principer för att minska riskerna med att skapa din första styrnings strategi.

**Distributions planering:** Innan du distribuerar en till gång ska du upprätta en prognosad budget baserat på förväntad molnbaserad allokering. Se till att information om ägarskap och redovisning för distributionen dokumenteras.

**Årlig planering:** Utför en upplyft analys på alla distribuerade och distribuerade till gångar årligen. Anpassa budgetar efter affär senheter, avdelningar, team och andra lämpliga avdelningar för att få en självbetjänings införande. Se till att chefen för varje fakturerings enhet är medveten om budgeten och hur du spårar utgifter.

Detta är den tid det tar att göra ett åtagande eller för att maximera rabatten. Det är klokt att justera årlig budget med moln leverantörens räkenskapsår till ytterligare intjänade rabatt alternativ på årets slut.

**Kvartals vis planering:** I varje kvartal bör du granska budgetar med varje fakturerings enhets ansvarig för att justera prognos och faktiska utgifter. Om det finns ändringar i planen eller oväntade utgifts mönster, justera och allokera om budgeten.

Den här kvartals planerings processen är också en lämplig tid att utvärdera det aktuella medlemskapet i moln styrnings teamet för kunskaps luckor som rör aktuella eller framtida affärs planer. Bjud in relevanta personal-och arbets belastnings ägare för att delta i granskningar och planering som antingen tillfälliga rådgivare eller permanenta medlemmar i ditt team.

**Utbildning och utbildning:** I en månad kan du erbjuda utbildning för att se till att verksamheten och IT-personalen är uppdaterade med de senaste Cost Management princip kraven. Som en del av den här processen kan du granska och uppdatera dokumentation, vägledning eller andra utbildnings resurser för att se till att de är synkroniserade med de senaste företags princip uttrycken.

**Månatlig rapportering:** Månads vis kan du rapportera faktiska utgifter mot prognos. Meddela fakturerings ledare om oväntade avvikelser.

Dessa grundläggande processer hjälper till att justera utgifterna och upprätta en grund för Cost Management disciplinen.

## <a name="ongoing-monitoring-processes"></a>Pågående övervaknings processer

En lyckad Cost Management styrnings strategi är beroende av insyn i tidigare, aktuella och planerade framtida molnbaserade utgifter. Utan möjlighet att analysera relevanta mått och data för dina befintliga kostnader kan du inte identifiera ändringar i riskerna eller identifiera överträdelser av dina risk toleranser. De löpande styrnings processer som beskrivs ovan kräver kvalitets data för att säkerställa att principen kan ändras för att bättre skydda infrastrukturen mot ändring av affärs krav och moln användning.

Se till att IT-teamen har implementerat automatiserade system för övervakning av dina moln utgifter och användning för oplanerade avvikelser från förväntade kostnader. Upprätta rapporterings-och aviserings system för att säkerställa snabb sökning och minskning av eventuella princip överträdelser.

## <a name="compliance-violation-triggers-and-enforcement-actions"></a>Fel utlösare för regelefterlevnad och tvingande åtgärder

När överträdelser identifieras bör du vidta tvingande åtgärder för att justera med principen. Du kan automatisera de flesta fel utlösare med hjälp av verktygen som beskrivs i [Cost Management verktygskedjan för Azure](./toolchain.md).

Följande är exempel på utlösare:

- **Månatlig budget avvikelser.** Diskutera eventuella avvikelser i månads utgifter som överstiger 20% prognos-till-faktisk-förhållande med fakturerings enhetens ledare. Registrera lösningar och ändringar i prognosen.
- **Implementerings steg.** Eventuella avvikelser på en prenumerations nivå som överstiger 20% utlöser en granskning med fakturerings enhetens ledare. Registrera lösningar och ändringar i prognosen.

## <a name="next-steps"></a>Nästa steg

Använd [mallen för moln hantering](./template.md)för att dokumentera de processer och utlösare som överensstämmer med den aktuella moln implementerings planen.

Vägledning om hur du kör moln hanterings principer i justering med implementerings planer finns i artikeln om Cost Management disciplin förbättringar.

> [!div class="nextstepaction"]
> [Cost Management disciplin förbättring](./discipline-improvement.md)
