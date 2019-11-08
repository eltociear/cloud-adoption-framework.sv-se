---
title: 'Styrnings guide för komplexa företag: förbättra säkerhets bas linje disciplinen'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Styrnings guide för komplexa företag: förbättra säkerhets bas linje disciplinen'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a8cf7c6bb09d2f4c505e3edcb97a0354a870a730
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753203"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-security-baseline-discipline"></a>Styrnings guide för komplexa företag: förbättra säkerhets bas linje disciplinen

Den här artikeln går vidare genom att lägga till säkerhets kontroller som stöder flytt av skyddade data till molnet.

## <a name="advancing-the-narrative"></a>Med den här berättelsenn

INFORMATIONS gruppen har ägnat flera månader åt att samar beta med kollegor och företagets juridiska personal. En hanterings konsult med expertis i cybersäkerhet var att hjälpa den befintliga IT-säkerheten och IT-styrningen att skriva en ny princip för skyddade data. Gruppen hade stöd för att ersätta den befintliga principen, vilket gör att känsliga personliga och finansiella data kan hanteras av godkända moln leverantörer. Detta krävs för att kunna använda en uppsättning säkerhets krav och styrnings processer för att verifiera och dokumentera iakttagande av dessa principer.

I de senaste 12 månaderna har moln implementerings teamen rensat ut de flesta av 5 000-resurserna från de två data centren som ska dras tillbaka. De 350 inkompatibla till gångarna flyttades till ett alternativt Data Center. Endast de 1 250 virtuella datorer som innehåller skyddade data finns kvar.

### <a name="changes-in-the-cloud-governance-team"></a>Ändringar i moln styrnings teamet

Moln styrnings teamet fortsätter att förändras tillsammans med de som behålls. De två identifierade medlemmarna i teamet är nu bland de mest respekterade moln arkitekterna i företaget. Samlingen av konfigurations skript har växt som nya team kan ta itu med nya distributioner. Moln styrnings teamet har också växt. De senaste medlemmarna i IT-avdelningen har anslutit sig till moln styrnings team för att förbereda för moln åtgärder. De moln arkitekter som hjälpte att utveckla den här communityn visas både som moln skydd och moln acceleratorer.

Skillnaden är diskret, men det är en viktig skillnad när du skapar en styrning – fokuserad IT-kultur. En moln övervakare rensar upp de problem som gjorts av innovativa moln arkitekter och de två rollerna har naturliga friktion och motsatta mål. En moln skyddare hjälper till att hålla molnet säkert så att andra moln arkitekter kan förflytta sig snabbare med färre röriga. En moln Accelerator utför båda funktionerna, men är också engagerad i att skapa mallar för att påskynda distribution och införande, bli en innovation-Accelerator och en Defender av de fem disciplinerna i moln styrning.

### <a name="changes-in-the-current-state"></a>Ändringar i det aktuella läget

I föregående fas av den här delen hade företaget påbörjat processen att ta ur driften av två Data Center. Den här kontinuerliga ansträngningen omfattar migrering av vissa program med äldre autentiseringskrav, vilka krävde stegvisa förbättringar av identitets bas linjen, som beskrivs i [föregående artikel](./identity-baseline-improvement.md).

Sedan dess har vissa saker ändrats som påverkar styrning:

- Tusentals IT-och företags till gångar har distribuerats till molnet.
- Program utvecklings teamet har implementerat en pipeline för kontinuerlig integrering och distribution (CI/CD) för att distribuera ett moln internt program med en förbättrad användar upplevelse. Programmet interagerar inte med skyddade data ännu, så det är inte produktions klart.
- Business Intelligence-teamet i IT kan aktivt granska data i molnet från logistik, inventering och data från tredje part. Dessa data används för att driva nya förutsägelser, vilket kan forma affärs processer. Dessa förutsägelser och insikter är dock inte åtgärdade förrän kund-och finans data kan integreras i data plattformen.
- IT-teamet fortlöper i informations chefs-och ekonomi planerna för att dra tillbaka två Data Center. Nästan 3 500 av till gångarna i de två data centren har dragits tillbaka eller migrerats.
- Principerna angående känsliga personliga och finansiella data har förberetts. De nya företags principerna är dock knutna till implementeringen av relaterade säkerhets-och styrnings principer. Team har fortfarande stoppats.

