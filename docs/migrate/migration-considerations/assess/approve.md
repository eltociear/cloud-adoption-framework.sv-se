---
title: Godkänna arkitekturändringar före migrering
description: Förstå vikten av godkännande före migrering
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 3776f468c48e7483d884a0c6cae8654218ac1a94
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76802760"
---
# <a name="approve-architecture-changes-before-migration"></a>Godkänna arkitekturändringar före migrering

Under utvärderingsprocessen för migrering utvärderas, konstrueras och beräknas varje arbetsbelastning i syfte att utveckla en plan för arbetsbelastningens framtida tillstånd. Vissa arbetsbelastningar kan migreras till molnet utan ändringar i arkitekturen. Lokalt underhåll av konfiguration och arkitektur kan minska riskerna och effektivisera migreringsprocessen. Tyvärr kan inte alla program köras i molnet utan ändringar i arkitekturen. När arkitekturändringar krävs kan den här artikeln hjälpa till att klassificera ändringarna och ge viss vägledning om lämpliga godkännandeaktiviteter.

## <a name="business-impact-and-approval"></a>Affärspåverkan och godkännande

Under migreringen är det troligt att vissa saker ändras på sätt som påverkar verksamheten. Även om ändringen ibland inte kan undvikas, bör överraskningar på grund av icke-avslöjade eller icke-genererade ändringar vara. För att upprätthålla från intressenter-support under hela migreringen är det viktigt att undvika överraskningar. Om programägarna eller verksamhetens intressenter överraskas kan implementeringsarbetet saktas ned eller stanna av helt.

Innan migreringen är det viktigt att förbereda arbets Belastningens företags ägare för alla ändringar som kan påverka affärs processer, till exempel ändringar i:

- Serviceavtal.
- Åtkomstmönster eller säkerhetskrav som påverkar slutanvändaren.
- Metoder för datakvarhållning.
- Viktig programprestanda.

Även om en viss arbetsbelastning kan migreras med minimal eller ingen ändring kan verksamheten ändå påverkas. Replikeringsprocesser kan minska prestanda i produktionssystem. Ändringar i miljön som förberedelse för migrering kan orsaka begränsningar för routnings- eller nätverksprestanda. Det finns många ytterligare typer av påverkan som kan bero på aktiviteter för replikering, mellanlagring eller upphöjning.

Regelbundna godkännandeaktiviteter kan hjälpa till att minimera eller undvika överraskningar på grund av förändringar eller prestandadriven verksamhetspåverkan. Molnimplementeringsteamet bör genomföra en process för ändringsgodkännande i slutet av utvärderingsprocessen, innan processen för migrering påbörjas.

## <a name="existing-culture"></a>Befintlig kultur

Dina IT-team har förmodligen befintliga mekanismer för att hantera förändringar som rör dina lokala tillgångar. Dessa mekanismer styrs vanligt vis av traditionella ITIL-baserade (Information Technology Infrastructure Library) processer för ändringshantering. I många företagsmigreringar omfattar dessa processer en ändringsnämnd (CAB, Change Advisory Board) som ansvarar för att granska, dokumentera och godkänna alla IT-relaterade begäranden om ändringar (RFC, Requests For Changes).

CAB:en innehåller vanligtvis experter från flera IT- och affärsteam som erbjuder en mängd olika perspektiv samt detaljerad granskning av alla IT-relaterade ändringar. En CAB-godkännandeprocess är ett beprövat sätt att minska riskerna och minimera affärspåverkan för förändringar som rör stabila arbetsbelastningar som hanteras av IT-avdelningen.

## <a name="technical-approval"></a>Tekniskt godkännande

Organisationens beredskap för godkännande av teknisk förändring är bland de vanligaste orsakerna till misslyckad molnmigrering. Fler projekt stoppas av en serie tekniska godkännanden än problem i molnplattformar. Förberedelse av organisationen för godkännande av tekniska ändringar är ett viktigt krav för att migreringen ska lyckas. Nedan följer viss bästa praxis för att säkerställa att organisationen är redo för tekniskt godkännande.

