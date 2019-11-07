---
title: 'Guide till Azure-innovation: Demokratisera data'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig hur du kan demokratisera data med hjälp av Azure.
author: absheik
ms.author: absheik
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 6c1e253d2ff49c331f4f1c153124f2ca06c81c36
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565552"
---
::: zone target="docs"

# <a name="azure-innovation-guide-democratize-data"></a>Guide till Azure-innovation: Demokratisera data

::: zone-end

::: zone target="chromeless"

# <a name="democratize-data"></a>Demokratisera data

::: zone-end

Ett av de första stegen för att demokratisera data är att förbättra datasynligheten. Att katalogisera och hantera datadelning kan hjälpa företag att få ut det mesta av befintliga informationstillgångar. Med Data Catalog kan användare som hanterar data enkelt identifiera och förstå datakällorna. Azure Data Catalog möjliggör hantering i ett företag medan Azure Data Share möjliggör hantering och delning utanför företaget.

Azure-tjänster som tillhandahåller databehandling som Azure Time Series Insights och Stream Analytics är andra funktioner som kunder och partner kan använda för sina innovationsbehov.

# <a name="catalogtabcatalog"></a>[Katalog](#tab/Catalog)

## <a name="azure-data-catalog"></a>Azure Data Catalog

Azure Data Catalog hjälper datakonsumenter med identifiering och underlättar för dataproducenter som arbetar med underhåll av informationstillgångar. Data Catalog bygger en bro mellan IT och verksamheten och låter alla bidra med sina erfarenheter. Du kan lagra dina data där du vill ha dem och ansluta till de verktyg som du vill använda. Med Azure Data Catalog kan du styra vem som ska kunna identifiera registrerade datatillgångar. Du kan integrera befintliga verktyg och processer med hjälp av öppna REST-API:er.

> [!div class="checklist"]
>
> - Registrera dig
> - Sök och anteckna
> - Anslut och hantera

::: zone target="docs"

**Gå till [dokumentationen för Azure Data Catalog](https://docs.microsoft.com/azure/data-catalog)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Åtgärd

Du kan endast använda en Azure Data Catalog per organisation. Om en datakatalog redan har skapats för din organisation kan du inte lägga till fler kataloger.

Så här skapar du en Azure Data Catalog för din organisation:

1. Gå till **Azure Data Catalog**.
2. Välj **Skapa**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataCatalog%2Fcatalogs]" submitText="Go to Azure Data Catalog" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

# <a name="sharetabshare"></a>[Dela](#tab/Share)

## <a name="azure-data-share"></a>Azure Data Share

Att uppnå balans mellan att öppet dela data och ha kontroll över vilka data som delas och med vem är en viktig faktor för innovation. När organisationer försöker demokratisera data är det lätt att de blir överväldigade av den enorma volymen, takten och livscykeln för dessa data. Med hjälp av Azure Data Share kan leverantörer ha kontroll över hur data hanteras genom att ange användningsvillkor för dataresursen. Datakonsumenten måste acceptera dessa villkor innan de kan ta emot data. Dataleverantörer kan ange hur ofta datakonsumenter får uppdateringar. Åtkomsten till nya uppdateringar kan när som helst återkallas av dataleverantören.

> [!div class="checklist"]
>
> - Skapa en dataresurs.
> - Lägg till datauppsättningar i dataresursen.
> - Aktivera ett synkroniseringsschema för dataresursen.
> - Lägg till mottagare i dataresursen.

::: zone target="docs"
**Gå till [dokumentationen för Azure Data Share](https://docs.microsoft.com/azure/data-share)**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Åtgärd

Så här skapar du en dataresurs:

1. Gå till **Dataresurser i Azure**.
2. Välj **Skapa dataresurs**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataShare%2Faccounts]" submitText="Go to Azure Data Shares" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

# <a name="insightstabinsights"></a>[Insikter](#tab/Insights)

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

I Azure Time Series Insights finns oändliga möjligheter till datainnovation. Du får tillgång till datautforskning av dataströmmar nästan i realtid och lagring på flera nivåer för tidsseriedata i IoT-skala. Du får också modeller för att kontextualisera råtelemetridata och härleda tillgångsbaserade insikter. Du kan leverera smidig och kontinuerlig integrering med andra datalösningar och tillhandahålla rotorsaksanalys och avvikelseidentifiering, inklusive anpassade programalternativ på Time Series Insights-plattformen.

> [!div class="checklist"]
>
> - Planera Time Series Insights-miljön.
> - Visualisera data i Utforskaren.
> - Förstå datakvarhållning.
> - Utveckla och dela anpassade vyer.

::: zone target="docs"

**Gå till [Azure Time Series Insights – översikt](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-update-overview)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Åtgärd

Så här skapar du en Azure Time Series Insights-miljö:

1. Gå till **Azure Time Series Insights-miljöer**.
2. Välj **Skapa Time Series Insights-miljö**.
3. Peka den här miljön till en händelsekälla, antingen Azure IoT Hub eller Event Hubs.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.TimeSeriesInsights%2Fenvironments]" submitText="Go to Azure Time Series Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
