---
title: 'Guide till Azure-innovation: Förbereda för kundfeedback'
description: Förbereda för kundfeedback
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: c78eae75bca30cac541a997fa9d4901b03b277c0
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808370"
---
::: zone target="docs"

# <a name="azure-innovation-guide-prepare-for-customer-feedback"></a>Guide till Azure-innovation: Förbereda för kundfeedback

::: zone-end

::: zone target="chromeless"

# <a name="prepare-for-customer-feedback"></a>Förbereda för kundfeedback

::: zone-end

Nyckeln till en lyckad innovation ligger i att göra det enkelt för användarna att ta till sig den, engagera sig i den och vilja fortsätta använda den. Varför det?

Att skapa en ny innovativ lösning handlar inte om att ge användarna vad de vill ha, eller vad de tror att de vill ha. Det handlar om att formulera en hypotes som kan testas och sedan förbättras. Testningen kan göras på två sätt:

- **Kvantitativ (testningsfeedback):** Den här feedbacken mäter de åtgärder vi hoppas att se.
- **Kvalitativ (kundfeedback):** Den här feedbacken säger oss vad de här måtten innebär för kunden.

Innan du integrerar feedbackslingor måste du ha en delad lagringsplats för din lösning. Med en central lagringsplats kan du samla in och agera på all feedback som kommer in om projektet. [GitHub](https://github.com) är ett nav för programvara med öppen källkod. Det är också en av de mest använda plattformarna för lagringsplatser i kommersiella utvecklingsprojekt. I artikeln om att [skapa GitHub-lagringsplatser](https://docs.microsoft.com/azure/devops/pipelines/repos/github?view=azure-devops&tabs=yaml) kan du få hjälp att komma igång med din egen lagringsplats.

Alla de här Azure-verktygen kan integreras med (eller är kompatibla med) projekt som lagras i GitHub:

## <a name="quantitative-feedback-for-web-appstabquantitative-apps"></a>[Kvantitativ feedback för webbappar](#tab/Quantitative-Apps)

Application Insights är ett övervakningsverktyg som gör att du kan få kvantitativ feedback om hur din app används, praktiskt taget i realtid. Den här feedbacken kan vara till hjälp när du ska testa och validera den nuvarande hypotesen och forma nästa funktion eller användarberättelse i de kvarvarande uppgifterna.

### <a name="action"></a>Åtgärd

Så här visar du kvantitativa data om dina program:

1. Gå till **Application Insights**.
   - Om du inte ser programmet i listan väljer du **Lägg till** och följer anvisningarna för att börja konfigurera Application Insights.
   - Om du ser programmet i listan väljer du det.
1. I fönstret **Översikt** visas en del statistik om programmet. Välj **Programinstrumentpanel** för att skapa en anpassad instrumentpanel och visa data som är mer relevanta för din hypotes.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents]" submitText="Go to Application Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Om du vill visa data om dina appar går du till [Azure-portalen](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents).

::: zone-end

### <a name="learn-more"></a>Läs mer

- [Konfigurera Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/learn/quick-monitor-portal)
- [Kom igång med Azure Monitor Application Insights](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-users)
- [Skapa en instrumentpanel för telemetri](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-app-dashboards)

## <a name="quantitative-feedback-for-apistabquantitative-apis"></a>[Kvantitativ feedback för API:er](#tab/Quantitative-APIs)

Den anslutna ekonomin förändrar hur företagen skapar nya innovationer. Marknader och branscher utvecklas snabbare än någonsin. De här förändringarna kan ta sig många olika uttryck, och företagen måste lära sig hantera _”innovatörens dilemma”_ : att kunna hålla en snabb förändringstakt utan att det stör den pågående verksamheten.

Företag använder API:er externt till att ändra hur de interagerar med kunder och samarbetspartner. Internt används API:er till att smidigt ansluta olika delar av verksamheten. API-ekonomin baseras på fyra byggstenar: sociala funktioner, mobila enheter, analyser och molnet. Appar och tjänster kan snabbt och kostnadseffektivt länkas samman för att skapa mervärde.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Åtgärd

Så här registrerar du kvantitativa data för dina API:er:

1. Gå till **API Management-tjänster**.
2. Välj önskat API i listan.
3. Välj **Diagnostikinställningar** i avsnittet **Övervakning**.

Så här visar du kvantitativa data om dina API:er:

1. Gå till **API Management-tjänster**.
2. Välj önskat API i listan.
3. Välj **Program** i avsnittet **Övervakning**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice]" submitText="Go to API Management services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Du öppnar API Management-tjänster via [Azure-portalen](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice).

::: zone-end

### <a name="learn-more"></a>Läs mer

- [Använd Azure Monitor till att få feedback från API:er](https://docs.microsoft.com/azure/api-management/api-management-howto-use-azure-monitor)

## <a name="qualitative-feedbacktabqualitative"></a>[Kvalitativ feedback](#tab/Qualitative)

I kvarvarande uppgifter (eller på tavlan) registreras feedback som användarberättelser. Det är också här som det relaterade arbetet spåras som åtgärder att utföra. Azure Boards kan integreras direkt i GitHub så att hanteringen av feedback och eventuell källkod kan skötas enhetligt.

::: zone target="docs"

### <a name="action"></a>Åtgärd

För Azure Board och Azure Pipelines krävs en egen portal separat från GitHub och Azure.
Om du vill komma igång med något av de här verktygen går du till [Azure DevOps](https://dev.azure.com).

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Åtgärd

Så här skapar du ett DevOps-projekt:

1. Gå till **Azure DevOps Projects**.
2. Välj **Skapa DevOps-projekt**.
3. Välj **Körning, ramverk och tjänst**.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/microsoft.visualstudio%2Faccount%2Fproject]" submitText="Go to Azure DevOps Projects" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="learn-more"></a>Läs mer

De här artiklarna visar hur du kan centralisera och hantera feedback med hjälp av Azure Boards och GitHub:

- [Kom igång med Azure Boards](https://docs.microsoft.com/azure/devops/boards/get-started/?view=azure-devops)
- [Azure Boards och GitHub](https://docs.microsoft.com/azure/devops/boards/github?view=azure-devops)

## <a name="close-the-loop-with-pipelinestabpipelines"></a>[Stäng loopen med pipelines](#tab/pipelines)

Att agera på feedback behöver inte alltid betyda att du lägger till en funktion som kunden efterfrågar. Men alla datapunkter bör dock resultera i någon ändring. En ändring kan till exempel vara att du ändrar åsikt om något. Eller så kan du behöva hitta en annan teknisk lösning än den som begärts. Oavsett så kan du använda pipelines för distribution och verktyg som Azure Pipelines till att snabbt publicera ändringarna, så att de kan delas med kunden ofta.

### <a name="action"></a>Åtgärd

Så här visar du aktuella distributioner i din pipeline:

1. Gå till **App Services**.
2. Välj önskat program i listan.
3. Välj **Distributionscenter** i avsnittet **Distribution**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites]" submitText="Go to App Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Om du vill se dina program i App Service öppnar du [Azure-portalen](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites).

::: zone-end

### <a name="learn-more"></a>Läs mer

Börja bygga ut dina pipelines för distribution:

- [Skapa din första pipeline](https://docs.microsoft.com/azure/devops/pipelines/create-first-pipeline?view=azure-devops&tabs=tfs-2018-2)
- [Publiceringsuppgifter på GitHub](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/github-release?view=azure-devops)