### <a name="incrementally-improve-the-future-state"></a>Förbättra framtida tillstånd stegvis

- Tidiga experiment från program utveckling och BI-team har visat potentiella förbättringar av kund upplevelser och data drivna beslut. Båda teamen skulle vilja utöka införandet av molnet under de kommande 18 månaderna genom att distribuera dessa lösningar till produktion.
- DEN har utvecklat en affärs motivering för att migrera fem fler data Center till Azure, vilket ytterligare minskar IT-kostnaderna och ger bättre flexibilitet i verksamheten. Vid mindre skala förväntas indragningen av dessa data Center för att minska den totala kostnads besparingarna.
- Utgifter för kapital-och drift kostnader har godkänts för att implementera de nödvändiga säkerhets-och styrnings principerna, verktygen och processerna. Förväntad kostnads besparingar från data Center indragningen är mer än tillräckligt för att betala för det nya initiativet. IT-och verksamhets ledande företag är säkra på att denna investering påskyndar realiseringen av returer på andra områden. Grassroots Cloud styrelses-teamet blev ett erkänt team med dedikerad ledarskap och personal.
- Kollektivt, moln implementerings team, moln styrnings teamet, IT-säkerhetsteamet och IT-styrningen kommer att implementera säkerhets-och styrnings krav för att tillåta moln antagande team att migrera skyddade data till molnet.

## <a name="changes-in-tangible-risks"></a>Förändringar i materiella risker

**Data intrång:** Det finns en sammanhängande ökning av skulder som är relaterade till data överträdelser när du antar nya data plattformar. Tekniker som inför moln teknologier har ökat ansvar för att implementera lösningar som kan minska risken. En robust säkerhets-och styrnings strategi måste implementeras för att säkerställa att dessa tekniker uppfyller dessa ansvars områden.

Den här affärs risken kan utökas till flera tekniska risker:

1. Verksamhets kritiska appar eller skyddade data kan distribueras oavsiktligt.
2. Skyddade data kan exponeras under lagringen på grund av dåliga krypterings beslut.
3. Obehöriga användare kan komma åt skyddade data.
4. Externt intrång kan leda till åtkomst till skyddade data.
5. Externt intrång eller denial of Service-attacker kan orsaka affärs avbrott.
6. Ändringar i organisationen eller sysselsättningen kan tillåta obehörig åtkomst till skyddade data.
7. Nya sårbarheter kan skapa möjligheter för intrång eller obehörig åtkomst.
8. Inkonsekventa distributions processer kan leda till säkerhets luckor som kan leda till data läckor eller avbrott.
9. Konfigurations luckor eller missade korrigeringar kan leda till oönskade säkerhets luckor som kan leda till data läckor eller avbrott.
10. Olika gräns enheter kan öka kostnaderna för nätverks drift.
11. Konfigurationer av olika enheter kan leda till överblick i konfigurationen och kompromettera säkerheten.
12. Cybersäkerhet-teamet insists kan vara en risk för att leverantören låser sig genom att generera krypterings nycklar på en enda moln leverantörs plattform. Även om det här anspråket är underbyggt accepteras det av teamet under tiden.

## <a name="incremental-improvement-of-the-policy-statements"></a>Stegvis förbättring av princip uttrycken

Följande ändringar i principen hjälper dig att åtgärda de nya riskerna och guidens implementering. Listan ser bra ut, men införandet av dessa principer kan vara enklare än vad som visas.

