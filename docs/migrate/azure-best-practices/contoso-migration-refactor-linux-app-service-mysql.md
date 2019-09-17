---
title: Omstrukturera en Linux Service Desk-app till Azure App Service och Azure Database for MySQL
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Läs om hur Contosos omstrukturerar sin lokala Linux-app genom att migrera den till Azure App Service med hjälp GitHub på webbnivå och Azure SQL Database.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: e504d4032fc019af43ec7cb1e8513504196559a2
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024216"
---
# <a name="refactor-a-linux-app-to-multiple-regions-using-azure-app-service-traffic-manager-and-azure-database-for-mysql"></a>Omstrukturera en Linux-app till flera regioner med Azure App Service, Traffic Manager och Azure Database for MySQL

Den här artikeln beskriver hur det fiktiva företaget Contoso omstrukturerar en Linux-baserad Apache/MySQL/PHP-app (LAMP) med två nivåer och migrerar den från den lokala miljön till Azure med hjälp av Azure App Service med GitHub och Azure Database for MySQL.

osTicket, supportappen som används i det här exemplet, är tillgänglig som öppen källkod. Om du vill använda den i ett eget test kan du ladda ned den från [GitHub](https://github.com/osTicket/osTicket).

## <a name="business-drivers"></a>Affärsdrivande faktorer

IT-ledningsgruppen har arbetat tillsammans med affärspartner för att komma fram till vad man vill uppnå:

- **Hantera företagets tillväxt.** Contoso växer och flyttas till nya marknader. Det behöver ytterligare kundtjänstagenter.
- **Skala.** Lösningen bör skapas så att Contoso kan lägga till fler kundtjänstagenter efter hand som verksamheten växer.
- **Förbättra elasticitet.**  Förr brukade systemproblem endast påverka interna användare. Med den nya affärsmodellen kommer externa användare att påverkas. Därför måste Contosos app ständigt vara i drift.

## <a name="migration-goals"></a>Migreringsmål

Molnteamet för Contoso har fastställt mål för migreringen för att avgöra vilken migreringsmetod som är bäst:

- Programmet bör skalanpassas bortom den aktuella lokala kapaciteten och prestandan. Contoso flyttar programmet för att dra nytta av Azures skalning på begäran.
- Contoso vill flytta programkodbasen till en pipeline för kontinuerlig leverans. Efter hand som ändringar push-överförs till GitHub vill Contoso distribuera ändringarna utan åtgärder för driftpersonalen.
- Programmet måste vara elastiskt med funktioner för tillväxt och redundans. Contoso vill distribuera appen i två olika Azure-regioner och konfigurera den så att den skalanpassas automatiskt.
- Contoso vill minimera databasadministrationen när programmet har flyttats till molnet.

## <a name="solution-design"></a>Lösningsdesign

När man har fastställt målen och kraven utformar och granskar Contoso en distributionslösning och identifierar migreringsprocessen, inklusive de Azure-tjänster som ska användas vid migreringen.

## <a name="current-architecture"></a>Nuvarande arkitektur

- Appen är indelad i nivåer på två virtuella datorer (OSTICKETWEB och OSTICKETMYSQL).
- De virtuella datorerna finns på VMware ESXi-värden **contosohost1.contoso.com** (version 6.5).
- VMware-miljön hanteras av vCenter Server 6.5 (**vcenter.contoso.com**), som körs på en virtuell dator.
- Contoso har ett lokalt datacenter (contoso-datacenter) med en lokal domänkontrollant (**contosodc1**).

![Nuvarande arkitektur](./media/contoso-migration-refactor-linux-app-service-mysql/current-architecture.png)

## <a name="proposed-architecture"></a>Föreslagen arkitektur

Här är den föreslagna arkitekturen:

- Webbnivå-appen på OSTICKETWEB kommer att migreras genom att kompilera en Azure App Service i två Azure-regioner. Azure App Service för Linux implementeras med hjälp av Docker-behållaren PHP 7.0.
- Appens kod kommer att flyttas till GitHub. Azure App Service-webbappen konfigureras för kontinuerlig leverans med GitHub.
- Azure App-servrar kommer att distribueras i både den primära (USA, östra 2) och den sekundära regionen (centrala USA).
- Traffic Manager kommer att konfigureras framför de två webbapparna i båda regionerna.
- Traffic Manager kommer att konfigureras i prioritetsläge för att tvinga trafiken genom USA, östra 2.
- Om Azure App-servern i USA, östra 2 kopplas från kan användarna komma åt redundansappen i centrala USA.
- Appdatabasen migreras till tjänsten Azure Database for MySQL PaaS med MySQL Workbench-verktyg. Den lokala databasen säkerhetskopieras lokalt och återställs direkt till Azure Database for MySQL.
- Databasen kommer att ligga i den primära regionen USA, östra2, i databasundernätet (PROD-DB-EUS2) i produktionsnätverket (VNET-PROD-EUS2):
- Eftersom de migrerar en produktionsarbetsbelastning placeras Azure-resurserna i produktionsresursgruppen **ContosoRG**.
- Traffic Managerresursen kommer att distribueras i Contosos infrastrukturresursgrupp **ContosoInfraRG**.
- De lokala, virtuella datorerna i Contoso-datacentret kommer att inaktiveras när migreringen är färdig.

![Scenariots arkitektur](./media/contoso-migration-refactor-linux-app-service-mysql/proposed-architecture.png)

## <a name="migration-process"></a>Migreringsprocess

Så här genomför Contoso migreringen:

1. Som ett första steg konfigurerar Contosos administratörer Azure-infrastrukturen. Detta inbegriper att etablera Azure App Service, installera Traffic Manager och etablera av en instans av Azure Database for MySQL.
2. När Azure har förberetts migrerar de databasen med MySQL Workbench.
3. När databasen är igång i Azure konfigurerar de en privat GitHub-lagringsplats för Azure App Service med kontinuerlig leverans och läser in den med appen osTicket.
4. I Azure Portal läser de in appen från GitHub till Docker-behållaren som kör Azure App Service.
5. De kan justerar DNS-inställningarna och konfigurerar automatiskskalning för appen.

![Migreringsprocess](./media/contoso-migration-refactor-linux-app-service-mysql/migration-process.png)

### <a name="azure-services"></a>Azure-tjänster

**Tjänst** | **Beskrivning** | **Kostnad**
--- | --- | ---
[Azure App Service](https://azure.microsoft.com/services/app-service) | Tjänsten kör och skalanpassar program med Azure PaaS-tjänsten för webbplatser. | Prissättningen baseras på instansernas storlek och de funktioner som krävs. [Läs mer](https://azure.microsoft.com/pricing/details/app-service/windows).
[Traffic Manager](https://azure.microsoft.com/services/traffic-manager) | En belastningsutjämnare som använder DNS för att dirigera användare till Azure eller externa webbplatser och tjänster. | Priset baseras på antalet mottagna DNS-frågor och antalet övervakade slutpunkter. | [Läs mer](https://azure.microsoft.com/pricing/details/traffic-manager).
[Azure Database for MySQL](https://docs.microsoft.com/azure/mysql) | Databasen baseras på MySQL-servermotorn med öppen källkod. Den innehåller en fullständigt hanterad, företagsklar community-version av en MySQL-databas som en apputvecklings- och appdistributionstjänst. | Priset baseras på kraven på processorstyrka, lagring och säkerhetskopiering. [Läs mer](https://azure.microsoft.com/pricing/details/mysql).

## <a name="prerequisites"></a>Förutsättningar

Det här behöver Contoso för att köra detta scenario.

<!-- markdownlint-disable MD033 -->

**Krav** | **Detaljer**
--- | ---
**Azure-prenumeration** | Contoso skapade prenumerationer i en tidigare i den här artikelserien. Om du inte har någon Azure-prenumeration kan du skapa ett [kostnadsfritt konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Om du skapar ett kostnadsfritt konto är du administratör för din prenumeration och kan utföra alla åtgärder.<br/><br/> Om du använder en befintlig prenumeration och inte är administratör måste du be administratören att ge dig ägar- eller deltagarbehörighet.
**Azure-infrastruktur** | Contoso konfigurerar Azure-infrastrukturen enligt beskrivningen i [Azure-infrastrukturen för migrering.](./contoso-migration-infrastructure.md)

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Scenariosteg

Så här slutför Contoso migreringen:

> [!div class="checklist"]
>
> - **Steg 1: Etablera Azure App Service.** Contosos administratörer etablerar webbappar i de primära och sekundära regionerna.
> - **Steg 2: Konfigurera Azure Traffic Manager.** De konfigurerar Traffic Manager framför webbapparna för att dirigera och belastingsutjämna trafik.
> - **Steg 3: Etablera MySQL.** I Azure etablerar de en instans av Azure Database for MySQL.
> - **Steg 4: Migrera databasen.** De migrerar databasen med MySQL Workbench.
> - **Steg 5: Konfigurera GitHub.** De konfigurerar en lokal GitHub-lagringsplats för appens webbplatser/kod.
> - **Steg 6: Distribuera webbapparna.** De distribuerar webbapparna från GitHub.

## <a name="step-1-provision-azure-app-service"></a>Steg 1: Etablera Azure App Service

Contosos administratörer etablerar två webbappar (en i varje region) med hjälp av Azure App Service.

1. De skapar en webappresurs i den primära regionen USA, östra2 **(osTicket-eus2**) från Azure Marketplace.
2. De placerar resursen i produktionsresursgruppen **ContosoRG**.

    ![Azure App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app1.png)

3. De skapar en ny App Service-plan i den primära regionen (**app-SVP-EUS2**) och väljer standardstorleken.

     ![Azure App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app2.png)

4. De väljer ett Linux-operativsystem med PHP 7.0 Runtime-stack, som är en Docker-behållare.

    ![Azure App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app3.png)

5. De skapar en andra webbapp (**osTicket-CUS**) och Azure App Service-plan för regionen centrala USA.

    ![Azure App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app4.png)

**Behöver du mer hjälp?**

- Lär mer om [webappar med Azure App Service](https://docs.microsoft.com/azure/app-service/overview).
- Läs om [Azure App Service](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro) i Linux.

## <a name="step-2-set-up-traffic-manager"></a>Steg 2: Konfigurera Traffic Manager

Contosos administratörer konfigurerar Traffic Manager för att dirigera inkommande webbförfrågningar till webbappar som körs på webbnivån för osTicket.

1. De skapar en Traffic Manager-resurs (**osTicket.trafficmanager.net**) från Azure Marketplace. De använder prioriterad routning så att USA, östra 2 är den primära platsen. De placerar resursen i infrastrukturresursgruppen (**ContosoInfraRG**). Observera att Traffic Manager är globalt och inte kopplat till en viss plats.

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager1.png)

2. Nu konfigurerar de Traffic Manager med slutpunkter. De lägger till en webbapp för USA, östra 2, som primärplats (**osticket-eus2**) och appen för centrala USA som sekundär (**osticket-cus**).

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager2.png)

3. När slutpunkterna har lagts till kan de övervaka dem.

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager3.png)

**Behöver du mer hjälp?**

- Läs mer om [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview).
- Läs mer om att [dirigera trafik till en prioriterad slutpunkt](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-configure-priority-routing-method).

## <a name="step-3-provision-azure-database-for-mysql"></a>Steg 3: Etablera Azure Database for MySQL

Contosos administratörer etablerar en MySQL-databasinstans i den primära regionen USA, östra 2.

1. På Azure-portalen skapar de en Azure Database for MySQL-resursen.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-1.png)

2. De lägger till namnet **contosoosticket** för Azure-databasen. De lägger till databasen i produktionsresursgruppen **ContosoRG** och anger autentiseringsuppgifter för den.
3. Den lokala MySQL-databasen är version 5.7, så de väljer den här versionen för kompatibilitet. De använder standardstorlekarna som matchar deras databaskrav.

     ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-2.png)

4. Som **redundansalternativ för säkerhetskopiering** väljer de att använda **geo-redundant**. Med det här alternativet kan de återställa databasen i den sekundära regionen, USA, centrala, om ett avbrott inträffar. De kan bara konfigurera det här alternativet när de etablerar databasen.

    ![Redundans](./media/contoso-migration-refactor-linux-app-service-mysql/db-redundancy.png)

5. De konfigurerar anslutningssäkerheten. I databasen > **Anslutningssäkerhet** konfigurerar de brandväggsreglerna så att databasen får åtkomst till Azure-tjänster.

6. De lägger till den lokala datorns klient-IP-adress till start- och slut-IP-adresserna. Detta gör att webbapparna får åtkomst till MySQL-databasen tillsammans med databasklienten som utför migreringen.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-3.png)

