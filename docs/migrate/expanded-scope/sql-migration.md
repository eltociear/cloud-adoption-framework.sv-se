---
title: Påskynda migreringen med en SQL-migrering
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Påskynda migreringen med en SQL-migrering
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4af94af91874ac666f45a917eed003b3cf881c51
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558225"
---
# <a name="accelerate-migration-with-a-sql-migration"></a>Påskynda migreringen med en SQL-migrering

Migrering av hela SQL Server instanser kan påskynda migreringen av arbetsbelastningar. Följande rikt linjer visar omfånget för [Azure migration guide](../azure-migration-guide/index.md) genom att migrera en SQL Server utanför en migrering för arbets belastnings fokus. Den här metoden kan dirigera migreringen av flera arbets belastningar med en enda data plattforms migrering.

## <a name="general-scope-expansion"></a>Allmän omfångsutökning

De flesta av de ansträngningar som krävs i denna omfattnings expansion sker under förutsättningarna, utvärderingen, migreringen och optimerings processen för en migrering.

<!-- markdownlint-disable MD026 -->

## <a name="is-this-expanded-scope-right-for-you"></a>Är det här utökade omfånget rätt för dig?

Den rekommenderade metoden som beskrivs i [Azure migration guide](../azure-migration-guide/index.md) är att migrera varje data struktur tillsammans med associerade arbets belastningar som en del av en enda migrering. Den iterativa metoden för migrering minskar identifieringen, utvärderingen och andra uppgifter som kan skapa Blocker och långsamma affärs värdes returer.

Vissa data strukturer kan dock migreras effektivare genom en separat migrering av data plattform. Följande är några exempel som kan leda till att den här utökade omfattnings vägledningen används:

