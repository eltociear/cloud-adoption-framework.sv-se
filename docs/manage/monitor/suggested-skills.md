---
title: Kompetens beredskap för moln övervakning
description: Kompetens beredskap för moln övervakning
author: BrianBlanchard
ms.author: magoedte
ms.date: 03/23/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 128aa99a978f70525e2279868d2317dec8c965cb
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433584"
---
<!-- cSpell:ignore kusto ITIL -->

# <a name="skills-readiness-for-cloud-monitoring"></a>Kompetens beredskap för moln övervakning

Under plan fasen av migreringen är målet att utveckla de planer som krävs för att vägleda implementeringen. Planerna måste också innehålla hur du ska använda arbets belastningarna innan de övergår till eller släpps i produktion, och inte efteråt. Affärs intressenter förväntar sig värdefulla tjänster och de förväntar sig dem utan avbrott. IT-personalen inser att de behöver lära sig nya kunskaper och anpassas så att de kan utnyttja de integrerade Azure-tjänsterna för att effektivt kunna övervaka resurser i Azure och hybrid miljöer.

De nödvändiga kunskaperna kan utvecklas snabbare med följande utbildningsvägar:

- Introduktion till [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/management/overview) diskuterar grundläggande koncept för hantering och distribution av Azure-resurser. IT-personalen som hanterar övervaknings miljön i företaget bör förstå hanterings omfång, rollbaserad åtkomst kontroll (RBAC) med. Azure Resource Manager mallar och hantering av resurser med hjälp av Azure CLI och Azure PowerShell.

