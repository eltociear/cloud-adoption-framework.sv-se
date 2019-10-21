---
title: Disciplin förbättring av resurs konsekvens
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Disciplin förbättring av resurs konsekvens
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 9d465716784d125edebaf44d8a1bae2f369b9d5a
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548078"
---
# <a name="resource-consistency-discipline-improvement"></a>Disciplin förbättring av resurs konsekvens

Disciplinen för resurs konsekvens fokuserar på sätt att etablera principer för drifts hantering av en miljö, ett program eller en arbets belastning. I de fem disciplinerna i moln styrning omfattar resurs konsekvens övervakning av program, arbets belastning och till gångens prestanda. Den innehåller också de uppgifter som krävs för att uppfylla skalnings kraven, åtgärda prestanda Serviceavtal (SLA) överträdelser och proaktivt undvika SLA-överträdelser via automatiserad reparation.

I den här artikeln beskrivs några potentiella uppgifter som företaget kan använda för att utveckla och engagera disciplinen för resurs konsekvens. Dessa uppgifter kan delas upp i planering, uppbyggnad, införande och drifts faser för implementering av en moln lösning, som sedan upprepas på att tillåta utveckling av en [stegvis metod för moln styrning](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Fyra faser i antagandet](../../_images/govern/adoption-phases.png)

*Figur 1 – implementerings faser för den stegvisa metoden för moln styrning.*

