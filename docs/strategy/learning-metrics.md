---
title: Hur kan vi justera insatser för meningsfulla inlärnings mått?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Förklaring av konceptet inlärnings mått
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: f761f85fa4b21b35e8428985707176624b92a5ec
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027461"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-can-we-align-efforts-to-meaningful-learning-metrics"></a>Hur kan vi justera insatser för meningsfulla inlärnings mått?

I [översikten över verksamhets resultatet](./business-outcomes/index.md) beskrivs olika sätt att mäta och förmedla den effekt en omvandling har på företaget. Tyvärr kan det ta flera år för några av dessa resultat för att skapa mätbara resultat. Tavlan och C-serien är missnöjd med rapporter som visar 0% delta under långa tids perioder.

Inlärnings mått är tillfälliga, kortare Mät värden som kan kopplas tillbaka till verksamhets resultat på längre sikt. Dessa mått stämmer bra med en tillväxt tänkesätt och hjälper dig att placera kulturen för att bli mer elastisk. I stället för att markera den förväntade bristen på framsteg mot ett långsiktigt affärs mål, markerar inlärnings måtten tidiga indikatorer för framgång. Måtten markerar också tidiga indikationer på felet, vilket troligen ger den bästa möjligheten att lära sig och justera planen.

Precis som med mycket av materialet i det här ramverket antar vi att du är bekant med [omvandlings resan](../govern/guides/index.md) som passar bäst med dina önskade affärs resultat. Den här artikeln beskriver några utbildnings mått för varje omvandlings resa för att illustrera konceptet.

## <a name="cloud-migration"></a>Molnmigrering

Den här omvandlingen fokuserar på kostnad, komplexitet och effektivitet, med tonvikt på IT-åtgärder. De enklaste Mät data bakom den här omvandlingen är flyttningen av till gångar till molnet. I den här typen av omvandling mäts den digitala fastigheten av virtuella datorer (VM), rack eller kluster som är värdar för dessa virtuella datorer, drifts kostnader för data Center, nödvändiga kapital kostnader för att underhålla system och avskrivning av dessa till gångar över tid.

När virtuella datorer flyttas till molnet minskas beroendet av lokala äldre till gångar. Kostnaden för till gångs underhåll minskar också. Företaget kan tyvärr inte inse kostnads minskningen förrän klustren har avetablerats och data centrets lån upphör att gälla. I många fall realiseras inte det fulla värdet för ansträngning förrän avskrivnings cyklerna har slutförts.

Justera alltid mot ekonomi chefen eller ekonomi kontoret innan du gör finansiella rapporter. IT-team kan dock vanligt vis uppskatta aktuella penning kostnader och framtida penning kostnads värden för varje virtuell dator baserat på CPU, minne och förbrukad lagring. Du kan sedan använda det värdet för varje migrerad virtuell dator för att uppskatta de omedelbara besparingarna och det framtida penning värdet för ansträngningen.

## <a name="application-innovation"></a>Program innovation

Cloud-aktiverad program innovation fokuserar i stor utsträckning på kund upplevelsen och kundens vilja använda produkter och tjänster som tillhandahålls av företaget. Det tar tid för stegvisa förändringar som påverkar konsumenternas eller kundens köp beteenden. Men Application innovation-cykler tenderar att vara mycket kortare än de är i andra former av omvandling. Den traditionella rådgivningen är att du bör börja med att förstå de speciella beteenden som du vill påverka och använda dessa beteenden som inlärnings mått. I ett e-handelsprogram kan till exempel det totala köpet eller tilläggets inköp vara mål beteendet. För ett video företag kan det vara dags att titta på video strömmar som mål.

Utmaningen med kund beteende mått är att de enkelt kan påverkas av yttre variabler. Det är ofta viktigt att inkludera relaterad statistik med inlärnings måtten. Den här relaterade statistiken kan omfatta versions takt, buggar löses per utgåva, kod täckning av enhets tester, antal sidvyer, sid data flöde, sid inläsnings tid och andra prestanda mått för appar. Var och en kan visa olika aktiviteter och ändringar i kodbasen och kund upplevelsen för att korrelera med en högre nivå av kund beteende mönster.

## <a name="data-innovation"></a>Data innovation

Att ändra en bransch, avbryta marknader eller omvandla produkter/tjänster kan ta flera år. I en molnbaserad data Innovations ansträngning är experimentet viktiga för att mäta framgång. Var transparent genom att dela förutsägelse mått som procent sannolikhet, antal misslyckade experiment och mängden modeller som har tränats. Felen kommer att ackumuleras snabbare än vad som lyckas. De här måtten kan vara discouraging och det är viktigt att ledningen förstår den tid och investering som krävs för att utnyttja data korrekt.

Å andra sidan är en del positiva indikatorer ofta kopplade till data driven inlärning: centralisering av heterogena data uppsättningar, data ingångar och democratization av data. När teamet har lärt oss om kunden i morgon kan du skapa verkliga resultat idag. Stödjande inlärnings mått kan vara:

- Antal tillgängliga modeller
- Antal förbrukade partner data källor
- Enheter som producerar ingångs data
- Volym för ingångs data
- Typer av data

Ett ännu mer värdefullt mått är antalet instrument paneler som skapats från kombinerade data källor. Det här talet visar de affärs processer för aktuella tillstånd som påverkas av nya data källor. Genom att dela nya data källor öppet kan ditt företag dra nytta av data med hjälp av rapporterings verktyg som Power BI för att skapa ökande insikter och driva företags förändringar.

## <a name="next-steps"></a>Nästa steg

När inlärnings måtten har justerats är du redo att börja [utvärdera den digitala fastigheten](../digital-estate/index.md) mot dessa mått. Resultatet blir en omvandling efter [släpning eller](../migrate/migration-considerations/prerequisites/technical-complexity.md)efter släpning för migrering.

> [!div class="nextstepaction"]
> [Utvärdera den digitala fastigheten](../digital-estate/index.md)
