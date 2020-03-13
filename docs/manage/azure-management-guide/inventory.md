---
title: Inventering och synlighet i Azure
description: Lär dig verktygen som både kan användas för inventering och insyn i inventeringens körningsstatus så att du kan samla in driftdata.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: da3675484c04c9c02384fcbbc0337accff2aaffe
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092127"
---
# <a name="inventory-and-visibility-in-azure"></a>Inventering och synlighet i Azure

_Inventering och synlighet_ är den första av tre discipliner i en baslinje för molnhantering.

![Baslinje för molnhantering](../../_images/manage/management-baseline.png)

Den här disciplinen kommer först eftersom det är viktigt att samla in rätt driftsdata när du fattar beslut om åtgärder. Molnhanteringsteamen måste förstå vad som hanteras och hur bra tillgångarna fungerar. Den här artikeln beskriver olika verktyg som ger både en inventering och insyn i inventeringens körningsstatus.

I den här tabellen ser du rekommenderade minimikrav för alla typer av miljöer i företagsklass.

|Process  |Verktyg  |Syfte  |
|---------|---------|---------|
|Övervaka hälsotillståndet för Azure-tjänster|Azure Service Health|Hälsa, prestanda och diagnostik för tjänster som körs i Azure|
|Central loggning|Log Analytics|Central loggning för alla synlighetssyften|
|Central övervakning|Azure Monitor|Central övervakning av driftdata och trender|
|Inventering av virtuella datorer och ändringsspårning|Ändringsspårning och inventering i Azure|Inventera virtuella datorer och övervaka ändringar för gästoperativsystem|
|Prenumerationsövervakning|Azure-aktivitetslogg|Övervaka ändringar på prenumerationsnivå|
|Övervakning av gästoperativsystem|Azure Monitor för virtuella datorer|Övervaka ändringar och prestanda för virtuella datorer|
|Nätverksövervakning|Azure Network Watcher|Övervaka nätverksändringar och prestanda|
|DNS-övervakning|DNS-analys|Säkerhet, prestanda och åtgärder för DNS|

::: zone target="docs"

## <a name="azure-service-health"></a>Azure Service Health

::: zone-end
::: zone target="chromeless"

## <a name="azure-service-health"></a>[Azure Service Health](#tab/AzureServiceHealth)

::: zone-end

Azure Service Health tillhandahåller en anpassad vy över hälsotillstånden för dina Azure-tjänster och Azure-regioner. Information om aktiva problem publiceras till Service Health för att hjälpa dig att förstå hur de inverkar på dina resurser. Regelbundna uppdateringar håller dig uppdaterad allt eftersom problemen åtgärdas.

Vi publicerar också planerat underhåll i Service Health så att du får information om ändringar som kan påverka resurstillgängligheten. Konfigurera Service Health-aviseringar så att du meddelas om tjänstproblem, planerat underhåll eller andra ändringar som kan påverka dina Azure-tjänster och Azure-regioner.

I Azure Service Health ingår:

- **Azure-status:** En global vy över Azure-tjänsternas hälsotillstånd.
- **Service Health:** En anpassad vy över hälsotillståndet hos dina Azure-tjänster.
- **Resource Health:** En mer detaljerad vy över hälsotillståndet för dina enskilda resurser.

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Åtgärd

Om du vill skapa en Service Health-avisering:

1. går du till **Service Health**.
2. Välj **Hälsoaviseringar**.
3. Skapa en Service Health-avisering.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts]" submitText="Go to Service Health" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Om du vill ställa in en Service Health-avisering går du till [Azure-portalen](https://portal.azure.com/#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts).

### <a name="learn-more"></a>Läs mer

