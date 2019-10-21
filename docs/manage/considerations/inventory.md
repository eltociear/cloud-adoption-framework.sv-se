---
title: Inventering och synlighet – moln hantering och åtgärder
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Inventering och synlighet – moln hantering och åtgärder
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: fe46ec035bb732ec82931358c7e79b41b4f18bd5
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558069"
---
# <a name="inventory-and-visibility-in-cloud-management"></a>Inventering och synlighet i moln hantering

Användnings hantering har ett tydligt beroende av data. Konsekvent hantering kräver en tydlig förståelse av vad som hanteras (inventering) och hur dessa hanterade arbets belastningar och till gångar ändras över tid (synlighet). En överskådlig klarhet om inventering och insyn gör det möjligt för teamet att hantera miljön effektivt. Alla andra operativa hanterings aktiviteter och-processer bygger på dessa två områden av insikter.

Några av de klassiska fraserna som är viktiga för mätningarna anger tonen för den här artikeln: hantera vad som är viktigt. Du kan bara hantera vad du kan mäta. Om du inte kan mäta det kanske det inte spelar någon roll. Inventerings-och Synlighets disciplinen bygger på dessa tidlösa-fraser. Innan du etablerar operativa hanterings processer är det viktigt att samla in data och skapa rätt nivå av synligheten för rätt team.

## <a name="common-customer-challenges"></a>Vanliga kund utmaningar

När inventerings-och Synlighets processer inte tillämpas konsekvent, kan drifts hanterings teamen drabbas av en högre mängd affärs avbrott, längre tid att återställa, och större mängder ansträngning som krävs för att felsöka och prioritering problem. I takt med att ändringar påverkar program med högre prioritet och större antal till gångar, ökar vart och ett av dessa mått ännu snabbare.

Dessa utmaningar härrör från ett litet antal frågor som bara kan besvaras genom konsekvent data/telemetri:

- Hur skiljer sig aktuella tillstånd från den normala Telemetrin om drifts prestanda?
- Vilka till gångar orsakar affärs avbrott på arbets belastnings nivån?
- Vilka till gångar måste åtgärdas för att återgå till acceptabel prestanda för den här arbets belastningen/affärs processen?
- När var avvikelsen igång? Vad var utlösaren?
- Vilka ändringar har gjorts i de underliggande till gångarna? Av vem?
- Var ändringarna avsiktliga? Typer?
- Hur påverkar ändringar prestanda telemetri?

Det är svårt, om inte omöjligt att svara på dessa frågor utan en omfattande, central källa för loggar och telemetridata. För att aktivera moln hantering måste bas linje tjänsten först börja med definitionen av processerna för att säkerställa en konsekvent konfiguration som krävs för att centralisera data. Dessa processer ska avbilda hur konfigurationen kommer att använda insamling av data för att stödja komponenterna i inventeringen och synligheten i nästa avsnitt.

## <a name="components-of-inventory-and-visibility"></a>Lager-och Synlighets komponenter

Det krävs några viktiga komponenter för att skapa synlighet på vilken moln plattform som helst:

1. Ansvar och synlighet
2. Inventering
3. Central loggning
4. Spårning av ändringar
5. Prestanda telemetri

### <a name="responsibility-and-visibility"></a>Ansvar och synlighet

