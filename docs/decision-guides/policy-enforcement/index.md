---
title: Beslutsguide för principframtvingande
description: Använd Cloud Adoption Framework för Azure för att lära dig mer om prenumerationer på principframtvingande som en grundläggande designprioritet i Azure-migreringar.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 2a5976d1aa1bb4ae0b1e8a0d810ae0acddabd883
ms.sourcegitcommit: 10637acba8c857a6f5aa8c4a80c0649903f60402
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/28/2020
ms.locfileid: "78170995"
---
# <a name="policy-enforcement-decision-guide"></a>Beslutsguide för principframtvingande

Att definiera en organisationsprincip gör ingen nytta såvida den inte kan framtvingas i organisationen. En viktig aspekt av att planera molnmigreringar är att avgöra det bästa sättet att kombinera verktyg som tillhandahålls av molnplattformen i dina befintliga IT-processer för att maximera principefterlevnad i hela molnegendomen.

![Alternativ för principframtvingande ordnade från minst till mest komplext, inriktat med direktlänkar nedan](../../_images/decision-guides/decision-guide-policy-enforcement.png)

Hoppa till: [Metodtips för baslinjen](#baseline-best-practices) | [Övervakning av principefterlevnad](#policy-compliance-monitoring) | [Principframtvingande](#policy-enforcement) | [Organisationsövergripande princip](#cross-organization-policy) | [Automatiserat framtvingande](#automated-enforcement)

Allt eftersom din molnegendom växer ställs du inför ett motsvarande behov att upprätthålla och framtvinga principer över en större mängd resurser och prenumerationer. När din egendom blir större och organisationens principkrav ökar behöver omfattningen av dina processer för principframtvingande utökas för att säkerställa konsekvent principefterlevnad och snabb identifiering av överträdelser.

Plattformstillhandahållna mekanismer för principframtvingande på resurs- eller prenumerationsnivå räcker oftast för mindre molnegendomar. Större distributioner motiverar en större omfattning av framtvingande och kan behöva utnyttja mer sofistikerade mekanismer för framtvingande som inbegriper distributionsstandarder, gruppering och organisering av resurser samt integrering av principframtvingande med dina loggnings- och rapporteringssystem.

De huvudsakliga faktorerna för att fastställa omfattningen av dina processer för principframtvingande är organisationens [krav för molnstyrning](../../govern/index.md), storleken och egenskaperna hos din molnegendom samt hur organisationen speglas i din [prenumerationsdesign](../subscriptions/index.md). Både en ökning av storleken på din egendom eller ett högre behov av att centralt hantera principframtvingande kan motivera en ökning av omfattning för framtvingande.

## <a name="baseline-best-practices"></a>Metodtips för baslinjen

För enkla molndistributioner och sådana med en enda prenumeration kan många företagsprinciper framtvingas med hjälp av funktioner som är inbyggda i resurser och prenumerationer i Azure. Konsekvent användning av de mönster som beskrivs i [beslutsguiderna](../index.md) för Cloud Adoption Framework kan hjälpa till att upprätta en baslinjenivå av principefterlevnad utan specifik investering i principframtvingande. Dessa funktioner omfattar:

- [Distributionsmallar](../resource-consistency/index.md) kan etablera resurser med standardiserad struktur och konfiguration.
- [Taggnings- och namngivningsstandarder](../resource-tagging/index.md) kan hjälpa till att organisera drift samt stödja redovisnings- och affärskrav.
- Trafikhantering och nätverksbegränsningar kan implementeras via [programvarudefinierade nätverk](../software-defined-network/index.md).
- [Rollbaserad åtkomstkontroll](../identity/index.md) kan skydda och isolera dina molnresurser.

Påbörja planeringen av framtvingande av molnprincip genom att undersöka hur tillämpningen av de standardmönster som beskrivs i dessa guider kan hjälpa dig att uppfylla organisationskraven.

## <a name="policy-compliance-monitoring"></a>Övervakning av principefterlevnad

Ett första steg bortom att helt enkelt förlita sig på de mekanismer för principframtvingande som tillhandahålls på Azure-plattformen är att säkerställa förmågan att kontrollera huruvida molnbaserade program och tjänster efterlever organisationsprincipen. Detta omfattar implementering av meddelandefunktioner för avisering av ansvariga parter om en resurs slutar efterleva principen. Effektiv [loggning och rapportering](../logging-and-reporting/index.md) av efterlevnadsstatus för dina molnarbetsbelastningar är en mycket viktig del av en företagsstrategi för principframtvingande.

Allt eftersom din molnegendom växer kan ytterligare verktyg såsom [Azure Security Center](https://docs.microsoft.com/azure/security-center) ge integrerad säkerhet och hotidentifiering samt hjälpa till att tillämpa centraliserad principhantering och avisering för båda dina lokala och molnbaserade tillgångar.

## <a name="policy-enforcement"></a>Policyframtvingande

I Azure kan du tillämpa konfigurationsinställningar och regler för resursskapande på nivå för hanteringsgrupp, prenumeration eller resursgrupp för att säkerställa principinriktning.

[Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) är en Azure-tjänst för att skapa, tilldela och hantera principer. De här principerna tillämpar olika regler och effekter på dina resurser så att resurserna efterlever dina företagsstandarder och serviceavtal. Azure Policy utvärderar dina resurser för bristande efterlevnad med tilldelade principer. Till exempel vill du kanske begränsa SKU-storleken för virtuella datorer i din miljö. När du har implementerat en associerad princip utvärderas nya och befintliga resursers efterlevnad. Med rätt princip kan befintliga resurser bli kompatibla.

## <a name="cross-organization-policy"></a>Organisationsövergripande princip

I takt med att din molnegendom växer till att omfatta många obligatoriska prenumerationer måste du fokusera på en strategi som omfattar hela molnegendomen för att säkerställa principefterlevnad.

Din [prenumerationsdesign](../subscriptions/index.md) måste ta hänsyn till förhållandet mellan principer och organisationens struktur. Utöver att stödja komplex organisering i din prenumerationsdesign kan [Azure-hanteringsgrupper](../../ready/azure-best-practices/scaling-subscriptions.md#manage-multiple-subscriptions) användas för att tilldela Azure Policy-regler över flera prenumerationer.

## <a name="automated-enforcement"></a>Automatiserat framtvingande

Medan standardiserade distributionsmallar är effektiva i liten skala möjliggör [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview) storskalig, standardiserad etablering och distributionsorkestrering av Azure-lösningar. Arbetsbelastningar över flera prenumerationer kan distribueras med konsekventa principinställningar för alla resurser som skapas.

För IT-miljöer där molnbaserade och lokala resurser integreras kan du behöva använda loggnings- och rapporteringssystem för att ge hybridövervakningsfunktioner. Dina driftsövervakningssystem från tredje part eller anpassade sådana har kanske ytterligare funktioner för principframtvingande. För större eller mognare molnegendomar bör du överväga vad som är bästa sätt att integrera dessa system med dina molntillgångar.

## <a name="next-steps"></a>Nästa steg

Principframtvingande är bara en av huvudkomponenterna för infrastruktur som kräver arkitektoniska beslut under en process för att implementera moln. Gå till [översikten över beslutsguider](../index.md) om vill veta mer om alternativa mönster eller modeller som används vid utformningsbeslut för andra typer av infrastrukturer.

> [!div class="nextstepaction"]
> [Beslutsguider för arkitektur](../index.md)
