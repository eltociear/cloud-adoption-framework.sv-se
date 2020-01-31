---
title: Verktyg för distributions acceleration i Azure
description: Verktyg för distributions acceleration i Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6617fe95f885836241e4b0f16bc17652f36c5a7d
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806330"
---
# <a name="deployment-acceleration-tools-in-azure"></a>Verktyg för distributions acceleration i Azure

[Distributions acceleration](./index.md) är en av de [fem disciplinerna i moln styrning](../governance-disciplines.md). Det här området handlar om metoder för att upprätta principer för styrning av tillgångskonfiguration eller -distribution. Inom fem ämnes områden i moln styrning innebär distributions accelerations disciplin distribution och konfigurations justering. Detta kan ske via manuella aktiviteter eller helt automatiserade DevOps-aktiviteter. I båda fallen skulle de berörda principerna förbli i stort sett samma.

Cloud förmyndare komponenter, Cloud Guardians och Cloud Architects med en intresse av styrning är var och en som sannolikt ägnar mycket tid i distributions accelerations disciplinen, som codifies principer och krav i flera moln införande åtgärder. Verktygen i den här verktygskedjan är viktiga för moln styrnings teamet och bör vara en hög prioritet för teamets utbildnings väg.

Följande är en lista över Azure-verktyg som kan hjälpa mogna för de principer och processer som har stöd för den här styrnings disciplinen.

|  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure-Hanteringsgrupper](https://docs.microsoft.com/azure/governance/management-groups) | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) | [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints/overview) | [Azure Resource Graph](https://docs.microsoft.com/azure/governance/resource-graph/overview) | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management) |
|---------|---------|---------|---------|---------|---------|---------|
|Implementera företags principer     |Ja |Inga  |Inga  |Inga | Inga |Inga |
|Tillämpa principer för prenumerationer     |Krävs |Ja  |Inga  |Inga | Inga |Inga |
|Distribuera definierade resurser     |Inga |Inga  |Ja  |Inga | Inga |Inga |
|Skapa helt kompatibla miljöer      |Krävs |Krävs  |Krävs  |Ja | Inga |Inga |
|Gransknings principer      |Ja |Inga  |Inga  |Inga | Inga |Inga |
|Fråga Azure-resurser      |Inga |Inga  |Inga  |Inga |Ja |Inga |
|Rapport om resursernas kostnader      |Inga |Inga  |Inga  |Inga |Inga |Ja |

Följande är ytterligare verktyg som kan krävas för att uppnå vissa mål för distributions acceleration. Dessa verktyg används ofta utanför styrnings gruppen, men betraktas fortfarande som en aspekt av distributions accelerationen som en disciplin.

|  | [Azure-portalen](https://azure.microsoft.com/features/azure-portal)  | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure DevOps](https://docs.microsoft.com/azure/devops/index) | [Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) | [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) |
|---------|---------|---------|---------|---------|---------|---------|
|Manuell distribution (enstaka till gång)     | Ja | Ja  | Inga  | Inte effektivt | Inga | Ja |
|Manuell distribution (fullständig miljö)     | Inte effektivt | Ja | Inga  | Inte effektivt | Inga | Ja |
|Automatiserad distribution (fullständig miljö)     | Inga  | Ja  | Inga  | Ja  | Inga | Ja |
|Uppdatera konfigurationen av en enskild till gång     | Ja | Ja | Inte effektivt | Inte effektivt | Inga | Ja – vid replikering |
|Uppdatera konfigurationen av en fullständig miljö     | Inte effektivt | Ja | Ja | Ja  | Inga | Ja – vid replikering |
|Hantera konfigurations avvikelser     | Inte effektivt | Inte effektivt | Ja  | Ja  | Inga | Ja – vid replikering |
|Skapa en automatiserad pipeline för att distribuera kod och konfigurera till gångar (DevOps)     | Inga | Inga | Inga | Ja | Inga | Inga |

Förutom de inbyggda Azure-verktygen som anges ovan är det vanligt att kunderna använder verktyg från tredje part för att under lätta distributions acceleration och DevOps distributioner.
