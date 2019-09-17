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
ms.openlocfilehash: 230e36d1ca59c208109eedbbdf7466f6373f4b00
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028852"
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
|Övervaka och identifiera trender     | Ja – begränsad         | Ja        | Ja         | Nej         |
|Identifiera utgifts avvikelser     | Nej         | Ja        | Ja         | Nej        |
|Socialize avvikelser     | Nej        | Ja        | Ja        | Nej        |