- **Tjänstens slut:** Att snabbt flytta en SQL Server-instans för att undvika problem med tjänstens slut för ande av tjänster kan leda till att den här guiden används utanför standard åtgärder för migrering.
- **SQL Server tjänster:** Data strukturen är en del av en bredare lösning som kräver SQL Server som körs på en virtuell dator. Detta är vanligt för lösningar som utnyttjar SQL Server tjänster som SQL Server Reporting Services, SQL Server Integration Services eller SQL Server Analysis Services.
- **Databaser med hög densitet och låg användning:** SQL Server har hög densitet av databaser. Var och en av dessa databaser har låga transaktions volymer och kräver lite beräknings resurser. Andra moderna lösningar bör övervägas, men en IaaS metod kan leda till betydligt lägre drifts kostnader.
- **Total ägande kostnad:** I förekommande fall kan [Azure Hybrid-förmåner](https://azure.microsoft.com/pricing/hybrid-benefit) användas på list priset för att skapa den lägsta ägande kostnaden för SQL-servrar. Detta är särskilt vanligt för kunder som är värdar för SQL Server i multimolns scenarier.
- **Migration Accelerator:** Lyft och Shift-migrering av en SQL Server instans kan flytta flera databaser i en iteration. Den här metoden gör ibland att framtida iterationer kan fokusera mer specifikt på program och virtuella datorer och migrera fler arbets belastningar i en enda iteration.
- **VMware-migrering:** En gemensam lokal arkitektur omfattar program och virtuella datorer på en virtuell värd och databaser på Bare Metal. När du migrerar den här gemensamma arkitekturen kan migreringen av VMWare-värden till Azure VMWare service (AVS) kompletteras av den här guiden för att migrera hela SQL Server instanser för att stödja de virtuella värdarna. Mer kostnads fri vägledning finns i [migrering av VMware-värdar](./vmware-host.md).

Om inget av ovanstående villkor gäller för migreringen kan det vara bäst att fortsätta med [standard processen för migrering](../index.md). I standard processen migreras data strukturer iterativt tillsammans med varje arbets belastning.

Om den här guiden överensstämmer med dina kriterier fortsätter du med den här utökade omfattnings guiden som en ansträngning inom [standard processen för migrering](../index.md). Under förutsättnings fasen kan arbets insatsen integreras i den övergripande implementerings planen.

## <a name="suggested-prerequisites"></a>Föreslagna förutsättningar

Innan du utför en SQL Server migrering börjar du med en expansion av den **digitala fastigheten** genom att inkludera en datafastighet. Datafastigheten registrerar en inventering av data till gångarna som ska migreras. Följande tabeller beskriver en metod för att registrera datafastigheten.

### <a name="server-inventory"></a>Server lager

Följande är ett exempel på en server inventering för SQL-servrar:

|SQL Server|Syfte|Version|[Allvarlighets grad](../../manage/considerations/criticality.md)|[Normal](../../govern/policy-compliance/data-classification.md)|Antal databaser|SSIS|SSRS|SSAS|Kluster|Antal noder|
|---------|---------|---------|---------|---------|---------|---------|---------|
|SQL-01|Kärn appar|2016|Verksamhets kritisk|Mycket konfidentiellt|40|Gäller inte|Gäller inte|Gäller inte|Ja|3|
|SQL-02|Kärn appar|2016|Verksamhets kritisk|Mycket konfidentiellt|40|Gäller inte|Gäller inte|Gäller inte|Ja|3|
|SQL-03|Kärn appar|2016|Verksamhets kritisk|Mycket konfidentiellt|40|Gäller inte|Gäller inte|Gäller inte|Ja|3|
|SQL-04|BI|2012|Hög|XX|6|Gäller inte|Sekretesskydd|Ja – flerdimensionell kub|Nej|1|
|SQL-05|Integrering|2008 R2|Låg|Allmänt|20|Ja|Gäller inte|Gäller inte|Nej|1|

### <a name="database-inventory"></a>Databas inventering

Följande är ett exempel på en databas inventering för en av SQL-servrarna ovan:

|Server|Databas|[Allvarlighets grad](../../manage/considerations/criticality.md)|[Normal](../../govern/policy-compliance/data-classification.md)|DMA-resultat|DMA-reparation|Mål plattform|
|---------|---------|---------|---------|---------|---------|---------|
|SQL-01|DB-1|Verksamhets kritisk|Mycket konfidentiellt|Överensstämmelse|Gäller inte|Azure SQL Database|
|SQL-01|DB-2|Hög|Sekretesskydd|Schema ändring krävs|Genomförda ändringar|Azure SQL Database|
|SQL-01|DB-1|Hög|Allmänt|Överensstämmelse|Gäller inte|Hanterad Azure SQL-instans|
|SQL-01|DB-1|Låg|Mycket konfidentiellt|Schema ändring krävs|Schemalagda ändringar|Hanterad Azure SQL-instans|
|SQL-01|DB-1|Verksamhets kritisk|Allmänt|Överensstämmelse|Gäller inte|Hanterad Azure SQL-instans|
|SQL-01|DB-2|Hög|Sekretesskydd|Överensstämmelse|Gäller inte|Azure SQL Database|

### <a name="integration-with-the-cloud-adoption-plan"></a>Integrering med moln implementerings planen

När identifieringen är klar kan planen ingå i [moln implementerings planen](../../plan/template.md). I moln implementerings planen lägger du till varje SQL Server instans som ska migreras som en [distinkt arbets belastning](../../plan/workloads.md). Inom varje arbets belastning kan databaserna och tjänsterna (SSIS, SSAS, SSRS) läggas till som [till gångar](../../plan/workloads.md). Information om hur du lägger till arbets belastningar och till gångar i bulk till implementerings planen finns i [lägga till och redigera arbets objekt med Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

När arbets belastningarna och till gångarna ingår i planen kan teamet fortsätta med en standard process för migrering med hjälp av implementerings planen för att vägleda insatser. När implementerings gruppen flyttas till utvärderings-, migrerings-och optimerings processer bör följande ändringar bedömas i ansträngningarna.

## <a name="assessment-process-changes"></a>Ändringar i utvärderings processen

Om en databas i planen kan migreras till en plattform som en tjänst (PaaS) data plattform använder du Data Migration Assistant för att utvärdera kompatibiliteten för den valda databasen. När databasen kräver schema konvertering rekommenderar vi att dessa konverteringar utförs som en del av utvärderings processen för att undvika avbrott i pipelinen för migrering.

### <a name="suggested-action-during-the-assessment-process"></a>Föreslagen åtgärd under utvärderings processen

För databaser som kan migreras till en PaaS-lösning slutförs följande åtgärder under utvärderings processen.

- **Utvärdera med Data Migration Assistant:** Använd Data Migration Assistant för att identifiera kompatibilitetsproblem som kan påverka databas funktioner i mål Azure SQL Database Hanterad instans, för att rekommendera förbättringar av prestanda och tillförlitlighet, samt för att flytta scheman, data och objekt som inte har inkluderats från käll servern till mål servern. Mer information finns i [Data Migration Assistant](/sql/dma/dma-overview).
- **Åtgärda och konvertera:** Konvertera dataschemat för data baserat på utdata från Data Migration Assistant för att åtgärda kompatibilitetsproblem. Testa det konverterade dataschemat med de beroende programmen.

## <a name="migrate-process-changes"></a>Ändringar i migreringsprocessen

Under migreringen finns det flera verktygs-och metod alternativ. Men varje metod följer en enkel process: Migrera schema, data och objekt. Synkronisera data med mål data källan.

Målet och källan för data strukturen och tjänsterna kan göra dessa två steg i stället komplicerade. Se vart och ett av följande avsnitt för att förstå det bästa verktygs valet utifrån dina beslut om migrering.

### <a name="suggested-action-during-the-migrate-process"></a>Föreslagna åtgärder under migreringsprocessen

Den föreslagna sökvägen för migrering och synkronisering använder en kombination av följande tre verktyg. I följande avsnitt beskrivs mer komplexa alternativ för migrering och synkronisering som möjliggör en bredare mängd olika mål-och käll lösningar.

|Migrations alternativ|Syfte|
|---------|---------|
|[Azure Database Migration Service](/sql/dma/dma-overview)|Azure DMS stöder online (minimal nedtid) och offline (en gång) migreringar i skala till en Azure SQL Database Hanterad instans från SQL Server 2005, SQL Server 2008 och SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 och SQL Server 2017.|
|[Transaktionsreplikering](/sql/relational-databases/replication/administration/enhance-transactional-replication-performance)|Transaktionsreplikering till en Azure SQL Database Hanterad instans stöds för migreringar från: SQL Server 2012 (SP2 CU8, SP3 eller senare), SQL Server 2014 (RTM CU10 eller senare eller SP1 CU3 eller senare), SQL Server 2016, SQL Server 2017|
|[Mass inläsning](/sql/t-sql/statements/bulk-insert-transact-sql)|Använd Mass inläsning till en Azure SQL Database Hanterad instans för data som lagras i SQL Server 2005, SQL Server 2008 och SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 och SQL Server 2017.|

### <a name="guidance-and-tutorials-for-suggested-migration-process"></a>Vägledning och självstudier för föreslagen migreringsprocessen

Att välja den bästa vägledningen för migrering med DMS är beroende av vilken källa och mål plattform du väljer. I följande tabell beskrivs självstudierna för var och en av standard metoderna för att migrera en SQL-databas med hjälp av DMS.

|Källa  |Målinrikta  |Verktyg  |Typ av migrering  |Vägledning  |
|---------|---------|---------|---------|---------|
|SQL Server|Azure SQL Database|DMS|Anslutningen|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|SQL Server|Azure SQL Database|DMS|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|SQL Server|Azure SQL Database Managed Instance|DMS|Anslutningen|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|SQL Server|Azure SQL Database Managed Instance|DMS|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|RDS-SQL Server|Azure SQL Database (eller hanterad instans)|DMS|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|

### <a name="guidance-and-tutorials-for-various-services-to-equivalent-paas-solutions"></a>Vägledning och självstudier för olika tjänster till motsvarande PaaS-lösningar

När du har flyttat databaser från en SQL Server till DMS kan schemat och data vara värd för i ett antal PaaS-lösningar. Andra nödvändiga tjänster kan dock fortfarande köras på den servern. Följande tre självstudier kommer att hjälpa till att flytta SSIS, SSAS och SSRS till motsvarande PaaS-tjänster på Azure.

|Källa  |Målinrikta  |Verktyg  |Typ av migrering  |Vägledning  |
|---------|---------|---------|---------|---------|
|SQL Server integrerings tjänst|Data Factory Integration Runtime|Azure Data Factory|Anslutningen|[Självstudie](https://docs.microsoft.com/azure/data-factory/create-azure-ssis-integration-runtime)|
|SQL Server Analysis Service-tabell modell|Azure Analysis Service|SSDT|Anslutningen|[Självstudie](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)|
|SQL Server repor ting service|Power BI rapport Server|Power BI|Anslutningen|[Självstudie](/power-bi/report-server/migrate-report-server)|

### <a name="guidance-and-tutorials-for-migration-from-sql-server-to-an-iaas-instance-of-sql-server"></a>Vägledning och självstudier för migrering från SQL Server till en IaaS-instans av SQL Server

När du har migrerat databaser och tjänster till PaaS-instanser kan det fortfarande finnas data strukturer och tjänster som inte är PaaS-kompatibla. När befintliga begränsningar förhindrar migrering av data strukturer eller tjänster, kan följande självstudie hjälpa till med migrering av olika till gångar i data portföljen till Azure IaaS-lösningar.

Den här metoden kan användas för att migrera databaser på SQL Server eller andra tjänster som körs på SQL Server-källan.

|Källa  |Målinrikta  |Verktyg  |Typ av migrering  |Vägledning  |
|---------|---------|---------|---------|---------|
|Enskild instans SQL Server|SQL Server på IaaS|Anpassa|Anslutningen|[Självstudie](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)|

## <a name="optimization-process-changes"></a>Ändringar i optimerings processen

Under optimeringen kan varje data struktur, tjänst eller SQL Server instans testas, optimeras och befordras till produktion. Detta är den största effekten av deviating från en per migrering av arbets belastning.

Vi rekommenderar att de beroende arbets belastningar, program och virtuella datorer kommer att migreras inom samma iteration som SQL Server-instansen. När det idealiska scenariot inträffar kan arbets belastningen testas tillsammans med data källan. När du har testat kan data strukturen befordras till produktion och synkroniseringen kan avslutas.

Den största förändringen i optimerings processen under en icke-arbetsstyrd migrering, kommer att ha en betydande tids lucka mellan migreringen av databasen och migrering av arbets belastning. När flera databaser migreras som en del av en SQL Server migrering, kan dessa databaser fungera både i molnet och lokalt för flera iterationer. Under denna tidsram måste du underhålla datasynkroniseringen tills dessa beroende till gångar migreras, testas och befordras.

Tills alla beroende arbets belastningar höjs ansvarar teamet för att stödja synkronisering av data från käll systemet till mål systemet. Den här synkroniseringen förbrukar nätverks bandbredd, moln kostnader och viktigast av folk tid. Lämplig justering av implementerings planen för SQL Server migreringen av arbets belastningen och alla beroende arbets belastningar/program minskar den dyra omkostnaderna.

### <a name="suggested-action-during-the-optimization-process"></a>Föreslagen åtgärd under optimerings processen

Under optimerings processerna bör följande uppgifter utföras varje iteration tills alla data strukturer och tjänster har befordrats till produktion.

1. Verifiera synkronisering av data.
2. Testa alla migrerade program.
3. Optimera program-och data strukturen för att justera kostnaderna.
4. Marknadsför programmen till produktion.
5. Testa för fortsatt lokal trafik mot den lokala databasen.
6. Avsluta synkroniseringen av data som befordras till produktion.
7. Avsluta den ursprungliga käll databasen.

Till steg 5 går det inte att avbryta databaser och synkronisering. Innan alla databaser på en SQL Server har genomgått steg 1-7, bör den lokala SQL Server behandlas som produktion och all synkronisering bör underhållas.

## <a name="next-steps"></a>Nästa steg

Gå tillbaka till [checklistan för utökat omfång](./index.md) och se till att din migreringsmetod är helt anpassad till kraven.

> [!div class="nextstepaction"]
> [Utökad checklista](./index.md)
