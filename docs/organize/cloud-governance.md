---
title: Funktioner för moln styrning
description: Använd ramverket för moln införande för Azure för att lära dig hur moln styrnings funktioner ser till att risker och risk tolerans utvärderas och hanteras korrekt.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 7569d0718f7b25625cc40887af81edda53ff0b1e
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79093891"
---
# <a name="cloud-governance-capabilities"></a>Funktioner för moln styrning

Alla typer av ändringar genererar nya risker. Moln styrnings funktioner säkerställer att risker och risk tolerans utvärderas och hanteras korrekt. Den här funktionen säkerställer rätt identifiering av risker som inte kan tolereras av verksamheten. De personer som tillhandahåller den här funktionen kan sedan omvandla risker till företags principer. Principer för styrning utförs sedan genom definierade ämnes områden som körs av personal medlemmar som tillhandahåller funktioner för moln styrning.

## <a name="possible-sources-for-this-capability"></a>Möjliga källor för den här funktionen

Beroende på de önskade affärs behoven kan de kunskaper som krävs för att tillhandahålla fullständiga funktioner för moln styrning tillhandahållas av:

- IT-styrning
- Företags arkitektur
- Säkerhet
- IT-åtgärder
- IT-infrastruktur
- Nätverk
- Identitet
- Virtualisering
- Affärskontinuitet och haveriberedskap
- Program ägare i det
- Ekonomi ägare

Moln styrnings funktionen identifierar risker relaterade till aktuella och framtida versioner. Den här funktionen visas i ansträngningarna att utvärdera risker, förstå de potentiella konsekvenserna och fatta beslut om risk tolerans. I detta syfte kan planer snabbt uppdateras för att avspegla de föränderliga behoven i [moln implementerings funktionen](./cloud-adoption.md).

## <a name="key-responsibilities"></a>Viktiga ansvars områden

Den primära avgiften för en moln styrnings funktion är att balansera konkurrerande krafter för omvandling och risk minskning. Dessutom säkerställer moln styrning att [moln implementeringen](./cloud-adoption.md) är medveten om rikt linjer för data-och till gångs klassificering och arkitektur som styr alla införande metoder. Teamet kommer också att arbeta med [moln Center](./cloud-center-of-excellence.md) med möjlighet att använda automatiska metoder för att hantera moln miljöer.

Dessa uppgifter utförs vanligt vis av moln styrnings funktionen varje månad.

**Tidiga planerings aktiviteter:**

- Förstå [affärs risker](../govern/policy-compliance/risk-tolerance.md) som införs av planen
- Representera [affärs toleransen för risk](../govern/policy-compliance/risk-tolerance.md)
- Stöd för att skapa en [styrnings MVP](../govern/guides/index.md)

**Pågående månads aktiviteter:**

- Förstå [affärs risker](../govern/policy-compliance/risk-tolerance.md) som introduceras under varje version
- Representera [affärs toleransen för risk](../govern/policy-compliance/risk-tolerance.md)
- Stöd i den stegvisa förbättringen av [princip-och efterlevnads kraven](../govern/policy-compliance/index.md)

## <a name="meeting-cadence"></a>Mötes takt

Moln styrnings funktioner levereras vanligt vis av ett arbets team. Tids åtagandet från varje grupp medlem utgör en stor del av deras dagliga scheman. Bidragen är inte begränsade till möten och feedback-cykler.

## <a name="additional-participants"></a>Ytterligare deltagare

Följande representerar deltagare som ofta kommer att delta i moln styrnings aktiviteter:

- Ledare från mellan hantering och direkt deltagare i viktiga roller som har utsetts att representera verksamheten kommer att hjälpa till att utvärdera risk toleranser.
- Moln styrnings funktionerna levereras av en utökning av [moln strategi funktionen](./cloud-strategy.md). Precis som CIO och affärsmässiga förväntas delta i moln strategins kapacitet förväntas deras direkt rapporter delta i moln styrnings aktiviteter.
- Företags anställda som är medlemmar i affär senheten som arbetar nära affärs ledningen bör fatta beslut om företags-och teknik risker.
- Information Technology (IT) och information Security (är) anställda som förstår de tekniska aspekterna av moln omvandlingen kan tjäna i en roterande kapacitet i stället för att vara en konsekvent leverantör av funktioner för moln styrning.

## <a name="maturation-of-cloud-governance-capability"></a>Lagring av moln styrnings funktioner

Vissa stora organisationer har befintliga, dedikerade team som fokuserar på IT-styrning. Dessa team specialiserar sig på risk hantering i IT-portföljen. När dessa team finns kan följande förfallo modeller accelereras snabbt. IT-styrningen uppmuntras dock att granska moln styrnings modellen för att förstå hur styrningen växlar något i molnet. Viktiga artiklar är [att utöka företags policyn till molnet](../govern/corporate-policy.md) och de [fem disciplinerna i moln styrning](../govern/governance-disciplines.md).

**Ingen styrning:** Det är vanligt för organisationer att gå över till molnet utan att klara planer för styrning. Före lång tid gäller säkerhet, kostnad, skalning och åtgärder för att utlösa konversationer om behovet av en styrnings modell och personer att bemanna de processer som är kopplade till den modellen. Att starta dessa konversationer innan de börjar gälla är alltid ett lämpligt första steg för att lösa antimönstret "ingen styrning". Avsnittet om hur du [definierar företags principer](../govern/corporate-policy.md) kan hjälpa dem att under lätta dessa konversationer.

