---
title: Skala en migrering till Azure
description: Läs om hur Contoso hanterar en skalad migrering till Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 8a807bfc20289339221056b9b0798260aaddbfd8
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807316"
---
# <a name="scale-a-migration-to-azure"></a>Skala en migrering till Azure

Den här artikeln visar hur det fiktiva företaget Contoso utför en migrering i stor skala till Azure. De funderar på hur de ska planera och utföra en migrering av fler än 3000 arbetsbelastningar, 8000-databaser och över 10 000-virtuella datorer.

## <a name="business-drivers"></a>Affärsdrivande faktorer

IT-ledningsgruppen har arbetat tillsammans med affärspartner för att komma fram till vad man vill uppnå med migreringen:

- **Hantera företagets tillväxt.** Contoso växer och det finns ett tryck på lokala system och infrastruktur.
- **Öka effektiviteten.** Contoso måste ta bort onödiga procedurer och effektivisera processer för utvecklare och användare. En snabb IT-lösning som inte slösar tid eller pengar är viktigt för företaget, så att man kan leverera snabbare enligt kundkraven.
- **Öka flexibiliteten.** Contosos IT-avdelning måste reagera snabbare på företagets behov. Den måste kunna reagera snabbare än förändringarna på marknaden för att företaget ska lyckas i en global ekonomi. Den får inte vara i vägen eller bromsa verksamheten.
- **Skala.** När företagets verksamhet växer måste Contosos IT-team tillhandahålla system som kan växa i samma takt.
- **Bättre kostnadsmodeller.** Contoso vill minska kapitalkraven i IT-budgeten. Contoso vill använda molnfunktioner för att skala och minska behovet av dyr maskinvara.
- **Lägre licenskostnader.** Contoso vill minimera molnkostnaderna.

## <a name="migration-goals"></a>Migreringsmål

Contosos molnteam har fastställt mål för migreringen. Målen användes för att fastställa den bästa migreringsmetoden.

**Krav** | **Detaljer**
--- | ---
**Flytta till Azure snabbt** | Contoso vill börja flytta appar och virtuella datorer till Azure så snabbt som möjligt.
**Kompilera en fullständig inventering** | Contoso vill ha en fullständig inventering av alla appar, databaser och virtuella datorer i organisationen.
**Utvärdera och klassificera appar** | Contoso vill utnyttja molnet fullt ut. Som standard förutsätter Contoso att alla tjänster kommer att köras som PaaS. IaaS kommer att användas där PaaS inte är tillämpligt.
**Utbilda och övergå till DevOps** | Contoso vill flytta till en DevOps-modell. Contoso tillhandahåller Azure- och DevOps-utbildning och organiserar teamen efter behov.

När Contoso har identifierat sina mål och behov granskar de IT-behovet och identifierar en migrationsprocess.

## <a name="current-deployment"></a>Aktuell distribution

När Contoso har planerat och konfigurerat en [Azure-infrastruktur](./contoso-migration-infrastructure.md) och testat olika POC-kombinationer (proof-of-Concept) som beskrivs i tabellen ovan är de redo att sätta igång en fullständig migrering till Azure i stor skala. Det här är vad Contoso vill migrera.

<!--markdownlint-disable MD033 -->

**Objekt** | **Volym** | **Detaljer**
--- | --- | ---
**Arbetsbelastningar** | Mer än 3 000 appar | Appar körs på virtuella datorer.<br/><br/>  Appar körs på Windows SQL och OSS LAMP.
**Databaser** | Cirka 8 500 | Databaserna är SQL Server, MySQL, PostgreSQL.
**Virtuella datorer** | Fler än 35 000 | Virtuella datorer körs på VMware-värdar och hanteras av vCenter-servrar.

<!--markdownlint-enable MD033 -->

## <a name="migration-process"></a>Migreringsprocessen

Nu när Contoso har identifierat sina affärsincitament och migreringsmål bestämmer de sig för en fyrdelad metod för migreringsprocessen:

- **Fas 1: utvärdera.** Identifiera aktuella tillgångar och ta reda på om de är lämpliga för migrering till Azure.
- **Fas 2: migrera.** Flytta tillgångarna till Azure. Hur de flyttar appar och objekt till Azure beror på appen och vad de vill uppnå.
- **Fas 3: optimera.** När de har flyttat resurser till Azure måste Contoso förbättra och effektivisera dem för högsta möjliga prestanda och effektivitet.
- **Fas 4: skydda och hantera.** Med allt på plats använder Contoso nu Azures säkerhets- och hanteringsresurser och -tjänster för att styra, skydda och övervaka dess molnappar i Azure.

