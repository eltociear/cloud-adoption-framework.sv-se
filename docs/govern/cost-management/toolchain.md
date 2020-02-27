---
title: Cost Management verktyg i Azure
description: Se hur Azures inbyggda verktyg kan hjälpa mogna principer och processer som stöder Cost Management styrnings disciplin.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 70014352d4b7f64f5c73a0fda96ef453f1a77176
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77708792"
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
