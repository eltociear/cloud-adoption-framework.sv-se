---
title: Balansera portföljen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lean för att balansera din moln portfölj.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 2b26f8c763d477d95b21e302158c318e3ab4b101
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548582"
---
# <a name="balance-the-portfolio"></a>Balansera portföljen

Molnimplementering handlar om portföljhantering förklädd som en teknisk implementering. I likhet med portfölj hanterings övningen är det viktigt att balansera portföljen. På strategisk nivå innebär detta att balansera migrering, innovation och experimentering för att få ut det mesta möjliga av molnet. När arbetet med molnimplementering går för långt i en viss riktning ökar komplexiteten i migreringsarbetet. Den här artikeln vägleder läsaren genom metoder för att uppnå balans i portföljen.

## <a name="general-scope-expansion"></a>Allmän omfångsutökning

Det här avsnittet handlar om den strategiska nivån. Därför är den metod som används i den här artikeln lika strategisk. I syfte att förankra strategin i datadrivna beslut förutsätter den här artikeln att läsaren har utvärderat den befintliga [digitala egendomen](../../digital-estate/index.md) (eller håller på att göra detta). Målet med den här metoden är att underlätta utvärdering av arbetsbelastningar för att säkerställa korrekt balans mellan portföljen via kvalitativa frågor och portföljförfining.

### <a name="documenting-business-outcomes"></a>Dokumentera affärsresultat

Innan portföljen balanseras är det viktigt att dokumentera och dela de affärsresultat som driver arbetet med molnmigrering. Några exempel på generella affärsresultat som är relaterade till molnmigreringar finns i [sammanfattningen av molnmigrering](../../getting-started/migrate.md).

Följande tabell kan hjälpa dig att dokumentera och dela önskade affärsresultat. Det är viktigt att notera att de flesta företag arbetar mot flera resultat samtidigt. Vikten av den här övningen är att klargöra de resultat som är närmast relaterade till arbetet med molnmigrering:

|Resultat  |Mätt enligt  |Mål  |Tidsram  |Prioritet för det här arbetet  |
|---------|---------|---------|---------|---------|
|Minska IT-kostnaderna     |Budget för datacenter         |Minska med 2 miljoner dollar         |12 månader         |Nr 1         |
|Datacenterutgång     |Utgång från datacenter         |2 datacenter         |6 månader         |Nr 2         |
|Öka affärsflexibiliteten     |Minska tiden till marknaden  |Minska distributionstiden med sex månader         |2 år         |Nr 3        |
|Förbättra kundupplevelsen     |Kundtillfredsställelse (CSAT)         |10 % förbättring         |12 månader         |Nr 4         |

> [!IMPORTANT]
> Tabellen ovan är ett fiktivt exempel och ska inte användas för att välja prioriteringar. I många fall kan den här tabellen betraktas som ett antimönster genom att kostnadsbesparingar prioriteras högre än kundupplevelser.

Tabellen ovan skulle kunna korrekt representera prioriteringarna i de team för molnstrategi och molnimplementering som övervakar en molnmigrering. På grund av kortsiktiga begränsningar lägger det här teamet starkare betoning på minskning av IT-kostnader och prioriterar en datacenterutgång som ett medel för att uppnå önskade minskningar av IT-kostnader. Genom att dokumentera de konkurrerande prioriteringarna i den här tabellen är det dock möjligt att hjälpa molnstrategiteamet att identifiera möjligheter att bättre anpassa implementeringen av den övergripande portföljstrategin.

### <a name="move-fast-while-maintaining-balance"></a>Flytta snabbt samtidigt som balansen upprätthålls

