---
title: 'Guide till Azure-innovation: Förbereda för kundfeedback'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Förbereda för kundfeedback
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: ec17c66fa92abc292a19a8e74c215111d8638a05
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769372"
---
::: zone target="docs"

# <a name="azure-innovation-guide-prepare-for-customer-feedback"></a>Guide till Azure-innovation: Förbereda för kundfeedback

::: zone-end

::: zone target="chromeless"

# <a name="prepare-for-customer-feedback"></a>Förbereda för kundfeedback

::: zone-end

Om innovationsarbetet ska lyckas är det viktigt att användarna inför lösningen, engagerar sig och inte ger upp. Varför?

Att skapa en ny innovativ lösning handlar inte om att ge användarna vad de vill ha, eller vad de tror att de vill ha. Det handlar om att formulera en hypotes som kan testas och sedan förbättras. Testningen kan göras på två sätt: Kvantitativt (feedback från testning), vilket innebär de åtgärder vi hoppas få se. Kvalitativt (feedback från kunder), vilket säger oss vad de här måtten innebär för kunden. Tillsammans utgör de en grund för nästa hypotes och nästa förbättring av lösningen. De här feedbacklooparna är grunden till [processen Skapa-mät-lär dig](../considerations/adoption.md).

Innan du integrerar feedbackloopar behöver du en delad lagringsplats för lösningen. Med en central lagringsplats kan du samla in och agera på all feedback som kommer in om projektet.  [GitHub](https://github.com/) är ett nav för programvara med öppen källkod. Det är också en av de mest använda plattformarna för lagringsplatser i kommersiella utvecklingsprojekt. I artikeln om att [skapa GitHub-lagringsplatser](https://docs.microsoft.com/azure/devops/pipelines/repos/github?view=azure-devops&tabs=yaml) kan du få hjälp att komma igång med din egen lagringsplats.

Alla de här Azure-verktygen kan integreras med (eller är kompatibla med) projekt som lagras i GitHub:

## <a name="quantitative-feedback-for-web-appstabquantitative-apps"></a>[Kvantitativ feedback för webbappar](#tab/Quantitative-Apps)

Application Insights är ett övervakningsverktyg med stöd för kvantitativ feedback om hur din app används, praktiskt taget i realtid. Den här feedbacken kan vara till hjälp när du ska testa och validera den nuvarande hypotesen och forma nästa funktion eller användarberättelse i de kvarvarande uppgifterna.

### <a name="action"></a>Åtgärd

Så här visar du kvantitativa data om dina program:

1. Öppna **App Insights**.
2. Om du inte ser programmet i listan klickar du på länken **Lägg till +** och följer anvisningarna för att börja konfigurera App Insights.
3. Om du ser programmet i listan väljer du det.
4. I fönstret **Översikt** visas en del statistik om programmet. Via länken **Programinstrumentpanel** kan du skapa en anpassad instrumentpanel och visa data som är mer relevanta för din hypotes.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents]" submitText="Go to App Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Om du vill visa data om dina appar öppnar du [Azure-portalen](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents).

::: zone-end

### <a name="learn-more"></a>Läs mer

- [Konfigurera Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/learn/quick-monitor-portal)
- [Kom igång med Azure Monitor App Insights](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-users)
- [Skapa en instrumentpanel för telemetri](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-app-dashboards)

## <a name="quantitative-feedback-for-apistabquantitative-apis"></a>[Kvantitativ feedback för API:er](#tab/Quantitative-APIs)

Den anslutna ekonomin förändrar hur företagen skapar nya innovationer.  Marknader och branscher utvecklas snabbare än någonsin. De här förändringarna kan ta sig många olika uttryck, och företagen måste lära sig hantera **”innovatörens dilemma”** : hur ska ni förhålla er till en snabb förändringstakt utan att snubbla över den pågående verksamheten.

