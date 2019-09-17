---
title: Verktyg för distributions acceleration i Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Verktyg för distributions acceleration i Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: b9cf2edd1edafb4390b89465dba4a8e8dcfc1b0e
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027642"
---
# <a name="deployment-acceleration-tools-in-azure"></a>Verktyg för distributions acceleration i Azure

[Distributions acceleration](./index.md) är en av de [fem disciplinerna i moln styrning](../governance-disciplines.md). Det här området handlar om metoder för att upprätta principer för styrning av tillgångskonfiguration eller -distribution. Inom fem ämnes områden i moln styrning innebär distributions accelerations disciplin distribution och konfigurations justering. Detta kan ske via manuella aktiviteter eller helt automatiserade DevOps-aktiviteter. I båda fallen skulle de berörda principerna förbli i stort sett samma.

Cloud förmyndare komponenter, Cloud Guardians och Cloud Architects med en intresse av styrning är var och en som sannolikt ägnar mycket tid i distributions accelerations disciplinen, som codifies principer och krav i flera moln införande åtgärder. Verktygen i den här verktygskedjan är viktiga för moln styrnings teamet och bör vara en hög prioritet för teamets utbildnings väg.

Följande är en lista över Azure-verktyg som kan hjälpa mogna för de principer och processer som har stöd för den här styrnings disciplinen.

|  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure-Hanteringsgrupper](https://docs.microsoft.com/azure/governance/management-groups) | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) | [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints/overview) | [Azure Resource Graph](https://docs.microsoft.com/azure/governance/resource-graph/overview) | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management) |
|---------|---------|---------|---------|---------|---------|---------|
|Implementera företags principer     |Ja |Nej  |Nej  |Nej | Nej |Nej |
|Tillämpa principer för prenumerationer     |Obligatorisk |Ja  |Nej  |Nej | Nej |Nej |
|Distribuera definierade resurser     |Nej |Nej  |Ja  |Nej | Nej |Nej |
|Skapa helt kompatibla miljöer      |Obligatorisk |Obligatorisk  |Obligatorisk  |Ja | Nej |Nej |
|Gransknings principer      |Ja |Nej  |Nej  |Nej | Nej |Nej |
|Fråga Azure-resurser      |Nej |Nej  |Nej  |Nej |Ja |Nej |
|Rapport om resursernas kostnader      |Nej |Nej  |Nej  |Nej |Nej |Ja |

Följande är ytterligare verktyg som kan krävas för att uppnå vissa mål för distributions acceleration. Dessa verktyg används ofta utanför styrnings gruppen, men betraktas fortfarande som en aspekt av distributions accelerationen som en disciplin.

|  | [Azure Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure DevOps](https://docs.microsoft.com/azure/devops/index) | [Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) | [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) |
|---------|---------|---------|---------|---------|---------|---------|
|Manuell distribution (enstaka till gång)     | Ja | Ja  | Nej  | Inte effektivt | Nej | Ja |
|Manuell distribution (fullständig miljö)     | Inte effektivt | Ja | Nej  | Inte effektivt | Nej | Ja |
|Automatiserad distribution (fullständig miljö)     | Nej  | Ja  | Nej  | Ja  | Nej | Ja |
|Uppdatera konfigurationen av en enskild till gång     | Ja | Ja | Inte effektivt | Inte effektivt | Nej | Ja – vid replikering |
|Uppdatera konfigurationen av en fullständig miljö     | Inte effektivt | Ja | Ja | Ja  | Nej | Ja – vid replikering |
|Hantera konfigurations avvikelser     | Inte effektivt | Inte effektivt | Ja  | Ja  | Nej | Ja – vid replikering |
|Skapa en automatiserad pipeline för att distribuera kod och konfigurera till gångar (DevOps)     | Nej | Nej | Nej | Ja | Nej | Nej |

Förutom de inbyggda Azure-verktygen som anges ovan är det vanligt att kunderna använder verktyg från tredje part för att under lätta distributions acceleration och DevOps distributioner.
