---
title: 'Styrnings guide för komplexa företag: förbättra Cost Management disciplin'
description: 'Styrnings guide för komplexa företag: förbättra Cost Management disciplin'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 2b66894ca215156aa9688ca1ab458910e8f496f8
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76805735"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-cost-management-discipline"></a>Styrnings guide för komplexa företag: förbättra Cost Management disciplin

Den här artikeln tar en berättelse genom att lägga till kostnads kontroller till den minimala MVP-styrningen (livsduglig produkt).

## <a name="advancing-the-narrative"></a>Med den här berättelsenn

Införande har ökat utöver tolerans indikatorn som definierats i styrnings MVP: en. Ökningarna i utgifterna motiverar nu en investering av tid från moln styrnings teamet för att övervaka och kontrol lera utgifts mönster.

Som en tydlig driv rutin för innovation visas den inte längre främst som ett kostnads ställe. Eftersom IT-organisationen ger mer värde, samtycker IT-chefen och ekonomi chefen att tiden är rätt att byta rollen som den spelar i företaget. Bland andra ändringar vill chefen testa en direkt betalnings metod för moln redovisning för den kanadensiska grenen av en av affär senheterna. Ett av de två tillbakadragna data centren var exklusivt värdbaserade till gångar för denna affär senhets kanadensiska åtgärder. I den här modellen debiteras affär senhetens kanadensiska dotter bolag direkt för de drift kostnader som är relaterade till de värdbaserade till gångarna. Den här modellen gör det möjligt för IT att fokusera mindre på att hantera någon annans utgifter och mer om att skapa ett värde. Men innan den här över gången kan börja Cost Management verktyg måste vara på plats.

### <a name="changes-in-the-current-state"></a>Ändringar i det aktuella läget

I föregående fas av den här delen flyttade IT-teamet aktivt produktions arbets belastningar med skyddade data till Azure.

Sedan dess har vissa saker ändrats som påverkar styrning:

- 5 000 till gångar har tagits bort från de två Data Center som har flaggats för pensionering. Anskaffning och IT-säkerhet avetablerar nu de återstående fysiska till gångarna.
- Program utvecklings teamen har implementerat CI/CD-pipeliner för att distribuera vissa molnbaserade program, vilket avsevärt påverkar kund upplevelsen.
- BI-teamet har skapat agg regerings-, hanterings-, insikter-och förutsägelse processer som kör konkreta förmåner för affärs verksamhet. Dessa förutsägelser ger nu nya kreativa produkter och tjänster.

### <a name="incrementally-improve-the-future-state"></a>Förbättra framtida tillstånd stegvis

Kostnads övervakning och rapportering ska läggas till i moln lösningen. Rapportering ska knyta direkta drift kostnader till de funktioner som konsumerar moln kostnaderna. Ytterligare rapportering bör göra det möjligt för IT att övervaka utgifter och tillhandahålla teknisk vägledning om kostnads hantering. För kanadensisk gren faktureras avdelningen direkt.

## <a name="changes-in-risk"></a>Ändringar i risk

**Budget kontroll:** Det finns en risk att självbetjänings funktioner leder till stora och oväntade kostnader på den nya plattformen. Styrnings processer för att övervaka kostnader och undvika kontinuerliga kostnads risker måste vara på plats för att säkerställa fortsatt justering med den planerade budgeten.

Den här affärs risken kan utökas till några tekniska risker:

- Det finns en risk för att faktiska kostnader överstiger planen.
- Ändring av affärs villkor. När de gör det kommer det att finnas fall då en affärs funktion behöver förbruka fler moln tjänster än förväntat, vilket leder till utgifts avvikelser. Det finns en risk att dessa ytterligare kostnader kommer att anses som överförbrukning i stället för en nödvändig justering i planen. Om det lyckas bör det kanadensiska experimentet hjälpa till att åtgärda den här risken.
- Det finns en risk för system som överutnyttjas, vilket resulterar i överskott.

## <a name="changes-to-the-policy-statements"></a>Ändringar i princip instruktionerna

Följande ändringar i principen hjälper dig att åtgärda de nya riskerna och guidens implementering.

- Alla moln kostnader bör övervakas mot plan per vecka med hjälp av moln styrnings teamet. Rapportering av avvikelser mellan moln kostnader och-planer är att delas med IT-ledande och ekonomi per månad. Alla moln kostnader och prenumerations uppdateringar bör granskas med IT-ledarskap och ekonomi.
- Alla kostnader måste allokeras till en affärs funktion i ansvars syfte.
- Moln till gångar bör övervakas kontinuerligt för optimerings möjligheter.
- Verktyget för moln styrning måste begränsa till gångs storleks alternativ till en godkänd lista över konfigurationer. Verktyget måste se till att alla till gångar kan identifieras och spåras av lösningen för kostnads övervakning.
- Under distributions planeringen bör alla nödvändiga moln resurser som är kopplade till värd för produktions arbets belastningar dokumenteras. I den här dokumentationen får du hjälp med att förfina budgetar och förbereda ytterligare automatiserings verktyg för att förhindra att dyra alternativ används. Under den här processen bör du ta hänsyn till olika rabatt verktyg som tillhandahålls av moln leverantören, till exempel reserverade instanser eller lägre licens kostnader.
- Alla program ägare krävs för att kunna delta i metoder för att optimera arbets belastningar för att bättre kontrol lera moln kostnaderna.

## <a name="incremental-improvement-of-the-best-practices"></a>Stegvis förbättring av bästa praxis

I det här avsnittet av artikeln får du förbättra designen för styrnings MVP för att inkludera nya Azure-principer och en implementering av Azure Cost Management. Tillsammans kommer dessa två design ändringar att uppfylla de nya företags princip satserna.

1. Gör ändringar i Azure-Enterprise Portal för att fakturera avdelnings administratören för den kanadensiska distributionen.
2. Implementera Azure Cost Management.
    1. Etablera rätt nivå för åtkomstscope så att den överensstämmer med prenumerations mönstret och resurs grupp mönstret. Om du antar justering med styrnings MVP: t som definierats i föregående artiklar, skulle detta kräva åtkomst till **konto omfånget** för moln styrnings teamet som körs på rapportering på hög nivå. Ytterligare team utanför styrning, t. ex. det kanadensiska inköps teamet, kräver åtkomst till **resurs gruppens omfång** .
    2. Upprätta en budget i Azure Cost Management.
    3. Granska och agera på inledande rekommendationer. Vi rekommenderar att du har en återkommande process som stöder rapporterings processen.
    4. Konfigurera och köra Azure Cost Management rapportering, både initial och återkommande.
3. Uppdatera Azure Policy.
    1. Granska taggar, hanterings grupp, prenumeration och resurs grupps värden för att identifiera eventuella avvikelser.
    2. Upprätta alternativ för SKU-storlek för att begränsa distributioner till SKU: er som anges i dokumentation om distributions planering.

## <a name="conclusion"></a>Slutsats

Genom att lägga till ovanstående processer och ändringar i styrnings MVP: n kan du åtgärda många av de risker som är förknippade med kostnads styrning. Tillsammans skapar de insyn, ansvar och optimering som krävs för att kontrol lera kostnaderna.

## <a name="next-steps"></a>Nästa steg

Eftersom moln införande växer och levererar ytterligare affärs värde, kommer risker och moln styrnings behov också att förändras. For this fictional company, the next step is using this governance investment to manage multiple clouds.

> [!div class="nextstepaction"]
> [Multicloud improvement](./multicloud-improvement.md)
