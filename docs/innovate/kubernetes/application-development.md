---
title: Programutveckling och programdistribution
description: Lär dig mer om att använda Kubernetes i moln implementerings ramverket för program utveckling och arkitektur.
author: sabbour
ms.author: asabbour
ms.topic: guide
ms.date: 03/20/2020
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 6ad36a6dfbce83b23bfcee382ff44daeb9db5f7f
ms.sourcegitcommit: 1a4b140f09bdaa141037c54a4a3b5577cda269db
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/30/2020
ms.locfileid: "80392772"
---
<!-- cSpell:ignore asabbour sabbour autoscaler Istio Linkerd -->

# <a name="application-development-and-deployment"></a>Programutveckling och programdistribution

Undersök mönster och metoder för programutveckling, konfigurera DevOps-pipelines och implementera metodtips för SRE (Site Reliability Engineering).

## <a name="plan-train-and-proof"></a>Plan, träna och korrektur

När du kommer igång hjälper check listan och resurserna nedan dig att planera din program utveckling och distribution. Du bör kunna besvara dessa frågor:

> [!div class="checklist"]
>
> - Har du för berett utvecklings miljön och installations arbets flödet?
> - Hur kommer du att strukturera projektmappen för att stödja Kubernetes program utveckling?
> - Har du identifierat tillstånd, konfiguration och lagrings krav för ditt program?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Checklista | Resurser |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Förbered utvecklings miljön.** Konfigurera din miljö med de verktyg du behöver för att skapa behållare och konfigurera ditt utvecklings arbets flöde. | [Arbeta med Docker i Visual Studio Code](https://code.visualstudio.com/docs/azure/docker) <br/>[Arbeta&nbsp;med&nbsp;Kubernetes&nbsp;i&nbsp;Visual&nbsp;Studio Code](https://code.visualstudio.com/docs/azure/kubernetes) <br/> [Introduktion till Azure dev Spaces](https://docs.microsoft.com/azure/dev-spaces/about) |
> | **Använd ditt program.** Bekanta dig med Kubernetes utvecklings erfarenhet, inklusive program ramverk, Inner-loop-arbetsflöden, program hanterings ramverk, CI/CD-pipelines, logg agg regering, övervakning och program mått. | [Använd dina appar med Docker och Kubernetes (e-bok)](https://azure.microsoft.com/resources/containerize-your-apps-with-docker-and-kubernetes) <br/> [Kubernetes utvecklings upplevelse från slut punkt till slut punkt på Azure (webb seminarium)](https://info.microsoft.com/AU-AzureApp-WBNR-FY20-11Nov-12-ContainerizeYourApplicationswithKubernetesonAzure-SRDEM10557_LP02OnDemandRegistration-ForminBody.html) |
> | **Granska vanliga Kubernetes-scenarier.** Kubernetes betraktas ofta som en plattform för att leverera mikrotjänster, men det blir en mycket bredare plattform. Titta på den här videon om du vill veta mer om vanliga Kubernetes-scenarier som batch Analytics och Workflow.    | [Vanliga&nbsp;scenarier&nbsp;&nbsp;använda&nbsp;Kubernetes&nbsp;(video)](https://www.youtube.com/watch?v=zd8vYhrFXp4&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=7) |
> | **Förbered ditt program för Kubernetes.** Förbered din program fil systemets layout för Kubernetes och organisera för varje vecka eller dagliga versioner. Lär dig hur Kubernetes-distributions processen aktiverar pålitliga, noll stillestånds uppgraderingar. | [Projekt design och layout för lyckade Kubernetes-appar (webb seminarium)](https://info.microsoft.com/ww-OnDemandRegistration-successful-kubernetes-applications-webinar.html) <br/> [Så här fungerar Kubernetes-distributioner (video)](https://www.youtube.com/watch?v=mNK14yXIZF4&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=3) </br> [Gå igenom en AKS-workshop](https://aka.ms/learn/aksworkshop) |
> | **Hantera program lagring.** Förstå prestanda behov och åtkomst metoder för poddar så att du kan ange lämpliga lagrings alternativ. Du bör också planera för sätt att säkerhetskopiera och testa återställningsprocessen för direktansluten lagring. | [Grunderna för tillstånds känsliga program i Kubernetes (video)](https://www.youtube.com/watch?v=GieXzb91I40&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=9) <br/> [Tillstånd och data i Docker-program](https://docs.microsoft.com/dotnet/architecture/microservices/architect-microservice-container-applications/docker-application-state-data) <br/>[Lagrings alternativ i Azure Kubernetes-tjänsten](https://docs.microsoft.com/azure/aks/operator-best-practices-storage) |
> | **Hantera program hemligheter.** Lagra inte autentiseringsuppgifter i program koden. Ett nyckel valv ska användas för att lagra och hämta nycklar och autentiseringsuppgifter.  | [Så här fungerar Kubernetes och konfigurations hantering (video)](https://www.youtube.com/watch?v=vRcQOZLnKUk&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=11) <br/> [Förstå hemligheter för hantering i Kubernetes (video)](https://www.youtube.com/watch?v=KmhM33j5WYk&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=10) <br/>[Använda Azure Key Vault med Kubernetes](https://github.com/Azure/kubernetes-keyvault-flexvol) <br/>[Använda Pod-identitet för att autentisera och få åtkomst till Azure-resurser](https://github.com/Azure/aad-pod-identity) |

## <a name="deploy-to-production-and-apply-best-practices"></a>Distribuera till produktion och Använd bästa praxis

När du förbereder programmet för produktion bör du implementera en minsta uppsättning bästa metoder. Använd check listan nedan i det här skedet. Du bör kunna besvara dessa frågor:

> [!div class="checklist"]
>
> - Kan du övervaka alla aspekter av ditt program?
> - Har du definierat resurs kraven för ditt program? Hur vill du ha skalnings krav?
> - Kan du distribuera nya versioner av programmet utan att påverka produktions systemen?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Checklista  | Resurser                                                                                                     |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Konfigurera beredskaps hälso kontroller.** Kubernetes använder beredskaps-och Live-kontroller för att veta när programmet är redo att ta emot trafik och när det behöver startas om. Utan att definiera sådana kontroller kommer Kubernetes inte att kunna avgöra om programmet är igång och körs.   | [Beredskaps-och beredskaps kontroller](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes) |
> | **Konfigurera loggning, program övervakning och aviseringar.** Övervaka dina behållare är viktigt, särskilt när du kör ett produktionskluster i skala med flera program.  Den rekommenderade loggnings metoden för program i behållare skrivs till strömmarna standardutdata (STDOUT) och standard fel (STDERR).   | [Logga in Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging) <br/> [Komma igång med övervakning och avisering för Kubernetes (video)](https://www.youtube.com/watch?v=W7aN_z-cyUw&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=16) <br/> [Azure Monitor för behållare](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview) <br/> [Aktivera och granska Kubernetes huvudnodloggar i Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/view-master-logs)  <br/> [Visa Kubernetes-loggar, händelser och Pod mått i real tid](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-livedata-overview) |
> | **Definiera resurs krav för programmet.** Ett primärt sätt att hantera beräknings resurserna i ett Kubernetes-kluster är att använda Pod-begäranden och-gränser. Dessa förfrågningar och gränser anger Kubernetes Scheduler vilka beräknings resurser som en POD ska tilldelas.     | [Definiera&nbsp;Pod&nbsp;resurs&nbsp;begär&nbsp;och&nbsp;gränser](https://docs.microsoft.com/azure/aks/developer-best-practices-resource-management) |
> | **Konfigurera program skalnings krav.** Kubernetes stöder horisontell Pod autoskalning för att justera antalet poddar i en distribution beroende på CPU-användning eller andra valda mått. Om du vill använda autoskalning måste alla behållare i din poddar ha processor förfrågningar och gränser definierade.    | [Konfigurera autoskalning för horisontell Pod](https://docs.microsoft.com/azure/aks/tutorial-kubernetes-scale#autoscale-pods) |
> | **Distribuera program med en automatiserad pipeline och DevOps.**  Den fullständiga automatiseringen av alla steg mellan kod incheckning och produktions distribution gör att grupper kan fokusera på att skapa kod och ta bort kostnader och potentiella mänskliga fel i manuella rutinmässiga-steg. Det går snabbare och enklare att distribuera ny kod, vilket hjälper teamen att bli mer flexibla, mer produktiva och mer säkra för att köra kod.    | [Utveckla dina DevOps-metoder](https://docs.microsoft.com/learn/paths/evolve-your-devops-practices) <br/> [Konfigurera en pipeline för Kubernetes-build (video)](https://www.youtube.com/watch?v=5irsAdKoEBU&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=6) <br/> [Distributions Center för Azure Kubernetes-tjänsten](https://docs.microsoft.com/azure/aks/deployment-center-launcher) <br/> [GitHub-åtgärder för att distribuera till Azure Kubernetes-tjänsten](https://docs.microsoft.com/azure/aks/kubernetes-action) <br/>  [CI/CD till Azure Kubernetes service med Jenkins](https://docs.microsoft.com/azure/aks/jenkins-continuous-deployment) |

## <a name="optimize-and-scale"></a>Optimera och skala

Hur kan du optimera ditt arbets flöde och förbereda ditt program och ditt team att skala? Använd check listan för optimering och skalning för att förbereda. Du bör kunna besvara dessa frågor:

> [!div class="checklist"]
>
> - Är program som är överstycknings bara abstrakta från ditt program?
> - Kan du underhålla system-och program tillförlitlighet, samtidigt som du kan fortsätta att använda nya funktioner och versioner?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Checklista  | Resurser                                                                                                     |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Distribuera en API-Gateway.** En API-gateway fungerar som en frontend-dörr för mikrotjänster, frigör klienter från mikrotjänster, lägger till ytterligare ett lager med säkerhet och minskar komplexiteten för mikrotjänster genom att ta bort belastningen på att hantera överstycknings frågor.     | [Använda Azure API Management med mikrotjänster som distribueras i Azure Kubernetes-tjänsten](https://docs.microsoft.com/azure/api-management/api-management-kubernetes) |
> | **Distribuera ett tjänst nät.** Ett tjänst nät ger funktioner som trafik hantering, återhämtning, policy, säkerhet, stark identitet och rätt till dina arbets belastningar. Programmet är frikopplat från dessa operativa funktioner och service nätet flyttar dem från program lagret och nedåt till infrastruktur skiktet.     | [Hur&nbsp;service&nbsp;nät&nbsp;arbets&nbsp;i&nbsp;Kubernetes&nbsp;(video)](https://www.youtube.com/watch?v=izVWk7rYqWI&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=15&t=0s) <br/> [Lär dig om service nät](https://docs.microsoft.com/azure/aks/servicemesh-about) <br/> [Använda Istio med Azure Kubernetes service](https://docs.microsoft.com/azure/aks/servicemesh-istio-about) <br/> [Använda Linkerd med Azure Kubernetes service](https://docs.microsoft.com/azure/aks/servicemesh-linkerd-about) <br/> [Använd konsulär med Azure Kubernetes-tjänsten](https://docs.microsoft.com/azure/aks/servicemesh-consul-about) |
> | **Implementera SRE-metoder (site Tillförlitlighets teknik).**  Site Tillförlitlighets teknik (SRE) är en beprövad metod för att upprätthålla viktiga system-och program tillförlitlighet samtidigt som du går igenom den hastighet som marknads platsen kräver.   | [Introduktion till site Tillförlitlighets teknik (SRE)](https://docs.microsoft.com/learn/modules/intro-to-site-reliability-engineering) <br/> [DevOps på Microsoft: SRE för spel strömning](https://azure.microsoft.com/resources/devops-at-microsoft-game-streaming-sre) |
