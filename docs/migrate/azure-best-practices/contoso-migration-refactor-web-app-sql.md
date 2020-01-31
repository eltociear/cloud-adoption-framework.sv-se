---
title: Omstrukturera en app genom att migrera den till Azure App Service och Azure SQL Database
description: Lär dig hur Contoso kan vara värd för en lokal app genom att migrera den till en Azure App Service-webbapp och Azure SQL Server-databas.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 35a64b9f42df3737e186d25a43ecad457010607d
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807452"
---
# <a name="refactor-an-on-premises-app-to-an-azure-app-service-web-app-and-azure-sql-database"></a>Omstrukturera en lokal app till en Azure App Service-webbapp och Azure SQL-databas

Den här artikeln visar hur det fiktiva företaget Contoso omstrukturerar en Windows .NET-app med två nivåer som körs på virtuella VMware-datorer som en del av en migrering till Azure. De migrerar appens virtuella frontend-dator till en Azure App Service-webbapp, och app-databasen till en Azure SQL-databas.

SmartHotel360-appen som används i det här exemplet tillhandahålls som öppen källkod. Om du vill använda den i ett eget test kan du ladda ned den från [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Affärsdrivande faktorer

IT-ledningsgruppen har arbetat tillsammans med affärspartner för att komma fram till vad man vill uppnå med migreringen:

- **Hantera företagets tillväxt.** Contoso växer och det finns ett tryck på lokala system och infrastruktur.
- **Öka effektiviteten.** Contoso måste ta bort onödiga procedurer och effektivisera processer för utvecklare och användare. En snabb IT-lösning som inte slösar tid eller pengar är viktigt för företaget, så att man kan leverera snabbare enligt kundkraven.
- **Öka flexibiliteten.**  Contosos IT-avdelning måste reagera snabbare på företagets behov. Den måste kunna reagera snabbare än förändringarna på marknaden för att företaget ska lyckas i en global ekonomi. Den får inte vara i vägen eller bromsa verksamheten.
- **Skala.** När företagets verksamhet växer måste Contosos IT-avdelning tillhandahålla system som kan växa i samma takt.
- **Minska kostnaderna.** Contoso vill minimera licenskostnaderna.

## <a name="migration-goals"></a>Migreringsmål

Contosos molnteam har fastställt mål för migreringen. Målen användes för att fastställa den bästa migreringsmetoden.

<!-- markdownlint-disable MD033 -->

**Krav** | **Detaljer**
--- | ---
**App** | Appen i Azure kommer att vara lika avgörande som den är i dag.<br/><br/> Den bör ha samma prestandafunktioner som den för närvarande har i VMware.<br/><br/> Teamet vill inte investera i appen. Tills vidare nöjer sig administratörerna med att flytta appen säkert till molnet.<br/><br/> Teamet vill avbryta stödet för Windows Server 2008 R2, där appen körs för närvarande.<br/><br/> Teamet vill också övergå från SQL Server 2008 R2 till en modern PaaS-databasplattform, vilket minimerar behovet av hantering.<br/><br/> Contoso vill dra nytta av sina investeringar i SQL Server-licensiering och Software Assurance där det är möjligt.<br/><br/> Contoso vill dessutom minimera den felkritiska systemdelen på webbnivån.
**Begränsningar** | Appen består av en ASP.NET-app och en WCF-tjänst som körs på samma virtuella dator. De vill dela upp detta i två webbappar med hjälp av Azure App Service.
**Azure** | Contoso vill flytta appen till Azure, men vill inte köra den på virtuella datorer. Contoso vill använda Azure PaaS-tjänster för både webb- och data nivåerna.
**DevOps** | Contoso vill flytta till en DevOps-modell med Azure DevOps för sina Build and Release-pipelines.

<!-- markdownlint-enable MD033 -->

## <a name="solution-design"></a>Lösningsdesign

Efter att ha fastställt målen och kraven kan Contoso utforma och granska en distributionslösning och identifiera migreringsprocessen, inklusive de Azure-tjänster som ska användas för migreringen.

### <a name="current-app"></a>Aktuell app

- Den lokala appen SmartHotel360 delas in i nivåer på två virtuella datorer (WEBVM och SQLVM).
- De virtuella datorerna finns på VMware ESXi-värden **contosohost1.contoso.com** (version 6.5)
- VMware-miljön hanteras av vCenter Server 6.5 (**vcenter.contoso.com**), som körs på en virtuell dator.
- Contoso har ett lokalt datacenter (contoso-datacenter) med en lokal domänkontrollant (**contosodc1**).
- De lokala, virtuella datorerna i Contosos datacentret inaktiveras när migreringen är färdig.

### <a name="proposed-solution"></a>Föreslagen lösning

- Contoso jämförde Azure SQL Database med SQL Server med hjälp av [den här artikeln](https://docs.microsoft.com/azure/sql-database/sql-database-features) för appens databasnivå. Contoso beslutade att satsa på Azure SQL Database av flera skäl:
  - Azure SQL Database är en hanterad relationsdatabastjänst. Den ger förutsägbar prestanda på flera servicenivåer med nästan obefintlig administration. Fördelarna är dynamisk skalbarhet utan driftavbrott, inbyggd, intelligent optimering och global skalbarhet och tillgänglighet.
  - Contoso kan använda förenklad Data Migration Assistant (DMA) för att utvärdera och migrera den lokala databasen till Azure SQL.
  - Med Software Assurance kan Contoso byta ut befintliga licenser till rabatterade priser på en SQL-databas med hjälp av Azure Hybrid-förmånen för SQL Server. Det kan ge besparingar på upp till 30 %.
  - SQL Database innehåller säkerhetsfunktioner som alltid krypterad, dynamisk datamaskning och säkerhets-/hotidentifiering på radnivå.
- För appens webbnivå har Contoso beslutat att använda Azure App Service. Med den här PaaS-tjänsten kan du distribuera appen med bara några få konfigurationsändringar. Contoso kommer att använda Visual Studio för att genomföra ändringen och distribuera två webbappar. En för webbplatsen och en för WCF-tjänsten.
- För att uppfylla kraven för en DevOps-pipeline har Contoso valt att använda Azure DevOps för källkodshantering med Git-databaser. Automatiserade versioner och lansering används för att bygga koden och distribuera den till Azure App Service.

### <a name="solution-review"></a>Utvärdering av lösningen

Contoso utvärderar den föreslagna designen genom att sätta samman en lista med för- och nackdelar.

<!-- markdownlint-disable MD033 -->

**Övervägande** | **Detaljer**
--- | ---
**Fördelar** | Koden för SmartHotel360-appen behöver inte ändras för migrering till Azure.<br/><br/> Contoso kan dra nytta av sina investeringar i Software Assurance och använda Azure Hybrid-förmånen för både SQL Server och Windows Server.<br/><br/> Efter migreringen behöver Windows Server 2008 R2 inte stödjas. [Läs mer](https://support.microsoft.com/lifecycle).<br/><br/> Contoso kan konfigurera webbnivån för appen med flera instanser, så att den inte längre är en felkritisk systemdel.<br/><br/> Databasen är inte längre beroende av åldrande SQL Server 2008 R2.<br/><br/> SQL Database stöder de tekniska kraven. Contoso utvärderade den lokala databasen med hjälp av Data Migration Assistant och kom fram till att den var kompatibel.<br/><br/> Azure SQL Database har inbyggd feltolerans som Contoso inte behöver konfigurera. Detta säkerställer att datanivån inte längre är en felkritisk systemdel.
**Nackdelar** | Azure App Service stöder endast en app-distribution för varje webbapp. Det innebär att två webbappar måste etableras (en för webbplatsen och en för WCF-tjänsten).<br/><br/> Om Contoso använder Data Migration Assistant i stället för Azure Database Migration Service för att migrera databasen, så har den inte den infrastruktur som är klar för migrering av databaser i stor skala. Contoso måste bygga en annan region för att säkerställa redundansväxling om den primära regionen inte är tillgänglig.

<!-- markdownlint-enable MD033 -->

## <a name="proposed-architecture"></a>Föreslagen arkitektur

![Scenariots arkitektur](media/contoso-migration-refactor-web-app-sql/architecture.png)

### <a name="migration-process"></a>Migreringsprocessen

1. Contoso etablerar en Azure SQL-instans och migrerar SmartHotel360-databasen till den.
2. Contoso tillhandahåller och konfigurerar webbappar och distribuerar SmartHotel360-appen till dem.

    ![Migreringsprocessen](media/contoso-migration-refactor-web-app-sql/migration-process.png)

### <a name="azure-services"></a>Azure-tjänster

**Tjänst** | **Beskrivning** | **Kostnad**
--- | --- | ---
[Data Migration Assistant (DMA)](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Contoso kommer att använda DMA för att utvärdera och identifiera kompatibilitetsproblem som kan påverka deras databasfunktioner i Azure. DMA utvärderar funktionsparitet mellan SQL-källor och -mål och rekommenderar förbättringar av prestanda och tillförlitlighet. | Det här verktyget kan laddas ned utan kostnad.
[Azure SQL Database](https://azure.microsoft.com/services/sql-database) | En intelligent, fullständigt hanterad och molnbaserad relationsdatabastjänst. | Kostnaden baseras på funktioner, dataflöde och storlek. [Läs mer](https://azure.microsoft.com/pricing/details/sql-database/managed).
[Azure App Service](https://docs.microsoft.com/azure/app-service/overview) | Skapa kraftfulla molnappar med en fullständigt hanterad plattform | Kostnaden baseras på storlek, plats och användningstid. [Läs mer](https://azure.microsoft.com/pricing/details/app-service/windows).
[Azure DevOps](https://docs.microsoft.com/azure/azure-portal/tutorial-azureportal-devops) | Tillhandahåller en pipeline för kontinuerlig integrering och distribution (CI/CD) för utveckling av appar. Pipelinen börjar med en Git-lagringsplats för hantering av app-kod, ett build-system för att skapa paket och andra build-artefakter och ett versionshanteringssystem för att distribuera ändringar i utvecklings-, test- och produktionsmiljöer.

## <a name="prerequisites"></a>Krav

Här måste Contoso måste köra följande scenario:

<!-- markdownlint-disable MD033 -->

**Krav** | **Detaljer**
--- | ---
**Azure-prenumeration** | Contoso skapade prenumerationer i en tidigare artikel. Om du inte har någon Azure-prenumeration kan du skapa ett [kostnadsfritt konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Om du skapar ett kostnadsfritt konto är du administratör för din prenumeration och kan utföra alla åtgärder.<br/><br/> Om du använder en befintlig prenumeration och inte är administratör måste du be administratören att ge dig ägar- eller deltagarbehörighet.
**Azure-infrastruktur** | [Läs om](./contoso-migration-infrastructure.md) hur Contoso konfigurerade en Azure-infrastruktur.

<!--markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Scenariosteg

Contoso genomför migreringen på följande sätt:

> [!div class="checklist"]
>
> - **Steg 1: etablera en SQL Database-instans i Azure.** Contoso tillhandahåller en SQL-instans i Azure. När appens webbplats har migrerats till Azure pekar WCF Service-webbappen på den här instansen.
> - **Steg 2: Migrera databasen med DMA.** Contoso migrerar app-databasen med Data Migration Assistant.
> - **Steg 3: etablera webbappar.** Contoso tillhandahåller de två webbapparna.
> - **Steg 4: Konfigurera Azure-DevOps.** Contoso skapar ett nytt Azure DevOps-projekt och importerar Git-lagringsplatsen.
> - **Steg 5: Konfigurera anslutnings strängar.** Contoso konfigurerar anslutningssträngar så att webbnivåns webbapp, WCF-tjänstens webbapp och SQL-instansen kan kommunicera.
> - **Steg 6: Konfigurera pipeliner för build och release.** Som ett sista steg konfigurerar Contoso Build and Release-pipelines för att skapa appen och distribuerar dem till två separata webbappar.

## <a name="step-1-provision-an-azure-sql-database"></a>Steg 1: etablera en Azure SQL Database

1. Contoso-administratörerna väljer att skapa en SQL Database i Azure.

    ![Etablera SQL](media/contoso-migration-refactor-web-app-sql/provision-sql1.png)

2. De anger ett databasnamn som matchar databasen som körs på den lokala virtuella datorn (**SmartHotel.Registration**). De placerar databasen i resursgruppen ContosoRG. Detta är den resursgrupp som används för produktionsresurser i Azure.

    ![Etablera SQL](media/contoso-migration-refactor-web-app-sql/provision-sql2.png)

3. De skapar en ny SQL Server-instans (**sql-smarthotel-eus2**) i den primära regionen.

    ![Etablera SQL](media/contoso-migration-refactor-web-app-sql/provision-sql3.png)

4. De ställer in prisnivån så att den matchar deras server- och databasbehov. De väljer också att spara pengar med Azure Hybrid-förmån eftersom de redan har en SQL Server-licens.
5. För att ändra storlek använder de v-Core-baserade inköp, och anger begränsningarna för de förväntade kraven.

    ![Etablera SQL](media/contoso-migration-refactor-web-app-sql/provision-sql4.png)

6. Sedan skapar de databasinstansen.

    ![Etablera SQL](media/contoso-migration-refactor-web-app-sql/provision-sql5.png)

7. När instansen har skapats öppnar de databasen och noterar information som de behöver när de använder Data Migration Assistant för migrering.

    ![Etablera SQL](media/contoso-migration-refactor-web-app-sql/provision-sql6.png)

**Behöver du mer hjälp?**

- [Få hjälp](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal) med att etablera en SQL-databas.
- [Läs mer](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools) om resursgränser för virtuell kärna.

## <a name="step-2-migrate-the-database-with-dma"></a>Steg 2: Migrera databasen med DMA

Contoso-administratörer migrerar SmartHotel360-databasen med hjälp av DMA.

### <a name="install-dma"></a>Installera DMA

1. De hämtar verktyget från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595) till den lokala, virtuella SQL Server-datorn (**SQLVM**).
2. De kör installationsprogrammet (DownloadMigrationAssistant.msi) på den virtuella datorn.
3. På sidan **Slutför** väljer de **Starta Microsoft Data Migration Assistant** innan de avslutar guiden.

### <a name="migrate-the-database-with-dma"></a>Migrera databasen med DMA

1. I DMA skapar de ett nytt projekt **(SmartHotelDB**) och väljer **Migrering**.
2. De väljer **SQL Server** som källservertyp och anger **Azure SQL Database** som mål.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-1.png)

3. I informationen om migreringen lägger de till **SQLVM** som källserver och databasen **SmartHotel.Registration**.

     ![DMA](media/contoso-migration-refactor-web-app-sql/dma-2.png)

4. De får ett felmeddelande som verkar vara förknippat med autentiseringen. Efter närmare undersökning visar det sig dock att punkten (.) i databasnamnet är problemet. För att lösa problemet beslutade de att etablera en ny SQL-databas med namnet **SmartHotel-Registration**. När de kör DMA igen kan de välja **SmartHotel-Registration** och fortsätta med guiden.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-3.png)

5. I **Välj objekt** väljer de databastabellerna och genererar ett SQL-skript.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-4.png)

6. När DMA har skapat skriptet väljer de **Distribuera schema**.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-5.png)

7. DMA bekräftar att distributionen har slutförts.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-6.png)

8. Nu påbörjar de migreringen.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-7.png)

9. När migreringen är klar kan Contoso-administratörerna verifiera att databasen körs på Azure SQL-instansen.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-8.png)

