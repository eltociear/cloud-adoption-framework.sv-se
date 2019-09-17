---
title: Översikt med exempel på programmigrering för Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Innehåller en översikt med de exempel på programmigrering som ingår i migreringsavsnittet för ramverket för molnimplementering.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: cc6ce12f425354cbf907474431f2ec0f45735fea
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024954"
---
# <a name="application-migration-patterns-and-examples"></a>Programmigrering – mönster och exempel

Det här avsnittet av ramverket för molnimplementering innehåller exempel på flera vanliga migreringsscenarier som demonstrerar hur du kan migrera lokal infrastruktur till [Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure)-molnet.

## <a name="introduction"></a>Introduktion

Azure ger tillgång till en omfattande uppsättning molntjänster. Som utvecklare och IT-proffs kan du använda dessa tjänster för att skapa, distribuera och hantera appar med en mängd verktyg och ramverk, genom ett globalt datacenternätverk. När ditt företag möter utmaningarna med digitaliseringen hjälper Azure-molnet dig att optimera resurser och åtgärder, interagera med dina kunder och anställda och transformera dina produkter.

Men även om det finns stora fördelar med att migrera till Azure och molnet i form av hastighet och flexibilitet, minskade kostnader, prestanda och tillförlitlighet, kan det för många organisationer ibland vara nödvändigt att köra lokala datacenter ibland. För att lösa problem med barriärer vid molnimplementering tillhandahåller Azure en hybridmolnstrategi, som bygger broar mellan dina lokala datacenter och det offentliga Azure-molnet. Det går till exempel att använda Azure-molnresurser såsom Azure Backup för att skydda lokala resurser, eller använda Azure Analytics för att få insikter om lokala arbetsbelastningar.

Som en del av hybridmolnstrategin tillhandahåller Azure allt fler lösningar för att migrera lokala appar och arbetsbelastningar till molnet. Med de här enkla stegen kan du noggrant bedöma dina lokala resurser för att ta reda på hur de skulle fungera i Azure-molnet. Sedan kan du på ett säkert sätt migrera dina resurser till Azure. När resurserna är igång och körs i Azure, kan du optimera dem för att behålla och förbättra åtkomsten, flexibiliteten, säkerheten och tillförlitligheten.

## <a name="migration-patterns"></a>Migrationsmönster

Strategier för migrering till molnet kan delas in i fyra allmänna mönster: värdbyte, refaktorisering, arkitekturomarbetning och återskapande. Den strategi du väljer beror på dina affärsdrivande faktorer och mål med migrering. Du kan införa flera mönster. Du kan till exempel välja att byta värd för enkla appar eller appar som inte är kritiskt viktiga för verksamheten, men utföra arkitekturomarbetning för dem som är mer komplexa och affärskritiska. Nu ska vi titta på de här mönstren.

<!-- markdownlint-disable MD033 -->

