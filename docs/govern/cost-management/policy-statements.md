---
title: Cost Management exempel på princip satser
description: Använd ramverket för moln införande för Azure för att hämta exempel Cost Management princip satser som hjälper dig att skapa ett utkast till princip satser.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 7908dfe5a4ab63d37f97296cf8b830f358a2f4ea
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434654"
---
# <a name="cost-management-sample-policy-statements"></a>Cost Management exempel på princip satser

Enskilda moln princips instruktioner är rikt linjer för att åtgärda specifika risker som identifieras under riskbedömningen. Dessa instruktioner bör ge en kortfattad sammanfattning av riskerna och planer för att hantera dem. Varje uttrycks definition ska innehålla dessa delar av informationen:

- **Affärs risk:** En sammanfattning av risken som den här principen kommer att åtgärda.
- **Princip instruktion:** En tydlig Sammanfattning av princip kraven.
- **Design alternativ:** Rekommendationer, specifikationer eller andra rikt linjer som IT-team och utvecklare kan använda när de implementerar principen.

Följande exempel på princip satser riktar sig mot vanliga kostnads relaterade affärs risker. Dessa instruktioner är exempel som du kan referera till när du använder policy-instruktioner för att uppfylla organisationens behov. Dessa exempel är inte avsedda att vara förebyggande och det finns potentiellt flera princip alternativ för att hantera varje identifierad risk. Arbeta nära företags-och IT-team för att identifiera de bästa principerna för din unika uppsättning risker.

## <a name="future-proofing"></a>Framtida korrektur

**Affärs risk:** Aktuella kriterier som inte garanterar en investering i en Cost Management disciplin från styrnings teamet. Men du förväntar dig en sådan investering i framtiden.

**Princip instruktion:** Du bör koppla alla till gångar som har distribuerats till molnet med en fakturerings enhet och ett program/arbets belastning. Den här principen säkerställer att framtida Cost Management ansträngningar träder i kraft.

**Design alternativ:** Information om hur du upprättar en framtida gransknings grund finns i diskussionerna om att skapa en styrnings-MVP i de användbara [design guiderna](../guides/index.md) som ingår i vägledningen för moln implementerings ramverk.

## <a name="budget-overruns"></a>Budget överskridningar

**Affärs risk:** Självbetjänings distribution skapar en risk för överförbrukning.

**Princip instruktion:** Alla moln distributioner måste tilldelas en fakturerings enhet med godkänd budget och en mekanism för budget gränser.

**Design alternativ:** I Azure kan du kontrol lera budgeten med [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/manage-budgets)

## <a name="underutilization"></a>Underutnyttjande

**Affärs risk:** Företaget har förbetalt för moln tjänster eller har gjort ett årligt åtagande att spendera en speciell mängd. Det finns en risk för att den överenskomna mängden inte används, vilket resulterar i en förlorad investering.

**Princip instruktion:** Varje fakturerings enhet med en tilldelad moln budget sammanfaller årligen för att ställa in budgetar, kvartals vis för att justera budgetar och månatlig att allokera tid för att granska planerade kontra faktiska utgifter. Diskutera eventuella avvikelser som är större än 20% med fakturerings enhetens ledare månads vis. I spårnings syfte tilldelar du alla till gångar till en fakturerings enhet.

**Design alternativ:**

- I Azure kan planerade kontra faktiska utgifter hanteras via [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/quick-acm-cost-analysis)
- Det finns flera alternativ för att gruppera resurser efter fakturerings enhet. I Azure väljs en [resurs konsekvens modell](../../decision-guides/resource-consistency/index.md) tillsammans med styrnings teamet och tillämpas på alla till gångar.

## <a name="overprovisioned-assets"></a>Överetablerat till gångar

**Affärs risk:** I traditionella lokala data Center är det vanligt att distribuera till gångar med extra kapacitets planering för tillväxt i en avlägsen framtid. Molnet kan skala snabbare än traditionell utrustning. Till gångar i molnet priss ätts också utifrån den tekniska kapaciteten. Det finns en risk för den gamla lokala övningen för moln utgifter som är artificiellt inflata.

**Princip instruktion:** Alla till gångar som distribueras till molnet måste vara registrerade i ett program som kan övervaka användningen och rapportera alla kapaciteter som överstiger 50% av användningen. Alla till gångar som distribueras till molnet måste grupperas eller taggas på ett logiskt sätt, så styrnings grupp medlemmar kan engagera arbets belastnings ägaren för all optimering av överetablerade till gångar.

**Design alternativ:**

- I Azure kan [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations) tillhandahålla optimerings rekommendationer.
- Det finns flera alternativ för att gruppera resurser efter fakturerings enhet. I Azure väljs en [resurs konsekvens modell](../../decision-guides/resource-consistency/index.md) tillsammans med styrnings teamet och tillämpas på alla till gångar.

## <a name="overoptimization"></a>Överoptimering

**Affärs risk:** Effektiv kostnads hantering skapar nya risker. Optimering av utgifter är invers till systemets prestanda. När du sänker kostnaderna finns det risk för att du översätter utgifter och genererar dåliga användar upplevelser.

**Princip instruktion:** Alla till gångar som direkt påverkar kund upplevelser måste identifieras genom gruppering eller taggning. Innan du optimerar en till gång som påverkar kund upplevelsen måste moln styrnings teamet justera optimeringen baserat på minst 90 dagars användnings trender. Dokumentera eventuella säsongs-och händelse drivna burst-objekt som beaktas när du optimerar till gångar.

**Design alternativ:**

- I Azure kan [Azure Monitor insikter-funktioner](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-performance) hjälpa till med analys av system användning.
- Det finns flera alternativ för att gruppera och tagga resurser baserat på roller. I Azure bör du välja en [resurs konsekvens modell](../../decision-guides/resource-consistency/index.md) tillsammans med styrnings teamet och tillämpa detta på alla till gångar.

## <a name="next-steps"></a>Nästa steg

Använd de exempel som nämns i den här artikeln som utgångs punkt för att utveckla principer som åtgärdar specifika affärs risker som överensstämmer med dina moln implementerings planer.

Om du vill börja utveckla dina egna anpassade policy-instruktioner som är relaterade till Cost Management hämtar du [Cost Management-mallen](./template.md).

För att påskynda införandet av denna disciplin väljer du den [Åtgärds bara styrnings guide](../guides/index.md) som bäst passar din miljö. Ändra sedan designen så att du kan lägga till dina företags princip beslut.

Skapa på risker och toleranser och upprätta en process för att övervaka och kommunicera Cost Management policyn.

> [!div class="nextstepaction"]
> [Upprätta rutiner för regelefterlevnad](./compliance-processes.md)