10. De tar bort den extra SQL-databasen **SmartHotel.Registration** i Azure Portal.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-9.png)

## <a name="step-3-provision-web-apps"></a>Steg 3: etablera webb program

När databasen har migrerats kan Contoso-administratörerna etablera de två webbapparna.

1. De väljer **Webbapp** på portalen.

    ![Webbapp](media/contoso-migration-refactor-web-app-sql/web-app1.png)

2. De tillhandahåller ett appnamn (**SHWEB-EUS2**), kör det på Windows och placerar det i produktionsresursgruppen **ContosoRG**. De skapar en ny webbapp och Azure App Service- plan.

    ![Webbapp](media/contoso-migration-refactor-web-app-sql/web-app2.png)

3. När webbappen har etablerats upprepas processen för att skapa en webbapp för WCF-tjänsten (**SHWCF-EUS2**)

    ![Webbapp](media/contoso-migration-refactor-web-app-sql/web-app3.png)

4. När de är klara bläddrar de till adressen för apparna för att kontrollera att de har skapats korrekt.

## <a name="step-4-set-up-azure-devops"></a>Steg 4: Konfigurera Azure-DevOps

Contoso måste bygga DevOps-infrastrukturen och pipelines för programmet. För att göra det skapar Contoso-administratörerna ett nytt DevOps-projekt, importerar koden och konfigurerar sedan Build and Release-pipelines.

