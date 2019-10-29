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
ms.openlocfilehash: 0386a8c30758cce6c1c3d23bfa73d1f90e919692
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72556980"
---
# <a name="platform-specialization-for-cloud-management"></a>Specialisering för plattformar för molnhantering

Till skillnad från den förbättrade baslinjen för hantering är specialisering för plattformar ett tillägg utöver den vanliga baslinjen för hantering. Nedan visas en punktlista över hur du kan utöka baslinjen för hantering. I den här artikeln beskrivs alternativet specialisering för plattformar.

![Bortom baslinjen för molnhantering](../../_images/manage/beyond-the-baseline.png)

- **Arbetsbelastningsåtgärder:** Största investering per arbetsbelastningsdrift. Högsta återhämtningsgrad. Föreslås för +/- 20 % av de arbetsbelastningar som driver affärsvärde. Vanligtvis reserverade för högkritiska eller verksamhetskritiska arbetsbelastningar.
- **Plattformsdrift:** Verksamhetsinvesteringar sprids över många arbetsbelastningar. Återhämtningsförbättringar påverkar alla arbetsbelastningar som använder den definierade plattformen. Föreslås för +/- 20 % av de mest kritiska plattformarna. Vanligtvis reserverade för medelkritiska till högkritiska arbetsbelastningar.
- **Förbättrad baslinje för hantering:** Den lägsta relativa verksamhetsinvesteringen. Något förbättrade företagsåtaganden med ytterligare molnbaserade driftsverktyg och processer.

För både arbetsbelastnings- och plattformsåtgärder krävs ändringar i design- och arkitekturprinciper. Dessa ändringar kan ta tid och leda till ökade driftskostnader. Om du vill minska antalet arbetsbelastningar som kräver sådana investeringar kan en förbättrad baslinje för hantering tillhandahålla en tillräcklig förbättring av åtagandet.

I följande tabell beskrivs några processer, verktyg och potentiella effekter som är vanliga i kunders förbättrade baslinje för hantering.

|Process  |Verktyg  |Syfte  |Förslag på hanteringsnivå  |
|---------|---------|---------|---------|
|Förbättra systemdesignen|Azure-arkitekturramverk|Förbättra arkitekturdesignen för plattformen för att förbättra driften|
|Automatisera reparationer|Azure Automation|Svara på avancerade plattformsdata med plattformsspecifik automatisering|Plattformsdrift|
|Tjänstkatalog|Center för hanterade program|Tillhandahålla en självbetjäningskatalog för godkända lösningar som uppfyller organisations standarder|Plattformsdrift|
|Prestanda för containrar|Azure Monitor för containrar|Övervakning och diagnostik för containrar|Plattformsdrift|
|PaaS-dataprestanda|Azure SQL-analys|Övervakning och diagnostik för PaaS-databaser|Plattformsdrift|
|IaaS-dataprestanda|Hälsokontroll för SQL Server|Övervakning och diagnostik för IaaS-databaser|Plattformsdrift|

## <a name="high-level-process"></a>Process på hög nivå

Specialisering av plattformar består av en disciplinerad körning av följande fyra processer med ett iterativt tillvägagångssätt. Varje process förklaras i detalj i följande avsnitt i den här artikeln.

- **Förbättra systemdesignen:** Förbättra utformningen av vanliga system (eller plattformar) för att effektivt minimera avbrott.
- **Automatisera reparationer:** Vissa förbättringar är inte kostnadseffektiva. I sådana fall kan det vara mer meningsfullt att automatisera reparationen och minska effekten av avbrott.
- **Skala lösningen:** När systemdesignen och automatiska reparationer förbättras kan dessa ändringar skalas över hela miljön via tjänstkatalogen.
- **Kontinuerliga förbättringar:** Olika övervakningsverktyg kan användas för att upptäcka stegvisa förbättringar som kan hanteras i nästa steg i systemutformningen, automatiseringen och skalningen.

::: zone target="docs"

## <a name="improve-system-design"></a>Förbättra systemdesignen

::: zone-end
::: zone target="chromeless"

## <a name="improve-system-designtabsystemsdesign"></a>[Förbättra systemdesignen](#tab/SystemsDesign)

::: zone-end

Att förbättra systemdesignen är den mest effektiva metoden för att förbättra driften av en plattform. Genom att förbättra systemdesignen kan du öka stabiliteten och minska avbrott i verksamheten. Utformningen av enskilda system ligger utanför omfånget för det miljöperspektiv som utgör utgångspunkten i Cloud Adoption Framework. Som komplement till det här ramverket innehåller Azure-arkitekturramverket metodtips för att förbättra återhämtningen för och utformningen av ett särskilt system. Dessa designförbättringar kan tillämpas på systemdesignen för en plattform eller en specifik arbetsbelastning.

Azure-arkitekturramverket fokuserar på förbättringar inom fem pelare för systemdesign:

- **Skalbarhet:** Skala vanliga plattformstillgångar för att hantera ökad belastning.
- **Tillgänglighet:** Minska driftavbrott genom att förbättra den potentiella drifttiden.
- **Återhämtning:** Förbättra återställningstiden för att minska avbrottstiden.
- **Säkerhet:** Skydda program och data mot externa hot.
- **Hantering:** Driftprocesser som är specifika för dessa vanliga plattformstillgångar.

