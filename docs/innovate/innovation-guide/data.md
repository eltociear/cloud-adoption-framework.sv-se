---
title: 'Guide till Azure-innovation: Demokratisera data'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig att demokratisera data med Azure.
author: absheik
ms.author: absheik
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 65c1ecd1d722286fb495af3069862131629c35d1
ms.sourcegitcommit: 0d14d89b9004a65a322724342cb5086ad2c77467
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/22/2019
ms.locfileid: "72777095"
---
::: zone target="docs"

# <a name="azure-innovation-guide-democratize-data"></a>Guide till Azure-innovation: Demokratisera data

::: zone-end

::: zone target="chromeless"

# <a name="democratize-data"></a>Demokratisera data

::: zone-end

Ett av de första stegen för att demokratisera data är att förbättra datasynligheten. Att katalogisera och hantera datadelning kan hjälpa företag att få ut det mesta av befintliga informationstillgångar. Data Catalog gör det enkelt för användare som hanterar data att identifiera och förstå datakällorna. Azure Data Catalog möjliggör hantering i ett företag medan Azure Data Share möjliggör hantering och delning utanför företaget.

Azure-tjänster som tillhandahåller databehandling som Azure Time Series Insights och Stream Analytics är andra funktioner som kunder och partner kan dra nytta av för sina innovationsbehov.

# <a name="catalogtabcatalog"></a>[Katalog](#tab/Catalog)

## <a name="azure-data-catalog"></a>Azure Data Catalog

Azure Data Catalog hjälper datakonsumenter med identifiering och dataproducenter med underhåll av informationstillgångar. Bygg en bro mellan IT och verksamheten och låt alla bidra med sina erfarenheter. Lagra dina data var du vill, anslut med de verktyg du väljer själv. Styr vem som får identifiera registrerade datatillgångar. Integrera befintliga verktyg och processer med öppna REST-API:er.

> [!div class="checklist"]
>
> - Registrera dig
> - Sök och anteckna
> - Anslut och hantera

::: zone target="docs"

**Gå till [Azure Data Catalog](https://docs.microsoft.com/azure/data-catalog).**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Åtgärd

Endast en Azure Data Catalog stöds per organisation. Om en katalog redan har skapats för din organisation kan du inte lägga till fler kataloger.

Så här skapar du Azure Data Catalog för din organisation:

1. Gå till **Azure Data Catalog**.
2. Klicka på knappen **Skapa**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataCatalog%2Fcatalogs]" submitText="Go to Azure Data Catalog" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

# <a name="sharetabshare"></a>[Dela](#tab/Share)

## <a name="azure-data-share"></a>Azure Data Share

Att uppnå balans mellan att öppet dela data och ha kontroll över vilka data som delas och med vem är en viktig faktor för innovation. I sin strävan att demokratisera data är det lätt att organisationer blir överväldigade av den enorma volymen, takten och livscykeln för sådana data. Med hjälp av Azure Data Share kan leverantören ha kontroll över hur data hanteras genom att ange användningsvillkor för dataresursen. Datakonsumenten måste acceptera dessa villkor innan de kan ta emot data. Dataleverantörer kan ange hur ofta datakonsumenter får uppdateringar. Åtkomsten till nya uppdateringar kan när som helst återkallas av dataleverantören.

> [!div class="checklist"]
>
> - Skapa en dataresurs.
> - Lägg till datauppsättningar i dataresursen.
> - Aktivera ett synkroniseringsschema för dataresursen.
> - Lägg till mottagare i dataresursen.

::: zone target="docs"
**Gå till [Azure Data Share](https://docs.microsoft.com/azure/data-share).**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Åtgärd

Skapa en Azure Data Share:

1. Gå till **Azure Data Share**.
2. Klicka på **Create Data Share** (Skapa dataresurs).

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataShare%2Faccounts]" submitText="Go to Azure Data Share" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

Använd [Azure Open Datasets](https://docs.microsoft.com/azure/open-datasets/overview-what-are-open-datasets) för att utöka din analys med data för [helgdagar](https://azure.microsoft.com/services/open-datasets/catalog/public-holidays), [väder](https://azure.microsoft.com/services/open-datasets/catalog/noaa-global-forecast-system) och [rumsliga bilder](https://azure.microsoft.com/services/open-datasets/catalog/hls) i dina modeller.

Information om [demokratisering av affärsprocesser](https://docs.microsoft.com/business-applications-release-notes/october18/microsoft-flow/democratize-business-processes) och [stärka medborgarutvecklare](https://docs.microsoft.com/business-applications-release-notes/october18/microsoft-flow/empower-citizen-developers) är nästa steg.

# <a name="insightstabinsights"></a>[Insikter](#tab/Insights)

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Möjligheterna för datainnovation är ändlösa med datautforskning nästan i realtid av dataströmmar och lagring i flera lager för tidsseriedata och modeller i IoT-skala för att kontextualisera råtelemetridata och härleda tillgångsbaserade insikter. Du kan leverera smidig och kontinuerlig integrering med andra datalösningar, tillhandahålla rotorsaksanalys och avvikelseidentifiering, inklusive anpassade programalternativ på Time Series Insights-plattformen.

> [!div class="checklist"]
>
> - Planera Time Series Insights-miljön.
> - Visualisera data i Utforskaren.
> - Förstå datakvarhållning.
> - Utveckla och dela anpassade vyer.

::: zone target="docs"

**Gå till [Azure Time Series Insights](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-update-overview).**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Åtgärd

Så här skapar du en Azure Time Series Insights-miljö:

1. Gå till **Azure Time Series Insights**.
2. Klicka på **Skapa Time Series Insights-miljö**.
3. Peka den här miljön till en händelsekälla, antingen IoT Hub eller Event Hub.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.TimeSeriesInsights%2Fenvironments]" submitText="Go to Azure Time Series Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
