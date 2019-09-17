---
title: Förbättra din första moln styrnings grund
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig hur du stegvis förbättrar din första moln styrnings grund.
author: BrianBlanchard
ms.author: brblanch
ms.date: 01/03/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: d4a0338daa65ea4269077f15acee05cd99a5fb10
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71029687"
---
# <a name="improve-your-initial-cloud-governance-foundation"></a>Förbättra din första moln styrnings grund

Den här artikeln förutsätter att du har upprättat en [första Cloud styrelsers-grund](./initial-foundation.md). När din implementerings plan för molnet har implementerats kommer de konkreta riskerna att bli av de föreslagna metoder genom vilka team vill använda molnet. När det gäller den här typen av risker i versions planering kan du använda följande rutnät för att snabbt identifiera några rekommenderade metoder för att komma före implementerings planen för att förhindra att risker blir riktiga hot.

## <a name="maturity-vectors"></a>Förfallo vektorer

När som helst kan följande rikt linjer tillämpas på den inledande styrnings Stiftelsen för att åtgärda den risk eller de behov som anges i tabellen nedan.

> [!IMPORTANT]
> Resurs organisationen kan påverka hur den här vägledningen för skript används. Det är viktigt att du börjar med de rekommendationer som bäst överensstämmer med den första moln styrnings grunden som du implementerade i föregående steg.

|Risk/behöver | Small-medium Enterprise | Stora företag |
|---|---|---|
|Känsliga data i molnet|[Rikt linjer för skript](./guides/standard/security-baseline-improvement.md)|[Rikt linjer för skript](./guides/complex/security-baseline-improvement.md)|
|Verksamhets kritiska appar i molnet|[Rikt linjer för skript](./guides/standard/resource-consistency-improvement.md)|[Rikt linjer för skript](./guides/complex/resource-consistency-improvement.md)|
|Hantering av moln kostnader|[Rikt linjer för skript](./guides/standard/cost-management-improvement.md)|[Rikt linjer för skript](./guides/complex/cost-management-improvement.md)|
|Flera moln|[Rikt linjer för skript](./guides/standard/multicloud-improvement.md)|[Rikt linjer för skript](./guides/complex/multicloud-improvement.md)|
|Komplex/äldre identitets hantering|         |[Rikt linjer för skript](./guides/complex/identity-baseline-improvement.md)|
|Styrning i flera lager|         |[Rikt linjer för skript](./guides/complex/multiple-layers-of-governance.md)|

## <a name="next-steps"></a>Nästa steg

Utöver tillämpning av rikt linjer för övervakning kan styrnings metoden i moln implementerings ramverket anpassas så att den passar unika affärs villkor. När du har följt rekommendationerna [utvärderar du företags policyn för att förstå ytterligare anpassnings krav](./corporate-policy.md).

> [!div class="nextstepaction"]
> [Utvärdera företags policyn](./corporate-policy.md)
