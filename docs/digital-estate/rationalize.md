---
title: Rationalisera den digitala egendomen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Utvärdera dina digitala till gångar och ta reda på hur det är bäst att vara värd för dem i molnet.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: governance
ms.openlocfilehash: 5cee6318edd04e219b33bce6b72a78c7aa21ba4f
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023423"
---
# <a name="rationalize-the-digital-estate"></a>Rationalisera den digitala egendomen

Cloud rationalisering är en process för att utvärdera till gångar för att fastställa den bästa metoden för att vara värd för dem i molnet. När du har fastställt en [metod](./approach.md) och sammanställt en [inventering](./inventory.md)kan moln rationalisering börja. [Cloud rationalisering](./rationalize.md) diskuterar de vanligaste rationalisering-alternativen.

## <a name="traditional-view-of-rationalization"></a>Traditionell vy av rationalisering

Det är enkelt att förstå rationalisering när du visualiserar den traditionella processen för rationalisering som ett komplext besluts träd. Varje till gång i den digitala fastigheten matas genom en process som resulterar i en av fem svar (den fem RS). För små fastigheter fungerar den här processen bra. För större fastigheter är det ineffektivt och kan leda till betydande fördröjningar. Vi går igenom processen för att se varför. Sedan kommer vi att presentera en mer effektiv modell.

**Hantering** En grundlig inventering av till gångar, inklusive program, program vara, maskin vara, operativ system och system prestanda mått, krävs för att slutföra en fullständig rationalisering med hjälp av traditionella modeller.

**Kvantitativ analys:** I besluts trädet driver kvantitativa frågor det första lagret med beslut. Vanliga frågor innehåller följande: Används den till gång som används idag? I så fall, är den optimerad och storlek korrekt? Vilka beroenden finns mellan till gångar? Dessa frågor är viktiga för klassificeringen av inventeringen.

**Kvalitativ analys:** Nästa uppsättning beslut kräver mänsklig intelligens i form av kvalitativ analys. Ofta är frågorna som finns här unika för lösningen och kan bara besvaras av affärs intressenter och privilegierade användare. Dessa beslut är vanligt vis försenade processen och saktar ned saker avsevärt. Den här analysen förbrukar vanligt vis 40 till 80 HELTIDs timmar per program.

Information om hur du skapar en lista med kvalitativa analys frågor finns i avsnittet [metoder för planering av digital auktion](./approach.md).

**Rationalisering-beslut:** I ett erfaret rationalisering-team skapar de kvalitativa och kvantitativa data tydliga beslut. Tyvärr är team som har en hög grad av rationalisering-upplevelse dyra att anställa eller ta några månader att träna.

## <a name="rationalization-at-enterprise-scale"></a>Rationalisering i företags skala

Om den här ansträngningen är tids krävande och avskräckande för 50 en digital VM-datafastighet, kan du föreställa dig den ansträngning som krävs för att driva affärs omvandlingen i en miljö med tusentals virtuella datorer och hundratals program. Den mänskliga ansträngningen kan vara lätt än 1 500 HELTIDs timmar och nio månaders planering.

Medan fullständig rationalisering är slut tillstånd och en bra riktning för att flytta i, ger den sällan en hög ROI (avkastning på investeringen) i förhållande till den tid och energi som krävs.

När rationalisering är viktigt för finansiella beslut är det värt att fundera över en organisation som specialiserar sig på en professionell tjänste organisation som specialiserar sig på molnet rationalisering. Dessutom kan hela rationalisering vara en kostsam och tids krävande ansträngning som fördröjer transformerings-eller affärs resultat.

Resten av den här artikeln beskriver en alternativ metod, som kallas stegvisa rationalisering.

## <a name="incremental-rationalization"></a>Stegvis rationalisering

Den fullständiga rationalisering av en stor digital egendom är känslig för risker och kan drabbas av fördröjningar på grund av dess komplexitet. Antaganden bakom den stegvisa metoden är att fördröjda beslut ökar belastningen på verksamheten för att minska risken för hindren. Med tiden skapar den här metoden en ekologisk modell för utveckling av de processer och den erfarenhet som krävs för att göra kvalificerade rationalisering-beslut mer effektivt.

