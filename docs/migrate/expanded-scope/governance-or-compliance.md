---
title: Strategi för styrning eller efterlevnad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Strategi för styrning eller efterlevnad
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 5a5becd757d1bca3f10b30297f4c502b49a659c4
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/11/2019
ms.locfileid: "70905603"
---
# <a name="governance-or-compliance-strategy"></a>Strategi för styrning eller efterlevnad

När styrning eller efterlevnad krävs under en migrering krävs ytterligare omfång. Följande riktlinjer ökar kapaciteten hos [migrationsguiden för Azure](../azure-migration-guide/index.md) för att hantera styrnings- eller efterlevnadskrav på olika sätt.

## <a name="general-scope-expansion"></a>Allmän omfångsutökning

Obligatoriska åtgärder påverkas mest när styrning eller efterlevnad krävs. Ytterligare justeringar kan krävas under utvärdering, migrering och optimering.

## <a name="suggested-prerequisites"></a>Föreslagna förutsättningar

Konfigurationen av den grundläggande Azure-miljön kan ändras avsevärt vid integrering av styrnings- och efterlevnadskrav. För att förstå hur dessa förutsättningar ändras är det viktigt att förstå kravens beskaffenhet. Innan du påbörjar en migrering som kräver styrning eller efterlevnad bör du välja och implementera en metod i molnmiljön. De följande är ett avancerade metoder som ofta används vid migrering:

**Gemensam styrningsmetod:** För de flesta organisationer är [styrningsmodellen molnimplementeringsramverk](../../governance/journeys/index.md) en tillräcklig metod som består av en implementering av en minsta användbar produkt (MVP), följt av riktade iterationer av styrningsmognad för att hantera konkreta risker som har identifierats i övergångsplanen. Den här metoder har minsta nödvändiga verktyg för att etablera en konsekvent styrning så att teamet kan förstå verktygen. Därefter utvecklas verktygen för att bemöta vanliga styrningsproblem.

**ISO 27001-efterlevnadsskiss:** För kunder som måste följa ISO-standarder kan [exempelskissen för ISO 27001 delade tjänster](/azure/governance/blueprints/samples/iso27001-shared/index) fungera som en effektivare MVP för att ge bättre styrningsbegränsningar tidigare i den iterativa processen. [Exemplet ISO 27001 App Service Environment/SQL Database](/azure/governance/blueprints/samples/iso27001-ase-sql-workload) utvecklar skissen och kartlägger kontroller samt distribuerar en gemensam arkitektur för en programmiljö. Efter hand som ytterligare skisser publiceras kommer de att visas här också.

