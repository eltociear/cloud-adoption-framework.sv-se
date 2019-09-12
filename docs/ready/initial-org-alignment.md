---
title: Inledande organisatorisk anpassning
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ger en översikt över den inledande organisatoriska anpassningen.
author: alexbuckgit
ms.author: abuck
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: governance
ms.openlocfilehash: a3e819cdd726e3df6edb4cbe0c20a7d652fde152
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70819171"
---
# <a name="initial-organization-alignment"></a>Inledande organisatorisk anpassning

Den **digitala omvandlingen** till molnbaserad databehandling representerar en övergång från lokala installationer till molnet. Denna förändring inkluderar nya sätt att göra affärer – ett exempel är att den digitala omvandlingen lett till att kapitalkostnader förskjutits från programvara och maskinvara för datacenter till utgifter för användning av molnresurser. Så här kommer du igång med [Microsoft Cloud Adoption Framework för Azure](../index.md).

## <a name="the-digital-transformation-process"></a>Den digitala omvandlingsprocessen

För att lyckas med övergången till molnet måste företaget förbereda sin organisation, sin personal och sina processer så att de är förberedda för den digitala omvandlingen. Alla företag har olika organisationsstrukturer vilket gör att det inte finns ett enhetligt sätt att hantera förberedelser för organisationer. Det här dokumentet beskriver de övergripande steg företag kan genomföra för att bli redo. Företaget måste lägga tid på att ta fram en detaljerad plan för att genomföra varje steg.

Den övergripande processen för digital omvandling är:

1. Skapa ett team för molnstrategi. Detta team ansvarar för att leda den digitala omvandlingen. Det är också viktigt att samtidigt skapa ett styrningsteam och ett säkerhetsteam för den digitala omvandlingen.
2. Medlemmar i teamet för molnstrategi går igenom det som är nytt och annorlunda när det gäller molnteknik.
3. Teamet för molnstrategi förbereder företaget genom att skapa affärsfall för digital omvandling – listar alla aktuella brister i affärsstrategi och tar fram övergripande lösningar för att eliminera dem.
4. Anpassa övergripande lösningar till olika affärsgrupper. Identifiera intressenter i varje affärsgrupp som kan ta ägarskap för design och implementering av varje lösning.
5. Anpassa befintliga roller, färdigheter och processer så att de inkluderar molnrelaterade roller, färdigheter och processer.

<!--6. Develop processes for operating in the cloud to make solutions more robust in terms of availability, resiliency, and security.
1. Optimize solutions for performance, scalability, and cost efficiency.-->

## <a name="step-1-create-a-cloud-strategy-team"></a>Steg 1: Skapa ett team för molnstrategi

Det första steget i företagets omvandling är att engagera verksamhetsledare runt om i organisationen för att skapa ett team för molnstrategi (cloud strategy team – CST). Detta team består av verksamhetsledare från ekonomi, IT-infrastruktur och programgrupper. Dessa team kan hjälpa till under molnanalysen och experimenteringsfasen.

Ett team för molnstrategi kan till exempel ledas av IT-chefen och bestå av medlemmar från företagets team för företagsarkitektur, ekonomiavdelningens IT-grupp, seniora tekniker från olika specifika IT-grupper (personalavdelning, ekonomi osv.), och ledare från infrastruktur-, säkerhets- och nätverksteamen.

Det är också viktigt att skapa två andra övergripande team: ett styrningsteam och ett säkerhetsteam. Dessa team ansvarar för att utforma, implementera samt löpande utvärdera företagets styrnings- och säkerhetsprinciper. Styrningsteamets team måste ha medlemmar som arbetat med tillgångsskydd, kostnadshantering, grupprinciper och relaterade ämnen. Säkerhetsteamet måste ha medlemmar som har stor erfarenhet av gällande säkerhetsstandarder samt företagets säkerhetsbehov.

![Team för molnstrategi med styrnings- och säkerhetsteam](../_images/getting-started-overview-1.png)

Styrningsteamet ansvarar för design och implementering av företagets styrningsmodell i molnet, samt för att införa och underhålla de delade infrastrukturtillgångar som är en del av den digitala omvandlingen. Dessa tillgångar omfattar maskinvara, programvara och nödvändiga molnresurser för att ansluta det lokala nätverket till det virtuella nätverket i molnet.

