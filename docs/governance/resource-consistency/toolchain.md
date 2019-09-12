---
title: Resurs konsekvens verktyg i Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Resurs konsekvens verktyg i Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6a0a2303473cffd9bb5175c67e12a84d6baa2814
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70824098"
---
# <a name="resource-consistency-tools-in-azure"></a>Resurs konsekvens verktyg i Azure

[Resurs konsekvens](index.md) är en av de [fem disciplinerna i moln styrning](../governance-disciplines.md). Det här området handlar om metoder för att upprätta principer som rör driftshantering av en miljö, ett program eller en arbetsbelastning. I de fem disciplinerna i moln styrning innebär resurs konsekvens disciplin övervakning av program, arbets belastning och till gångens prestanda. Det omfattar också de uppgifter som krävs för att uppfylla skalnings kraven, åtgärda SLA-överträdelser för prestanda och proaktivt undvika SLA-överträdelser i prestanda genom automatisk reparation.

Följande är en lista över Azure-verktyg som kan hjälpa mogna för de principer och processer som har stöd för den här styrnings disciplinen.

| Verktyg | [Azure Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview)  | [Azure Blueprint](/azure/governance/blueprints/overview) | [Azure Automation](/azure/automation/automation-intro) | [Azure AD](/azure/active-directory/fundamentals/active-directory-whatis) | [Azure Backup](/azure/backup/backup-introduction-to-azure-backup) | [Azure Site Recovery](/azure/site-recovery/site-recovery-overview) |
|---------|---------|---------|---------|---------|---------|---------|---------|
| Distribuera resurser                             | Ja | Ja | Ja | Ja | Nej  | Nej | Nej |
| Hantera resurser                             | Ja | Ja | Ja | Ja | Nej  | Nej | Nej |
| Distribuera resurser med hjälp av mallar             | Nej  | Ja | Nej  | Ja | Nej  | Nej | Nej |
| Distribution av dirigerad miljö          | Nej  | Nej  | Ja | Nej  | Nej  | Nej | Nej |
| Definiera resurs grupper                       | Ja | Ja | Ja | Nej  | Nej  | Nej | Nej |
| Hantera arbets belastning och konto ägare           | Ja | Ja | Ja | Nej  | Nej  | Nej | Nej |
| Hantera villkorlig åtkomst till resurser       | Ja | Ja | Ja | Nej  | Nej  | Nej | Nej |
| Konfigurera RBAC-användare                         | Ja | Nej  | Nej  | Nej  | Ja | Nej | Nej |
| Tilldela roller och behörigheter till resurser | Ja | Ja | Ja | Nej  | Ja | Nej | Nej |
| Definiera beroenden mellan resurser        | Nej  | Ja | Ja | Nej  | Nej  | Nej | Nej |
| Använd åtkomst kontroll                         | Ja | Ja | Ja | Nej  | Ja | Nej | Nej |
| Utvärdera tillgänglighet och skalbarhet          | Nej  | Nej  | Nej  | Ja | Nej  | Nej | Nej |
| Använd taggar för resurser                      | Ja | Ja | Ja | Nej  | Nej  | Nej | Nej |
| Tilldela Azure Policy regler                    | Ja | Ja | Ja | Nej  | Nej  | Nej | Nej |
| Använd automatiserad reparation                  | Nej  | Nej  | Nej  | Ja | Nej  | Nej | Nej |
| Hantera fakturering                               | Ja | Nej  | Nej  | Nej  | Nej  | Nej | Nej |
| Planera resurser för haveri beredskap         | Ja | Ja | Ja | Nej  | Nej  | Ja | Ja |
|Återställa data under ett avbrott eller SLA-överträdelse     | Nej | Nej  | Nej  | Nej  | Nej  | Ja | Ja |
|Återställa program och data under ett avbrott eller SLA-överträdelse     | Nej | Nej  | Nej  | Nej  | Nej  | Ja | Ja |

Tillsammans med dessa resurs konsekvens verktyg och funktioner måste du övervaka dina distribuerade resurser för prestanda-och hälso problem. [Azure Monitor](/azure/azure-monitor/overview) är standard lösningen för övervakning och rapportering i Azure. Azure Monitor tillhandahåller funktioner för att övervaka dina moln resurser. Den här listan visar vilken funktion som behandlar vanliga övervaknings krav.

| Verktyg | [Azure Portal](https://azure.microsoft.com/features/azure-portal) | [Application Insights](/azure/application-insights/app-insights-overview) | [Log Analytics](/azure/azure-monitor/log-query/log-query-overview) | [Azure Monitor REST API](/rest/api/monitor) |
|----------------------------------------------------|--------------|----------------------|---------------|------------------------|
| Logga data för telemetri för virtuell dator                 | Nej           | Nej                   | Ja           | Nej                     |
| Logga data för telemetri för virtuella nätverk              | Nej           | Nej                   | Ja           | Nej                     |
| Logga PaaS Services telemetridata                   | Nej           | Nej                   | Ja           | Nej                     |
| Information om log Application-telemetri                     | Nej           | Ja                  | Nej            | Nej                     |
| Konfigurera rapporter och aviseringar                       | Ja          | Nej                   | Nej            | Ja                    |
| Schemalägga vanliga rapporter eller anpassade analyser        | Nej           | Nej                   | Nej            | Nej                     |
| Visualisera och analysera logg-och prestanda data     | Ja          | Nej                   | Nej            | Nej                     |
| Integrera med en lokal eller tredje parts övervaknings lösning     | Nej           | Nej                   | Nej            | Ja                    |

När du planerar distributionen måste du fundera över var loggnings data lagras och hur du integrerar molnbaserade [rapporterings-och övervaknings tjänster](../../decision-guides/log-and-report/index.md) med dina befintliga processer och verktyg.

> [!NOTE]
> Organisationer använder även DevOps-verktyg från tredje part för att övervaka arbets belastningar och resurser. Mer information finns i [DevOps-verktyg integreringar](https://azure.microsoft.com/products/devops-tool-integrations).

## <a name="next-steps"></a>Nästa steg

Lär dig hur du skapar, tilldelar och hanterar [princip definitioner](/azure/governance/policy) i Azure.
