---
title: Migrera tillgångar
description: Den här guiden hjälper dig att initiera din miljömigrering genom att identifiera lämpliga verktyg för att nå ”färdigt tillstånd”, däribland inbyggda verktyg, verktyg från tredje part samt verktyg för projekthantering.
author: matticusau
ms.author: mlavery
ms.date: 08/08/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 9da81d0f9c51343b7d31fbc5591607fdfd36a1aa
ms.sourcegitcommit: 58ea417a7df3318e3d1a76d3807cc4e7e3976f52
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/07/2020
ms.locfileid: "78892865"
---
<!-- cSpell:ignore Cloudamize agentless uncontained SSMA Carbonite Movere -->

# <a name="migrate-assets-infrastructure-apps-and-data"></a>Migrera tillgångar (infrastruktur, appar och data)

I den här fasen av resan använder du resultatet av utvärderingsfasen för att inleda migreringen av miljön. Den här guiden hjälper dig att identifiera lämpliga verktyg för att nå ”färdigt tillstånd”, däribland inbyggda verktyg, verktyg från tredje part samt verktyg för projekthantering.

<!-- markdownlint-disable MD025 -->

# <a name="native-migration-tools"></a>[Inbyggda migreringsverktyg](#tab/Tools)

I följande avsnitt beskrivs de inbyggda Azure-verktyg som är tillgängliga för att utföra eller underlätta migreringen. Information om hur du väljer rätt verktyg för migreringen finns i [guiden för beslut om migreringsverktyg för Cloud Adoption Framework](../../decision-guides/migrate-decision-guide/index.md).

## <a name="azure-migrate"></a>Azure Migrate

Azure Migrate levererar en enhetlig och utökningsbar migreringsupplevelse. Azure Migrate ger en samlad, dedikerad upplevelse där du kan spåra migreringsresan genom faserna för utvärdering och migrering till Azure. Du kan använda valfria verktyg för att spåra migreringsförloppet.

Azure Migrate innehåller följande funktioner:

1. Förbättrade funktioner för utvärdering och migrering:
    - Utvärderingar av Hyper-V.
    - Förbättrad utvärdering av VMware.
    - Agentlös migrering av virtuella VMware-datorer till Azure.
1. Enhetlig utvärdering, migrering och förloppsspårning.
1. Utökningsbar metod med ISV-integrering (till exempel Cloudamize).

Följ dessa steg om du vill utföra en migrering med Azure Migrate:

1. Sök efter Azure Migrate under **Alla tjänster**. Välj **Azure Migrate** för att fortsätta.
1. Välj **Lägg till ett verktyg** för att starta migreringsprojektet.
1. Välj den prenumeration, resursgrupp och geografi som ska vara värd för migreringen.
1. Välj **Välj utvärderings verktyg** > **Azure Migrate: Server utvärdering** >  **Nästa**.
1. Välj **Granska + lägg till verktyg** och verifiera konfigurationen. Välj **Lägg till verktyg** för att starta jobbet för att skapa migreringsjobbet och registrera de valda lösningarna.

### <a name="learn-more"></a>Läs mer

