---
title: Molncenter för utmärkthet
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Beskriver bildande av en expert på ett moln Center (CCoE).
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: c1819bafaed5e75e6667754d598b075eb3204925
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73564302"
---
# <a name="cloud-center-of-excellence"></a>Molncenter för utmärkthet

Företags-och teknisk rörlighet är grund mål för de flesta IT-organisationer. CCoE (Cloud Center of expert) är en funktion som skapar balans mellan hastighet och stabilitet.

## <a name="function-structure"></a>Funktions struktur

CCoE kräver samarbete mellan var och en av följande funktioner:

- Moln införande (särskilt lösnings arkitekter)
- Moln strategi (särskilt program-och projektledare)
- Molnstyrning
- Molnplattform
- Molnautomatisering

## <a name="impact-and-cultural-change"></a>Inverkan och kulturell förändring

När den här funktionen är korrekt strukturerad och stöds kan deltagarna påskynda innovationen och migreringen samtidigt som den totala kostnaden för förändringar och ökad affärs flexibilitet minskas. När den här funktionen har implementerats kan den skapa märkbara minskningar i tid till marknad. Som lag praxis kan kvalitets indikatorer förbättra, inklusive tillförlitlighet, prestanda effektivitet, säkerhet, underhåll och kund tillfredsställelse. Dessa vinster i effektivitet, flexibilitet och kvalitet är särskilt viktiga om företaget planerar att implementera storskaliga migreringar av moln migrering eller vill använda molnet för att driva innovationer som är kopplade till marknads differentiering.

När det är klart kommer en CCoE-modell att skapa en betydande kulturell skiftning. Den grundläggande lokala CCoE-metoden är att den fungerar som en koordinator, partner eller representant för verksamheten. Den här modellen är en paradigm skiftning från den traditionella vyn som en drift enhet eller ett abstraktions lager mellan verksamheten och IT-tillgångar.

Följande bild ger en analog till den här kulturella ändringen. Utan en CCoE metod är det att fokusera på att tillhandahålla kontroll-och centrala ansvar, som fungerar som stoppljus i ett snitt. När CCoE är klar är fokus på frihet och delegerat ansvar, vilket är mer som en Roundabout vid ett snitt.

![Analogt för en CCoE paradigm-skiftning](../_images/ready/ccoe-paradigm-shift.png)

Ingen av de metoder som illustreras i den analoga bilden ovan är rätt eller felaktig, men de är bara alternativa vyer av ansvar och hantering. Om du vill upprätta en självbetjänings modell som gör det möjligt för affär senheter att fatta egna beslut med en uppsättning rikt linjer och etablerade, upprepnings bara kontroller, kan en CCoE modell få plats i teknik strategin.

## <a name="key-responsibilities"></a>Viktiga ansvars områden

Den främsta avgiften för CCoE-teamet är att påskynda moln användningen genom molnbaserade eller hybrid lösningar.

Målet med CCoE är att:

- Hjälp till att skapa en modern IT-organisation genom flexibla metoder för att samla in och implementera affärs krav.
- Använd återanvändbara distributions paket som överensstämmer med säkerhets-, efterlevnads-och tjänst hanterings principer.
- Underhålla en fungerande Azure-plattform i justering med operativa procedurer.
- Granska och godkänn användningen av molnbaserade verktyg.
- Med tiden kan du standardisera och automatisera de plattforms komponenter och lösningar som behövs.

## <a name="meeting-cadence"></a>Mötes takt

CCoE är en funktion som bemannas av fyra grupper med hög efter frågan. Det är viktigt att tillåta ekologiskt samarbete och spåra tillväxt genom en gemensam lagrings plats/lösnings katalog. Maximera naturliga interaktioner, men minimera möten. När den här funktionen är vuxen bör teamen försöka begränsa särskilda möten. Närvaro vid återkommande möten, t. ex. release-möten som är värdbaserade av moln implementerings teamet, kommer att tillhandahålla indata. Parallellt kan ett möte efter att varje versions plan delas ut kan ge den här gruppen en minimal touch-punkt.

## <a name="solutions-and-controls"></a>Lösningar och kontroller

Varje medlem i CCoE har kunskaper om nödvändiga begränsningar, risker och skydd som ledde till den aktuella uppsättningen av IT-kontroller. CCoE gemensamma ansträngningar bör göra det möjligt att förstå de molnbaserade (eller hybrid lösningar) lösningar eller kontroller som möjliggör önskade affärs resultat. När lösningar skapas delas de med olika team i form av kontroller eller automatiseringar som fungerar som guardrails för olika ansträngningar. Dessa guardrails hjälper till att dirigera de kostnads fria aktiviteterna i olika team, samtidigt som du delegerar ansvaret till deltagarna i olika migrerings-eller Innovations arbete.

