---
title: Beslutsguide för resurskonsekvens
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Läs mer om resurskonsekvens vid planering av en Azure-migrering.
author: doodlemania2
ms.author: dermar
ms.date: 09/19/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: c32bbb180bc7b78a74681dc4a2554fd449bb21dc
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72547879"
---
# <a name="resource-consistency-decision-guide"></a>Beslutsguide för resurskonsekvens

[Prenumerationsdesign](../subscriptions/index.md) med Azure definierar hur du organiserar dina molntillgångar i förhållande till organisationens struktur, redovisningsmetoder och arbetsbelastningskrav. Utöver den här nivån av struktur kräver åtgärd av organisationens krav gällande styrningsprincip i din molnegendom förmågan att konsekvent organisera, distribuera och hantera resurser i en prenumeration.

![Alternativ för resurskonsekvens ordnade från minst till mest komplext, inriktat med direktlänkar nedan](../../_images/decision-guides/decision-guide-resource-consistency.png)

Hoppa till: [Grundläggande gruppering](#basic-grouping) | [Distributionskonsekvens](#deployment-consistency) | [Principkonsekvens](#policy-consistency) | [Hierarkisk konsekvens](#hierarchical-consistency) | [Automatiserad konsekvens](#automated-consistency)

Beslut om nivån på kraven för din molnegendoms resurskonsekvens drivs huvudsakligen av dessa faktorer: storlek på digital egendom efter migrering, affärs- eller miljökrav som inte passar in särskilt bra i dina befintliga metoder för prenumerationsdesign eller behovet av att framtvinga styrning över tid efter att resurser har distribuerats.

När dessa faktorer blir allt viktigare gäller det även fördelarna med att säkerställa konsekvent distribution, gruppering och hantering av molnbaserade resurser. För att uppnå mer avancerade nivåer av resurskonsekvens för att uppfylla ökande krav krävs mer arbete med automation, verktyg och konsekvensframtvingande. Detta resulterar i ytterligare tidsåtgång för ändringshantering och spårning.

## <a name="basic-grouping"></a>Grundläggande gruppering

I Azure är [resursgrupper](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) en central mekanism för resursorganisering för logisk gruppering av resurser i en prenumeration.

Resursgrupper fungerar som containrar för resurser med gemensam livscykel eller delade hanteringsrestriktioner såsom krav för princip- eller rollbaserad åtkomstkontroll (RBAC). Resursgrupper kan inte kapslas, och resurser kan endast tillhöra en enskild resursgrupp. Alla kontrollplansåtgärder fungerar med alla resurser i en resursgrupp. Till exempel tas alla resurser bort i en resursgrupp om resursgruppen i sig tas bort. Följande frågor kan användas som vägledning för resursgruppshantering:

1. Utvecklas innehållet i resursgruppen tillsammans?
1. Hanteras, uppdateras och övervakas innehållet i resursgruppen tillsammans och av samma personer eller team?
1. Dras innehållet i resursgruppen tillbaka tillsammans?

Om du svarar _nej_ på någon av ovanstående frågor bör resursen i fråga placeras någon annanstans, i en annan resursgrupp.

> [!IMPORTANT]
> Resursgrupper är även landsspecifika, men det är vanligt att resurserna finns i olika regioner i samma resursgrupp eftersom de hanteras tillsammans på det sätt som beskrivs ovan. Mer information om hur du väljer region finns [här](../regions/index.md).

## <a name="deployment-consistency"></a>Distributionskonsekvens

Azure-plattformen bygger ovanpå den grundläggande grupperingsmekanismen för att ge ett system för användning av mallar vid distribution av resurser till molnmiljön. Du kan använda mallar för att skapa konsekvent organisering och namngivningskonventioner när du distribuerar arbetsbelastningar, så att du framtvingar de aspekterna av din resursdistribution och hanteringsdesign.

[Azure Resource Manager-mallar](https://docs.microsoft.com/azure/azure-resource-manager/template-deployment-overview) gör att du upprepade gånger kan distribuera resurser i ett konsekvent tillstånd med hjälp av en förutbestämd struktur för konfiguration och resursgruppering. Resource Manager-mallar hjälper dig att definiera en uppsättning standarder som utgångspunkt för dina distributioner.

Du kan till exempel ha en standardmall för distribution av en webbserverarbetsbelastning som innehåller två virtuella datorer som webbservrar kombinerat med en lastbalanserare för att distribuera trafik mellan servrarna. Du kan sedan återanvända den här mallen för att skapa en strukturellt identisk uppsättning virtuella datorer och en lastbalanserare när den här typen av arbetsbelastning behövs. I det fallet ändrar du bara det distributionsnamn och de IP-adresser som är aktuella.

Du kan även programmatiskt distribuera dessa mallar och integrera dem med dina CI/CD-system.

## <a name="policy-consistency"></a>Principkonsekvens

För att säkerställa att styrningsprinciper tillämpas när resurserna skapas omfattar en del av designen av resursgruppering användning av en gemensam konfiguration vid distribution av resurser.

Genom att kombinera resursgrupper och standardiserade Resource Manager-mallar kan du framtvinga standarder för vilka inställningar som krävs i en distribution och vilka [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview)-regler som tillämpas på varje resursgrupp eller resurs.

Du kan till exempel ha ett krav att alla virtuella datorer som distribueras i prenumerationen ansluter till ett gemensamt undernät som hanteras av ditt centrala IT-team. Du kan skapa en standardmall för att distribuera virtuella arbetsbelastningsdatorer för att skapa en separat resursgrupp för arbetsbelastningen och distribuera nödvändiga virtuella datorer där. Den här resursgruppen skulle ha en principregel för att endast tillåta nätverksgränssnitt i den resursgrupp som ska kopplas till det delade undernätet.

En mer detaljerad beskrivning av framtvingande av dina principbeslut i en molndistribution finns i [Principframtvingande](../policy-enforcement/index.md).

## <a name="hierarchical-consistency"></a>Hierarkisk konsekvens

Med resursgrupper kan du stödja ytterligare nivåer av hierarki i din organisation i prenumerationen samt tillämpa Azure Policy-regler och åtkomstkontroller på resursgruppsnivå. När storleken på din molnegendom växer kan du dock behöva stödja mer komplicerade och prenumerationsöverskridande styrningskrav som kan stödjas med hjälp av Azure Enterprise-avtalets hierarki för företag/avdelning/konto/prenumeration.

[Azure-hanteringsgrupper](https://docs.microsoft.com/azure/governance/management-groups) gör att du kan organisera prenumerationer i mer sofistikerade organisationsstrukturer genom att gruppera prenumerationer i en hierarki som är särskild från Enterprise-avtalets hierarki. Med den här alternativa hierarkin kan du tillämpa mekanismer för åtkomstkontroll och principframtvingande över flera prenumerationer och de resurser som dessa innehåller. Hierarkier för hanteringsgrupper kan användas till att matcha din molnegendoms prenumerationer med krav för åtgärder eller affärsstyrning. Mer information finns i guiden [Prenumerationsbeslut](../subscriptions/index.md).

## <a name="automated-consistency"></a>Automatiserad konsekvens

För stora molndistributioner blir global styrning både viktigare och mer komplex. Det är viktigt att automatiskt tillämpa och framtvinga styrningskrav när du distribuerar resurser samt uppfylla uppdaterade krav för befintliga distributioner.

[Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview) (skisser) gör att organisationer kan stödja global styrning av stora molnegendomar i Azure. Skisser ger fler funktioner än vanliga Azure Resource Manager-mallar och skapar fullständiga distributionsorkestreringar som kan distribuera resurser och tillämpa principregler. Skisser stöder versionshantering, möjligheten att uppdatera alla prenumerationer där skissen användes, samt möjligheten att låsa distribuerade prenumerationer för att undvika att resurser skapas eller ändras utan behörighet.

Dessa distributionspaket gör att IT och utvecklingsteam snabbt kan distribuera nya arbetsbelastningar och nätverkstillgångar som uppfyller föränderliga krav på organisationsprinciper. Skisser kan även integreras i CI/CD-pipelines för att tillämpa ändrade styrningsstandarder på distributioner när de uppdateras.

## <a name="next-steps"></a>Nästa steg

Resurskonsekvens är bara en av huvudkomponenterna för infrastruktur som kräver arkitektoniska beslut under en process för att implementera moln. Gå till [översikten över beslutsguider](../index.md) om vill veta mer om alternativa mönster eller modeller som används vid utformningsbeslut för andra typer av infrastrukturer.

> [!div class="nextstepaction"]
> [Beslutsguider för arkitektur](../index.md)