1. På Contoso Azure DevOps-kontot skapar de ett nytt projekt (**ContosoSmartHotelRefactor**) och väljer **Git** för versionskontroll.

    ![Nytt projekt](./media/contoso-migration-refactor-web-app-sql/vsts1.png)

2. De importerar Git-lagringsplatsen som för närvarande innehåller appens kod. Den finns på en [offentlig lagringsplats](https://github.com/Microsoft/SmartHotel360-internal-booking-apps) och kan laddas ned.

    ![Ladda ned appkod](./media/contoso-migration-refactor-web-app-sql/vsts2.png)

3. När koden har importerats ansluter de Visual Studio till lagringsplatsen och klonar koden med hjälp av Team Explorer.

    ![Ansluta till projekt](./media/contoso-migration-refactor-web-app-sql/devops1.png)

4. När databasen har klonats till utvecklarens dator öppnar de lösningsfilen för appen. Webbappen och WCF-tjänsten har separata projekt i filen.

    ![Lösningsfil](./media/contoso-migration-refactor-web-app-sql/vsts4.png)

## <a name="step-5-configure-connection-strings"></a>Steg 5: Konfigurera anslutnings strängar

Contoso-administratörerna måste se till att webbapparna och databasen kan kommunicera. Det gör de genom att konfigurera anslutningssträngar i koden och i webbapparna.

1. I webbappen för WCF-tjänsten (**SHWCF-EUS2**) > **Inställningar** > **Programinställningar** lägger de till en ny anslutningssträng med namnet **DefaultConnection**.
2. Anslutningssträngen hämtas från databasen för **SmartHotel-registrering** och bör uppdateras med de rätta autentiseringsuppgifterna.

    ![Anslutningssträng](media/contoso-migration-refactor-web-app-sql/string1.png)

3. Med Visual Studio öppnar de projektet **SmartHotel.Registration.wcf** från lösningsfilen. Avsnittet **connectionStrings** i filen web.config för WCF-tjänsten SmartHotel.Registration.Wcf bör uppdateras med anslutningssträngen.

     ![Anslutningssträng](media/contoso-migration-refactor-web-app-sql/string2.png)

4. Avsnittet **client** i filen Web.config för SmartHotel. registration. Web ska ändras så att det pekar på den nya platsen för WCF-tjänsten. Det här är URL:en för WCF-webbappen som är värd för tjänstslutpunkten.

    ![Anslutningssträng](media/contoso-migration-refactor-web-app-sql/strings3.png)

5. När ändringarna väl finns i koden måste administratörerna genomföra ändringarna. Med hjälp av Team Explorer i Visual Studio genomför och synkroniserar de.

## <a name="step-6-set-up-build-and-release-pipelines-in-azure-devops"></a>Steg 6: Konfigurera en pipeline för build och release i Azure DevOps

Contoso-administratörerna konfigurerar nu Azure DevOps för att utföra Build- och Release-processen.

1. I Azure DevOps väljer de **Build and release** > **Ny pipeline**.

    ![Ny pipeline](./media/contoso-migration-refactor-web-app-sql/pipeline1.png)

2. De väljer **Azure Repos Git** och den relevanta lagringsplatsen.

    ![Git och lagringsplats](./media/contoso-migration-refactor-web-app-sql/pipeline2.png)

3. Under **Välj en mall** väljer de ASP.NET-mallen för sin version.

     ![ASP.NET-mall](./media/contoso-migration-refactor-web-app-sql/pipeline3.png)

4. Namnet **ContosoSmartHotelRefactor-ASP.NET-CI** används för versionen. De väljer **Save & Queue** (Spara och köa).

     ![Spara och köa](./media/contoso-migration-refactor-web-app-sql/pipeline4.png)

5. Det här startar den första versionen. De väljer build-numret för att se processen. När det är klart kan de se återkopplingen för processen och välja **Artefakter** för att granska build-resultaten.

    ![Granska](./media/contoso-migration-refactor-web-app-sql/pipeline5.png)

6. **Avlämningsmappen** innehåller build-resultatet.

    - De två zip-filerna är de paket som innehåller apparna.
    - De här filerna används i versionspipelinen för distribution till Azure App Service.

     ![Artefakt](./media/contoso-migration-refactor-web-app-sql/pipeline6.png)

7. De väljer **Versioner** >  **+Ny pipeline**.

    ![Ny pipeline](./media/contoso-migration-refactor-web-app-sql/pipeline7.png)

8. De väljer distributionsmallen för Azure App Service.

    ![Distributionsmall för Azure App Service](./media/contoso-migration-refactor-web-app-sql/pipeline8.png)

9. De tilldelar versionspipelinen namnet **ContosoSmartHotel360Refactor** och anger namnet på WCF-webbappen (SHWCF-EUS2) som **stegets** namn.

    ![Miljö](./media/contoso-migration-refactor-web-app-sql/pipeline9.png)

10. Under stegen väljer de **1 jobb, 1 uppgift** för att konfigurera distributionen av WCF-tjänsten.

    ![Distribuera WCF](./media/contoso-migration-refactor-web-app-sql/pipeline10.png)

11. De verifierar att prenumerationen är markerad och auktoriserad och väljer **App-tjänstnamnet**.

     ![Välja App-tjänstnamnet](./media/contoso-migration-refactor-web-app-sql/pipeline11.png)

12. På pipelinen > **Artefakter** väljer de **+Lägga till en artefakt** och väljer sedan att skapa med pipelinen **ContosoSmarthotel360Refactor**.

     ![Version](./media/contoso-migration-refactor-web-app-sql/pipeline12.png)

13. De markerar blixten på artefakten för att aktivera utlösaren för kontinuerlig distribution.

     ![Blixt](./media/contoso-migration-refactor-web-app-sql/pipeline13.png)

14. Utlösaren för kontinuerlig distribution ska vara inställd på **Aktiverad**.

    ![Kontinuerlig distribution aktiverad](./media/contoso-migration-refactor-web-app-sql/pipeline14.png)

15. Nu går de tillbaka till steget 1-jobb, 1 uppgift och väljer **Distribuera Azure App Service**.

    ![Testa Azure App Service](./media/contoso-migration-refactor-web-app-sql/pipeline15.png)

16. I **Välj en fil eller mapp** hittar de filen **SmartHotel.Registration.Wcf.zip** som skapades under kompileringen och väljer **Spara**.

    ![Spara WCF](./media/contoso-migration-refactor-web-app-sql/pipeline16.png)

17. De väljer **pipeline** > **steg** **+ Lägg**till för att lägga till en miljö för **SHWEB-EUS2**. De väljer en annan Azure App Service-distribution.

    ![Lägga till miljö](./media/contoso-migration-refactor-web-app-sql/pipeline17.png)

18. De upprepar processen för att publicera webbappen (**SmartHotel.Registration.Web.zip**) till rätt webbapp.

    ![Publicera webbapp](./media/contoso-migration-refactor-web-app-sql/pipeline18.png)

19. När versionspipelinen har sparats visas den på följande sätt.

     ![Sammanfattning för versionspipeline](./media/contoso-migration-refactor-web-app-sql/pipeline19.png)

20. De återgår till **Version** och väljer **Utlösare** > **Enable continuous integration** (Aktivera kontinuerlig integrering). Åtgärden aktiverar pipelinen så att en fullständig kompilering och lansering sker när ändringar görs i koden.

    ![Aktivera kontinuerlig integrering](./media/contoso-migration-refactor-web-app-sql/pipeline20.png)

21. De väljer **Save & Queue** (Spara och köa) för att köra hela pipelinen. En ny version utlöses, som i sin tur skapar den första versionen av appen till Azure App Service.

    ![Spara pipeline](./media/contoso-migration-refactor-web-app-sql/pipeline21.png)

22. Contoso-administratörerna kan följa processen för att kompilera och lansera pipelinen från Azure DevOps. När kompileringen är klar startar lanseringen.

    ![Kompilera och lansera app](./media/contoso-migration-refactor-web-app-sql/pipeline22.png)

23. När pipelinen är klar har båda platserna distribuerats och appen körs online.

    ![Slutföra version](./media/contoso-migration-refactor-web-app-sql/pipeline23.png)

I det här läget har appen migrerats till Azure.

## <a name="clean-up-after-migration"></a>Rensa efter migrering

Efter migreringen måste Contoso utföra följande steg för rensning:

- Ta bort de lokala virtuella datorerna från vCenter-lagret.
- Ta bort de virtuella datorerna från lokala säkerhetskopieringsjobb.
- Uppdatera intern dokumentation för att visa den nya platsen för appen SmartHotel360. Visa att databasen körs i Azure SQL-databasen och att klientdelen körs i två webbappar.
- Granska alla resurser som interagerar med de inaktiverade virtuella datorerna och uppdatera alla relevanta inställningar eller dokumentation så att de överensstämmer med den nya konfigurationen.

## <a name="review-the-deployment"></a>Granska distributionen

Med de migrerade resurserna i Azure måste Contoso fullständigt operationalisera och skydda sin nya infrastruktur.

### <a name="security"></a>Säkerhet

- Contoso måste se till att deras nya databas för **SmartHotel-registrering** är säker. [Läs mer](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).
- Framför allt bör Contoso uppdatera webbapparna så att de använder SSL med certifikat.

### <a name="backups"></a>Säkerhetskopior

- Contoso måste granska kraven för säkerhetskopiering för Azure SQL-databasen. [Läs mer](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).
- Contoso behöver också lära mer om hur de hanterar säkerhetskopiering och återställning av SQL-databaser. [Läs mer](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups) om automatisk säkerhetskopiering.
- Contoso bör överväga att implementera redundansgrupper för att tillhandahålla regional redundans för databasen. [Läs mer](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview).
- Contoso måste överväga att distribuera webbappen i huvudregionen USA, östra 2 och Centrala USA för återhämtning. Contoso skulle kunna konfigurera Traffic Manager för att säkerställa redundansväxling i händelse av regionala avbrott.

### <a name="licensing-and-cost-optimization"></a>Licensierings- och kostnadsoptimering

- När alla resurser har distribuerats bör Contoso tilldela Azure-taggar baserat på deras [infrastrukturplanering](./contoso-migration-infrastructure.md#set-up-tagging).
- All licensiering är inbyggd i kostnaden för de PaaS-tjänster som Contoso använder. Detta kommer att dras av från Enterprise-avtalet.
- Contoso aktiverar Azure Cost Management som licensieras av Cloudyn, ett Microsoft-dotterbolag. Det är en kostnadshanteringslösning med flera moln som hjälper dig att använda och hantera Azure och andra molnresurser. [Läs mer](https://docs.microsoft.com/azure/cost-management/overview) om Azure Cost Management.

## <a name="conclusion"></a>Slutsats

I den här artikeln omstrukturerade Contoso SmartHotel360-appen i Azure genom att migrera appens frontend-VM till två Azure App Service-webbappar. Appdatabasen migrerades till en Azure SQL-databas.
