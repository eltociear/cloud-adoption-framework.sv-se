---
title: Validera antaganden för utvärderingen före migrering
description: Använd Cloud Adoption Framework för Azure för att lära dig hur du verifierar antaganden för utvärdering innan du påbörjar migreringen till molnet.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: a04208a147d2cf9f50b30f8053b49367fa08aabe
ms.sourcegitcommit: da7ebd67a0ebf29361f093f00e10217b212a2eb2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/01/2020
ms.locfileid: "80527687"
---
# <a name="validate-assessment-assumptions-before-migration"></a>Validera antaganden för utvärderingen före migrering

Många av dina befintliga arbetsbelastningar är utmärkta kandidater för molnmigrering, men inte alla tillgångar är kompatibla med molnplattformar och inte alla arbetsbelastningar kan dra nytta av värdhantering i molnet. Med [Planering för digital egendom](../../../digital-estate/index.md) kan du skapa en övergripande [uppgiftslista för migrering](../prerequisites/technical-complexity.md#migration-backlog-aligning-business-priorities-and-timing) för potentiella arbetsbelastningar som kan migreras. Det här planeringsarbetet sker dock på hög nivå. Det förlitar sig på antaganden som gjordes av teamet för molnstrategi och går inte in på djupet i tekniska frågor.

Innan du migrerar en arbetsbelastning till molnet är det därför mycket viktigt att utvärdera de enskilda tillgångar som associeras med den arbetsbelastningen med avseende på deras migreringslämplighet. Under den här utvärderingen bör molnimplementeringsteamet utvärdera teknisk kompatibilitet, den arkitektur som krävs, förväntningar på prestanda/storleksbestämning samt beroenden för att säkerställa att den migrerade arbetsbelastningen effektivt kan distribueras till molnet.

*Utvärderingsprocessen* är den första av fyra inkrementella aktiviteter som inträffar i en iteration. Enligt beskrivningen i artikeln om förutsättningar gällande [teknisk komplexitet och ändringshantering](../prerequisites/technical-complexity.md) bör ett beslut fattas i förväg för att avgöra hur den här fasen ska genomföras. I synnerhet: kommer utvärderingar att slutföras av teamet för molnimplementering under samma sprint som det faktiska migreringsarbetet? Alternativt: kommer en våg- eller fabriksmodell användas för att slutföra utvärderingar i en separat iteration? Om den här grundläggande processfrågan inte kan besvaras av varje medlem i teamet kan det vara bra att gå igenom avsnittet [Förutsättningar](../prerequisites/index.md) igen.

## <a name="objective"></a>Mål

Utvärdera en migreringskandidat samt arbetsbelastningen, associerade tillgångar och beroenden före migrering.

## <a name="definition-of-done"></a>Definitionen av *klar*

Den här processen är färdig när följande är kända om en enskild migreringskandidat:

- Sökvägen från lokal plats till molnet, inklusive beslut om tillvägagångssättet för produktionsuppflyttning, har definierats.
- Alla nödvändiga processer för godkännanden, ändringar, kostnadsuppskattningar och validering har slutförts så att teamet för molnimplementering kan genomföra migreringen.

## <a name="accountability-during-assessment"></a>Ansvarstagande under utvärdering

Molnimplementeringsteamet ansvarar för hela utvärderingsprocessen. Medlemmar i molnstrategiteamet har dock vissa ansvarsområden som anges i följande avsnitt.

## <a name="responsibilities-during-assessment"></a>Ansvarsområden under utvärdering

Utöver det övergripande ansvaret finns det åtgärder som en person eller en grupp måste vara direkt ansvarig för. Här följer några aktiviteter som ansvariga parter måste tilldelas:

- **Affärsprioritet.** Teamet förstår syftet med att migrera den här arbetsbelastningen, inbegripet alla avsedda effekter på verksamheten.
  - En medlem i molnstrategiteamet ska ha det slutliga ansvaret för den här aktiviteten under ledning av molnimplementeringsteamet.
- **Inriktning med intressenter.** Teamet riktar in förväntningar och prioriteringar med interna intressenter och identifierar framgångskriterier för migreringen. Hur ser framgång ut efter migrering?
- **Förfinad rationalisering.** Utvärdera de första antagandena om rationalisering. Bör en annan [rationaliseringsmetod](../../../digital-estate/rationalize.md) användas för att migrera den här speciella arbetsbelastningen?
- **Moderniseringsbeslut.** Oaktat rationaliseringsbeslutet, ska olika resurser i arbetsbelastningen moderniseras för att utnyttja PaaS-baserade lösningar?
- **Kostnad.** Kostnaden för målarkitekturen har beräknats, och den övergripande budgeten har justerats.
- **Migreringsstöd.** Teamet har beslutat hur det tekniska arbetet med migreringen ska genomföras, däribland beslut om partner- eller Microsoft-support.
- **Utvärdering.** Arbetsbelastningen utvärderas för kompatibilitet och beroenden.
  - Den här aktiviteten ska ges till en ämnesexpert som är bekant med arkitekturen och driften av kandidatarbetsbelastningen.
- **Arkitektur.** Teamet har kommit överens om sluttillståndsarkitekturen för den migrerade arbetsbelastningen.
- **Migreringsverktyg.** Beroende på metoder för modernisering och arkitektur kan olika migreringsverktyg användas för att automatisera migreringen. Kommer migreringen att använda de bästa [migreringsverktygen](../../../decision-guides/migrate-decision-guide/index.md)?
- **Inriktning med uppgiftslista.** Molnimplementeringsteamet granskar krav och beslutar om migreringen av kandidatarbetsbelastningen. Efter beslutet ska lanseringens uppgiftslista och iterationens uppgiftslista uppdateras därefter.
- **Uppdelad arbetsstruktur eller bakåtplanerat arbetsschema.** Teamet upprättar ett schema för huvudmilstolpar och identifierar mål för då processer för planering, implementering och granskning har slutförts.
- **Slutligt godkännande.** Alla nödvändiga godkännare har granskat planen och godkänt metoden för migrering av tillgången.
  - I syfte att undvika överraskningar senare i processen bör minst en representant från företaget delta i godkännandeprocessen.

> [!CAUTION]
> Den här fullständiga listan över ansvarsområden och åtgärder kan stödja stora och komplexa migreringar som omfattar flera roller med olika ansvarsnivåer och som kräver en detaljerad godkännandeprocess. Mindre och enklare migreringsarbeten kräver kanske inte alla roller och åtgärder som beskrivs här. För att fastställa vilka av dessa aktiviteter som ger värde och vilka som är onödiga bör molnimplementeringsteamet och molnstrategiteamet använda den här fullständiga processen som en del av den första arbetsbelastningsmigreringen. När arbetsbelastningen har verifierats och testats kan teamet utvärdera den här processen och välja vilka åtgärder som ska användas därefter.

## <a name="next-steps"></a>Nästa steg

Nu när du har en allmän förståelse för utvärderingsprocessen är du redo att påbörja processen genom att [klassificera arbetsbelastningar](./classify.md).

> [!div class="nextstepaction"]
> [Klassificera arbetsbelastningar](./classify.md)
