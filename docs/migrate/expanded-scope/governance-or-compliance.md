---
title: Strategi för styrning eller efterlevnad
description: Strategi för styrning eller efterlevnad
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 17952dc4c3ff28f2fcfe1a378a9efb969d65925b
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76803134"
---
# <a name="governance-or-compliance-strategy"></a>Strategi för styrning eller efterlevnad

När styrning eller efterlevnad krävs under en migrering krävs ytterligare omfång. Följande riktlinjer ökar kapaciteten hos [migrationsguiden för Azure](../azure-migration-guide/index.md) för att hantera styrnings- eller efterlevnadskrav på olika sätt.

## <a name="general-scope-expansion"></a>Allmän omfångsutökning

Obligatoriska åtgärder påverkas mest när styrning eller efterlevnad krävs. Ytterligare justeringar kan krävas under utvärdering, migrering och optimering.

## <a name="suggested-prerequisites"></a>Föreslagna förutsättningar

Konfigurationen av den grundläggande Azure-miljön kan ändras avsevärt vid integrering av styrnings- och efterlevnadskrav. För att förstå hur dessa förutsättningar ändras är det viktigt att förstå kravens beskaffenhet. Innan du påbörjar en migrering som kräver styrning eller efterlevnad bör du välja och implementera en metod i molnmiljön. De följande är ett avancerade metoder som ofta används vid migrering:

**Gemensam styrnings metod:** För de flesta organisationer är [styrnings modellen för moln införande i ramverket](../../govern/guides/index.md) ett tillräckligt tillvägagångs sätt som består av en minimal implementering av en praktisk produkt (MVP), följt av riktade iterationer av styrnings period för att åtgärda konkreta risker som identifieras i implementerings planen. Den här metoder har minsta nödvändiga verktyg för att etablera en konsekvent styrning så att teamet kan förstå verktygen. Därefter utvecklas verktygen för att bemöta vanliga styrningsproblem.

**ISO 27001-överensstämmelse ritningar:** För kunder som måste följa ISO-standardkompatibiliteten kan de [skiss exempel för delade tjänster i iso 27001](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-shared/index) fungera som en effektivare MVP för att ge bättre styrnings styrnings begränsningar tidigare i den iterativa processen. [Exemplet ISO 27001 App Service Environment/SQL Database](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-ase-sql-workload) utvecklar skissen och kartlägger kontroller samt distribuerar en gemensam arkitektur för en programmiljö. Efter hand som ytterligare skisser publiceras kommer de att visas här också.

**Virtuellt Data Center:** En mer robust start punkt för styrning kan krävas. I sådant fall bör du överväga [Azure Virtual Datacenter (VDC)](../../reference/vdc.md). Den här metoden rekommenderas ofta för implementeringar i företagsskala, särskilt för implementeringar som överstiger 10 000 tillgångar. Det är också det naturliga valet i komplexa styrningsscenarier när något av följande krävs: omfattande krav på efterlevnad med tredje part, djupgående domänexpertis eller paritet med mogna IT-styrningsprinciper och efterlevnadskrav.

### <a name="partnership-option-to-complete-prerequisites"></a>Partnerskapsalternativ för att uppfylla förhandskrav