Säkerhetsteamet ansvarar för design och implementering av företagets säkerhetsprinciper för molnet, i nära samarbete med styrningsteamet. Säkerhetsteamet ansvarar för utökningen av säkerhetsgränsen från det lokala nätverket till det virtuella nätverket i molnet. Detta kan ske i form av ägande och underhåll av brandväggarna för inkommande och utgående trafik i det virtuella nätverket i molnet samt verktyg och principer som förhindrar införande av obehöriga resurser.

## <a name="step-2-learn-whats-new-in-the-cloud"></a>Steg 2: Nyheter i molnet

Nästa steg i företagets digitala omvandling är att medlemmarna i teamet för molnstrategi lär sig hur molnteknik kommer att förändra hur företaget arbetar. Detta är förberedelser och planering för de ändringar som kommer att påverka verksamheten, personalen och tekniken. Det är viktigt att medlemmarna i teamet för molnstrategi förstår vad som är nytt och annorlunda i molnet jämfört med i lokala installationer.

![Teamen för molnstrategi, styrning och säkerhet lär sig metodtips för att använda molnet.](../_images/getting-started-overview-2.png)

Startpunkten för att förstå molnet är att lära sig [hur Azure fungerar](../getting-started/what-is-azure.md) övergripande. Sedan behöver de lära sig grunderna för [styrning i Azure](../governance/resource-consistency/what-is-governance.md) för att lägga grunden för att [förstå åtkomsthantering för resurser](../governance/resource-consistency/azure-resource-access.md).

För avancerad information ska styrningsteamet gå igenom guiderna för koncept och design i styrningsavsnittet i innehållsförteckningen. Avsnitten om infrastruktur och arbetsbelastning är användbara för att lära sig om typiska arkitekturer och arbetsbelastningar i molnet.

## <a name="step-3-identify-gaps-in-business-strategy"></a>Steg 3: Identifiera luckor i affärsstrategin

Nästa steg är att teamet för molnstrategi listar de affärsproblem som kräver en lösning som bygger på digital omvandling. Ett företag kan till exempel ha ett befintligt lokalt datacenter med maskinvara som nått slutet på sin livstid och behöver bytas. Ett annat exempel är ett företag som har problem att få ut nya funktioner och tjänster på marknaden tillräckligt snabbt och börjar tappa till konkurrenterna. Dessa luckor representerar _målen_ för företagets digitala omvandling.

Luckor i affärsstrategi kan klassificeras i följande kategorier:

| Category | Beskrivning |
| --- | --- |
| Kostnadshantering | Representerar en lucka i hur företaget betalar för teknik. |
| Styrning | Representerar en lucka i de processer som används av företaget för att skydda tillgångar från obehörig användning som kan leda till högre kostnader, säkerhetsproblem eller problem med efterlevnad. |
| Efterlevnad | Representerar en lucka i hur företaget följer sina egna interna processer och principer samt externa lagar, förordningar och standarder. |
| Säkerhet | Representerar en lucka i hur företaget skyddar sin teknik och datatillgångar från externa hot. |
| Datastyrning | Representerar en lucka i hur företaget hanterar sina data, särskilt kunddata. Den allmänna dataskyddsförordningen (GDPR) i EU har till exempel strikta krav på skydd av kundernas data som kan kräva ny maskin- och programvara. |

När företaget klassificerat alla luckor i affärsstrategin i dessa kategorier är nästa steg att bestämma en högnivålösning för varje problem.

Följande tabell innehåller flera exempel:

