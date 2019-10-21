---
title: 'Cloud innovation: mått'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introduktion till moln innovation – Mät innehåll
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 00928171c3bfba1638a7e8e43ea08df4745754d2
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557653"
---
# <a name="measure-for-customer-impact"></a>Mått för kund påverkan

Det finns flera sätt att mäta för kund påverkan. I den här artikeln får du hjälp med att definiera åtgärder som kan hjälpa dig att validera Hypotheses som skapas vid försök att [skapa med kund empati](./build.md).

## <a name="strategic-metrics"></a>Strategiska mått

Under [strategi fasen](../../strategy/index.md) i moln implementeringens livs cykel, vägleds läsarna genom att skapa och dokumentera information om [motivation](../../strategy/motivations.md) och [affärs resultat](../../strategy/business-outcomes/index.md). De här övningarna ger en uppsättning mått som du kan använda som ett test av kund påverkan. När innovationen lyckas skapas resultat som är justerade med strategi mål.

Innan du etablerar inlärnings mått måste du definiera ett litet antal strategiska mått som denna innovation förväntas påverka. Vanligt vis anpassas de strategiska måtten till ett eller flera av följande resultat områden: [affärs smidighet](../../strategy/business-outcomes/agility-outcomes.md), [kund engagemang](../../strategy/business-outcomes/engagement-outcomes.md), [kund täckning](../../strategy/business-outcomes/reach-outcomes.md), [finansiell påverkan](../../strategy/business-outcomes/fiscal-outcomes.md)eller i händelse av drifts innovation: [lösning Prestanda](../../strategy/business-outcomes/fiscal-outcomes.md).

Dokumentera de överenskomna måtten och spåra påverkan ofta. Men du förväntar dig inte resultat i något av dessa mått för att få flera iterationer. Se [åtagandet att upprepas](./index.md#commitment-to-iteration) för att justera förväntningarna.

Förutom motivation och affärs resultat, fokuserar resten av den här artikeln på inlärnings mått som har utformats för att vägleda identifiering och kund fokuserade iterationer. Se [engagemang för transparens](./index.md#commitment-to-transparency) för att justera förväntningarna.

## <a name="learning-metrics"></a>Inlärnings mått

När den första versionen av en minimal livskraftig produkt (MVP) delas med kunder, helst i slutet av den första utvecklings iterationen, kommer det inte att påverka strategiska mått. Flera iterationer senare kan teamet fortfarande vara kämpar för att ändra beteenden tillräckligt för att påverka strategiska mått. Under inlärnings processer, till exempel bygge-Measure-lära, är det tillrådligt att teamet antar inlärnings mått. Dessa mått kan enkelt spåras och utnyttjas i möjligheter att lära sig.

### <a name="customer-flow-and-learning-metrics"></a>Kund flöde och utbildnings mått

Om en MVP-lösning verifierar en kundfokuserad hypotes, kommer lösningen att köra vissa förändringar i kund beteenden. Dessa beteenden mellan olika kund kohorter kommer att driva affärs resultat. Lyckligt vis är ändring av kund beteende ofta en process i flera steg. Varje steg ger en möjlighet att mäta påverkan, så att implementerings teamet kan lära sig och bygga en bättre lösning.

Att lära dig om förändringar i kund beteenden börjar genom att mappa det önskade flödet som skapats av en MVP-lösning.

![Kund flöde som används för att fastställa inlärnings mått](../../_images/innovate/customer-flow-learning-metrics.png)

I de flesta fall får ett kund flöde en enkelt definierad start punkt och högst två slut punkter. Mellan start-och slut punkterna finns olika inlärnings mått som ska användas som mått i feedback-slingan:

1. **Start punkt – första utlösare:** Start punkten är det scenario som utlöser behovet av den här lösningen. När lösningen har skapats med kund empati bör den inledande utlösaren inspirera en kund för att testa MVP-lösningen.
2. **Kunden behöver uppfyllas:** Hypotesen verifieras när en kund behöver uppfylls med hjälp av lösningen.
3. **Lösnings steg:** Varje steg som krävs för att flytta kunden från den första utlösaren till ett lyckat resultat är ett lösnings steg. Varje steg skapar ett inlärnings mått baserat på kund beslut för att gå vidare till nästa steg.
4. **Individuell tillämpning som uppnås:** Nästa gång som utlösaren påträffas, om kunden återgår till lösningen så att behovet uppfylls igen, så uppnås ett individuellt införande.
5. **Indikator för affärs resultat:** När en kund beter sig på ett sätt som positivt bidrar till det definierade affärs resultatet, observeras en indikator för affärs resultat.
6. **Verklig innovation:** När "affärs resultats indikatorer" och "individuell införande" båda sker i den önskade skalan, är den sanna innovationen erfaren.

Varje steg i kund flödet genererar inlärnings mått. Efter varje iteration (eller version) testas en ny version av hypotesen. På samma tid testas anpassningar till lösningen för att avspegla förändringar i hypotesen. När kunderna följer den angivna sökvägen i ett valfritt steg registreras ett positivt mått. När kunderna avviker från den angivna sökvägen för att uppfylla sina behov registreras ett negativt mått.

Dessa justerings-och avvikelse räknare skapar inlärnings mått. Vart och ett bör registreras och spåras som moln implementerings team för att gå vidare till förverkligande av affärs resultat och verklig innovation. I nästa artikel lär vi dig hur du kan [använda](./learn.md) dessa mått för att lära dig och bygga bättre lösningar.

### <a name="grouping-and-observing-customer-partners"></a>Gruppera och iaktta kund partner

Det första måttet för att definiera inlärnings mått är kund partner definitionen. Alla kunder som deltar i innovations cyklar kvalificeras som kund partner. För att kunna mäta beteendet är det viktigt att definiera kund partner i en kohort modell. I den här modellen grupperas kunderna för att bäst förstå hur de svarar på eventuella ändringar i MVP: en. Kund partner är ofta grupperade baserat på data punkter som följande:

- **Experiment eller fokus grupp:** Gruppering baserat på kunders medverkan i ett särskilt experiment för att testa ändringar över tid.
- **Segment:** Gruppera kunder efter företagets storlek.
- **Lodrätt:** Att gruppera kunder efter de branscher som de representerar.
- **Enskilda demografiska:** Gruppering baserat på personliga demografiska som ålder eller fysisk plats.

Den här typen av gruppering gör det möjligt att verifiera inlärnings mått över olika kors delar av de kunder som väljer att samar beta med dig under Innovations ansträngningar. Alla efterföljande mått bör observeras baserat på en definierbar kund grupp.

## <a name="next-steps"></a>Nästa steg

När inlärnings mått är ackumulerade kan teamet börja [lära sig kunderna](./learn.md).

> [!div class="nextstepaction"]
> [Lär dig med kunder](./learn.md)

Några av begreppen i den här artikeln bygger vidare på ämnen som beskrivs i [den Lean-starten](http://theleanstartup.com/book), skrivet av Eric Återställ inställningar.
