---
title: Specialiserade arbetsbelastningar för molnhantering
description: Använd Cloud Adoption Framework för Azure för att lära dig om specialiserade arbetsbelastningar för molnhantering.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 7108f90ac19e5a566e068e3292d2fab8bd1b7e3d
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341733"
---
# <a name="workload-specialization-for-cloud-management"></a>Specialisering för arbetsbelastningar för molnhantering

Specialiseringen för arbetsbelastningar bygger på begrepp som beskrivs i [Specialisering för plattformar](./platform-specialization.md).

![Bortom baslinjen för molnhantering](../../_images/manage/beyond-the-baseline.png)

- **Arbetsbelastningsåtgärder:** Den största investeringen per arbetsbelastning och den högsta graden av återhämtning. Vi föreslår arbetsbelastningsåtgärder för cirka 20 % av arbetsbelastningarna som genererar affärsvärde. Den här specialiseringen används vanligtvis för mycket kritiska eller verksamhetskritiska arbetsbelastningar.
- **Plattformsdrift:** Verksamhetsinvesteringar sprids över många arbetsbelastningar. Återhämtningsförbättringar påverkar alla arbetsbelastningar som använder den definierade plattformen. Vi föreslår plattformsåtgärder för cirka 20 % av plattformarna som är mest kritiska. Den här specialiseringen används vanligtvis för arbetsbelastningar som är kritiska eller mycket kritiska.
- **Förbättrad baslinje för hantering:** Den relativt minsta driftsinvesteringen. Den här specialiseringen förbättrar företagsåtaganden något med hjälp av fler molnbaserade verksamhetsspecifika verktyg och processer.

## <a name="high-level-process"></a>Process på hög nivå

Specialisering av arbetsbelastningar består av en disciplinerad körning av följande fyra processer med ett iterativt tillvägagångssätt. Varje process förklaras i detalj i [Plattformsspecialisering](./platform-specialization.md).

- **Förbättra systemdesignen:** Förbättra utformningen av en speciell arbetsbelastning för att effektivt minimera avbrott.
- **Automatisera reparationer:** Vissa förbättringar är inte kostnadseffektiva. I sådana fall kan det vara mer meningsfullt att automatisera reparationen och minska effekten av avbrott.
- **Skala lösningen:** När du förbättrar systemdesignen och den automatiserade reparationen kan du skala ändringarna i miljön via tjänstkatalogen.
- **Kontinuerliga förbättringar:** Du kan använda olika övervakningsverktyg för att upptäcka stegvisa förbättringar. Dessa förbättringar kan hanteras i nästa steg av systemdesign-, automations- och skalningsprocessen.

## <a name="cultural-change"></a>Kulturell förändring

Arbetsbelastningsspecialisering utlöser ofta en kulturell förändring i traditionella IT-utvecklingsprocesser som fokuserar på att leverera en hanteringsbaslinje, förbättrade baslinjer och plattformsåtgärder. Dessa typer av erbjudanden kan skalas över hela miljön. Arbetsbelastningsspecialiseringen liknar plattformsspecialiseringen när det gäller utförandet. Men till skillnad från vanliga plattformar skalas ofta inte den specialisering som krävs för enskilda arbetsbelastningar.

När arbetsbelastningsspecialisering krävs utvecklas driftshanteringen ofta bortom ett centralt IT-perspektiv. Metoden som föreslås i Cloud Adoption Framework är en distribution av molnhanteringsfunktioner.

I den här modellen flyttas operativa uppgifter som övervakning, distribution, DevOps och andra innovationsfokuserade funktioner till en programutvecklings- eller affärsenhetsorganisation. Molnplattforms- och molnövervakningsteamen levererar fortfarande i enlighet med baslinjen för hantering i miljön.

Dessa centraliserade team vägleder och instruerar även team som är specialiserade på arbetsbelastningar om hur de ska hantera sina arbetsbelastningar. Men ansvaret för den dagliga driften ligger hos ett molnhanteringsteam som styrs utanför IT-avdelningen. Den här typen av distribuerad kontroll är ett av de viktigaste tecknen på mognad i Cloud Center of Excellence.

## <a name="beyond-platform-specialization-application-insights"></a>Bortom specialisering för plattformar: Application Insights

Mer information om den specifika arbetsbelastning som krävs för att tillhandahålla en tydlig arbetsbelastningsdrift. Under fasen för kontinuerlig förbättring är Application Insights ett nödvändigt tillägg i verktygskedjan för molnhantering.

|Krav|Verktyg|Syfte|
|---|---|---|
|Programövervakning|Application Insights|Övervakning och diagnostik för appar|
|Prestanda, tillgänglighet och användning|Application Insights|Avancerad programövervakning med instrumentpaneler för appar, sammansatta mappningar, användning och spårning|

### <a name="deploy-application-insights"></a>Distribuera Application Insights

1. Gå till **Application Insights** på Azure-portalen.
1. Välj **+ Lägg till** för att skapa en Application Insights-resurs för att övervaka ditt live-webbprogram.
1. Följ anvisningarna på skärmen.

Se [Azure Monitor Application Insights Hub](https://docs.microsoft.com/azure/azure-monitor/azure-monitor-app-hub) för vägledning om hur du konfigurerar programmet för övervakning.

::: zone target="chromeless"

::: form action="OpenBlade[#create/Microsoft.AppInsights]" submitText="Create Application Insight resources" :::

::: zone-end

### <a name="monitor-performance-availability-and-usage"></a>Övervaka prestanda, tillgänglighet och användning

1. Sök efter **Application Insights** i Azure-portalen.
1. Välj en av Application Insights-resurserna i listan.

Application Insights innehåller olika typer av alternativ för att övervaka prestanda, tillgänglighet, användning och beroenden. Var och en av dessa vyer över programdata förtydligar feedbackslingan för kontinuerlig förbättring.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents]" submitText="Monitor applications" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
