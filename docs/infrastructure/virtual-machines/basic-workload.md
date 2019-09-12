---
title: Distribuera en grundläggande arbetsbelastning
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Beskriver hur du distribuerar en grundläggande arbets belastning till Azure
author: alexbuckgit
ms.author: abuck
ms.date: 12/31/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 5a5e241e550f2fd79fcd7de48a0b041809340b78
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70830481"
---
# <a name="deploy-a-basic-workload-in-azure"></a>Distribuera en grundläggande arbets belastning i Azure

Termen *arbets belastning* definieras vanligt vis som en godtycklig funktions enhet, till exempel ett program eller en tjänst. Det hjälper till att tänka på en arbets belastning i termer av de kod artefakter som distribueras till en server och även andra tjänster som är specifika för ett program. Detta kan vara en användbar definition för ett lokalt program eller en tjänst, men för moln program måste de expanderas.

I molnet är en arbets belastning inte bara omfatta alla artefakter, utan även moln resurser. Ingår moln resurser som en del av definitionen på grund av det koncept som kallas "infrastruktur som kod". När du lärt dig i [Hur fungerar Azure?](../../getting-started/what-is-azure.md)resurser i Azure distribueras av en Orchestrator-tjänst. Den här Orchestrator-tjänsten exponerar funktioner via ett webb-API och du kan anropa webb-API: et med flera verktyg som PowerShell, Azure CLI och Azure Portal. Det innebär att du kan ange Azure-resurser i en maskinläsbar fil som kan lagras tillsammans med de kod artefakter som är associerade med programmet.

På så sätt kan du definiera en arbets belastning i termer av kod artefakter och nödvändiga moln resurser, så att du ytterligare kan isolera arbets belastningar. Du kan isolera arbets belastningar på det sätt som resurserna organiseras, av nätverk sto pol Ogin eller av andra attribut. Målet med arbets belastnings isolering är att koppla en arbets belastnings resurser till ett team, så att teamet kan hantera alla aspekter av dessa resurser på ett oberoende sätt. Detta gör att flera team kan dela resurs hanterings tjänster i Azure samtidigt som du förhindrar oavsiktlig borttagning eller ändring av var och en av resurserna.

Den här isoleringen aktiverar också ett annat koncept, som kallas DevOps. DevOps innehåller program utvecklings praxis som omfattar både program utveckling och IT-åtgärder ovan och lägger till användningen av Automation så så mycket som möjligt. En av principerna för DevOps kallas kontinuerlig integrering och kontinuerlig leverans (CI/CD). Kontinuerlig integrering syftar på automatiserade Bygg processer som körs varje gång en utvecklare genomför en kod ändring. Kontinuerlig leverans avser de automatiserade processer som distribuerar den här koden till olika miljöer, till exempel en utvecklings miljö för testning eller en produktions miljö för slutlig distribution.

## <a name="basic-workload"></a>Grundläggande arbets belastning

En *grundläggande arbets belastning* definieras vanligt vis som ett enda webb program eller ett virtuellt nätverk (VNet) med en virtuell dator (VM).

> [!NOTE]
> Den här guiden omfattar inte program utveckling. Mer information om hur du utvecklar program på Azure finns i [Guide för Azure Application arkitektur](/azure/architecture/guide).

Oavsett om arbets belastningen är ett webb program eller en virtuell dator krävs en *resurs grupp*för var och en av dessa distributioner. En användare med behörighet att skapa en resurs grupp måste göra detta innan du följer stegen nedan.

## <a name="basic-web-application-paas"></a>Basic-webbprogram (PaaS)

För ett grundläggande webb program väljer du en av snabb starterna på fem minuter från [Web Apps-dokumentationen](/azure/app-service?toc=/azure/architecture/cloud-adoption-guide/toc.json) och följer stegen.

> [!NOTE]
> En del snabb starts guider distribuerar en resurs grupp som standard. I det här fallet behöver du inte skapa en resurs grupp uttryckligen. Annars distribuerar du webb programmet till resurs gruppen som du skapade ovan.

När du har distribuerat en enkel arbets belastning kan du lära dig mer om beprövade metoder för att distribuera ett [grundläggande webb program](/azure/architecture/reference-architectures/app-service-web-app/basic-web-app?toc=/azure/architecture/cloud-adoption-guide/toc.json) till Azure.

## <a name="single-windows-or-linux-vm-iaas"></a>Enskild virtuell Windows-eller Linux-dator (IaaS)

Det första steget är att distribuera ett virtuellt nätverk för en enkel arbets belastning som körs på en virtuell dator. Alla IaaS-resurser (Infrastructure as a Service) i Azure, till exempel virtuella datorer, belastningsutjämnare och gateways, kräver ett virtuellt nätverk. Lär dig mer om [virtuella Azure-nätverk](/azure/virtual-network/virtual-networks-overview?toc=/azure/architecture/cloud-adoption-guide/toc.json)och följ sedan stegen för att [distribuera en Virtual Network till Azure med hjälp av portalen](/azure/virtual-network/quick-create-portal?toc=/azure/architecture/cloud-adoption-guide/toc.json). När du anger inställningarna för det virtuella nätverket i Azure Portal måste du ange namnet på resurs gruppen som du skapade ovan.

Nästa steg är att bestämma om du ska distribuera en enskild virtuell Windows-eller Linux-dator. För virtuella Windows-datorer följer du stegen för att [distribuera en virtuell Windows-dator till Azure med portalen](/azure/virtual-machines/windows/quick-create-portal?toc=/azure/architecture/cloud-adoption-guide/toc.json). När du har angett inställningarna för den virtuella datorn i Azure Portal anger du namnet på resurs gruppen som du skapade ovan.

När du har följt stegen och distribuerat den virtuella datorn kan du lära dig mer om [beprövade metoder för att köra en virtuell Windows-dator på Azure](/azure/architecture/reference-architectures/virtual-machines-windows/single-vm?toc=/azure/architecture/cloud-adoption-guide/toc.json). För en virtuell Linux-dator följer du stegen för att [distribuera en virtuell Linux-dator till Azure med portalen](/azure/virtual-machines/linux/quick-create-portal?toc=/azure/architecture/cloud-adoption-guide/toc.json). Du kan också lära dig mer om [beprövade metoder för att köra en virtuell Linux-dator på Azure](/azure/architecture/reference-architectures/virtual-machines-linux/single-vm?toc=/azure/architecture/cloud-adoption-guide/toc.json).

## <a name="next-steps"></a>Nästa steg

Se [vägledning för arkitektoniska beslut](../../decision-guides/index.md) om hur du använder kärn infrastrukturs komponenter i Azure-molnet.
