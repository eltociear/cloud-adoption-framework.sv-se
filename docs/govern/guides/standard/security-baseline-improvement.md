---
title: 'Standard företags styrning: förbättra disciplinen för säkerhets bas linjer'
description: Använd ramverket för moln införande för Azure för att lära dig mer om att lägga till säkerhets kontroller som stöder flytt av skyddade data till molnet.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: f34938fc6690949d017ee538c444a4ccef389aef
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80357020"
---
# <a name="standard-enterprise-governance-guide-improve-the-security-baseline-discipline"></a>Standard styrnings guide för företag: förbättra disciplinen för säkerhets bas linjer

Den här artikeln går vidare genom att lägga till säkerhets kontroller som stöder flytt av skyddade data till molnet.

## <a name="advancing-the-narrative"></a>Med den här berättelsenn

IT-avdelningen och affärs ledningen har varit nöjd med resultatet från experimentering av tidiga steg av IT, app Development och BI Teams. För att kunna realisera konkreta affärs värden från dessa experiment måste dessa grupper kunna integrera skyddade data i lösningar. Detta utlöser ändringar i företags principen, men kräver även en stegvis förbättring av moln styrnings implementeringar innan skyddade data kan landa i molnet.

### <a name="changes-to-the-cloud-governance-team"></a>Ändringar i moln styrnings teamet

Till följd av den föränderliga bevaran och den support som tillhandahölls hittills, visas nu moln styrnings teamet på olika sätt. De två system administratörer som startade teamet visas nu som erfarna moln arkitekter. I takt med att det här är en uppfattning kommer de att växla från att bli moln förmyndare komponenter till mer av en roll för moln skydd.

Skillnaden är diskret, men det är en viktig skillnad när du skapar en styrning – fokuserad IT-kultur. En moln övervakare rensar upp de röriga som gjorts av innovativa moln arkitekter. De två rollerna har naturlig friktion och motsatta mål. Å andra sidan hjälper moln skydd att hålla molnet säkert, så att andra moln arkitekter kan förflytta sig snabbare, med mindre röriga. Dessutom ingår en moln skydds funktion för att skapa mallar som påskyndar distribution och införande, vilket gör dem till en innovation-Accelerator samt en Defender av de fem disciplinerna i moln styrning.

### <a name="changes-in-the-current-state"></a>Ändringar i det aktuella läget

I början av den här delen fungerade program utvecklings teamen fortfarande i en utveckling/test-kapacitet och BI-teamet befann sig fortfarande i experiment fasen. DEN drivs av två värdbaserade infrastruktur miljöer, med namnet Prod och DR.

Sedan dess har vissa saker ändrats som påverkar styrning:

- Program utvecklings teamet har implementerat en CI/CD-pipeline för att distribuera ett internt program i molnet med en bättre användar upplevelse. Appen har ännu inte interagerat med skyddade data, så det är inte produktions klart.
- Business Intelligence-teamet i IT kan aktivt granska data i molnet från logistik, inventering och tredje parts källor. Dessa data används för att driva nya förutsägelser, vilket kan forma affärs processer. Dessa förutsägelser och insikter är dock inte åtgärdade förrän kund-och finans data kan integreras i data plattformen.
- IT-teamet fortlöper i informations chefen och ekonomi chefen för att dra tillbaka DR-datacenter. Mer än 1 000 av 2 000-till gångarna i DR-datacenter har dragits tillbaka eller migrerats.
- De lösta definierade principerna angående person uppgifter och ekonomiska data har förberetts. De nya företags principerna är dock knutna till implementeringen av relaterade säkerhets-och styrnings principer. Team har fortfarande stoppats.

### <a name="incrementally-improve-the-future-state"></a>Förbättra framtida tillstånd stegvis

Tidiga experiment från App dev och BI Teams visar potentiella förbättringar av kund upplevelser och data drivna beslut. Båda teamen vill utöka implementeringen av molnet under de kommande 18 månaderna genom att distribuera dessa lösningar till produktion.

Under de återstående sex månaderna kommer moln styrnings teamet att implementera säkerhets-och styrnings krav för att tillåta moln implementerings team att migrera skyddade data i dessa data Center.

Ändringarna av aktuell och framtida status ger nya risker som kräver nya princip satser.

## <a name="changes-in-tangible-risks"></a>Förändringar i materiella risker

**Data intrång:** När du implementerar en ny data plattform, finns det en sammanhängande ökning av skulder relaterade till potentiella data intrång. Tekniker som inför moln teknologier har ökat ansvar för att implementera lösningar som kan minska risken. En robust säkerhets-och styrnings strategi måste implementeras för att säkerställa att dessa tekniker uppfyller dessa ansvars områden.

