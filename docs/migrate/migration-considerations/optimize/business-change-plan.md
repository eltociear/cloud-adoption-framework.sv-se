---
title: Utveckla en plan för verksamhets ändring
description: Använd ramverket för moln införande för Azure för att lära dig mer om hur en plan för företags förändringar kan hjälpa dig att implementera en bredare användar implementerings plan.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: d1c842c672cc091deaad4e0b7f4ffc89231895c7
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79312041"
---
# <a name="business-change-plan"></a>Plan för verksamhetsändring

Traditionellt har IT-avdelningen hanterat införandet av nya arbetsbelastningar. Under en större omvandling, som en migrering av datacenter eller molnmigrering kan ett liknande tillvägagångssätt där IT-avdelningen leder migreringen användas. Detta kan dock leda till missade möjligheter att hitta ytterligare affärsvärden. Därför rekommenderas att ett annorlunda arbetssätt används vid migrering av arbetsbelastning. Denna artikel beskriver de sätt som en plan för verksamhetsförändring tillför värde till en vanlig plan för att få användare att använda ny teknik.

## <a name="traditional-user-adoption-approach"></a>Traditionellt tillvägagångssätt för användarinförande

Planer för att introducera ny teknik för användare fokuserar på hur användarna kommer att börja använda ny teknik eller hantera förändringar i befintlig teknik. Detta arbetssätt är välbeprövat när det gäller att introducera användare för nya verktyg. I en typisk plan för användarinförande fokuserar IT-avdelningen på installation, konfiguration, underhåll och den utbildning som hör till de tekniska förändringar som införs i verksamheten.

Även om arbetssätten varierar finns det allmänna ämnen som ingår i de flesta planer för användarinförande. Dessa teman baseras vanligtvis på ett arbetssätt som bygger på riskstyrning och på att underlätta införandet vid stegvisa förbättringar. Eason-matrisen, som visas i bilden nedan, representerar drivkrafterna bakom dessa ämnen för olika införandetyper.

![Eason-matris för fokus vid användarinförande](../../../_images/migrate/eason-matrix.jpg)

*Eason-matris för typer av användarinförande.*

Dessa ämnen baseras normalt på antagandet att införandet av nya lösningar för användare i hög utsträckning ska fokusera på riskstyrning och på att underlätta hanteringen av förändring. Dessutom har IT-avdelningar i stor utsträckning fokuserat på riskerna vid teknikförändringen och på att underlätta ändringen.

## <a name="create-business-change-plans"></a>Skapa affärs ändrings planer

En plan för verksamhetsändring ser längre än till den tekniska förändringen och antar att varje införande i en migrering driver någon typ av affärsprocessförändring. Den följer tidslinjen både framåt och bakåt vad gäller de tekniska förändringarna. Följande frågor hjälper användare att tänka på användarinförande utifrån perspektivet verksamhetsändring, för att maximera verksamhetspåverkan:

**Bakåtriktade frågor.** Bakåtriktade frågor ser på påverkan eller ändringar som kommer före användarinförandet:

- Har ett förväntat [affärsresultat](../../../strategy/business-outcomes/index.md) kvantifierats?
- Kan verksamhetspåverkan överföras till definierade [inlärningsmått](../../../strategy/learning-metrics.md)?
- Vilka affärsprocesser och team drar fördel av denna tekniska lösning?
- Vem inom företaget kan bäst välja rätt avancerade användare för testning och feedback?
- Har de verksamhetsledare som påverkas varit inblandade i prioriterings- och migreringsplaneringen?
- Finns det kritiska händelser eller datum för företaget som kan påverkas av ändringen?
- Maximerar planen för verksamhetsändring påverkan samtidigt som den minimerar verksamhetsavbrott?
- Förväntas något driftsstopp? Har slutanvändarna informerats om en driftstoppsperiod?

**Framåtriktade frågor.** När införandet är slutfört kan verksamhetsförändringen inledas. Tyvärr är det här många planer för användarinförande slutar. Framåtriktade frågor hjälper teamet för molnstrategi att bibehålla fokus på omvandling efter att den tekniska ändringen är genomförd:

- Hanterar verksamhetsanvändarna ändringarna på ett bra sätt?
- Har förväntningarna på prestanda bibehållits nu när den tekniska ändringen införts?
- Förändras verksamhetsprocesser eller kundupplevelser på förväntade sätt?
- Krävs ytterligare ändringar för inlärningsmått?
- Överensstämde ändringarna med de avsedda verksamhetsmålen? Om inte, varför inte?
- Krävs fler ändringar för att realisera verksamhetsmål?
- Har några negativa effekter observerats som ett resultat av denna ändring?

Planen för verksamhetsförändring varierar från företag till företag. Målet med dessa frågor är att underlätta att bättre integrera verksamheten i de ändringar som hör till varje införande. Genom att inte se varje införande som en teknikförändring som måste införas utan som en plan för verksamhetsförändring kan det bli enklare att nå verksamhetsmål.

## <a name="next-steps"></a>Nästa steg

När verksamhetsförändring dokumenterats och planerats kan [verksamhetstestning](./business-test.md) inledas.

> [!div class="nextstepaction"]
> [Ledning för verksamhetstestning (UAT) under migrering](./business-test.md)

## <a name="references"></a>Referenser

- Eason, K. (1988) _informations teknik och organisatoriska förändringar_, New York: Taylor och Francis.
