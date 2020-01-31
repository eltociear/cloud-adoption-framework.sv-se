---
title: Princip satser för resurs konsekvens exempel
description: Princip satser för resurs konsekvens exempel
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 5e997dee318d0d6799167de4f4c61a93c814c548
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807265"
---
# <a name="resource-consistency-sample-policy-statements"></a>Princip satser för resurs konsekvens exempel

Enskilda moln princips instruktioner är rikt linjer för att åtgärda specifika risker som identifieras under riskbedömningen. Dessa instruktioner bör ge en kortfattad sammanfattning av riskerna och planer för att hantera dem. Varje uttrycks definition ska innehålla dessa delar av informationen:

- **Teknisk risk:** En sammanfattning av risken som den här principen kommer att åtgärda.
- **Princip instruktion:** En tydlig Sammanfattning av princip kraven.
- **Design alternativ:** Rekommendationer, specifikationer eller andra rikt linjer som IT-team och utvecklare kan använda när de implementerar principen.

Följande exempel på princip satser löser vanliga affärs risker relaterade till resurs konsekvens. Dessa instruktioner är exempel som du kan referera till när du använder policy-instruktioner för att uppfylla organisationens behov. Dessa exempel är inte avsedda att vara proskriptiga och det finns potentiellt flera princip alternativ för att hantera varje identifierad risk. Arbeta nära företags-och IT-team för att identifiera de bästa principerna för din unika uppsättning risker.

## <a name="tagging"></a>Taggar

**Teknisk risk:** Utan korrekt metadata-taggning som är associerad med distribuerade resurser kan IT-avdelningen inte prioritera support eller optimering av resurser baserat på nödvändigt service avtal, viktigt för affärs åtgärder eller drifts kostnader. Detta kan resultera i en mis-allokering av IT-resurser och potentiella fördröjningar i incident lösning.

**Princip instruktion:** Följande principer kommer att implementeras:

- Distribuerade till gångar ska vara taggade med följande värden:
  - Kostnad
  - Allvarlighets grad
  - SLA
  - Miljö
- Styrnings verktyg måste verifiera taggning som rör kostnader, allvarlighets grad, SLA, program och miljö. Alla värden måste justeras mot fördefinierade värden som hanteras av styrnings teamet.

**Potentiella design alternativ:** I Azure stöds [taggar för standardvärden metadata](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) på de flesta resurs typer. [Azure policy](https://docs.microsoft.com/azure/governance/policy/overview) används för att genomdriva vissa taggar som en del av att skapa en resurs.

## <a name="ungoverned-subscriptions"></a>Inte reglerade prenumerationer

**Teknisk risk:** Godtycklig skapande av prenumerationer och hanterings grupper kan leda till isolerade delar av din moln egendom som inte är korrekt underkastade dina styrnings principer.

**Princip instruktion:** Att skapa nya prenumerationer eller hanterings grupper för alla verksamhets kritiska program eller skyddade data kräver en granskning från moln styrnings teamet. Godkända ändringar integreras i en korrekt skiss tilldelning.

**Potentiella design alternativ:** Lås administrativ åtkomst till dina organisationers [hanterings grupper i Azure](https://docs.microsoft.com/azure/governance/management-groups) till endast godkända styrnings grupp medlemmar som styr skapande och åtkomst kontroll processen för prenumerationen.

## <a name="manage-updates-to-virtual-machines"></a>Hantera uppdateringar på virtuella datorer

**Teknisk risk:** Virtuella datorer (VM: ar) som inte är uppdaterade med de senaste uppdateringarna och program varu korrigeringarna är utsatta för säkerhets-eller prestanda problem, vilket kan leda till avbrott i tjänsten.

**Princip instruktion:** Styrnings verktyg måste framtvinga att automatiska uppdateringar aktive ras på alla distribuerade virtuella datorer. Överträdelser måste granskas med operativa hanterings team och åtgärdas i enlighet med Operations policys. Till gångar som inte uppdateras automatiskt måste ingå i processer som ägs av IT-åtgärder.

**Potentiella design alternativ:** För virtuella Azure-datorer kan du tillhandahålla konsekvent uppdaterings hantering med hjälp av [uppdateringshantering-lösningen i Azure Automation](https://docs.microsoft.com/azure/automation/automation-update-management).

## <a name="deployment-compliance"></a>Kompatibilitet för distribution

**Teknisk risk:** Distributions skript och automatiserings verktyg som inte är helt testats av moln styrnings teamet kan leda till resurs distributioner som bryter mot principen.

**Princip instruktion:** Följande principer kommer att implementeras:

- Distributions verktyg måste godkännas av moln styrnings teamet för att säkerställa fort löp ande styrning av distribuerade till gångar.
- Distributions skripten måste finnas i den centrala lagrings platsen som är tillgänglig för gruppen moln styrning för regelbunden granskning och granskning.

**Potentiella design alternativ:** Konsekvent användning av [Azure-ritningar](https://docs.microsoft.com/azure/governance/blueprints) för att hantera automatiserade distributioner ger konsekventa distributioner av Azure-resurser som följer organisationens styrnings standarder och principer.

## <a name="monitoring"></a>Övervakning

**Teknisk risk:** Inkorrekt implementerad eller inkonsekvent instrumenterad övervakning kan förhindra identifiering av problem med arbets belastnings hälsa eller andra överträdelser av policyn.

**Princip instruktion:** Följande principer kommer att implementeras:

- Styrnings verktyg måste kontrol lera att alla till gångar ingår i övervakningen av resurs uttömdhet, säkerhet, efterlevnad och optimering.
- Styrnings verktyg måste verifiera att lämplig nivå av loggnings data samlas in för alla program och data.

**Potentiella design alternativ:** [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) är standard övervaknings tjänsten i Azure och konsekvent övervakning kan tillämpas via [Azure-ritningar](https://docs.microsoft.com/azure/governance/blueprints) när du distribuerar resurser.

## <a name="disaster-recovery"></a>Haveriberedskap

**Teknisk risk:** Resurs fel, borttagningar eller skador kan leda till avbrott i verksamhets kritiska program eller tjänster och förlust av känsliga data.

**Princip instruktion:** Alla verksamhets kritiska program och skyddade data måste ha säkerhets kopierings-och återställnings lösningar som har implementerats för att minimera affärs påverkan av avbrott eller systemfel.

**Potentiella design alternativ:** Tjänsten [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) tillhandahåller funktioner för säkerhets kopiering, återställning och replikering som minimerar tiden för avbrott i affärs kontinuitet och haveri beredskap (BCDR).

## <a name="next-steps"></a>Nästa steg

Använd de exempel som nämns i den här artikeln som utgångs punkt för att utveckla principer som åtgärdar specifika affärs risker som överensstämmer med dina moln implementerings planer.

Om du vill börja utveckla dina egna anpassade princip satser som är relaterade till resurs konsekvens laddar du ned [mallen resurs konsekvens](./template.md).

För att påskynda införandet av denna disciplin väljer du den [Åtgärds bara styrnings guide](../guides/index.md) som bäst passar din miljö. Ändra sedan designen så att du kan lägga till dina företags princip beslut.

Skapa på risker och tolerans, upprätta en process för styrning och kommunikation av resurs konsekvens policyn.

> [!div class="nextstepaction"]
> [Upprätta rutiner för regelefterlevnad](./compliance-processes.md)
