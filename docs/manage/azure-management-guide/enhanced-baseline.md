---
title: Förbättrad baslinje för hantering i Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Förbättringar i baslinjen för hantering
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 8cdd9a48d8d229fdca7cba383d677a49525d06cc
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73752963"
---
# <a name="enhanced-management-baseline-in-azure"></a>Förbättrad baslinje för hantering i Azure

De tre första molnhanteringsdisciplinerna beskriver en baslinje för hantering. I de tidigare artiklarna i den här guiden beskrevs en MVP (minsta fungerande produkt) för molnhanteringstjänster, kallad en hanteringsbaslinje. I den här artikeln beskrivs ett par förbättringar i baslinjen.

Syftet med en baslinje för hantering är att skapa ett enhetligt erbjudande som tillhandahåller en minsta åtagandenivå för företaget för *alla* arbetsbelastningar som stöds. Med den här baslinjen med upprepningsbara hanteringserbjudanden kan teamet leverera optimerad drifthantering med minimal avvikelse.

Ditt företag kan dock behöva en högre åtagandenivå än standardnivån. Följande bild och lista visar tre sätt att gå bortom baslinjen för hantering.

![Bortom baslinjen för molnhantering](../../_images/manage/beyond-the-baseline.png)

- **Arbetsbelastningsåtgärder:**
  - Största investeringen per arbetsbelastning.
  - Högsta återhämtningsgrad.
  - Föreslås för ungefär 20 % av de arbetsbelastningar som driver affärsvärde.
  - Är vanligtvis reserverad för högkritiska eller verksamhetskritiska arbetsbelastningar.
- **Plattformsdrift:**
  - Verksamhetsinvesteringar sprids över många arbetsbelastningar.
  - Återhämtningsförbättringar påverkar alla arbetsbelastningar som använder den definierade plattformen.
  - Rekommenderas för cirka 20 % av plattformarna som är mest kritiska.
  - Är vanligtvis reserverad för medelkritiska till högkritiska arbetsbelastningar.
- **Förbättrad baslinje för hantering:**
  - Den lägsta relativa verksamhetsinvesteringen.
  - Något förbättrade företagsåtaganden med ytterligare molnbaserade driftsverktyg och processer.

För både arbetsbelastnings- och plattformsåtgärder krävs ändringar i design- och arkitekturprinciper. Dessa ändringar kan ta tid och kan leda till ökade driftskostnader. Om du vill minska antalet arbetsbelastningar som kräver sådana investeringar kan en förbättrad baslinje för hantering tillhandahålla en tillräcklig förbättring av åtagandet.

I följande tabell beskrivs några processer, verktyg och potentiella effekter som är vanliga i kundernas förbättrade hanteringsbaslinjer:

