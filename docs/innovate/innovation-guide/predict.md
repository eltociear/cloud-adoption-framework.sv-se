---
title: 'Azure-innovation: Förutspå och påverka'
description: Lär dig mer om Azure-lösningar för att förutsäga kundernas behov och integrera förutsägelser i din lösning för att påverka kundbeteendet.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: adb39a25cfb232b19bd983e5d4e0ab7d7370add1
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80356598"
---
::: zone target="docs"

# <a name="azure-innovation-guide-predict-and-influence"></a>Guide till Azure-innovation: Förutspå och påverka

::: zone-end

::: zone target="chromeless"

# <a name="predict-and-influence"></a>Förutspå och påverka

::: zone-end

Som innovatörer så har företaget tillgång till insikter om data, olika beteenden och kundernas behov. Genom att studera dessa insikter kan ni förutsäga kundernas behov, kanske redan innan de själva blir medvetna om dem. I den här artikeln introducerar vi några metoder för att leverera prediktiva lösningar. I den sista delen går vi igenom några metoder för att integrera förutsägelserna i din lösning så att du kan påverka kundernas beteenden.

Använd den här tabellen till att hitta den bästa lösningen sett till just dina implementeringsbehov.

|Tjänst  |Fördefinierade modeller  |Skapa och experimentera  |Träna och skapa med Python|Nödvändiga kunskaper|
|---------|---------|---------|---------|---------|
|Azure Cognitive Services|Ja|Inga|Inga|Kunskaper om API:er och utveckling|
|Azure Machine Learning Studio|Ja|Ja|Inga|Allmän förståelse för prediktiva algoritmer|
|Azure Machine Learning-tjänst|Ja|Ja|Ja|Data Scientist|

## <a name="azure-cognitive-services"></a>[Azure Cognitive Services](#tab/CognitiveServices)

Den snabbaste och enklaste vägen till att förutsäga kundernas behov är att använda Azure Cognitive Services. Med Cognitive Services kan du göra förutsägelser baserat på befintliga modeller som inte behöver tränas upp ytterligare. De här tjänsterna passar perfekt och är effektiva när det inte finns någon data scientist i personalen som kan träna den prediktiva modellen. För vissa tjänster krävs ingen utbildning alls. Andra tjänster kräver ytterst lite utbildning.

Du hittar en lista med tillgängliga tjänster och hur mycket utbildning som krävs i [Cognitive Services och maskininlärning](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-and-machine-learning#service-requirements-for-the-data-model).

### <a name="action"></a>Åtgärd

Så här använder du ett API för kognitiva tjänster:

1. Gå till **Cognitive Services** i [Azure-portalen](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.CognitiveServices%2FAccounts).
2. Välj **Lägg till** för att leta reda på ett API för kognitiva tjänster i Azure Marketplace.
3. Gör något av följande:
   - Om du vet namnet på tjänsten du vill använda kan du ange det i rutan **Sök på Marketplace**.
   - Om du istället vill visa en lista med API:er för kognitiva tjänster klickar du på länken **Visa fler** bredvid Cognitive Services-rubriken.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Gå direkt till Cognitive Services i [Azure-portalen](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts).

::: zone-end

## <a name="azure-machine-learning-studio"></a>[Azure Machine Learning Studio](#tab/MachineLearningStudio)

Om de befintliga modellerna i de kognitiva tjänsterna inte överensstämmer med den förutsägelse du vill göra kan det finnas ett sätt att skapa önskade förutsägelser i Azure Machine Learning Studio, utan att det krävs kompetens som data scientist.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Åtgärd

Så här kan du skapa en modell och experimentera med den i Azure Machine Learning Studio:

1. Gå till **Azure Machine Learning Studio** i [Azure-portalen](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2FWorkspaces).
2. Välj **Skapa en Machine Learning Studio-arbetsyta** och följ sedan anvisningarna för att skapa en arbetsyta.

   Den nya arbetsytan har ett gränssnitt med dra-och-släpp-funktion där du kan skapa och experimentera med modellen, som ett alternativ till djupinlärning.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2FWorkspaces]" submitText="Go to Azure Machine Learning Studio" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Gå direkt till Azure Machine Learning Studio i [Azure-portalen](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2FWorkspaces).

::: zone-end

## <a name="azure-machine-learning-service"></a>[Azure Machine Learning-tjänst](#tab/MachineLearningService)

Med Azure Machine Learning-tjänsten får du tillgång till en mer ingående och kodbaserad metod som krävs för djupinlärning av kundernas datamängder. En data scientist kan använda språk som Python till att träna upp och sedan skapa en algoritm som förutsäger kundernas behov.

### <a name="action"></a>Åtgärd

En data scientist kan använda en Azure Machine Learning-tjänst till att träna upp och skapa en modell med hjälp av avancerade språk som Python:

1. Öppna **Azure Machine Learning-tjänsten**.
2. Välj **Skapa arbetsytor för Machine Learning-tjänsten** och följ sedan anvisningarna för att skapa en arbetsyta.
3. På den nya arbetsytan används en kodbaserad metod som gör att data scientists kan träna upp och skapa modeller som kräver mer avancerad analys för att förutsäga kundernas behov.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces]" submitText="Go to Azure Machine Learning service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Gå direkt till Azure Machine Learning Studio i [Azure-portalen](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces).

::: zone-end

## <a name="influence"></a>Påverkan

Alla metoder som beskrivs ovan resulterar i ett API där förutsägelsemodellen exponeras för olika program. Du kan använda de här metoderna i din lösning och mata in data som samlas in från kunderna till ett prediktivt API. Resultaten kan sedan integreras i kundernas upplevelse som förslag på nästa steg.

Dessa förslag på nästa steg kan hjälpa till att forma kundernas beteendemönster och påverka hur kunderna reagerar. Eftersom de föreslagna nästa stegen baseras på prediktiva algoritmer så används tidigare kundbehov och tillgängliga data till att förutsäga framtida kundbehov och att uppfylla det behovet, ofta innan kunden ens själv blir medveten om behovet.