**Microsoft-tjänster:** Microsoft Services tillhandahåller lösnings erbjudanden som kan anpassas till moln implementerings ramverkets styrnings modell, uppfyllande ritningar eller virtuella Data Center alternativ för att säkerställa den lämpligaste styrningen eller efterlevnaden. Använd lösningen [Secure Cloud Insights (SCI)](https://download.microsoft.com/download/C/7/C/C7CEA89D-7BDB-4E08-B998-737C13107361/Secure_Cloud_Insights_Datasheet_EN_US.pdf) som etablerar en datadriven bild av en kunddistribution i Azure och validera kundens Azure-övergångsmognad medan du identifierar optimeringen av befintliga distributionsarkitekturer och skyddar dig mot risker mot styrningssäkerheten och tillgängligheten. Baserat på kundinsikter bör du inleda med följande metoder:

- **Cloud Foundation:** Etablera kundens centrala design, mönster och styrnings arkitektur med [Hybrid Cloud Foundation (HCF)](https://download.microsoft.com/download/D/8/7/D872DFD0-1C46-4145-95E4-B5EAB2958B96/Hybrid_Cloud_Foundation_Datasheet_EN_US.pdf) lösnings erbjudande. Mappa kundens krav till den lämpligaste referens arkitekturen. Implementera en minimal användbar produkt som består av delade tjänster och IaaS-arbetsbelastningar.
- **Cloud modernisering:** Använd [Cloud modernisering](https://download.microsoft.com/download/3/7/3/373F90E3-8568-44F3-B096-CD9C1CD28AB7/Cloud_Modernization_Datasheet_EN_US.pdf) -lösningen som en omfattande metod för att flytta program, data och infrastruktur till ett företags klart moln, samt för att optimera och modernisera efter moln distribution.
- **Förnya med molnet:** Engagera kunden genom en innovativ och unik lösning [för CCoE-lösning (Cloud Center of expert)](https://download.microsoft.com/download/F/8/B/F8BBE4BD-E5F8-4DFB-82F7-C0A4E17051BB/Cloud_Center_of_Excellence_Datasheet_EN_US.pdf) som skapar en modern IT-organisation för att möjliggöra rörlighet i stor skala med DevOps samtidigt som kontrollen är klar. Implementerar en smidig metod för att samla in verksamhetsbehov, återanvända distributionspaket med anpassad säkerhet, efterlevnad och tjänsthanteringsprinciper. Azure-plattformen förblir anpassad till driftsrutinerna.

## <a name="assess-process-changes"></a>Utvärdera processändringar

Under utvärderingen krävs ytterligare beslut för att anpassa lösningen till den nödvändiga styrningsmetoden. Molnstyrningsteamet bör ge alla medlemmar i molnimplementeringsteamet eventuella policyinstruktioner, arkitekturvägledningar eller styrnings-och efterlevnadskrav innan arbetsbelastningen utvärderas.

### <a name="suggested-action-during-the-assess-process"></a>Föreslagna åtgärder under utvärderingsprocessen

Kraven på styrning och bedömning av efterlevnad är för kundspecifika för att kunna ge allmänna riktlinjer för utvärderingsstegen. Processen bör dock innehålla uppgifter och tidsallokeringar för "justering av krav på efterlevnad/styrning". För att förstå dessa krav bättre kan du följa följande länkar:

För en djupare förståelse för styrningen, se [översikten Fem discipliner för molnstyrning](../../govern/governance-disciplines.md). Det här avsnittet av Ramverk för molnimplementering innehåller även mallar för att dokumentera principerna, vägledningen och kraven för var och en av de fem avsnitten:

- [Kostnadshantering](../../govern/cost-management/template.md)
- [Säkerhetsbaslinje](../../govern/security-baseline/template.md)
- [Resurs konsekvens].. /.. /govern/resource-consistency/template.md)
- [Identitets bas linje].. /.. /govern/identity-baseline/template.md)
- [Distributionsacceleration](../../govern/deployment-acceleration/template.md)

Vägledning om hur du utvecklar styrningsriktlinjer baserade på styrningsmodellen för Ramverk för molnimplementering finns i [Implementera en strategi för molnstyrning](../../govern/corporate-policy.md).

## <a name="optimize-and-promote-process-changes"></a>Optimera och flytta upp processändringar

Under optimerings-och marknadsförings processerna investerar shluld för moln styrning tid för att testa och validera efterlevnad av styrning och efterlevnad. Det här steget är också ett lämpligt tillfälle att mata in processer som molnstyrningsteamet kan omvandla till mallar som kan [accelerera distributionen](../../govern/deployment-acceleration/index.md) ytterligare för framtida projekt.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Föreslagen åtgärd i samband med optimering och uppflyttning

Under den här processen bör projekt planen omfatta tidsallokeringar för moln styrnings teamet för att utföra en kompatibilitetskontroll för varje arbets belastning som planeras för produktions befordran.

## <a name="next-steps"></a>Nästa steg

Som det sista objektet i den [expanderade check listan](./index.md), gå tillbaka till check listan och utvärdera eventuella ytterligare omfångs krav för migreringen.

> [!div class="nextstepaction"]
> [Utökad checklista](./index.md)
