---
title: Exempel princip satser för distributions acceleration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Exempel princip satser för distributions acceleration
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 4a2b1666332ca884dfb95b2b2372f3b5518bd635
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030603"
---
# <a name="deployment-acceleration-sample-policy-statements"></a>Exempel princip satser för distributions acceleration

Enskilda moln princips instruktioner är rikt linjer för att åtgärda specifika risker som identifieras under riskbedömningen. Dessa instruktioner bör ge en kortfattad sammanfattning av riskerna och planer för att hantera dem. Varje uttrycks definition ska innehålla dessa delar av informationen:

- **Teknisk risk.** En sammanfattning av risken som den här principen kommer att åtgärda.
- **Princip instruktion.** En tydlig Sammanfattning av princip kraven.
- **Design alternativ.** Rekommendationer, specifikationer eller andra rikt linjer som IT-team och utvecklare kan använda när de implementerar principen.

Följande exempel på princip satser hanterar vanliga konfigurations relaterade affärs risker. Dessa instruktioner är exempel som du kan referera till när du använder policy-instruktioner för att uppfylla organisationens behov. Dessa exempel är inte avsedda att vara proskriptiga och det finns potentiellt flera princip alternativ för att hantera varje identifierad risk. Arbeta nära företags-och IT-team för att identifiera de bästa principerna för din unika uppsättning risker.

## <a name="reliance-on-manual-deployment-or-configuration-of-systems"></a>Beroende på manuell distribution eller konfiguration av system

**Teknisk risk:** Att förlita sig på mänsklig inblandning eller konfiguration ökar sannolikheten för mänskligt fel och minskar repeterbarheten och förutsägbarheten för system distributioner och konfiguration. Det leder också till långsammare distribution av system resurser.

**Princip instruktion:** Alla till gångar som distribueras till molnet bör distribueras med hjälp av mallar eller Automation-skript närhelst det är möjligt.

**Potentiella design alternativ:** [Azure Resource Manager mallar](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) innehåller en infrastruktur som kod för att distribuera dina resurser till Azure. [Azures Bygg stenar](https://github.com/mspnp/template-building-blocks/wiki) tillhandahåller ett kommando rads verktyg och en uppsättning Resource Manager-mallar som har utformats för att förenkla distributionen av Azure-resurser.

## <a name="lack-of-visibility-into-system-issues"></a>Brist på insyn i system problem

**Teknisk risk:** Otillräcklig övervakning och diagnostik för företag förhindrar drifts personal från att identifiera och åtgärda problem innan ett system avbrott uppstår, och det kan avsevärt öka den tid som krävs för att lösa ett avbrott.

**Princip instruktion:** Följande principer kommer att implementeras:

- Nyckel mått och diagnostiska mått kommer att identifieras för alla produktions system och-komponenter, och övervaknings-och diagnostikverktyg kommer att tillämpas på dessa system och övervakas regelbundet av drifts personal.
- Åtgärder bör använda övervaknings-och diagnostikverktyg i miljöer som inte är för produktion, till exempel mellanlagring och frågor och svar för att identifiera system problem innan de inträffar i produktions miljön.

**Potentiella design alternativ:** [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor), som även innehåller Log Analytics och Application Insights, innehåller verktyg för att samla in och analysera telemetri för att hjälpa dig att förstå hur dina program presterar och proaktivt identifiera problem som påverkar dem och resurser som de är beroende av.

## <a name="configuration-security-reviews"></a>Säkerhets granskningar av konfiguration

**Teknisk risk:** Med tiden kan nya säkerhetshot eller problem öka risken för obehörig åtkomst till säkra resurser.

**Princip instruktion:** Moln styrnings processer måste ta med kvartals granskning med konfigurations hanterings team för att identifiera skadliga aktörer eller användnings mönster som bör förhindras av konfiguration av moln till gångar.

**Potentiella design alternativ:** Upprätta ett kvartals Visa säkerhets gransknings möte som omfattar både styrelse ledamöter och IT-personal som ansvarar för konfiguration av moln program och resurser. Granska befintliga säkerhets data och mått för att skapa luckor i aktuell distributions accelerations princip och verktyg och uppdatera principer för att åtgärda eventuella nya risker.

## <a name="next-steps"></a>Nästa steg

Använd de exempel som nämns i den här artikeln som utgångs punkt för att utveckla principer som åtgärdar specifika affärs risker som överensstämmer med dina moln implementerings planer.

Om du vill börja utveckla dina egna anpassade policy-instruktioner som rör identitets hantering laddar du ned [bas linje mal len för identiteten](./template.md).

För att påskynda införandet av denna disciplin väljer du den [Åtgärds bara styrnings guide](../guides/index.md) som bäst passar din miljö. Ändra sedan designen så att du kan lägga till dina företags princip beslut.

Skapa på risker och tolerans, upprätta en process för styrning och kommunikation av distributions accelerations policyn.

> [!div class="nextstepaction"]
> [Upprätta rutiner för regelefterlevnad](./compliance-processes.md)
