---
title: Vad är dataklassificering?
description: Med data klassificering kan du fastställa och tilldela ett värde till din organisations data och det är en gemensam utgångs punkt för styrning.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 1f476aaccfc88eab4a2bea1db17e7b1d33f31ee9
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76805089"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-data-classification"></a>Vad är dataklassificering?

Med data klassificering kan du fastställa och tilldela ett värde till din organisations data och det är en gemensam utgångs punkt för styrning. Data klassificerings processen kategoriserar data efter känslighet och affärs påverkan för att identifiera risker. När data klassificeras kan du hantera dem på ett sätt som skyddar känsliga eller viktiga data från stöld eller förlust.

## <a name="understand-data-risks-then-manage-them"></a>Förstå data risker och hantera dem

Innan en risk kan hanteras måste den förstås. I händelse av ansvars skyldighet för data intrång börjar det förstås med data klassificering. Data klassificering är en process för att associera en metadata-egenskap till varje till gång i en digital fastighet som identifierar den typ av data som är kopplade till till gången.

En till gång som identifieras som en potentiell kandidat för migrering eller distribution till molnet bör ha dokumenterade metadata för att registrera data klassificering, affärs kritiskhet och fakturerings ansvar. Dessa tre klassificerings punkter kan vara ett långt sätt att förstå och minimera risker.

## <a name="classifications-microsoft-uses"></a>Klassificeringar som används av Microsoft

Följande är en lista över klassificeringar som används av Microsoft. Beroende på din bransch eller befintliga säkerhets krav kan data klassificerings standarder redan finnas i din organisation. Om det inte finns någon standard kanske du vill använda den här exempel klassificeringen för att bättre förstå din egen digitala egendom och risk profil.

- **Icke-företag:** Data från din personliga liv som inte tillhör Microsoft.
- **Offentlig:** Affärs data som är allmänt tillgängliga och godkända för offentlig konsumtion.
- **Allmänt:** Affärs data som inte är avsedda för en offentlig publik.
- **Konfidentiellt:** Affärs data som kan orsaka skada på Microsoft om de överdelas.
- **Mycket konfidentiellt:** Affärs data som kan orsaka omfattande skada på Microsoft om de överdelas.

## <a name="tagging-data-classification-in-azure"></a>Tagga data klassificering i Azure

Resurs taggar är en lämplig metod för lagring av metadata och du kan använda taggarna för att använda data klassificerings information till distribuerade resurser. Även om tagga moln till gångar enligt klassificering inte är en ersättning för en formell data klassificerings process, är det ett värdefullt verktyg för att hantera resurser och tillämpa principer. [Azure information Protection](https://docs.microsoft.com/azure/information-protection/what-is-information-protection) är en utmärkt lösning som hjälper dig att klassificera _data_ , oavsett var de finns (lokalt, i Azure eller någon annan stans). Överväg detta som en del av en övergripande klassificerings strategi.

Mer information om resurs taggning i Azure finns i [använda taggar för att ordna dina Azure-resurser](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

## <a name="next-steps"></a>Nästa steg

Använd data klassificeringar under en av de åtgärds bara styrnings guiderna.

> [!div class="nextstepaction"]
> [Välj en guide för åtgärds bara styrning](../guides/index.md)
