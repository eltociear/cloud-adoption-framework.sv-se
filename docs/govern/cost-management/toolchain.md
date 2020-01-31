---
title: Cost Management verktyg i Azure
description: Cost Management verktyg i Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: e35530fbf3a858c000cb78c0c076d7d56d5fbd86
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806415"
---
# <a name="cost-management-tools-in-azure"></a>Cost Management verktyg i Azure

[Cost Management](./index.md) är en av de [fem disciplinerna i moln styrning](../governance-disciplines.md). Den här disciplinen fokuserar på sätt att upprätta moln utgifts planer, tilldelning av moln budgetar, övervakning och verk ställande av moln budgetar, upptäcka kostsamma avvikelser och justera moln styrnings planen när faktiska utgifter är feljusterade.

Följande är en lista över inbyggda Azure-verktyg som hjälper dig att mogna de principer och processer som har stöd för den här styrnings disciplinen.

| Verktyg | [Azure-portalen](https://azure.microsoft.com/features/azure-portal)  | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview-cost-mgt)  | [Innehålls paket för Azure EA](https://docs.microsoft.com/power-bi/service-connect-to-azure-enterprise)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) |
|---------|---------|---------|---------|---------|
|Enterprise-avtal krävs.     | Inga         | Inga         | Ja         | Inga         |
|Budget kontroll     | Inga         | Ja         | Inga         | Ja         |
|Övervaka utgifter på en enskild resurs    | Ja         | Ja         | Ja         | Inga         |
|Övervaka utgifter mellan flera resurser    | Inga         | Ja        | Ja         | Inga         |
|Kontroll utgifter på en enskild resurs     | Ja – manuell storlek         | Ja         | Inga         | Ja         |
|Framtvinga utgifter för flera resurser    | Inga         | Ja         | Inga         | Ja         |
|Framtvinga redovisnings-metadata för resurser    | Inga         | Inga         | Inga         | Ja         |
|Övervaka och identifiera trender     | Ja          | Ja        | Ja         | Inga         |
|Identifiera utgifts avvikelser     | Inga         | Ja        | Ja         | Inga        |
|Socialize avvikelser     | Inga        | Ja        | Ja        | Inga        |