Vägledningen om [inkrementell rationalisering av den digitala egendomen](../../digital-estate/index.md) föreslår en metod där rationalisering börjar med en obalanserad position. Molnstrategiteamet bör utvärdera alla arbetsbelastningar med avseende på kompatibilitet med en metod för värdbyte. En sådan metod föreslås eftersom den tillåter snabb utvärdering av en komplex digital egendom baserat på kvantitativa data. Ett sådant första antagande gör att molnimplementeringsteamet kan börja arbeta snabbt, vilket minskar tiden till affärsresultat. Enligt vad som anges i den artikeln ger kvalitativa frågor dock den nödvändiga balansen i portföljen. I den här artikeln dokumenteras processen för att skapa den utlovade balansen.

### <a name="importance-of-sunset-and-retire-decisions"></a>Betydelsen av beslut om upphörande och tillbakadragning

Tabellen i avsnittet [Dokumentera affärsresultat](#documenting-business-outcomes) ovan saknar ett viktigt resultat som skulle stödja det främsta målet: att minska IT-kostnader. När minskning av IT-kostnader överhuvudtaget förekommer i listan över affärsresultat är det viktigt att överväga möjligheten med upphörande eller tillbakadragning av arbetsbelastningar. I vissa scenarier kan kostnadsbesparingar komma från att arbetsbelastningar som inte motiverar kortsiktig investering INTE migreras. Vissa kunder har rapporterat kostnadsbesparingar över 20 % av de totala kostnadsminskningarna genom att dra tillbaka underutnyttjade arbetsbelastningar.

För att balansera portföljen, så att den på ett bättre sätt återspeglar beslut om upphörande och tillbakadragning, bör teamen för molnstrategi och molnimplementering ställa följande frågor angående varje arbetsbelastning inom processerna för utvärdering och migrering:

- Har arbetsbelastningen använts av slutanvändare under de senaste sex månaderna?
- Är slutanvändartrafiken konsekvent eller växande?
- Kommer den här arbetsbelastningen att behövas av verksamheten 12 månader från nu?

Om svaret på någon av dessa frågor är ”nej” kan arbetsbelastningen vara en kandidat för tillbakadragning. Om potential för tillbakadragning bekräftas med appägaren är det kanske inte värt det att migrera arbetsbelastningen. Detta leder i sin tur till några kvalificeringsfrågor:

- Kan en plan för tillbakadragning eller upphörande skapas för den här arbetsbelastningen?
- Kan den här arbetsbelastningen dras tillbaka före datacenterutgången?

Om svaret på båda dessa frågor är ”ja” är det klokt att överväga att _inte_ migrera arbetsbelastningen. Den här metoden hjälper till att uppfylla målen med kostnadsbesparingar och datacenterutgång.

Om svaret på endera frågan är ”nej” kan det vara klokt att upprätta en plan för värdhantering av arbetsbelastningen tills den kan dras tillbaka. Den här planen kan omfatta flyttning av tillgångar till ett datacenter med lägre kostnader eller ett alternativt datacenter, vilket även skulle uppfylla målen med kostnadsbesparingar och datacenterutgång.

## <a name="suggested-prerequisites"></a>Föreslagna förutsättningar

De förutsättningar som anges i baslinjeguiden bör fortfarande vara tillräckliga för att behandla det här komplexitetsämnet. Dock bör till gångs lagret och den digitala fastigheten markeras och fetstilas bland dessa krav, eftersom dessa data kommer att driva följande aktiviteter.

## <a name="assess-process-changes"></a>Utvärdera processändringar

Balansering av portföljen kräver ytterligare kvalitativ analys under utvärderingsprocessen, vilket hjälper till att öka enkel rationalisering av portföljen.

### <a name="suggested-action-during-the-assess-process"></a>Föreslagna åtgärder under utvärderingsprocessen

Baserat på data från tabellen i avsnittet [Dokumentera affärsresultat](#documenting-business-outcomes) ovan finns det en sannolik risk för att portföljen inriktar sig för mycket på en migreringsfokuserad genomförandemodell. Om kundupplevelsen vore den främsta prioriteten skulle en innovationsinriktad portfölj vara mer trolig. Ingen av dessa är rätt eller fel, men om fokuset riktas för starkt åt ett håll avtar ofta nyttan, onödig komplexitet införs och genomförandetiden vid arbete med molnimplementering ökar.

För att minska komplexiteten bör läsaren följa en traditionell metod för portföljrationalisering, men i en iterativ modell. Följande steg beskriver en kvalitativ modell för en sådan metod:

- Molnstrategiteamet har en prioriterad lista över kvarvarande uppgifter för arbetsbelastningar som ska migreras.
- Teamen för molnstrategi och molnimplementering håller ett möte om lanseringsplanering före slutförandet av varje lansering.
- I mötet om lanseringsplanering kommer teamen överens om de 5 till 10 främsta arbetsbelastningarna i den prioriterade listan över kvarvarande uppgifter.
- Utanför mötet om lanseringsplanering ställer molnimplementeringsteamet följande frågor till programägarna och ämnesexperterna:
  - Skulle det här programmet kunna ersättas med en PaaS-motsvarighet (Platform as a Service)?
  - Är det här programmet ett program från tredje part?
  - Har budgeten godkänts för investering i pågående utveckling av programmet under de kommande 12 månaderna?
  - Skulle ytterligare utveckling av programmet förbättra kundupplevelsen? Skulle det skapa en konkurrenskraftig differentiering? Skulle det öka verksamhetens intäkter?
  - Kommer data i den här arbetsbelastningen att bidra till senare innovation inom BI, maskininlärning, IoT eller relaterad teknik?
  - Är arbetsbelastningen kompatibel med moderna programplattformar såsom Azure App Service?
- Svaren på ovanstående frågor och annan nödvändig kvalitativ analys påverkar justeringarna av den prioriterade listan över kvarvarande uppgifter. Dessa justeringar kan omfatta följande:
  - Om en arbetsbelastning kan ersättas med en PaaS-lösning kan den tas bort från migreringslistan helt. Åtminstone bör ytterligare undersökning av valet mellan värdbyte och ersättning läggas till som en uppgift, så att den arbetsbelastningens prioritet i migreringslistan minskas tillfälligt.
  - Om det sker (eller bör ske) vidareutveckling av en viss arbetsbelastning kan det vara så att den passar bäst i en modell för refaktorisering/arkitekturomarbetning/återskapande. Eftersom innovation och migrering kräver olika tekniska kunskaper rekommenderas det ofta att program som passar för en metod för refaktorering/arkitekturomarbetning/återskapande hanteras via en lista över kvarvarande uppgifter för innovation snarare än en sådan för migrering.
  - Om en arbetsbelastning ingår i senare innovation kan det vara bäst att refaktorisera dataplattformen men lämna kvar programlagren som en kandidat för värdbyte. Mindre refaktorisering av en arbetsbelastnings dataplattform kan ofta utföras i en lista med kvarvarande uppgifter för migrering eller innovation. Detta rationaliseringsresultat kan leda till mer detaljerade arbetsobjekt i listan med kvarvarande uppgifter, men skulle i övrigt inte ändra några prioriteter.
  - Om en arbetsbelastning inte är strategisk men är kompatibel med moderna, molnbaserade programvärdplattformar kan det vara klokt att utföra mindre refaktorisering av programmet för att distribuera det som en modern app. Detta kan bidra till övergripande besparingar genom att molnmigreringens allmänna krav för IaaS- och operativsystemlicensiering minskas.
  - Om en arbetsbelastning är ett program från tredje part, och den arbetsbelastningens data inte planeras för användning i senare innovation, kan det vara bäst att låta den vara kvar som ett alternativ för värdbyte i listan över kvarvarande uppgifter.

Dessa frågor bör inte utgöra hela den kvalitativa analys som slutförs för varje arbetsbelastning, utan är tänkta att vägleda ett samtal som berör komplexiteten i en obalanserad portfölj.

## <a name="migrate-process-changes"></a>Ändringar i migreringsprocessen

Under migreringen kan aktiviteter för portföljbalansering ha en negativ inverkan på migreringens hastighet (den hastighet med vilken tillgångar migreras). Följande riktlinjer går närmare in på varför och hur arbete bör anpassas så att störningar i migreringsarbetet undviks.

### <a name="suggested-action-during-the-migrate-process"></a>Föreslagna åtgärder under migreringsprocessen

Portföljrationalisering kräver tekniskt arbete av olika slag. Det är lockande för molnimplementeringsteam att matcha den portföljvariationen i migreringsarbetet. Affärsintressenter kan uppmana ett enda molnimplementeringsteam att hantera hela migreringslistan. Detta är sällan en lämplig metod, och i många fall kan den vara direkt kontraproduktiv.

Vi rekommenderar att dessa olika arbeten delas upp bland två eller fler molnimplementeringsteam. Med hjälp av en modell med två team som ett exempel för genomförande är Team 1 migreringsteamet, och Team 2 är innovationsteamet. För större arbeten kan dessa team delas upp ytterligare för att hantera andra metoder såsom ersättning/PaaS eller mindre refaktorisering. Följande beskriver de kunskaper och roller som behövs för metoderna för värdbyte, omstrukturering eller mindre refaktorisering:

**Rehost:** Rehost kräver att grupp medlemmar implementerar ändringar i infrastrukturen. Normalt används ett verktyg såsom Azure Site Recovery för att migrera virtuella datorer eller andra tillgångar till Azure. Detta arbete är väl lämpat för datacenteradministratörer eller IT-implementatörer. Molnmigreringsteamet har en lämplig struktur för att leverera detta arbete i stor skala. Det här är den snabbaste metoden för att migrera befintliga tillgångar i de flesta scenarier.

**Återfaktum:** Du måste ha grupp medlemmar för att kunna ändra käll koden, ändra arkitekturen för ett program eller införa nya moln tjänster. För sådant arbete används oftast utvecklingsverktyg såsom Visual Studio och distributionspipelineverktyg som Azure DevOps för att omdistribuera moderniserade program till Azure. Detta arbete är väl lämpat för programutvecklingsroller eller DevOps-pipelineutvecklingsroller. Molninnovationsteamet har den bästa strukturen för att leverera detta arbete. Det kan ta längre tid att ersätta befintliga tillgångar med molntillgångar via den här metoden, men apparna kan dra nytta av molnspecifika funktioner.

**Mindre omfabriker:** Vissa program kan förvaras med mindre omfaktor på data-eller program nivå. Detta arbete kräver att teammedlemmar distribuerar data till molnbaserade dataplattformar eller gör mindre konfigurationsändringar i programmet. Detta kan kräva visst stöd från ämnesexperter inom data- eller programutveckling. Detta arbete liknar dock det arbete som utförs av IT-implementatörer vid distribution av appar från tredje part. Detta arbete kan enkelt anpassas till teamet för molnmigrering eller molnstrategi. Detta arbete är inte alls lika snabbt som en migrering med värdbyte, men det tar ändå mindre tid att genomföra än arbete med refaktorisering.

Under migreringen rekommenderas det att arbetet delas upp på de tre sätt som beskrivs ovan samt att detta arbetet utförs av rätt team i rätt iteration. Även om det rekommenderas att portföljen diversifieras är det även lämpligt att hålla arbetet mycket fokuserat och uppdelat.

## <a name="optimize-and-promote-process-changes"></a>Optimera och höja upp processändringar

Inga ytterligare ändringar krävs i processerna för optimering och upphöjning under migreringsarbetet.

## <a name="secure-and-manage-process-changes"></a>Skydda och hantera processändringar

Inga ytterligare ändringar krävs i processerna för skydd och hantering under migreringsarbetet.

## <a name="next-steps"></a>Nästa steg

Gå tillbaka till [checklistan för utökat omfång](./index.md) och se till att din migreringsmetod är helt anpassad till kraven.

> [!div class="nextstepaction"]
> [Utökad checklista](./index.md)
