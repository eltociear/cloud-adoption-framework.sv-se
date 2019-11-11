---
title: Specialisering för plattformar för molnhantering i Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Förbättra plattformsspecifika molnhanteringsåtgärder.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 5b775feb4b007629a6c93e762c8b02e5d5ef0a8a
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565455"
---
# <a name="platform-specialization-for-cloud-management"></a>Specialisering för plattformar för molnhantering

Till skillnad från den förbättrade baslinjen för hantering är specialisering för plattformar ett tillägg utöver den vanliga baslinjen för hantering. Se följande bild och lista som visar hur du utökar hanteringsbaslinjen. I den här artikeln beskrivs alternativen för plattformsspecialisering.

![Bortom baslinjen för molnhantering](../../_images/manage/beyond-the-baseline.png)

- **Arbetsbelastningsåtgärder:** Den största investeringen per arbetsbelastning och den högsta återhämtningsgraden. Vi föreslår arbetsbelastningsåtgärder för cirka 20 % av arbetsbelastningarna som genererar affärsvärde. Den här specialiseringen används vanligtvis för mycket kritiska eller verksamhetskritiska arbetsbelastningar.
- **Plattformsdrift:** Verksamhetsinvesteringar sprids över många arbetsbelastningar. Återhämtningsförbättringar påverkar alla arbetsbelastningar som använder den definierade plattformen. Vi föreslår plattformsåtgärder för cirka 20 % av plattformarna som är mest kritiska. Den här specialiseringen används vanligtvis för arbetsbelastningar som är kritiska eller mycket kritiska.
- **Förbättrad baslinje för hantering:** Den relativt minsta driftsinvesteringen. Den här specialiseringen förbättrar företagets åtaganden något genom att använda ytterligare molnbaserade verksamhetsspecifika verktyg och processer.

För både arbetsbelastnings- och plattformsåtgärder krävs ändringar i design- och arkitekturprinciper. Dessa ändringar kan ta tid och kan leda till ökade driftskostnader. Om du vill minska antalet arbetsbelastningar som kräver sådana investeringar kan en förbättrad hanteringsbaslinje ge en tillräcklig förbättring av företagets åtaganden.

I följande tabell beskrivs några processer, verktyg och potentiella effekter som är vanliga i kundernas förbättrade hanteringsbaslinjer:

|Process  |Verktyg  |Syfte  |Förslag på hanteringsnivå  |
|---------|---------|---------|---------|
|Förbättra systemdesignen|Azure-arkitekturramverk|Förbättra driften genom att förbättra plattformens arkitekturdesign|Saknas|
|Automatisera reparationer|Azure Automation|Svara på avancerade plattformsdata med plattformsspecifik automatisering|Plattformsdrift|
|Tjänstkatalog|Center för hanterade program|Tillhandahålla en självbetjäningskatalog för godkända lösningar som uppfyller organisationsstandarder|Plattformsdrift|
|Prestanda för containrar|Azure Monitor för containrar|Övervakning och diagnostik för containrar|Plattformsdrift|
|Prestanda för PaaS-data (Platform as a Service)|Azure SQL-analys|Övervakning och diagnostik för PaaS-databaser|Plattformsdrift|
|Prestanda för IaaS-data (Infrastructure as a Service)|Hälsokontroll för SQL Server|Övervakning och diagnostik för PaaS-databaser|Plattformsdrift|

## <a name="high-level-process"></a>Process på hög nivå

Specialisering av plattformar består av en disciplinerad körning av följande fyra processer med ett iterativt tillvägagångssätt. Varje process förklaras i detalj i senare avsnitt i den här artikeln.

- **Förbättra systemdesignen:** Förbättra utformningen av vanliga system (eller plattformar) för att effektivt minimera avbrott.
- **Automatisera reparationer:** Vissa förbättringar är inte kostnadseffektiva. I sådana fall kan det vara mer meningsfullt att automatisera reparationen och minska effekten av avbrott.
- **Skala lösningen:** När systemdesignen och automatiska reparationer förbättras kan dessa ändringar skalas över hela miljön via tjänstkatalogen.
- **Kontinuerliga förbättringar:** Olika övervakningsverktyg kan användas för att identifiera stegvisa förbättringar. Dessa förbättringar kan hanteras i nästa steg av systemdesign-, automations- och skalningsprocessen.

::: zone target="docs"

## <a name="improve-system-design"></a>Förbättra systemdesignen

::: zone-end
::: zone target="chromeless"

## <a name="improve-system-designtabsystemsdesign"></a>[Förbättra systemdesignen](#tab/SystemsDesign)

::: zone-end

Att förbättra systemdesignen är den mest effektiva metoden för att förbättra driften av en plattform. Genom att förbättra systemdesignen kan du öka stabiliteten och minska avbrott i verksamheten. Utformningen av enskilda system ligger utanför omfånget för det miljöperspektiv som utgör utgångspunkten i Cloud Adoption Framework för Azure.

Som komplement till Cloud Adoption Framework innehåller Azures arkitekturramverk metodtips för att förbättra återhämtningen för och utformningen av ett specifikt system. Dessa designförbättringar kan tillämpas på systemdesignen för en plattform eller en specifik arbetsbelastning.

Azure-arkitekturramverket fokuserar på förbättringar inom fem pelare för systemdesign:

