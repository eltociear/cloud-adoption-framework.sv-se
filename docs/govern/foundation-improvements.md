---
title: Förbättra din första moln styrnings grund
description: Använd ramverket för moln införande för Azure för att lära dig hur du stegvis förbättrar din första moln styrnings grund.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/13/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 050d9cdfd2069a4d7da2e411233f6a60f270eb10
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77706616"
---
# <a name="improve-your-initial-cloud-governance-foundation"></a>Förbättra din första moln styrnings grund

Den här artikeln förutsätter att du har upprättat en [första Cloud styrelsers-grund](./initial-foundation.md). När din implementerings plan för molnet har implementerats kommer de konkreta riskerna att bli av de föreslagna metoder genom vilka team vill använda molnet. När det gäller den här typen av risker i versions planering kan du använda följande rutnät för att snabbt identifiera några av de bästa metoderna för att komma före implementerings planen för att förhindra att risker blir riktiga hot.

## <a name="maturity-vectors"></a>Förfallo vektorer

När som helst kan följande metod tips användas för den inledande styrnings grunden för att åtgärda den risk eller de behov som anges i tabellen nedan.

> [!IMPORTANT]
> Resurs organisationen kan påverka hur dessa metod tips används. Det är viktigt att du börjar med de rekommendationer som bäst överensstämmer med den första moln styrnings grunden som du implementerade i föregående steg.

|Risk/behöver | Standardföretag | Komplext företag |
|---|---|---|
|Känsliga data i molnet|[Disciplin förbättringar](./guides/standard/security-baseline-improvement.md)|[Disciplin förbättringar](./guides/complex/security-baseline-improvement.md)|
|Verksamhets kritiska appar i molnet|[Disciplin förbättringar](./guides/standard/resource-consistency-improvement.md)|[Disciplin förbättringar](./guides/complex/resource-consistency-improvement.md)|
|Hantering av moln kostnader|[Disciplin förbättringar](./guides/standard/cost-management-improvement.md)|[Disciplin förbättringar](./guides/complex/cost-management-improvement.md)|
|Flera moln|[Disciplin förbättringar](./guides/standard/multicloud-improvement.md)|[Disciplin förbättringar](./guides/complex/multicloud-improvement.md)|
|Komplex/äldre identitets hantering|Saknas|[Disciplin förbättringar](./guides/complex/identity-baseline-improvement.md)|
|Styrning i flera lager|Saknas|[Disciplin förbättringar](./guides/complex/multiple-layers-of-governance.md)|

## <a name="next-steps"></a>Nästa steg

Förutom att det går att få bästa praxis kan styrnings metoden i moln implementerings ramverket anpassas så att den passar unika affärs villkor. När du har följt rekommendationerna [utvärderar du företags policyn för att förstå ytterligare anpassnings krav](./corporate-policy.md).

> [!div class="nextstepaction"]
> [Utvärdera företags policyn](./corporate-policy.md)
