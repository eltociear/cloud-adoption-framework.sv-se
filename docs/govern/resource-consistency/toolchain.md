---
title: Resurs konsekvens verktyg i Azure
description: Resurs konsekvens verktyg i Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a2f553285f9d44085cc816c2db34f76fcb02235d
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76805191"
---
# <a name="resource-consistency-tools-in-azure"></a>Resurs konsekvens verktyg i Azure

[Resurs konsekvens](./index.md) är en av de [fem disciplinerna i moln styrning](../governance-disciplines.md). Det här området handlar om metoder för att upprätta principer som rör driftshantering av en miljö, ett program eller en arbetsbelastning. I de fem disciplinerna i moln styrning innebär resurs konsekvens disciplin övervakning av program, arbets belastning och till gångens prestanda. Det omfattar också de uppgifter som krävs för att uppfylla skalnings kraven, åtgärda SLA-överträdelser för prestanda och proaktivt undvika SLA-överträdelser i prestanda genom automatisk reparation.

Följande är en lista över Azure-verktyg som kan hjälpa mogna för de principer och processer som har stöd för den här styrnings disciplinen.

| Verktyg | [Azure-portalen](https://azure.microsoft.com/features/azure-portal)  | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints/overview) | [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) | [Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis) | [Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) | [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) |
|---------|---------|---------|---------|---------|---------|---------|---------|
| Distribuera resurser                             | Ja | Ja | Ja | Ja | Inga  | Inga | Inga |
| Hantera resurser                             | Ja | Ja | Ja | Ja | Inga  | Inga | Inga |
| Distribuera resurser med hjälp av mallar             | Inga  | Ja | Inga  | Ja | Inga  | Inga | Inga |
| Distribution av dirigerad miljö          | Inga  | Inga  | Ja | Inga  | Inga  | Inga | Inga |
| Definiera resurs grupper                       | Ja | Ja | Ja | Inga  | Inga  | Inga | Inga |
| Hantera arbets belastning och konto ägare           | Ja | Ja | Ja | Inga  | Inga  | Inga | Inga |
| Hantera villkorlig åtkomst till resurser       | Ja | Ja | Ja | Inga  | Inga  | Inga | Inga |
| Konfigurera RBAC-användare                         | Ja | Inga  | Inga  | Inga  | Ja | Inga | Inga |
| Tilldela roller och behörigheter till resurser | Ja | Ja | Ja | Inga  | Ja | Inga | Inga |
| Definiera beroenden mellan resurser        | Inga  | Ja | Ja | Inga  | Inga  | Inga | Inga |
| Använd åtkomst kontroll                         | Ja | Ja | Ja | Inga  | Ja | Inga | Inga |
| Utvärdera tillgänglighet och skalbarhet          | Inga  | Inga  | Inga  | Ja | Inga  | Inga | Inga |
| Använd taggar för resurser                      | Ja | Ja | Ja | Inga  | Inga  | Inga | Inga |
| Tilldela Azure Policy regler                    | Ja | Ja | Ja | Inga  | Inga  | Inga | Inga |
| Använd automatiserad reparation                  | Inga  | Inga  | Inga  | Ja | Inga  | Inga | Inga |
| Hantera fakturering                               | Ja | Inga  | Inga  | Inga  | Inga  | Inga | Inga |
| Planera resurser för haveri beredskap         | Ja | Ja | Ja | Inga  | Inga  | Ja | Ja |
|Återställa data under ett avbrott eller SLA-överträdelse     | Inga | Inga  | Inga  | Inga  | Inga  | Ja | Ja |
|Återställa program och data under ett avbrott eller SLA-överträdelse     | Inga | Inga  | Inga  | Inga  | Inga  | Ja | Ja |

Tillsammans med dessa resurs konsekvens verktyg och funktioner måste du övervaka dina distribuerade resurser för prestanda-och hälso problem. [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) är standard lösningen för övervakning och rapportering i Azure. Azure Monitor tillhandahåller funktioner för att övervaka dina moln resurser. Den här listan visar vilken funktion som behandlar vanliga övervaknings krav.

| Verktyg | [Azure-portalen](https://azure.microsoft.com/features/azure-portal) | [Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) | [Log Analytics](https://docs.microsoft.com/azure/azure-monitor/log-query/log-query-overview) | [Azure Monitor REST API](https://docs.microsoft.com/rest/api/monitor) |
|----------------------------------------------------|--------------|----------------------|---------------|------------------------|
| Logga data för telemetri för virtuell dator                 | Inga           | Inga                   | Ja           | Inga                     |
| Logga data för telemetri för virtuella nätverk              | Inga           | Inga                   | Ja           | Inga                     |
| Logga PaaS Services telemetridata                   | Inga           | Inga                   | Ja           | Inga                     |
| Information om log Application-telemetri                     | Inga           | Ja                  | Inga            | Inga                     |
| Konfigurera rapporter och aviseringar                       | Ja          | Inga                   | Inga            | Ja                    |
| Schemalägga vanliga rapporter eller anpassade analyser        | Inga           | Inga                   | Inga            | Inga                     |
| Visualisera och analysera logg-och prestanda data     | Ja          | Inga                   | Inga            | Inga                     |
| Integrera med en lokal eller tredje parts övervaknings lösning     | Inga           | Inga                   | Inga            | Ja                    |

När du planerar distributionen måste du fundera över var loggnings data lagras och hur du integrerar molnbaserade [rapporterings-och övervaknings tjänster](../../decision-guides/logging-and-reporting/index.md) med dina befintliga processer och verktyg.

> [!NOTE]
> Organisationer använder även DevOps-verktyg från tredje part för att övervaka arbets belastningar och resurser. Mer information finns i [DevOps-verktyg integreringar](https://azure.microsoft.com/products/devops-tool-integrations).

## <a name="next-steps"></a>Nästa steg

Lär dig hur du skapar, tilldelar och hanterar [princip definitioner](https://docs.microsoft.com/azure/governance/policy) i Azure.