1. Alla distribuerade till gångar måste kategoriseras efter allvarlighets grad och data klassificering. Klassificeringarna bör granskas av moln styrnings teamet och programmet innan distributionen till molnet.
2. Program som lagrar eller kommer åt skyddade data ska hanteras annorlunda än de som inte är det. De bör minst segmenteras för att undvika oavsiktlig åtkomst till skyddade data.
3. Alla skyddade data måste krypteras när de är i vilo läge.
4. Utökade behörigheter i alla segment som innehåller skyddade data ska vara ett undantag. Eventuella sådana undantag kommer att registreras med moln styrnings teamet och granskas regelbundet.
5. Nätverks under nät som innehåller skyddade data måste isoleras från andra undernät. Nätverks trafik mellan skyddade data under nät kommer att granskas regelbundet.
6. Det går inte att komma åt ett undernät som innehåller skyddade data direkt via det offentliga Internet eller i flera data Center. Åtkomst till dessa undernät måste dirigeras via mellanliggande undernät. All åtkomst till dessa undernät måste komma via en brand Väggs lösning som kan utföra paket genomsökning och blockera funktioner.
7. Styrnings verktyg måste granska och genomdriva krav på nätverks konfiguration som definieras av Security Management-teamet.
8. Styrnings verktyg måste begränsa VM-distributionen till godkända avbildningar.
9. När det är möjligt bör konfigurations hantering för noden tillämpa princip krav för konfigurationen av gäst operativ system. Konfigurations hantering för noder bör respektera den befintliga investeringen i grupprincip objekt (GPO) för resurs konfiguration.
10. Styrnings verktyg granskar att automatiska uppdateringar har Aktiver ATS på alla distribuerade till gångar. När det är möjligt tillämpas automatiska uppdateringar. Om du inte tillämpar verktygs hantering måste överträdelser på radnivås nivå granskas med operativa hanterings team och åtgärdas i enlighet med drift principer. Till gångar som inte uppdateras automatiskt måste ingå i processer som ägs av IT-åtgärder.
11. Att skapa nya prenumerationer eller hanterings grupper för alla verksamhets kritiska program eller skyddade data kräver en granskning från moln styrnings teamet för att säkerställa en korrekt skiss tilldelning.
12. En åtkomst modell med minst behörighet kommer att tillämpas på alla prenumerationer som innehåller verksamhets kritiska program eller skyddade data.
13. Moln leverantören måste kunna integrera krypterings nycklar som hanteras av den befintliga lokala lösningen.
14. Moln leverantören måste kunna stödja den befintliga gräns enhets lösningen och alla konfigurationer som krävs för att skydda alla offentligt exponerade nätverks gränser.
15. Moln leverantören måste kunna stödja en delad anslutning till det globala WAN-nätverket, med data överföring dirigerad genom den befintliga gräns enhets lösningen.
16. Trender och utnyttjande som kan påverka moln distributioner bör regelbundet granskas av säkerhets teamet för att tillhandahålla uppdateringar av verktyget för säkerhets bas linjer som används i molnet.
17. Distributions verktyg måste godkännas av moln styrnings teamet för att säkerställa fort löp ande styrning av distribuerade till gångar.
18. Distributions skripten måste finnas i en central lagrings plats som kan nås av moln styrnings teamet för regelbunden granskning och granskning.
19. Styrnings processer måste innehålla revisioner vid distributions platsen och regelbundet för att säkerställa konsekvens för alla till gångar.
20. Distribution av program som kräver kundautentisering måste använda en godkänd identitets leverantör som är kompatibel med den primära identitets leverantören för interna användare.
21. Moln styrnings processer måste innehålla kvartals Visa recensioner med identitets bas grupper för att identifiera skadliga aktörer eller användnings mönster som bör förhindras av konfiguration av moln till gångar.

## <a name="incremental-improvement-of-the-best-practices"></a>Stegvis förbättring av bästa praxis

Det här avsnittet ändrar designen för styrnings MVP till att inkludera nya Azure-principer och en implementering av Azure Cost Management. Tillsammans kommer dessa två design ändringar att uppfylla de nya företags princip satserna.

De nya bästa metoderna är i två kategorier: företags IT (hubb) och molnbaserad adoption (eker).

**Upprätta en företags IT-hubb och eker-prenumeration för att centralisera säkerhets bas linjen:** I den här bästa praxis omsluts den befintliga styrnings kapaciteten av en [nav-och eker-topologi med delade tjänster](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services), med några viktiga tillägg från moln styrnings teamet.

