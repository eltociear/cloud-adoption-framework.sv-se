---
title: Överflyttnings strategier för stordator program
description: Lär dig strategier som att byta värd för, ta bort, återskapa eller ersätta appar för att migrera från stordator miljöer till Azure.
author: njray
ms.author: v-nanra
ms.date: 12/26/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: e0823eef01a2966459a10293c25d877b1c732c64
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80425815"
---
<!-- cSpell:ignore njray nanra Attunity Codit DRDA ISAM ISQL LPARS VSAM ODBC JDBC GDGs REXX dbextents Raincode Tmax -->

# <a name="mainframe-application-migration"></a>Migrering av program från stordatorer

När du migrerar program från stordator miljöer till Azure följer de flesta team en Pragmatic-metod: Återanvänd var och när det är möjligt och starta sedan en stegvis distribution där program skrivs om eller ersätts.

Programmigreringen omfattar vanligt vis en eller flera av följande strategier:

- **Rehost:** Du kan flytta befintliga kod, program och program från stordatoren och sedan kompilera om koden så att den körs i en stordator-emulator som finns i en moln instans. Den här metoden börjar normalt med att flytta program till en molnbaserad emulator och sedan migrera databasen till en molnbaserad databas. Vissa tekniker och omfactoring krävs tillsammans med data-och fil versioner.

    Alternativt kan du vara värd för med hjälp av en traditionell värd leverantör. En av de huvudsakliga fördelarna med molnet är att lägga ut infrastruktur hantering. Du kan hitta en data Center leverantör som ska vara värd för dina stordator belastningar. Den här modellen kan köpa tid, minska leverantörs låset och skapa interimistiska kostnads besparingar.

- **Dra tillbaka:** Alla program som inte längre behövs bör dras tillbaka innan migreringen.

- **Återskapa:** Vissa organisationer väljer att helt skriva om program med modern teknik. Med tanke på den extra kostnaden och komplexiteten i den här metoden är det inte lika vanligt som en hiss och Skift-metod. Ofta efter den här typen av migrering är det klokt att börja ersätta moduler och kod med hjälp av kod omvandlings motorer.

- **Ersätt:** Den här metoden ersätter stordator funktioner med motsvarande funktioner i molnet. Program vara som en tjänst (SaaS) är ett alternativ, som använder en lösning som skapats specifikt för ett företags problem, till exempel ekonomi, personal, produktion eller företags resurs planering. Dessutom är många branschspecifika appar tillgängliga för att lösa problem med anpassade stordator lösningar som används för att lösa problemet tidigare.

Du bör börja med att planera de arbets belastningar som du vill migrera och sedan fastställa dessa krav för att flytta associerade program, äldre kod baser och databaser.

## <a name="mainframe-emulation-in-azure"></a>Stordator emulering i Azure

Azure Cloud Services kan emulera traditionella stordator miljöer, så att du kan återanvända befintlig stordator kod och program. Vanliga Server komponenter som du kan emulera inkluderar OLTP (Online Transaction Processing), batch och data inmatnings system.

### <a name="oltp-systems"></a>OLTP-system

Många stordatorer har OLTP-system som bearbetar tusentals eller miljon tals uppdateringar för ett stort antal användare. Dessa program använder ofta transaktions bearbetnings-och skärm formulär hanterings program, till exempel CICS (Customer Control system), informations hanterings system (IMS) och Terminal Interface-processor (TIP).

När du flyttar OLTP-program till Azure, är emulatorer för system övervakaren för stordatorer (transaktions bearbetning) tillgängliga för körning som infrastruktur som en tjänst (IaaS) med hjälp av virtuella datorer (VM) i Azure. Skärm hanterings-och formulär funktionerna kan också implementeras av webb servrar. Den här metoden kan kombineras med databas-API: er, till exempel ActiveX Data Objects (ADO), Open Database Connectivity (ODBC) och Java Database Connectivity (JDBC) för data åtkomst och transaktioner.

### <a name="time-constrained-batch-updates"></a>Tidsbegränsade batch-uppdateringar

Många stordator system utför månatliga eller årliga uppdateringar av miljon tals konto poster, till exempel sådana som används i bank-, försäkrings-och myndighets sektorn. Stordatorer hanterar dessa typer av arbets belastningar genom att erbjuda data hanterings system med stora data flöden. Batch-jobb i stordatorer är vanligt vis seriella och är beroende av de in-/utdata-åtgärder per sekund (IOPS) som tillhandahålls av stordator stamnät för prestanda.

I molnbaserade batch-miljöer används parallell beräkning och snabba nätverk för prestanda. Om du behöver optimera batch-prestanda tillhandahåller Azure olika alternativ för beräkning, lagring och nätverk.