## <a name="step-4-migrate-the-database"></a>Steg 4: Migrera databasen

Contosos administratörer migrerar databasen med hjälp av säkerhetskopiering och återställning, med MySQL-verktyg. De installerar MySQL Workbench, säkerhetskopierar databasen från OSTICKETMYSQL och återställer den sedan till Azure Database for MySQL Server.

### <a name="install-mysql-workbench"></a>Installera MySQL Workbench

1. De kontrollerar [kraven och laddar ned MySQL Workbench](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).
2. De installerar MySQL Workbench för Windows i enlighet med [installationsanvisningarna](https://dev.mysql.com/doc/workbench/en/wb-installing.html). Datorn där installationen sker måste vara tillgänglig för den virtuella datorn OSTICKETMYSQL och Azure via Internet.
3. I MySQL Workbench skapar de en MySQL-anslutning till OSTICKETMYSQL.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench1.png)

4. De exporterar databasen som **osTicket** till en lokal, självständig fil.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench2.png)

5. När databasen har säkerhetskopierats lokalt skapas en anslutning till Azure Database for MySQL-instansen.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench3.png)

6. Nu kan de importera (återställa) databasen i Azure Database for MySQL-instansen från den självständiga filen. Ett nytt schema (osTicket) skapas för instansen.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench4.png)