Den här affärs risken kan utökas till några tekniska risker:

1. Verksamhets kritiska program eller skyddade data kan distribueras oavsiktligt.
2. Skyddade data kan exponeras under lagringen på grund av dåliga krypterings beslut.
3. Obehöriga användare kan komma åt skyddade data.
4. Externt intrång kan leda till åtkomst till skyddade data.
5. Externt intrång eller denial of Service-attacker kan orsaka affärs avbrott.
6. Ändringar i organisationen eller sysselsättningen kan tillåta obehörig åtkomst till skyddade data.
7. Nya sårbarheter kan skapa nya intrångs-eller åtkomst möjligheter.
8. Inkonsekventa distributions processer kan leda till säkerhets luckor, vilket kan leda till data läckor eller avbrott.
9. Konfigurations luckor eller missade korrigeringar kan leda till oönskade säkerhets luckor, vilket kan leda till data läckor eller avbrott.

## <a name="incremental-improvement-of-the-policy-statements"></a>Stegvis förbättring av princip uttrycken

Följande ändringar i principen hjälper dig att åtgärda de nya riskerna och guidens implementering. Listan ser länge ut, men det kan vara lättare att införa dessa principer.

1. Alla distribuerade till gångar måste kategoriseras efter allvarlighets grad och data klassificering. Klassificeringarna bör granskas av moln styrnings teamet och program ägaren innan distributionen till molnet.
2. Program som lagrar eller kommer åt skyddade data ska hanteras annorlunda än de som inte är det. De bör minst segmenteras för att undvika oavsiktlig åtkomst till skyddade data.
3. Alla skyddade data måste krypteras när de är i vilo läge. Även om detta är standard för alla Azure Storage-konton kan ytterligare krypterings strategier behövas, inklusive kryptering av data i lagrings kontot, kryptering av virtuella datorer och kryptering på databas nivå när SQL används i en virtuell dator (TDE och kolumn kryptering ).
4. Utökade behörigheter i alla segment som innehåller skyddade data ska vara ett undantag. Eventuella sådana undantag kommer att registreras med moln styrnings teamet och granskas regelbundet.
5. Nätverks under nät som innehåller skyddade data måste isoleras från andra undernät. Nätverks trafik mellan skyddade data under nät kommer att granskas regelbundet.
6. Det går inte att komma åt ett undernät som innehåller skyddade data direkt via det offentliga Internet eller i flera data Center. Åtkomst till dessa undernät måste dirigeras via mellanliggande undernät. All åtkomst till dessa undernät måste komma via en brand Väggs lösning som kan utföra paket genomsökning och blockera funktioner.
7. Styrnings verktyg måste granska och genomdriva krav på nätverks konfiguration som definieras av Security Management-teamet.
8. Styrnings verktyg måste begränsa VM-distributionen till godkända avbildningar.
9. När det är möjligt bör konfigurations hantering för noden tillämpa princip krav för konfigurationen av gäst operativ system.
10. Styrnings verktyg måste framtvinga att automatiska uppdateringar aktive ras på alla distribuerade till gångar. Överträdelser måste granskas med operativa hanterings team och åtgärdas i enlighet med Operations policys. Till gångar som inte uppdateras automatiskt måste ingå i processer som ägs av IT-åtgärder.
11. Att skapa nya prenumerationer eller hanterings grupper för alla verksamhets kritiska program eller skyddade data kräver en granskning från moln styrnings teamet för att säkerställa att rätt skiss tilldelas.
12. En åtkomst modell med minst behörighet kommer att tillämpas på alla hanterings grupper eller prenumerationer som innehåller verksamhets kritiska appar eller skyddade data.
13. Trender och utnyttjande som kan påverka moln distributioner bör regelbundet granskas av säkerhets teamet för att tillhandahålla uppdateringar av verktyg för säkerhets hantering som används i molnet.
14. Distributions verktyg måste godkännas av moln styrnings teamet för att säkerställa fort löp ande styrning av distribuerade till gångar.
15. Distributions skripten måste finnas i en central lagrings plats som kan nås av moln styrnings teamet för regelbunden granskning och granskning.
16. Styrnings processer måste innehålla revisioner vid distributions platsen och regelbundet för att säkerställa konsekvens för alla till gångar.
17. Distribution av program som kräver kundautentisering måste använda en godkänd identitets leverantör som är kompatibel med den primära identitets leverantören för interna användare.
18. Moln styrnings processer måste innehålla kvartals Visa recensioner med identitets hanterings team. Dessa granskningar kan hjälpa till att identifiera skadliga aktörer eller användnings mönster som bör förhindras av konfiguration av moln till gångar.