Det är omöjligt för något dokument att redovisa kraven i alla företag. I den här artikeln beskrivs de föreslagna minimi-och potentiella exempel aktiviteterna för varje fas i processens mognads process. Det första målet med dessa aktiviteter är att hjälpa dig att skapa en [policy MVP](../guides/index.md#an-incremental-approach-to-cloud-governance) och upprätta ett ramverk för stegvisa princip förbättringar. Ditt moln styrnings team måste bestämma hur mycket du ska investera i dessa aktiviteter för att förbättra funktionerna för resurs konsekvens styrning.

> [!CAUTION]
> Varken de minsta eller potentiella aktiviteter som beskrivs i den här artikeln är justerade med specifika företags principer eller krav för tredje parts efterlevnad. Den här vägledningen är utformad för att hjälpa till att under lätta de konversationer som kommer att leda till justering av båda kraven med en modell för moln styrning.

## <a name="planning-and-readiness"></a>Planering och beredskap

Den här fasen av styrnings mognads bryggor förenar indelningen mellan affärs resultat och insats bara strategier. Under den här processen definierar ledarskaps gruppen vissa mått, mappar dessa mått till den digitala egendomen och börjar planera den totala migreringen.

**Minsta antal föreslagna aktiviteter:**

- Utvärdera alternativen för [resurs konsekvens verktygskedjan](./toolchain.md) .
- Förstå licensierings kraven för din moln strategi.
- Utveckla ett utkast till rikt linjer för arkitektur och distribuera till viktiga intressenter.
- Bekanta dig med den Resource Manager som du använder för att distribuera, hantera och övervaka alla resurser för din lösning som en grupp.
- Utbilda och involvera de personer och grupper som påverkas av rikt linjerna för arkitektur utveckling.
- Lägg till prioriterade resurs distributions uppgifter i efter släpning i migreringen.

**Potentiella aktiviteter:**

- Arbeta med affärs intressenter och ditt moln strategi team för att förstå den önskade metoden för moln redovisning och kostnads redovisning inom dina affär senheter och organisationer som helhet.
- Definiera kraven för [övervakning och princip tillämpning](./compliance-processes.md) .
- Undersök affärs värde och-kostnader för avbrott för att definiera reparations policy och krav på service nivå avtal.
- Ta reda på om du ska distribuera en [enkel arbets belastning](./governance-simple-workload.md) eller [flera team](./governance-multiple-teams.md) styrnings strategier för dina resurser.
- Fastställ skalbarhets kraven för dina planerade arbets belastningar.

## <a name="build-and-predeployment"></a>Bygg och för distribution

Det krävs flera tekniska och tekniska krav för att kunna migrera en miljö. Den här processen fokuserar på beslut, beredskap och kärn infrastrukturen som fortsätter med migreringen.

**Minsta antal föreslagna aktiviteter:**

- Implementera [verktygskedjan för resurs konsekvens](./toolchain.md) genom att distribuera i en för distributions fas.
- Uppdatera dokument för arkitektur rikt linjer och distribuera till viktiga intressenter.
- Implementera resurs distributions uppgifter i efter släpning för prioriterad migrering.
- Utveckla utbildningsmaterial och dokumentation, medvetenhets kommunikation, stimulans åtgärder och andra program för att hjälpa att använda användar införande.

**Potentiella aktiviteter:**

- Välj en [prenumerations design strategi](../../decision-guides/subscriptions/index.md)och välj de prenumerations mönster som passar bäst för din organisation och dina arbets belastnings behov.
- Använd en [resurs konsekvens](../../decision-guides/resource-consistency/index.md) strategi för att upprätthålla rikt linjer för arkitektur över tid.
- Implementera [resurs namn och tagga standarder](../../decision-guides/resource-tagging/index.md) för dina resurser så att de överensstämmer med dina organisations-och redovisnings krav.
- Om du vill skapa proaktiva styrnings-och tids styrning använder du mallar för distribution och automatisering för att använda vanliga konfigurationer och en konsekvent gruppering när du distribuerar resurser och resurs grupper.
- Upprätta en behörighets modell med minst behörighet, där användare saknar behörighet som standard.
- Ta reda på vem i organisationen som äger varje arbets belastning och konto och vem som behöver åtkomst till att underhålla eller ändra resurserna. Definiera moln roller och ansvars områden som matchar dessa behov och Använd dessa roller som grund för åtkomst kontroll.
- Definiera beroenden mellan resurser.
- Implementera automatisk resurs skalning för att matcha de krav som definierats i plan fasen.
- Genomför åtkomst prestanda för att mäta kvaliteten på de mottagna tjänsterna.
- Överväg att distribuera [principen](https://docs.microsoft.com/azure/governance/policy/overview) för att hantera SLA-tvång med hjälp av konfigurations inställningar och regler för att skapa resurser.

## <a name="adopt-and-migrate"></a>Införa och migrera

Migrering är en stegvis process som fokuserar på förflyttning, testning och införande av program eller arbets belastningar i en befintlig digital egendom.

**Minsta antal föreslagna aktiviteter:**

- Migrera [resurs konsekvens verktygskedjan](./toolchain.md) från för distribution till produktion.
- Uppdatera dokument för arkitektur rikt linjer och distribuera till viktiga intressenter.
- Utveckla utbildningsmaterial och dokumentation, medvetenhets kommunikation, stimulans åtgärder och andra program för att hjälpa att använda användar införande.
- Migrera eventuella befintliga automatiserade reparations skript eller verktyg för att stödja definierade SLA-krav.

**Potentiella aktiviteter:**

- Slutför och testa övervakning och rapportering av data med din valda lokala, molnbaserade gateway eller hybrid lösning.
- Avgör om du behöver göra ändringar i SLA eller hanterings principen för resurser.
- Förbättra drifts aktiviteterna genom att implementera fråge funktioner för att effektivt hitta resurser i din moln egendom.
- Justera resurser för att ändra verksamhets behov och styrnings krav.
- Se till att dina virtuella datorer, virtuella nätverk och lagrings konton återspeglar faktiska resurs åtkomst behov under varje version och justera efter behov.
- Verifiera automatisk skalning av resurser som uppfyller åtkomst kraven.
- Granska användar åtkomst till resurser, resurs grupper och Azure-prenumerationer och justera åtkomst kontroller efter behov.
- Övervaka ändringar i resurs åtkomst planer och validera med intressenter om ytterligare inloggningar behövs.
- Uppdatera ändringar i rikt linjer för arkitektur för att avspegla faktiska kostnader.
- Ta reda på om din organisation kräver en tydlig ekonomisk justering för P & LS for Business Units.
- För globala organisationer ska du implementera kraven för SLA-efterlevnad eller suveränitets krav.
- För moln agg regering distribuerar du en gateway-lösning till en moln leverantör.
- För verktyg som inte tillåter hybrid-eller gateway-alternativ kan du nära övervaka med ett verktyg för drifts övervakning som omfattar alla data Center och moln.

## <a name="operate-and-post-implementation"></a>Drift och efter implementering

När omvandlingen är klar måste styrning och åtgärder vara aktiva för den naturliga livs cykeln för ett program eller en arbets belastning. Den här fasen av styrnings förfallo tid fokuserar på de aktiviteter som vanligt vis kommer efter att lösningen har implementerats och omvandlings cykeln börjar stabilisera sig.

**Minsta antal föreslagna aktiviteter:**

- Anpassa din [resurs konsekvens verktygskedjan](./toolchain.md) utifrån uppdateringar av organisationens föränderliga Cost Management behov.
- Överväg att automatisera eventuella meddelanden och rapporter för att avspegla den faktiska resursanvändningen.
- Förfina rikt linjerna för arkitekturen för att vägleda framtida införande processer.
- Utbilda berörda team med jämna mellanrum för att se till att det pågår rikt linjerna för arkitekturen.

**Potentiella aktiviteter:**

- Justera planer kvartals vis för att avspegla ändringar i de faktiska resurserna.
- Tillämpa och tillämpa styrnings krav automatiskt under framtida distributioner.
- Utvärdera underutnyttjade resurser och Fastställ om de är värda att fortsätta.
- Identifiera fel justeringar och avvikelser mellan planerad och faktisk resursanvändning.
- Bidra till moln implementerings team och moln strategi team för att förstå och lösa dessa avvikelser.
- Avgör om ändringar behöver göras i resurs konsekvensen för fakturerings-och service avtal.
- Utvärdera verktyg för loggning och övervakning för att avgöra om din lokala, moln-gateway eller hybrid lösning behöver justera.
- För affär senheter och geografiskt distribuerade grupper avgör du om din organisation bör överväga att använda ytterligare moln hanterings funktioner, till exempel [Azures hanterings grupper](https://docs.microsoft.com/azure/governance/management-groups) , för att bättre tillämpa centraliserade principer och uppfylla SLA-krav.

## <a name="next-steps"></a>Nästa steg

Nu när du förstår begreppet moln resurs styrning kan du gå vidare till Lär dig mer om [hur resurs åtkomst hanteras](./resource-access-management.md) i Azure för att lära dig hur du utformar en styrnings modell för en [enkel arbets belastning](./governance-simple-workload.md) eller [flera team](./governance-multiple-teams.md) .

> [!div class="nextstepaction"]
> Lär dig mer om [resurs åtkomst hantering i azure](./resource-access-management.md) 
> [Lär dig mer om service nivå avtal för Azure](https://azure.microsoft.com/support/legal/sla) 
> [Lär dig mer om loggning, rapportering och övervakning](../../decision-guides/logging-and-reporting/index.md)