Exempel på den här över gången:

| Scenario | Lösning för CCoE | Lösning efter CCoE |
|---------|---------|---------|
| Etablera en produktions SQL Server | Nätverks-, IT-och data plattforms team etablerar olika komponenter i flera dagar eller till och med veckor. | Teamet som kräver servern distribuerar en PaaS-instans av Azure SQL Database. Alternativt kan en förgodkännd mall användas för att distribuera alla IaaS-tillgångar till molnet i timmar. |
| Etablera en utvecklings miljö | Nätverks-, IT-, utvecklings-och DevOps-teamen samtycker till specifikationer och distribuerar en miljö. | Utvecklings teamet definierar sina egna specifikationer och distribuerar en miljö baserat på allokerad budget. |
| Uppdatera säkerhets kraven för att förbättra data skyddet | Nätverks-, IT-och säkerhets team uppdaterar olika nätverks enheter och virtuella datorer i flera miljöer för att lägga till skydd. | Cloud styrelsers verktyg används för att uppdatera principer som kan tillämpas direkt på alla till gångar i alla moln miljöer. |

## <a name="negotiations"></a>Misslycka

I roten för en CCoE ansträngning är en pågående förhandlings process. CCoE-teamet förhandlar med befintliga IT-funktioner för att minska den centrala kontrollen. Kompromisserna för verksamheten i denna förhandling är frihet, flexibilitet och hastighet. Värdet av kompromisser för befintliga IT-team levereras som nya lösningar. De nya lösningarna ger det befintliga IT-teamet en eller flera av följande fördelar:

- Möjlighet att automatisera vanliga problem.
- Förbättringar i konsekvens (minskning av de dagliga besvären).
- Möjlighet att lära sig och distribuera nya tekniska lösningar.
- Minskning av incidenter med hög allvarlighets grad (färre snabb korrigeringar eller svar på senaste kvälls tid).
- Möjlighet att utöka sitt tekniska område och adressera bredare ämnen.
- Deltagande i affärs lösningar på högre nivå, vilket riktar sig på teknikens påverkan.
- Minskning av menial underhålls uppgifter.
- Ökad teknik strategi och automatisering.

I utbyte för dessa förmåner kan den befintliga IT-funktionen vara handel med följande värden, oavsett om det är reellt eller uppfattat:

- Kontroll av manuella godkännande processer.
- Uppfattning om stabilitet från ändrings kontroll.
- En uppfattning om jobb säkerhet från slutförandet av nödvändiga, men repetitiva uppgifter.
- Konsekvens som kommer från iakttagande av befintliga IT-lösningar-leverantörer.

I friska Cloud Forward-företag är den här förhandlings processen en dynamisk konversation mellan peer-datorer och partner IT-team. De tekniska detaljerna kan vara komplexa, men är hanterbara när de förstår målet och har stöd för CCoE-ansträngningarna. När det är mindre än stöd för, kan följande avsnitt om hur du aktiverar CCoE lyckas hjälpa till att lösa kultur Blocker.

## <a name="enable-ccoe-success"></a>Aktivering av CCoE lyckades

Innan du fortsätter med den här modellen är det viktigt att validera företagets tolerans för en tillväxt tänkesätt och det är lättare att släppa ut centrala ansvar. Som nämnts ovan är syftet med en CCoE att utbyta kontroll över rörlighet och hastighet.

Den här typen av ändring tar tid, experiment och förhandling. Det kommer att finnas ojämnheter och ställa in säkerhets kopieringar under den här lagrings processen. Men om teamet är upprättat och inte är underställt från experimentering, finns det en hög sannolikhet att lyckas med att förbättra flexibiliteten, hastigheten och tillförlitligheten. En av de största faktorerna när en CCoE lyckades eller misslyckades har stöd från ledarskap och viktiga intressenter.

### <a name="key-stakeholders"></a>Viktiga intressenter

IT-ledarskap är den första och mest uppenbara från intressenter. IT-chefer kommer att spela en viktig del. IT-CHEFens support och andra IT-ledare krävs dock för den här processen.

Mindre uppenbart är behovet av affärs intressenter. Affärs flexibilitet och tids till marknad är viktiga motivation för CCoE-investeringar. Därför bör de viktigaste intressenterna ha en förtjänad andel av dessa områden. Exempel på affärs intressenter är verksamhets ledare, ekonomi chefer, drift ledare och affärs produkt ägare.

### <a name="business-stakeholder-support"></a>Business från intressenter-support