**Mönster** | **Definition** | **När det bör användas**
--- | --- | ---
**Värdbyte** | Detta kallas ofta för lift-and-shift-migrering. Det här alternativet kräver inte kodändringar och gör att du snabbt kan migrera dina befintliga appar till Azure. Varje app migreras i befintligt skick för att dra nytta av molnets fördelar utan de risker och kostnader som är förknippade med kodändringar. | När du behöver flytta appar till molnet snabbt.<br/><br/> När du vill flytta en app utan att ändra den.<br/><br/> När dina appar konstrueras så att de kan dra nytta av [Azure IaaS](https://azure.microsoft.com/overview/what-is-iaas)-skalbarhet efter migreringen.<br/><br/> När appar är viktiga för verksamheten men du inte behöver omedelbara ändringar av appfunktioner.
**Refaktorisering** | Refaktorisering kallas ofta ”ompaketering” och kräver minimala ändringar i appar så att de kan ansluta till [Azure-PaaS](https://azure.microsoft.com/overview/what-is-paas) och använda molnerbjudanden.<br/><br/> Du skulle till exempel kunna migrera befintliga appar till Azure App Service eller Azure Kubernetes Service (AKS).<br/><br/> Du skull även kunna refaktorisera relationsdatabaser och icke-relationella databaser till alternativ såsom Azure SQL Database Managed Instance, Azure Database for MySQL, Azure Database for PostgreSQL samt Azure Cosmos DB. | Om din app enkelt kan paketeras om till att fungera i Azure.<br/><br/> Om du vill använda innovativa DevOps-metoder som tillhandahålls av Azure, eller om du överväger DevOps med en containerstrategi för arbetsbelastningar.<br/><br/> För refaktorisering behöver du tänka på portabiliteten i din befintliga kodbas samt tillgängliga utvecklingskunskaper.
**Arkitekturomarbetning** | Arkitekturomarbetning för migrering fokuserar på att ändra och utöka appfunktionaliteten och kodbasen för att optimera apparkitekturen för molnskalbarhet.<br/><br/> Du kan till exempel dela upp ett monolitiskt program i en grupp med mikrotjänster som fungerar tillsammans och skalas enkelt.<br/><br/> Eller så kan du utföra arkitekturomarbetning för relationsdatabaser och icke-relationella databaser till fullständigt hanterade hanterad Azure SQL Database-instans, Azure Database for MySQL, Azure Database for PostgreSQL samt Azure Cosmos DB. | När dina appar kräver större revideringar för att införliva nya funktioner eller för att fungera effektivt på en molnplattform.<br/><br/> När du vill använda befintliga programinvesteringar, uppfylla skalbarhetskrav, använda innovativa Azure DevOps-metoder och minimera användningen av virtuella datorer.
**Återskapande** | Återskapande går ett steg längre genom att återskapa en app från grunden med hjälp av Azure-molntekniker.<br/><br/> Till exempel kan du skapa helt nya appar med [molnbaserade](https://azure.com/cloudnative) tekniker såsom Azure Functions, Azure AI, hanterad Azure SQL Database-instans samt Azure Cosmos DB. | När du vill utveckla snabbt, och befintliga appar har begränsad funktionalitet och livslängd.<br/><br/> När du är redo att påskynda företagsinnovationen (däribland DevOps-metoder som tillhandahålls av Azure) kan du skapa nya program med hjälp av molnbaserade tekniker och dra nytta av framsteg inom AI, blockkedjan och IoT.

<!-- markdownlint-enable MD033 -->

## <a name="migration-example-articles"></a>Artiklar med migreringsexempel

Artiklarna i det här avsnittet innehåller exempel på flera vanliga migreringsscenarier. Vart och ett av dessa exempel innehåller bakgrundsinformation och detaljerade distributionsscenarier som illustrerar hur du konfigurerar en infrastruktur för migrering och utvärderar lokala resursers lämplighet med avseende på migrering. Fler artiklar kommer att läggas till i det här avsnittet med tiden.

![Vanliga projekt för migrering/modernisering](./media/migration-patterns.png)

*Kategorier för vanliga projekt för migrering/modernisering.*

Artiklarna i serien sammanfattas nedan.

- Varje migreringsscenario styrs av något olika affärsmål som avgör migreringsstrategin.
- För varje distributionsscenario tillhandahåller vi information om affärsdrivande faktorer och mål, en föreslagen arkitektur, steg för att utföra migreringen, rekommendationer för rensning samt nästa steg efter att migreringen är klar.

### <a name="assessment"></a>Utvärdering

**Artikel** | **Detaljer**
--- | ---
[Utvärdera lokala resurser för migrering till Azure](./contoso-migration-assessment.md) | Den här artikeln visar hur du kör en utvärdering av en lokal app som körs på VMware. I exemplet utvärderar en exempelorganisation virtuella appdatorer med hjälp av Azure Migrate-tjänsten och SQL Server-appdatabasen med hjälp av Data Migration Assistant.

### <a name="infrastructure"></a>Infrastruktur

**Artikel** | **Detaljer**
--- | ---
[Distribuera Azure-infrastruktur](./contoso-migration-infrastructure.md) | Den här artikeln visar hur en organisation kan förbereda sin lokala infrastruktur och Azure-infrastruktur för migrering. Det infrastrukturexempel som upprättats i den här artikeln hänvisas till i de andra exempel som ges i det här avsnittet.

### <a name="windows-server-workloads"></a>Windows Server-arbetsbelastningar

**Artikel** | **Detaljer**
--- | ---
[Byta värd för en app på virtuella Azure-datorer](./contoso-migration-rehost-vm.md) | Den här artikeln innehåller ett exempel på migrering av lokala virtuella appdatorer till virtuella Azure-datorer med hjälp av Site Recovery-tjänsten.
[Utföra arkitekturomarbetning för en app i Azure-containrar och Azure SQL Database](./contoso-migration-rearchitect-container-sql.md) | Den här artikeln innehåller ett exempel på migrering av en app samtidigt som arkitekturomarbetning utförs för appwebblagret som en Windows-container som körs i Azure Service Fabric samt databasen med Azure SQL Database.

### <a name="linux-workloads"></a>Linux-arbetsbelastningar

**Artikel** | **Detaljer**
--- | ---
[Byta värd för en Linux-app på virtuella Azure-datorer och Azure Database for MySQL](./contoso-migration-rehost-linux-vm-mysql.md) | Den här artikeln innehåller ett exempel på migrering av en Linux-värdbaserad app till virtuella Azure-datorer med hjälp av Site Recovery. Den migrerar appdatabasen till Azure Database for MySQL med hjälp av MySQL Workbench.
[Byta värd för en Linux-app på virtuella Azure-datorer](./contoso-migration-rehost-linux-vm.md) | Det här exemplet visar hur du utför en lift-and-shift-migrering av en Linux-baserad app till virtuella Azure-datorer med hjälp av Site Recovery-tjänsten.

### <a name="sql-server-workloads"></a>SQL Server-arbetsbelastningar

**Artikel** | **Detaljer**
--- | ---
[Byta värd för en app på en virtuell Azure-dator och hanterad SQL Database-instans](./contoso-migration-rehost-vm-sql-managed-instance.md) | Den här artikeln innehåller ett exempel på en lift-and-shift-migrering till Azure för en lokal app. Detta inbegriper migrering av appens virtuella klientdatorn med hjälp av [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) och appdatabasen till en hanterad Azure SQL Database-instans med hjälp av [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview).
[Byta värd för en app på virtuella Azure-datorer och i en SQL Server AlwaysOn-tillgänglighetsgrupp](./contoso-migration-rehost-vm-sql-ag.md) | Det här exemplet visar hur du migrerar en app och data med hjälp av Azure-värdhanterade virtuella SQL Server-datorer. Det använder Site Recovery för att migrera de virtuella appdatorerna och Azure Database Migration Service för att migrera appdatabasen till ett SQL Server-kluster som skyddas av en AlwaysOn-tillgänglighetsgrupp.

### <a name="aspnet--php--java-apps"></a>ASP.NET-/PHP-/Java-appar

**Artikel** | **Detaljer**
--- | ---
[Refaktorisera en app i en Azure-webapp och Azure SQL Database](./contoso-migration-refactor-web-app-sql.md) | Det här exemplet visar hur du migrerar en lokal Windows-baserad app till en Azure-webbapp och migrerar appdatabasen till en Azure SQL Server-instans med Data Migration Assistant.
[Refaktorisera en Linux-app till flera regioner med hjälp av Azure App Service, Azure Traffic Manager och Azure Database for MySQL](./contoso-migration-refactor-linux-app-service-mysql.md) | Det här exemplet visar hur du migrerar en lokal Linux-baserad app till en Azure-webbapp i flera Azure-regioner med hjälp av Azure Traffic Manager, integrerat med GitHub för kontinuerlig leverans. Appdatabasen migreras till en Azure Database for MySQL-instans.
[Återskapa en app i Azure](./contoso-migration-rebuild.md) | Den här artikeln innehåller ett exempel på återskapande av en lokal app med hjälp av en rad Azure-funktioner och hanterade tjänster, däribland Azure App Service, Azure Kubernetes Service (AKS), Azure Functions, Azure Cognitive Services och Azure Cosmos DB.
[Refaktorisera Team Foundation Server på Azure DevOps Services](./contoso-migration-tfs-vsts.md) | Den här artikeln visar ett exempel på migrering av en lokal Team Foundation Server-distribution till Azure DevOps Services i Azure.

### <a name="migration-scaling"></a>Skalning av migrering

**Artikel** | **Detaljer**
--- | ---
[Skala en migrering till Azure](./contoso-migration-scale.md) | Den här artikeln visar hur en exempelorganisation förbereder att skala till en fullständig migrering till Azure.

### <a name="demo-apps"></a>Demoappar

I de exempelartiklar som anges i det här avsnittet används två demoappar: SmartHotel360 och osTicket.

- **SmartHotel360:** Den här appen utvecklades av Microsoft som en testapp som du kan använda när du arbetar med Azure. Den tillhandahålls med öppen källkod, och du kan ladda ned den från [GitHub](https://github.com/Microsoft/SmartHotel360). Det är en ASP.NET-app som är ansluten till en SQL Server-databas. I de scenarier som beskrivs i dessa artiklar distribueras den aktuella versionen av den här appen till två virtuella VMware-datorer som kör Windows Server 2008 R2 och SQL Server 2008 R2. Dessa virtuella appdatorer värdhanteras lokalt och hanteras av vCenter Server.
- **osTicket:** En supportapp för biljetter med öppen källkod som körs i Linux. Du kan ladda ned den från [GitHub](https://github.com/osTicket/osTicket). I de scenarier som beskrivs i dessa artiklar distribueras den aktuella versionen av den här appen lokalt till två virtuella VMware-datorer som kör Ubuntu 16.04 LTS med hjälp av Apache 2, PHP 7.0 och MySQL 5.7