**Virtuellt datacenter:** En mer stabil startpunkt för styrningen kan krävas. I sådant fall bör du överväga [Azure Virtual Datacenter (VDC)](https://docs.microsoft.com/azure/architecture/vdc). Den här metoden rekommenderas ofta för implementeringar i företagsskala, särskilt för implementeringar som överstiger 10 000 tillgångar. Det är också det naturliga valet i komplexa styrningsscenarier när något av följande krävs: omfattande krav på efterlevnad med tredje part, djupgående domänexpertis eller paritet med mogna IT-styrningsprinciper och efterlevnadskrav.

### <a name="partnership-option-to-complete-prerequisites"></a>Partnerskapsalternativ för att uppfylla förhandskrav

**Microsoft Services:** Microsoft Services erbjuder lösningar som kan anpassa alternativ för styrningsmodellen Ramverk för molnimplementering, efterlevnadsskisser eller virtuella datacenter så att du får den lämpligaste styrnings- eller efterlevnadsmodellen. Använd lösningen [Secure Cloud Insights (SCI)](https://download.microsoft.com/download/C/7/C/C7CEA89D-7BDB-4E08-B998-737C13107361/Secure_Cloud_Insights_Datasheet_EN_US.pdf) som etablerar en datadriven bild av en kunddistribution i Azure och validera kundens Azure-övergångsmognad medan du identifierar optimeringen av befintliga distributionsarkitekturer och skyddar dig mot risker mot styrningssäkerheten och tillgängligheten. Baserat på kundinsikter bör du inleda med följande metoder:

- **Cloud Foundation:** Etablera kundens centrala Azure-design, -mönster och -styrningsarkitektur med lösningen [Hybrid Cloud Foundation (HCF)](https://download.microsoft.com/download/D/8/7/D872DFD0-1C46-4145-95E4-B5EAB2958B96/Hybrid_Cloud_Foundation_Datasheet_EN_US.pdf). Kartlägg kundens behov och avgör vilken referensarkitektur som passar bäst. Implementera en minimal användbar produkt som består av delade tjänster och IaaS-arbetsbelastningar.
- **Molnmodernisering:** Använd [molnmoderniseringslösningen](https://download.microsoft.com/download/3/7/3/373F90E3-8568-44F3-B096-CD9C1CD28AB7/Cloud_Modernization_Datasheet_EN_US.pdf) som en heltäckande metod för att flytta program, data och infrastruktur till ett företagsredo moln, samt för att optimera och modernisera i molnet.
- **Förnya med molnet:** Engagera kunden genom en innovativ och unik lösning [för CCoE-lösning (Cloud Center of expert)](https://download.microsoft.com/download/F/8/B/F8BBE4BD-E5F8-4DFB-82F7-C0A4E17051BB/Cloud_Center_of_Excellence_Datasheet_EN_US.pdf) som skapar en modern IT-organisation för att möjliggöra rörlighet i stor skala med DevOps samtidigt som kontrollen är klar. Implementerar en smidig metod för att samla in verksamhetsbehov, återanvända distributionspaket med anpassad säkerhet, efterlevnad och tjänsthanteringsprinciper. Azure-plattformen förblir anpassad till driftsrutinerna.

## <a name="assess-process-changes"></a>Utvärdera ändringar i processen

Under utvärderingen krävs ytterligare beslut för att anpassa lösningen till den nödvändiga styrningsmetoden. Molnstyrningsteamet bör ge alla medlemmar i molnimplementeringsteamet eventuella policyinstruktioner, arkitekturvägledningar eller styrnings-och efterlevnadskrav innan arbetsbelastningen utvärderas.

### <a name="suggested-action-during-the-assess-process"></a>Föreslagna åtgärder under utvärderingsprocessen

Kraven på styrning och bedömning av efterlevnad är för kundspecifika för att kunna ge allmänna riktlinjer för utvärderingsstegen. Det rekommenderas dock att processen omfattar uppgifter och tidstilldelningar för "justeringar i förhållande till efterlevnads-/styrningskrav”. För att förstå dessa krav bättre kan du följa följande länkar:

För en djupare förståelse för styrningen, se [översikten Fem discipliner för molnstyrning](/azure/architecture/cloud-adoption/governance/governance-disciplines). Det här avsnittet av Ramverk för molnimplementering innehåller även mallar för att dokumentera principerna, vägledningen och kraven för var och en av de fem avsnitten:

- [Kostnadshantering](/azure/architecture/cloud-adoption/governance/cost-management/template)
- [Säkerhetsbaslinje](/azure/architecture/cloud-adoption/governance/security-baseline/template)
- [Resurskonsekvens](/azure/architecture/cloud-adoption/governance/resource-consistency/template)
- [Identitetsbaslinje](/azure/architecture/cloud-adoption/governance/identity-baseline/template)
- [Distributionsacceleration](/azure/architecture/cloud-adoption/governance/deployment-acceleration/template)

Vägledning om hur du utvecklar styrningsriktlinjer baserade på styrningsmodellen för Ramverk för molnimplementering finns i [Implementera en strategi för molnstyrning](/azure/architecture/cloud-adoption/governance/corporate-policy).

## <a name="optimize-and-promote-process-changes"></a>Optimera och höja upp processändringar

Under optimerings- och uppflyttningsprocesserna rekommenderar vi att molnstyrningsteamet investerar tid i att testa och kontrollera överensstämmelse med styrnings- och efterlevnadskrav. Det här steget är också ett lämpligt tillfälle att mata in processer som molnstyrningsteamet kan omvandla till mallar som kan [accelerera distributionen](/azure/architecture/cloud-adoption/governance/deployment-acceleration) ytterligare för framtida projekt.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Föreslagna åtgärder i samband med optimering och befordran

Under den här processen rekommenderar vi att projektplanen avsätter tid molnstyrningsteamet så att de kan utföra en efterlevnadsgranskning för varje arbetsbelastning som flyttas upp.

## <a name="next-steps"></a>Nästa steg

Den sista punkten på den [utökade checklistan](./index.md) är att gå tillbaka till checklistan och överväga eventuella omfångsbehov som migrationen kan ha.

> [!div class="nextstepaction"]
> [Utökad checklista](./index.md)