De flesta driftavbrotten beror på någon form av teknisk skuld eller brist i arkitekturen. För befintliga distributioner kan förbättringar av systemdesignen ses som ett sätt att betala av den tekniska skulden. För nya distributioner kan förbättringar av systemdesignen ses som ett sätt att undvika att hamna i teknisk skuld. På nästa flik, Automatiserad reparation, beskrivs sätt att hantera teknisk skuld som inte kan eller behöver åtgärdas.

Läs mer om hur du förbättrar systemdesignen med [Azure-arkitekturramverket](https://docs.microsoft.com/azure/architecture/guide/pillars).

När systemdesignen har förbättrats kan du komma tillbaka till den här artikeln och hitta nya möjligheter att förbättra och skala dessa förbättringar i din miljö.

::: zone target="docs"

## <a name="automated-remediation"></a>Automatiserad reparation

::: zone-end
::: zone target="chromeless"

## <a name="automated-remediationtabautomatedremediation"></a>[Automatiserad reparation](#tab/AutomatedRemediation)

::: zone-end

Vissa tekniska skulder kan inte åtgärdas. Det kan vara för dyrt att lösa problemet. Det går att planera en lösning, men projektet kommer att vara länge. Driftstoppet kanske inte har någon markant effekt på verksamheten eller så kanske företaget prioriterar en snabb återställning i stället för att investera i återhämtning.

Om en lösning av den tekniska skulden inte är önskad väg att gå är automatiserad reparation ett vanligt nästa steg. Att använda Azure Automation och Azure Monitor för att identifiera trender och tillhandahålla automatiserad reparation är den vanligaste metoden när det gäller automatisk reparation.

Vägledning om automatiserad reparation finns i den här artikeln om [Azure Automation och aviseringar](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

::: zone target="docs"

## <a name="scale-the-solution-with-a-service-catalog"></a>Skala lösningen med en tjänstkatalog

::: zone-end
::: zone target="chromeless"

## <a name="scale-the-solution-with-a-service-catalogtabservicecatalog"></a>[Skala lösningen med en tjänstkatalog](#tab/ServiceCatalog)

::: zone-end

Hörnstenen för plattformsspecialisering och plattformsdrift är en välhanterad tjänstkatalog. Det är så förbättringar av systemdesignen och reparationer skalas ut i en miljö. Molnplattformsteamet och molnautomatiseringsteamet samarbetar för att skapa upprepningsbara lösningar för vanliga plattformar i alla miljöer. Men om dessa lösningar inte används konsekvent kan molnhanteringen erbjuda lite mer än ett baslinjeerbjudande.

För att maximera införandet och minimera underhållskostnaderna för en optimerad plattform bör plattformen läggas till i en tjänstkatalog i Azure. Varje program i katalogen kan distribueras för intern användning via tjänstkatalogen eller som ett Marketplace-erbjudande för externa konsumenter.

Anvisningar om hur du publicerar till en tjänstkatalog finns i artikelserien om att [publicera till en tjänstkatalog](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="deploy-applications-from-the-service-catalog"></a>Distribuera program från tjänstkatalogen

1. Sök efter **Center för Managed Applications (förhandsversion)** i Azure-portalen.
2. Klicka på **Tjänstkatalogprogram** under avsnittet **Bläddra**.
3. Klicka på **+ Lägg till** och välj en programdefinition från ditt företags tjänstkatalog.

Alla hanterade program som du underhåller visas här.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Appliance/ManagedAppsHubBlade/browseServiceCatalog]" submitText="Go to Virtual Machines" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="manage-service-catalog-applications"></a>Hantera tjänstkatalogprogram

1. Sök efter **Center för Managed Applications (förhandsversion)** i Azure-portalen.
2. Klicka på **Tjänstkatalogprogram** under avsnittet **Tjänst**.

Alla hanterade program som du underhåller visas här.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Appliance/ManagedAppsHubBlade/serviceServiceCatalogApps]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

## <a name="continuous-improvement"></a>Kontinuerliga förbättringar

::: zone-end
::: zone target="chromeless"

## <a name="continuous-improvementtabcontinuousimprovement"></a>[Kontinuerliga förbättringar](#tab/ContinuousImprovement)

::: zone-end

Plattformsspecialiseringen och plattformsdriften är båda beroende av starka feedbackslingor mellan införande-, plattforms-, automatiserings- och hanteringsteamen. Genom att lägga till dessa feedbackslingor i data får varje team möjlighet att fatta kloka beslut. För att uppnå långsiktiga affärsåtaganden för plattformsdriften är det viktigt att utnyttja insikter som är specifika för den centraliserade plattformen. Eftersom containrar och SQL Server är de två vanligaste centralt hanterade plattformarna finns ett par artiklar nedan som kan hjälpa di att komma igång med datainsamling för kontinuerliga förbättringar.

[Containerprestanda](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview)
[PaaS-databasprestanda](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql)
[IaaS-databasprestanda](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
