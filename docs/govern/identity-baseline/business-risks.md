---
title: Identitets bas affärs risker
description: Förstå och se exempel på typisk kund införande av en identitets bas linje disciplin i en moln styrnings strategi. 
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: fa8bd53e2d920f8d69fe6484d427d9c9400ad174
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80429895"
---
# <a name="identity-baseline-motivations-and-business-risks"></a>Motiveringar och affärs risker för identitets bas

I den här artikeln beskrivs orsakerna till att kunderna vanligt vis antar en identitets bas disciplin i en strategi för moln styrning. Det innehåller också några exempel på affärs risker som enhets princips instruktioner.

<!-- markdownlint-disable MD026 -->

## <a name="identity-baseline-relevancy"></a>Identitets bas linje relevanta

Traditionella lokala kataloger är utformade för att tillåta företag att strikt kontrol lera behörigheter och principer för användare, grupper och roller i sina interna nätverk och data Center. Dessa kataloger har normalt stöd för implementeringar av en klient, med tjänster som är tillämpliga endast inom den lokala miljön.

Cloud Identity Services utökar en organisations funktioner för autentisering och åtkomst kontroll till Internet. De stöder flera innehavare och kan användas för att hantera användare och åtkomst principer i moln program och distributioner. Offentliga moln plattformar har molnbaserade identitets tjänster som stöder hanterings-och distributions uppgifter och som kan [variera mellan olika integrerings nivåer](../../decision-guides/identity/index.md) med dina befintliga lokala identitets lösningar. Alla dessa funktioner kan resultera i att moln identitets principer är mer komplicerade än dina traditionella lokala lösningar kräver.

Betydelsen av identitets bas disciplinen för moln distributionen beror på teamets storlek och måste integrera din molnbaserade identitets lösning med en befintlig lokal identitets tjänst. De första test distributionerna kanske inte kräver mycket av användarens organisation eller hantering, men eftersom moln fastigheten mognar, behöver du förmodligen stöd för mer komplex organisations integrering och centraliserad hantering.

## <a name="business-risk"></a>Affärs risk

Identitets bas disciplinen försöker hantera kärn affärs risker relaterade till identitets tjänster och åtkomst kontroll. Arbeta med din verksamhet för att identifiera dessa risker och övervaka var och en av dem efter relevans när du planerar för och implementerar dina moln distributioner.

Riskerna varierar mellan olika organisationer, men följande fungerar som vanliga identiteter för identiteter som du kan använda som utgångs punkt för diskussioner i din moln styrnings grupp:

- **Obehörig åtkomst.** Känsliga data och resurser som kan användas av obehöriga användare kan leda till data läckor eller avbrott i tjänsten, vilket bryter mot organisationens säkerhets perimeter och risk för verksamhet eller juridiskt ansvar.
- **Ineffektivning på grund av flera identitets lösningar.** Organisationer med flera Identity Services-klienter kan kräva flera konton för användare. Detta kan leda till ineffektivhet för användare som behöver komma ihåg flera uppsättningar med autentiseringsuppgifter och för den vid hantering av konton över flera system. Om tilldelningen av användar åtkomst inte uppdateras mellan identitets lösningar som personal, team och affärs mål, kan moln resurserna vara sårbara för obehörig åtkomst eller användare som inte kan komma åt nödvändiga resurser.
- **Det går inte att dela resurser med externa partner.** Svårt att lägga till externa affärs partner till dina befintliga identitets lösningar kan förhindra effektiv resurs delning och företags kommunikation.
- **Lokala identitets beroenden.** Äldre autentiseringsmekanismer eller Multi-Factor Authentication i tredje part kanske inte är tillgängliga i molnet, vilket kräver att migrera arbets belastningar som ska återanvändas eller att ytterligare identitets tjänster kan distribueras till molnet. Antingen kan kravet fördröjas eller förhindra migrering och öka kostnaderna.

## <a name="next-steps"></a>Nästa steg

Använd [moln hanterings mal len](./template.md)för att dokumentera affärs risker som sannolikt kommer att introduceras av den aktuella moln implementerings planen.

När en förståelse av realistiska affärs risker har upprättats är nästa steg att dokumentera affärs toleransen för risker och indikatorer och viktiga mått för att övervaka den toleransen.

> [!div class="nextstepaction"]
> [Förstå indikatorer, mått och risk tolerans](./metrics-tolerance.md)