Företag använder API:er externt till att ändra hur de interagerar med kunder och samarbetspartner. Internt används API:er till att smidigt ansluta olika delar av verksamheten. API-ekonomin baseras på fyra byggstenar: sociala funktioner, mobila enheter, analyser och molnet. Appar och tjänster kan snabbt och kostnadseffektivt länkas samman för att skapa mervärde.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Åtgärd

Så här registrerar du kvantitativa data för dina API:er:

1. Öppna **API Management-tjänsten**.
2. Välj önskat API i listan.
3. Välj **Diagnostikinställningar** i avsnittet **Övervakning**.

Så här visar du kvantitativa data om dina API:er:

1. Öppna **API Management-tjänsten**.
2. Välj önskat API i listan.
3. Välj **Program** i avsnittet **Övervakning**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice]" submitText="Go to API Management Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Du öppnar API Management-tjänsten via [Azure-portalen](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice).

::: zone-end

### <a name="learn-more"></a>Läs mer

I den här artikeln får du hjälp att använda [Azure Monitor till att få feedback från API:er](https://docs.microsoft.com/azure/api-management/api-management-howto-use-azure-monitor)

## <a name="qualitative-feedbacktabqualitative"></a>[Kvalitativ feedback](#tab/Qualitative)

I kvarvarande uppgifter (eller på tavlan) registreras feedback som användarberättelser. Det är också här som det relaterade arbetet spåras som åtgärder att utföra. Azure Boards kan integreras direkt i GitHub så att hanteringen av feedback och eventuell källkod kan skötas enhetligt.

::: zone target="docs"

### <a name="action"></a>Åtgärd

För Azure Board och Azure Pipelines krävs en egen portal separat från GitHub och Azure.
Om du vill komma igång med något av de här verktygen går du till [Azure DevOps](https://dev.azure.com/)

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Åtgärd

Så här skapar du ett DevOps-projekt:

1. Gå till **Azure DevOps-projekt**.
2. Klicka på **Skapa DevOps-projekt**.
3. Välj **Körning, ramverk och tjänst**.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/microsoft.visualstudio%2Faccount%2Fproject]" submitText="Go to Azure DevOps Project" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="learn-more"></a>Läs mer

Följande länkar hjälper dig att centralisera och hantera feedback med hjälp av Azure Boards och GitHub:

- [Kom igång med Azure Boards](https://docs.microsoft.com/azure/devops/boards/boards/kanban-quickstart?view=azure-devops)
- [Azure Boards och GitHub](https://docs.microsoft.com/azure/devops/boards/boards/kanban-quickstart?view=azure-devops)

## <a name="close-the-loop-with-pipelinestabpipelines"></a>[Stäng loopen med pipelines](#tab/pipelines)

När du agerar på feedback behöver inte resultatet bli den funktion som kunden efterfrågade. Alla datapunkter bör dock resultera i någon ändring. Den här ändringen kan gälla sättet du tänker på saker. Den kan också vara en helt annan teknisk ändring än vad som begärts. Oavsett så kan du använda pipelines för distribution och verktyg som Azure Pipelines till att snabbt publicera ändringarna, så att de kan delas med kunden ofta.

Så här visar du alla aktiva distributioner relaterade till de program du kör i Azure:

### <a name="action"></a>Åtgärd

Så här visar du aktuella distributioner i din pipeline:

1. Gå till **App Service**.
2. Välj önskat program i listan.
3. Välj **Distributionscenter** i avsnittet **Distribution**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites]" submitText="Go to App Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Om du vill se dina program i App Service öppnar du [Azure-portalen](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites).

::: zone-end

### <a name="learn-more"></a>Läs mer

Här är några fler länkar om att skapa egna pipelines för distribution:

- [Skapa din första pipeline](https://docs.microsoft.com/azure/devops/pipelines/create-first-pipeline?view=azure-devops&tabs=tfs-2018-2)
- [Publiceringsuppgifter på GitHub](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/github-release?view=azure-devops)