|Lucka i affärsstrategin|Kategori &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|Lösning &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|-----|-----|-----|
| Tjänster som är lokalt installerade har problem med tillgänglighet, återhämtning och skalbarhet vid behovstoppar, vilket utgör cirka 10 procent av användningen. Servrar i lokalt datacenter har nått slutet på sin livslängd. Företagets IT-avdelning rekommenderar att köpa nya servrar för lokal installation med specifikationer för att hantera belastningstoppar.| Kostnadshantering | Migrera påverkade lokala arbetsbelastningar till molnet och betala bara för använda resurser. |
| Externa lagar och regelverk som rör datahantering kräver att företaget uppfyller ett antal standardkrav som innebär kryptering av data i vila, vilket kräver ny maskin- och programvara. | Datastyrning | Flytta till Azure storage-tjänsten för kryptering av vilande data. |
| Tjänster i lokala datacenter har drabbats av DDoS-attacker (Distributed Denial of Service) mot offentliga tjänster. Attackerna är svåra att hantera och kräver ny maskinvara, programvara och säkerhetspersonal. | Säkerhet | Migrera tjänsterna till Azure och utnyttja Azure DDoS-skydd.|

När alla luckorna i affärsstrategin har räknats upp och övergripande lösningar tagits fram ska listan ordnas efter prioritet. Listan kan ordnas i prioriteringsordning genom att ställa in luckorna i affärsstrategin med företagets kort- och långsiktiga mål inom varje kategori. Om företaget till exempel har ett kortsiktigt mål att minska IT-utgifterna under de kommande två kvartalen kan luckorna i kategorin *kostnadshantering* prioriteras efter den beräknade kostnadsbesparingen för varje.

Resultatet av denna process är en ordnad lista med övergripande lösningar som är anpassade till verksamhetskategorier.

## <a name="step-4-align-high-level-solutions-with-business-groups-to-design-solutions"></a>Steg 4: Anpassa övergripande lösningar till affärsgrupper för att ta fram lösningar

När nu målen för den digitala omvandlingen listats och ordnats i prioriteringsordning samt övergripande lösningar föreslagits är nästa steg att teamet för molnstrategi tilldelar var och en av de övergripande lösningarna till design- och implementeringsteam i var och en av affärsgrupperna.

Teamen tar listorna och arbetar sig igenom varje övergripande lösning för att utforma varje specifik lösning. Designprocessen inkluderar specificering av ny infrastruktur och nya arbetsbelastningar. Det kan även ske förändringar i rollerna för personer och de processer de följer. Det är också viktigt att i detta läge inkludera både styrningsteamet och säkerhetsteamet för granskning av varje design. Varje design måste ligga inom de principer och procedurer som definierats av styrningsteamet och säkerhetsteamet och dessa team måste vara inkluderade i det slutliga godkännandet för varje design.

![Team för molnstrategi levererar övergripande lösningar till design- och implementeringsteam.](../_images/getting-started-overview-3.png)

Utformningen av varje lösning är inte en enkel uppgift. Allteftersom lösningar utformas måste de utvärderas i sammanhang med andra lösningar som utformas av andra team. Om flera av lösningarna till exempel innebär en migrering av befintliga lokalt installerade program och tjänster till molnet så kan det vara effektivare att samla dessa och utforma en övergripande migreringsstrategi. Ett annat exempel är om det inte är möjligt att migrera vissa befintliga lokalt installerade program och tjänster och lösningen är att ersätta dem med nyutvecklade lösningar eller externa tjänster. I detta fall kan det vara effektivare att samla dessa och utvärdera eventuella överlappningar för att avgöra om en extern tjänst kan användas för mer än en lösning.

När utformningen av en lösning är klar går teamet vidare till implementeringsfasen för varje design. Implementeringsfasen för varje lösning kan hanteras med vanliga projekthanteringsprocesser.

## <a name="step-5-adapt-existing-roles-skills-and-process-for-the-cloud"></a>Steg 5: Anpassa befintliga roller, färdigheter och processer för molnet

Under varje fas i IT-branschens historia markeras de största förändringarna oftast av förändringar i personalroller. Under övergången från stordatorer till klient/server-modellen försvann rollen som datoroperatör i stort sett och ersattes av systemadministratören. När virtualiseringen kom minskade behovet av personer som arbetade med fysiska servrar och ersattes av ett behov av specialister på virtualisering. På samma sätt kommer rollerna antagligen att förändras med övergången till molnbaserad databehandling. Exempelvis kommer datacenterspecialister kanske att ersättas av personal som är specialiserad på ekonomiska analyser av molnanvändning. Även om IT-befattningarna inte har bytt namn, har det dagliga arbetet ändrats avsevärt.

