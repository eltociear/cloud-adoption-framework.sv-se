---
title: Förbereda ett migrerat program för produktionsbefordran
description: Använd ramverket för moln införande för Azure för att förstå validering som är engagerade i att förbereda ett migrerat program för produktions befordran.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 2ad912c7bc2e61465a81e278714f5018c2373f7f
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80429235"
---
# <a name="prepare-a-migrated-application-for-production-promotion"></a>Förbereda ett migrerat program för produktionsbefordran

När en arbetsbelastning befordras dirigeras produktionsanvändartrafiken till de migrerade tillgångarna. Beredskapsaktiviteter hjälper dig att förbereda arbetsbelastningen för den trafiken. Här följer några affärsrelaterade och tekniska överväganden som hjälp för beredskapsarbetet.

## <a name="validate-the-business-change-plan"></a>Validera planen för verksamhetsändring

Omvandlingen sker när affärsanvändare eller kunder utnyttjar en teknisk lösning för att köra processer som driver verksamheten. Beredskap är en bra möjlighet att validera [planen för verksamhetsändringar](./business-change-plan.md) och erbjuda en lämplig utbildning för de affärsteam och tekniska team som deltar. Se särskilt till att följande tekniska aspekter av ändringsplanen kommuniceras korrekt:

- Utbildning av slutanvändare har slutförts (eller åtminstone planerats).
- Alla avbrottsfönster har kommunicerats och godkänts.
- Produktionsdata har synkroniserats och verifierats av slutanvändare.
- Verifiera tidpunkten för befordran och implementering. Se till att tidslinjer och ändringar har förmedlats till slutanvändare.

## <a name="final-technical-readiness-tests"></a>Slutgiltigt tekniskt beredskapstest

*Redo* är det sista steget före produktionsversionen. Det innebär också att det är den sista chansen att testa arbetsbelastningen. Följande är några test som är lämpliga under den här fasen:

- **Nätverksisoleringstest.** Testa och övervaka nätverkstrafik för att säkerställa korrekt isolering och inga oväntade nätverks sårbarheter förekommer. Kontrollera också att nätverksroutning som ska avbrytas under övergången inte har oväntad trafik.
- **Beroendetest.** Kontrollera att alla beroenden för arbetsbelastningsprogram har migrerats och är tillgängliga från de migrerade tillgångarna.
- **Test av affärskontinuitet och haveriberedskap.** Kontrollera att alla säkerhetskopior och SLA:er har etablerats. Om möjligt kan du utföra en fullständig återställning av tillgångarna från lösningen för affärskontinuitet och haveriberedskap.
- **Test av slutanvändarväg.** Verifiera trafikmönster och routning för slutanvändartrafik. Se till att nätverksprestandan stämmer överens med förväntningarna.
- **Slutgiltig prestandakontroll.** Se till att prestandatesten har slutförts och godkänts av slutanvändarna. Kör automatiserade prestandatest.

## <a name="final-business-validation"></a>Slutgiltig företagsvalidering

När företagets ändringsplan och tekniska beredskap har verifierats kan följande sista steg slutföra företagsvalideringen:

- **Kostnadsvalidering (plan jämfört med faktiska).** Testningen kommer sannolikt att medföra ändringar av storlek och arkitektur. Se till att den faktiska distributionsprissättningen fortfarande överensstämmer med den ursprungliga planen.
- **Kommunicera och köra startpunktplan.** Innan starten ska startpunkten kommuniceras och köras.

## <a name="next-steps"></a>Nästa steg

När alla beredskapsaktiviteter har slutförts är det dags att [befordra arbetsbelastningen](./promote.md).

> [!div class="nextstepaction"]
> [Vad krävs för att befordra en migrerad resurs till produktion?](./promote.md)