- Lär dig hur du skyddar resurser med hjälp av princip, rollbaserad åtkomst kontroll och andra Azure-tjänster genom att se [implementera säkerhet för resurs hantering i Azure](https://docs.microsoft.com//learn/paths/implement-resource-mgmt-security).

- Introduktion till [Azure policy](https://docs.microsoft.com/azure/governance/policy/overview) hjälper dig att lära dig hur du kan använda Azure policy för att skapa, tilldela och hantera principer. Azure Policy kan distribuera och konfigurera Azure Monitors agenter, aktivera övervakning med Azure Monitor for VMs och Azure Security Center, distribuera diagnostikinställningar, granska gäst konfigurations inställningar med mera.

- Introduktion till [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli?view=azure-cli-latest) (CLI), som är vår plattforms oberoende kommando rads upplevelse för att hantera Azure-resurser. Granska även introduktion till [Azure PowerShell](https://docs.microsoft.com/powershell/azure/?view=azps-3.6.1). LinkedIn-erbjudanden, som en del av [Azures utbildnings verktyg](https://www.linkedin.com/learning/learning-azure-management-tools)för utbildning i nybörjare, som omfattar Azure CLI och PowerShell-programmeringsspråk:

  - [Använd Azure CLI](https://www.linkedin.com/learning/learning-azure-management-tools/use-the-azure-cli).
  - [Komma igång med Azure PowerShell](https://www.linkedin.com/learning/learning-azure-management-tools/understand-azure-powershell)

- Lär dig hur du skriver [logg frågor i Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/log-query/get-started-queries).  Frågespråket för Kusto är den primära resurs som används för att skriva Azure Monitor logg frågor för att utforska och analysera loggdata mellan insamlade data från Azure och hybrid resurs program beroenden, inklusive Live-programmet.

- Förstå hur [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) hjälper dig att Visa tillgänglighet och prestanda för dina program och tjänster tillsammans från en och samma plats. Pluralsight erbjuder följande kurser för att hjälpa:

  - [Microsoft Azure övervakning och hantering av IaaS](https://www.pluralsight.com/courses/azure-iaas-monitoring-management-getting-started) hjälper dig att lära dig hur du använder Azure Monitor för att utföra grundläggande övervakning av arbets belastningar som körs på IaaS.

  - [Övervakning av Microsoft Azure resurser och arbets belastningar](https://www.pluralsight.com/courses/microsoft-azure-resources-workloads-monitoring) hjälper dig att lära dig hur du använder Microsoft Azure övervaknings verktyg för att övervaka Azure-nätverk (och lokal-resurser).

  - [Microsoft Azure DevOps-tekniker: optimera feedback-mekanismer](https://www.pluralsight.com/courses/microsoft-azure-optimize-feedback-mechanisms) hjälper dig att förbereda dig för att använda Azure Monitor, inklusive Application Insights och Log Analytics för att övervaka och optimera dina webb program.

  - [Microsoft Azure Database Monitoring Spelbok](https://www.pluralsight.com/courses/microsoft-azure-database-playbook-monitoring) hjälper dig att lära dig hur du implementerar och använder övervakning av Azure SQL Database, Azure SQL Data Warehouse och Azure Cosmos dB.

- Med [Azure-båge för-servrar](https://docs.microsoft.com/azure/azure-arc/servers/overview)kan du lära dig hur du hanterar dina Windows-och Linux-datorer utanför Azure på samma sätt som du hanterar interna virtuella Azure-datorer.

## <a name="deeper-skills-exploration"></a>Fördjupning

Utöver de här inledande alternativen finns en mängd andra inlärningsalternativ.

### <a name="typical-mappings-of-cloud-it-roles"></a>Typiska mappningar av moln-IT-roller

Microsoft och våra partner har en mängd alternativ för alla målgrupper som gör det möjligt att utöka dina kunskaper med Azure-tjänster:

- [Microsoft IT Pro karriär Center](https://www.microsoft.com/itpro): fungerar som en kostnads fri online-resurs för att kartlägga din moln karriärs väg. Få tips från branschexperter för din molnroll och vilka kunskaper du behöver för att komma dit. Följ ett utbildningsprogram i din egen takt för att bygga de kunskaper du behöver för att hålla dig uppdaterad.

Omvandla dina kunskaper om Azure till ett officiellt erkännande med vår [certifieringsutbildning och examinering för Microsoft Azure]( https://www.microsoft.com/learning/azure-certification.aspx).

## <a name="azure-devops-and-project-management"></a>Azure-DevOps och projekt hantering

Hybrid moln miljön stör den med odefinierade roller, ansvars områden och aktiviteter. Organisationerna måste gå över till moderna tjänste hanterings metoder, inklusive Agile-och DevOps-metoder, för att bättre möta de senaste affärs företagens omvandlings-och optimerings behov på ett effektiviserat och effektivt sätt.

Som en del av migreringen till en plattform för moln övervakning behöver IT-teamet som ansvarar för att hantera övervakning i företaget ha smidig utbildning och deltagande i DevOps-aktiviteter. Detta omfattar även följande *utveckling* i DevOps genom att ta krav och omvandla flexibla Agile-krav för att leverera minimalt lönsamma övervaknings lösningar som är raffinerade iterativa och i linje med affärs behov. För käll kontroll för att hantera de iterativa övervaknings lösnings paketen och annan relaterad säkerhet, ansluter du Azure DevOps Server-projektet med en GitHub Enterprise Server-lagringsplats. Detta ger en länk mellan GitHub incheckningar och pull-begäranden till arbets objekt. Du kan använda GitHub Enterprise för utveckling i stöd för kontinuerlig övervakning av integrering och distribution, medan Azure-kort används för att planera och spåra ditt arbete.

Läs mer i följande avsnitt:

- [Kom igång med Azure DevOps](https://docs.microsoft.com/learn/modules/get-started-with-devops).

- [Lär dig mer om DevOps Dojo White bälte Foundation](https://docs.microsoft.com/learn/paths/devops-dojo-white-belt-foundation)

- [Utveckla dina DevOps-metoder](https://docs.microsoft.com/learn/paths/evolve-your-devops-practices)

- [Automatisera dina distributioner med Azure DevOps](https://docs.microsoft.com/learn/paths/automate-deployments-azure-devops)

## <a name="other-considerations"></a>Andra överväganden

Kunder har ofta svårt att hantera, underhålla och leverera det förväntade företaget (och IT-organisationen) för de tjänster som den debiteras med leverans. Övervakningen anses vara kärnan till att hantera infrastrukturen och verksamheten, med fokus på att mäta kvaliteten på tjänsten och kund upplevelsen.  För att uppnå dessa mål kan du lägga grunden med ITSM tillsammans med DevOps, som hjälper övervaknings teamet att bli vuxen hur de hanterar, levererar och stöder övervaknings tjänsten. Genom att anta ett ITSM-ramverk kan övervaknings teamet fungera som en leverantör och få igenkänning som en betrodd affärs möjlighet genom att anpassa sig till organisationens strategiska mål.

Läs följande om du vill förstå de uppdateringar som har gjorts i de populäraste ITSM Framework [ITIL v4 och data för molnbaserad data behandling](https://www.axelos.com/case-studies-and-white-papers/itil-4-and-the-cloud), som fokuserar på att ansluta till befintlig ITIL-vägledning med bästa praxis från DevOps, Agile och Lean. Överväg också [IT4IT-referens arkitekturen](https://www.opengroup.org/it4it) som ger en alternativ skiss om hur du omvandlar den med hjälp av ett process oberoende Framework.

## <a name="learn-more"></a>Läs mer

Bläddra i [Microsoft Learn katalogen](https://docs.microsoft.com/learn/browse)om du vill identifiera ytterligare utbildnings vägar. Använd roles-filtret för att justera utbildnings vägar med din roll.
