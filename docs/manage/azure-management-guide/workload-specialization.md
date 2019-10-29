---
title: Specialisering för arbetsbelastningar för molnhantering i Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Förbättra arbetsbelastningsspecifika molnhanteringsåtgärder
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 51bdf23ccb2262202dfa095c5e9b57f727d11d3b
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72556997"
---
# <a name="workload-specialization-for-cloud-management"></a>Specialisering för arbetsbelastningar för molnhantering

Specialiseringen för arbetsbelastningar bygger på begrepp som beskrivs i [Specialisering för plattformar](./platform-specialization.md).

![Bortom baslinjen för molnhantering](../../_images/manage/beyond-the-baseline.png)

- **Arbetsbelastningsåtgärder:** Största investering per arbetsbelastningsdrift. Högsta återhämtningsgrad. Föreslås för +/- 20 % av de arbetsbelastningar som driver affärsvärde. Vanligtvis reserverade för högkritiska eller verksamhetskritiska arbetsbelastningar.
- **Plattformsdrift:** Verksamhetsinvesteringar sprids över många arbetsbelastningar. Återhämtningsförbättringar påverkar alla arbetsbelastningar som använder den definierade plattformen. Föreslås för +/- 20 % av de mest kritiska plattformarna. Vanligtvis reserverade för medelkritiska till högkritiska arbetsbelastningar.
- **Förbättrad baslinje för hantering:** Den lägsta relativa verksamhetsinvesteringen. Något förbättrade företagsåtaganden med ytterligare molnbaserade driftsverktyg och processer.

## <a name="high-level-process"></a>Process på hög nivå

Specialisering av arbetsbelastningar består av en disciplinerad körning av följande fyra processer med ett iterativt tillvägagångssätt. Varje process förklaras mer i detalj i artikeln [Specialisering för plattformar](./platform-specialization.md).

- **Förbättra systemdesignen:** Förbättra utformningen av en speciell arbetsbelastning för att effektivt minimera avbrott.
- **Automatisera reparationer:** Vissa förbättringar är inte kostnadseffektiva. I sådana fall kan det vara mer meningsfullt att automatisera reparationen och minska effekten av avbrott.
- **Skala lösningen:** När systemdesignen och automatiska reparationer förbättras kan dessa ändringar skalas över hela miljön via tjänstkatalogen.
- **Kontinuerliga förbättringar:** Olika övervakningsverktyg kan användas för att upptäcka stegvisa förbättringar som kan hanteras i nästa steg i systemutformningen, automatiseringen och skalningen.

## <a name="cultural-change"></a>Kulturell förändring

Specialiseringen för arbetsbelastningar utlöser ofta en kulturell förändring. Traditionellt inom IT skapas processer som fokuserar på att leverera en baslinje för hantering, förbättrade baslinjer och plattformsåtgärder. Dessa typer av erbjudanden kan skalas över hela miljön. Specialiseringen för arbetsbelastningar är mycket lik specialiseringen för plattformar när det gäller utförandet. Men till skillnad från vanliga plattformar skalas ofta inte den specialisering som krävs för enskilda arbetsbelastningar.

När det krävs en specialisering av arbetsbelastningar är det vanligt att den operativa ledningen ser bortom ett centralt IT-perspektiv. Den metod som föreslås i Cloud Adoption Framework är en distribution av molnhanteringsfunktionalitet.

I den här modellen flyttas operativa uppgifter som övervakning, distribution, DevOps och andra innovationsfokuserade funktioner till en programutvecklings- eller affärsenhetsorganisation. Molnplattforms- och molnövervakningsteamen levererar fortfarande i enlighet med baslinjen för hantering i miljön. Dessa centraliserade team vägleder och instruerar också team som är specialiserade på arbetsbelastningar om hur de ska hantera sina arbetsbelastningar. Men ansvaret för den dagliga driften ligger hos ett molnhanteringsteam som styrs utanför IT-avdelningen. Den här typen av distribuerad kontroll är ett av de viktigaste tecknen på Cloud Center of Excellence-mognad.

## <a name="beyond-platform-specialization---application-insights"></a>Bortom specialisering för plattformar – Application Insights

Mer information om den specifika arbetsbelastning som krävs för att tillhandahålla en tydlig arbetsbelastningsdrift. Under fasen för kontinuerlig förbättring är Application Insights ett nödvändigt tillägg i verktygskedjan för molnhantering.

|Programövervakning|Application Insights|Övervakning och diagnostik för appar| |Prestanda, tillgänglighet, användning|Application Insights|Avancerad programövervakning med Appinstrumentpanel, sammansatta kartor, användning och spårning|

### <a name="deploy-application-insights"></a>Distribuera Application Insights

1. Sök efter **Application Insights** i Azure-portalen.
2. Klicka på **+ Lägg till** för att skapa en Application Insights-resurs för att övervaka ditt live-webbprogram.
3. Följ anvisningarna på skärmen

Se [Azure Monitor Application Insights Hub](https://docs.microsoft.com/azure/azure-monitor/azure-monitor-app-hub) för vägledning om hur du konfigurerar programmet för övervakning.

::: zone target="chromeless"

::: form action="OpenBlade[#create/Microsoft.AppInsights]" submitText="Create Application Insight resources" :::

::: zone-end

### <a name="monitor-performance-availability-and-usage"></a>Övervaka prestanda, tillgänglighet och användning

1. Sök efter **Application Insights** i Azure-portalen.
2. Välj en av Application Insights-resurserna i listan

Navigeringen för Application Insights innehåller en mängd olika alternativ för att övervaka prestanda, tillgänglighet, användning och beroenden. Var och en av dessa vyer över programdata förtydligar feedbackslingan för kontinuerlig förbättring.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents]" submitText="Monitor applications" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