| Disciplin  | Process  | Verktyg | Potentiell påverkan | Läs mer |
|---|---|---|---|---|
|Inventering och synlighet|Tjänständringsspårning|Azure Resource Graph|Bättre insyn i förändringar i Azure-tjänster kan hjälpa dig att snabbare identifiera och åtgärda negativ påverkan.|[Översikt över Azure Resource Graph](https://docs.microsoft.com/azure/governance/resource-graph/overview)|
|Inventering och synlighet|ITSM-integrering (IT Service Management)|IT Service Management Connector|Automatisk ITSM-anslutning skapar medvetenhet tidigare.|[Anslutningsprogram för hantering av IT-tjänster (ITSM)](https://docs.microsoft.com/azure/azure-monitor/platform/itsmc-overview)|
|Driftsmässig efterlevnad|Automatisering av åtgärder|Azure Automation|Automatisera driftsmässig efterlevnad för att vidta snabbare och mer korrekta åtgärder vid ändringar.|Se följande avsnitt|
|Driftsmässig efterlevnad|Åtgärder i flera moln|Azure Automation Hybrid Runbook Worker|Automatisera driften över flera moln.|[Översikt över Hybrid Runbook Worker](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker)|
|Driftsmässig efterlevnad|Gästautomatisering| Önskad tillståndskonfiguration (DSC)|Kodbaserad konfiguration av gästoperativsystem för att minska fel- och konfigurationsavvikelser.|[DSC-översikt](https://docs.microsoft.com/powershell/scripting/dsc/overview/overview)|
|Skydda och återställa|Överträdelseanmälan|Azure Security Center|Utöka skyddet för att inkludera återställningsutlösare för säkerhetsöverträdelser.|Se följande avsnitt|

::: zone target="docs"

## <a name="azure-automation"></a>Azure Automation

::: zone-end
::: zone target="chromeless"

## <a name="azure-automationtabazureautomation"></a>[Azure Automation](#tab/AzureAutomation)

::: zone-end

Azure Automation har ett centraliserat system för hantering av automatiserade kontroller. I Azure Automation kan du köra enkla reparations-, skalnings- och optimeringsprocesser som svar på miljörelaterade mått. De här processerna minskar kostnaden jämfört med manuell bearbetning av incidenter.

Det viktigaste är att automatiserad reparation kan levereras nästan i realtid, vilket minskar avbrotten i verksamhetsprocesserna avsevärt. En studie av de vanligaste verksamhetsavbrotten identifierar aktiviteter i din miljö som kan automatiseras.

### <a name="runbooks"></a>Runbooks

Den grundläggande kodenheten för att leverera automatiserad reparation är en runbook. Runbook-flöden innehåller instruktioner för att åtgärda eller återställa från en incident.

Så här skapar eller hanterar du runbook-flöden:

1. Gå till [Azure Automation](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts).
1. Välj **Automation-konton** och välj ett av kontona i listan.
1. Gå till **Processautomatisering**.
1. Med de alternativ som visas kan du skapa eller hantera runbooks, scheman och andra automatiska reparationsfunktioner.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts]" submitText="Assign Policy" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
::: zone target="docs"

## <a name="azure-security-center"></a>Azure Security Center

::: zone-end
::: zone target="chromeless"

## <a name="azure-security-centertabazuresecuritycenter"></a>[Azure Security Center](#tab/AzureSecurityCenter)

::: zone-end

Azure Security Center är också en viktig del i din skydds- och återställningsstrategi. Där kan du övervaka säkerheten för dina datorer, nätverk, lagringsutrymmen, datatjänster och appar.

Med Azure Security Center får du en avancerad hotidentifiering via maskininlärning och beteendeanalys som hjälper dig att identifiera aktiva hot mot dina Azure-resurser. Dessutom får du ett skydd som blockerar skadlig kod och annan oönskad kod, och minskar den yta som är exponerad för brute force-attacker och andra nätverksattacker.

När Azure Security Center identifierar ett hot kan du få en säkerhetsvarning med de åtgärder du behöver vidta för att hantera en attack. Den innehåller också en rapport med information om det identifierade hotet.

Azure Security Center finns på två nivåer: Kostnadsfri och Standard. Funktioner såsom säkerhetsrekommendationer är tillgängliga utan kostnad på den kostnadsfria nivån. På Standard-nivån får du ytterligare skydd som avancerad hotidentifiering och skydd för arbetsbelastningar i hybridmoln.

::: zone target="chromeless"

### <a name="action"></a>Åtgärd

#### <a name="try-standard-tier-for-free-for-your-first-30-days"></a>Prova Standard-nivån kostnadsfritt i 30 dagar.

När du aktiverar och ställer in säkerhetsprinciper för en prenumerations resurser kan du se säkerhetstillståndet för dina resurser och eventuella problem i rutan **Skydd**. Problemen visas även i en lista på panelen **Recommendations (Rekommendationer)** .

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end

::: zone target="docs"

Om du vill utforska Azure Security Center går du till [Azure-portalen](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0).

### <a name="learn-more"></a>Läs mer

Läs mer i [dokumentationen om Azure Security Center](https://docs.microsoft.com/azure/security-center).

::: zone-end