När du etablerar åtaganden för varje arbets belastning är [hanterings ansvaret](./commitment.md#management-responsibility) en viktig faktor. Delegerat ansvar skapar ett behov av delegerad synlighet. Det första steget mot inventering och synlighet är att se till att de ansvariga parterna har till gång till rätt data. Innan du implementerar några molnbaserade verktyg för synlighet bör du se till att varje övervaknings verktyg har kon figurer ATS med rätt åtkomst och omfattning för varje drift team.

### <a name="inventory"></a>Inventering

Om det inte finns någon som vet att en till gång finns är det mycket svårt för till gången att hanteras. Innan en till gång eller arbets belastning kan hanteras måste den inventeras och klassificeras. Det första tekniska steget mot stabila åtgärder är en validering av inventeringen och klassificeringen av inventeringen.

### <a name="central-logging"></a>Central loggning

Centraliserad loggning är nödvändig för att det ska bli synligt för de dagliga Operations Management teamen. Alla till gångar som distribueras till molnet bör registrera loggar på en central plats. Den centrala platsen i Azure är Log Analytics. Centralisering av loggnings enheter rapporterar om ändrings hantering, service hälsa, konfiguration och de flesta andra aspekter av IT-åtgärder.

Att framtvinga konsekvent användning av central loggning är det första steget mot konsekventa upprepnings bara åtgärder. Verkställighet kan utföras genom företags principer. Men när en eventuell tvång bör automatiseras för att säkerställa konsekvens.

### <a name="change-tracking"></a>Spårning av ändringar

Ändra är en konstant i en teknik miljö. Medvetenhet och förståelse för förändringar i flera arbets belastningar är mycket viktigt för tillförlitliga åtgärder. Alla moln hanterings lösningar bör innehålla en metod för att förstå när, hur och varför tekniska ändringar. Utan dessa data punkter hindras reparations åtgärder avsevärt.

### <a name="performance-telemetry"></a>Prestanda telemetri

Affärs åtaganden avseende moln hantering drivs av data. För att kunna upprätthålla åtaganden måste moln drifts teamet först förstå telemetri om stabilitet, prestanda och drift av arbets belastningen och till gångar som har stöd för arbets belastningen.

Kontinuerlig hälsa och drift av nätverket, DNS, operativ system och andra grundläggande aspekter av miljön är kritiska data punkter som bedömer den övergripande hälso tillståndet för alla arbets belastningar.

## <a name="processes"></a>Processer

Det kanske är viktigare än funktionerna i moln hanterings plattformen och moln hanterings processer kommer att realisera drifts åtaganden med verksamheten. Alla moln hanterings metoder bör minst omfatta följande processer:

- Reaktiv övervakning: när avvikelser påverkar affärs åtgärder som åtgärdar dessa avvikelser? Vilka åtgärder vidtar de för att åtgärda avvikelserna.
- Proaktiv övervakning: när avvikelser upptäcks men affärs åtgärder inte påverkas, hur är dessa avvikelser och av vem?
- Åtagande rapportering: Hur ska företaget bekräfta att verksamheten har genomförts med affärs intressenter?
- Budget granskningar: Vad är processen för att granska dessa åtaganden mot budgeterade kostnader? Vad är processen för att justera den distribuerade lösningen eller åtagandena att skapa justering?
- Eskalerings Sök vägar: vilka eskalering sökvägar är tillgängliga när någon av ovanstående processer inte uppfyller företagets behov?

Det finns flera processer relaterade till inventering och synlighet. Listan ovan är utformad för att provoke förväntas bland drift teamet. Genom att besvara dessa frågor kan du utveckla några av de nödvändiga processerna. Det kommer förmodligen att utlösa nya djupare frågor.

## <a name="responsibilities"></a>Ansvar

När du utvecklar processer för drifts övervakning är det lika viktigt att fastställa ansvars områden för daglig drift och vanlig support för varje process.

I en central IT-organisation skulle den ge drifts expert kunskaper. Företaget skulle vara råd i sin natur när de åtgärdar problem.
I ett moln Center med expert organisationer skulle affärs verksamhet ge expert isen och ansvaret för hantering av dessa processer. Det skulle fokusera på automatisering och stöd för team, när de driver miljön.

Men de är vanliga ansvars områden. Organisationer kräver ofta en blandning av ansvar för att uppfylla affärs åtaganden.

## <a name="acting-on-inventory-and-visibility"></a>Handla på inventering och synlighet

Oavsett moln plattform används de fem komponenterna i inventering och synlighet för att driva de flesta operativa processerna. Alla efterföljande ämnes områden kommer att bygga på de data som samlas in. I följande artiklar i den här serien beskrivs hur du kan agera på dessa data och integrera andra data källor.

### <a name="sharing-visibility"></a>Delnings synlighet

Data utan åtgärd ger lite avkastning. Moln hantering kan utökas utöver molnbaserade verktyg och processer. För att kunna hantera bredare processer kan en moln hanterings bas linje behöva förbättras för att inkludera rapportering, IT-tjänstehanterings integrering eller data centralisering. Moln hantering kan behöva inkludera ett eller flera av följande under olika drifts faser.

### <a name="reporting"></a>Rapportering

Offline-processer och kommunikation om åtaganden till affärs intressenter kräver ofta rapportering. Rapportering av självbetjäning eller periodisk rapportering kan vara en nödvändig komponent i en förbättrad hanterings bas linje.

### <a name="it-service-management-itsm-integration"></a>IT Service Management (ITSM)-integrering

ITSM-integrering är ofta det första exemplet på att handla på inventering och synlighet. När avvikelser från förväntade prestanda mönster uppstår använder ITSM-integrering aviseringar från moln plattformen för att utlösa biljetter i ett separat tjänst hanterings verktyg för att utlösa reparations aktiviteter. Vissa drift modeller kan kräva ITSM-integrering som en aspekt av den förbättrade hanterings bas linjen.

### <a name="data-centralization"></a>Data centralisering

Det finns en mängd olika orsaker till varför en verksamhet kan kräva flera klienter i en enda moln leverantör. I dessa scenarier är data centralisering en obligatorisk komponent i den utökade hanterings bas linjen för att ge insyn i var och en av dessa klienter eller miljöer.

## <a name="next-steps"></a>Nästa steg

Operativa krav bygger på inventerings funktioner genom att tillämpa hanterings automatisering och kontroller. Se hur [operativa efterlevnad](./operational-compliance.md) mappar till dina processer.

> [!div class="nextstepaction"]
> [Planera för operativa krav](./operational-compliance.md)
