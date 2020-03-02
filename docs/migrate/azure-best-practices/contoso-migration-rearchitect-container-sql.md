---
title: Ändra utformningen av en app i en Azure-container och Azure SQL Database
description: Se hur Contoso ändrar utformningen av en app i Azure Windows-containrar och Azure SQL Database.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: d41c63d9876a5ead14acee9b39542ab256144920
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78223106"
---
<!-- cSpell:ignore reqs contosohost contosodc contosoacreus contososmarthotel smarthotel vcenter WEBVM SQLVM -->

# <a name="rearchitect-an-on-premises-app-to-an-azure-container-and-azure-sql-database"></a>Ändra utformningen av en lokal app i en Azure-container och Azure SQL Database

Den här artikeln visar hur det fiktiva företaget Contoso bygger om en Windows .NET-app med två nivåer som körs på virtuella VMware-datorer som en del av en migrering till Azure. Contoso migrerar appens klientdelsdator till en Azure Windows-container och appdatabasen till en Azure SQL-databas.

SmartHotel360-appen som används i det här exemplet tillhandahålls som öppen källkod. Om du vill använda den i ett eget test kan du ladda ned den från [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Affärsdrivande faktorer

Contosos IT-ledningsgrupp har arbetat tillsammans med affärspartner för att förstå vad man vill uppnå med migreringen:

- **Hantera företagets tillväxt.** Contoso växer, vilket leder till tryck på lokala system och infrastruktur.
- **Öka effektiviteten.** Contoso måste ta bort onödiga procedurer och effektivisera processer för utvecklare och användare. En snabb IT-lösning som inte slösar tid eller pengar är viktigt för företaget, så att man kan leverera snabbare enligt kundkraven.
- **Öka flexibiliteten.** Contosos IT-avdelning måste reagera snabbare på företagets behov. Den måste kunna reagera snabbare än förändringarna på marknaden för att företaget ska lyckas i en global ekonomi. Den får inte vara i vägen eller bromsa verksamheten.
- **Skala.** När verksamheten växer måste företaget tillhandahålla system som kan växa i samma takt.
- **Minska kostnaderna.** Contoso vill minimera licenskostnaderna.

## <a name="migration-goals"></a>Migreringsmål

Contosos molnteam har fastställt mål för migreringen. Målen användes för att fastställa den bästa migreringsmetoden.

<!-- markdownlint-disable MD033 -->

**Mål** | **Detaljer**
--- | ---
**Appkrav** | Appen i Azure kommer att vara lika kritisk som den är i dag.<br/><br/> Den bör ha samma prestandafunktioner som den för närvarande har i VMware.<br/><br/> Contoso vill sluta stödja Windows Server 2008 R2, som för närvarande är värd för appen och contoso är villig att investera i appen.<br/><br/> Contoso vill flytta bort från SQL Server 2008 R2 till en modern, hanterad databas plattform som minimerar behovet av hantering.<br/><br/> Contoso vill dra nytta av sina investeringar i SQL Server-licensiering och Software Assurance där det är möjligt.<br/><br/> Contoso vill skala webb nivån för appen efter behov.
**Begränsningar** | Appen består av en ASP.NET-app och en WCF-tjänst som körs på samma virtuella dator. Contoso vill dela upp detta i två webbappar med hjälp av Azure App Service.
**Azure-krav** | Contoso vill flytta appen till Azure och köra den i en container för att förlänga appens livslängd. Den vill inte börja helt från grunden med att implementera appen i Azure.
**DevOps** | Contoso vill flytta till en DevOps-modell med Azure DevOps för sina tjänst-som-kodversioner and lanseringspipelines.

<!-- markdownlint-enable MD033 -->

## <a name="solution-design"></a>Lösningsdesign

När de har fastställt målen och kraven utformar och utvärderar Contoso en distributionslösning och identifierar migreringsprocessen, inklusive de Azure-tjänster som Contoso använder för migreringen.

### <a name="current-app"></a>Aktuell app

- Den lokala appen SmartHotel360 delas in i nivåer på två virtuella datorer (WEBVM och SQLVM).
- De virtuella datorerna finns på VMware ESXi-värden **contosohost1.contoso.com** (version 6.5)
- VMware-miljön hanteras av vCenter Server 6.5 (**vcenter.contoso.com**), som körs på en virtuell dator.
- Contoso har ett lokalt datacenter (contoso-datacenter) med en lokal domänkontrollant (**contosodc1**).
- De lokala, virtuella datorerna i Contosos datacenter inaktiveras när migreringen är färdig.

### <a name="proposed-architecture"></a>Föreslagen arkitektur

- Contoso jämförde Azure SQL Database med SQL Server med hjälp av [den här artikeln](https://docs.microsoft.com/azure/sql-database/sql-database-features) för appens databasnivå. De beslutade att satsa på Azure SQL Database av flera skäl:
  - Azure SQL Database är en hanterad relationsdatabastjänst. Den ger förutsägbar prestanda på flera servicenivåer med nästan obefintlig administration. Fördelarna är dynamisk skalbarhet utan driftavbrott, inbyggd, intelligent optimering och global skalbarhet och tillgänglighet.
  - Contoso använder förenklad Data Migration Assistant (DMA) för att utvärdera och migrera den lokala databasen till Azure SQL.
  - Med Software Assurance kan Contoso byta ut befintliga licenser till rabatterade priser på en SQL-databas med hjälp av Azure Hybrid Benefit för SQL Server. Det kan ge besparingar på upp till 30 %.
  - SQL Database innehåller flera säkerhetsfunktioner som alltid krypterad, dynamisk datamaskning och säkerhets-/hotidentifiering på radnivå.
- För appens webbnivå har Contoso valt att konvertera det till Windows-containern med Azure DevOps Services.
  - Contoso distribuerar appen med Azure Service Fabric och hämtar Windows-behållaravbildningen från Azure Container Registry (ACR).
  - En prototyp för att utöka appen till att inkludera känsloanalys implementeras som en annan tjänst i Service Fabric, som är ansluten till Cosmos DB. Detta läser information från Twitter och visar den i appen.
- För att implementera en DevOps-pipeline använder Contoso Azure DevOps för källkodshantering med Git-databaser. Automatiserade versioner och versioner kommer att användas för att utveckla kod och distribuera den till Azure Container Registry och Azure Service Fabric.

    ![Scenariots arkitektur](./media/contoso-migration-rearchitect-container-sql/architecture.png)

### <a name="solution-review"></a>Lösningsgranskning

Contoso utvärderar den föreslagna designen genom att skapa en lista med för- och nackdelar.

<!-- markdownlint-disable MD033 -->

**Övervägande** | **Detaljer**
--- | ---
**Fördelar** | Koden för SmartHotel360-appen behöver inte ändras för migrering till Azure Service Fabric. Arbetsinsatsen är dock minimal tack vare verktygen i Service Fabric SDK.<br/><br/> Med flytten till Service Fabric kan Contoso börja utveckla mikrotjänster för att snabbt få tillgång till programmet, utan risk för den ursprungliga kodbasen.<br/><br/> Windows-containrar ger samma fördelar som containrar i allmänhet. De ger bättre flexibilitet, portabilitet och kontroll.<br/><br/> Contoso kan dra nytta av sina investeringar i Software Assurance och använda Azure Hybrid Benefit för både SQL Server och Windows Server.<br/><br/> Efter migreringen behövs inte längre stöd för Windows Server 2008 R2. [Läs mer](https://support.microsoft.com/lifecycle).<br/><br/> Contoso kan konfigurera webbnivån för appen med flera instanser, så att den inte längre är en felkritisk systemdel.<br/><br/> Den är inte längre beroende av åldrande SQL Server 2008 R2.<br/><br/> SQL Database stöder Contosos tekniska krav. Contosos administratörer utvärderade den lokala databasen med hjälp av Data Migration Assistant och kom fram till att den var kompatibel.<br/><br/> SQL Database har inbyggd feltolerans som Contoso inte behöver konfigurera. Detta säkerställer att datanivån inte längre är en felkritisk systemdel.
**Nackdelar** | Containrar är mer komplexa än andra migreringsalternativ. Inlärningskurvan för containrar kan vara ett problem för Contoso. De medför komplexitet på en ny nivå, som ger stort värde trots kurvan.<br/><br/> Driftteamet på Contoso måste lära sig mer om Azure, containrar och mikrotjänster för appen.<br/><br/> Om Contoso använder Data Migration Assistant i stället för Azure Database Migration Service för att migrera databasen, så har den inte den infrastruktur som är klar för migrering av databaser i stor skala.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Migreringsprocess

1. Contoso etablerar Azure Service Fabric-kluster för Windows.

1. De etablerar en Azure SQL-instans och migrerar SmartHotel360-databasen till den.

1. Contoso konverterar den virtuella datorns webbnivå till en Docker-container med hjälp av Service Fabric SDK-verktyg.

1. Den ansluter Service Fabric-klustret till ACR och distribuerar appen med hjälp av Azure Service Fabric.

    ![Migreringsprocess](./media/contoso-migration-rearchitect-container-sql/migration-process.png)

### <a name="azure-services"></a>Azure-tjänster

**Tjänst** | **Beskrivning** | **Kostnad**
--- | --- | ---
[Data Migration Assistant (DMA)](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Utvärderar och identifierar kompatibilitetsproblem som kan påverka databasfunktioner i Azure. DMA utvärderar funktionsparitet mellan SQL-källor och -mål och rekommenderar förbättringar av prestanda och tillförlitlighet. | Det här verktyget kan laddas ned utan kostnad.
[Azure SQL Database](https://azure.microsoft.com/services/sql-database) | En intelligent, fullständigt hanterad och molnbaserad relationsdatabastjänst. | Kostnaden baseras på funktioner, dataflöde och storlek. [Läs mer](https://azure.microsoft.com/pricing/details/sql-database/managed).
[Azure Container Registry](https://azure.microsoft.com/services/container-registry) | Lagrar avbildningar för alla typer av containerdistributioner. | Kostnad baserad på funktioner, lagring och användningstid. [Läs mer](https://azure.microsoft.com/pricing/details/container-registry).
[Azure Service Fabric](https://azure.microsoft.com/services/service-fabric) | Skapa och hantera skalbara och distribuerade appar som alltid är igång | Kostnaden beräknas på beräkningsnodernas storlek, plats och varaktighet. [Läs mer](https://azure.microsoft.com/pricing/details/service-fabric).
[Azure DevOps](https://docs.microsoft.com/azure/azure-portal/tutorial-azureportal-devops) | Tillhandahåller en pipeline för kontinuerlig integrering och distribution (CI/CD) för utveckling av appar. Pipelinen börjar med en Git-lagringsplats för hantering av app-kod, ett build-system för att skapa paket och andra build-artefakter och ett versionshanteringssystem för att distribuera ändringar i utvecklings-, test- och produktionsmiljöer.

## <a name="prerequisites"></a>Förutsättningar

Det här behöver Contoso för att köra detta scenario:

<!-- markdownlint-disable MD033 -->

**Krav** | **Detaljer**
--- | ---
**Azure-prenumeration** | Contoso skapade prenumerationer i en tidigare i den här artikelserien. Om du inte har någon Azure-prenumeration kan du skapa ett [kostnadsfritt konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Om du skapar ett kostnadsfritt konto är du administratör för din prenumeration och kan utföra alla åtgärder.<br/><br/> Om du använder en befintlig prenumeration och inte är administratör måste du be administratören att ge dig ägar- eller deltagarbehörighet.
**Azure-infrastruktur** | [Läs om](./contoso-migration-infrastructure.md) hur Contoso konfigurerade en Azure-infrastruktur tidigare.
**Krav för utvecklare** | Contoso behöver följande verktyg på en arbetsstation för utvecklare:<br/><br/> - [Visual Studio 2017 Community Edition: Version 15,5](https://www.visualstudio.com)<br/><br/> .NET-arbetsbelastning aktiverad.<br/><br/> - [Git](https://git-scm.com)<br/><br/> - [Service Fabric SDK 3.0 eller senare](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started)<br/><br/> - [Docker CE (Windows 10) eller Docker EE (Windows Server)](https://docs.docker.com/docker-for-windows/install) konfigurerat att använda Windows-containrar.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Steg i scenariot

Så här genomför Contoso migreringen:

> [!div class="checklist"]
>
> - **Steg 1: etablera en SQL Database-instans i Azure.** Contoso tillhandahåller en SQL-instans i Azure. När den virtuella datorn för klientdelen har migrerats till en Azure-container kommercontainerinstansen med appens klientdel att vara riktad mot den här databasen.
> - **Steg 2: skapa en Azure Container Registry (ACR).** Contoso etablerar ett företagscontainerregister för avbildningarna av Docker-containern.
> - **Steg 3: etablera Azure-Service Fabric.** Contoso etablerar ett Service Fabric-kluster.
> - **Steg 4: hantera Service Fabric-certifikat.** Contoso konfigurerar certifikat för åtkomst till klustret för Azure DevOps Services.
> - **Steg 5: Migrera databasen med DMA.** Contoso migrerar appdatabasen med Data Migration Assistant.
> - **Steg 6: Konfigurera Azure DevOps Services.** Contoso konfigurerar ett nytt projekt i Azure DevOps-tjänster och importerar koden till Git-lagringsplatsen.
> - **Steg 7: konvertera appen.** Contoso konverterar appen till en container med hjälp av Azure DevOps och SDK-verktyg.
> - **Steg 8: Konfigurera build och release.** Contoso konfigurerar pipeliner för kompilering och lansering för att skapa och publicera appen till ACR- och Service Fabric-klustret.
> - **Steg 9: utöka appen.** När appen är offentlig utökas den för att dra nytta av Azure-funktionerna. Därefter publiceras den på nytt i Azure med hjälp av pipelinen.

## <a name="step-1-provision-an-azure-sql-database"></a>Steg 1: etablera en Azure SQL Database

Contosos administratörer etablerar en Azure SQL-databas.

1. De väljer att skapa en **SQL Database** i Azure.

    ![Etablera SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql1.png)

1. De anger ett databasnamn som matchar databasen som körs på den lokala virtuella datorn (**SmartHotel.Registration**). De placerar databasen i resursgruppen ContosoRG. Detta är den resursgrupp som används för produktionsresurser i Azure.

    ![Etablera SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql2.png)

1. De skapar en ny SQL Server-instans (**sql-smarthotel-eus2**) i den primära regionen.

    ![Etablera SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql3.png)

1. De ställer in prisnivån så att den matchar server- och databasbehoven. De väljer också att spara pengar med Azure Hybrid Benefit eftersom de redan har en SQL Server-licens.

1. För att ändra storlek använder de v-Core-baserade inköp, och anger begränsningarna för de förväntade kraven.

    ![Etablera SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql4.png)

1. Sedan skapar de databasinstansen.

    ![Etablera SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql5.png)

1. När instansen har skapats öppnar de databasen och noterar information som de behöver när de använder Data Migration Assistant för migrering.

    ![Etablera SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql6.png)

**Behöver du mer hjälp?**

- [Få hjälp](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal) med att etablera en SQL-databas.
- [Läs mer](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools) om resursgränser för virtuell kärna.

## <a name="step-2-create-an-acr-and-provision-an-azure-container"></a>Steg 2: skapa en ACR och etablera en Azure-behållare

Azure-containern skapas med de exporterade filerna från den virtuella webbdatorn. Behållaren är sparad i Azure Container Registry (ACR).

1. Contosos administratörer skapar ett containerregister med Azure-portalen.

     ![Container Registry](./media/contoso-migration-rearchitect-container-sql/container-registry1.png)

1. De skapar ett namn för registret (**contosoacreus2**) och placerar det i den primära regionen i resursgruppen som de använder för sina infrastrukturresurser. De ger åtkomst till administratörsanvändare och anger den som en Premium-SKU så att de kan använda georeplikering.

    ![Container Registry](./media/contoso-migration-rearchitect-container-sql/container-registry2.png)

## <a name="step-3-provision-azure-service-fabric"></a>Steg 3: etablera Azure-Service Fabric

Containern SmartHotel360 kommer att köras i Azure Service Fabric-klustret. Contosos administratörer skapar Service Fabric-klustret enligt följande:

1. Skapa en Service Fabric-resurs från Azure Marketplace.

     ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric1.png)

1. I **Grundläggande** tillhandahåller de ett unikt DS-namn för klustret och autentiseringsuppgifter för åtkomst till den lokala virtuella datorn. De placerar resursen i produktionsresursgruppen (**ContosoRG**) i den primära regionen USA, östra 2.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric2.png)

1. I **Nodtypskonfiguration** anger de ett nodnamn, hållbarhet inställningar, storlek på den virtuella datorn och programslutpunkter.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric3.png)

1. I **Skapa nyckelvalv** skapar de ett nyckelvalv i infrastrukturresursgruppen där certifikatet ska ligga.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric4.png)

1. I **Åtkomstprinciper** ger de virtuella datorer behörighet att distribuera nyckelvalvet.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric5.png)

1. De anger ett namn för certifikatet.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric6.png)

1. På sidan Sammanfattning kopieras länken som används för att hämta certifikatet. De behöver detta för att ansluta till Service Fabric-klustret.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric7.png)

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric8.png)

1. När verifieringen har godkänts etablerar de klustret.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric9.png)

1. I guiden Importera certifikat importerar de det hämtade certifikatet till utvecklardatorer. Certifikatet används för att autentisera till klustret.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric10.png)