### <a name="itil-change-advisory-board-challenges"></a>Utmaningar med ITIL-ändringsnämnd

Varje metod för ändringshantering har sin egen uppsättning kontroller och godkännandeprocesser. Migrering är en serie kontinuerliga ändringar som börjar med en hög grad av tvetydighet och utvecklar ytterligare klarhet allt eftersom genomförande fortskrider. Därför styrs migrering bäst med Agile-baserade metoder för ändringshantering, med molnstrategiteamet i rollen som produktägare.

Skalan och frekvensen för ändringar under en molnbaserad migrering passar dock inte särskilt bra för ITIL-processerna. Kraven för ett CAB-godkännande kan äventyra migreringen och sakta ned eller stoppa arbetet. I de tidiga stegen i migreringen är tvetydigheten dessutom hög, och ämnesexpertisen tenderar att vara låg. Under de första migreringarna eller lanseringarna av arbetsbelastningar lär sig ofta molnimplementeringsteamet allt eftersom processen fortskrider. Därför kan det vara svårt för teamet att tillhandahålla de typer av data som krävs för att få CAB-godkännande.

Följande bästa praxis kan hjälpa CAB:en att känna visst förtroende under migreringen utan att bli ett besvärligt hinder.

### <a name="standardize-change"></a>Standardisera förändring

För ett molnimplementeringsteam är det lockande att överväga detaljerade arkitekturbeslut för varje arbetsbelastning som migreras till molnet. Det är lika lockande att använda molnmigrering som en katalysator för att refaktorisera tidigare arkitektoniska beslut. För organisationer som migrerar några hundra virtuella datorer eller några dussin arbetsbelastningar kan endera metoden hanteras korrekt. Vid migrering av 1 000 eller fler tillgångar till ett datacenter anses båda dessa metoder vara ett antimönster med hög risk som avsevärt minskar sannolikheten för ett lyckat resultat. Att ställa av, omforma och återskapa alla program kräver olika kunskaps uppsättningar och en stor mängd olika ändringar, och dessa uppgifter skapar beroenden för mänskliga ansträngningar i stor skala. Var och en av dessa beroenden medför risker för migreringsarbetet.

I artikeln om [rationalisering av digital egendom](../../../digital-estate/rationalize.md) diskuteras flexibiliteten och de tidsbesparande effekterna av grundläggande antaganden vid rationalisering av en digital egendom. Det finns ytterligare en fördel med standardiserad förändring. Genom att välja en standardmetod för rationalisering till att styra migreringsarbetet kan molnrådgivningsstyrelsen eller produktägaren granska och godkänna tillämpningen av en enskild ändring på en lång lista av arbetsbelastningar. Detta minskar det tekniska godkännandet av varje arbetsbelastning till dem som kräver en betydande arkitekturändring för att säkerställa molnkompatibilitet.

### <a name="clarify-expectations-and-roles-of-approvers"></a>Klargöra godkännarnas förväntningar och roller

Innan den första arbetsbelastningen utvärderas bör molnstrategiteamet dokumentera och förmedla förväntningarna till alla som är inblandade i ändringsgodkännandet. Den här enkla aktiviteten kan förhindra kostsamma fördröjningar när molnimplementeringsteamet är fullt sysselsatta.

### <a name="seek-approval-early"></a>Söka godkännande tidigt

När det är möjligt bör tekniska ändringar identifieras och dokumenteras under utvärderingsprocessen. Oavsett godkännandeprocesser bör molnimplementeringsteamet kontakta godkännare i ett tidigt skede. Ju tidigare godkännandeprocessen kan börja, desto mindre troligt är det att en godkännandeprocess hindrar migreringsaktiviteterna.

## <a name="next-steps"></a>Nästa steg

Med hjälp av denna bästa praxis bör det bli lättare att integrera korrekt godkännande med låg risk i migreringsarbetet. När ändringar i arbetsbelastning har godkänts är molnimplementeringsteamet redo att [migrera arbetsbelastningar](../migrate/index.md).

> [!div class="nextstepaction"]
> [Migrera arbetsbelastningar](../migrate/index.md)