IT-personal kan vara oroliga för sina roller och positioner när de inser att andra kunskaper krävs för support av molnlösningar. Flexibla medarbetare som utforskar och tar till sig nya molntekniker behöver inte vara rädda. De kan leda övergången till molnlösningar och hjälpa organisationen förstå och ta till sig de relaterade förändringarna.

### <a name="capturing-concerns"></a>Fånga upp och hantera oro

Under den digitala omvandlingen ska varje team fånga upp eventuell oro från personalen allteftersom den uppstår. Identifiera följande när farhågor fångas in:

- **Typen av farhåga.** Personal kan till exempel motsätta sig de förändringar i arbetsuppgifter som medföljer den digitala omvandlingen.
- **Farhågornas effekt om de inte hanteras.** Motstånd mot den digitala omvandlingen kan till exempel leda till att personal är långsamma när de utför de nödvändiga förändringarna.
- **Den instans som är bäst lämpad att hantera farhågorna.** Om det till exempel är personal från IT-avdelningen som tvekar när det gäller att ta till sig ny kunskap är det IT-intressenterna som är bäst rustade för att hantera det. Att identifiera den instans som ska hantera farhågorna kan ibland vara svårt och i dessa fall kan du behöva ta upp det med ledningen.

### <a name="identify-gaps"></a>Identifiera luckor

En annan aspekt av att lösa problemen med företagets digitala omvandling är att identifiera **luckor**. En lucka är en roll, kompetens eller process som krävs för den digitala omvandlingen men inte finns inom företaget.

Börja med att lista de nya ansvarsområden som medföljer den digitala omvandlingen, med betoning på nya ansvarsområden och aktuella ansvarsområden som kommer att försvinna. Identifiera det område som hör till varje ansvarsområde. För nya ansvarsområden bestämmer du hur relevanta de är för området. En del ansvarsområden kan täcka flera områden och detta är en möjlighet för bättre anpassning som ska fångas in som en farhåga. I de fall där inget område kan identifieras som ansvarigt ska det fångas in som en lucka.

Identifiera sedan de kunskaper som krävs för ansvarsområdet. Ta reda på om företaget har befintliga resurser med dessa kunskaper. Om inga befintliga resurser finns bestäms vilka utbildningsprogram eller vilket kompetenstillskott som krävs. Bestäm inom vilken tid som ansvarsområdet måste vara bemannat för att den digitala omvandlingen ska hålla tidsplanen.

Identifiera slutligen de roller som ska inneha denna kompetens. En del av den befintliga personalen kommer att överta delar av rollen och i andra fall kan det vara nödvändigt med en helt ny roll.

### <a name="partner-across-teams"></a>Skapa partnerskap mellan team

De kunskaper som krävs för att fylla luckorna i organisationens digitala omvandling kommer normalt inte att vara begränsade till en enskild roll, eller ens en viss avdelning. Kompetenser kommer att ha förhållanden och beroenden som kan sträcka sig över en eller flera roller och dessa roller kan finnas i olika avdelningar. En ägare av en arbetsbelastning kan till exempel behöva att någon i en IT-roll tillhandahåller grundläggande resurser som prenumerationer och resursgrupper.

Dessa beroenden utgör nya processer som organisationen implementerar för att hantera arbetsflödet mellan roller. I exemplet ovan kan flera olika typer av processer stödja förhållandet mellan ägaren av arbetsbelastningen och IT-rollen. Ett verktyg för arbetsflöde kan till exempel skapas för att hantera processen eller så kan en enkel e-postmall användas.

Håll reda på dessa beroenden och dokumentera de processer som kommer att stödja dem samt om processen för tillfället finns eller inte. För processer som kräver framtagning av verktyg säkerställer du att tidslinjen för införandet av verktyg stämmer överens med tidtabellen för den övergripande digitala omvandlingen.

## <a name="next-steps"></a>Nästa steg

Den digitala omvandlingen är en iterativ process där alla team blir effektivare för varje iteration.

> [!div class="nextstepaction"]
> [Förstå hur Azure fungerar](../getting-started/what-is-azure.md)