1. När klustret har etablerats ansluter de till Service Fabric-klusterutforskaren.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric11.png)

1. De måste välja rätt certifikat.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric12.png)

1. Service Fabric Explorer läses in och contoso-administratören kan hantera klustret.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric13.png)

## <a name="step-4-manage-service-fabric-certificates"></a>Steg 4: hantera Service Fabric certifikat

Contoso behöver klustercertifikat för åtkomst till klustret för Azure DevOps Services. Contosos administratörer konfigurerar detta.

1. Öppna Azure-portalen och bläddra till Nyckelvalv.

1. De öppnar certifikaten och kopierar tumavtrycket för det certifikat som skapades under etablerings processen.

    ![Kopiera tumavtryck](./media/contoso-migration-rearchitect-container-sql/cert1.png)

1. De kopierar det till en textfil för att komma åt det senare.

1. Nu lägger de till ett klientcertifikat som kommer att vara ett administratörsklientcertifikat på klustret. Detta gör att Azure DevOps-tjänster kan ansluta till klustret för att distribuera appar i lanseringspipelinen. För att göra det öppnar de Key Vault i portalen och väljer sedan **certifikat** > **generera/importera**.

    ![Generera klientcertifikat](./media/contoso-migration-rearchitect-container-sql/cert2.png)

