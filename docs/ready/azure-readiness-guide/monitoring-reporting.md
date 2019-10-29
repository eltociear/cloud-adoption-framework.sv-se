---
title: Övervakning och rapportering i Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig hur du konfigurerar övervakning, rapportering och aviseringar för din Azure-miljö.
author: timleyden
ms.author: tileyden
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 5cb88bba1b82bf4255fb13f9ac9d415018316dec
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548898"
---
# <a name="monitoring-and-reporting-in-azure"></a>Övervakning och rapportering i Azure

Azure har en serie tjänster som tillsammans utgör en heltäckande lösning för att samla in, analysera och agera utifrån telemetrin i din app och de Azure-resurser den använder. Tjänsterna kan dessutom utökas så att de övervakar kritiska lokala resurser så att du får en hybridövervakningsmiljö.

# <a name="azure-monitortabazuremonitor"></a>[Azure Monitor](#tab/AzureMonitor)

Azure Monitor är en enhetlig hubb för alla övervaknings- och diagnostikdata i Azure. Du kan använda den för att få insyn i dina resurser. Med Azure Monitor kan du hitta och åtgärda problem och optimera prestanda. Du kan också förstå kundbeteendet.

- **Övervaka och visualisera mått.** Mått är numeriska värden från Azure-resurser som hjälper dig att förstå dina systems hälsotillstånd. Anpassa diagram för dina instrumentpaneler och använd arbetsböcker för rapportering.

- **Köra frågor mot och analysera loggar.** Loggarna kan vara aktivitets- och diagnostikloggar från Azure. Samla in ytterligare loggar från andra lösningar för övervakning och hantering som du använder i molnet eller lokalt. Använd Log Analytics som centralt datalager för alla dessa data. Därifrån kan köra du frågor för att felsöka problem eller visualisera data.

- **Konfigurera aviseringar och åtgärder.** Aviseringar kan informera dig om kritiska tillstånd proaktivt. Du kan vidta korrigerande åtgärder baserat på utlösare för mått, loggar eller problem med tjänster. Du kan ställa in olika meddelanden och åtgärder och skicka data till dina hanteringsverktyg för IT-tjänster.

::: zone target="docs"

 Börja övervaka dina:

