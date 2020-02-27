---
title: Etablera processer för policyefterlevnad
description: Skapa en strategi och processer för att säkerställa att moln distributionen följer dina princip krav. 
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 760015fc72cd893cb14dd39d9a9b3078d304da97
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77709472"
---
<!-- markdownlint-disable MD026 -->

# <a name="establish-policy-adherence-processes"></a>Etablera processer för policyefterlevnad

När du har upprättat ditt Cloud policy-uttryck och skapat en design guide måste du skapa en strategi för att se till att moln distributionen hålls i överensstämmelse med dina princip krav. Den här strategin måste omfatta ditt moln styrnings Teams pågående gransknings-och kommunikations processer, fastställa kriterier för när princip överträdelser kräver åtgärder och definiera kraven för automatiska övervaknings-och efterlevnadsprinciper som kommer att identifiera överträdelser och Utlös reparations åtgärder.

Se avsnittet företags principer för de [stödda styrnings guiderna](../guides/index.md) för att få exempel på hur processen stämmer in i en plan för moln styrning.

## <a name="prioritize-policy-adherence-processes"></a>Prioritera policys process processer

Hur mycket investering i utvecklings processer krävs för att stödja dina policy mål? Beroende på hur stor moln distributionen är och hur lång tid det tar, kan det som krävs för att upprätta processer som stöder efterlevnad, och kostnaderna som är förknippade med denna ansträngning variera mycket.

För små distributioner som består av utvecklings-och test resurser kan princip kraven vara enkla och kräva få dedikerade resurser för att åtgärda detta. Å andra sidan kan en vuxen verksamhets kritisk moln distribution med hög prioritets krav för säkerhet och prestanda kräva ett team av personal, omfattande interna processer och anpassat övervaknings verktyg som stöder dina princip mål.

Som ett första steg i att definiera policyn för policyn, ska du utvärdera hur processerna som beskrivs nedan kan stödja dina princip krav. Ta reda på hur mycket ansträngning som är värt att investera i dessa processer och Använd sedan den här informationen för att upprätta realistiska budget-och personal planer för att möta dessa behov.

## <a name="establish-cloud-governance-team-processes"></a>Upprätta team processer för moln styrning

Innan du definierar utlösare för policy för efterlevnad av principer måste du upprätta de övergripande processerna som ditt team kommer att använda och hur information ska delas och eskaleras mellan IT-personal och moln styrnings teamet.

### <a name="assign-cloud-governance-team-members"></a>Tilldela team medlemmar för moln styrning

Ditt moln styrnings team ger fort löp ande vägledning om policy efterlevnad och hantering av policy-relaterade problem som uppstår när du distribuerar och hanterar dina moln till gångar. När du skapar det här teamet kan du bjuda in personal medlemmar som har expertis inom områden som omfattas av dina definierade policy-uttryck och identifierade risker.

Vid inledande test distributioner kan detta begränsas till några system administratörer som ansvarar för att etablera grunderna för styrning. När dina styrnings processer är vuxen granskar du moln guidens medlemskap regelbundet för att säkerställa att du kan åtgärda nya potentiella risker och princip krav på rätt sätt. Identifiera medlemmar av IT-avdelningen och företags personalen med relevant erfarenhet eller intresse av vissa delar av styrningen och ta med dem i teamen på ett permanent eller tillfälligt sätt vid behov.

### <a name="reviews-and-policy-iteration"></a>Recensioner och princip upprepning

När ytterligare resurser och arbets belastningar distribueras måste moln styrnings teamet se till att nya arbets belastningar eller till gångar uppfyller princip kraven. Utvärdera nya krav från arbets belastnings utvecklings grupper för att säkerställa att deras planerade distributioner överensstämmer med dina design guider och uppdatera dina principer för att stödja dessa krav när det är lämpligt.

Planera för att utvärdera nya potentiella risker och uppdatera princip satser och design guider efter behov. Arbeta med IT-personal och arbets belastnings grupper för att utvärdera nya Azure-funktioner och-tjänster kontinuerligt. Du kan också schemalägga regelbundna granskningar i alla de fem styrnings disciplinerna för att säkerställa att principen är aktuell och att den efterlevs.