1. De anger namnet på certifikatet och anger ett unikt X.509-namn i **Ämne.**

     ![Certifikatnamn](./media/contoso-migration-rearchitect-container-sql/cert3.png)

1. När certifikatet har skapats laddar de ned det lokalt i PFX-format.

     ![Ladda ner certifikat](./media/contoso-migration-rearchitect-container-sql/cert4.png)

1. Därefter går de tillbaka till certifikatlistan i nyckelvalvet och kopierar tumavtrycket för det klientcertifikat som precis har skapats. De sparar det i text filen.

     ![Tumavtryck för klientcertifikat](./media/contoso-migration-rearchitect-container-sql/cert5.png)

1. För distribution av Azure DevOps Services måste de bestämma Base64-värdet för certifikatet. De gör detta på den lokala utvecklararbetsstationen med PowerShell. De klistrar in utdata i en textfil för senare användning.

    ```powershell
    [System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("C:\path\to\certificate.pfx"))
    ```

     ![Base64-värde](./media/contoso-migration-rearchitect-container-sql/cert6.png)

1. Slutligen lägger de till det nya certifikatet i Service Fabric-klustret. Det gör du genom att öppna klustret i portalen och sedan välja **säkerhet**.

     ![Lägg till klientcertifikat](./media/contoso-migration-rearchitect-container-sql/cert7.png)