- **Skalbarhet:** Skala vanliga plattformstillgångar för att hantera ökad belastning
- **Tillgänglighet:** Minska driftavbrott genom att förbättra den potentiella drifttiden
- **Återhämtning:** Förbättra återställningstider för att minska avbrottstiden
- **Säkerhet:** Skydda program och data mot externa hot
- **Hantering:** Driftprocesser som är specifika för dessa vanliga plattformstillgångar

De flesta verksamhetsavbrotten beror på tekniska skulder och brister i arkitekturen. För befintliga distributioner kan du se förbättringar av systemdesignen som betalningar mot befintliga tekniska skulder. För nya distributioner kan du se förbättringarna som ett sätt att undvika tekniska skulder.

Fliken **Automatiserad reparation** visar hur du kan åtgärda tekniska skulder som inte kan eller borde åtgärdas.

Läs mer om hur du förbättrar systemdesignen med [Azure-arkitekturramverket](https://docs.microsoft.com/azure/architecture/guide/pillars).

När systemdesignen har förbättrats kan du komma tillbaka till den här artikeln och hitta nya möjligheter att förbättra och skala dessa förbättringar i din miljö.

::: zone target="docs"

## <a name="automated-remediation"></a>Automatiserad reparation

::: zone-end
::: zone target="chromeless"

## <a name="automated-remediationtabautomatedremediation"></a>[Automatiserad reparation](#tab/AutomatedRemediation)

::: zone-end

Vissa tekniska skulder kan inte åtgärdas. Lösningen kan vara för dyr att korrigera eller kan planeras men kräva mycket tid. Avbrottet i verksamheten kanske inte har en betydande effekt på verksamheten. Eller så kan prioriteten vara en snabb återhämtning i stället för att investera i själva återhämtningsförmågan.

Om en lösning av den tekniska skulden inte är önskad väg att gå är automatiserad reparation ett vanligt nästa steg. Att använda Azure Automation och Azure Monitor för att identifiera trender och tillhandahålla automatiserad reparation är den vanligaste metoden när det gäller automatisk reparation.

Vägledning om automatiserad reparation finns i [Azure Automation och aviseringar](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

::: zone target="docs"

## <a name="scale-the-solution-with-a-service-catalog"></a>Skala lösningen med en tjänstkatalog

::: zone-end
::: zone target="chromeless"

## <a name="scale-the-solution-with-a-service-catalogtabservicecatalog"></a>[Skala lösningen med en tjänstkatalog](#tab/ServiceCatalog)

::: zone-end

Hörnstenen för plattformsspecialisering och plattformsdrift är en välhanterad tjänstkatalog. Användningen av en katalog är hur förbättringar av systemdesignen och reparationer skalas ut i en miljö.

Molnplattformsteamet och molnautomatiseringsteamet samarbetar för att skapa upprepningsbara lösningar för vanliga plattformar i alla miljöer. Men om dessa lösningar inte används konsekvent kan molnhanteringen inte erbjuda mycket mer än ett baslinjeerbjudande.

För att maximera implementeringen och minimera underhållskostnaderna för en optimerad plattform bör du lägga till plattformen i en Azure-tjänstkatalog. Varje program i katalogen kan distribueras för intern användning via tjänstkatalogen eller som ett Marketplace-erbjudande för externa konsumenter.

Anvisningar om hur du publicerar till en tjänstkatalog finns i artikelserien om att [publicera till en tjänstkatalog](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="deploy-applications-from-the-service-catalog"></a>Distribuera program från tjänstkatalogen

1. Gå till **Center för hanterade program (förhandsversion)** på Azure-portalen.
2. Välj **Tjänstkatalogprogram** i rutan **Bläddra**.
3. Klicka på **+ Lägg till** och välj en programdefinition från ditt företags tjänstkatalog.

Alla hanterade program som du underhåller visas.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Appliance/ManagedAppsHubBlade/browseServiceCatalog]" submitText="Go to Virtual Machines" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="manage-service-catalog-applications"></a>Hantera tjänstkatalogprogram

1. Gå till **Center för hanterade program (förhandsversion)** på Azure-portalen.
1. Välj **Tjänstkatalogprogram** i rutan **Tjänst**.

Alla hanterade program som du underhåller visas.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Appliance/ManagedAppsHubBlade/serviceServiceCatalogApps]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

## <a name="continuous-improvement"></a>Kontinuerliga förbättringar

::: zone-end
::: zone target="chromeless"

## <a name="continuous-improvementtabcontinuousimprovement"></a>[Kontinuerlig förbättring](#tab/ContinuousImprovement)

::: zone-end

Plattformsspecialiseringen och plattformsdriften är båda beroende av starka feedbackslingor mellan införande-, plattforms-, automatiserings- och hanteringsteamen. Genom att använda dessa feedbackslingor med data kan teamen fatta kloka beslut. För att uppnå långsiktiga affärsåtaganden för plattformsdriften är det viktigt att utnyttja insikter som är specifika för den centraliserade plattformen.

Containrar och SQL Server är de två vanligaste centralt hanterade plattformarna. De här artiklarna kan hjälpa dig att komma igång med datainsamling med kontinuerlig förbättring på dessa plattformar:

- [Prestanda för containrar](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview)
- [Prestanda för PaaS-databaser](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql)
- [Prestanda för IaaS-databaser](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
