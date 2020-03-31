---
title: Klusterdesign och klusteråtgärder
description: Lär dig mer om Kubernetes i moln implementerings ramverket för kluster design och-åtgärder.
author: sabbour
ms.author: asabbour
ms.date: 12/16/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 31ea5b2e5906f08de5197906b57cbe32337e80f9
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80426850"
---
<!-- cSpell:ignore asabbour sabbour autoscaler PDBs -->

# <a name="cluster-design-and-operations"></a>Klusterdesign och klusteråtgärder

Tänk igenom klusterkonfigurationen och nätverksdesignen. Framtida korrektur skalbarhet genom att automatisera infrastruktur etableringen. Säkerställ hög tillgänglighet genom att planera för verksamhetskontinuitet och haveriberedskap.

## <a name="plan-train-and-proof"></a>Plan, träna och korrektur

När du kommer igång hjälper check listan och resurserna nedan dig att planera kluster designen. Du bör kunna besvara dessa frågor:

<!-- markdownlint-disable MD033 -->

> [!div class="checklist"]
>
> - Har du identifierat nätverks design kraven för klustret?
> - Har du arbets belastningar med varierande krav? Hur många noder i pooler ska du använda?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Checklista  | Resurser |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Identifiera nätverks design överväganden.** Förstå nätverks design överväganden för kluster, jämför nätverks modeller och välj den Kubernetes nätverk-plugin som passar dina behov.    | [Kubernetes och Azure Container Network Interface (CNI)](https://docs.microsoft.com/azure/aks/concepts-network#azure-virtual-networks) <br/> [Använda Kubernetes-nätverk med dina egna IP-adressintervall i Azure Kubernetes service (AKS)](https://docs.microsoft.com/azure/aks/configure-kubenet) <br/> [Konfigurera Azure CNI Networking i Azure Kubernetes service (AKS)](https://docs.microsoft.com/azure/aks/configure-azure-cni) <br/> [Säker nätverks design för ett AKS-kluster](https://github.com/Azure/sg-aks-workshop/blob/master/cluster-design/NetworkDesign.md)|
> | **Skapa flera Node-pooler.** Om du vill stödja program som har olika beräknings-eller lagrings krav kan du konfigurera klustret med flera noder. Du kan till exempel använda ytterligare resurspooler för att tillhandahålla GPU: er för beräknings intensiva program eller åtkomst till SSD-lagring med höga prestanda.   | [Skapa och hantera flera Node-pooler för ett kluster i Azure Kubernetes-tjänsten](https://docs.microsoft.com/azure/aks/use-multiple-node-pools) |
> | **Bestäm tillgänglighets krav.** För att tillhandahålla en högre tillgänglighets nivå för dina program kan kluster distribueras mellan tillgänglighets zoner. Dessa zoner är fysiskt separata data Center inom en specifik region. När kluster komponenterna distribueras över flera zoner kan klustret tolerera ett fel i någon av dessa zoner. Dina program och hanterings åtgärder fortsätter att vara tillgängliga även om ett helt data Center har problem.   | [Skapa ett Azure Kubernetes service-kluster (AKS) som använder tillgänglighets zoner](https://docs.microsoft.com/azure/aks/availability-zones) |

## <a name="go-to-production-and-apply-best-practices"></a>Gå till produktion och Använd bästa praxis

När du förbereder programmet för produktion bör du implementera en minsta uppsättning bästa metoder. Använd check listan nedan i det här skedet. Du bör kunna besvara dessa frågor:

> [!div class="checklist"]
>
> - Kan du distribuera kluster infrastrukturen på ett säkert sätt?
> - Har du tillämpat resurs kvoter?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Checklista  | Resurser                                                                                                     |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Automatisera kluster etablering.** Med infrastruktur som kod kan du automatisera infrastruktur etableringen för att ge mer återhämtning vid katastrofer och få bättre flexibilitet för att snabbt distribuera om infrastrukturen vid behov.     | [Skapa ett Kubernetes-kluster med Azure Kubernetes-tjänsten med hjälp av terraform](https://docs.microsoft.com/azure/terraform/terraform-create-k8s-cluster-with-tf-and-aks)|
> | **Planera för tillgänglighet med hjälp av Pod-störande budgetar.** Om du vill behålla tillgängligheten för program definierar du Pod avbrotts budgetar (PDBs) för att säkerställa att ett minsta antal poddar är tillgängliga i klustret under maskin varu fel eller kluster uppgraderingar. | [Planera för tillgänglighet med hjälp av Pod-avbrott i budgetar](https://docs.microsoft.com/azure/aks/operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets)  |
> | **Tvinga resurs kvoter på namn områden.** Planera och tillämpa resurs kvoter på namn områdes nivå. Kvoter kan anges för beräknings resurser, lagrings resurser och antal objekt.| [Framtvinga resurs kvoter](https://docs.microsoft.com/azure/aks/operator-best-practices-scheduler#enforce-resource-quotas)  |

## <a name="optimize-and-scale"></a>Optimera och skala

Hur kan du optimera ditt arbets flöde och förbereda ditt program och ditt team att skala? Utnyttja check listan för optimering och skalning för att förbereda. Du bör kunna besvara dessa frågor:

> [!div class="checklist"]
>
> - Har du en plan för verksamhets kontinuitet och haveri beredskap?
> - Kan klustret skalas för att uppfylla program kraven?
> - Kan du övervaka ditt kluster och dina program hälsa och få aviseringar?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Checklista  | Resurser |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Skala automatiskt ett kluster så att det uppfyller program kraven.** För att hålla dig uppdaterad om programmets krav kan du behöva justera antalet noder som kör arbets belastningarna automatiskt med hjälp av klustrets automatiska skalning. | [Konfigurera Kubernetes-kluster autoskalning](https://docs.microsoft.com/azure/aks/cluster-autoscaler)    |
> | **Planera för verksamhets kontinuitet och haveri beredskap.** Planera för distribution i flera regioner, skapa en plan för lagringsmigrering och aktivera geo-replikering för behållar avbildningar. | [Metod tips för distributioner i flera regioner](https://docs.microsoft.com/azure/aks/operator-best-practices-multi-region)  <br/> [Azure Container Registry geo-replikering](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication)  |
> | **Konfigurera övervakning och fel sökning i stor skala.** Konfigurera aviseringar och övervakning för program i Kubernetes. Lär dig mer om standard konfigurationen, hur du integrerar mer avancerade mått och hur du lägger till din egen anpassade övervakning och avisering för att köra ditt program på ett tillförlitligt sätt. | [Komma igång med övervakning och avisering för Kubernetes (video)](https://www.youtube.com/watch?v=W7aN_z-cyUw&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=16) <br/> [Konfigurera aviseringar med hjälp av Azure Monitor för behållare](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview) <br/> [Granska diagnostikloggar för huvud komponenter](https://docs.microsoft.com/azure/aks/view-master-logs) <br/> [Diagnostik för Azure Kubernetes service (AKS)](https://docs.microsoft.com/azure/aks/concepts-diagnostics)    |
