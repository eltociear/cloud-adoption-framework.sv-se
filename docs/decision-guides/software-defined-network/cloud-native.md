---
title: 'Program varu definition nätverk: Cloud-Native'
description: Använd ramverket för moln införande för Azure för att lära dig mer om molnbaserade virtuella nätverk, vilket krävs för att distribuera virtuella datorer till molnet.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: ffcec60ce604cd4698daa78065223c52d1136c51
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80431279"
---
# <a name="software-defined-networking-cloud-native"></a>Program varu definition nätverk: Cloud-Native

Ett Cloud-inbyggt virtuellt nätverk krävs när du distribuerar IaaS-resurser, till exempel virtuella datorer till en moln plattform. Åtkomst till virtuella nätverk från externa källor, på samma sätt som på webben, måste uttryckligen tillhandahållas. De här typerna av virtuella nätverk har stöd för att skapa undernät, routningsregler och virtuella brand väggar och Traffic Management-enheter.

Ett moln-internt virtuellt nätverk har inga beroenden i organisationens lokala eller andra icke-moln resurser för att stödja arbets belastningar som hanteras i molnet. Alla nödvändiga resurser etablerades antingen i själva det virtuella nätverket eller med hjälp av hanterade PaaS-erbjudanden.

## <a name="cloud-native-assumptions"></a>Cloud-ursprungliga antaganden

Att distribuera ett Cloud-inbyggt virtuellt nätverk förutsätter följande:

- De arbets belastningar som du distribuerar till det virtuella nätverket är inte beroende av program eller tjänster som bara är tillgängliga i det lokala nätverket. Om de inte tillhandahåller slut punkter som är tillgängliga via det offentliga Internet, kan inte program och tjänster som är internt lokalt lokalt användas av resurser som finns på en moln plattform.
- Din arbets belastnings identitets hantering och åtkomst kontroll beror på moln plattformens identitets tjänster eller IaaS-servrar som finns i moln miljön. Du behöver inte ansluta direkt till de lokala identitets tjänsterna eller andra externa platser.
- Dina identitets tjänster behöver inte stöd för enkel inloggning (SSO) med lokala kataloger.

Moln-interna virtuella nätverk har inga externa beroenden. Detta gör det enkelt att distribuera och konfigurera, och därför är den här arkitekturen ofta det bästa valet för experiment eller andra mindre självständiga eller snabbt itererande distributioner.

Ytterligare problem ditt moln implementerings team bör tänka på när du diskuterar en Cloud-inbyggd virtuell nätverks arkitektur är:

- Befintliga arbets belastningar som är utformade för att köras i ett lokalt Data Center kan kräva omfattande modifieringar för att dra nytta av molnbaserade funktioner, till exempel lagrings-eller Autentiseringstjänsten.
- Molnbaserade nätverk hanteras enbart via moln plattforms hanterings verktyg och kan därför leda till hanterings-och princip avvikelser från dina befintliga IT-standarder när tid går vidare.

## <a name="next-steps"></a>Nästa steg

Mer information om Cloud-inbyggda virtuella nätverk i Azure finns i:

- [Azure Virtual Network: instruktions guider](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm). Nyligen skapade virtuella Azure-nätverk är Cloud-Native som standard. Använd dessa guider för att planera designen och distributionen av dina virtuella nätverk.
- [Prenumerations begränsningar: nätverk](https://docs.microsoft.com/azure/azure-subscription-service-limits?toc=/azure/virtual-network/toc.json#networking-limits). Varje virtuellt nätverk och anslutna resurser finns i en enda prenumeration. De här resurserna är kopplade till prenumerations begränsningar.
