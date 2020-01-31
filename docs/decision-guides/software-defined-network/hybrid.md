---
title: 'Program varu definition nätverk: hybrid nätverk'
description: Diskussion om hur hybrid nätverk gör det möjligt för dina virtuella moln nätverk att ansluta till lokala resurser.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 61ce3447a852ec8aa1caa0737b0f3757f0f26450
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806619"
---
# <a name="software-defined-networking-hybrid-network"></a>Program varu definition nätverk: hybrid nätverk

Nätverks arkitekturen i hybrid molnet gör det möjligt för virtuella nätverk att komma åt dina lokala resurser och tjänster och vice versa, med hjälp av en särskild WAN-anslutning som ExpressRoute eller annan anslutnings metod för att ansluta nätverken direkt.

![Hybridnätverk](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/images/expressroute.png)

Genom att bygga vidare på den molnbaserade virtuella nätverks arkitekturen, isoleras ett hybrid virtuellt nätverk när de skapas första gången. Om du lägger till anslutningen till den lokala miljön beviljar du åtkomst till och från det lokala nätverket, men alla andra inkommande trafik mål resurser i det virtuella nätverket måste vara explicit tillåtna. Du kan skydda anslutningen med hjälp av virtuella brand Väggs enheter och regler för routning för att begränsa åtkomsten, eller så kan du ange exakt vilka tjänster som kan nås mellan de två nätverken med hjälp av molnets inbyggda routningsfunktioner eller distribuera virtuella nätverks installationer (NVA) till hantera trafik.

Även om hybrid nätverks arkitekturen stöder VPN-anslutningar, är dedikerade WAN-anslutningar som ExpressRoute önskade på grund av högre prestanda och ökad säkerhet.

## <a name="hybrid-assumptions"></a>Hybrid antaganden

Att distribuera ett hybrid virtuellt nätverk omfattar följande antaganden:

- Dina IT-säkerhetsteam har en anpassad och molnbaserad nätverks säkerhets princip för att säkerställa att molnbaserade virtuella nätverk kan kommunicera direkt med lokala system.
- Dina molnbaserade arbets belastningar kräver åtkomst till lagring, program och tjänster som finns i dina lokala nätverk eller från tredje part, eller dina användare eller program i din lokala miljö behöver åtkomst till resurser som är baserade på molnet.
- Du måste migrera befintliga program och tjänster som är beroende av lokala resurser, men vill inte använda resurserna i omutvecklingen för att ta bort dessa beroenden.
- Att ansluta dina lokala nätverk till moln resurser via VPN eller dedikerad WAN, förhindras inte av företagets policy, data suveränitets krav eller andra regler för regelefterlevnad.
- Dina arbets belastningar kräver antingen inte flera prenumerationer för att kringgå begränsningar för prenumerations resurser, eller arbets belastningarna omfattar flera prenumerationer, men kräver inte central hantering av anslutningar eller delade tjänster som används av resurser som sprids över flera prenumerationer.

Dina moln implementerings team bör ta hänsyn till följande problem när du tittar på implementering av en hybrid virtuell nätverks arkitektur:

- Att ansluta lokala nätverk med moln nätverk ökar komplexiteten i dina säkerhets krav. Båda nätverken måste skyddas mot externa sårbarheter och obehörig åtkomst från båda sidor i hybrid miljön.
- Skalning av antalet och storleken för arbets belastningar i en hybrid moln miljö kan öka komplexiteten för Routning och trafik hantering.
- Du måste utveckla kompatibla principer för hantering och åtkomst kontroll för att upprätthålla konsekvent styrning i hela organisationen.

## <a name="learn-more"></a>Läs mer

Mer information om hybrid nätverk i Azure finns i:

- [Referens arkitektur för Hybrid nätverk](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/expressroute). Azure Hybrid Virtual Networks använder antingen en ExpressRoute-krets eller Azure VPN för att ansluta ditt virtuella nätverk till din organisations befintliga IT-resurser som inte finns i Azure. I den här artikeln beskrivs alternativen för att skapa ett hybrid nätverk i Azure.