**Styrning blockerad:** När det gäller säkerhets-, kostnads-, skalnings-och drifts åtgärder som inte har svarat, kan projekt och affärs mål bli blockerade. Brist på rätt styrning genererar en frukt, osäkerhet och tvivel mellan intressenter och tekniker. Stoppa detta i dess spår genom att vidta åtgärder tidigt. De två styrnings guiderna som definierats i moln implementerings ramverket kan hjälpa dig att starta små, ange regler för att begränsa antalet osäkerheter och vuxen styrning över tid. Välj från den [komplexa Enterprise-guiden](../govern/guides/complex/index.md) eller [standard Enterprise-guiden](../govern/guides/standard/index.md).

**Frivillig styrning:** Det tenderar att Brave Souls i alla företag. Dessa Gallant få vem som är villiga att gå in och hjälpa teamet att lära sig av misstag. Detta är ofta hur styrning startar, särskilt i mindre företag. Dessa Brave soulsr i ideell tid för att åtgärda vissa problem och skicka moln användnings team till en konsekvent och välhanterad uppsättning bästa praxis.

De här individernas ansträngningar är mycket bättre än scenarier med "ingen styrning" eller "styrning blockerade". När deras ansträngningar skulle vara Commended bör den här metoden inte förväxlas med styrning. Lämplig styrning kräver mer än sporadisk support för att öka konsekvensen, vilket är målet för alla goda styrnings metoder. Rikt linjerna i de [fem disciplinerna i moln styrning](../govern/governance-disciplines.md) kan hjälpa dig att utveckla denna disciplin.

**Cloud Övervakare:** Den här monikern har blivit en skylt för många moln arkitekter som specialiserar sig på styrning av tidiga steg. När styrnings metoder först börjar ut ser resultatet ut ungefär som för styrning frivilliga. Det finns dock en avgörande skillnad. En moln övervakare har en plan i åtanke. I det här skedet är det dags att rensa upp de röriga arkitekter som gjorts av de moln arkitekter som var före. Molnet övervakare anpassar dock denna ansträngning till en väl strukturerad [företags policy](../govern/corporate-policy.md). De använder också verktyg för styrnings automatisering, som de som beskrivs i [styrnings MVP](../govern/guides/complex/index.md): t.

En annan grundläggande skillnad mellan en moln övervakare och en styrning ideella är ledarskaps support. Den ideella tiden är extra timmar över vanliga förväntningar på grund av deras fråge-och-verksamhet. Cloud övervakare får support från ledarskap för att minska sina dagliga uppgifter för att se till att regelbunden tilldelning av tid kan investeras i att förbättra moln styrningen.

**Moln skydd:** Som styrnings metoder som stärka och som godkänns av moln implementerings team, är rollen för moln arkitekter som specialiserar sig på styrning en bit, precis som rollen i moln styrnings teamet. I allmänhet får de mer mogna metoderna uppmärksamhet för andra ämnes experter som kan hjälpa till att förstärka de skydd som tillhandahålls av styrnings implementeringar.

Skillnaden är diskret, men det är en viktig skillnad när du skapar en styrning – fokuserad IT-kultur. En moln övervakare rensar upp de problem som gjorts av innovativa moln arkitekter och de två rollerna har naturliga friktion och motsatta mål. En moln skyddare hjälper till att hålla molnet säkert så att andra moln arkitekter kan förflytta sig snabbare med färre röriga.

Moln skydd börjar använda mer avancerade styrnings metoder för att påskynda plattforms distributionen och hjälpa team att själv underhålla sina miljö behov, så att de kan gå snabbare. Exempel på dessa mer avancerade funktioner finns i de stegvisa förbättringarna av styrnings-MVP: t, till exempel [förbättring av säkerhets bas linjen](../govern/guides/complex/security-baseline-improvement.md).

**Moln acceleratorer:** Moln skydd och moln förmyndare komponenter naturlig skördad skript och automatiseringar som påskyndar distributionen av miljöer, plattformar eller till och med komponenter i olika program. Att granska och dela dessa skript förutom centraliserade styrnings ansvars områden utvecklar en hög grad av respekt för dessa arkitekter inom IT.

De som arbetar med att dela med sig av sina granskade skript hjälper till att leverera teknik projekt snabbare och inbäddad styrning i arbets Belastningens arkitektur. Den här arbets belastnings påverkan och stöd för väldesignade mönster ökar moln acceleratorerna till en högre rangordning av styrnings specialisten.

**Global styrning:** När organisationer är beroende av globalt spridda IT-behov kan det finnas betydande avvikelser i drift och styrning i olika geografiska områden. Krav för affär senheter och till och med lokal data suveränitet kan orsaka styrning av bästa praxis för att störa de åtgärder som krävs. I de här scenarierna möjliggör en nivåAD styrnings modell minimal konsekvens och lokaliserad styrning. Artikeln om [flera olika lager styrning](../govern/guides/complex/multiple-layers-of-governance.md) ger mer insikter om att nå den här förfallo nivån.

Alla företag är unika, och därför är deras styrnings behov. Välj den utgångs nivå som passar din organisation och Använd ramverket för moln införande för att vägleda de metoder, processer och verktyg som hjälper dig att komma dit.

## <a name="next-steps"></a>Nästa steg

I takt med att moln styrningen är vuxen kommer team att kunna utnyttja molnet i någonsin snabbare. Fortsatta moln införande tenderar att utlösa förfallo tid i IT-driften. Denna mognad kan också kräva utveckling av [moln drifts funktioner](./cloud-operations.md).

> [!div class="nextstepaction"]
> [Utveckla moln drifts funktioner](./cloud-operations.md)