### <a name="inventory-reduce-discovery-data-points"></a>Hantering Minska identifierings data punkter

Några organisationer investerar tid, energi och kostnader för att upprätthålla en korrekt, real tids inventering av den fullständiga digitala fastigheten. Förlust, stöld, uppdaterings cykler och medarbetarprogram ofta motiverar detaljerad till gångs spårning av slut användar enheter. RÄNTABILITETen att underhålla en korrekt Server-och program inventering i ett traditionellt, lokalt Data Center är ofta låg. De flesta IT-organisationer har andra fler problem med att trycka på och spåra användningen av fasta till gångar i ett Data Center.

I en moln omvandling korrelerar lagret direkt med drifts kostnaderna. Korrekt inventerings information krävs för korrekt planering. De nuvarande alternativen för miljö genomsökning kan tyvärr fördröja beslut efter veckor eller månader. Lyckligt vis kan några trick påskynda data insamlingen.

Agent-baserad genomsökning är den mest citerade fördröjningen. De robusta data som krävs för en traditionell rationalisering kan ofta bara samlas in med en agent som körs på varje till gång. Det här beroendet av agenter saktar ner sig ofta, eftersom det kan kräva feedback från funktioner för säkerhet, åtgärder och administration.

I en stegvis rationalisering-process kan en agent lös lösning användas för en inledande identifiering för att påskynda tidiga beslut. Beroende på komplexitets nivån i miljön kan en agent-baserad lösning fortfarande krävas. Men det kan tas bort från den kritiska vägen till företags förändringar.

### <a name="quantitative-analysis-streamline-decisions"></a>Kvantitativ analys: Effektivisera beslut

Oavsett vilken metod som används för inventerings identifieringen kan kvantitativ analys driva inledande beslut och antaganden. Detta gäller särskilt när du försöker identifiera den första arbets belastningen eller när målet för rationalisering är en kostnads jämförelse på hög nivå. I en stegvis rationalisering process begränsar moln strategi teamet och moln implementerings teamen [fem RS-rationalisering](./5-rs-of-rationalization.md) till två kortfattade beslut och tillämpar bara dessa kvantitativa faktorer. Detta effektiviserar analysen och minskar mängden inledande data som krävs för att ändra på enheten.

Om en organisation till exempel är i pågående för en IaaS-migrering till molnet kan du anta att de flesta arbets belastningar antingen dras tillbaka eller reageras.

### <a name="qualitative-analysis-temporary-assumptions"></a>Kvalitativ analys: Tillfälliga antaganden

Genom att minska antalet möjliga resultat är det enklare att komma fram till ett första beslut om en till gångs framtida tillstånd. När du minskar alternativen minskar du också antalet frågor som ställts i företaget i det här skedet.

Om till exempel alternativen är begränsade till att vara värd för eller tas ur bruk, behöver företaget bara besvara en fråga under den första rationalisering, vilket är om du vill dra tillbaka till gången.

"Analysen föreslår att inga användare använder den här till gången aktivt. Är det korrekt eller har vi överblickat något? " Sådan binär fråga är vanligt vis mycket enklare att köra genom kvalitativ analys.

Den här effektiviserade metoden skapar bas linjer, ekonomiska planer, strategi och riktning. I senare aktiviteter går varje till gång genom ytterligare rationalisering och kvalitativ analys för att utvärdera andra alternativ. Alla antaganden som du gör i den här inledande rationalisering testas innan

## <a name="challenge-assumptions"></a>Utmanings antaganden

Resultatet av det föregående avsnittet är en grov rationalisering som är fullständig för antaganden. Nu är det dags att utmana några av dessa antaganden.

### <a name="retire-assets"></a>Dra tillbaka till gångar