Läs mer i [Azure Service Health-dokumentationen](https://docs.microsoft.com/azure/service-health).

## <a name="log-analytics"></a>Log Analytics

::: zone-end
::: zone target="chromeless"

## <a name="log-analytics"></a>[Log Analytics](#tab/Log-Analytics)

::: zone-end

En [Log Analytics-arbetsyta](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace) är en unik miljö för lagring av Azure Monitor-loggdata. Varje arbetsyta har sitt eget datalager och sin egen konfiguration. Datakällor och lösningar konfigureras för att lagra data i specifika arbetsytor. Azure-övervakningslösningar kräver att alla servrar är anslutna till en arbetsyta, så att det går att lagra och komma åt deras loggdata.

::: zone target="chromeless"

### <a name="action"></a>Åtgärd

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.OperationalInsights%2Fworkspaces]" submitText="Explore Azure Monitor" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

### <a name="learn-more"></a>Läs mer

Mer information finns i [dokumentationen om hur du skapar en Log Analytics-arbetsyta](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace).

## <a name="azure-monitor"></a>Azure Monitor

::: zone-end
::: zone target="chromeless"

## <a name="azure-monitor"></a>[Azure Monitor](#tab/Azure-Monitor)

::: zone-end

Azure Monitor använder en enda hubb för alla övervaknings- och diagnostikdata i Azure och ger bra insyn i alla dina resurser. Med Azure Monitor kan du hitta och åtgärda problem och optimera prestanda. Dessutom får du hjälp med att förstå kundernas beteende.

- **Övervaka och visualisera mått.** Mått är numeriska värden som är tillgängliga från Azure-resurser. De ger information om hälsostatusen i dina system. Anpassa diagram för dina instrumentpaneler och använd arbetsböcker för rapportering.

- **Köra frågor mot och analysera loggar.** Loggarna kan vara aktivitets- och diagnostikloggar från Azure. Samla in ytterligare loggar från andra lösningar för övervakning och hantering som du använder i molnet eller lokalt. Använd Log Analytics som centralt datalager för alla dessa data. Därifrån kan köra du frågor för att felsöka problem eller visualisera data.

- **Konfigurera aviseringar och åtgärder.** Aviseringar meddelar dig om kritiska situationer. Du kan vidta korrigerande åtgärder baserat på utlösare för mått, loggar eller problem med tjänster. Du kan ställa in olika aviseringar och åtgärder och kan även skicka data till dina hanteringsverktyg för IT-tjänster.

::: zone target="chromeless"

### <a name="action"></a>Åtgärd

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview]" submitText="Explore Azure Monitor" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

 Börja övervaka dina:

- [Program](https://docs.microsoft.com/azure/application-insights/app-insights-overview)
- [Containrar](https://docs.microsoft.com/azure/monitoring/monitoring-container-overview)
- [Virtuella datorer](https://docs.microsoft.com/azure/monitoring/monitoring-service-map)
- [Nätverk](https://docs.microsoft.com/azure/networking/network-monitoring-overview)

Du kan hitta fler lösningar för resursövervakning på Azure Marketplace.

Om du vill utforska Azure Monitor går du till [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview).

### <a name="learn-more"></a>Läs mer

Mer information finns i [dokumentationen om Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics).

## <a name="onboard-solutions"></a>Publicera lösningar

::: zone-end
::: zone target="chromeless"

## <a name="onboard-solutions"></a>[Publicera lösningar](#tab/Configure-solutions)

::: zone-end

För att kunna aktivera lösningar måste du konfigurera Log Analytics-arbetsytan. Publicerade virtuella Azure-datorer och lokala servrar får lösningar från de Log Analytics-arbetsytor som de är anslutna till.

Publiceringen kan göras på två sätt:

- [Enstaka virtuell dator](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-single-vm)
- [Hel prenumeration](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-at-scale)

Varje artikel vägleder dig genom en rad steg för att implementera dessa lösningar:

- Uppdateringshantering
- Ändringsspårning och inventering
- Azure-aktivitetslogg
- Azure Log Analytics Agenthälsa
- Utvärdering av program mot skadlig kod
- Azure Monitor för virtuella datorer
- Azure Security Center

De föregående stegen förklarar hur du etablerar inventeringen och synligheten.
