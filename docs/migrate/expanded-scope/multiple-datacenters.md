---
title: Flera datacenter
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Flera datacenter
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b2491d349628d2c9640097ddd2c94b79505a0921
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024795"
---
# <a name="multiple-datacenters"></a>Flera datacenter

En migrering omfattar ofta flera datacenter. Följande riktlinjer utökar [migrationsguiden för Azure](../azure-migration-guide/index.md) till att hantera flera datacenter.

## <a name="general-scope-expansion"></a>Allmän omfångsutökning

Det mesta av arbetet som krävs för denna utökning sker under förutsättnings-, utvärderings- och optimeringsprocesserna för migreringen.

## <a name="suggested-prerequisites"></a>Föreslagna förutsättningar

Innan migreringen skapar du epos i projekthanteringsverktyget för att representera varje datacenter som ska migreras. Det är sedan viktigt att förstå de verksamhetsresultat och motivationer som gör migreringen nödvändig. Dessa motivationer kan användas för att ordna prioriteringslistan med epos (eller datacenter). Om migreringen till exempel drivs av en önskan att lämna datacenter innan avtalen måste förnyas ska varje epos prioriteras baserat på när avtalen måste förnyas.

Inom varje epos hanteras de arbetsbelastningar som ska utvärderas som funktioner. Varje tillgång inom arbetsbelastningen hanteras som en användarberättelse. Det arbete som krävs för att utvärdera, migrera, optimera, befordra, skydda och hantera varje tillgång representeras som uppgifter för varje tillgång.

Sprintar eller iterationer skulle sedan bestå av en serie uppgifter som krävs för att migrera tillgångarna och användarberättelserna som fastställts av teamet för molnimplementering. Versioner skulle sedan bestå av en eller flera arbetsbelastningar eller funktioner som kan befordras till produktionsanvändning.

## <a name="assess-process-changes"></a>Utvärdera ändringar i processen

Den största ändringen av utvärderingsprocessen vid en utökning för att hantera flera datacenter rör den korrekta registreringen och prioriteringen av arbetsbelastningar och beroenden mellan datacenter.

### <a name="suggested-action-during-the-assess-process"></a>Föreslagna åtgärder under utvärderingsprocessen

**Utvärdera beroenden mellan datacenter:** [Verktygen för beroendevisualisering i Azure Migrate](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization) kan underlätta identifieringen av beroenden. Att använda denna verktygsuppsättning innan migrering är ett bra allmänt regelverk. När det gäller komplexitet på global nivå är det dock ett nödvändigt steg i utvärderingsprocessen. Genom [beroendegruppering](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies) kan visualiseringen underlätta identifieringen av IP-adresser och portar för alla tillgångar som krävs för att hantera arbetsbelastningen.

> [!IMPORTANT]
> Två viktiga kommentarer: Först så krävs en ämnesexpert med förståelse för tillgångsplacering och IP-adresscheman för att identifiera tillgångar som ligger i sekundära datacenter. Sedan är det viktigt att utvärdera både underordnade beroenden och klienter visuellt för att förstå dubbelriktade beroenden.

## <a name="migrate-process-changes"></a>Migrering av processändringar

Migrering av flera datacenter liknar processen för att slå samman datacenter. Efter migreringen blir molnet den enhetliga datacenterlösningen för flera olika tillgångar. Den troligaste omfattningsutökningen under migreringsprocessen är valideringen och tilldelningen av IP-adresser.

### <a name="suggested-action-during-the-migrate-process"></a>Föreslagna åtgärder under migreringsprocessen

Följande aktiviteter har stor påverkan på framgången för en molnmigrering:

- **Utvärdera nätverkskonflikter:** Vid konsolidering av datacenter till en molnleverantör är det sannolikt att det skapas nätverks-, DNS- eller andra konflikter. Under migreringen är det viktigt att testa för att upptäcka konflikter och undvika avbrott i produktionssystem som körs i molnet.
- **Uppdatera routingtabeller:** Ofta krävs ändringar i routingtabellerna vid konsolidering av nätverk eller datacenter.

## <a name="optimize-and-promote-process-changes"></a>Optimera och flytta upp processändringar

Under optimering kan ytterligare testning krävas.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Föreslagna åtgärder i samband med optimering och befordran

Innan befordran är det viktigt att tillhandahålla ytterligare nivåer av testning under omfångsutökningen. Under testning är det viktigt att testa för att upptäcka routingproblem och andra konflikter. Det är även viktigt att isolera det överförda programmet och testa om för att validera att alla beroenden migrerats till molnet. I detta fall innebär isolering att den överförda miljön separeras från produktionsnätverken. Det kan avslöja förbisedda tillgångar som fortfarande körs lokalt.

## <a name="secure-and-manage-process-changes"></a>Skydda och hantera processändringar

Processer för att skydda och hantera processändringar påverkas inte av denna omfångsutökning.

## <a name="next-steps"></a>Nästa steg

Gå tillbaka till [checklistan för utökat omfång](./index.md) och se till att din migreringsmetod är helt anpassad till kraven.

> [!div class="nextstepaction"]
> [Checklista för utökat omfång](./index.md)