I en traditionell lokal miljö är värd för små, oanvända till gångar sällan en betydande inverkan på årliga kostnader. Med några få undantag kan du använda en HELTIDs insats som krävs för att analysera och dra tillbaka den faktiska till gången och på så sätt dra tillbaka kostnads besparingarna från att rensa och ta bort dessa till gångar.

Men när du flyttar till en moln redovisnings modell kan du ta bort till gångar för att få betydande besparingar i årliga drifts kostnader och åtgärder för att flytta fram och tillbaka.

Det är inte ovanligt att organisationerna drar tillbaka 20% eller mer av sin digitala egendom när en kvantitativ analys har slutförts. Vi rekommenderar att du utför ytterligare kvalitativ analys innan du bestämmer dig för en sådan åtgärd. När den har bekräftats kan indragningen av dessa till gångar producera den första ROI-Victory i moln migreringen. I många fall är detta en av de största kostnads besparingarna. Därför rekommenderar vi att moln strategi teamet övervakar valideringen och pensionering av till gångar, parallellt med build-fasen av migreringsprocessen, för att möjliggöra en tidig ekonomisk vinst.

### <a name="program-adjustments"></a>Program justeringar

Ett företag sig sällan vid bara en omvandlings resa. Valet mellan kostnads minskning, marknads tillväxt och nya intäkts strömmar är sällan ett binära beslut. Därför rekommenderar vi att moln strategi teamet arbetar med den för att identifiera till gångar med parallella omvandlings ansträngningar som ligger utanför omfånget för den primära omvandlings resan.

I exemplet på IaaS-migrering som du fick i den här artikeln:

- Be DevOps-teamet om att identifiera till gångar som redan ingår i en distributions automatisering och ta bort dessa till gångar från kärn migrerings planen.

- Be data-och R-& D-teamen att identifiera till gångar som driver nya intäkts strömmar och ta bort dem från den grundläggande migrations planen.

Det här programmet – fokuserad kvalitativ analys kan utföras snabbt och skapa en justering över flera olika migreringar av migreringen.

Du kanske fortfarande måste ta hänsyn till vissa till gångar som att vara värd åt till gångar en stund. Du kan stega i senare rationalisering efter den första migreringen.

## <a name="select-the-first-workload"></a>Välj den första arbets belastningen

Implementering av den första arbets belastningen är nyckeln till testning och inlärning. Det är den första möjligheten att demonstrera och bygga en tillväxt tänkesätt.

### <a name="business-criteria"></a>Affärs kriterier

För att garantera affärs genomskinlighet, identifiera en arbets belastning som stöds av en medlem i moln strategi teamets affär senhet. Välj helst en i vilken teamet har fått en fördelad spel och ett starkt motivation att flytta till molnet.

### <a name="technical-criteria"></a>Tekniska kriterier

Välj en arbets belastning som har minsta beroenden och som kan flyttas som en liten grupp av till gångar. Vi rekommenderar att du väljer en arbets belastning med en definierad test Sök väg för att göra valideringen enklare.

Den första arbets belastningen distribueras ofta i en experimentell miljö utan drift-eller styrnings kapacitet. Det är viktigt att välja en arbets belastning som inte interagerar med säkra data.

### <a name="qualitative-analysis"></a>Kvalitativ analys

Moln implementerings teamen och moln strategi teamet kan samar beta för att analysera den här lilla arbets belastningen. Det här samarbetet skapar en kontrollerad möjlighet att skapa och testa kvalitativa analys villkor. Den mindre populationen skapar en möjlighet att undersöka de berörda användarna och att slutföra en detaljerad kvalitativ analys på en vecka eller mindre. Vanliga kvalitativa analys faktorer finns i det specifika rationalisering-målet i [5 RS-rationalisering](./5-rs-of-rationalization.md).

### <a name="migration"></a>Migrering

Parallellt med fortsatt rationalisering kan moln implementerings teamet börja migrera den små arbets belastningen för att utöka inlärningen i följande viktiga områden:

- Förbättra färdigheterna med moln leverantörens plattform.
- Definiera de kärn tjänster (och Azure-standarder) som behövs för att passa den långsiktiga visionen.
- Bättre förståelse för hur åtgärder kan behöva ändras senare i omvandlingen.
- Förstå eventuella affärs risker och affärs tolerans för dessa risker.
- Upprätta en bas linje eller en minimal livskraftig produkt (MVP) för styrning baserat på affärs risk tolerans.

## <a name="release-planning"></a>Versions planering

Även om moln implementerings teamet kör migreringen eller implementeringen av den första arbets belastningen kan moln strategi teamet börja prioritera återstående program och arbets belastningar.

### <a name="power-of-10"></a>Kraft på 10

Den traditionella metoden för rationalisering försöker möta alla förutsebara behov. Lyckligt vis krävs det ofta en plan för varje program för att starta en omvandlings resa. I en stegvis modell är kraften hos 10 en lämplig start punkt. I den här modellen väljer moln strategi teamet de första 10 program som ska migreras. De tio arbets belastningarna bör innehålla en blandning av enkla och komplexa arbets belastningar.

### <a name="build-the-first-backlogs"></a>Bygg de första-loggfilerna

Moln implementerings teamen och moln strategi teamet kan arbeta tillsammans med den kvalitativa analysen för de första 10 arbets belastningarna. Den här ansträngningen skapar den första prioriterade migreringen efter släpning och den första prioriterade versionen efter släpning. Den här metoden gör det möjligt för team att iterera på metoden och ger tillräckligt med tid för att skapa en lämplig process för kvalitativ analys.

### <a name="mature-the-process"></a>Mogna processen

När de två teamen har samtycker till kriterierna för kvalitativa analyser kan utvärderingen bli en uppgift inom varje iteration. Att nå enighet om bedömnings kriterier kräver vanligt vis två till tre versioner.

När utvärderingen har flyttats till den stegvisa körningen av migreringen kan moln implementerings gruppen iterera snabbare om utvärdering och arkitektur. I det här skedet är moln strategi teamet också sammankopplat, vilket minskar tömningen vid deras slut tid. Detta gör det också möjligt för moln strategi teamet att fokusera på att prioritera de program som ännu inte finns i en speciell version, vilket säkerställer en strikt anpassning av marknads villkoren.

Alla prioriterade program är inte redo för migrering. Sekvenseringen kan komma att ändras eftersom teamet gör djupare kvalitativ analys och identifierar affärs händelser och beroenden som kan göra en omprioritering av efter släpning. Vissa versioner kan gruppera ett litet antal arbets belastningar. Andra kanske bara innehåller en enda arbets belastning.

Moln implementerings teamet kör förmodligen iterationer som inte genererar en fullständig migrering av arbets belastning. Ju mindre arbets belastning, och färre beroenden, är det mer sannolikt att arbets belastningen får plats i en enda Sprint eller iteration. Av den anledningen rekommenderar vi att de första programmen i friutgåvan blir små och innehåller få externa beroenden.

## <a name="end-state"></a>Slut tillstånd

Med tiden kommer kombinationen av moln antagande teamet och moln strategi teamet att slutföra en fullständig rationalisering av inventeringen. Den här stegvisa metoden gör det möjligt för teamen att fort löp ande gå fortare i rationalisering-processen. Det hjälper också omvandlings resan att ge upphov till konkreta affärs resultat som tidigare, utan lika mycket drifts analys arbete.

I vissa fall kan den finansiella modellen vara för nära att fatta ett beslut utan ytterligare rationalisering. I sådana fall kan du behöva en mer traditionell metod för rationalisering.

## <a name="next-steps"></a>Nästa steg

Resultatet av en rationalisering-ansträngning är en prioriterad efter släpning av alla till gångar som påverkas av den valda omvandlingen. Den här efter släpning är nu redo att användas som grund för kostnadsbaserade modeller av moln tjänster.

> [!div class="nextstepaction"]
> [Justera kostnads modeller med den digitala fastigheten](./calculate.md)