### <a name="data-ingestion-systems"></a>Data inmatnings system

Stordatorer inhämtar stora batchar av data från detalj handel, finansiella tjänster, tillverkning och andra lösningar för bearbetning. Med Azure kan du använda enkla kommando rads verktyg som [AzCopy](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy) för att kopiera data till och från lagrings platsen. Du kan också använda [Azure Data Factory](https://docs.microsoft.com/azure/data-factory/introduction) tjänsten, så att du kan mata in data från olika data lager för att skapa och schemalägga data drivna arbets flöden.

Förutom emuleringsenheter tillhandahåller Azure plattform som en tjänst (PaaS) och analys tjänster som kan förbättra befintliga stordator miljöer.

## <a name="migrate-oltp-workloads-to-azure"></a>Migrera OLTP-arbetsbelastningar till Azure

Det går inte att använda alternativet för att lyfta och flytta befintliga program till Azure. Varje program migreras i befintligt skick, vilket ger fördelarna med molnet utan risker eller kostnader för att göra kod ändringar. Användning av en emulator för transaktions bearbetning av stordatorer (TP) i Azure har stöd för den här metoden.

TP-övervakare är tillgängliga från olika leverantörer och körs på virtuella datorer, ett IaaS-alternativ (Infrastructure as a Service) på Azure. I följande före och efter-diagram visas en migrering av ett online-program som backas upp av IBM DB2, ett Relations databas hanterings system (DBMS) på en IBM z/OS-stordator. DB2 för z/OS använder VSAM-filer (Virtual Storage Access Method) för att lagra data och indexerad sekventiell åtkomst metod (ISAM) för flata filer. Den här arkitekturen använder också CICS för transaktions övervakning.

!["Lyft och Shift" migrering av en stordator miljö till Azure med hjälp av emulering](../../_images/mainframe-migration/mainframe-vs-azure.png)

I Azure används emuleringsklienter för att köra TP Manager och de batch-jobb som använder JCL. I data skiktet ersätts DB2 av [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview), även om Microsoft SQL Server, DB2 LUW eller Oracle Database också kan användas. En emulator stöder IMS, VSAM och SEQ. Stordator system hanterings verktyg ersätts av Azure-tjänster och program vara från andra leverantörer som körs i virtuella datorer.

Funktionerna för skärm hantering och formulär inmatning implementeras ofta med hjälp av webb servrar, som kan kombineras med databas-API: er, till exempel ADO, ODBC och JDBC för data åtkomst och transaktioner. Exakt vilken rad med Azure IaaS-komponenter som ska användas beror på vilket operativ system du föredrar. Exempel:

- Windows-baserade virtuella datorer: IIS (Internet Information Server) tillsammans med ASP.NET för skärm hantering och affärs logik. Använd ADO.NET för data åtkomst och transaktioner.

- Linux-baserade virtuella datorer: Java-baserade program servrar som är tillgängliga, till exempel Apache Tomcat för skärm hantering och Java-baserade företags funktioner. Använd JDBC för data åtkomst och transaktioner.

## <a name="migrate-batch-workloads-to-azure"></a>Migrera batch-arbetsbelastningar till Azure

Batch-åtgärder i Azure skiljer sig från den typiska batch-miljön i stordatorer. Stordator jobb är vanligt vis seriella och är beroende av IOPS från stordator stamnät för prestanda. I molnbaserade batch-miljöer används parallell data behandling och höghastighets nätverk för prestanda.

Du kan optimera batch-prestanda med hjälp av Azure genom att tänka på [beräknings](https://docs.microsoft.com/azure/virtual-machines/windows/overview)-, [lagrings](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction)-, [nätverks](https://azure.microsoft.com/blog/maximize-your-vm-s-performance-with-accelerated-networking-now-generally-available-for-both-windows-and-linux)-och [övervaknings](https://docs.microsoft.com/azure/azure-monitor/overview) alternativen enligt följande.

### <a name="compute"></a>Compute

Använd

- Virtuella datorer med högsta klock hastighet. Stordator program är ofta en enkel tråds processor och stordatorer har en mycket hög klock frekvens.

- Virtuella datorer med stor minnes kapacitet för att tillåta cachelagring av data och program arbets områden.

- Virtuella datorer med högre densitet virtuella processorer för att dra nytta av flertrådad bearbetning om programmet har stöd för flera trådar.

- Parallell bearbetning kan i Azure skalas enkelt för parallell bearbetning, vilket ger mer beräknings kraft för en batch-körning.

### <a name="storage"></a>Storage

Använd

- [Azure Premium SSD](https://docs.microsoft.com/azure/virtual-machines/windows/premium-storage) eller [Azure Ultra SSD](https://docs.microsoft.com/azure/virtual-machines/windows/disks-ultra-ssd) för maximal tillgänglig IOPS.

- Stripning med flera diskar för fler IOPS per lagrings storlek.

- Partitionering för lagring för att sprida IO över flera Azure Storage-enheter.

### <a name="networking"></a>Nätverk

- Använd [Azure-accelererat nätverk](https://docs.microsoft.com/azure/virtual-network/create-vm-accelerated-networking-powershell) för att minimera svars tiden.

### <a name="monitoring"></a>Övervakning

- Använd övervaknings verktyg, [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview), [Azure Application insikter](https://docs.microsoft.com/azure/application-insights/app-insights-overview)och Azure-loggar gör det möjligt för administratörer att övervaka alla över prestanda för batch-körningar och bidra till att eliminera Flask halsar.

## <a name="migrate-development-environments"></a>Migrera utvecklings miljöer

Molnets distribuerade arkitekturer förlitar sig på en annan uppsättning utvecklingsverktyg som ger fördelen med modern praxis och programmeringsspråk. För att under lätta den här över gången kan du använda en utvecklings miljö med andra verktyg som är utformade för att emulera IBM z/OS-miljöer. I följande lista visas alternativ från Microsoft och andra leverantörer:

| Komponent        | Azure-alternativ                                                                                                                                  |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| z/OS             | Windows, Linux eller UNIX                                                                                                                      |
| CICS             | Azure-tjänster som erbjuds av Micro Focus, Oracle, GT Software (Fujitsu), TmaxSoft, Raincode och NTT data eller omskrivning med Kubernetes |
| IMS              | Azure-tjänster som erbjuds av Micro Focus och Oracle                                                                                  |
| Assembler        | Azure-tjänster från Raincode och TmaxSoft; eller COBOL, C eller Java, eller mappa till operativ system funktioner               |
| JCL              | JCL, PowerShell eller andra skript verktyg                                                                                                   |
| COBOL            | COBOL, C eller Java                                                                                                                            |
| Fysiska          | Naturlig, COBOL, C eller Java                                                                                                                  |
| FORTRAN och PL/I | FORTRAN, PL/I, COBOL, C eller Java                                                                                                           |
| REXX och PL/I    | REXX, PowerShell eller andra skript verktyg                                                                                                  |

## <a name="migrate-databases-and-data"></a>Migrera databaser och data

Programmigreringen innebär vanligt vis att vara värd för data nivån. Du kan migrera SQL Server, öppen källkod och andra Relations databaser till fullständigt hanterade lösningar i Azure, till exempel [Azure SQL Database Hanterad instans](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), [Azure Database Service för postgresql](https://docs.microsoft.com/azure/postgresql/overview)och [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) med [Azure Database migration service](https://docs.microsoft.com/azure/dms/dms-overview).

Du kan till exempel migrera om data nivån stordator använder:

- IBM DB2 eller en IMS-databas, Använd Azure SQL Database, SQL Server, DB2 LUW eller Oracle Database på Azure.

- VSAM och andra flata filer använder du filer med indexerad sekventiell åtkomst metod (ISAM) för Azure SQL, SQL Server, DB2 LUW eller Oracle.

- Generations datum grupper (GDGs), migrera till filer på Azure som använder en namngivnings konvention och fil namns tillägg som tillhandahåller liknande funktioner som GDGs.

IBM-datanivån innehåller flera viktiga komponenter som du även måste migrera. När du till exempel migrerar en databas, migrerar du även en samling data som finns i pooler, som innehåller dbextents, som är data uppsättningar i z/OS-VSAM. Migreringen måste innehålla katalogen som identifierar data platser i lagringspooler. Dessutom måste migreringen ta hänsyn till databas loggen, som innehåller en post med åtgärder som utförs på databasen. En databas kan ha en, två (dubbla eller alternativa) eller fyra (dubbla och alternativa) loggar.

Migreringen av databasen omfattar även dessa komponenter:

- **Databas hanteraren:** Ger åtkomst till data i databasen. Databas hanteraren körs i en egen partition i en z/OS-miljö.
- **Program beställare:** Accepterar begär Anden från program innan de skickas till en program Server.
- **Online-resurs kort:** Innehåller komponenter för programbegäran som används i CICS transaktioner.
- **Batch-resurs kort:** Implementerar komponenter för programbegäran för batch-program för z/OS.
- **Interaktiv SQL (ISQL):** Körs som ett CICS program och gränssnitt som gör det möjligt för användare att ange SQL-uttryck eller operator kommandon.
- **CICS-program:** Körs under kontrollen av CICS med tillgängliga resurser och data källor i CICS.
- **Batch-program:** Kör process logik utan interaktiv kommunikation med användare till, till exempel att skapa Mass data uppdateringar eller generera rapporter från en databas.

## <a name="optimize-scale-and-throughput-for-azure"></a>Optimera skalning och data flöde för Azure

I allmänhet skalar stordatorer upp, medan molnet skalas ut. För att optimera skalning och data flöde i stordator program som körs på Azure är det viktigt att du förstår hur stordatorer kan separera och isolera program. En-stordator i z/OS använder en funktion som kallas logiska partitioner (LPARS) för att isolera och hantera resurser för ett visst program på en enda instans.

En stordator kan till exempel använda en logisk partition (LPAR) för en CICS-region med tillhör ande COBOL-program och en separat LPAR för DB2. Ytterligare LPARs används ofta för utveckling, testning och mellanlagrings miljöer.

I Azure är det vanligare att använda separata virtuella datorer för det här ändamålet. Azure-arkitekturer distribuerar vanligt vis virtuella datorer för program nivån, en separat uppsättning virtuella datorer för data nivån, en annan uppsättning för utveckling och så vidare. Varje nivå av bearbetning kan optimeras med den lämpligaste typen av virtuella datorer och funktioner i den miljön.

Dessutom kan varje nivå även tillhandahålla lämpliga haveri beredskaps tjänster. Till exempel kan virtuella datorer och databaser kräva en frekvent eller varm återställning, medan de virtuella datorerna i utvecklings-och testnings miljön stöder en kall återställning.

Följande bild visar en möjlig Azure-distribution med hjälp av en primär och en sekundär plats. På den primära platsen distribueras produktion, mellanlagring och testning av virtuella datorer med hög tillgänglighet. Den sekundära platsen är för säkerhets kopiering och haveri beredskap.

![En möjlig Azure-distribution med hjälp av en primär och en sekundär plats](../../_images/mainframe-migration/migration-backup-dr.png)

## <a name="perform-a-staged-mainframe-to-azure"></a>Utföra en mellanlagrad stordator till Azure

Att flytta lösningar från en stordator till Azure kan omfatta en *mellanlagrad* migrering, vilket innebär att vissa program flyttas först och att andra finns kvar i stordatoren tillfälligt eller permanent. Den här metoden kräver vanligt vis system som gör det möjligt för program och databaser att samverka mellan stordatorer och Azure.

Ett vanligt scenario är att flytta ett program till Azure samtidigt som du behåller data som används av programmet på stordatoren. En speciell program vara används för att aktivera program på Azure för att komma åt data från stordatoren. Lyckligt vis erbjuder en mängd olika lösningar integrering mellan Azure och befintliga stordator miljöer, stöd för Hybrid scenarier och migrering över tid. Microsoft-partner, oberoende program varu leverantörer och system integrerare kan hjälpa dig på resan.

Ett alternativ är [Microsoft Host Integration Server](https://docs.microsoft.com/host-integration-server), en lösning som tillhandahåller den distribuerade Relations databas arkitekturen (DRDA) som krävs för att program i Azure ska kunna komma åt data i DB2 som finns kvar i stordatoren. Andra alternativ för stordator-till-Azure-integrering innehåller lösningar från IBM, Attunity, Codit, andra leverantörer och alternativ för öppen källkod.

## <a name="partner-solutions"></a>Partnerlösningar

Om du överväger en stordator-migrering är partner eko systemet tillgängligt för att hjälpa dig.

Azure tillhandahåller en beprövad, hög tillgänglig och skalbar infrastruktur för system som för närvarande körs på stordatorer. Vissa arbets belastningar kan migreras med relativt enkelt. Andra arbets belastningar som är beroende av äldre systemprogram, till exempel CICS och IMS, kan reageras med partner lösningar och migreras till Azure över tid. Oavsett vilket alternativ du gör är Microsoft och våra partner tillgängliga för att hjälpa dig att optimera för Azure samtidigt som program varu funktionerna i stordator systemet upprätthålls.

## <a name="learn-more"></a>Läs mer

Mer information finns i följande resurser:

- [Kom igång med Azure](https://docs.microsoft.com/azure)

- [Distribuera IBM DB2 pureScale på Azure](https://azure.microsoft.com/resources/deploy-ibm-db2-purescale-on-azure)

- [Dokumentation om Host Integration Server](https://docs.microsoft.com/host-integration-server)
