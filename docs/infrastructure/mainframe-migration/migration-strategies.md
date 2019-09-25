---
title: 'Stordator-migrering: Gör växeln från stordatorer till Azure'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migrera program från stordator miljöer till Azure för system som körs i stordatorer.
author: njray
ms.author: v-nanra
ms.date: 12/26/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 8416abd3429a0dafd50eda91323eb74bfb1bf9cd
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221518"
---
# <a name="make-the-switch-from-mainframes-to-azure"></a>Gör växeln från stordatorer till Azure

Som en alternativ plattform för att köra traditionella stordator program erbjuder Azure storskalig beräkning och lagring i en miljö med hög tillgänglighet. Du får värde och flexibilitet för en modern, molnbaserad plattform utan kostnader som är kopplade till en stordator miljö.

Det här avsnittet innehåller teknisk vägledning för att göra växeln från en stordator plattform till Azure.

![Stordatorer och Azure](../../_images/mainframe-migration/make-the-switch.png)

## <a name="mips-vs-vcpus"></a>MIPS vs. virtuella processorer

Det finns ingen Universal Mapping-formel som finns för att fastställa antalet virtuella centrala bearbetnings enheter (virtuella processorer) som krävs för att köra stordator belastningar. Måttet på en miljon instruktioner per sekund (MIPS) är dock ofta mappat till virtuella processorer på Azure. MIPS mäter den övergripande beräknings kraften i en stordator genom att tillhandahålla ett konstant värde för antalet cykler per sekund för en viss dator.