## <a name="incremental-improvement-of-governance-practices"></a>Inkrementell förbättring av styrningsmetoder

Designen styrning MVP kommer att ändras till att inkludera nya Azure-principer och en implementering av Azure Cost Management. Tillsammans kommer dessa två design ändringar att uppfylla de nya företags princip satserna.

1. Nätverks-och IT-säkerhetsteamen definierar nätverks krav. Moln styrnings teamet kommer att stödja konversationen.
2. Identitets-och IT-säkerhetsteamen definierar identitets krav och gör nödvändiga ändringar i den lokala Active Directory implementeringen. Moln styrnings teamet kommer att granska ändringar.
3. Skapa en lagrings plats i Azure DevOps för att lagra och version av alla relevanta Azure Resource Manager mallar och konfigurationer med skript.
4. Azure Security Center implementering:
    1. Konfigurera Azure Security Center för alla hanterings grupper som innehåller skyddade data klassificeringar.
    2. Ange automatisk etablering till på som standard för att säkerställa att du korrigerar kompatibiliteten.
    3. Upprätta OS-säkerhetskonfigurationer. IT-säkerhetsteamet definierar konfigurationen.
    4. Ge support till IT-säkerhetsteamet i den första användningen av Security Center. Över gången till användningen av Security Center till IT-säkerhetsteamet, men ha kvar åtkomsten för att ständigt förbättra styrningen.
    5. Skapa en Resource Manager-mall som motsvarar de ändringar som krävs för Security Center konfiguration i en prenumeration.
5. Uppdatera Azure-principer för alla prenumerationer:
    1. Granska och genomdriva allvarlighets grad och data klassificering i alla hanterings grupper och prenumerationer för att identifiera eventuella prenumerationer med skyddade data klassificeringar.
    2. Granska och Använd endast godkända avbildningar.
6. Uppdatera Azure-principer för alla prenumerationer som innehåller skyddade data klassificeringar:
    1. Granska och Använd endast Azure RBAC-roller med standard typ.
    2. Granska och genomdriva kryptering för alla lagrings konton och filer i vila på enskilda noder.
    3. Granska och framtvinga tillämpning av en NSG för alla nätverkskort och undernät. Nätverks-och IT-säkerhetsteamen kommer att definiera NSG.
    4. Granska och genomdriva användningen av godkända nätverks under nät och vNet per nätverks gränssnitt.
    5. Granska och genomdriva begränsningen för användardefinierade vägvals tabeller.
    6. Använd de inbyggda principerna för gäst konfiguration enligt följande:
        1. Granska att Windows-webbservrar använder säkra kommunikations protokoll.
        2. Granska att inställningarna för lösen ords säkerhet är korrekt i Linux-och Windows-datorer.
7. Brandväggskonfiguration:
    1. Identifiera en konfiguration av Azure-brandväggen som uppfyller nödvändiga säkerhets krav. Du kan också identifiera en kompatibel tredje parts installation som är kompatibel med Azure.
    2. Skapa en Resource Manager-mall för att distribuera brand väggen med nödvändiga konfigurationer.
8. Azure-skiss:
    1. Skapa en ny skiss med namnet `protected-data`.
    2. Lägg till brand väggen och Azure Security Center mallar i skissen.
    3. Lägg till de nya principerna för skyddade data prenumerationer.
    4. Publicera skissen till alla hanterings grupper som för närvarande planerar att vara värd för skyddade data.
    5. Tillämpa den nya skissen på varje berörd prenumeration, förutom befintliga ritningar.

## <a name="conclusion"></a>Sammanfattning

Att lägga till ovanstående processer och ändringar i styrnings MVP: n hjälper till att åtgärda många av de risker som är förknippade med säkerhets styrning. Tillsammans lägger de till de nätverks-, identitets-och säkerhets övervaknings verktyg som behövs för att skydda data.

## <a name="next-steps"></a>Nästa steg

När moln implementeringen fortsätter och ger ytterligare affärs värde, behöver risker och moln styrning också förändringar. För det fiktiva företaget i den här hand boken är nästa steg att stödja verksamhets kritiska arbets belastningar. Detta är den punkt då kontrollerna av resurs konsekvens krävs.

> [!div class="nextstepaction"]
> [Förbättra resurs konsekvensen](./resource-consistency-improvement.md)
