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
ms.openlocfilehash: e019e99cd6af2047e040ae02c1899ce21c222545
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/11/2019
ms.locfileid: "70906092"
---
# <a name="improve-your-initial-cloud-governance-foundation"></a>Förbättra din första moln styrnings grund

Den här artikeln förutsätter att du har upprättat en [första Cloud styrelsers-grund](./getting-started.md). När din implementerings plan för molnet har implementerats kommer de konkreta riskerna att bli av de föreslagna metoder genom vilka team vill använda molnet. När det gäller den här typen av risker i versions planering kan du använda följande rutnät för att snabbt identifiera några rekommenderade metoder för att komma före implementerings planen för att förhindra att risker blir riktiga hot.

## <a name="maturity-vectors"></a>Förfallo vektorer

När som helst kan följande rikt linjer tillämpas på den inledande styrnings Stiftelsen för att åtgärda den risk eller de behov som anges i tabellen nedan.

> [!IMPORTANT]
> Resurs organisationen kan påverka hur den här vägledningen för skript används. Det är viktigt att du börjar med de rekommendationer som bäst överensstämmer med den första moln styrnings grunden som du implementerade i föregående steg.

|Risk/behöver | Small-medium Enterprise | Stora företag |
|---|---|---|
|Känsliga data i molnet|[Rikt linjer för skript](./journeys/standard-enterprise/security-baseline-evolution.md)|[Rikt linjer för skript](./journeys/complex-enterprise/security-baseline-evolution.md)|
|Verksamhets kritiska appar i molnet|[Rikt linjer för skript](./journeys/standard-enterprise/resource-consistency-evolution.md)|[Rikt linjer för skript](./journeys/complex-enterprise/resource-consistency-evolution.md)|
|Hantering av moln kostnader|[Rikt linjer för skript](./journeys/standard-enterprise/cost-management-evolution.md)|[Rikt linjer för skript](./journeys/complex-enterprise/cost-management-evolution.md)|
|Flera moln|[Rikt linjer för skript](./journeys/standard-enterprise/multicloud-evolution.md)|[Rikt linjer för skript](./journeys/complex-enterprise/multicloud-evolution.md)|
|Komplex/äldre identitets hantering|         |[Rikt linjer för skript](./journeys/complex-enterprise/identity-baseline-evolution.md)|
|Styrning i flera lager|         |[Rikt linjer för skript](./journeys/complex-enterprise/multiple-layers-of-governance.md)|

## <a name="next-steps"></a>Nästa steg

Utöver tillämpning av rikt linjer för övervakning kan styrnings metoden i moln implementerings ramverket anpassas så att den passar unika affärs villkor. När du har följt rekommendationerna [utvärderar du företags policyn för att förstå ytterligare anpassnings krav](./corporate-policy.md).

> [!div class="nextstepaction"]
> [Utvärdera företags policyn](./corporate-policy.md)
