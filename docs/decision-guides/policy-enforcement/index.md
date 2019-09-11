---
title: Beslutsguide för principframtvingande
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Läs mer om prenumerationer på principframtvingande som en grundläggande designprioritet i Azure-migreringar.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 3c519de24d6c7ac83240d1b1e14b0a21c67f67df
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817663"
---
# <a name="policy-enforcement-decision-guide"></a>Beslutsguide för principframtvingande

Att definiera en organisationsprincip gör ingen nytta såvida den inte kan framtvingas i organisationen. En viktig aspekt av att planera molnmigreringar är att avgöra det bästa sättet att kombinera verktyg som tillhandahålls av molnplattformen i dina befintliga IT-processer för att maximera principefterlevnad i hela molnegendomen.

![Alternativ för principframtvingande ordnade från minst till mest komplext, inriktat med direktlänkar nedan](../../_images/discovery-guides/discovery-guide-policy-enforcement.png)

Hoppa till: [Rekommenderade baslinjemetoder](#baseline-recommended-practices) | [Övervakning av principefterlevnad](#policy-compliance-monitoring) | [Principframtvingande](#policy-enforcement) | [Organisationsövergripande princip](#cross-organization-policy) | [Automatiserat framtvingande](#automated-enforcement)

Allt eftersom din molnegendom växer ställs du inför ett motsvarande behov att upprätthålla och framtvinga principer över en större mängd resurser och prenumerationer. När din egendom blir större och organisationens principkrav ökar behöver omfattningen av dina processer för principframtvingande utökas för att säkerställa konsekvent principefterlevnad och snabb identifiering av överträdelser.

Plattformstillhandahållna mekanismer för principframtvingande på resurs- eller prenumerationsnivå räcker oftast för mindre molnegendomar. Större distributioner motiverar en större omfattning av framtvingande och kan behöva utnyttja mer sofistikerade mekanismer för framtvingande som inbegriper distributionsstandarder, gruppering och organisering av resurser samt integrering av principframtvingande med dina loggnings- och rapporteringssystem.

De huvudsakliga faktorerna för att fastställa omfattningen av dina processer för principframtvingande är organisationens [krav för molnstyrning](/azure/architecture/cloud-adoption/governance/overview), storleken och egenskaperna hos din molnegendom samt hur organisationen speglas i din [prenumerationsdesign](../subscriptions/index.md). Både en ökning av storleken på din egendom eller ett högre behov av att centralt hantera principframtvingande kan motivera en ökning av omfattning för framtvingande.

## <a name="baseline-recommended-practices"></a>Rekommenderade baslinjemetoder

För enkla molndistributioner och sådana med en enda prenumeration kan många företagsprinciper framtvingas med hjälp av funktioner som är inbyggda i resurser och prenumerationer i Azure. Konsekvent användning av de mönster som beskrivs i [beslutsguiderna](../index.md) för Cloud Adoption Framework kan hjälpa till att upprätta en baslinjenivå av principefterlevnad utan specifik investering i principframtvingande. Dessa funktioner omfattar:

- [Distributionsmallar](../resource-consistency/index.md) kan etablera resurser med standardiserad struktur och konfiguration.
- [Taggnings- och namngivningsstandarder](../resource-tagging/index.md) kan hjälpa till att organisera drift samt stödja redovisnings- och affärskrav.
- Trafikhantering och nätverksbegränsningar kan implementeras via [programvarudefinierade nätverk](../software-defined-network/index.md).
- [Rollbaserad åtkomstkontroll](../identity/index.md) kan skydda och isolera dina molnresurser.

Påbörja planeringen av framtvingande av molnprincip genom att undersöka hur tillämpningen av de standardmönster som beskrivs i dessa guider kan hjälpa dig att uppfylla organisationskraven.

## <a name="policy-compliance-monitoring"></a>Övervakning av principefterlevnad

Ett första steg bortom att helt enkelt förlita sig på de mekanismen för principframtvingande som tillhandahålls av Azure-plattformen är att säkerställa förmågan att kontrollera huruvida molnbaserade program och tjänster efterlever organisationsprincipen. Detta omfattar implementering av meddelandefunktioner för avisering av ansvariga parter om en resurs slutar efterleva principen. Effektiv [loggning och rapportering](../log-and-report/index.md) av efterlevnadsstatus för dina molnarbetsbelastningar är en mycket viktig del av en företagsstrategi för principframtvingande.

Allt eftersom din molnegendom växer kan ytterligare verktyg såsom [Azure Security Center](/azure/security-center) ge integrerad säkerhet och hotidentifiering samt hjälpa till att tillämpa centraliserad principhantering och avisering för båda dina lokala och molnbaserade tillgångar.

## <a name="policy-enforcement"></a>Policyframtvingande

I Azure kan du tillämpa konfigurationsinställningar och regler för resursskapande på nivå för hanteringsgrupp, prenumeration eller resursgrupp för att säkerställa principinriktning.

[Azure Policy](/azure/governance/policy/overview) är en Azure-tjänst för att skapa, tilldela och hantera principer. De här principerna tillämpar olika regler och effekter på dina resurser så att resurserna efterlever dina företagsstandarder och serviceavtal. Azure Policy utvärderar dina resurser för bristande efterlevnad med tilldelade principer. Till exempel vill du kanske begränsa SKU-storleken för virtuella datorer i din miljö. När en motsvarande princip har implementerats skulle nya och befintliga resurser utvärderas för efterlevnad. Med rätt princip kan befintliga resurser bli kompatibla.

## <a name="cross-organization-policy"></a>Organisationsövergripande princip

Allt eftersom din molnegendom växer till att omfatta många prenumerationer som kräver framtvingande behöver du fokusera på en framtvingandestrategi för hela molnegendomen för att säkerställa principefterlevnad.

Din [prenumerationsdesign](../subscriptions/index.md) behöver ta med principens relation till din organisationsstruktur i beräkningen. Utöver att stödja komplex organisering i din prenumerationsdesign kan [Azure-hanteringsgrupper](../../ready/considerations/scaling-subscriptions.md#managing-multiple-subscriptions) användas för att tilldela Azure Policy-regler över flera prenumerationer.

## <a name="automated-enforcement"></a>Automatiserat framtvingande

Medan standardiserade distributionsmallar är effektiva i liten skala möjliggör [Azure Blueprints](/azure/governance/blueprints/overview) storskalig, standardiserad etablering och distributionsorkestrering av Azure-lösningar. Arbetsbelastningar över flera prenumerationer kan distribueras med konsekventa principinställningar för alla resurser som skapas.

För IT-miljöer där molnbaserade och lokala resurser integreras kan du behöva använda loggnings- och rapporteringssystem för att ge hybridövervakningsfunktioner. Dina driftsövervakningssystem från tredje part eller anpassade sådana har kanske ytterligare funktioner för principframtvingande. För större eller mognare molnegendomar bör du överväga vad som är bästa sätt att integrera dessa system med dina molntillgångar.

## <a name="next-steps"></a>Nästa steg

Principframtvingande är bara en av huvudkomponenterna för infrastruktur som kräver arkitektoniska beslut under en process för att implementera moln. Gå till [översikten över beslutsguider](../index.md) om vill veta mer om alternativa mönster eller modeller som används vid utformningsbeslut för andra typer av infrastrukturer.

> [!div class="nextstepaction"]
> [Beslutsguider för arkitektur](../index.md)
