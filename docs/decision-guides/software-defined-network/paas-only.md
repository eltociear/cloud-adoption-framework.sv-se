---
title: 'Program varu definitions nätverk: Endast PaaS'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Diskussion av PaaS-modellen för program varu definierade nätverk i molnet.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 9613e4be1173687e5f40409c34799c26480b0702
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70829454"
---
# <a name="software-defined-networking-paas-only"></a>Program varu definitions nätverk: Endast PaaS

När du implementerar en PaaS-resurs (Platform as a Service) skapar distributions processen automatiskt ett förmodat underliggande nätverk med ett begränsat antal kontroller över nätverket, inklusive belastnings utjämning, Port blockering och anslutningar till andra PaaS Terminal.

I Azure kan flera PaaS-resurs typer [distribueras till](/azure/virtual-network/virtual-network-for-azure-services) eller [anslutas till](/azure/virtual-network/virtual-network-service-endpoints-overview) ett virtuellt nätverk, så att dessa resurser kan integreras med din befintliga virtuella nätverks infrastruktur. Andra tjänster, till exempel [App Service miljöer](/azure/app-service/environment/intro), [Azure Kubernetes Services](/azure/aks/intro-kubernetes)och [Service Fabric](/azure/service-fabric/service-fabric-overview) måste distribueras i det virtuella nätverket. I många fall är det dock tillräckligt med en PaaS nätverks arkitektur, som endast förlitar sig på de inbyggda standard nätverksfunktioner som tillhandahålls av PaaS-resurser, så att det räcker att uppfylla arbets Belastningens anslutnings-och trafik hanterings krav.

Om du överväger en PaaS nätverks arkitektur måste du kontrol lera att de nödvändiga antagandena överensstämmer med dina krav.

## <a name="paas-only-assumptions"></a>PaaS-antaganden

Att distribuera en nätverks arkitektur för PaaS förutsätter följande:

- Det program som distribueras är ett fristående program eller är beroende av andra PaaS-resurser som inte kräver ett virtuellt nätverk.
- IT-avdelningen kan uppdatera sina verktyg, utbildning och processer för att stödja hantering, konfiguration och distribution av fristående PaaS-program.
- PaaS-programmet är inte en del av en bredare moln migrering som omfattar IaaS-resurser.

Dessa antaganden är minimala kvalificerare som är justerade för att distribuera ett PaaS nätverk. Den här metoden kan justeras med kraven för en enda program distribution, och varje moln antagande team bör ta hänsyn till dessa långsiktiga frågor:

- Kommer den här distributionen att utökas i omfattning eller skala för att kräva åtkomst till andra icke-PaaS resurser?
- Planeras andra PaaS-distributioner än den aktuella lösningen?
- Har organisationen planer för andra framtida moln migreringar?

Svaren på dessa frågor skulle inte hindra ett team från att välja ett alternativ för PaaS utan bör övervägas innan du fattar ett slutligt beslut.