En liten organisation kan kräva mindre än 500 MIPS, medan en stor organisation vanligt vis använder mer än 5 000 MIPS. Vid $1 000 per enskild MIPS tillbringar en stor organisation cirka $5 000 000 årligen för att distribuera en 5 000-MIPS-infrastruktur. Den årliga kostnads beräkningen för en typisk Azure-distribution av den här skalan är ungefär en tiondel av kostnaden för en MIPS-infrastruktur. Mer information finns i tabell 4 i [avmystifiera-migreringen från stordator till Azure](https://azure.microsoft.com/resources/demystifying-mainframe-to-azure-migration) White Paper.

En korrekt beräkning av MIPS till virtuella processorer med Azure beror på typen av vCPU och den exakta arbets belastningen som du kör. Benchmark-undersökningar ger dock en bättre beräkning av antalet och typen av virtuella processorer som du behöver. Ett nyligen HPE zREF-prestandatest ger följande uppskattningar:

- 288 MIPS per Intel-baserad kärna som körs på HP-baserade, beroende servrar för online-jobb (CICS).

- 170 MIPS per Intel Core för COBOL batch-jobb.

Den här guiden uppskattar 200 MIPS per vCPU för online-bearbetning och 100 MIPS per vCPU för batchbearbetning.

> [!NOTE]
> Dessa uppskattningar kan komma att ändras när nya serier för virtuella datorer (VM) blir tillgängliga i Azure.

## <a name="high-availability-and-failover"></a>Hög tillgänglighet och redundans

Stordator system erbjuder ofta fem nior tillgänglighet (99,999 procent) när du använder stordator koppling och parallella Sysplex. System operatörer behöver fortfarande schemalägga nedtid för underhåll och inledande program belastningar (IPLs). Den faktiska tillgängligheten närmar sig två eller tre nior, som är jämförbara med avancerade, Intel-baserade servrar.

Med hjälp av jämförelse erbjuder Azure Service nivå avtal (service avtal), där flera nior-tillgänglighet är standard, som är optimerade med lokal eller geo-baserad replikering av tjänster.

Azure ger ytterligare tillgänglighet genom att replikera data från flera lagrings enheter, antingen lokalt eller i andra geografiska regioner. I händelse av ett Azure-baserat haveri kan beräknings resurser komma åt replikerade data på antingen den lokala eller regionala nivån.

När du använder Azures PaaS-resurser (Platform as a Service), till exempel [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) och [Azure Cosmos Database](https://docs.microsoft.com/azure/cosmos-db/introduction), kan Azure automatiskt hantera redundans. När du använder Azure Infrastructure as a Service (IaaS) förlitar sig redundans på vissa systemfunktioner, till exempel SQL Server Always on-funktioner, redundanskluster och tillgänglighets grupper.

## <a name="scalability"></a>Skalbarhet

Stordatorer skalar vanligt vis upp, medan moln miljöerna skalas ut. Stordatorer kan skalas ut med hjälp av en kopplings funktion (CF), men den höga kostnaden för maskin vara och lagring gör att stordatorer blir dyra för att skala ut.

En CF erbjuder också nära sammansatta beräkningar, medan de skalbara funktionerna i Azure är löst kopplade. Molnet kan skala upp eller ned för att matcha exakta användar uppgifter, med beräknings kraft, lagring och tjänsters skalning på begäran under en användnings-baserad fakturerings modell.

## <a name="backup-and-recovery"></a>Säkerhetskopiering och återställning

Stordator kunder bevarar vanligt vis katastrof återställnings webbplatser eller använder eller en oberoende stordator leverantör för katastrof beredskap. Synkronisering med en haveri beredskaps plats sker vanligt vis genom offline-kopior av data. Båda alternativen innebär höga kostnader.

Automatisk geo-redundans är också tillgängligt via stordator kopplings funktionen, med stor kostnad och är vanligt vis reserverad för verksamhets kritiska system. Azure har däremot enkla och kostnads effektiva alternativ för [säkerhets kopiering](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup), [återställning](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)och [redundans](https://docs.microsoft.com/azure/storage/common/storage-redundancy) på lokala eller regionala nivåer eller via GEO-redundans.

## <a name="storage"></a>Storage

En del av att förstå hur stordatorer fungerar är att avkoda olika överlappande villkor. Till exempel, central lagring, Real minne, verklig lagring och huvud lagring, avser alla allmänt lagrings utrymmen direkt till stordator processorn.

Stordator maskin vara innehåller processorer och många andra enheter, till exempel Direct-Access Storage-enheter (DASDs), Magnet band enheter och flera olika typer av användar konsoler. Band och DASDs används för system funktioner och användar program.

Typer av fysisk lagring för stordatorer omfattar:

- **Central lagring:** Detta kallas även för processor eller Real lagring, som finns direkt på stordator processorn.
- **Hjälp lagring:** Den här typen innehåller lagring på DASDs och finns separat från stordatoren och kallas även för växlings lagring.

Molnet erbjuder ett antal flexibla, skalbara alternativ och du betalar bara för de alternativ som du behöver. [Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-introduction) erbjuder en massivt skalbar objekt lagring för data objekt, en fil system tjänst för molnet, ett Reliable Messaging Store och ett NoSQL-lager. För virtuella datorer, hanterade och ohanterade diskar finns beständiga, säkra disk lagring.

## <a name="mainframe-development-and-testing"></a>Utveckling och testning av stordatorer

En större driv rutin i stordator projekt är den föränderliga miljön för program utveckling. Organisationer vill att deras utvecklings miljö ska vara mer flexibel och svara på affärs behov.

Stordatorer har vanligt vis separata logiska partitioner (LPARs) för utveckling och testning, till exempel frågor och svar och mellanlagring av LPARs. Utvecklings lösningar för stordatorer innehåller kompilatorer (COBOL, PL/I, assembler) och redigerare. Det vanligaste är den interaktiva system produktivitets funktionen (ISPF) för operativ systemet z/OS som körs på IBM-stordatorer. Andra inkluderar ROSCOE Programming Facility (RPF) och Computer Associates-verktyg, till exempel CA librarian och CA-Panvalet.

Emuleringsklienter och kompilatorer är tillgängliga på x86-plattformar, så utveckling och testning kan normalt ske bland de första arbets belastningarna som migreras från en stordator till Azure. Tillgängligheten och den omfattande användningen av [DevOps-verktygen i Azure](https://azure.microsoft.com/solutions/devops) påskyndar migreringen av utvecklings-och testnings miljöer.

När lösningar utvecklas och testas på Azure och är redo att distribueras till stordatoren, måste du kopiera koden till stordatoren och kompilera den där.

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Migrering av stordator program](./application-strategies.md)
