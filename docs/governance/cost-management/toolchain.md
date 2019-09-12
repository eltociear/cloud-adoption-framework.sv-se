---
title: Cost Management verktyg i Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Cost Management verktyg i Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 32c05e04c224f88008ded6e9fe2c69bb6095d346
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70828102"
---
# <a name="cost-management-tools-in-azure"></a>Cost Management verktyg i Azure

[Cost Management](./index.md) är en av de [fem disciplinerna i moln styrning](../governance-disciplines.md). Den här disciplinen fokuserar på sätt att upprätta moln utgifts planer, tilldelning av moln budgetar, övervakning och verk ställande av moln budgetar, upptäcka kostsamma avvikelser och justera moln styrnings planen när faktiska utgifter är feljusterade.

Följande är en lista över inbyggda Azure-verktyg som hjälper dig att mogna de principer och processer som har stöd för den här styrnings disciplinen.

| Verktyg | [Azure Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Cost Management](/azure/cost-management/overview-cost-mgt)  | [Innehålls paket för Azure EA](/power-bi/service-connect-to-azure-enterprise)  | [Azure Policy](/azure/governance/policy/overview) |
|---------|---------|---------|---------|---------|
|Enterprise-avtal krävs.     | Nej         | Nej         | Ja         | Nej         |
|Budget kontroll     | Nej         | Ja         | Nej         | Ja         |
|Övervaka utgifter på en enskild resurs    | Ja         | Ja         | Ja         | Nej         |
|Övervaka utgifter mellan flera resurser    | Nej         | Ja        | Ja         | Nej         |
|Kontroll utgifter på en enskild resurs     | Ja – manuell storlek         | Ja         | Nej         | Ja         |
|Framtvinga utgifter för flera resurser    | Nej         | Ja         | Nej         | Ja         |
|Framtvinga redovisnings-metadata för resurser    | Nej         | Nej         | Nej         | Ja         |
|Övervaka och identifiera trender     | Ja – begränsad         | Ja        | Ja         | Nej         |
|Identifiera utgifts avvikelser     | Nej         | Ja        | Ja         | Nej        |
|Socialize avvikelser     | Nej        | Ja        | Ja        | Nej        |
