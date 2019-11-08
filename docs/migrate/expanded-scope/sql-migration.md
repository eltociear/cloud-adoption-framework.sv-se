---
title: Påskynda migreringen genom att migrera en instans av SQL Server
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migrering av hela SQL Server instanser kan påskynda migreringen av arbetsbelastningar.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 71632e8f3f995922f4021f216f2090b742141169
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753534"
---
# <a name="accelerate-migration-by-migrating-an-instance-of-sql-server"></a>Påskynda migreringen genom att migrera en instans av SQL Server

Migrering av hela SQL Server instanser kan påskynda migreringen av arbetsbelastningar. Följande rikt linjer utökar omfånget för [Azure migration guide](../azure-migration-guide/index.md) genom att migrera en instans av SQL Server utanför en migrering för arbets belastnings fokus. Den här metoden kan dirigera migreringen av flera arbets belastningar med en enda data plattforms migrering. De flesta insatser som krävs i denna omfattnings expansion sker under förutsättningarna, utvärderingen, migreringen och optimerings processen för en migrering.

<!-- markdownlint-disable MD026 -->

## <a name="is-this-expanded-scope-right-for-you"></a>Är det här utökade omfånget rätt för dig?

Den metod som rekommenderas i [Azure migration guide](../azure-migration-guide/index.md) är att migrera varje data struktur tillsammans med associerade arbets belastningar som en del av en enda migrering. Den iterativa metoden för migrering minskar identifieringen, utvärderingen och andra uppgifter som kan skapa Blocker och långsamma affärs värdes returer.

Vissa data strukturer kan dock migreras effektivare genom en separat migrering av data plattform. Detta är några exempel:

- **Tjänstens slut:** Att snabbt flytta en SQL Server-instans för att undvika problem med tjänstens slut för ande av tjänster kan motivera användningen av den här guiden utanför standardmigreringen.
- **SQL Server tjänster:** Data strukturen är en del av en bredare lösning som kräver SQL Server som körs på en virtuell dator. Detta är vanligt för lösningar som använder SQL Server tjänster som SQL Server Reporting Services, SQL Server Integration Services eller SQL Server Analysis Services.
- **Databaser med hög densitet och låg användning:** Instansen av SQL Server har hög densitet av databaser. Var och en av dessa databaser har låga transaktions volymer och kräver en liten beräknings resurs. Du bör överväga andra, fler moderna lösningar, men en infrastruktur som en tjänst (IaaS) kan leda till betydligt lägre drifts kostnader.
- **Total ägande kostnad:** När det är tillämpligt kan du använda [Azure Hybrid-förmåner](https://azure.microsoft.com/pricing/hybrid-benefit) för List priset för att skapa den lägsta ägande kostnaden för instanser av SQL Server. Detta är särskilt vanligt för kunder som är värdar för SQL Server i multimolns scenarier.
- **Migration Accelerator:** Migrering av en SQL Server instans av en instans kan flytta flera databaser i en iteration. Den här metoden gör ibland att framtida iterationer kan fokusera mer specifikt på program och virtuella datorer, vilket innebär att du kan migrera fler arbets belastningar i en enda iteration.
- **VMware-migrering:** En gemensam lokal arkitektur omfattar program och virtuella datorer på en virtuell värd och databaser på Bare Metal. I det här scenariot kan du migrera hela SQL Server instanser för att stödja migrering av VMware-värden till Azure VMware-tjänsten. Mer information finns i [migrering av VMware-värdar](./vmware-host.md).

Om inget av ovanstående villkor gäller för migreringen kan det vara bäst att fortsätta med [standard processen för migrering](../index.md). I standard processen migreras data strukturer iterativt, tillsammans med varje arbets belastning.

Om den här guiden överensstämmer med dina kriterier fortsätter du med den här utökade omfattnings guiden som en ansträngning inom [standard processen för migrering](../index.md). Under förutsättnings fasen kan du integrera arbetet i den övergripande implementerings planen.

## <a name="suggested-prerequisites"></a>Föreslagna förutsättningar

Innan du utför en SQL Server migrering börjar du med en expansion av den digitala fastigheten genom att inkludera en datafastighet. Datafastigheten registrerar en inventering av de data till gångar som du överväger för migrering. Följande tabeller beskriver en metod för att registrera datafastigheten.

### <a name="server-inventory"></a>Server lager

Följande är ett exempel på en server inventering:

|SQL Server|Syfte|Version|[Allvarlighets grad](../../manage/considerations/criticality.md)|[Normal](../../govern/policy-compliance/data-classification.md)|Antal databaser|SSIS|SSRS|SSAS|Kluster|Antal noder|
|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|SQL-01|Kärn appar|2016|Verksamhetskritiskt|Mycket konfidentiellt|40|Gäller inte|Gäller inte|Gäller inte|Ja|3|
|SQL-02|Kärn appar|2016|Verksamhetskritiskt|Mycket konfidentiellt|40|Gäller inte|Gäller inte|Gäller inte|Ja|3|
|SQL-03|Kärn appar|2016|Verksamhetskritiskt|Mycket konfidentiellt|40|Gäller inte|Gäller inte|Gäller inte|Ja|3|
|SQL-04|BI|2012|Hög|XX|6|Gäller inte|Sekretesskydd|Ja – flerdimensionell kub|Nej|1|
|SQL-05|Integrering|2008 R2|Låg|Allmänt|20|Ja|Gäller inte|Gäller inte|Nej|1|

### <a name="database-inventory"></a>Databas inventering

Följande är ett exempel på en databas inventering för en av servrarna ovan:

|Server|Databas|[Allvarlighets grad](../../manage/considerations/criticality.md)|[Normal](../../govern/policy-compliance/data-classification.md)|Data Migration Assistant resultat (DMA)|DMA-reparation|Mål plattform|
|---------|---------|---------|---------|---------|---------|---------|
|SQL-01|DB-1|Verksamhetskritiskt|Mycket konfidentiellt|Överensstämmelse|Gäller inte|Azure SQL Database|
|SQL-01|DB-2|Hög|Sekretesskydd|Schema ändring krävs|Genomförda ändringar|Azure SQL Database|
|SQL-01|DB-1|Hög|Allmänt|Överensstämmelse|Gäller inte|Azure SQL-hanterad instans|
|SQL-01|DB-1|Låg|Mycket konfidentiellt|Schema ändring krävs|Schemalagda ändringar|Azure SQL-hanterad instans|
|SQL-01|DB-1|Verksamhetskritiskt|Allmänt|Överensstämmelse|Gäller inte|Azure SQL-hanterad instans|
|SQL-01|DB-2|Hög|Sekretesskydd|Överensstämmelse|Gäller inte|Azure SQL Database|

### <a name="integration-with-the-cloud-adoption-plan"></a>Integrering med moln implementerings planen

När den här identifierings processen är klar kan du ta med den i [moln implementerings planen](../../plan/template.md). I moln implementerings planen lägger du till varje SQL Server instans som ska migreras som en [distinkt arbets belastning](../../plan/workloads.md). Inom varje arbets belastning kan databaserna och tjänsterna (SSIS, SSAS, SSRS) läggas till som [till gångar](../../plan/workloads.md). Information om hur du lägger till arbets belastningar och till gångar i bulk till implementerings planen finns i [lägga till och redigera arbets objekt med Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

När arbets belastningarna och resurserna ingår i planen kan du och ditt team fortsätta med en standard process för migrering med hjälp av implementerings planen. När implementerings gruppen flyttas till utvärderings-, migrerings-och optimerings processerna kan du gå igenom ändringarna som beskrivs i följande avsnitt.

## <a name="assessment-process-changes"></a>Ändringar i utvärderings processen

Om en databas i planen kan migreras till en plattform som en tjänst (PaaS)-data plattform använder du DMA för att utvärdera kompatibiliteten för den valda databasen. När databasen kräver schema konvertering bör du slutföra dessa konverteringar som en del av utvärderings processen för att undvika avbrott i pipelinen för migrering.

### <a name="suggested-action-during-the-assessment-process"></a>Föreslagen åtgärd under utvärderings processen

För databaser som kan migreras till en PaaS-lösning slutförs följande åtgärder under utvärderings processen.

- **Utvärdera med DMA:** Använd Data Migration Assistant för att identifiera kompatibilitetsproblem som kan påverka databas funktionen i mål Azure SQL Database Hanterad instans. Använd DMA för att rekommendera förbättringar av prestanda och tillförlitlighet, och för att flytta schema, data och objekt som inte har inkluderats från käll servern till mål servern. Mer information finns i [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview).
- **Åtgärda och konvertera:** Konvertera dataschemat för data baserat på utdata från DMA för att åtgärda kompatibilitetsproblem. Testa det konverterade dataschemat med de beroende programmen.

## <a name="migrate-process-changes"></a>Ändringar i migreringsprocessen

Under migreringen kan du välja bland många olika verktyg och metoder. Men varje metod följer en enkel process: Migrera schema, data och objekt. Synkronisera sedan data till mål data källan.

Målet och källan för data strukturen och tjänsterna kan göra dessa två steg i stället komplicerade. Följande avsnitt hjälper dig att förstå det bästa verktygs valet, baserat på dina beslut om migrering.

### <a name="suggested-action-during-the-migrate-process"></a>Föreslagna åtgärder under migreringsprocessen

Den föreslagna sökvägen för migrering och synkronisering använder en kombination av följande tre verktyg. I följande avsnitt beskrivs mer komplexa alternativ för migrering och synkronisering som möjliggör en bredare mängd olika mål-och käll lösningar.

|Migrations alternativ|Syfte|
|---------|---------|
|[Azure Database Migration Service](https://docs.microsoft.com/sql/dma/dma-overview)|Har stöd för online (minimal nedtid) och offline (en gång) migreringar i skala till en Azure SQL Database Hanterad instans. Stöder migrering från: SQL Server 2005, SQL Server 2008 och SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 och SQL Server 2017.|
|[Transaktionsreplikering](https://docs.microsoft.com/sql/relational-databases/replication/administration/enhance-transactional-replication-performance)|Transaktionsreplikering till en Azure SQL Database Hanterad instans stöds för migreringar från: SQL Server 2012 (SP2 CU8, SP3 eller senare), SQL Server 2014 (RTM CU10 eller senare eller SP1 CU3 eller senare), SQL Server 2016, SQL Server 2017.|
|[Mass inläsning](https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql)|Använd Mass inläsning till en Azure SQL Database Hanterad instans för data som lagras i: SQL Server 2005, SQL Server 2008 och SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 och SQL Server 2017.|

### <a name="guidance-and-tutorials-for-suggested-migration-process"></a>Vägledning och självstudier för föreslagen migreringsprocessen

Att välja den bästa vägledningen för migrering genom att använda Azure Database Migration Service är beroende av den källa och mål plattform som du väljer. Följande tabell länkar till självstudier för var och en av standard metoderna för att migrera en SQL-databas med hjälp av Azure Database Migration Service.

|Källa  |Målinrikta  |Verktyg  |Typ av migrering  |Vägledning  |
|---------|---------|---------|---------|---------|
|SQL Server|Azure SQL Database|Database Migration Service|Anslutningen|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|SQL Server|Azure SQL Database|Database Migration Service|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|SQL Server|Hanterad Azure SQL Database-instans|Database Migration Service|Anslutningen|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|SQL Server|Hanterad Azure SQL Database-instans|Database Migration Service|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|RDS-SQL Server|Azure SQL Database (eller hanterad instans)|Database Migration Service|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|

### <a name="guidance-and-tutorials-for-various-services-to-equivalent-paas-solutions"></a>Vägledning och självstudier för olika tjänster till motsvarande PaaS-lösningar

När du har flyttat databaser från en instans av SQL Server till Azure Database Migration Service kan schemat och data vara värd för i ett antal PaaS-lösningar. Andra nödvändiga tjänster kan dock fortfarande köras på den servern. Följande tre självstudier hjälper dig att flytta SSIS, SSAS och SSRS till motsvarande PaaS-tjänster på Azure.

|Källa  |Målinrikta  |Verktyg  |Typ av migrering  |Vägledning  |
|---------|---------|---------|---------|---------|
|SQL Server Integration Services|Azure Data Factory integration runtime|Azure Data Factory|Anslutningen|[Självstudie](https://docs.microsoft.com/azure/data-factory/create-azure-ssis-integration-runtime)|
|SQL Server Analysis Services tabell modell|Azure Analysis Services|SQL Server Data Tools|Anslutningen|[Självstudie](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)|
|SQL Server Reporting Services|Power BI-rapportserver|Power BI|Anslutningen|[Självstudie](https://docs.microsoft.com/power-bi/report-server/migrate-report-server)|

### <a name="guidance-and-tutorials-for-migration-from-sql-server-to-an-iaas-instance-of-sql-server"></a>Vägledning och självstudier för migrering från SQL Server till en IaaS-instans av SQL Server

När du har migrerat databaser och tjänster till PaaS-instanser kan du fortfarande ha data strukturer och tjänster som inte är PaaS-kompatibla. När befintliga begränsningar förhindrar migrering av data strukturer eller tjänster, kan följande självstudie hjälpa till med migrering av olika till gångar i data portföljen till Azure IaaS-lösningar.

Använd den här metoden för att migrera databaser eller andra tjänster på instansen av SQL Server.

|Källa  |Målinrikta  |Verktyg  |Typ av migrering  |Vägledning  |
|---------|---------|---------|---------|---------|
|Enskild instans SQL Server|SQL Server på IaaS|Anpassa|Anslutningen|[Självstudie](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)|

## <a name="optimization-process-changes"></a>Ändringar i optimerings processen

Under optimeringen kan du testa, optimera och befordra till produktion av varje data struktur, tjänst eller SQL Server instans. Detta är den största effekten av deviating från en migrering per arbets belastnings modell.

Vi rekommenderar att du migrerar beroende arbets belastningar, program och virtuella datorer inom samma iteration som SQL Server-instansen. När det idealiska scenariot inträffar kan du testa arbets belastningen tillsammans med data källan. Efter testning kan du befordra data strukturen till produktion och avsluta synkroniseringsprocessen.

Nu ska vi ta en titt på scenariot där det finns en betydande tids lucka mellan migreringen av databasen och migrering av arbets belastning. Det kan tyvärr vara den största ändringen i optimerings processen under en icke-arbetsstyrd migrering. När du migrerar flera databaser som en del av en SQL Server migreringen kan dessa databaser finnas i både molnet och lokalt, för flera iterationer. Under den tiden måste du underhålla datasynkroniseringen tills dessa beroende till gångar migreras, testas och befordras.

Tills alla beroende arbets belastningar har uppgraderats ansvarar du och ditt team för att stödja synkronisering av data från käll systemet till mål systemet. Den här synkroniseringen förbrukar nätverks bandbredd, moln kostnader och viktigast av folk tid. Lämplig justering av implementerings planen för arbets belastningen SQL Server migrering, och alla beroende arbets belastningar och program, kan minska den dyra omkostnaderna.

### <a name="suggested-action-during-the-optimization-process"></a>Föreslagen åtgärd under optimerings processen

Under optimerings processerna utför du följande uppgifter varje iteration, tills alla data strukturer och tjänster har befordrats till produktion.

1. Verifiera synkronisering av data.
2. Testa alla migrerade program.
3. Optimera program-och data strukturen för att justera kostnaderna.
4. Marknadsför programmen till produktion.
5. Testa för fortsatt lokal trafik mot den lokala databasen.
6. Avsluta synkroniseringen av data som befordras till produktion.
7. Avsluta den ursprungliga käll databasen.

Du kan inte avsluta databaser och synkronisering förrän steg 5 har passerat. Tills alla databaser på en instans av SQL Server har gått igenom alla sju stegen bör du behandla den lokala instansen av SQL Server som produktion. All synkronisering ska vara kvar.

## <a name="next-steps"></a>Nästa steg

Gå tillbaka till [checklistan för utökat omfång](./index.md) och se till att din migreringsmetod är helt anpassad till kraven.

> [!div class="nextstepaction"]
> [Utökad checklista](./index.md)
