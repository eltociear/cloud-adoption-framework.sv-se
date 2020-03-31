---
title: Cost Management disciplin förbättring
description: Förstå de potentiella aktiviteter som ett företag utför för att utveckla och mogna sitt Cost Management disciplin i varje fas av moln införande.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 47d6cd60e67b6f17a3a9a3abef6788847854f2f1
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434726"
---
# <a name="cost-management-discipline-improvement"></a>Cost Management disciplin förbättring

Cost Management disciplinen försöker lösa kärn affärs risker relaterade till utgifter som uppstår vid värdbaserade molnbaserade arbets belastningar. Inom de fem disciplinerna i moln styrning är Cost Management involverad för att kontrol lera kostnaden och användningen av moln resurser med målet att skapa och underhålla en planerad kostnads cykel.

Den här artikeln beskriver potentiella uppgifter som ditt företag utför för att utveckla och mogna din Cost Management disciplin. Dessa uppgifter kan delas upp i planering, uppbyggnad, införande och drifts faser för implementering av en moln lösning, som sedan upprepas på att tillåta utveckling av en [stegvis metod för moln styrning](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Fyra faser i antagandet](../../_images/govern/adoption-phases.png)

*Figur 1 – implementerings faser för den stegvisa metoden för moln styrning.*

Inget enskilt dokument kan uppfylla kraven i alla företag. I den här artikeln beskrivs de föreslagna minimi-och potentiella exempel aktiviteterna för varje fas i processens mognads process. Det första målet med dessa aktiviteter är att hjälpa dig att skapa en [policy MVP](../guides/index.md#an-incremental-approach-to-cloud-governance) och upprätta ett ramverk för stegvisa princip förbättringar. Ditt moln styrnings team måste bestämma hur mycket du ska investera i dessa aktiviteter för att förbättra dina Cost Management styrnings funktioner.

> [!CAUTION]
> Varken de minsta eller potentiella aktiviteter som beskrivs i den här artikeln är justerade med specifika företags principer eller krav för tredje parts efterlevnad. Den här vägledningen är utformad för att hjälpa till att under lätta de konversationer som kommer att leda till justering av båda kraven med en modell för moln styrning.

## <a name="planning-and-readiness"></a>Planering och beredskap

Den här fasen av styrnings mognads bryggor förenar indelningen mellan affärs resultat och insats bara strategier. Under den här processen definierar ledarskaps gruppen vissa mått, mappar dessa mått till den digitala egendomen och börjar planera den totala migreringen.

**Minsta antal föreslagna aktiviteter:**

- Utvärdera [Cost Management verktygskedjan](./toolchain.md) -alternativ.
- Utveckla ett utkast till rikt linjer för arkitektur och distribuera till viktiga intressenter.
- Utbilda och involvera de personer och grupper som påverkas av rikt linjerna för arkitektur utveckling.

**Potentiella aktiviteter:**

- Se till att budget besluten har stöd för affärs justeringen för din moln strategi.
- Verifiera inlärnings mått som du använder för att rapportera om den genomförda allokeringen av finansiering.
- Förstå den önskade moln redovisnings modellen som påverkar hur moln kostnader ska redovisas.
- Bekanta dig med planen för digital plan och validera förväntningarna för korrekt kostnads beräkning.
- Utvärdera köp alternativ för att avgöra om det är bättre att "betala per användning" eller att göra ett åtagande genom att köpa en Enterprise-avtal.
- Justera affärs målen med planerade budgetar och justera budget planen efter behov.
- Utveckla en mål-och budget rapporterings mekanism för att meddela tekniska och affärs intressenter i slutet av varje kostnads cykel.

## <a name="build-and-predeployment"></a>Bygg och för distribution

Det krävs flera tekniska och tekniska krav för att kunna migrera en miljö. Den här processen fokuserar på beslut, beredskap och kärn infrastrukturen som fortsätter med migreringen.

**Minsta antal föreslagna aktiviteter:**

- Implementera [Cost Management verktygskedjan](./toolchain.md) genom att distribuera i en för distributions fas.
- Uppdatera dokument för arkitektur rikt linjer och distribuera till viktiga intressenter.
- Utveckla utbildningsmaterial och dokumentation, medvetenhets kommunikation, stimulans åtgärder och andra program för att hjälpa att använda användar införande.
- Ta reda på om dina inköps krav överensstämmer med dina budgetar och mål.

**Potentiella aktiviteter:**

- Justera dina budget planer med [prenumerations strategin](../../decision-guides/subscriptions/index.md) som definierar din Core ägarskaps modell.
- Använd [strategin för resurs konsekvens](../../decision-guides/resource-consistency/index.md) för att upprätthålla rikt linjer för arkitektur och kostnader över tid.
- Fastställ om några kostnads avvikelser påverkar dina implementerings-och migrerings planer.

## <a name="adopt-and-migrate"></a>Införa och migrera

Migrering är en stegvis process som fokuserar på förflyttning, testning och införande av program eller arbets belastningar i en befintlig digital egendom.

**Minsta antal föreslagna aktiviteter:**

- Migrera din [Cost Management verktygskedjan](./toolchain.md) från för distribution till produktion.
- Uppdatera dokument för arkitektur rikt linjer och distribuera till viktiga intressenter.
- Utveckla utbildningsmaterial och dokumentation, medvetenhets kommunikation, stimulans åtgärder och andra program för att hjälpa att använda användar införande.

**Potentiella aktiviteter:**

- Implementera din moln redovisnings modell.
- Se till att dina budgetar återspeglar dina faktiska utgifter under varje version och justera efter behov.
- Övervaka ändringar i budget planer och validera med intressenter om ytterligare inloggningar behövs.
- Uppdatera ändringar i rikt linjer för arkitektur för att avspegla faktiska kostnader.

## <a name="operate-and-post-implementation"></a>Drift och efter implementering

När omvandlingen har slutförts måste styrning och åtgärder vara aktiva för livs cykeln för ett program eller en arbets belastning. Den här fasen av styrnings förfallo tid fokuserar på de aktiviteter som vanligt vis kommer efter att lösningen har implementerats och omvandlings cykeln börjar stabilisera sig.

**Minsta antal föreslagna aktiviteter:**

- Anpassa din [Cost Management verktygskedjan](./toolchain.md) baserat på ändringar i din organisations behov av kostnads hantering.
- Överväg att automatisera eventuella meddelanden och rapporter för att avspegla faktiska utgifter.
- Förfina rikt linjerna för arkitekturen för att vägleda framtida införande processer.
- Utbilda berörda team regelbundet för att se till att det pågår rikt linjerna i arkitekturen.

**Potentiella aktiviteter:**

- Kör en kvartals vis moln företags granskning för att kommunicera värde som levereras till företaget och tillhör ande kostnader.
- Justera planer kvartals vis för att återspegla ändringar av faktiska utgifter.
- Fastställ ekonomisk justering till P & LS för Business Unit-prenumerationer.
- Analysera från intressenter värde och kostnads rapport metoder varje månad.
- Åtgärda underutnyttjade till gångar och Fastställ om de är värda att fortsätta.
- Identifiera fel justeringar och avvikelser mellan planen och faktiska utgifter.
- Bidra till moln implementerings team och moln strategi teamet med att förstå och lösa dessa avvikelser.

## <a name="next-steps"></a>Nästa steg

Nu när du förstår begreppet moln identitets styrning kan du undersöka [Cost Management verktygskedjan](./toolchain.md) för att identifiera de Azure-verktyg och-funktioner som du behöver när du utvecklar den Cost Management styrnings disciplinen på Azure-plattformen.

> [!div class="nextstepaction"]
> [Cost Management verktygskedjan för Azure](./toolchain.md)
