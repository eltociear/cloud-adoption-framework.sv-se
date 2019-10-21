---
title: Underhåll av affärsprioriteringar under en långsiktig omvandlingsprocess
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Underhåll av affärsprioriteringar under en långsiktig omvandlingsprocess.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: a609dbc1c8779452c5dfc9e4fdf67eb407e6c787
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72549207"
---
# <a name="business-priorities-maintaining-alignment"></a>Affärs prioriteringar: bevara justering

*Omvandlingen* definieras ofta som en dramatisk eller spontan förändring. På ledningsnivå kan ändringen se ut som en dramatisk omvandling. För de som arbetar med ändringsprocessen i organisationen är transformeringen dock lite missvisande. Här beskrivs omvandlingen bättre som en serie med korrekt utförda övergångar från ett tillstånd till ett annat.

Hur lång tid det tar att rationalisera eller överföra en arbetsbelastning varierar beroende på den tekniska komplexiteten. Men även om den här processen kan tillämpas på en enskild arbetsbelastning eller grupp med program snabbt, tar det tid att skapa stora ändringar i användarbasen. Det tar längre tid att sprida ändringarna genom olika lager av befintliga affärsprocesser. Om omvandlingen förväntas skapa beteendemönster hos konsumenter, kan det ta längre tid att visa resultat.

Marknaden väntar tyvärr inte på företagens övergångar. Konsumenternas beteendemönster ändras och det sker ofta oväntat. Marknadens uppfattning om ett företag och dess produkter kan påverkas av sociala medier eller en konkurrents framgångar. Snabba och oväntade marknadsändringar kräver att företagen är flexibla och lyhörda.

Möjligheten att köra processer och tekniska övergångar kräver en konsekvent och stabil insats. Snabba beslut och flexibla åtgärder krävs för att kunna hantera marknadens villkor. Dessa två är motsägande, vilket innebär att prioriteringarna kanske inte justeras. I den här artikeln beskrivs metoder för att upprätthålla övergångsjusteringen under migreringen.

<!-- markdownlint-disable MD026 -->

## <a name="how-can-business-and-technical-priorities-stay-aligned-during-a-migration"></a>Hur kan man fortsätta justera företags- och teknikprioriteringar under en migrering?

Teamen för molnimplementering och molnstyrning fokuserar på att köra den aktuella iterationen och den aktuella versionen. Iterationer ger en stabil ökning av det tekniska arbetet och man undviker därmed kostsamma avbrott som annars skulle leda till att migreringen fördröjs. Versioner säkerställer att den tekniska insatsen och energin förblir fokuserad på affärsmålen för arbetsbelastningsmigreringen. Ett migreringsprojekt kan kräva många versioner under en längre tid. När det är slutfört har marknadsvillkoren troligen ändrats avsevärt.

Molnstrategiteamet fokuserar parallellt på att köra affärsändringsplanen och förbereda för nästa version. Molnstrategiteamet ligger vanligtvis minst en version före och övervakar ändrade marknadsvillkor, samt justerar migreringens kvarvarande uppgifter i enlighet med detta. Detta fokus på att hantera omvandling och justera planen skapar naturliga förändringar av det tekniska arbetet. När affärsprioriteringarna förändras är införandet bara en version bort, vilket ger en teknisk och företagsmässig flexibilitet.

## <a name="business-alignment-questions"></a>Frågor vid affärsanpassning

Följande frågor kan hjälpa molnstrategiteamet att skapa och prioritera migreringens kvarvarande uppgifter för att säkerställa att omvandlingen anpassas efter aktuella affärsbehov.

- Har teamet för molnimplementering sammanställt en lista med de arbetsbelastningar som är klara för migrering?
- Har teamet för molnimplementering valt en kandidat för en första migrering i listan med arbetsbelastningar?
- Har teamen för molnimplementering och molnstyrning samtliga data som krävs för att arbetsbelastningen och molnmiljön ska lyckas?
- Kommer den första arbetsbelastningen att visa den mest relevanta påverkan för verksamheten i nästa version?
- Finns det andra arbetsbelastningar som är bättre kandidater för migreringen?

## <a name="tangible-actions"></a>Materiella åtgärder

Under körningen av affärsändringsplanen letar molnstrategiteamet efter positiva och negativa resultat. När dessa observationer kräver en teknisk förändring läggs justeringarna till som arbetsobjekt i versionens kvarvarande uppgifter för att prioriteras i nästa iteration.

När marknaden ändras samverkar molnstrategiteamet med företaget för att se hur man bäst ska bemöta ändringarna. När det krävs en ändring av migreringsprioriteringen, justeras kvarvarande uppgifter för migreringen. Detta innebär att arbetsbelastningar som tidigare hade lägre prioritet flyttas upp.

## <a name="next-steps"></a>Nästa steg

Med korrekt justerade affärsprioriteringar kan teamet för molnimplementering börja [utvärdera arbetsbelastningar](./evaluate.md) och utveckla arkitektur- och migreringsplaner.

> [!div class="nextstepaction"]
> [Utvärdera arbetsbelastningar](./evaluate.md)
