---
title: 'Guide till Azure-innovation: Förutspå och påverka'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig att förutspå och påverka användningen av Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: b2ed1b072d5226649e5248e350edfa3578978c4c
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769243"
---
::: zone target="docs"

# <a name="azure-innovation-guide-predict-and-influence"></a>Guide till Azure-innovation: Förutspå och påverka

::: zone-end

::: zone target="chromeless"

# <a name="predict-and-influence"></a>Förutspå och påverka

::: zone-end

Som innovatörer så har företaget tillgång till insikter om data, olika beteenden och kundernas behov. Genom att studera dessa insikter kan ni förutsäga kundernas behov redan innan de själva blir medvetna om dem. I den här artikeln introducerar vi några metoder för att leverera prediktiva lösningar. I den senare delen går vi igenom några metoder för att integrera förutsägelserna i din lösning så att du kan påverka kundernas beteenden.

Använd den här tabellen till att hitta den bästa lösningen sett till just dina implementeringsbehov.

|Tjänst  |Färdiga modeller  |Skapa och experimentera  |Träna och skapa med Python|Nödvändiga kunskaper|
|---------|---------|---------|---------|---------|
|Cognitive Services|Ja|Nej|Nej|Kunskaper om API:er och utveckling|
|Azure Machine Learning Studio|Ja|Ja|Nej|Allmän förståelse för prediktiva algoritmer|
|Azure Machine Learning-tjänsten|Ja|Ja|Ja|Data Scientist|

## <a name="azure-cognitive-servicestabcognitiveservices"></a>[Azure Cognitive Services](#tab/CognitiveServices)

Den snabbaste och enklaste vägen till förutsägelser är Azure Cognitive Services. Med Cognitive Services kan du göra förutsägelser baserat på befintliga modeller som inte behöver tränas upp ytterligare. De här tjänsterna passar perfekt när det inte finns någon data scientist i personalen som kan sköta inträningen av den prediktiva modellen. För vissa tjänster krävs ingen utbildning alls. Andra kräver ytterst lite utbildning.

Du hittar en lista med tillgängliga tjänster och hur mycket utbildning som krävs i [Cognitive Services och maskininlärning](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-and-machine-learning#service-requirements-for-the-data-model).

### <a name="action"></a>Åtgärd

Så här använder du ett API för kognitiva tjänster:

1. Gå till **Cognitive Services**.
2. Leta rätt på en kognitiv tjänst från Marketplace genom att klicka på **Lägg till+** .
3. Om du vet namnet på tjänsten du vill använda kan du ange det i textrutan **Sök på Marketplace-** .
4. Om du istället vill visa en lista med kognitiva tjänster klickar du på länken **Visa fler** Cognitive Services-rubriken.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Gå direkt till Cognitive Services i [Azure-portalen](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts).

::: zone-end

## <a name="azure-machine-learning-studiotabmachinelearningstudio"></a>[Azure Machine Learning Studio](#tab/MachineLearningStudio)

Om de befintliga modellerna i de kognitiva tjänsterna inte överensstämmer med förutsägelse du vill göra kan det finnas ett sätt att skapa önskade förutsägelser i Azure Machine Learning Studio, utan att det krävs kompetens som data scientist.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Åtgärd

Du kan skapa en modell och experimentera med den i Azure Machine Learning Studio:

1. Öppna **Azure Machine Learning Studio**.
2. Klicka på **Skapa en Machine Learning Studio-arbetsyta** och följ anvisningarna för att skapa en arbetsyta.
3. Den nya arbetsytan har ett gränssnitt med dra-och-släpp-funktion där du kan skapa och experimentera med modellen, som ett alternativ till djupinlärning.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2Fworkspaces]" submitText="Go to Azure Machine Learning Studio" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Gå direkt till Azure Machine Learning Studio i [Azure-portalen](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2Fworkspaces).

::: zone-end

## <a name="azure-machine-learning-servicetabmachinelearningservice"></a>[Azure Machine Learning-tjänsten](#tab/MachineLearningService)

Med Azure Machine Learning-tjänsten får du tillgång till en mer ingående och kodbaserad metod för djupinlärning av kundernas datamängder. En data scientist kan använda språk som Python till att träna upp och sedan skapa en algoritm som förutsäger kundernas behov.

### <a name="action"></a>Åtgärd

En data scientist kan använda en Azure Machine Learning-tjänst till att träna upp och skapa en modell med hjälp av avancerade språk som Python:

1. Öppna **Azure Machine Learning-tjänsten**.
2. Klicka på **Skapa arbetsytor för Machine Learning-tjänsten** och följ anvisningarna för att skapa en arbetsyta.
3. På den nya arbetsytan används en kodbaserad metod där data scientists kan träna upp och skapa modeller där mer avancerad analys används till att förutsäga kundernas behov.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2Fworkspaces]" submitText="Go to Azure Machine Learning Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Gå direkt till Azure Machine Learning Studio i [Azure-portalen](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2Fworkspaces).

::: zone-end

## <a name="influence"></a>Påverkan

Alla metoder som beskrivs ovan resulterar i ett API där förutsägelsemodellen exponeras för olika program. Du kan använda de här metoderna i din lösning och mata in data som samlas in från kunderna till ett prediktivt API. Resultaten kan sedan integreras i kundernas upplevelse som förslag på nästa steg.

Syftet med de här stegen är att forma kundens beteende och påverka hur kunden reagerar. Eftersom de föreslagna nästa stegen baseras på prediktiva algoritmer så används tidigare kunder och tillgängliga data till att förutsäga kundens behov och att uppfylla det behovet, ofta innan kunden ens själv blir medveten om behovet.
