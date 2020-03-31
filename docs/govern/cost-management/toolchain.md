---
title: Cost Management verktyg i Azure
description: Se hur Azures inbyggda verktyg kan hjälpa mogna principer och processer som stöder Cost Management styrnings disciplin.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a0429ed857bce3b364f057af950657fed885cc74
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434624"
---
# <a name="cost-management-tools-in-azure"></a>Cost Management verktyg i Azure

[Cost Management](./index.md) är en av de [fem disciplinerna i moln styrning](../governance-disciplines.md). Den här disciplinen fokuserar på sätt att upprätta moln utgifts planer, tilldelning av moln budgetar, övervakning och verk ställande av moln budgetar, upptäcka kostsamma avvikelser och justera moln styrnings planen när faktiska utgifter är feljusterade.

Följande är en lista över inbyggda Azure-verktyg som hjälper dig att mogna de principer och processer som har stöd för den här styrnings disciplinen.

| Verktyg | [Azure Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview-cost-mgt)  | [Innehålls paket för Azure EA](https://docs.microsoft.com/power-bi/service-connect-to-azure-enterprise)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) |
|---------|---------|---------|---------|---------|
|Enterprise-avtal krävs.     | Nej         | Nej         | Ja         | Nej         |
|Budget kontroll     | Nej         | Ja         | Nej         | Ja         |
|Övervaka utgifter på en enskild resurs    | Ja         | Ja         | Ja         | Nej         |
|Övervaka utgifter mellan flera resurser    | Nej         | Ja        | Ja         | Nej         |
|Kontroll utgifter på en enskild resurs     | Ja – manuell storlek         | Ja         | Nej         | Ja         |
|Framtvinga utgifter för flera resurser    | Nej         | Ja         | Nej         | Ja         |
|Framtvinga redovisnings-metadata för resurser    | Nej         | Nej         | Nej         | Ja         |
|Övervaka och identifiera trender     | Ja          | Ja        | Ja         | Nej         |
|Identifiera utgifts avvikelser     | Nej         | Ja        | Ja         | Nej        |
|Socialize avvikelser     | Nej        | Ja        | Ja        | Nej        |