7. När data har återställts kan den frågas med hjälp av Workbench och visas i Azure Portal.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench5.png)

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench6.png)

8. Slutligen måste de uppdatera databasinformationen på webbapparna. På MySQL-instansen öppnar de **Anslutningssträngarna**.

     ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench7.png)

9. I listan över strängar identifierar de webbappinställningar och väljer att kopiera dem.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench8.png)

10. De öppnar ett fönster i Anteckningar och kopierar strängen i en ny fil. De uppdaterar den sedan för att motsvara inställningarna för osticket-databasen, MySQL-instansen och inloggningsinformationen.

     ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench9.png)

11. De kan verifiera servernamnet och inloggningen från **Översikten** i MySQL-instansen i Azure Portal.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench10.png)

## <a name="step-5-set-up-github"></a>Steg 5: Konfigurera GitHub

Contosos administratörer skapar en ny privat GitHub-lagringsplats och konfigurerar en anslutning till osTicket-databasen i Azure Database for MySQL. Sedan läser de in webbprogrammet i Azure App Service.

1. De bläddrar till lagringsplatsen OsTicket Software Public GitHub och förgrenar den till Contoso GitHub-kontot.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github1.png)

2. Efter förgreningen navigerar de till **inkluderingsmappen** och hittar filen **ost-config.php**.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github2.png)

