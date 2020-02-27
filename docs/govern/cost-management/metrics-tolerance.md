---
title: Mått och indikatorer för Cost Management risk tolerans
description: Använd ramverket för moln införande för Azure för att kvantifiera Cost Management risk tolerans mått och indikatorer i förhållande till moln styrning.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: c44fc6974be69ff684089c65aa23da5eefbfd814
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77708826"
---
# <a name="cost-management-metrics-indicators-and-risk-tolerance"></a>Cost Management mått, indikatorer och risk tolerans

I den här artikeln får du hjälp med att kvantifiera affärs risk toleransen när det gäller Cost Management. Genom att definiera mått och indikatorer kan du skapa ett affärs ärende för att göra en investering i den Cost Management disciplinen.

## <a name="metrics"></a>Mått

Cost Management fokuserar vanligt vis på mått som rör kostnader. Som en del av din riskanalys vill du samla in data som är relaterade till dina aktuella och planerade utgifter i molnbaserade arbets belastningar för att fastställa hur mycket risk du möter och hur viktiga investeringar i kostnads styrning är till din moln införande strategi.

Följande är exempel på användbara mått som du bör samla för att utvärdera risk tolerans i Cost Management disciplin:

- **Årliga utgifter:** Den totala årliga kostnaden för tjänster som tillhandahålls av en moln leverantör.
- **Månads utgifter:** Den totala månads kostnaden för tjänster som tillhandahålls av en moln leverantör.
- **Prognostiserat jämfört med faktisk kvot:** Förhållandet mellan prognostiserade och faktiska utgifter (månatlig eller årlig).
- **Relations takt för införande (MOM):** Procent andelen av delta i moln kostnader från månad till månad.
- **Ackumulerad kostnad:** Totalt antal upplupna dagliga utgifter från början av månaden.
- **Utgifts trender:** Utgifts trend mot budgeten.

## <a name="risk-tolerance-indicators"></a>Risk tolerans indikatorer

Vid tidiga storskaliga distributioner, t. ex. utveckling/testning eller experimentella första arbets belastningar, kommer Cost Management troligen vara av relativt låg risk. När fler till gångar distribueras ökar risken och affärs toleransen för risk är sannolikt att avböja. I takt med att fler moln implementerings grupper ges möjlighet att konfigurera eller distribuera till gångar till molnet, ökar risken och toleranserna minskar. I takt med att utveckla en Cost Managements disciplin tar människor från moln införande fasen att distribuera mer nya nya tekniker.

I det tidiga skedet av moln implementeringen kommer du att arbeta med din verksamhet för att fastställa en risk tolerans bas linje. När du har en bas linje måste du bestämma vilka kriterier som skulle utlösa en investering i Cost Management disciplinen. Dessa kriterier är förmodligen olika för alla organisationer.

När du har identifierat [affärs risker](./business-risks.md)arbetar du med din verksamhet för att identifiera de riktmärken som du kan använda för att identifiera utlösare som potentiellt kan öka riskerna. Här följer några exempel på hur mått, till exempel de som nämns ovan, kan jämföras med toleransen för risk bas linjen för att ange ditt företags behov av att investera i Cost Management.

- **Åtagande driven (vanligt förekommande):** Ett företag som är förpliktigat att _$x utgifter, 000000_ det här året på en moln leverantör. De behöver en Cost Management disciplin för att säkerställa att verksamheten inte överskrider sina utgifts mål med mer än 20% och att de kommer att använda minst 90% av sitt åtagande.
- **Procent utlösare:** Ett företag med moln utgifter som är stabila för sina produktions system. Om detta ändras med mer än _x%_ är en Cost Management disciplin en bra investering.
- **Överetablerad utlösare:** Ett företag som bedömer att de distribuerade lösningarna har överetablerats. Cost Management är en prioritets investering tills de visar rätt justering av etablering och till gångs användning.
- **Månads utgifts utlösare:** Ett företag som tillbringar över _$x 000_ per månad betraktas som en justerbar kostnad. Om utgifterna överstiger den summan under en angiven månad måste de investera i Cost Management.
- **Utlösare för årliga utgifter:** Ett företag med en IT R & D-budget som gör det möjligt för utgifter _$x 000_ per år på moln experimentet. De kan köra produktions arbets belastningar i molnet, men de anses fortfarande experimentella lösningar om budgeten inte överstiger den mängden. Om budgeten överskrids måste de behandla budgeten som en produktions investering och hantera utgifter på ett nära och samma sätt.
- **Drifts kostnad-negativ (ovanlig):** Som ett företag är de viktiga för drifts kostnader och behöver kontrollerna för kostnads hantering på plats innan du distribuerar en arbets belastning för utveckling/testning.

## <a name="next-steps"></a>Nästa steg

Använda [mallen för moln hantering](./template.md), dokument mått och tolerans indikatorer som överensstämmer med den aktuella moln implementerings planen.

Granska exempel Cost Management principer som utgångs punkt för att utveckla principer som åtgärdar specifika affärs risker som överensstämmer med dina moln implementerings planer.

> [!div class="nextstepaction"]
> [Granska exempel principer](./policy-statements.md)