- [Program](https://docs.microsoft.com/azure/application-insights/app-insights-overview)
- [Containrar](https://docs.microsoft.com/azure/monitoring/monitoring-container-overview)
- [Virtuella datorer](https://docs.microsoft.com/azure/monitoring/monitoring-service-map)
- [Nätverk](https://docs.microsoft.com/azure/networking/network-monitoring-overview)

Du kan hitta fler lösningar för resursövervakning på Azure Marketplace.

Om du vill utforska Azure Monitor går du till [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview).

## <a name="learn-more"></a>Läs mer

Mer information finns i [dokumentationen om Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics).

::: zone-end

::: zone target="chromeless"

## <a name="action"></a>Åtgärd

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview]" submitText="Explore Azure Monitor" :::

::: zone-end

# <a name="azure-service-healthtabazureservicehealth"></a>[Azure Service Health](#tab/AzureServiceHealth)

Azure Service Health tillhandahåller en anpassad vy över hälsotillstånden för de Azure-tjänster och Azure-regioner som du använder. Information om aktiva problem publiceras till Service Health för att hjälpa dig att förstå hur de inverkar på dina resurser. Regelbundna uppdateringar håller dig informerad när problemet har lösts.

Vi publicerar också planerade underhållshändelser i Service Health så att du får information om ändringar som kan påverka resursernas tillgänglighet. Konfigurera aviseringar för Service Health som meddelar när problem med tjänsten, planerat underhåll eller andra ändringar kan påverka de Azure-tjänster och -regioner du använder.

I Azure Service Health ingår:

- **Azure-status:** En global vy över Azure-tjänsternas hälsotillstånd.
- **Service Health:** En anpassad vy över hälsotillståndet hos dina Azure-tjänster.
- **Resource Health:** En mer ingående vy över hälsotillståndet för varje enskild resurs.

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

## <a name="action"></a>Åtgärd

Om du vill skapa en Service Health-avisering:

1. går du till **Service Health**.
2. Välj **Hälsoaviseringar**.
3. Skapa en Service Health-avisering.

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts]" submitText="Go to Service Health" :::

::: zone-end

::: zone target="docs"

Om du vill ställa in en Service Health-avisering går du till [Azure-portalen](https://portal.azure.com/#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts).

## <a name="learn-more"></a>Läs mer

Läs mer i [Azure Service Health-dokumentationen](https://docs.microsoft.com/azure/service-health).

::: zone-end

# <a name="azure-advisortabazureadvisor"></a>[Azure Advisor](#tab/AzureAdvisor)

Azure Advisor är en anpassad och kostnadsfri molnkonsult som hjälper dig att följa bästa praxis för Azure-distributioner. Tjänsten analyserar din resurskonfiguration och användningstelemetri och rekommenderar lösningar som kan optimera din miljö. Rekommendationerna är indelade i fyra kategorier:

- **Hög tillgänglighet:** Förbättra kontinuiteten i dina verksamhetskritiska appar. Rekommendationerna kan gälla att lägga till virtuella datorer i en tillgänglighetsuppsättning eller att lägga till geo-redundanta slutpunkter.
- **Säkerhet:** Identifiera hot och sårbarheter som kan leda till säkerhetsproblem. Rekommendationerna kan gälla att använda diskkryptering eller nätverkssäkerhetsgrupper.
- **Prestanda:** Gör dina appar snabbare. Rekommendationerna kan gälla att förbättra svarstiden för SQL-frågor genom att skapa index eller konfigurera om dina Traffic Manager-inställningar.
- **Kostnad:** Optimera och minska din totalkostnad för Azure. Rekommendationerna kan gälla att ändra storlek på eller stänga av virtuella datorer som används för lite eller att byta till Azure-reservationer för att minska den totala ägandekostnaden.

Rekommendationerna i Advisor baseras på de resurser du distribuerar och de åtgärder du utför i Azure. Du kan kontrollera Advisor regelbundet så att du får aktuella rekommendationer.

::: zone target="chromeless"

## <a name="action"></a>Åtgärd

::: form action="OpenBlade[#blade/Microsoft_Azure_Expert/AdvisorBlade]" submitText="Explore Azure Advisor" :::

::: zone-end

::: zone target="docs"

Om du vill utforska Azure Advisor går du till [Azure-portalen](https://portal.azure.com/#blade/Microsoft_Azure_Expert/AdvisorBlade).

## <a name="learn-more"></a>Läs mer

Mer information finns i [dokumentationen om Azure Advisor](https://docs.microsoft.com/azure/advisor).

::: zone-end

# <a name="azure-security-centertabazuresecuritycenter"></a>[Azure Security Center](#tab/AzureSecurityCenter)

Azure Security Center är också en viktig del i din övervakningsstrategi. Där kan du övervaka säkerheten för dina datorer, nätverk, lagringsutrymmen, datatjänster och appar. Security Center en avancerad hotidentifiering via maskininlärning och beteendeanalys som hjälper dig att identifiera aktiva hot mot dina Azure-resurser. Dessutom får du ett skydd som blockerar skadlig kod och annan oönskad kod, och minskar den yta som är exponerad för brute force-attacker och andra nätverksattacker.

När Security Center identifierar ett hot kan du få en säkerhetsvarning med de åtgärder du behöver vidta för att reagera på en attack. Det skapar också en rapport med information om hotet som har identifierats.

Azure Security Center är tillgängligt på två nivåer – kostnadsfri och standard. Funktioner som säkerhetsrekommendationer är tillgängliga utan kostnad. På Standard-nivån får du ytterligare skydd som avancerad hotidentifiering och skydd för arbetsbelastningar i hybridmoln.

::: zone target="chromeless"

## <a name="action"></a>Åtgärd

**Prova Standard-nivån kostnadsfritt i 30 dagar.**

När du aktiverar och ställer in säkerhetsprinciper för prenumerationens resurser kan du se säkerhetstillståndet för dina resurser och eventuella problem i avsnittet **Skydd**. Problemen visas även i en lista på panelen **Recommendations (Rekommendationer)** .

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end

::: zone target="docs"

Om du vill utforska Azure Security Center går du till [Azure-portalen](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0).

## <a name="learn-more"></a>Läs mer

Läs mer i [dokumentationen om Azure Security Center](https://docs.microsoft.com/azure/security-center).

::: zone-end
