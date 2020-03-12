---
title: Beslut som påverkar migrering
description: Använd ramverket för moln införande för Azure för att fatta lämpliga beslut och välja körnings aktiviteter som har stöd för en lyckad migrering.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 07856662f95a588f252c78e8a3dd67eba6e8163c
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79094067"
---
<!-- cSpell:ignore migrateable -->

# <a name="decisions-that-affect-migration"></a>Beslut som påverkar migrering

Under migreringen finns det vissa faktorer som påverkar beslut och körning. Den här artikeln förklarar det centrala temat för dessa beslut och utforskar några frågor som är genomgående för alla diskussioner om migreringsprinciper i det här avsnittet av Ramverk för molnimplementering.

## <a name="business-outcomes"></a>Affärsresultat

Målet eller syftet med en implementering kan ha en avgörande betydelse för den föreslagna implementeringsmetoden.

- **Migrering.** Brådskande affärsdrivande faktorer, implementeringshastighet eller kostnadsöverväganden är exempel på verksamhetsresultat. Dessa resultat är avgörande för projekt som skapar affärsvärde från övergångar hos IT eller driftmodeller. Migreringsavsnittet i Ramverk för molnimplementering fokuserar starkt på migreringsrelaterade verksamhetsresultat.
- **Programinnovation.** Exempel på stegvisa resultat är förbättringen av kundupplevelsen och en större marknadsandel. Resultaten kommer från många olika stegvisa ändringar som fokuserar på de aktuella kundernas behov och önskemål.
- **Datadriven innovation.** Nya produkter eller tjänster, särskilt de som kommer från data styrkan, är exempel på störande resultat. Dessa resultat är resultatet av experimentering och förutsägelser som använder data för att bryta ny mark på marknaden.

Det finns inget företag som endast satsar på ett av dessa resultat. Utan verksamheten finns det inga kunder och vice versa. Molnimplementeringen är inget undantag. Företag arbetar ofta för att uppnå var och ett av dessa resultat, men om du fokuserar på alla samtidigt riskerar du att fördela dina resurser för brett och så att de viktigaste framstegen för din verksamhet sker långsammare.

Den här förutsättningen är inte ett krav för att du ska kunna välja något av dessa tre mål, utan ska hjälpa molnstrategiteamet och molnimplementeringsteamet att ta fram verksamhetsprioriteteter som vägledning för de kommande tre till sex månaderna. Dessa prioriteter ställs in genom att rangordna var och ett av dessa tre alternativen från *viktigast* till *minst viktig* eftersom de avgör vad teamet kan bidra med under nästa eller de kommande två kvartalen.

### <a name="act-on-migration-outcomes"></a>Vidta åtgärder vid migreringen

Om drift resultatet är högst rangordnat i listan passar det här avsnittet av ramverket för moln införande bättre. I det här avsnittet förutsätter vi att du behöver prioritera hastighets- och kostnadsbesparingar som primära nyckeltal (KPI: er), vilket innebär att en migreringsmodell för implementering ska vara anpassad till dessa resultat. En migrerings modell är kraftigt predikat på hissen och Shift-migreringen av infrastruktur som en tjänst (IaaS) till gångar som tar slut på ett Data Center och ger kostnads besparingar. I en sådan modell kan modernisering ske, men detta är av mindre betydelse tills den primära migreringsprioriteten har uppnåtts.

### <a name="act-on-application-innovations"></a>Agera på program innovationer

Om marknads andelar och kund upplevelser är dina primära driv rutiner kanske det här avsnittet inte är det bästa avsnittet i moln implementerings ramverket för att vägleda dina Teams ansträngningar. Programinnovation kräver en plan som fokuserar på modernisering och övergång av arbetsbelastningar, oavsett vilken underliggande infrastruktur som används. I sådana fall kan riktlinjerna i det här avsnittet vara informativa men utgör inte det bästa sättet att fatta grundläggande beslut.

### <a name="act-on-data-innovations"></a>Agera på data innovationer

Om data, experimentering, forskning och utveckling (R & D) eller nya produkter är din prioritet under de kommande sex månaderna eller så är det här avsnittet inte det bästa avsnittet i moln implementerings ramverket som vägleder dina Teams ansträngningar. All datainnovation gynnas av vägledning om migrering av befintliga källdata. Men projektets huvudsakliga fokus ska ligga på ingående data och integration av fler datakällor. Att utöka den här vägledningen med förutsägelser och nya upplevelser är mycket viktigare än migreringen av IaaS-tillgångar.

## <a name="effort"></a>Projektet

Migreringen kan variera beroende på de berörda arbetsbelastningarnas storlek och komplexitet. En mindre migrering av arbetsbelastningar som omfattar ett par hundra virtuella datorer är en taktisk process som kan genomföras med automatiserade verktyg såsom[Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-overview). Å andra sidan kräver en storskalig företagsmigrering med tiotusentals arbetsbelastningar en mycket strategisk process som kan inbegripa omfattande omstrukturering, återuppbyggnad och ersättning av befintliga program för att integrera kapacitet för plattform som en tjänst (PaaS) och programvara som en tjänst (SaaS). [Det är viktigt att identifiera och balansera omfattningen](../../../strategy/balance-the-portfolio.md) av dina planerade migreringar.

