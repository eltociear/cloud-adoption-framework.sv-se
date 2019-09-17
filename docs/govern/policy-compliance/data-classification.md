---
title: Vad är dataklassificering?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vad är dataklassificering?
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: d293aa5b4427b8f714175b85c6bb5197b53f107a
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027206"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-data-classification"></a>Vad är dataklassificering?

Med data klassificering kan du fastställa och tilldela ett värde till din organisations data och det är en gemensam utgångs punkt för styrning. Data klassificerings processen kategoriserar data efter känslighet och affärs påverkan för att identifiera risker. När data har klassificerats kan de hanteras på ett sätt som skyddar känsliga eller viktiga data från stöld eller förlust.

## <a name="understand-data-risks-then-manage-them"></a>Förstå data risker och hantera dem

Innan en risk kan hanteras måste den förstås. I händelse av ansvars skyldighet för data intrång börjar det förstås med data klassificering. Data klassificering är en process för att associera en meta data-egenskap till varje till gång i en digital fastighet som identifierar den typ av data som är kopplade till till gången.

Microsoft rekommenderar att alla till gångar som har identifierats som en potentiell kandidat för migrering eller distribution till molnet ska ha dokumenterade metadata för att registrera data klassificering, affärs kritiskhet och fakturerings ansvar. Dessa tre klassificerings punkter kan vara ett långt sätt att förstå och minimera risker.

## <a name="microsofts-data-classification"></a>Microsofts data klassificering

Följande är en lista över klassificeringar som används av Microsoft. Beroende på din bransch eller befintliga säkerhets krav kan data klassificerings standarder redan finnas i din organisation. Om ingen standard finns, bjuder vi in dig att använda den här exempel klassificeringen för att bättre förstå din egen digitala egendom och risk profil.

- **Icke-företag:** Data från din personliga liv som inte tillhör Microsoft.
- **Folkhälsan** Affärs data som är allmänt tillgängliga och godkända för offentlig konsumtion.
- **Redovisningsjournalmallar** Affärs data som inte är avsedda för en offentlig publik.
- **Sekretesskydd** Affärs data som kan orsaka skada på Microsoft om de överdelas.
- **Mycket konfidentiellt:** Affärs data som kan orsaka omfattande skada på Microsoft om de överdelas.

## <a name="tagging-data-classification-in-azure"></a>Tagga data klassificering i Azure

Varje moln leverantör bör erbjuda en mekanism för att registrera metadata om en till gång. När det gäller Azure är resurs Taggar den föreslagna metoden för lagring av metadata och dessa taggar kan användas för att tillämpa data klassificerings information till distribuerade resurser. Även om tagga moln till gångar enligt klassificering inte är en ersättning för en formell data klassificerings process, är det ett värdefullt verktyg för att hantera resurser och tillämpa principer.

Mer information om resurs taggning i Azure finns i artikeln om [att använda taggar för att ordna dina Azure-resurser](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

## <a name="next-steps"></a>Nästa steg

Använd data klassificeringar under en av de åtgärds bara styrnings guiderna.

> [!div class="nextstepaction"]
> [Välj en guide för åtgärds bara styrning](../guides/index.md)