3. Filen öppnas i webbläsaren och de redigerar den.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github3.png)

4. I redigeraren uppdaterar de databasinformationen, särskilt **DBHOST** och **DBUSER**.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github4.png)

5. De genomför sedan ändringarna.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github5.png)

6. För varjewebbapp (**osTicket-eus2** och **osTicket-CUS**) ändrar de **programinställningarna** i Azure Portal.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github6.png)

7. De anger anslutningssträngen med namnet **osTicket**och kopierar strängen från anteckningar till **värdeområdet**. De väljer **MySQL** i listrutan bredvid strängen och sparar inställningarna.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github7.png)

## <a name="step-6-configure-the-web-apps"></a>Steg 6: Konfigurera webbapparna

Som det sista steget i migreringsprocessen konfigurerar Contosos administratörer webbapparna med osTicket-webbplatserna.

1. I den primära webbappen (**osTicket-eus2**) öppnar de **distributionsalternativet** och anger **GitHub** som källa.

    ![Konfigurera app](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app1.png)

2. De väljer distributionsalternativ.

    ![Konfigurera app](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app2.png)

3. När de har angett alternativen visas konfigurationen som väntande i Azure Portal.

    ![Konfigurera app](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app3.png)

4. När konfigurationen har uppdaterats och osTicket-webbappen har lästs in från GitHub till Docket-behållaren som kör Azure App Service visas platsen som aktiv.

    ![Konfigurera app](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app4.png)