1. De väljer **Lägg till** > **administratörsklient** och klistrar in i tumavtrycket för det nya klientcertifikatet. Därefter väljer de **Lägg till**. Det här kan ta upp till 15 minuter.

     ![Lägg till klientcertifikat](./media/contoso-migration-rearchitect-container-sql/cert8.png)

## <a name="step-5-migrate-the-database-with-dma"></a>Steg 5: Migrera databasen med DMA

Contoso-administratörerna migrerar nu SmartHotel360-databasen med hjälp av DMA.

### <a name="install-dma"></a>Installera DMA

1. De hämtar verktyget från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595) till den lokala, virtuella SQL Server-datorn (**SQLVM**).

1. De kör installationsprogrammet (DownloadMigrationAssistant.msi) på den virtuella datorn.

1. På sidan **Slutför** väljer de **Starta Microsoft Data Migration Assistant** innan de avslutar guiden.

### <a name="configure-the-firewall"></a>Konfigurera brandväggen

För att ansluta till Azure SQL Database har contoso-administratörerna konfigurerat en brandväggsregel för att tillåta åtkomst.

1. I egenskaperna för **brandväggen och virtuella nätverk** för databasen ger de tillgång till Azure-tjänster och lägger till en regel för klientens IP-adress för den lokala virtuella SQL Serverdatorn.

