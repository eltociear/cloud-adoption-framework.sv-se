---
title: 'Standard Enterprise-guide: förbättra Cost Management disciplin'
description: 'Standard Enterprise-guide: förbättra Cost Management disciplin'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 83fe35135b37fe96a95f7335639aec65538ee829
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806211"
---
# <a name="standard-enterprise-guide-improve-the-cost-management-discipline"></a>Standard Enterprise-guide: förbättra Cost Management disciplin

Den här artikeln tar en berättelse genom att lägga till kostnads kontroller i styrnings MVP.

## <a name="advancing-the-narrative"></a>Med den här berättelsenn

Införande har ökat enligt den kostnads tolerans indikator som definierats i styrnings MVP. Detta är en bra sak, eftersom det motsvarar migreringar från "DR"-data centret. Ökningen av utgifterna motiverar nu en investering av tid från moln styrnings teamet.

### <a name="changes-in-the-current-state"></a>Ändringar i det aktuella läget

I föregående fas av den här delen hade den dragits tillbaka 100% av DR-datacentret. Program utvecklingen och BI team var klara för produktions trafik.

Sedan dess har vissa saker ändrats som påverkar styrning:

- Migration-teamet har börjat migrera virtuella datorer från produktions data centret.
- Program utvecklings teamen skickar aktivt produktions program till molnet via CI/CD-pipeliner. Dessa program kan skalas om med användar krav.
- Business Intelligences teamet inom IT har levererat flera verktyg för förutsägelse analys i molnet. Volymerna för data som sammanställs i molnet fortsätter att växa.
- All den här tillväxten stöder bekräftade affärs resultat. Men kostnaderna har börjat Mushroom. Planerade budgetar växer snabbare än förväntat. Ekonomi chefen behöver förbättrade metoder för att hantera kostnader.

### <a name="incrementally-improve-the-future-state"></a>Förbättra framtida tillstånd stegvis

Kostnads övervakning och rapportering ska läggas till i moln lösningen. DEN fungerar fortfarande som ett kostnads clearing hus. Det innebär att betalning för moln tjänster fortfarande kommer från IT-tillvaratagande. Rapportering bör dock knyta direkta rörelsekostnader till de funktioner som konsumerar moln kostnaderna. Den här modellen kallas för moln redovisnings modell för "Visa tillbaka".

Ändringarna i det aktuella och framtida läget ger nya risker som kräver nya princip instruktioner.

## <a name="changes-in-tangible-risks"></a>Förändringar i materiella risker

**Budget kontroll:** Det finns en risk att självbetjänings funktioner leder till stora och oväntade kostnader på den nya plattformen. Styrnings processer för att övervaka kostnader och undvika kontinuerliga kostnads risker måste vara på plats för att säkerställa fortsatt justering med den planerade budgeten.

Den här affärs risken kan utökas till några tekniska risker:

- De faktiska kostnaderna kan överstiga planen.
- Ändring av affärs villkor. När de gör det kommer det att finnas fall då en affärs funktion behöver förbruka fler moln tjänster än förväntat, vilket leder till utgifts avvikelser. Det finns en risk för att dessa extra utgifter kommer att betraktas som överförbrukning, i stället för en nödvändig justering av planen.
- System kan överetableras, vilket resulterar i större utgifter.

## <a name="incremental-improvement-of-the-policy-statements"></a>Stegvis förbättring av princip uttrycken

Följande ändringar i principen hjälper dig att åtgärda de nya riskerna och guidens implementering.

- Alla moln kostnader bör övervakas mot plan i varje vecka av styrnings teamet. Rapportering av avvikelser mellan moln kostnader och-planer är att delas med IT-ledande och ekonomi per månad. Alla moln kostnader och prenumerations uppdateringar bör granskas med IT-ledarskap och ekonomi.
- Alla kostnader måste allokeras till en affärs funktion i ansvars syfte.
- Moln till gångar bör övervakas kontinuerligt för optimerings möjligheter.
- Verktyget för moln styrning måste begränsa till gångs storleks alternativ till en godkänd lista över konfigurationer. Verktyget måste se till att alla till gångar kan identifieras och spåras av lösningen för kostnads övervakning.
- Under distributions planeringen bör alla nödvändiga moln resurser som är kopplade till värd för produktions arbets belastningar dokumenteras. I den här dokumentationen får du hjälp med att förfina budgetar och förbereda ytterligare automatisering för att förhindra att dyra alternativ används. Under den här processen bör du ta hänsyn till olika rabatt verktyg som tillhandahålls av moln leverantören, till exempel reserverade instanser eller lägre licens kostnader.
- Alla program ägare krävs för att kunna delta i metoder för att optimera arbets belastningar för att bättre kontrol lera moln kostnaderna.

## <a name="incremental-improvement-of-the-best-practices"></a>Stegvis förbättring av bästa praxis

Det här avsnittet av artikeln ändrar designen för styrnings MVP till att inkludera nya Azure-principer och en implementering av Azure Cost Management. Tillsammans kommer dessa två design ändringar att uppfylla de nya företags princip satserna.

1. Implementera Azure Cost Management.
    1. Upprätta rätt omfång för åtkomst att justeras efter prenumerations mönstret och disciplinen för resurs konsekvens. Om du antar justering med styrnings MVP: t som definierats i föregående artiklar **, kräver detta att du** får åtkomst till moln styrnings gruppen för moln styrning som körs på rapportering på hög nivå. Ytterligare team utanför styrning kan kräva åtkomst till **resurs gruppens omfång** .
    1. Upprätta en budget i Azure Cost Management.
    1. Granska och agera på inledande rekommendationer. Ha en återkommande process för att stödja rapportering.
    1. Konfigurera och köra Azure Cost Management rapportering, både initial och återkommande.
2. Uppdatera Azure Policy
    1. Granska värdena för taggning, hanterings grupp, prenumeration och resurs grupp för att identifiera eventuella avvikelser.
    1. Upprätta alternativ för SKU-storlek för att begränsa distributioner till SKU: er som anges i dokumentation om distributions planering.

## <a name="conclusion"></a>Slutsats

Genom att lägga till dessa processer och ändringar i styrnings MVP: n kan du åtgärda många av de risker som är förknippade med kostnads styrning. Tillsammans skapar de insyn, ansvar och optimering som krävs för att kontrol lera kostnaderna.

## <a name="next-steps"></a>Nästa steg

När moln implementeringen fortsätter och levererar ytterligare affärs värde, kommer risker och moln styrnings behov också att ändras. För det fiktiva företaget i den här hand boken använder nästa steg denna styrnings investering för att hantera flera moln.

> [!div class="nextstepaction"]
> [Utveckling av multimoln](./multicloud-improvement.md)
