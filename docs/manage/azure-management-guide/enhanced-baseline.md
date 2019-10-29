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
ms.openlocfilehash: 85e289867ac69f3403d964078a7c3f3b2a6c96a7
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683705"
---
# <a name="enhanced-management-baseline-in-azure"></a>Förbättrad baslinje för hantering i Azure

De tre första molnhanteringsdisciplinerna beskriver en baslinje för hantering. I de tidigare artiklarna i den här guiden beskrevs en minsta livskraftiga produkt (MVP) för molnhanteringstjänster som refereras till som en baslinje för hantering. I den här artikeln beskrivs ett par förbättringar i baslinjen.

Syftet med en baslinje för hantering är att skapa ett enhetligt erbjudande som tillhandahåller en minsta åtagandenivå för företaget för **alla*** arbetsbelastningar som stöds. Den här baslinjen med upprepningsbara hanteringserbjudanden låter teamet leverera optimerad drifthantering med minimal avvikelse. Men det kan behövas ett större åtagande för verksamheten utöver standarderbjudandet. Följande bild och punkter visar tre sätt att gå bortom baslinjen för hantering.

![Bortom baslinjen för molnhantering](../../_images/manage/beyond-the-baseline.png)

- **Arbetsbelastningsåtgärder:**
  - Största investering per arbetsbelastningsdrift.
  - Högsta återhämtningsgrad.
  - Föreslås för ungefär 20 % av de arbetsbelastningar som driver affärsvärde.
  - Är vanligtvis reserverad för högkritiska eller verksamhetskritiska arbetsbelastningar.
- **Plattformsdrift:**
  - Verksamhetsinvesteringar sprids över många arbetsbelastningar.
  - Återhämtningsförbättringar påverkar alla arbetsbelastningar som använder den definierade plattformen.
  - Föreslås för +/-20 % av de mest kritiska plattformarna.
  - Är vanligtvis reserverad för medelkritiska till högkritiska arbetsbelastningar.
- **Förbättrad baslinje för hantering:**
  - Den lägsta relativa verksamhetsinvesteringen.
  - Något förbättrade företagsåtaganden med ytterligare molnbaserade driftsverktyg och processer.

För både arbetsbelastnings- och plattformsåtgärder krävs ändringar i design- och arkitekturprinciper. Dessa ändringar kan ta tid och leda till ökade driftskostnader. Om du vill minska antalet arbetsbelastningar som kräver sådana investeringar kan en förbättrad baslinje för hantering tillhandahålla en tillräcklig förbättring av åtagandet.

I följande tabell beskrivs några processer, verktyg och potentiella effekter som är vanliga i kunders förbättrade baslinje för hantering.

|Disciplin  |Process  |Verktyg  |Potentiell påverkan| Läs mer |
|---------|---------|---------|---------|---------|
|Inventering och synlighet|Tjänständringsspårning|Azure Resource Graph|Bättre insyn i förändringar i Azure-tjänster kan hjälpa dig att snabbare identifiera och åtgärda negativ påverkan|[Översikt över Azure Resource Graph](https://docs.microsoft.com/azure/governance/resource-graph/overview)|
|Inventering och synlighet|ITSM-integrering (IT Service Management)|IT Service Management Connector|Automatisk ITSM-anslutning skapar medvetenhet tidigare|[Azure ITSM-anslutning](https://docs.microsoft.com/azure/azure-monitor/platform/itsmc-overview)|
|Driftsmässig efterlevnad|Automatisering av åtgärder|Azure Automation|Automatisera driftsmässig efterlevnad för att vidta snabbare och mer korrekta åtgärder vid ändringar|Se nedan|
|Driftsmässig efterlevnad|Åtgärder i flera moln|Azure Automation Hybrid Runbook Worker|Automatisera driften över flera moln|[Översikt över Hybrid Runbook](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker)|
|Driftsmässig efterlevnad|Gästautomatisering|Önskad tillståndskonfiguration (DSC)|Kodbaserad konfiguration av gästoperativsystem för att minska fel och konfigurationsförändringar|[DSC-översikt](/powershell/scripting/dsc/overview/overview)|
|Skydda och återställa|Överträdelseanmälan|Azure Security Center|Utöka skyddet för att inkludera återställningsutlösare för säkerhetsöverträdelser|Se nedan|

::: zone target="docs"

## <a name="azure-automation"></a>Azure Automation

::: zone-end
::: zone target="chromeless"

## <a name="azure-automationtabazureautomation"></a>[Azure Automation](#tab/AzureAutomation)

::: zone-end

Azure Automation har ett centraliserat system för hantering av automatiserade kontroller. I Azure Automation kan enkla reparations-, skalnings- och optimeringsprocesser köras som svar på miljömått som minskar prestandakostnaderna för manuell incidentbearbetning. Det viktigaste är att automatiserad reparation kan levereras nästan i realtid, vilket minskar avbrotten i verksamhetsprocesserna avsevärt. En studie av de vanligaste verksamhetsavbrotten identifierar aktiviteter i din miljö som kan automatiseras.

### <a name="runbooks"></a>Runbooks

Den grundläggande kodenheten för att leverera automatisk reparation är en runbook. Runbook-flöden innehåller instruktioner för att åtgärda eller återställa från en incident.

Så här skapar eller hanterar du runbook-flöden:

1. Gå till [Azure Automation](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts).
2. Välj ett av de **Automation-konton** som visas.
3. Leta reda på avsnittet **Processautomatisering** i portalen.
4. Med alternativen i avsnittet kan du skapa eller hantera runbook-flöden, scheman och andra automatiska reparationsfunktioner.

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

Azure Security Center är också en viktig del i din skydds- och återställningsstrategi. Där kan du övervaka säkerheten för dina datorer, nätverk, lagringsutrymmen, datatjänster och appar. Med Azure Security Center får du en avancerad hotidentifiering via maskininlärning och beteendeanalys som hjälper dig att identifiera aktiva hot mot dina Azure-resurser. Dessutom får du ett skydd som blockerar skadlig kod och annan oönskad kod, och minskar den yta som är exponerad för brute force-attacker och andra nätverksattacker.

När Azure Security Center identifierar ett hot kan du få en säkerhetsvarning med de åtgärder du behöver vidta för att reagera på en attack. Det skapar också en rapport med information om hotet som har identifierats.

Azure Security Center är tillgängligt på två nivåer – kostnadsfri och standard. Funktioner som säkerhetsrekommendationer är tillgängliga utan kostnad i den kostnadsfria nivån. På Standard-nivån får du ytterligare skydd som avancerad hotidentifiering och skydd för arbetsbelastningar i hybridmoln.

::: zone target="chromeless"

### <a name="action"></a>Åtgärd

**Prova Standard-nivån kostnadsfritt i 30 dagar.**

När du aktiverar och ställer in säkerhetsprinciper för en prenumerations resurser kan du se säkerhetstillståndet för dina resurser och eventuella problem i avsnittet **Skydd**. Problemen visas även i en lista på panelen **Recommendations (Rekommendationer)** .

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end

::: zone target="docs"

Om du vill utforska Azure Security Center går du till [Azure-portalen](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0).

### <a name="learn-more"></a>Läs mer

Läs mer i [dokumentationen om Azure Security Center](https://docs.microsoft.com/azure/security-center).

::: zone-end
