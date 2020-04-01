---
title: Kluster- och programsäkerhet
description: Lär dig mer om Kubernetes i moln implementerings ramverket för kluster-och program säkerhet.
author: sabbour
ms.author: asabbour
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: c7d27fb64e03358876eb8384c09e3add5f5c433e
ms.sourcegitcommit: da7ebd67a0ebf29361f093f00e10217b212a2eb2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/01/2020
ms.locfileid: "80527245"
---
<!-- cSpell:ignore asabbour sabbour kured -->

# <a name="cluster-and-application-security"></a>Kluster- och programsäkerhet

Bekanta dig med Kubernetes Security Essentials och granska den säkra konfigurationen för kluster och program säkerhets vägledning.

## <a name="plan-train-and-proof"></a>Plan, träna och korrektur

När du kommer igång hjälper check listan och resurserna nedan dig att planera för kluster åtgärder och säkerhet. Du bör kunna besvara dessa frågor:

> [!div class="checklist"]
>
> - Har du granskat säkerhets-och hot modellen för Kubernetes-kluster?
> - Har klustret Aktiver ATS för rollbaserad åtkomst kontroll?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Checklista  | Resurser |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Bekanta dig med fakta bladet Security Essentials.** De främsta målen med en säker Kubernetes-miljö är att säkerställa att de program som de kör är skyddade, att säkerhets problem kan identifieras och åtgärdas snabbt och att framtida liknande problem kommer att förhindras. | [Den definitiva guiden för att skydda Kubernetes (whitepaper)](https://clouddamcdnprodep.azureedge.net/gdc/gdc8LXmoZ/original)     |
> | **Granska inställningarna för säkerhets härdning för klusternoderna.** Ett säkerhets härdnings värd operativ system minskar arbets ytan för angrepp och distribuerar behållare på ett säkert sätt. | [Säkerhets härdning i AKS virtuella dator värdar](https://docs.microsoft.com/azure/aks/security-hardened-vm-host-image)     |
> | **Konfigurera kluster rollbaserad åtkomst kontroll (RBAC).** Med den här kontrollen kan du tilldela användare eller grupper av användare behörighet att göra saker som att skapa eller ändra resurser, eller Visa loggar från att köra program arbets belastningar. | [Förstå rollbaserad åtkomst kontroll (RBAC) i Kubernetes (video)](https://www.youtube.com/watch?v=G3R24JSlGjY&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=12) <br/> [Integrera Azure AD med Azure Kubernetes-tjänsten](https://docs.microsoft.com/azure/aks/azure-ad-integration) <br/> [Begränsa åtkomsten till kluster konfigurations filen](https://docs.microsoft.com/azure/aks/control-kubeconfig-access)   |

## <a name="deploy-to-production-and-apply-best-practices"></a>Distribuera till produktion och Använd bästa praxis

När du förbereder programmet för produktion bör du implementera en minsta uppsättning bästa metoder. Använd check listan nedan i det här skedet. Du bör kunna besvara dessa frågor:

> [!div class="checklist"]
>
> - Har du konfigurerat nätverks säkerhets regler för inkommande, utgående och Pod kommunikation?
> - Är klustret konfigurerat för att automatiskt tillämpa uppdatering av nods säkerhets uppdateringar?
> - Kör du en lösning för säkerhets genomsökning för ditt kluster och behållar arbets belastningar?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Checklista  | Resurser |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Kontrol lera åtkomsten till kluster med grupp medlemskap.** Konfigurera Kubernetes-rollbaserad åtkomst kontroll (RBAC) för att begränsa åtkomsten till kluster resurser baserat användar identitet eller grupp medlemskap. | [Kontrol lera åtkomsten till kluster med RBAC och Azure AD-grupper](https://docs.microsoft.com/azure/aks/azure-ad-rbac)    |
> | **Skapa en princip för hantering av hemligheter.** Distribuera och hantera känslig information på ett säkert sätt, t. ex. lösen ord och certifikat, med hjälp av hemligheter i Kubernetes. | [Förstå hemligheter för hantering i Kubernetes (video)](https://www.youtube.com/watch?v=KmhM33j5WYk&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=10) |
> | **Skydda nätverks trafik inom Pod med nätverks principer.** Använd principen för minsta behörighet för att kontrol lera flödet av nätverks trafiken mellan poddar i klustret. | [Säker trafik mellan Pod med nätverks principer](https://docs.microsoft.com/azure/aks/use-network-policies) |
> | **Begränsa åtkomsten till API-servern med hjälp av auktoriserade IP-adresser.** Förbättra kluster säkerheten och minimera attack ytan genom att begränsa åtkomsten till API-servern till en begränsad uppsättning IP-adressintervall. | [Säker åtkomst till API-servern](https://docs.microsoft.com/azure/aks/api-server-authorized-ip-ranges) |
> | **Begränsa utgående trafik för klustret.** Lär dig vilka portar och adresser som ska tillåtas om du begränsar utgående trafik för klustret. Du kan använda Azure-brandväggen eller en brand Väggs enhet från tredje part för att skydda utgående trafik och definiera dessa obligatoriska portar och adresser. | [Styra utgående trafik för klusternoder i AKS](https://docs.microsoft.com/azure/aks/limit-egress-traffic) |
> | **Skydda trafik med en brand vägg för webbaserade program (WAF).** Använd Azure Application Gateway som en ingångs kontroll för Kubernetes-kluster.  | [Konfigurera Azure Application Gateway som en ingångs kontroll enhet](https://docs.microsoft.com/azure/application-gateway/ingress-controller-overview)    |
> | **Tillämpa säkerhets-och kernel-uppdateringar på arbetsnoder.** Förstå uppdaterings upplevelsen av AKS-noden. För att skydda dina kluster tillämpas säkerhets uppdateringar automatiskt på Linux-noder i AKS. Dessa uppdateringar omfattar säkerhets korrigeringar för operativ system eller kernel-uppdateringar. Vissa av dessa uppdateringar kräver att en nod startas om för att slutföra processen. | [Använd kured för att automatiskt starta om noder för att tillämpa uppdateringar](https://docs.microsoft.com/azure/aks/node-updates-kured) |
> | **Konfigurera en lösning för att söka efter behållare och kluster.** Skannings behållare flyttas till Azure Container Registry och får djupare insyn i klusternoderna, moln trafiken och säkerhets kontrollerna. | [Azure Container Registry integration med Security Center](https://docs.microsoft.com/azure/security-center/azure-container-registry-integration) <br/> [Integrering med Azure Kubernetes service med Security Center](https://docs.microsoft.com/azure/security-center/azure-kubernetes-service-integration)  |

## <a name="optimize-and-scale"></a>Optimera och skala

Hur kan du optimera ditt arbets flöde och förbereda ditt program och ditt team att skala? Använd check listan för optimering och skalning för att förbereda. Du bör kunna svara:

> [!div class="checklist"]
>
> - Kan du tillämpa styrnings-och kluster principer i stor skala?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Checklista  | Resurser |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Tillämpa kluster styrnings principer.** Tillämpa skalningar i skala och skydda dina kluster på ett centraliserat, konsekvent sätt. | [Styra distributioner med Azure Policy](https://docs.microsoft.com/azure/governance/policy/concepts/rego-for-aks)    |
> | **Rotera kluster certifikat med jämna mellanrum.** Kubernetes använder certifikat för autentisering med många av dess komponenter. Du kanske vill använda en regelbunden rotation av dessa certifikat för säkerhets-eller princip orsaker. | [Rotera certifikat i Azure Kubernetes service (AKS)](https://docs.microsoft.com/azure/aks/certificate-rotation)    |
