---
title: Procedurer för efterlevnad av distributions accelerations principer
description: Använd ramverket för moln införande för Azure för att lära dig hur du skapar processer som har stöd för en hanterings disciplin för distributions hantering.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3c5d6d187e72217c16ca380f6ef433560b647574
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434571"
---
# <a name="deployment-acceleration-policy-compliance-processes"></a>Procedurer för efterlevnad av distributions accelerations principer

Den här artikeln beskriver en metod för att följa policyer som styr [distributions accelerationen](./index.md). Effektiv styrning av moln konfiguration börjar med återkommande manuella processer som har utformats för att identifiera problem och införa principer för att åtgärda dessa risker. Du kan dock automatisera dessa processer och komplettera dem med verktyg för att minska kostnaderna för styrning och tillåta snabbare svar på avvikelser.

## <a name="planning-review-and-reporting-processes"></a>Planering, granskning och rapportering av processer

Verktyg för bästa distributions acceleration i molnet är bara lika bra som de processer och principer som de stöder. Följande är en uppsättning exempel processer som ofta används som en del av en distributions accelerations disciplin. Använd de här exemplen som en start punkt när du planerar de processer som gör att du kan fortsätta att uppdatera distributions-och konfigurations principer baserat på affärs förändringar och feedback från utvecklings-och IT-team som ansvarar för att dra styrnings vägledningen till tgärd.

**Inledande riskbedömning och planering:** Som en del av ditt första antagande av distributions accelerations disciplinen kan du identifiera de viktiga affärs riskerna och toleranserna som är relaterade till distributionen av dina affärs program. Använd den här informationen för att diskutera tekniska risker med medlemmar i IT-avdelningen och utveckla en bas linje uppsättning distributions-och konfigurations principer för att åtgärda dessa risker för att fastställa din inledande styrnings strategi.

**Distributions planering:** Innan du distribuerar en till gång kan du utföra en säkerhets-och åtgärds granskning för att identifiera eventuella nya risker och se till att alla relevanta princip krav för distribution är uppfyllda.

**Distributions testning:** Som en del av distributions processen för en till gång är moln styrnings teamet i samarbete med IT-avdelningen ansvariga för att granska distributions principens efterlevnad.

**Årlig planering:** Genomför en årlig översyn av distributions accelerations strategin på hög nivå. Utforska framtida företags prioriteringar och uppdaterade moln implementerings strategier för att identifiera potentiell risk ökning och andra nya konfigurations behov och affärs möjligheter. Du kan också använda den här tiden för att granska de senaste DevOps-bästa metoderna och integrera dem i dina principer och gransknings processer.

**Kvartals vis granskning och planering:** Genomför en kvartals granskning av drift gransknings data och incident rapporter för att identifiera eventuella ändringar som krävs i distributions accelerations principen. Som en del av den här processen granskar du aktuella metoder för DevOps och DevTechOps och uppdaterar principen efter behov. När granskningen är klar kan du justera rikt linjerna för program-och system design med den uppdaterade principen.

Den här planerings processen är också en lämplig tid att utvärdera det aktuella medlemskapet i moln styrnings teamet för kunskaps luckor som rör nya eller föränderliga principer och risker relaterade till DevOps och distributions acceleration. Bjud in relevant IT-personal för att delta i granskningar och planering som antingen tillfälliga tekniska rådgivare eller permanenta medlemmar i teamet.

**Utbildning och utbildning:** I en månad kan du erbjuda utbildning för att se till att IT-personal och utvecklare är uppdaterade på den senaste distributions accelerations strategin och kraven. Som en del av den här processen kan du granska och uppdatera dokumentation, vägledning eller andra utbildnings resurser för att se till att de är synkroniserade med de senaste företags princip uttrycken.

**Granskningar av månads granskning och rapportering:** Genomför en månatlig granskning på alla moln distributioner för att säkerställa att de fortsätter att justera med konfigurations principen. Granska distributions-relaterade aktiviteter med IT-personal och identifiera eventuella kompatibilitetsproblem som inte redan hanteras som en del av den pågående övervaknings-och tvångs processen. Resultatet av den här granskningen är en rapport för moln strategi teamet och varje moln antagande team för att kommunicera den övergripande efterlevnaden av principen. Rapporten lagras också för granskning och juridiskt syfte.

## <a name="ongoing-monitoring-processes"></a>Pågående övervaknings processer

Avgöra om din strategi för distributions accelerations styrningen lyckas beror på insyn i den aktuella och den tidigare statusen för din moln infrastruktur. Utan möjlighet att analysera relevanta mått och data för moln resursernas operativa hälsa och aktivitet kan du inte identifiera ändringar i riskerna eller identifiera överträdelser av dina risk toleranser. De löpande styrnings processer som beskrivs ovan kräver kvalitets data för att säkerställa att principen kan ändras för att skydda infrastrukturen mot att ändra hot och risker från felkonfigurerade resurser.

Se till att IT-avdelningen har implementerat automatiska övervaknings system för din moln infrastruktur som samlar in relevanta loggdata som du behöver för att utvärdera risken. Se till att övervaka dessa system och se till att det går att identifiera och minska risken för eventuella policy överträdelser och se till att din övervaknings strategi är i linje med distributions-och konfigurations behov.

## <a name="violation-triggers-and-enforcement-actions"></a>Fel utlösare och tvingande åtgärder

Eftersom inkompatibilitet med konfigurations principer kan leda till risker för kritiska tjänst störningar bör moln styrnings teamet ha insyn i allvarliga princip överträdelser. Se till att IT-personalen har tydliga eskalering sökvägar för rapportering av kompatibilitetsproblem till styrnings grupps medlemmar som är bäst lämpade att identifiera och kontrol lera att princip problem minimeras när de upptäcks.

När överträdelser identifieras bör du vidta åtgärder för att justera med principen så snart som möjligt. IT-teamet kan automatisera de flesta överträdelser med de verktyg som beskrivs i [distributions accelerationen verktygskedjan för Azure](./toolchain.md).

Följande utlösare och tvingande åtgärder innehåller exempel som du kan använda när du diskuterar hur du använder övervaknings data för att lösa princip överträdelser:

- **Oväntade ändringar i konfigurationen har identifierats.** Om konfigurationen av en resurs ändras oväntad, arbetar du med IT-personal och arbets belastnings ägare för att identifiera rotor saken och utveckla en reparations plan.
- **Konfigurationen av nya resurser följer inte med policyn.** Arbeta med DevOps-team och arbets belastnings ägare för att granska distributions accelerations principer under projekt starten så att alla kan använda relevanta princip krav.
- **Distributions fel eller konfigurations problem orsakar fördröjningar i projekt scheman.** Arbeta med utvecklings team och arbets belastnings ägare för att se till att teamet förstår hur du automatiserar distributionen av molnbaserade resurser för konsekvens och repeterbarhet. Helt automatiserade distributioner bör krävas tidigt i utvecklings cykeln&mdash;att försöka göra detta sent i utvecklings cykeln leder vanligt vis till oväntade problem och fördröjningar.

## <a name="next-steps"></a>Nästa steg

Använd [mallen för moln hantering](./template.md)för att dokumentera de processer och utlösare som överensstämmer med den aktuella moln implementerings planen.

Vägledning om hur du kör moln hanterings principer i justering med implementerings planer finns i artikeln om disciplin förbättringar.

> [!div class="nextstepaction"]
> [Förbättringar av distributions accelerations disciplin](./discipline-improvement.md)