Innan du fattar beslut som kan ha en långsiktig inverkan på det aktuella migreringsprogrammet är det viktigt att du skapar samförstånd om följande beslut.

### <a name="effort-type"></a>Typ av projekt

Vid all migrering av stor skala (mer än 250 virtuella datorer) migreras till gångar med hjälp av en mängd olika över gångs alternativ, som diskuteras i de femRS-rationalisering: *Rehost*, *rekonstruktör, rekonstruktion, återskapa*och *Ersätt*.

Vissa arbetsbelastningar moderniseras genom att *återskapa* eller *omarbeta arkitekturen*, vilket skapar modernare program med nya funktioner och teknisk kapacitet. Andra tillgångar genomgår en *omstrukturering*, till exempel en övergång till containrar eller andra modernare värd- och driftmetoder som inte påverkar lösningarnas kodbas. Vanliga virtuella datorer och andra till gångar som är mer väl etablerade går genom en *Rehost* -process och över de till gångarna från data centret till molnet. Vissa arbets belastningar kan eventuellt migreras till molnet, men ska i stället *ersättas* med service-baserade (SaaS) moln tjänster som uppfyller samma affärs behov&mdash;exempelvis genom att använda Office 365 som ett alternativ till att migrera Exchange Server-instanser.

I de flesta scenarier skapar vissa företagshändelser en tvingande funktion som gör att en hög procentandel av tillgångarna tillfälligt migreras med *värdbyte*, följt av en mer betydande sekundär övergång med en av de andra migreringsstrategierna när de väl är i molnet. Den här processen kallas ofta för en *molnövergång*.

Under processen med att [rationalisera den digitala egendomen](../../../digital-estate/calculate.md) används de här typerna av beslut för varje tillgång som ska migreras. Nu är det dock nödvändigt att göra ett antagande om baslinjen. Vilken av de fem migreringsstrategierna passar bäst med verksamhetsmålen eller verksamhetsresultaten som ligger till grund för migreringen? Det här antagandet vägleder migreringen.

### <a name="effort-scale"></a>Projektets skala

Migreringens skala är nästa viktiga förhandsbeslut. De processer som krävs för att migrera 1 000-till gångar skiljer sig från de processer som krävs för att flytta 10 000-till gångar. Innan du påbörjar en migrering är det viktigt att besvara följande frågor:

- **Hur många tillgångar som stöder arbetsbelastningarna som ska migreras har jag i dag?** Tillgångar omfattar datastrukturer, program, virtuella datorer och nödvändiga IT-enheter. Vi rekommenderar att du väljer en relativt liten arbetsbelastning för din första migrering.
- **Av dessa till gångar hur många ska migreras?** Det är vanligt att avsluta en del av tillgångarna under migreringen, på grund av att slutanvändarberoendet inte längre upprätthålls.
- **Vilka uppskattningar är uppifrån och ned för skalan av de migrerade till gångarna?** Beräkna antalet stödtillgångar, till exempel program, virtuella datorer, datakällor och IT-enheter för arbetsbelastningarna som ingår i migreringen. Se avsnittet om [digital egendom](../../../digital-estate/index.md) i Cloud Adoption Framwork för vägledning om att identifiera relevanta tillgångar.

### <a name="effort-timing"></a>Tidsramar för projektet

Ofta motiveras migreringar av en viktig händelse för verksamheten som är tidskänslig. En vanlig drivkraft är slutet eller början på ett värdkontrakt med tredje part. Även om det finns många potentiella affärs händelser som kräver en migrering, delar de en gemensam faktor: ett slutdatum. Det är viktigt att förstå tidsschemat för kommande verksamhetshändelser så att åtgärder och hastigheter kan planeras och verifieras ordentligt.

## <a name="recap"></a>Sammanfattning

Innan du fortsätter måste du dokumentera följande antaganden och dela dem med molnstrategiteamet och molnimplementeringsteamet:

- Affärsresultat.
- Roller, dokumenterade och raffinerade för att *utvärdera*, *migrera*, *optimera*och *skydda och hantera* migreringsprocessen.
- Definition av färdig, dokumenterad och raffinerad separat för *utvärderingen*, *migrera*, *optimera*och *skydda och hantera* migreringsprocessen.
- Typ av projekt.
- Projektets skala.
- Tidsramar för projektet.

## <a name="next-steps"></a>Nästa steg

När processen har tolkats mellan teamet är det dags att granska tekniska krav. [Checklistan för planering av migreringsmiljön](./planning-checklist.md) används för att kontrollera att det finns en färdig teknisk grund för migreringen.

När processen har förståts i teamet, är det dags att granska tekniska krav för [planerings check lista för migrering] för att säkerställa att den tekniska grunden är redo för migrering.

> [!div class="nextstepaction"]
> [Läs checklistan för planering av migrering](./planning-checklist.md)