5. De upprepar stegen ovan för den sekundära webbappen (**osTicket-CUS**).
6. När platsen har konfigurerats är den tillgänglig via Traffic Manager profilen. DNS-namnet är den nya platsen för osTicket-appen. [Läs mer](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain#map-a-cname-record).

    ![Konfigurera app](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app5.png)

7. Contoso vill ha ett DNS-namn som är lätt att komma ihåg. De skapar en aliasresurspost (CNAME) **osTicket.contoso.com** som pekar på Traffic Manager-namnet i DNS för deras domänkontrollanter.

    ![Konfigurera app](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app6.png)

8. De konfigurerar båda webbapparna (**osTicket-eus2** och **osTicket-CUS**) webbappar så att anpassade värdnamn tillåts.

    ![Konfigurera app](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app7.png)

### <a name="set-up-autoscaling"></a>Konfigurera automatisk skalning

Slutligen ställer de in automatisk skalning för appen. Detta innebär att appinstanserna ökar och minskar när agenter använder appen i förhållande till verksamhetens behov.

1. I App Service **APP-SRV-EUS2** öppnar de **skalnings enheten**.
2. De konfigurerar en ny inställning för autoskalning med en enda regel som ökar antalet instanser med en när processorprocenten för den aktuella instansen är över 70 % i 10 minuter.

    ![Automatisk skalning](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale1.png)

3. De konfigurerar samma inställning på **APP-SRV-CUS** för att säkerställa att samma beteende gäller om appen växlar över till den sekundära regionen. Den enda skillnaden är att de anger standardinstansen till 1 eftersom detta endast gäller för redundans.

   ![Automatisk skalning](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale2.png)

## <a name="clean-up-after-migration"></a>Rensa efter migreringen

När migreringen är klar omstruktureras osTicket-appen för att köras i en Azure App Service webbapp med kontinuerlig leverans med hjälp av en privat GitHub-lagringsplats. Appen körs i två regioner för ökad elasticitet. OsTicket-databasen körs i Azure Database for MySQL efter migrering till PaaS-plattformen.

Contoso måste göra följande rensning:

- Ta bort de virtuella VMware-datorerna från vCenter-lagret.
- Ta bort de lokala virtuella datorerna från lokala säkerhetskopieringsjobb.
- Uppdatera intern dokumentation med de nya platserna och IP-adresserna.
- Granska alla resurser som interagerar med de lokala virtuella datorerna och uppdatera alla relevanta inställningar eller dokumentation så att de överensstämmer med den nya konfigurationen.
- Konfigurera om övervakningen så att den pekar på URL:en osticket-trafficmanager.net så att de kan se om appen är igång och körs.

## <a name="review-the-deployment"></a>Granska distributionen

Nu när appen körs måste Contoso operationalisera och säkra den nya infrastrukturen.

### <a name="security"></a>Säkerhet

Contosos säkerhetsteam granskar appen för att fastställa eventuella säkerhetsproblem. De identifierade att kommunikationen mellan osTicket-appen och MySQL-databasinstansen inte har konfigurerats för SSL. De måste göra detta för att säkerställa att databastrafiken inte kan hackas. [Läs mer](https://docs.microsoft.com/azure/mysql/howto-configure-ssl).

### <a name="backups"></a>Säkerhetskopior

- OsTicket-webbappar innehåller inte tillståndsdata och behöver därför inte säkerhetskopieras.
- De behöver inte konfigurera säkerhetskopiering för databasen. Azure Database for MySQL skapar och lagrar automatiskt serversäkerhetskopior. De valde att använda geo-redundans för databasen, så den är elastisk och produktionsklar. Säkerhetskopieringar kan användas för att återställa servern till en vald tidpunkt. [Läs mer](https://docs.microsoft.com/azure/mysql/concepts-backup).

### <a name="licensing-and-cost-optimization"></a>Licensierings- och kostnadsoptimering

- Det finns inga licensproblem för PaaS-distributionen.
- Contoso aktiverar Azure Cost Management som licensieras av Cloudyn, ett Microsoft-dotterbolag. Det är en kostnadshanteringslösning med flera moln som hjälper dig att använda och hantera Azure och andra molnresurser. [Läs mer](https://docs.microsoft.com/azure/cost-management/overview) om Azure Cost Management.
