---
title: Mät kund påverkan
description: Definiera det önskade kund flödet och upprätta utbildnings mått för att mäta kundens beteende och införande.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 3ba4cc99b210784c7503085234c25c1d9a0ae634
ms.sourcegitcommit: d660484d534bc61fc60470373f3fcc885a358219
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/18/2020
ms.locfileid: "79508006"
---
# <a name="measure-for-customer-impact"></a>Mät kundernas påverkan

Det finns flera sätt att mäta för kund påverkan. Den här artikeln hjälper dig att definiera mått för att validera Hypotheses som kan uppstå i arbetet för att [bygga med kund empati](./build.md).

## <a name="strategic-metrics"></a>Strategiska mått

Under [strategi fasen](../../strategy/index.md) i moln implementeringens livs cykel, granskar vi [motivation](../../strategy/motivations.md) och [affärs resultat](../../strategy/business-outcomes/index.md). Dessa metoder tillhandahåller en uppsättning mått som du kan använda för att testa kund påverkan. När innovationen är klar brukar du se resultaten som är justerade med dina strategiska mål.

Innan du etablerar inlärnings statistik definierar du ett litet antal strategiska mått som du vill att innovationen ska påverka. Vanligt vis överensstämmer dessa strategiska mått med en eller flera av följande resultat områden: [affärs smidighet](../../strategy/business-outcomes/agility-outcomes.md), [kund engagemang](../../strategy/business-outcomes/engagement-outcomes.md), [kund täckning](../../strategy/business-outcomes/reach-outcomes.md), [finansiell påverkan](../../strategy/business-outcomes/fiscal-outcomes.md)eller i händelse av drifts innovation: [lösnings prestanda](../../strategy/business-outcomes/fiscal-outcomes.md).

Dokumentera de överenskomna måtten och spåra deras inverkan ofta. Men det förväntar sig inte att något av dessa mått visas för flera iterationer. Mer information om hur du ställer in och justerar förväntningar för de berörda parterna finns i [åtagande till iteration](./index.md#commitment-to-iteration).

Förutom motivation och affärs resultat, fokuserar resten av den här artikeln på inlärnings mått som har utformats för att hjälpa till med transparent identifiering och kundfokuserade iterationer. För ytterligare information om dessa aspekter, se [engagemang för genomskinlighet](./index.md#commitment-to-transparency).

## <a name="learning-metrics"></a>Inlärnings mått

När den första versionen av en minimal livskraftig produkt (MVP) delas med kunder, helst i slutet av den första utvecklings iterationen, kommer det inte att påverka strategiska mått. Flera iterationer senare kan teamet fortfarande vara kämpar för att ändra beteenden tillräckligt för att påverka strategiska mått. Under inlärnings processer, t. ex. bygge-Measure – lära, kan vi informera teamet om att anta inlärnings mått. Dessa mått som spårar och inlärnings möjligheter.

### <a name="customer-flow-and-learning-metrics"></a>Kund flöde och utbildnings mått

Om en MVP-lösning verifierar en kundfokuserad hypotes, kommer lösningen att köra vissa förändringar i kund beteenden. De här beteende ändringarna mellan kund kohorter bör förbättra affärs resultatet. Tänk på att ändring av kund beteende vanligt vis är en process i flera steg. Eftersom varje steg ger möjlighet att mäta påverkan kan antagande teamet hålla inlärningen på vägen och bygga en bättre lösning.

Att lära dig om förändringar av kund beteenden börjar genom att mappa flödet som du hoppas att du vill se från en MVP-lösning.

![Kund flöde som används för att fastställa inlärnings mått](../../_images/innovate/customer-flow-learning-metrics.png)

I de flesta fall får ett kund flöde en enkelt definierad start punkt och högst två slut punkter. Mellan start-och slut punkterna finns olika inlärnings mått som ska användas som mått i feedback-slingan:

1. **Start punkt – första utlösare:** Start punkten är det scenario som utlöser behovet av den här lösningen. När lösningen har skapats med kund empati bör den inledande utlösaren inspirera en kund för att testa MVP-lösningen.
2. **Kunden behöver uppfyllas:** Hypotesen verifieras när en kund behöver uppfylls med hjälp av lösningen.
3. **Lösnings steg:** Den här termen avser de steg som krävs för att flytta kunden från den första utlösaren till ett lyckat resultat. Varje steg skapar ett inlärnings mått baserat på ett kund beslut att gå vidare till nästa steg.
4. **Individuell tillämpning som uppnås:** Nästa gång som utlösaren påträffas, om kunden återgår till lösningen för att få behov uppfyllda, har ett individuellt införande uppnåtts.
5. **Indikator för affärs resultat:** När en kund beter sig på ett sätt som bidrar till det definierade affärs resultatet observeras en indikator för affärs resultat.
6. **Verklig innovation:** När *affärs resultats indikatorer* och *individuell införande* båda sker i önskad skala har du faktiskt en riktig innovation.

Varje steg i kund flödet genererar inlärnings mått. Efter varje iteration (eller version) testas en ny version av hypotesen. På samma tid testas anpassningar till lösningen för att avspegla förändringar i hypotesen. När kunderna följer den angivna sökvägen i ett valfritt steg registreras ett positivt mått. När kunderna avviker från den angivna sökvägen registreras ett negativt mått.

Dessa justerings-och avvikelse räknare skapar inlärnings mått. Vart och ett bör registreras och spåras som moln implementerings team för att gå vidare till företags resultat och verklig innovation. I [Lär dig med kunder](./learn.md)diskuterar vi hur du kan använda dessa mått för att lära dig och bygga bättre lösningar.

### <a name="grouping-and-observing-customer-partners"></a>Gruppera och iaktta kund partner

Det första måttet i definiera inlärnings mått är kund partner definitionen. Alla kunder som deltar i innovations cyklar kvalificeras som kund partner. För att du ska kunna mäta beteendet bör du använda en kohort modell för att definiera kund partner. I den här modellen grupperas kunderna för att öka din förståelse av deras svar på förändringar i MVP: er. Dessa grupper liknar vanligt vis följande:

- **Experiment eller fokus grupp:** Gruppera kunder baserat på deras medverkan i ett särskilt experiment som har utformats för att testa ändringar över tid.
- **Segment:** Gruppera kunder efter företagets storlek.
- **Lodrätt:** Att gruppera kunder efter de *branscher* som de representerar.
- **Enskilda demografiska:** Gruppering baserat på personliga demografiska som ålder och fysisk plats.

Med hjälp av dessa typer av grupperingar kan du verifiera inlärnings mått över olika kors delar av de kunder som väljer att samar beta med dig under dina Innovations insatser. Alla efterföljande mått bör härledas från definierbar kund grupper.

## <a name="next-steps"></a>Nästa steg

När inlärnings måtten ackumuleras kan teamet börja [lära sig kunderna](./learn.md).

> [!div class="nextstepaction"]
> [Lär dig med kunder](./learn.md)

Några av begreppen i den här artikeln bygger vidare på ämnen som beskrivs i [den Lean-starten](http://theleanstartup.com/book), skrivet av Eric Återställ inställningar.