1. Azure DevOps-lagringsplats. Skapa en lagrings plats i Azure DevOps för att lagra och version av alla relevanta Azure Resource Manager mallar och konfigurationer med skript.
2. Mall för hubb och eker:
    1. Rikt linjerna i [topologin hubb och eker med delade tjänster](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services) kan användas för att skapa Resource Manager-mallar för de till gångar som krävs i en företags IT-hubb.
    2. Med hjälp av dessa mallar kan den här strukturen göras repeterbar, som en del av en central styrnings strategi.
    3. Förutom den aktuella referens arkitekturen bör en mall för nätverks säkerhets grupper skapas för att avbilda alla port spärrnings-eller vit listning-krav för det virtuella nätverket som värd för brand väggen. Den här nätverks säkerhets gruppen skiljer sig från tidigare grupper, eftersom det är den första nätverks säkerhets gruppen som tillåter offentlig trafik till ett VNet.
3. Skapa Azure-principer. Skapa en princip med namnet `Hub NSG Enforcement` för att genomdriva konfigurationen av den nätverks säkerhets grupp som har tilldelats till ett virtuellt nätverk som skapats i den här prenumerationen. Använd de inbyggda principerna för gäst konfiguration enligt följande:
    1. Granska att Windows-webbservrar använder säkra kommunikations protokoll.
    2. Granska att inställningarna för lösen ords säkerhet är korrekt i Linux-och Windows-datorer.
4. IT-skiss för företag
    1. Skapa en Azure-skiss med namnet `corporate-it-subscription`.
    2. Lägg till hubb-och eker-mallarna och `Hub NSG Enforcement` principen.
5. Expanderar den inledande hanterings gruppens hierarki.
    1. För varje hanterings grupp som har begärt stöd för skyddade data tillhandahåller `corporate-it-subscription-blueprint` skissen en accelererad nav lösning.
    2. Eftersom hanterings grupper i det här fiktiva exemplet innehåller en regional hierarki förutom en affär senhets hierarki, kommer den här skissen att distribueras i varje region.
    3. Skapa en prenumeration med namnet `Corporate IT Subscription` för varje region i hanterings gruppens hierarki.
    4. Använd `corporate-it-subscription-blueprint` skissen på varje regional instans.
    5. Detta upprättar en hubb för varje affär senhet i varje region. Obs! ytterligare kostnads besparingar kan uppnås, men delnings nav mellan affär senheter i varje region.