Dessa faser är inte seriella i hela organisationen. Varje del av Contosos migreringsprojekt kommer att befinna sig i olika skeden av utvärderings- och migreringsprocessen. Optimering, säkerhet och hantering kommer att pågå under en längre tid.

## <a name="phase-1-assess"></a>Fas 1: utvärdera

Contoso inleder sin Azure-migrering med att identifiera och utvärdera lokala appar, data och infrastruktur. Det här är vad Contoso planerar att göra:

- Contoso måste identifiera program, kartlägga beroenden mellan program och bestämma sig för en migreringsordning och -prioritet.
- Under utvärderingen måste Contoso noggrant inventera alla program och resurser. I samband med inventeringen kommer Contoso att använda och uppdatera den befintliga konfigurationshanteringsdatabasen (CMDB) och servicekatalogen.
  - Konfigurationshanteringsdatabasen innehåller tekniska konfigurationer för Contoso-appar.
  - Servicekatalogen dokumenterar driftsinformation om program, inklusive tillhörande affärspartners och serviceavtal.

### <a name="discover-apps"></a>Upptäck appar

Contoso kör tusentals appar över ett stort antal servrar. Utöver CMDB och servicekatalogen behöver Contoso övervaknings- och utvärderingsverktyg.

- Verktygen måste ge en mekanisk som kan föra in utvärderingsdata i migreringsprocessen.
- Utvärderingsverktyget måste tillhandahålla data som intelligent inventerar Contosos fysiska och virtuella resurser. Data ska innehålla profilinformation och prestandamått.
- När inventeringen är slutförd bör Contoso ha sammanställt alla tillgångar och metadata som associeras med dessa. Förteckningen kommer att användas för att definiera migreringsplanen.

### <a name="identify-classifications"></a>Identifiera klassificeringar

Contoso identifierar några vanliga kategorier för att klassificera tillgångar i förteckningen. De här klassificeringarna är viktiga för Contosos beslut att utföra migrering. Klassificeringslistan hjälper till att upprätta prioriteringar för migrering och identifiera komplexa problem.

**Kategori** | **Tilldelat värde** | **Detaljer**
--- | --- | ---
Affärsgrupp | Lista över namn på affärsgrupper | Vilken grupp ansvarar för vilken del av inventeringen?
POC-kandidat | Ja/nej | Kan appen användas som POC eller prototyp för molnbaserad migrering?
Teknisk skuld | Ingen/viss/grav | Använder eller kör inventeringspunkten en produkt, en plattform eller ett operativsystem som inte längre omfattas av support?
Brandväggskonsekvenser | Ja/nej | Kommunicerar appen med Internet/extern trafik?  Kan den integreras med en brandvägg?
Säkerhetsproblem | Ja/nej | Har programmet kända säkerhetsproblem?  Använder appen krypterade data eller inaktuella plattformar?

### <a name="discover-app-dependencies"></a>Upptäck appberoenden

Som en del av bedömningsprocessen måste Contoso identifiera var appar körs och identifiera beroenden och anslutningar mellan programservrar. Contoso kartlägger miljön stegvis.

1. Det första steget går ut på att Contoso upptäcker hur servrar och datorer mappas till enskilda appar, nätverksplatser och grupper.
2. Med den här informationen kan Contoso tydligt identifiera appar som har få beroende och därför är lämpliga för en snabb migrering.
3. Contoso kan använda mappning för att hjälpa dem att identifiera mer komplexa beroenden och kommunikation mellan appservrar. Contoso kan sedan gruppera servrarna logiskt för att representera appar och planera en migreringsstrategi baserat på dessa grupper.

När mappningen är klar kan Contoso se till att alla appkomponenter identifieras och redovisas när du skapar migreringsprocessen.

![Beroendemappning](./media/contoso-migration-scale/dependency-map.png)

### <a name="evaluate-apps"></a>Utvärdera appar

Det sista steget i identifierings- och utvärderingsprocessen går ut på att Contoso utvärderar och kartlägger resultaten för att bedöma hur varje mapp ska migreras i servicekatalogen.

För att maximera värdet av utvärderingsprocessen lägger de till ett par övriga klassificeringar i inventeringen.