### <a name="education"></a>Utbildning

Policy efterlevnad kräver IT-personal och utvecklare för att förstå de princip krav som påverkar deras ansvars områden. Planera att ägna resurser till att dokumentera beslut och krav och utbilda alla relevanta team på de design guider som har stöd för dina princip krav.

När princip ändringar uppdateras regelbundet dokumentations-och utbildnings material, och säkerställer att utbildnings insatserna kommunicerar med uppdaterade krav och rikt linjer för relevant IT-personal.

I olika stadier av din moln resa kanske du tycker att det är bäst att kontakta partner och professionella utbildningsprogram för att förbättra din grupps utbildning, både tekniskt och procedur mässiga. Dessutom är många hitta att formella certifieringar är ett värdefullt tillägg till din utbildnings portfölj och bör övervägas.

### <a name="establish-escalation-paths"></a>Upprätta vägar för eskalering

Om en resurs upphör att uppfylla kraven får han ett meddelande? Om IT-personalen identifierar ett problem med efterlevnaden av principen kontaktar de dem? Se till att eskalera processen till moln styrnings gruppen är tydligt definierad. Se till att dessa kommunikations kanaler uppdateras för att avspegla ändringar i personal och organisationer.

## <a name="violation-triggers-and-actions"></a>Fel utlösare och åtgärder

När du har definierat ditt team för moln styrning och dess processer, måste du uttryckligen definiera vad som är kvalificerat som överträdelser som utlöser åtgärder och vad dessa åtgärder ska vara.

### <a name="define-triggers"></a>Definiera utlösare

Granska kraven för var och en av dina princip instruktioner för att fastställa vad som utgör en princip överträdelse. Generera dina utlösare med hjälp av den information som du redan har etablerat som en del av princip definitions processen.

- **Risk tolerans:** Skapa fel utlösare baserat på de mått och risk indikatorer som du upprättar som en del av din [risk tolerans analys](./risk-tolerance.md).
- **Definierade princip krav:** Princip satser kan tillhandahålla service avtal (SLA), verksamhets kontinuitet och haveri beredskap (BCDR) eller prestanda krav som ska användas som utgångs punkt för kompatibilitets utlösare.

### <a name="define-actions"></a>Definiera åtgärder

Varje överträdelse-utlösare ska ha motsvarande åtgärd. Utlösta åtgärder bör alltid meddela en lämplig IT-personal eller moln styrnings grupp medlem när en överträdelse inträffar. Det här meddelandet kan leda till en manuell granskning av problemet eller kickoff en fördefinierad reparations process beroende på typen och allvarlighets graden för den identifierade överträdelsen.

Några exempel på fel utlösare och åtgärder:

| Moln styrnings disciplin | Exempel utlösare | Exempel åtgärd |
|-----------------------------|----------------|---------------|
| Cost Management | Månads moln utgifter är mer än 20% högre än förväntat. | Meddela den fakturerings enhets ledare som ska påbörja en granskning av resursanvändningen. |
| Grundläggande säkerhet | Identifiera misstänkt användar aktivitet. | Meddela IT-säkerhetsteamet och inaktivera det misstänkta användar kontot. |
| Resurskonsekvens | PROCESSOR belastningen för en arbets belastning är större än 90%. | Meddela IT-avdelningen och skala ut ytterligare resurser för att hantera belastningen. |

## <a name="automation-of-monitoring-and-compliance"></a>Automatisering av övervakning och efterlevnad

När du har definierat fel utlösare och åtgärder för regelefterlevnad kan du börja planera hur du ska använda loggnings-och rapporterings verktygen och andra funktioner i moln plattformen för att automatisera strategin för övervakning och policy efterlevnad.

För hjälp med att välja det bästa övervaknings mönstret för din distribution, se [loggning och rapportering av besluts guide](../../decision-guides/logging-and-reporting/index.md).

## <a name="next-steps"></a>Nästa steg

Lär dig mer om regelefterlevnad i molnet.

> [!div class="nextstepaction"]
> [Regelefterlevnad](./regulatory-compliance.md)
