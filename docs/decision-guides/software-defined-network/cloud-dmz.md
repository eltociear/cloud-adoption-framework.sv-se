---
title: 'Program varu definition nätverk: Cloud DMZ'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Den här nätverks arkitekturen ger begränsad åtkomst mellan dina lokala och molnbaserade nätverk.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 6b96fbae9c3e31fc4c133ce6a19589324a86dd83
ms.sourcegitcommit: 50788e12bb744dd44da14184b3e884f9bddab828
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/18/2019
ms.locfileid: "74160041"
---
# <a name="software-defined-networking-cloud-dmz"></a>Program varu definition nätverk: Cloud DMZ

Cloud DMZ Network Architecture ger begränsad åtkomst mellan dina lokala och molnbaserade nätverk, med hjälp av ett virtuellt privat nätverk (VPN) för att ansluta nätverken. Även om en DMZ-modell används ofta när du vill skydda extern åtkomst till ett nätverk, är den moln DMZ-arkitektur som beskrivs här särskilt avsedd att säkra åtkomsten till det lokala nätverket från molnbaserade resurser och vice versa.

![Skydda hybridnätverksarkitektur](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/images/dmz-private.png)

Den här arkitekturen är utformad för att ge stöd för scenarier där din organisation vill börja integrera molnbaserade arbets belastningar med lokala arbets belastningar, men kanske inte har fullständigt förmognade moln säkerhets principer eller skaffat en säker, säker WAN-anslutning mellan de två miljöerna. Därför bör moln nätverk behandlas som en demilitariserad-zon för att säkerställa att lokala tjänster är säkra.

DMZ distribuerar virtuella nätverks installationer (NVA) för att implementera säkerhetsfunktioner, till exempel brand väggar och paket granskning. Trafik som passerar mellan lokala och molnbaserade program eller tjänster måste passera genom DMZ där den kan granskas. VPN-anslutningar och regler som avgör vilken trafik som tillåts genom DMZ-nätverket styrs strikt av IT-säkerhetsteamen.

## <a name="cloud-dmz-assumptions"></a>DMZ-antaganden för molnet

Att distribuera en moln DMZ omfattar följande antaganden:

- Dina säkerhets team har inte helt justerade lokala och molnbaserade säkerhets krav och principer.
- Dina molnbaserade arbets belastningar kräver åtkomst till begränsade del mängder av tjänster som finns i lokala nätverk eller från tredje part, eller användare eller program i din lokala miljö behöver begränsad åtkomst till molnbaserade resurser.
- Att implementera en VPN-anslutning mellan dina lokala nätverk och moln leverantören förhindras inte av företagets policy, myndighets krav eller problem med teknisk kompatibilitet.
- Dina arbets belastningar kräver antingen inte flera prenumerationer för att kringgå begränsningar för prenumerations resurser, eller flera prenumerationer, men kräver inte central hantering av anslutningar eller delade tjänster som används av resurser som sprids över flera prenumerationer.

Dina moln implementerings team bör tänka på följande när man tittar på implementering av en DMZ för virtuella nätverk i molnet:

- Att ansluta lokala nätverk med moln nätverk ökar komplexiteten i dina säkerhets krav. Även om anslutningar mellan moln nätverk och den lokala miljön är säkra måste du ändå se till att moln resurserna är säkra. Alla offentliga IP-adresser som skapats för att komma åt molnbaserade arbets belastningar måste vara korrekt skyddade med hjälp av en [offentlig DMZ](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) eller [Azure-brandvägg](https://docs.microsoft.com/azure/firewall).
- Cloud DMZ-arkitekturen används ofta som en stege-sten när anslutningen är ytterligare skyddad och säkerhets principer som är justerade mellan lokala och molnbaserade nätverk, vilket ger ett bredare införande av en hybrid nätverks arkitektur med fullständig skalning. Det kan dock även gälla isolerade distributioner med vissa krav på säkerhet, identitet och anslutning som DMZ-metoden för molnet uppfyller.

## <a name="learn-more"></a>Läs mer

Mer information om hur du implementerar en moln DMZ i Azure finns i:

- [Implementera en DMZ mellan Azure och ditt lokala data Center](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid). Den här artikeln beskriver hur du implementerar en säker hybrid nätverks arkitektur i Azure.
