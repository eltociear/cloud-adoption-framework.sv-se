---
title: Designbeslut för Azure-beredskap för processor
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Designbeslut för Azure-beredskap för processor
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: bd31f07a24a17a50953eff54856118e9b22d054e
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70819392"
---
# <a name="compute-design-decisions"></a>Beslut om processordesign

Det är viktigt att avgöra vilka processorkrav du har för att arbetsbelastningen när du planerar din molnimplementering. Produkter och tjänster för Azure-processorer har stöd för en mängd olika scenarier och funktioner för processorer. Konfigurationen av din landningszonmiljö i förhållande till dina processor beror på din arbetsbelastningsstyrning, samt tekniska och företagsrelaterade krav.

## <a name="identify-compute-services-requirements"></a>Identifiera krav för processortjänster

Som del av utvärderingen och förberedelsen av landningszonen måste du identifiera de processorresurser som din landningszon måste ha stöd för. Processen förutsätter att du bedömer var och ett av de program och tjänster som utgör arbetsbelastningarna för att fastställa dina processor- och värdbehov. När du har identifierat och dokumenterat dessa krav kan du skapa principer för din landnings zon för att kontrollera tillåtna resurstyper utifrån dina arbetsbelastningsbehov.

För varje program eller tjänst som du distribuerar till din landningszonmiljö använder du följande beslutsträd som utgångspunkt för att hjälpa dig att avgöra vilka processortjänster du behöver:

![Beslutsträd för Azure-processortjänster](../../_images/ready/compute-decision-tree.png)

> [!NOTE]
> Läs mer om hur du kan utvärdera processoralternativ för var och ett av dina program eller [tjänster i Azures](/azure/architecture/guide/technology-choices/compute-overview) programarkitekturguide.

### <a name="key-questions"></a>Viktiga frågor

Besvara följande frågor om dina arbetsbelastningar för att skapa ett beslutsunderlag baserat på beslutsträdet för Azure-processortjänster:

- **Skapar du helt nya program och tjänster eller migrerar du från befintliga lokala arbetsbelastningar?** Genom att utveckla nya program som en del av din molnimplementering kan du dra full nytta av modern molnbaserad värdteknik redan från utvecklingsfasen.
- **Om du migrerar befintliga arbetsbelastningar, kan de använda modern molnteknik?** Migrering av lokala arbetsbelastningar kräver analys: Kan du enkelt optimera befintliga program och tjänster för att dra nytta av modern molnteknik eller kommer en *lift and shift*-metod fungera bättre för dina arbetsbelastningar?
- **Kan dina program eller tjänster använda behållare?** Om dina program är bra kandidater för behållarvärdtjänster kan du utnyttja resurseffektiviteten, skalbarheten och samordningskapaciteten hos [Azure Container Services](https://azure.microsoft.com/product-categories/containers). Både [Azure Disk Storage](/azure/virtual-machines/windows/managed-disks-overview) och[Azure Files](/azure/storage/files/storage-files-introduction) kan användas för beständig lagring för program i behållare.
- **Är dina program webbaserade eller API-baserade och använder de PHP, ASP.NET, Node. js eller liknande teknik?** Webbappar kan distribueras till hanterade [Azure App Service](/azure/app-service/overview)-instanser så att du inte behöver underhålla virtuella datorer som servrar.
- **Behöver du fullständig kontroll över operativsystemet och värdmiljön för din arbetsbelastning?** Om du behöver kontrollera värd miljön, inklusive operativsystemet, diskar, lokal programvara och andra konfigurationer kan du använda [virtuella Azure-datorer](https://azure.microsoft.com/services/virtual-machines) som värd för dina program och tjänster. Utöver valet av storlek på de virtuella datorerna och prestandanivåer påverkar dina beslut om virtuellt diskutrymme prestanda och serviceavtal för dina IaaS-baserade (infrastruktur som en tjänst) arbetsbelastningar. Mer information finns i [dokumentationen om Azure-disklagring](/azure/virtual-machines/windows/managed-disks-overview).
- **Kommer arbetsbelastningen att omfatta HPC-funktioner (databehandling med hög prestanda)?** Med [Azure Batch](/azure/batch/batch-technical-overview) får du jobbschemaläggning och autoskalning av databearbetningsresurser som en plattformstjänst, vilket gör det enkelt att köra storskaliga program och HPC-program parallellt i molnet.
- **Kommer dina program att använda en mikrotjänstarkitektur?** Program som använder en mikrotjänstbaserad arkitektur kan använda flera optimerade processortekniker. Fristående och händelsedrivna arbetsbelastningar kan använda [Azure Functions](/azure/azure-functions/functions-overview) för att bygga skalbara serverlösa program som inte behöver någon infrastruktur. För program som kräver mer kontroll över miljön där mikrotjänsterna körs kan du använda behållartjänster som [Azure Container-instances](/azure/container-instances/container-instances-overview), [Azure Kubernetes Service](/azure/aks/intro-kubernetes) och [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).

> [!NOTE]
> De flesta Azure-processortjänster används tillsammans Azure Storage. Se riktlinjerna för [beslut om lagringsutrymme](./storage-guidance.md) för relaterade lagringsbeslut.

## <a name="common-compute-scenarios"></a>Vanliga processorscenarier

I följande tabell visas några vanliga användningsscenarier och rekommenderade processortjänster för att hantera dessa:

| **Scenario** | **Processortjänst** |
| --- | --- |
| Jag behöver etablera virtuella Linux- och Windows-datorer på några sekunder med mina valda konfigurationer. | [Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines) |
| Jag behöver hög tillgänglighet genom automatisk skalning för att skapa tusentals virtuella datorer på några minuter. | [Skaluppsättningar för virtuella datorer](https://azure.microsoft.com/services/virtual-machine-scale-sets) |
| Jag vill förenkla distributionen, hanteringen och driften av Kubernetes. | [Azure Kubernetes Service (AKS)](https://azure.microsoft.com/services/kubernetes-service) |
| Jag behöver påskynda utvecklingen av appar med hjälp av en händelsedriven serverlös arkitektur. | [Azure Functions](https://azure.microsoft.com/services/functions) |
| Jag behöver utveckla mikrotjänster och dirigera behållare i Windows och Linux. | [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric) |
| Jag vill snabbt skapa molnappar för webben och mobilt med en helt hanterad plattform. | [Azure App Service](https://azure.microsoft.com/services/app-service) |
| Jag vill köra appar i behållare och köra behållarna enkelt med ett enda kommando. | [Azure Container Instances](https://azure.microsoft.com/services/container-instances) |
| Jag behöver jobbschemaläggning och processorhantering i molnskala med möjlighet att skala till tiotals, hundratals eller tusentals virtuella datorer. | [Azure Batch](https://azure.microsoft.com/services/batch) |
| Jag behöver skapa högtillgängliga, skalbara molnprogram och API:er som kan hjälpa mig att fokusera på appar istället för maskinvara. | [Azure Cloud Services](https://azure.microsoft.com/services/cloud-services) |

## <a name="regional-availability"></a>Regional tillgänglighet

Med Azure kan du leverera tjänster i den skala du behöver för att nå dina kunder och partners  _var de än befinner sig_. En viktig faktor vid planeringen av molndistributionen är att avgöra vilken Azure-region som ska vara värd för dina arbetsbelastningsresurser.

Vissa processoralternativ, till exempel Azure App Service, är allmänt tillgängliga i de flesta Azure-regioner. Vissa processortjänster stöds dock bara i utvalda regioner. Vissa typer av virtuella datorer och deras tillhörande lagringstyper har begränsad regional tillgänglighet. Innan du bestämmer vilka regioner du ska distribuera dina beräkningsresurser till rekommenderar vi att du läser [regionsidan](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=azure-vmware-cloudsimple,cloud-services,batch,container-instances,app-service,service-fabric,functions,kubernetes-service,virtual-machine-scale-sets,virtual-machines)  för att kontrollera den senaste statusen för regional tillgänglighet.

Mer information om den globala Azure-infrastrukturen finns på  [sidan med Azure-regioner](https://azure.microsoft.com/global-infrastructure/regions). Du kan också visa [produkter som är tillgängliga](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=all) per region för detaljerad information om de övergripande tjänster som är tillgängliga i varje Azure-region.

## <a name="data-residency-and-compliance-requirements"></a>Krav för dataplacering och efterlevnad

Juridiska krav och avtalskrav som är relaterade till datalagring gäller ofta för dina arbetsbelastningar. Dessa krav kan variera beroende på organisationens plats, domsagan där filer och data lagras och bearbetas och din aktuella affärssektor. Dataskyldighetsöverväganden omfattar dataklassificering, dataplats och tillämpliga ansvar för dataskydd enligt modellen för gemensamt ansvar. Många processorlösningar är beroende av länkade lagringsresurser. Detta krav kan också påverka dina processorbeslut. Hjälp med att förstå dessa krav finns i vitboken  [Uppnå datahemvist och säkerhet som följer standard med hjälp av Azure](https://azure.microsoft.com/resources/achieving-compliant-data-residency-and-security-with-azure).

En del av ert efterlevnadsarbete kan omfatta att kontrollera var era processorresurser är fysiskt placerade. De geografiska Azure-regionerna är ordnade i grupper som kallas områden. Ett geografiskt  [Azure-område](https://azure.microsoft.com/global-infrastructure/geographies) garanterar att krav på dataplacering, landsbaserad placering, efterlevnad och elasticitet stöds inom geografiska och politiska gränser. Om dina arbetsbelastningar är föremål för datasuveränitet eller andra krav på efterlevnad måste du distribuera dina lagringsresurser i en region som ligger i ett kompatibelt Azure-område.

## <a name="establish-controls-for-compute-services"></a>Upprätta kontroller för processortjänster

När du förbereder din landningszonmiljö kan du upprätta kontroller som begränsar vilka resurser som varje användare kan distribuera. Kontrollerna kan hjälpa dig att hantera kostnader och begränsa säkerhetsriskerna, samtidigt som utvecklare och IT-team kan distribuera och konfigurera de resurser som behövs för att stödja dina arbetsbelastningar.

När du har identifierat och dokumenterat kraven för landningszonen kan du använda [Azure Policy](/azure/governance/policy/overview) för att kontrollera vilka beräkningsresurser som användarna kan skapa. Kontroller kan antingen [tillåta eller neka att vissa typer av processorresurser skapas](/azure/governance/policy/samples/allowed-resource-types). Du kan till exempel begränsa användarna till att endast kunna skapa Azure App Service eller Azure Functions. Du kan också använda principer för att kontrollera de alternativ som tillåts när en resurs skapas, t.ex. [genom att begränsa vilka SKU:er för virtuella datorer som kan tillhandahållas](https://docs.microsoft.com/azure/governance/policy/samples/allowed-skus-storage) eller [bara vissa avbildningar av virtuella datorer](https://docs.microsoft.com/azure/governance/policy/samples/allowed-custom-images).

Principer kan begränsas till resurser, resursgrupper, prenumerationer och hanteringsgrupper. Du kan inkludera principerna i definitionerna för [Azure Blueprint](/azure/governance/blueprints/overview) och tillämpa dem flera gånger i din molnegendom.