- [Azure Migrate-självstudier – Migrera fysiska eller virtualiserade servrar till Azure](https://docs.microsoft.com/azure/migrate/tutorial-migrate-physical-virtual-machines)

## <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery-tjänsten kan hantera migreringen av lokala resurser till Azure. Den kan även hantera och samordna haveriberedskap för lokala datorer och virtuella Azure-datorer i BCDR-syfte (affärskontinuitet och haveriberedskap).

Följande steg beskriver processen med att använda Site Recovery för att migrera:

> [!TIP]
> Beroende på ditt scenario kan de här stegen skilja sig något. Mer information finns i artikeln [Migrera lokala datorer till Azure](https://docs.microsoft.com/azure/site-recovery/migrate-tutorial-on-premises-azure).

### <a name="prepare-azure-site-recovery-service"></a>Förbereda Azure Site Recovery-tjänsten

1. I Azure-portalen väljer du **+Skapa en resurs > Hanteringsverktyg > Säkerhetskopiering och webbplatsåterställning**.
1. Om du ännu inte har skapat ett återställningsvalv slutför du guiden för att skapa en resurs för **Recovery Services-valv**.
1. I menyn **Resurs** väljer du **Site Recovery > Förbered infrastruktur > Skyddsmål**.
1. I **Skyddsmål** väljer du vad du vill migrera.
    1. **VMware:** Välj **Azure > Ja, med VMware vSphere hypervisor**.
    1. **Fysisk dator:** Välj **till Azure > inte virtualiserad/övrigt**.
    1. **Hyper-V:** Välj **Azure > Ja, med Hyper-V**. Om de virtuella Hyper-V-datorerna hanteras av VMM väljer du **Ja**.

### <a name="configure-migration-settings"></a>Konfigurera migreringsinställningar

1. Konfigurera källmiljön enligt vad som är lämpligt.
1. Konfigurera målmiljön.
    1. Välj **Förbered infrastruktur > mål**och välj sedan den Azure-prenumeration som du vill använda.
    1. Ange Resource Manager-distributionsmodellen.
    1. Site Recovery kontrollerar att du har ett eller flera kompatibla Azure-lagringskonton och Azure-nätverk.
1. Konfigurera en replikeringsprincip.
1. Aktivera replikering.
1. Kör en testmigrering (testa redundansväxling).

### <a name="migrate-to-azure-using-failover"></a>Migrera till Azure med hjälp av redundansväxling

1. I **Inställningar > Replikerade objekt** väljer du datorn > **Redundans**.
1. I **Redundans** väljer du en **återställningspunkt** att redundansväxla till. Välj den senaste återställningspunkten.
1. Konfigurera eventuella inställningar för krypteringsnycklar efter behov.
1. Välj **Stäng datorn innan du påbörjar redundans**. Site Recovery försöker att stänga av virtuella datorer innan redundansen utlöses. Redundansväxlingen fortsätter även om avstängningen misslyckas. Du kan följa redundansförloppet på sidan Jobb.
1. Kontrollera att den virtuella Azure-datorn visas i Azure som förväntat.
1. I **Replikerade objekt** högerklickar du på den virtuella datorn och väljer **Slutför migrering**.
1. Utför eventuella steg efter migreringen efter behov (se relevant information i den här guiden).

::: zone target="chromeless"

::: form action="Create[#create/Microsoft.RecoveryServices]" submitText="Create a Recovery Services vault" :::

::: zone-end

::: zone target="docs"

Mer information finns i:

- [Migrera lokala datorer till Azure](https://docs.microsoft.com/azure/site-recovery/migrate-tutorial-on-premises-azure)

::: zone-end

## <a name="azure-database-migration-service"></a>Azure Database Migration Service

Azure Database Migration Service är en fullständigt hanterad tjänst som möjliggör sömlösa migreringar från flera databaskällor till Azure-dataplattformar med minimal avbrottstid (onlinemigreringar). Azure Database Migration Service utför alla nödvändiga steg. Du kan inleda migreringsjobb med tryggheten att processen utförs med den bästa praxis som rekommenderas av Microsoft.

### <a name="create-an-azure-database-migration-service-instance"></a>Skapa en Azure Database Migration Service-instans

Om det här är första gången du använder Azure Database Migration Service behöver du registrera resursprovidern för din Azure-prenumeration:

1. Välj **Alla tjänster** följt av **Prenumerationer** och välj sedan målprenumerationen.
1. Välj **Resursprovidrar**.
1. Sök efter `migration`. Till höger om **Microsoft.DataMigration** väljer du sedan **Registrera**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to Subscriptions" :::

::: zone-end

När du har registrerat resursprovidern kan du skapa en instans av Azure Database Migration Service.

1. Välj **+Skapa en resurs** och sök på marknadsplatsen efter **Azure Database Migration Service**.
1. Slutför guiden **skapa migrations tjänst** och välj sedan **skapa**.

Tjänsten är nu redo att migrera de källdatabaser som stöds (till exempel SQL Server, MySQL, PostgreSQL eller MongoDB).

::: zone target="chromeless"

::: form action="Create[#create/Microsoft.AzureDMS]" submitText="Create an Azure Database Migration Service instance" :::

::: zone-end

::: zone target="docs"

Mer information finns i:

- [Översikt över Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview)
- [Skapa en instans av Azure Database Migration Service](https://docs.microsoft.com/azure/dms/quickstart-create-data-migration-service-portal)
- [Azure Migrate i Azure-portalen](https://portal.azure.com/#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade)
- [Azure Portal: skapa ett migreringsjobb](https://portal.azure.com/#create/Microsoft.AzureMigrate)

::: zone-end

## <a name="data-migration-assistant"></a>Data Migration Assistant

Med Data Migration Assistant (DMA) kan du uppgradera till en modern dataplattform genom att identifiera kompatibilitetsproblem som kan påverka databasfunktionalitet i din nya version av SQL Server eller Azure SQL Database. DMA rekommenderar prestanda- och tillförlitlighetsförbättringar för din målmiljö och gör att du kan flytta schema, data och beroende objekt från källservern till målservern.

> [!NOTE]
> För stora migreringar (vad gäller antal och storlek på databaser) rekommenderar vi att du använder Azure Database Migration Service, som kan migrera databaser i stor skala.
>

Börja använda Data Migration Assistant med följande steg:

1. Hämta och installera Data Migration Assistant från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595).
1. Skapa en utvärdering genom att välja ikonen **ny (+)** och välj sedan **bedömnings** projekt typ.
1. Ange käll-och mål server typ och välj sedan **skapa**.
1. Konfigurera utvärderingsalternativen efter behov (standardvärden för alla rekommenderas).
1. Lägg till de databaser som ska utvärderas.
1. Välj **Nästa** för att starta utvärderingen.
1. Visa resultat i Data Migration Assistant-verktygsuppsättningen.

För företag rekommenderar vi att du följer den metod som beskrivs i [Utvärdera ett företag och konsolidera utvärderingsrapporter med DMA](https://docs.microsoft.com/sql/dma/dma-consolidatereports) för att utvärdera flera servrar, kombinerar rapporterna och sedan använder de tillhandahållna Power BI-rapporterna för att analysera resultatet.

Mer information, däribland detaljerade användningssteg, finns i följande avsnitt:

- [Översikt av Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview)
- [Utvärdera ett företag och konsolidera utvärderingsrapporter med DMA](https://docs.microsoft.com/sql/dma/dma-consolidatereports)
- [Analysera konsoliderade utvärderingsrapporter som skapats av Data Migration Assistant med Power BI](https://docs.microsoft.com/sql/dma/dma-powerbiassesreport)

## <a name="sql-server-migration-assistant"></a>SQL Server Migration Assistant

Microsoft SQL Server Migration Assistant (SSMA) är ett verktyg som utformats för att automatisera databasmigrering till SQL Server från Microsoft Access, DB2, MySQL, Oracle och SAP ASE. Det allmänna konceptet är att samla in, utvärdera och granska med dessa verktyg, men på grund av varianser i processen för varje källsystem rekommenderar vi att du läser den detaljerade [dokumentationen för SQL Server Migration Assistant](https://docs.microsoft.com/sql/ssma/sql-server-migration-assistant).

Mer information finns i:

- [Översikt av SQL Server Migration Assistant](https://docs.microsoft.com/sql/ssma/sql-server-migration-assistant)

## <a name="database-experimentation-assistant"></a>Database Experimentation Assistant

Database Experimentation Assistant (DEA) är en ny A/B-testlösning för SQL Server-uppgraderingar. Den hjälper till att utvärdera en målversion av SQL för en viss arbetsbelastning. Kunder som uppgraderar från tidigare SQL Server-versioner (SQL Server 2005 och senare) till en ny version av SQL Server kan använda dessa analysmått.

Database Experimentation Assistant innehåller följande arbetsflödesaktiviteter:

- **Avbildning:** Det första steget i SQL Server A/B-testning är att avbilda en spårning på käll servern. Källservern är vanligtvis produktionsservern.
- **Spela upp igen:** Det andra steget i SQL Server A/B-test är att spela upp spårnings filen som har registrerats på mål servrarna. Samla sedan in omfattande spårningar från återuppspelningarna för analys.
- **Analys:** Det sista steget är att generera en analys rapport med hjälp av uppspelnings spåren. Analysrapporten kan hjälpa dig att få insikt om prestandakonsekvenserna för den föreslagna ändringen.

Mer information finns i:

- [Översikt av Database Experimentation Assistant](https://docs.microsoft.com/sql/dea/database-experimentation-assistant-overview)

## <a name="cosmos-db-data-migration-tool"></a>Azure Cosmos DB-datamigreringsverktyget

Med datamigreringsverktyget i Azure Cosmos DB kan du importera data från olika källor till samlingar och tabeller i Azure Cosmos DB. Du kan importera från JSON-filer, CSV-filer, SQL, MongoDB, Azure Table Storage, Amazon DynamoDB och till och med Azure Cosmos DB SQL API-samlingar. Datamigreringsverktyget kan också användas när du migrerar från en enda partitionssamling till en samling med flera partitioner för SQL API.

Mer information finns i:

- [Azure Cosmos DB-datamigreringsverktyget](https://docs.microsoft.com/azure/cosmos-db/import-data)

<!-- markdownlint-disable MD025 -->

# <a name="third-party-migration-tools"></a>[Migreringsverktyg från tredje part](#tab/third-party-tools)

Det finns flera migreringsverktyg från tredje part och ISV-tjänster som kan hjälpa till med migreringsprocessen. De har alla olika fördelar och styrkor. Dessa verktyg innefattar:

## <a name="unifycloud"></a>UnifyCloud

UnifyCloud är en ISV-tjänst som tillhandahåller verktyg för bedömning, migrering och modernisering Automation.

[Läs mer](https://www.unifycloud.com/)

## <a name="cloudamize"></a>Cloudamize

Cloudamize är en ISV-tjänst som omfattar alla faser av migrationsstrategin.

[Läs mer](https://www.cloudamize.com)

## <a name="zerto"></a>Zerto

Zerto tillhandahåller virtuell replikering som hanterar miljöer för både Microsoft Hyper-V-och VMware vSphere.

[Läs mer](https://www.zerto.com/modernize)

## <a name="carbonite"></a>Carbonite

Carbonite tillhandahåller lösningar för server- och datamigrering för att migrera arbetsbelastningar till, från eller mellan fysiska, virtuella eller molnbaserade miljöer.

[Läs mer](https://www.carbonite.com/data-protection/data-migration-software)

## <a name="movere"></a>Movere

Movere är en identifieringslösning som tillhandahåller de data och insikter som krävs för att planera migrering av molnet och kontinuerligt optimera, övervaka och analysera IT-miljöer med förtroende.

[Läs mer](https://www.movere.io)

## <a name="cosmos-db-partners"></a>Cosmos DB-partner

Du kan välja mellan olika erfarna systemintegreringspartner och verktyg som underlättar Azure Cosmos DB-migreringen baserat på dina NoSQL-databaskrav.

[Läs mer](https://docs.microsoft.com/azure/cosmos-db/partners-migration-cosmosdb#migration-tools)

Besök [Azure Migration Center](https://azure.microsoft.com/migration/support) för att identifiera organisationer som erbjuder färdiga partnertekniklösningar som passar dina migreringsscenarier och få mer information om ytterligare migreringsverktyg från tredje part samt supporttjänster.

I [Azure Database-migreringsguiden](https://datamigration.microsoft.com) hittar du en rad olika alternativ för databasmigrering och inbyggd stegvis vägledning och hjälp från partner.

# <a name="project-management-tools"></a>[Verktyg för projekthantering](#tab/project-management-tools)

Projekt som inte spåras och hanteras löper större risk att stöta på problem. För att säkerställa ett lyckat resultat anser vi att du bör använda ett verktyg för projekthantering. Det finns många olika tillgängliga verktyg, och kanske har projektledarna i din organisation redan en favorit.

Azure DevOps är det rekommenderade verktyget för projekthantering vid en molnbaserad migrering. För att påskynda användningen av Azure DevOps innehåller Cloud Adoption Framework ett verktyg för automatisk distribution av en projektmall. Mallen innehåller de uppgifter som vanligtvis utförs under en migrering. Distribuera mallen genom att följa [dessa anvisningar](https://docs.microsoft.com/azure/architecture/cloud-adoption/plan/template). Sedan kan du ändra mallen så att den överensstämmer med de [arbetsbelastningar](https://docs.microsoft.com/azure/architecture/cloud-adoption/plan/workloads) och [tillgångar](https://docs.microsoft.com/azure/architecture/cloud-adoption/plan/assets) som ska migreras.

Microsoft erbjuder även följande verktyg för projekthantering, som kan fungera tillsammans för att tillhandahålla bredare funktioner:

- [Microsoft Planner](https://tasks.office.com): ett enkelt, visuellt sätt att organisera lag arbete.
- [Microsoft Project](https://products.office.com/project/project-and-portfolio-management-software): projekt-och portfölj hantering, hantering av resurs kapacitet, ekonomisk hantering, tid rapport och schema hantering.
- [Microsoft Teams](https://products.office.com/microsoft-teams): Team samarbete och kommunikations verktyg. Teams integrerar även Planner och andra verktyg för att förbättra samarbetet.
- [Azure-DevOps](https://dev.azure.com): planerings mal len för moln införande ramverk krävs inte för att använda Azure DevOps. Du kan använda tjänsten utan mallen för att hantera din infrastruktur som kod eller använda arbetsobjekt och paneler för att hantera projekt. När dina kunskaper växer kan din organisation dra nytta av CI/CD-funktionerna.

Det finns även fler verktyg utöver dessa. Många andra verktyg från tredje part används ofta inom projekthantering.

## <a name="set-up-for-devops"></a>Förbereda inför DevOps

När du migrerar till molntekniker ger detta en bra möjlighet att förbereda organisationen för DevOps och CI/CD. Även om din organisation endast hanterar infrastrukturen kan du, när du börjar hantera infrastrukturen som kod samt använder branschmönstren och -metoderna för DevOps, börja öka agiliteten med hjälp av CI/CD-pipelines. Därmed kan du snabbare anpassa dig till scenarier för ändring, tillväxt, lanseringar och även återställning.

Azure DevOps tillhandahåller alla nödvändiga funktioner och integrering med Azure, lokala miljöer eller till och med andra moln. Mer information finns i [Azure DevOps](https://azure.microsoft.com/services/devops). Vägledd utbildning finns i [CI och CD med Azure DevOps – snabbstart](https://microsoft.github.io/PartsUnlimited/pandp/200.1x-PandP-CICDQuickstartwithVSTS.html).

## <a name="suggested-skills"></a>Föreslagna färdigheter

Microsoft Learn är en ny metod för inlärning. Det är inte helt enkelt att förbereda sig för de nya ansvarsområdena som medföljer vid en övergång till molnet. Microsoft Learn erbjuder en mer givande metod för konkret inlärning som hjälper er att uppnå era mål snabbare. Tjäna poäng och nivåer och uträtta mer!

Här är ett exempel på en skräddarsydd utbildningsväg på Microsoft Learn som kompletterar DevOps-vägledningen i Cloud Adoption Framework.

[Bygg program med Azure DevOps](https://docs.microsoft.com/learn/paths/build-applications-with-azure-devops/): samar beta med andra för att bygga dina program med hjälp av Azure-pipeliner och GitHub. Kör automatiserade tester i din pipeline för att verifiera kodkvalitet. Sök igenom källkoden och komponenter från tredje part efter potentiella sårbarheter. Skapa ditt program genom att definiera flera pipelines som fungerar tillsammans. Skapa program med hjälp av både Microsoft-baserade agenter och dina egna skapandeagenter.

# <a name="cost-management"></a>[Kostnadshantering](#tab/ManageCost)

När du migrerar resurser till din molnmiljö är det viktigt att utföra regelbunden kostnadsanalys. Detta hjälper dig att undvika oväntade användningsavgifter eftersom migreringsprocessen kan ålägga dina tjänster ytterligare användningskrav. Du kan också ändra storlek på resurser efter behov för att balansera kostnader och arbets belastningar (beskrivs mer detaljerat i avsnittet **[optimera och transformera](./optimize-and-transform.md)** ).
