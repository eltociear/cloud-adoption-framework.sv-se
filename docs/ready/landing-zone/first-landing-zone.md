---
title: Azure-landingzon – att tänka på
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig hur en landningszon fungerar som den grundläggande byggstenen i alla typer av miljöer för molnimplementering.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: b451ec6f58a684bd4fb5998f1915dc79761b7a44
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78228449"
---
# <a name="first-landing-zone"></a>Den första landningszonen

Infrastruktur som kod är en naturlig över gång under de flesta moln införande åtgärder. Distribution av dina första landnings zoner i molnet är en gemensam start punkt för att flytta till en kod driven miljö. Den här artikeln hjälper dig att förstå termen _landnings zon_ och bestämma vilken landnings zon som passar bäst för dina befintliga implementerings behov.

## <a name="code-first-approach-to-landing-zones"></a>Kod-första metod till landnings zoner

Följande bild visar ett antal alternativ för landnings zoner. Följande alternativ hjälper dig att välja rätt landnings zon idag. Det hjälper också till att skapa en vision för dina framtida landnings zon behov.

![Alternativ för landnings zon](../../_images/ready/landing-zone-options.png)

A. Börja med kod för att skapa enhetliga, upprepnings bara landnings zoner. Om du är van vid omstrukturering (eller raffinering av koden och infrastrukturen) som du lär dig börjar du med en enkel kodbas, till exempel molnet för att migrera landnings zon. Den här metoden påskyndar implementeringen och skapar praktiska utbildnings möjligheter. Den här typen av inledande landnings zon är dock inte utformad för känsliga data eller verksamhets kritiska arbets belastningar utan ytterligare omfaktorering.

B. I takt med att implementeringen växer och kraven blir tydligare, kommer antagande-och plattforms teamen att göra omstarts zoner utifrån vad de lär sig. Processen för att expandera dina landnings zoner förbereder miljöer för mer komplexa krav på efterlevnad eller arkitektur. [Expandera landnings zonen](../considerations/index.md) innehåller besluts guider och länkar till bästa praxis för att hjälpa till att omväga arbetet. Expandering av landnings zonen kan hjälpa till att uppfylla säkerhets-, drift-och styrnings krav.

C. Vissa moln införande planer styrs av externa krav på efterlevnad. Azure innehåller några exempel på Azure-ritningar för att minska belastningen på att uppfylla dessa krav. Några av exemplen kan läggas till i din första första skiss. Andra exempel är också en speciell implementering som kan fungera som en första landnings zon.

D. När en partner tillhandahåller kontinuerliga hanterade tjänster eller som ingår i implementerings planen, kommer de normalt att tillhandahålla sin egen landnings zon. Genom att använda en partner landnings zon kan du påskynda implementeringen och säkerställa konsekventa drifts hanterings krav. Men du får ytterligare hänsyn till interna styrnings-och säkerhets krav för att säkerställa justering.

E. Antagande team som har ett midterm-mål (inom 24 månader) som **värd för fler än 1 000-tillgångar (appar, infrastruktur eller data till gångar) i molnet**, bör titta på Northstar för moln införande i molnet som en vägledning för plattforms arkitektur och landnings zoner. Northstar är en mer avancerad översikt, inklusive plattforms arkitektur och referens implementeringar i mål tillstånd. Den här översikten omfattar aspekter av parallella metoder som styrning och åtgärder för att bättre förbereda för verksamhets kritiska, säkra, komplexa och efterlevnads regler.

## <a name="choosing-a-first-landing-zone"></a>Välja en första landnings zon

Valet av den första landnings zonen beror på ett antal variabler. Följande rutnät fångar upp några av alternativen för första landnings zoner, tillsammans med variabler som kan driva beslutet.

| Landnings zon                                 | Moln upplevelse  | Skala             | Identifierings tid | Produktions klar | Hybrid             | Känsliga data     | Verksamhets kritisk   | Efterlevnad         |
|----------------------------------------------|-------------------|-------------------|----------------|------------------|--------------------|--------------------|--------------------|--------------------|
| [Migrera CAF](./migrate-landing-zone.md)     | Nytt till molnet      | < 1 000-tillgångar    | 1 till 5 dagar    | Begränsad omfattning – > | Expansion krävs | Expansion krävs | Expansion krävs | Expansion krävs |
| [CAF terraform](./terraform-landing-zone.md) | Olika mallar | Olika mallar | 10 till 20 veckor | Begränsad omfattning – > | Tillgängliga moduler  | Tillgängliga moduler  | Tillgängliga moduler  | Tillgängliga moduler  |

I följande tabell visas samma landnings zoner från ett något annorlunda perspektiv till vägledning för fler tekniska besluts processer.

| Landnings zon                                 | Hubb                          | Spoke    | Moln modell | Teknologi      |
|----------------------------------------------|------------------------------|----------|-------------|-----------------|--|--|--|
| [Migrera CAF](./migrate-landing-zone.md)     | Omuppgift krävs            | Ingår | Endast Azure  | Azure Blueprint |
| [CAF terraform](./terraform-landing-zone.md) | Ingår i NorthStar-modulen | Ingår | Flera moln  | Terraform       |

## <a name="next-steps"></a>Nästa steg

Om du fortfarande är osäker på vilken första landnings zon du väljer rekommenderar vi att du börjar med [CAF migrera landnings zon](./migrate-landing-zone.md).

> [!div class="nextstepaction"]
> [CAF migrera landnings zon skiss](./migrate-landing-zone.md)