1. En brandväggsregel på servernivå skapas.

    ![Brandvägg](./media/contoso-migration-rearchitect-container-sql/sql-firewall.png)

**Behöver du mer hjälp?**

[Lär dig](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) mer om att skapa och hantera brandväggsregler för Azure SQL Database.

### <a name="migrate"></a>Migrera

Contoso-administratörerna migrerar nu databasen.

1. I DMA skapar du ett nytt projekt (**SmartHotelDB**) och väljer sedan **migrering**.

1. De väljer **SQL Server** som källservertyp och anger **Azure SQL Database** som mål.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-1.png)

1. I informationen om migreringen lägger de till **SQLVM** som källserver och databasen **SmartHotel.Registration**.

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-2.png)

1. De får ett felmeddelande som verkar vara förknippat med autentiseringen. Efter närmare undersökning visar det sig dock att punkten (.) i databasnamnet är problemet. För att lösa problemet beslutade de att etablera en ny SQL-databas med namnet **SmartHotel-Registration**. När de kör DMA igen kan de välja **SmartHotel-registrering**och fortsätta med guiden.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-3.png)

1. I **Välj objekt** väljer de databastabellerna och genererar ett SQL-skript.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-4.png)

1. När DMA har skapat skriptet väljer de **Distribuera schema**.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-5.png)

1. DMA bekräftar att distributionen har slutförts.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-6.png)

1. Nu påbörjar de migreringen.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-7.png)

1. När migreringen är klar kan Contoso verifiera att databasen körs på Azure SQL-instansen.

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-8.png)

1. De tar bort den extra SQL-databasen **SmartHotel.Registration** i Azure Portal.

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-9.png)

## <a name="step-6-set-up-azure-devops-services"></a>Steg 6: Konfigurera Azure DevOps Services

Contoso måste bygga DevOps-infrastrukturen och pipelines för programmet. För att göra det skapar Contoso-administratörerna ett nytt Azure DevOps-projekt, importerar koden och konfigurerar sedan kompilerings- och lanseringspipelines.

1. I Contoso Azure DevOps-kontot skapar de ett nytt projekt (**ContosoSmartHotelRearchitect**) och väljer **git** för versions kontroll.
![Nytt projekt](./media/contoso-migration-rearchitect-container-sql/vsts1.png)