6. Integrera grup princip objekt (GPO) via önskad tillstånds konfiguration (DSC):
    1. Konvertera GPO till DSC – [Microsoft Baseline Management-projektet](https://github.com/Microsoft/BaselineManagement) i GitHub kan påskynda denna ansträngning. Se till att lagra DSC i databasen parallellt med Resource Manager-mallar.
    2. Distribuera Azure Automation tillstånds konfiguration till alla instanser av företags IT-prenumerationen. Azure Automation kan användas för att tillämpa DSC på virtuella datorer som distribuerats i stödda prenumerationer i hanterings gruppen.
    3. Den aktuella översikten planerar att aktivera anpassade principer för gäst konfiguration. När funktionen släpps krävs inte längre användningen av Azure Automation i den här rekommenderade metoden.

**Använda ytterligare styrning för en moln implementerings prenumeration (eker):** Genom att bygga vidare på `Corporate IT Subscription` kan mindre förbättringar av styrnings MVP: en för varje prenumeration som är avsedd för program archetypes skapa snabb förbättring.

I tidigare repetitiva ändringar av bästa praxis definierade vi nätverks säkerhets grupper för att blockera offentlig trafik och vit listas intern trafik. Dessutom skapade Azure-skissen tillfälligt DMZ och Active Directory funktioner. I den här iterationen ska vi anpassa dessa till gångar till en bit, vilket skapar en ny version av Azure-skissen.

1. Mall för nätverks peering. Den här mallen kommer att peer-nätverket i varje prenumeration med hubb-VNet i den företags IT-prenumerationen.
    1. Referens arkitekturen från föregående avsnitt, [hubb och eker-topologi med delade tjänster](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services), genererade en Resource Manager-mall för att aktivera VNet-peering.
    2. Mallen kan användas som en guide för att ändra DMZ-mallen från föregående styrnings iteration.
    3. Nu lägger vi till VNet-peering i DMZ VNet som tidigare var anslutna till den lokala Edge-enheten via VPN.
    4. Dessutom bör VPN också tas bort från den här mallen även för att se till att ingen trafik dirigeras direkt till det lokala data centret utan att passera genom den lokala IT-prenumerationen och brand Väggs lösningen. Du kan också ange den här VPN-kretsen som en redundansväxling i händelse av en ExpressRoute-krets outge.
    5. Ytterligare [nätverks konfiguration](https://docs.microsoft.com/azure/automation/automation-dsc-overview#network-planning) krävs av Azure Automation att använda DSC för virtuella datorer som är värdar för virtuella datorer.
2. Ändra nätverks säkerhets gruppen. Blockera all offentlig **och** direkt lokal trafik i nätverks säkerhets gruppen. Den enda inkommande trafiken ska komma via VNet-peer i IT-prenumerationen för företaget.
    1. I den tidigare iterationen skapades en nätverks säkerhets grupp som blockerar all offentlig trafik och vit listning all intern trafik. Nu vill vi byta till den här nätverks säkerhets gruppen en bit.
    2. Den nya nätverks säkerhets grupp konfigurationen ska blockera all offentlig trafik, tillsammans med all trafik från det lokala data centret.
    3. Trafik som anger det här virtuella nätverket ska endast komma från VNet på den andra sidan av VNet-peer-datorn.
3. Azure Security Center implementering:
    1. Konfigurera Azure Security Center för alla hanterings grupper som innehåller skyddade data klassificeringar.
    2. Ange automatisk etablering till på som standard för att säkerställa att du korrigerar kompatibiliteten.
    3. Upprätta OS-säkerhetskonfigurationer. IT-säkerhet för att definiera konfigurationen.
    4. Stöd IT-säkerhet vid inledande användning av Azure Security Center. Över gångs användning av Security Center till IT-säkerhet, men bevara åtkomsten för kontinuerligt förbättrings syfte.
    5. Skapa en Resource Manager-mall som återspeglar de ändringar som krävs för Azure Security Center konfiguration i en prenumeration.
4. Uppdatera Azure Policy för alla prenumerationer.
    1. Granska och Använd allvarlighets grad och data klassificering i alla hanterings grupper och prenumerationer för att identifiera eventuella prenumerationer med skyddade data klassificeringar.
    2. Granska och Använd endast godkända OS-avbildningar.
    3. Granska och Använd gäst konfigurationerna baserat på säkerhets krav för varje nod.
5. Uppdatera Azure Policy för alla prenumerationer som innehåller skyddade data klassificeringar.
    1. Granska och Använd endast standard roller
    2. Granska och framtvinga kryptering av kryptering för alla lagrings konton och filer i vila på enskilda noder.
    3. Granska och tillämpa den nya versionen av DMZ-nätverks säkerhets gruppen.
    4. Granska och Framtvinga användning av godkända nätverks under nät och VNet per nätverks gränssnitt.
    5. Granska och genomdriva begränsningen för användardefinierade vägvals tabeller.
6. Azure-skiss:
    1. Skapa en Azure-skiss med namnet `protected-data`.
    2. Lägg till VNet-peer, nätverks säkerhets grupp och Azure Security Center mallar i skissen.
    3. Se till att mallen för Active Directory från föregående iteration **inte** ingår i skissen. Eventuella beroenden på Active Directory anges av IT-prenumerationen för företaget.
    4. Avsluta alla befintliga Active Directory virtuella datorer som distribuerats i föregående iteration.
    5. Lägg till de nya principerna för skyddade data prenumerationer.
    6. Publicera skissen till alla hanterings grupper som ska vara värd för skyddade data.
    7. Använd den nya skissen på varje berörd prenumeration tillsammans med befintliga ritningar.

## <a name="conclusion"></a>Sammanfattning

Genom att lägga till dessa processer och ändringar i styrnings MVP: n kan du åtgärda många av de risker som är förknippade med säkerhets styrningen. Tillsammans lägger de till de nätverks-, identitets-och säkerhets övervaknings verktyg som behövs för att skydda data.

## <a name="next-steps"></a>Nästa steg

När moln implementeringen fortsätter och ger ytterligare affärs värde, behöver risker och moln styrning också förändringar. För det fiktiva företaget i den här hand boken är nästa steg att stödja verksamhets kritiska arbets belastningar. Detta är den punkt då kontrollerna av resurs konsekvens krävs.

> [!div class="nextstepaction"]
> [Förbättra disciplinen för resurs konsekvens](./resource-consistency-improvement.md)