**Kategori** | **Tilldelat värde** | **Detaljer**
--- | --- | ---
Affärsgrupp | Lista över namn på affärsgrupper | Vilken grupp ansvarar för vilken del av inventeringen?
POC-kandidat | Ja/nej | Kan appen användas som POC eller prototyp för molnbaserad migrering?
Teknisk skuld | Ingen/viss/grav | Använder eller kör inventeringspunkten en produkt, en plattform eller ett operativsystem som inte längre omfattas av support?
Brandväggskonsekvenser | Ja/nej | Kommunicerar appen med Internet/extern trafik?  Kan den integreras med en brandvägg?
Säkerhetsproblem | Ja/nej | Har programmet kända säkerhetsproblem?  Använder appen krypterade data eller inaktuella plattformar?
Migreringsstrategi | Byt värd/omstrukturera/omarbeta arkitektur/återskapa | Vilken typ av migrering behövs för appen? Hur kommer appen distribueras i Azure? [Läs mer](./contoso-migration-overview.md#migration-patterns).
Teknisk komplexitet | 1-5 | Hur komplex är migreringen? Det här värdet ska definieras av Contoso DevOps och relevanta partner.
Verksamhetskritisk | 1-5 | Hur viktigt är appen för verksamheten? Till exempel kan en liten arbetsgruppsapp tilldelas värdet ett, medan en kritisk app som används i hela organisationen kan tilldelas värdet fem. Poängen kommer att påverka prioritetsnivån för migreringen.
Prioritet för migrering | 1/2/3 | Vad är appens migreringsprioritet?
Migreringsrisk | 1-5 | Hur stor är risken med att migrera appen? Det här värdet ska definieras av Contoso DevOps och relevanta partner.

### <a name="figure-out-costs"></a>Räkna ut kostnader

För att räkna ut kostnaderna och de potentiella besparingarna i Azure-migreringen kan Contoso [använda den totala ägandekostnaden (TCO)](https://azure.microsoft.com/pricing/tco/calculator) för att beräkna och jämföra TCO för Azure med en jämförbar lokal distribution.

### <a name="identify-assessment-tools"></a>Identifiera utvärderingsverktyg

Contoso bestämmer vilket verktyg som ska användas för identifiering, utvärdering och utveckling av inventeringen. Contoso identifierar en blandning av Azure-verktyg och -tjänster, inbyggda appverktyg och skript samt partnerverktyg. Contoso är särskilt intresserat av att veta hur Azure Migrate kan användas för att utvärdera i stor skala.

#### <a name="azure-migrate"></a>Azure Migrate

Azure Migrate beskriver hur du identifierar och utvärderar lokala virtuella VMware-datorer inför migrering till Azure. Så här gör Azure Migrate:

1. Identifiera: identifiera lokala virtuella VMware-datorer.
    - Azure Migrate stöder identifiering från flera vCenter-servrar (seriellt) och kan köra identifieringar i separata Azure Migrate-projekt.
    - Azure Migrate utför identifieringen med hjälp av en virtuell VMware-dator som kör migreringsinsamlaren. Samma insamlare kan identifiera virtuella datorer på olika vCenter-servrar och skicka data till olika projekt.
2. Utvärdera beredskap: Bedöm om lokala datorer är lämpliga för att köra i Azure. Utvärderingen inkluderar:
    - Storleks rekommendationer: få storleks rekommendationer för virtuella Azure-datorer, baserat på lokala virtuella datorers prestanda historik.
    - Uppskattade månads kostnader: få beräknade kostnader för att köra lokala datorer i Azure.
3. Identifiera beroenden: visualisera beroenden för lokala datorer för att skapa optimala dator grupper för utvärdering och migrering.

![Azure Migrate](./media/contoso-migration-scale/azure-migrate.png)

##### <a name="migrate-at-scale"></a>Migrera i stor skala

Contoso måste använda Azure Migrate korrekt med tanke på migreringens skala.

- Contoso kommer att utvärdera varje app individuellt med Azure Migrate. Detta säkerställer att Azure Migrate returnerar data i tid till Azure Portal.
- Contosos administratörer läser [om att distribuera Azure Migrate i stor skala](https://docs.microsoft.com/azure/migrate/how-to-scale-assessment)
- Contoso noterar Azure Migrate-gränserna som sammanfattas i följande tabell.

**Åtgärd** | **Gräns**
--- | ---
Skapa ett Azure Migrate-projekt | 10 000 virtuella datorer
Identifiering | 10 000 virtuella datorer
Utvärdering | 10 000 virtuella datorer

Contoso använder Azure Migrate på följande sätt:

- I vCenter organiserar Contoso virtuella datorer i mappar. Detta gör det enkelt för dem att fokusera när de kör en utvärdering mot virtuella datorer i en specifik mapp.
- Azure Migrate använder Azure-tjänstkartan för att visa beroenden mellan datorer. Detta kräver att agenter installeras på de virtuella datorer som ska utvärderas.
  - Contoso kommer att använda automatiserade skript för att installera de Windows-eller Linux-agenter som krävs.
  - Med skript kan Contoso skicka installationen till virtuella datorer i en vCenter-mapp.

#### <a name="database-tools"></a>Databasverktyg

Förutom Azure Migrate fokuserar Contoso på att använda verktyg som är specifika för utvärderingen av databasen. Verktyg som [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017) bidrar till att utvärdera SQL Server-databaser för migrering.

Data Migration Assistant (DMA) kan hjälpa Contoso att ta reda på om lokala databaser är kompatibla med ett utbud av Azure Database-lösningar, till exempel Azure SQL Database, SQL Server som körs på en virtuell Azure IaaS-dator och Azure SQL-hanterad instans.

Förutom DMS har Contoso några andra skript som de använder för att identifiera och dokumentera SQL Server-databaser. Dessa finns i GitHub-lagringsplatsen.

#### <a name="partner-assessment-tools"></a>Partnerutvärderingsverktyg

Det finns flera andra partnerverktyg som kan hjälpa Contoso att utvärdera den lokala migreringsmiljön för Azure. [Lär dig mer](https://azure.microsoft.com/migration/partners) om Azure-migreringspartners.

## <a name="phase-2-migrate"></a>Fas 2: migrera

Med deras bedömning måste du identifiera verktyg för att flytta appar, data och infrastruktur till Azure.

### <a name="migration-strategies"></a>Migreringsstrategier

Det finns fyra huvudsakliga migreringsstrategier som Contoso kan överväga.

<!--markdownlint-disable MD033 -->

**Strategi** | **Detaljer** | **Användning**
--- | --- | ---
**Värdbyte** | Kallas ofta för en _hiss och Shift_ -migrering. det här är ett alternativ utan kod för att migrera befintliga appar till Azure snabbt.<br/><br/> En app migreras i befintligt skick för att dra nytta av molnets fördelar utan de risker och kostnader som är förknippade med kodändringar. | Contoso kan vara värd för mindre strategiska appar, vilket innebär att inga kodändringar krävs.
**Refaktorisering** | Den här strategin kallas även "ompaketering" och kräver minimal kod för appar eller konfigurationsändringar som krävs för att ansluta appen till Azure PaaS och för att utnyttja molnfunktionerna bättre. | Contoso kan omstrukturera strategiska appar för att behålla samma grundläggande funktioner men flytta dem till att köras på en Azure-plattform som Azure App Service.<br/><br/> Detta kräver minimala kodändringar.<br/><br/> Å andra sidan måste contoso underhålla en VM-plattform eftersom den inte hanteras av Microsoft.
**Arkitekturomarbetning** | Den här strategin ändrar eller utökar en apps kodbas för att optimera appens arkitektur för molnfunktioner och skalning.<br/><br/> Den moderniserar en app till en elastisk och mycket skalbar arkitektur som kan distribueras självständigt.<br/><br/> Använd Azure-tjänster om du vill accelerera processen, skala ut program säkert och hantera dina appar utan problem.
**Återskapande** | Den här strategin återskapa en app från grunden med hjälp av inbyggd molnteknik.<br/><br/> Azure PaaS (plattform som tjänst) levererar en fullständig miljö för utveckling och distribution i molnet. Vissa av kostnaderna samt komplexiteten programvarulicenserna minskar och underliggande appinfrastruktur, mellanprogram och andra resurser behövs inte. | Contoso kan skriva om viktiga appar från grunden för att utnyttja molnteknik, till exempel en serverlös dator eller mikrotjänster.<br/><br/> Contoso hanterar sin app och tjänst medan Azure hanterar allt annat.

<!--markdownlint-enable MD033 -->

Data måste övervägas, särskilt med Contosos stora databaser. Contosos standardmetod är att använda PaaS-tjänster som Azure SQL Database för att dra full nytta av molnfunktionerna. Genom att flytta till en PaaS-tjänst för databaser behöver Contoso bara underhålla data och lämna den underliggande plattformen till Microsoft.

### <a name="evaluate-migration-tools"></a>Utvärdera migreringsverktyg

Contoso använder i första hand ett par Azure-tjänster och -verktyg för migreringen:

- [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview): dirigerar haveri beredskap och migrerar lokala virtuella datorer till Azure.
- [Azure Database migration service](https://docs.microsoft.com/azure/dms/dms-overview): migrerar lokala databaser som SQL Server, MySQL och Oracle till Azure.

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery är den primära Azure-tjänsten för att samordna haveriberedskap och migrering inifrån Azure och från lokala platser till Azure.

1. Site Recovery aktiverar och samordnar replikeringen från dina lokala platser till Azure.
2. När replikeringen har etablerats och körs kan lokala datorer redundansväxla till Azure och slutföra migreringen.

Contoso har [redan slutfört en POC](./contoso-migration-rehost-vm.md) för att se hur Site Recovery kan hjälpa dem att migrera till molnet.

##### <a name="use-site-recovery-at-scale"></a>Använd Site Recovery i skala

Contoso planerar att utföra flera migreringar och Shift-migreringar. För att detta ska fungera kommer Site Recovery att replikera omgångar med cirka 100 virtuella datorer i taget. Contoso måste utföra en kapacitetsplanering för den föreslagna Site Recovery-migreringen lära sig hur detta går till.

- Contoso måste samla in information om deras trafikvolymer. Framför allt:
  - Contoso måste bestämma ändringstakten för de virtuella datorer som de vill replikera.
  - Contoso måste också överväga nätverksanslutningen från den lokala platsen till Azure.
- Som svar på kapacitets-och volymkraven måste Contoso tilldela tillräckligt med bandbredd baserat på den dagliga dataändringstakten för de virtuella datorer som krävs för att uppfylla återställningspunktmålet.
- Slutligen måste de räkna ut hur många servrar behövs för att köra de Site Recovery-komponenter som behövs för distributionen.

###### <a name="gather-on-premises-information"></a>Samla in lokal information

Contoso kan använda verktyget [Site Recovery Deployment Planner](https://docs.microsoft.com/azure/site-recovery/site-recovery-deployment-planner) för att utföra dessa steg:

- Contoso kan använda verktyget för att fjärrhantera virtuella datorer utan påverkan på produktionsmiljön. Detta bidrar till att hitta bandbredds- och lagringskrav för replikering och redundans.
- Contoso kan köra verktyget utan att installera alla Site Recovery-komponenter lokalt.
- Verktyget samlar in information om kompatibla och inkompatibla virtuella datorer, diskar per virtuell dator och dataomsättning per disk. Verktyget identifierar även kraven på nätverksbandbredd och vilken Azure-infrastruktur som krävs för en lyckad replikering och redundans.
- Contoso måste kontrollera till att du kör planeringsverktyget på en Windows Server-dator som uppfyller minimikraven för Site Recovery-konfigurationsservern. Konfigurationsservern är en Site Recovery-dator som behövs för att kunna replikera lokala virtuella VMware-datorer.

###### <a name="identify-site-recovery-requirements"></a>Identifiera Site Recovery-krav

Förutom de virtuella datorer som replikeras kräver Site Recovery flera komponenter för VMware-migrering.

<!--markdownlint-disable MD033 -->

**Komponent** | **Detaljer**
--- | ---
**Konfigurationsserver** | Vanligtvis en virtuell VMware-dator med en OVF-mall.<br/><br/> Konfigurationsserverkomponenten samordnar kommunikationen mellan den lokala miljön och Azure och hanterar datareplikering.
**Processervern** | Installeras som standard på konfigurationsservern.<br/><br/> Processerverkomponenten tar emot replikeringsdata, optimerar dem med cachelagring, komprimering och kryptering och skickar dem till Azure Storage.<br/><br/> Processervern installerar också mobilitetstjänsten Azure Site Recovery på de virtuella datorer du vill replikera, samt utför automatisk identifiering av lokala virtuella VMware-datorer.<br/><br/> Skalade distributioner behöver ytterligare, fristående processservrar för att hantera stora mängder replikeringstrafik.
**Mobilitetstjänst** | Mobilitetstjänstagenten installeras på varje virtuell VMware-dator som kommer att migreras med Site Recovery.

<!--markdownlint-enable MD033 -->

Contoso måste räkna ut hur dessa komponenter ska distribueras baserat på kapacitetsöverväganden.

<!--markdownlint-disable MD033 -->

**Komponent** | **Kapacitetskrav**
--- | ---
**Maximal daglig ändringshastighet** | En enda processerver kan hantera en daglig ändrings hastighet på upp till 2 TB. Eftersom en virtuell dator bara kan använda en processerver är det högsta antalet dagliga data ändringar som stöds för en replikerad virtuell dator 2 TB.
**Maximalt dataflöde** | Ett Azure Storage-standardkonto kan hantera högst 20 000 förfrågningar per sekund och in-/utdataåtgärder per sekund (IOPS) över en replikerad virtuell dator ska ligga inom den här gränsen. Till exempel, om en virtuell dator har 5 diskar och varje disk genererar 120 IOPS (8K storlek) på den virtuella datorn kommer den att ligga inom Azures IOPS-gräns per disk på 500.<br/><br/> Observera att antalet lagringskonton som behövs motsvarar den totala källdatorns IOPS delat med 20 000. En replikerad dator kan bara tillhöra ett enda lagrings konto i Azure.
**Konfigurationsserver** | Baserat på Contosos uppskattning av de behöver replikera 100=200 virtuella datorer och [storlekskraven för konfigurationsservern](https://docs.microsoft.com/azure/site-recovery/site-recovery-plan-capacity-vmware#size-recommendations-for-the-configuration-server-and-inbuilt-process-server) uppskattar Contoso att de behöver följande konfigurationsserverdator:<br/><br/> CPU: 16 virtuella processorer (2 Sockets &#215; 8 kärnor @ 2,5 GHz)<br/><br/> Minne: 32 GB<br/><br/> Cache-disk: 1 TB<br/><br/> Data ändrings frekvens: 1 TB till 2 TB.<br/><br/> Utöver storlekskraven vill Contoso se till att konfigurationsservern är belägen på en optimal plats, samt på samma nätverk och LAN-segment som den virtuella datorn som ska migreras.
**Processervern** | Contoso distribuerar en fristående dedikerad processerver med möjlighet att replikera 100-200 virtuella datorer:<br/><br/> CPU: 16 virtuella processorer (2 Sockets &#215; 8 kärnor @ 2,5 GHz)<br/><br/> Minne: 32 GB<br/><br/> Cache-disk: 1 TB<br/><br/> Data ändrings frekvens: 1 TB till 2 TB.<br/><br/> Processervern kommer att arbeta hårt och därför bör den finnas på en ESXi-värd som kan hantera sådana volymer för disk-I/O, nätverk trafik och CPU som krävs för replikeringen. Contoso överväger att använda den dedikerad värd för detta.
**Nätverk** | Contoso har granskat den aktuella plats-till-plats-VPN-infrastrukturen och beslutat sig för att implementera Azure-ExpressRoute. Implementeringen är kritisk eftersom den kommer att minska svarstiden och förbättra bandbredden till Contosos primära region: USA, östra 2.<br/><br/> **Övervakning:** Contoso måste noggrant övervaka data som flödar från processervern. Om data överbelastar nätverksbandbredden kan Contoso överväga att [begränsa processerverns bandbredd](https://docs.microsoft.com/azure/site-recovery/site-recovery-plan-capacity-vmware#control-network-bandwidth).
**Azure Storage** | För migreringen måste Contoso identifiera och skapa rätt typ och antal för sina Azure Storage-målkonton. Site Recovery replikerar data från virtuella datorer till Azure Storage.<br/><br/> Site Recovery kan replikeras till standard- eller premiumlagringskonton (SSD).<br/><br/> Contoso måste granska [lagrings gränserna](https://docs.microsoft.com/azure/virtual-machines/windows/disks-types) och bedöma den förväntade tillväxten och ökade användning över tid för att fatta ett beslut om lagring. Med tanke på hastigheten och prioriteten hos migreringar har contoso valt att använda Premium-SSD.<br/><br/>
Contoso har valt att använda hanterade diskar för alla virtuella datorer som distribueras till Azure. IOPS-behovet avgör om diskarna ska vara Standard HDD, Standard SSD eller Premium (SSD).<br/><br/>

<!--markdownlint-enable MD033 -->

#### <a name="azure-database-migration-service"></a>Azure Database Migration Service

Azure Database Migration Service är en fullständigt hanterad tjänst som möjliggör sömlösa migreringar från flera databaskällor till Azure-dataplattformar med minimal avbrottstid.

- DMS integrerar funktioner hos befintliga verktyg och tjänster. Den använder Data Migration Assistant (DMA) för att skapa utvärderingsrapporter som lokaliserar rekommendationer om databasens kompatibilitet och eventuella nödvändiga ändringar.
- DMS använder en enkel, självgående migreringsprocess med intelligent utvärdering som hjälper användaren att åtgärda eventuella problem inför migreringen.
- DMS kan migrera i rätt skala från flera källor till Azure-måldatabasen.
- DMS har stöd från SQL Server 2005 till SQL Server 2017.

DMS är inte det enda migreringsverktyget för Microsoft Database. Få en [jämförelse av verktyg och tjänster](https://blogs.msdn.microsoft.com/datamigration/2017/10/13/differentiating-microsofts-database-migration-tools-and-services).

##### <a name="use-dms-at-scale"></a>Använd DMS i skala

Contoso kommer att använda DMS vid migrering från SQL Server.

- När Contoso etablerar DMS måste de ändra storlek på det korrekt och ställa in storlek för att optimera prestanda för datamigreringar. Contoso väljer alternativet ”verksamhetskritisk nivå med 4 virtuella kärnor”, vilket gör att tjänsten kan dra nytta av flera virtuella processorer för parallellisering och snabbare dataöverföring.

    ![DMS-skalning](./media/contoso-migration-scale/dms.png)

- En annan skalningsstrategi för Contoso är att tillfälligt skala upp Azure SQL- eller My DQL-databasmålinstansen till ett SKU på premiumnivå under datamigreringen. Detta minimerar databasbegränsningen som kan påverka data överföringsaktiviteter när du använder SKU:er på lägre nivå.

##### <a name="use-other-tools"></a>Använd andra verktyg

Förutom DMS kan Contoso använda andra verktyg och tjänster för att identifiera information om en virtuell dator.

- De har skript som underlättar vid manuella migreringar. Dessa finns i GitHub-lagringsplatsen.
- Olika [partnerverktyg](https://azure.microsoft.com/migration/partners) kan också användas för migrering.

## <a name="phase-3-optimize"></a>Fas 3: optimera

När Contoso har flyttat resurser till Azure måste de effektivisera dem för att förbättra prestandan och maximera avkastningen med kostnadshanteringsverktyg. Med tanke på att Azure är en tjänst med betalning per användning är det viktigt för Contoso att förstå hur systemen presterar och se till att de har rätt storlek.

### <a name="azure-cost-management"></a>Azure Cost Management

För att få ut så mycket som möjligt av sin molninvestering använder Contoso det kostnadsfria verktyget Azure Cost Management.

- Med den här licensierade lösningen som har skapats av Cloudyn, ett dotterbolag till Microsoft, kan Contoso hantera molnutgifter med insyn och precision. Den innehåller verktyg för att övervaka, allokera och minska molnkostnader.
- Azure Cost Management innehåller enkla rapportpaneler som hjälper med kostnadsallokering, kostnadsvisning och debitering baserat på faktisk förbrukning.
- Cost Management optimerar molnutgifterna genom att identifiera underutnyttjade resurser som Contoso sedan kan hantera och anpassa.
- [Läs mer](https://docs.microsoft.com/azure/cost-management/overview) om Azure Cost Management.

![Kostnadshantering](./media/contoso-migration-scale/cost-management.png)

### <a name="native-tools"></a>Inbyggda verktyg

Contoso kommer också att använda skript för att hitta oanvända resurser.

- Vid stora migreringar finns ofta kvarblivna data, till exempel virtuella hårddiskar (VHD:er) som debiteras utan att tillföra värde till företaget. Skript är tillgängliga i GitHub-lagringsplatsen.
- Contoso kommer att utnyttja arbete som utförs av Microsofts IT-avdelning och överväga att implementera ARO-verktygslådan (Azure Resource Optimization).
- Contoso kan distribuera ett Azure Automation-konto med förkonfigurerade runbooks och scheman till prenumerationen och börja spara pengar. Azure-resursoptimering sker automatiskt i en prenumeration efter att ett schema har aktiverats eller skapats, inklusive optimering av nya resurser.
- Detta ger decentraliserade automatiseringsfunktioner som minskar kostnaderna. Funktionerna omfattar:
  - Automatiskt viloläge för virtuella Azure-datorer baserat på låg processoranvändning.
  - Schemalägg virtuella Azure-datorer att aktivera och avaktivera viloläget.
  - Schemalägg virtuella Azure-datorer att aktivera eller avaktivera viloläge i stigande och fallande ordning med Azure-taggar.
  - Massborttagning av resursgrupper på begäran.
- Kom igång med verktygslådan ARO i den här [GitHub-](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit)lagringsplatsen.

### <a name="partner-optimization-tools"></a>Optimeringsverktyg från partner

Partnerverktyg som [Hanu](https://hanu.com/insight) och [Scalr]( https://www.scalr.com/cost-optimization) kan användas.

## <a name="phase-4-secure-and-manage"></a>Fas 4: skydda och hantera

I den här fasen använder Contoso Azures säkerhets- och hanteringsresurser för att styra, skydda och övervaka molnappar i Azure. De här resurserna hjälper dig att köra en säker och välhanterad miljö samtidigt som du använder produkter som är tillgängliga på Azure-portalen. Contoso börjar använda de här tjänsterna under migreringen och fortsätter, med Azures hybridstöd, att använda flera av dem för att få en enhetlig upplevelse i hybridmolnet.

### <a name="security"></a>Säkerhet

Contoso förlitar sig på Azure Security Center för enhetlig säkerhetshantering och avancerat skydd mot hot i sina olika hybridmolnarbetsbelastningar.

- Med Security Center får de full synlighet och kontroll över säkerheten för molnprogram i Azure.
- Contoso kan snabbt identifiera hot och vidta åtgärder, och minska exponeringen genom att aktivera adaptivt hotskydd.

[Lär dig mer](https://azure.microsoft.com/services/security-center) om Security Center.

### <a name="monitoring"></a>Övervakning

Contoso behöver insyn i hälsa och prestanda för de nyligen migrerade apparna, infrastrukturen och data som nu kör Azure. Contoso kommer att använda inbyggda Azure-molnhanteringsverktyg som Azure Monitor, Log Analytics-arbetsytan och Application Insights.

- Med dessa verktyg kan Contoso enkelt samla in data från källor och få värdefulla insikter. Contoso kan till exempel mäta CPU-, disk- och minnesanvändning för virtuella datorer, visa program- och nätverksberoenden mellan flera VM och spåra programprestanda.
- Contoso kommer att använda dessa verktyg för molnövervakning för att vidta åtgärder och integrera med sina tjänsthanteringslösningar.
- [Läs mer](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) om Azure-övervakning.

### <a name="business-continuity-and-disaster-recovery"></a>Affärskontinuitet och haveriberedskap

Contoso behöver en strategi för affärskontinuitet och haveriberedskap (BCDR) för sina Azure-resurser.

- Azure innehåller [inbyggda BCDR-funktioner](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications) för att skydda data och hålla igång appar/tjänster.
- Förutom de inbyggda funktionerna vill Contoso se till att de kan återhämta sig efter haverier, undvika kostsamma verksamhetsavbrott, uppfylla efterlevnadsmål och skydda data mot utpressningstrojaner och den mänskliga faktorn. Gör så här:
  - Contoso distribuerar Azure Backup som en kostnadseffektiv lösning för säkerhetskopiering av Azure-resurser. Eftersom den är inbyggd kan Contoso konfigurera moln säkerhets kopieringar i några enkla steg.
  - Contoso kommer att konfigurera haveriberedskap för virtuella Azure-datorer som använder Azure Site Recovery för replikering, redundans och återställning efter fel mellan de Azure-regioner som de anger. Detta säkerställer att appar som körs på virtuella Azure-datorer är tillgängliga i en sekundär region som Contosos väljer om ett avbrott inträffar i den primära regionen. [Läs mer](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

## <a name="conclusion"></a>Slutsats

I den här artikeln planerade Contoso en Azure-migrering i stor skala. De delade in migreringsprocessen i fyra stadier. Från utvärdering och migrering till optimering, säkerhet och hantering efter att migreringen hade slutförts. Vanligtvis är det viktigt att planera ett migreringsprojekt som en fullständig process men att utföra själva migreringen inom organisationen genom att bryta ner det i klassificeringar och mängder som passar företaget. Genom att utvärdera data och tillämpa klassificeringar kan projektet delas upp i en serie mindre migreringar som kan köras på ett säkert och snabbt sätt. Summan av dessa mindre migreringar omvandlas snabbt till en stor lyckad migrering till Azure.