1. De importerar Git-lagringsplatsen som för närvarande innehåller appens kod. Den finns på en [offentlig lagringsplats](https://github.com/Microsoft/SmartHotel360-internal-booking-apps) och kan laddas ned.

    ![Ladda ned appkod](./media/contoso-migration-rearchitect-container-sql/vsts2.png)

1. När koden har importerats ansluter de Visual Studio till lagringsplatsen och klonar koden med hjälp av Team Explorer.

1. När databasen har klonats till utvecklarens dator öppnar de lösningsfilen för appen. Webbappen och WCF-tjänsten har separata projekt i filen.

    ![Lösningsfil](./media/contoso-migration-rearchitect-container-sql/vsts4.png)

## <a name="step-7-convert-the-app-to-a-container"></a>Steg 7: konvertera appen till en behållare

Den lokala appen är en vanlig app på tre nivåer:

- Den innehåller WebForms och en WCF-tjänst som ansluter till SQL Server.
- Den använder Entity Framework för att integrera med data i SQL-databasen och exponerar den via en WCF-tjänst.
- WebForms-programmet interagerar med WCF-tjänsten.

Contoso-administratörer kommer att konvertera appen till en container med hjälp av Visual Studio och SDK-verktyg enligt följande:

1. Med Visual Studio granskar de den öppna lösnings filen (SmartHotel.Registration.sln) i **katalogen** SmartHotel360-Internal-Booking-apps\src\Registration i den lokala lagringsplatsen. Två appar visas. Webbklientdelens SmartHotel.Registration.Web och WCF-tjänstappen SmartHotel.Registration.WCF.

    ![Container](./media/contoso-migration-rearchitect-container-sql/container2.png)

1. De högerklickar på webbappen > **Lägga till** > **Stöd för Container Orchestator**.

1. I **Lägg till stöd för Container Orchestrator** väljer de **Service Fabric**.

    ![Container](./media/contoso-migration-rearchitect-container-sql/container3.png)

1. De upprepar processen för appen SmartHotel.Registration.WCF.

1. Nu kontrollerar de hur lösningen har ändrats.

    - Den nya appen är **SmartHotel.RegistrationApplication/**
    - Den innehåller två tjänster: **SmartHotel. registration. WCF** och **SmartHotel. registration. Web**.

    ![Container](./media/contoso-migration-rearchitect-container-sql/container4.png)

1. Visual Studio skapade Docker-filen och hämtade de avbildningar som krävs lokalt till utvecklardatorn.

    ![Container](./media/contoso-migration-rearchitect-container-sql/container5.png)

1. En manifestfil (**ServiceManifest. xml**) skapas och öppnas av Visual Studio. Filen instruerar Service Fabric hur containern ska konfigureras när den distribueras till Azure.

    ![Container](./media/contoso-migration-rearchitect-container-sql/container6.png)

1. En annan manifestfil (**ApplicationManifest.xml) innehåller konfigurationsprogram för containrarna.

    ![Container](./media/contoso-migration-rearchitect-container-sql/container7.png)

1. De öppnar filen **ApplicationParameters/Cloud.xml** och uppdaterar anslutningssträngen för att ansluta appen till Azure SQL-databasen. Anslutningssträngen kan finnas i databasen i Azure Portal.

    ![Anslutningssträng](./media/contoso-migration-rearchitect-container-sql/container8.png)

1. De skickar den uppdaterade koden och push-överför till Azure DevOps Services.

    ![Checka in](./media/contoso-migration-rearchitect-container-sql/container9.png)

## <a name="step-8-build-and-release-pipelines-in-azure-devops-services"></a>Steg 8: bygga och släppa pipelines i Azure DevOps Services

Contoso-administratörerna konfigurerar nu Azure DevOps för att utföra kompilerings- och lanseringsprocessen för att verkställa DevOps-tjänsterna.

1. I Azure DevOps väljer de **Kompilering och Lansering** > **Ny pipeline**.

    ![Ny pipeline](./media/contoso-migration-rearchitect-container-sql/pipeline1.png)

1. De väljer **Azure DevOpsRepos Git** och den relevanta lagringsplatsen.

    ![Git och lagringsplats](./media/contoso-migration-rearchitect-container-sql/pipeline2.png)

1. I **Välj en mall** väljer de en infrastruktur med stöd för Docker.

     ![Infrastruktur och Docker](./media/contoso-migration-rearchitect-container-sql/pipeline3.png)

1. De ändrar åtgärdstaggbilderna för att **Kompilera en avbildning** och konfigurerar uppgiften att använda den etablerade ACR:n.

     ![Register](./media/contoso-migration-rearchitect-container-sql/pipeline4.png)

1. I aktiviteten **Push-överför avbildningar** konfigurerar de avbildningen så att den flyttas till ACR och väljer att inkludera den senaste taggen.

1. I **Utlösare** aktiverar de kontinuerlig integrering och lägger till huvudgrenen.

    ![Utlösare](./media/contoso-migration-rearchitect-container-sql/pipeline5.png)

1. De väljer **Spara och köa** för att starta en kompilering.

1. När kompileringen har slutförts övergår de till lanseringspipelinen. I Azure DevOps väljer de **Lansering** > **Ny pipeline**.

    ![Lanseringspipeline](./media/contoso-migration-rearchitect-container-sql/pipeline6.png)

1. De väljer mallen för distribution av **Azure-Service Fabric** och namnger scenen (**SmartHotelSF**).

    ![Miljö](./media/contoso-migration-rearchitect-container-sql/pipeline7.png)

1. De skapar ett namn för pipelinen (**ContosoSmartHotel360Rearchitect**). För scenen väljer de **1 jobb, 1 uppgift** för att konfigurera Service Fabric-distributionen.

    ![Fas och uppgift](./media/contoso-migration-rearchitect-container-sql/pipeline8.png)

1. Nu väljer de **Ny** för att lägga till en ny klusteranslutning.

    ![Ny anslutning](./media/contoso-migration-rearchitect-container-sql/pipeline9.png)

1. I **Lägg till Service Fabric-tjänstanslutning** konfigurerar de anslutningen och de autentiseringsinställningar som kommer att användas av Azure DevOps Services för att distribuera appen. Klusterslutpunkten kan finnas i Azure Portal och de lägger till **tcp://** som prefix.

1. Den certifikatinformation som samlas in är indata för **Servercertifikatets tumavtryck** och **Klientcertifikat**.

    ![Certifikat](./media/contoso-migration-rearchitect-container-sql/pipeline10.png)

1. De väljer pipelinen > **Lägga till en artefakt**.

     ![Artefakt](./media/contoso-migration-rearchitect-container-sql/pipeline11.png)

1. De väljer projektet och bygger pipelinen med den senaste versionen.

     ![Utveckla](./media/contoso-migration-rearchitect-container-sql/pipeline12.png)

1. Observera att blixten på artefakten har markerats.

     ![Artefaktstatus](./media/contoso-migration-rearchitect-container-sql/pipeline13.png)

1. Observera också att den kontinuerliga distributionsutlösaren är aktiverad.
   ![Kontinuerlig distribution aktiverad](./media/contoso-migration-rearchitect-container-sql/pipeline14.png)

1. De väljer **Spara** > **Skapa en lansering**.

    ![Frisläpp](./media/contoso-migration-rearchitect-container-sql/pipeline15.png)

1. När distributionen är klar körs Service Fabric av SmartHotel360.

    ![Publicera](./media/contoso-migration-rearchitect-container-sql/publish4.png)

1. För att ansluta till appen dirigerar de trafiken till den offentliga IP-adressen för Azure Load Balancer framför Service Fabric-noderna.

    ![Publicera](./media/contoso-migration-rearchitect-container-sql/publish5.png)

## <a name="step-9-extend-the-app-and-republish"></a>Steg 9: utöka appen och publicera igen

När SmartHotel360-appen och databasen väl körs i Azure vill Contoso utöka appen.

- Contosos utvecklare är prototyper av ett nytt .NET Core-program som ska köras på Service Fabric klustret.
- Appen kommer att användas för att hämta sentimentdata från Cosmos DB.
- Dessa data kommer att vara i formatet Tweets som bearbetas med en serverlös Azure-funktion och Azure Cognitive Services API för textanalys.

### <a name="provision-azure-cosmos-db"></a>Etablera Azure Cosmos DB

Som första steg etablerar Contosos administratörer en Azure Cosmos-databas.

1. De skapar en Azure Cosmos DB-resurs på Azure Marketplace.

    ![Utöka](./media/contoso-migration-rearchitect-container-sql/extend1.png)

1. De tillhandahåller ett databasnamn (**contososmarthotel**) väljer SQL-API:et och placerar resursen i produktionsresursgruppen i den primära regionen USA, östra 2.

    ![Utöka](./media/contoso-migration-rearchitect-container-sql/extend2.png)

1. I **Komma igång**väljer de **Datautforskaren** och lägger till en ny samling.

1. I **Lägg till** samling uppger de ID och anger lagringskapacitet och dataflöde.

    ![Utöka](./media/contoso-migration-rearchitect-container-sql/extend3.png)

1. I portalen öppnar de den nya databasen > **samling** > **dokument**och väljer sedan **nytt dokument**.

1. De klistrar in följande JSON-kod i dokumentfönstret. Detta är exempeldata i form av en enda tweet.

    ```json
    {
            "id": "2ed5e734-8034-bf3a-ac85-705b7713d911",
            "tweetId": 927750234331580911,
            "tweetUrl": "https://twitter.com/status/927750237331580911",
            "userName": "CoreySandersWA",
            "userAlias": "@CoreySandersWA",
            "userPictureUrl": "",
            "text": "This is a tweet about #SmartHotel360",
            "language": "en",
            "sentiment": 0.5,
            "retweet_count": 1,
            "followers": 500,
            "hashtags": [
                ""
            ]
    }
    ```

    ![Utöka](./media/contoso-migration-rearchitect-container-sql/extend4.png)

1. De identifierar Cosmos DB-slutpunkten och autentiseringsnyckeln. Dessa används i appen för att ansluta till samlingen. I databasen väljer de **Nycklar** och kopierar URI:n och primärnyckeln till Anteckningar.

    ![Utöka](./media/contoso-migration-rearchitect-container-sql/extend5.png)

### <a name="update-the-sentiment-app"></a>Uppdatera sentimentappen

När Cosmos DB har etablerats kan Contosos administratörer konfigurera vilken app som ska anslutas till den.

1. I Visual Studio öppnar de filen ApplicationModern\ApplicationParameters\cloud.xml i Solution Explorer.

    ![Sentimentapp](./media/contoso-migration-rearchitect-container-sql/sentiment1.png)

1. De fyller i följande två parametrar:

   ```xml
   <Parameter Name="SentimentIntegration.CosmosDBEndpoint" Value="[URI]" />
   ```

   ```xml
   <Parameter Name="SentimentIntegration.CosmosDBAuthKey" Value="[Key]" />
   ```

    ![Sentimentapp](./media/contoso-migration-rearchitect-container-sql/sentiment2.png)

### <a name="republish-the-app"></a>Publicera om appen

När Contosos administratörer har utökat appen publicerar de om den till Azure med hjälp av pipelinen.

1. De skickar den uppdaterade koden och push-överför den till Azure DevOps Services. Detta startar kompilerings- och lanseringspipelinen.

1. När kompileringen och distributionen är klara körs Service Fabric av SmartHotel360. I Service Fabric Management Console visas nu tre tjänster.

    ![Publicera om](./media/contoso-migration-rearchitect-container-sql/republish3.png)

1. De kan nu klicka igenom tjänsterna för att se att SentimentIntegration-appen är igång.

    ![Publicera om](./media/contoso-migration-rearchitect-container-sql/republish4.png)

## <a name="clean-up-after-migration"></a>Rensa efter migreringen

Efter migreringen måste Contoso utföra följande steg för rensning:

- Ta bort de lokala virtuella datorerna från vCenter-lagret.
- Ta bort de virtuella datorerna från lokala säkerhetskopieringsjobb.
- Uppdatera intern dokumentation för att visa den nya platsen för appen SmartHotel360. Visa att databasen körs i Azure SQL-databasen och att klientdelen körs i Service Fabric.
- Granska alla resurser som interagerar med de inaktiverade virtuella datorerna och uppdatera alla relevanta inställningar eller dokumentation så att de överensstämmer med den nya konfigurationen.

## <a name="review-the-deployment"></a>Granska distributionen

Med de migrerade resurserna i Azure måste Contoso fullständigt operationalisera och skydda sin nya infrastruktur.

### <a name="security"></a>Säkerhet

- Contosos administratörer måste se till att deras nya databas för **SmartHotel-registrering** är säker. [Läs mer](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).
- Framför allt bör de uppdatera containern så att den använder SSL med certifikat.
- De bör överväga att använda Key Vault för att skydda hemligheter för deras Service Fabric-appar. [Läs mer](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="backups"></a>Säkerhetskopior

- Contoso måste granska kraven för säkerhetskopiering för Azure SQL-databasen. [Läs mer](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).
- Contosos administratörer bör överväga att implementera redundansgrupper för att tillhandahålla regional redundans för databasen. [Läs mer](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview).
- De kan dra nytta av geo-replikering för ACR Premium-SKU:n. [Läs mer](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication).
- Contoso måste överväga att distribuera webbappen i huvudregionen USA, östra 2 och USA, centrala när webbappen för containrar blir tillgänglig. Contosos administratörer skulle kunna konfigurera Traffic Manager för att säkerställa redundansväxling i händelse av regionala avbrott.
- Cosmos DB säkerhetskopieras automatiskt. Contoso [Läs om](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore) den här processen för att lära dig mer.

### <a name="licensing-and-cost-optimization"></a>Licensierings- och kostnadsoptimering

- När alla resurser har distribuerats bör Contoso tilldela Azure-taggar baserat på deras [infrastrukturplanering](./contoso-migration-infrastructure.md#set-up-tagging).
- All licensiering är inbyggd i kostnaden för de PaaS-tjänster som Contoso använder. Detta kommer att dras av från Enterprise-avtalet.
- Contoso aktiverar Azure Cost Management som licensieras av Cloudyn, ett Microsoft-dotterbolag. Det är en kostnadshanteringslösning med flera moln som hjälper dig att använda och hantera Azure och andra molnresurser. [Läs mer](https://docs.microsoft.com/azure/cost-management/overview) om Azure Cost Management.

## <a name="conclusion"></a>Sammanfattning

I den här artikeln omstrukturerade Contoso SmartHotel360-appen i Azure genom att migrera appens frontend-VM till Service Fabric. App-databasen migrerades till en Azure SQL-databas.