CCoE-ansträngningar kan påskyndas med support från affärs intressenterna. En stor del av CCoE-ansträngningarna är centrerad runt att göra långsiktiga förbättringar av affärs flexibilitet och snabbhet. Att definiera påverkan av aktuella operativ modeller och värdet av förbättringar är värdefullt som ett guide-och förhandlings verktyg för CCoE. Att dokumentera följande objekt föreslås för CCoE-support:

- Upprätta en uppsättning affärs resultat och mål som förväntas till följd av affärs flexibilitet och hastighet.
- Definiera tydligt färger som skapats av aktuella IT-processer (till exempel hastighet, flexibilitet, stabilitet och kostnads utmaningar).
- Definiera tydligt den historiska effekten av de här smärta punkterna (till exempel förlorad marknads andel, konkurrenternas vinster i funktioner och funktioner, dåliga kund upplevelser och budget ökningar).
- Definiera affärs förbättrings möjligheter som blockeras av de aktuella smärta punkterna och drift modellerna.
- Upprätta tids linjer och mått som är relaterade till dessa affärs möjligheter.

Dessa data punkter är inte ett angrepp på den. I stället hjälper de CCoE att lära sig tidigare och upprätta realistiska efter släpning och planera för förbättringar.

**Kontinuerlig support och engagemang:** CCoE team kan demonstrera snabb returer i vissa områden. De högre målen, till exempel affärs flexibilitet och tid till marknad, kan dock ta mycket längre tid. Under mognaden är det en hög risk för CCoE som kommer att undvikas eller tas bort för att fokusera på andra IT-ansträngningar.

Under de första sex till nio månaderna av CCoE-ansträngningar rekommenderar vi att affärs intressenterna fördelar tiden för att möta varje månad med IT-ledarskap och CCoE. Det finns lite behov av formell ceremoni till dessa möten. Att helt enkelt komma ihåg CCoE-medlemmar och deras ledarskap av vikten av det här programmet kan gå ihop med att köra CCoE-framgång.

Dessutom rekommenderar vi att affärs intressenterna håller sig informerad om de framsteg och Blocker som CCoE-teamet upplever. Många av deras ansträngningar ser ut som teknisk minutiae. Det är dock viktigt för affärs intressenter att förstå hur planen fortskrider, så att de kan engagera sig när gruppen skadar ånga eller blir distraherande av andra prioriteringar.

### <a name="it-stakeholder-support"></a>Support för IT-från intressenter

**Stöd för visionen:** En lyckad CCoE-ansträngning kräver stor förhandling med befintliga IT-gruppmedlemmar. När du är färdig med detta bidrar all IT till lösningen och du kan känna dig van vid ändringen. Om detta inte är fallet kan vissa medlemmar i det befintliga IT-teamet behöva hålla på för att kontrol lera mekanismer av olika anledningar. Support för IT-intressenter är avgörande för att CCoE ska lyckas när dessa situationer inträffar. Uppmuntra och stärkande av de övergripande målen för CCoE är viktigt att lösa blockerare till rätt förhandling. I sällsynta fall kan IT-intressenter till och med behöva stega in och dela upp ett död läge eller en bunden röst för att hålla CCoE-processen.

**Behåll fokus:** En CCoE kan vara ett betydande åtagande för alla resurs begränsade IT-team. Att ta bort starka arkitekter från kortsiktiga projekt för att fokusera på långsiktiga vinster kan skapa problem för team medlemmar som inte är en del av CCoE. Det är viktigt att IT-parter är fokuserade på målet för CCoE. Supporten för IT-ledare och IT-intressenter krävs för att kunna avprioritera avbrott i dagliga åtgärder för att prioritera CCoE-uppgifter.

**Skapa en buffert:** CCoE-teamet kommer att experimentera med nya metoder. Vissa av dessa metoder kan inte justeras korrekt med befintliga åtgärder eller tekniska begränsningar. Det finns en Real risk för CCoE som är i drift eller kan gå igenom andra team när experimentet slutar fungera. Att uppmuntra och buffra teamet från följderna av inlärnings möjligheterna "snabba misslyckanden" är viktigt. Det är lika viktigt att hålla grupp kontot till en växande tänkesätt, vilket säkerställer att de är i beaktande med de experimenten och hitta bättre lösningar.

## <a name="next-steps"></a>Nästa steg

I moln Center med hög kvalitet krävs både [moln plattforms funktioner](./cloud-platform.md) och [moln automatiserings funktioner](./cloud-automation.md). Nästa steg är att justera [moln plattformens funktioner](./cloud-platform.md).

> [!div class="nextstepaction"]
> [Justera en moln plattforms kapacitet](./cloud-platform.md)
