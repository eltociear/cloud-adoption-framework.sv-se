---
title: Byta värd för en Linux-supportapp till Azure och Azure Database for MySQL
description: Se hur Contoso byter värd för en lokal Linux-app genom att migrera den till virtuella Azure-datorer och Azure Database for MySQL.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: d6f812c8f32ec9481942f697151e7ed803654a1b
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807418"
---
# <a name="rehost-an-on-premises-linux-app-to-azure-vms-and-azure-database-for-mysql"></a>Byta värd för en lokal Linux-app till virtuella Azure-datorer och Azure Database for MySQL

Den här artikeln beskriver hur det fiktiva företaget Contoso byter värd för en Linux-baserad Apache/MySQL/PHP-app (LAMP) med två nivåer och migrerar den från den lokala miljön till Azure med hjälp av virtuella Azure-datorer och Azure Database for MySQL.

osTicket, supportappen som används i det här exemplet, är tillgänglig som öppen källkod. Om du vill använda den i ett eget test kan du ladda ned den från [GitHub](https://github.com/osTicket/osTicket).

## <a name="business-drivers"></a>Affärsdrivande faktorer

IT-ledningsgruppen har arbetat tillsammans med affärspartner för att komma fram till vad man vill uppnå:

- **Hantera företagets tillväxt.** Contoso växer, vilket leder till tryck på lokala system och infrastruktur.
- **Begränsa risken.** Supportappen är viktig för verksamheten. Contoso vill flytta den till Azure utan några risker.
- **Utöka.** Contoso vill inte ändra appen just nu. Det vill bara hålla appen stabil.

## <a name="migration-goals"></a>Migreringsmål

Molnteamet för Contoso har fastställt mål för migreringen för att avgöra vilken migreringsmetod som är bäst:

- Efter migreringen ska appen i Azure ha samma prestandafunktioner som den har i dag i den lokala VMware-miljön. Appen är lika viktig i molnet som den är lokalt.
- Contoso vill inte investera i den här appen. Den är viktig för verksamheten, men i dess aktuella form vill Contoso bara flytta den till molnet på ett säkert sätt.
- Efter att ha gjort ett par migreringar av Windows-appar vill Contoso lära sig hur man använder en Linux-baserad infrastruktur i Azure.
- Contoso vill minimera databasadministrationen när programmet har flyttats till molnet.

## <a name="proposed-architecture"></a>Föreslagen arkitektur

I det här scenariot:

- Appen är nivåindelad på två virtuella datorer (`OSTICKETWEB` och `OSTICKETMYSQL`).
- De virtuella datorerna finns på VMware ESXi-värden `contosohost1.contoso.com` (version 6.5).
- VMware-miljön hanteras av vCenter Server 6.5 (`vcenter.contoso.com`) som körs på en virtuell dator.
- Contoso har ett lokalt datacenter (`contoso-datacenter`) med en lokal domänkontrollant (`contosodc1`).
- Webbnivåappen på `OSTICKETWEB` migreras till en virtuell Azure IaaS-dator.
- Appdatabasen migreras till tjänsten Azure Database for MySQL PaaS.
- Eftersom Contoso migrerar en produktionsarbetsbelastning placeras resurserna i produktionsresursgruppen `ContosoRG`.
- Resurserna replikeras till den primära regionen (USA, östra 2) och placeras i produktionsnätverket (`VNET-PROD-EUS2`):
  - Den virtuella webbdatorn placeras i undernätet på klientsidan (`PROD-FE-EUS2`).
  - Databasinstansen placeras i databasundernätet (`PROD-DB-EUS2`).
- Appdatabasen migreras till Azure Database for MySQL med MySQL-verktyg.
- De lokala, virtuella datorerna i Contosos datacentret inaktiveras när migreringen är färdig.

![Scenariots arkitektur](./media/contoso-migration-rehost-linux-vm-mysql/architecture.png)

## <a name="migration-process"></a>Migreringsprocessen

Så här genomför Contoso migreringen:

Migrering av den virtuella webbdatorn:

1. Som ett första steg konfigurerar Contoso Azure-infrastrukturen och den lokala infrastrukturen som krävs för att distribuera Site Recovery.
2. När de har förberett Azure-komponenterna och de lokala komponenterna konfigurerar och aktiverar Contoso replikering för den virtuella webbdatorn.
3. När replikeringen är igång migrerar Contoso den virtuella datorn genom att redundansväxla till Azure.

Migrering av databasen:

1. Contoso etablerar en MySQL-instans i Azure.
2. Contoso konfigurerar MySQL Workbench och säkerhetskopierar databasen lokalt.
3. Contoso återställer sedan databasen från den lokala säkerhetskopian till Azure.

![Migreringsprocessen](./media/contoso-migration-rehost-linux-vm-mysql/migration-process.png)

### <a name="azure-services"></a>Azure-tjänster

**Tjänst** | **Beskrivning** | **Kostnad**
--- | --- | ---
[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery) | Tjänsten orkestrerar och hanterar migrering och haveriberedskap för virtuella Azure-datorer, lokala virtuella datorer och fysiska servrar. | Vid replikering till Azure debiteras Azure Storage-avgifter. Virtuella Azure-datorer skapas och medför kostnader i samband med en redundansväxling. [Läs mer](https://azure.microsoft.com/pricing/details/site-recovery) om avgifter och priser.
[Azure Database for MySQL](https://docs.microsoft.com/azure/mysql) | Databasen baseras på MySQL-servermotorn med öppen källkod. Den innehåller en fullständigt hanterad, företagsklar community-version av en MySQL-databas som en apputvecklings- och appdistributionstjänst.

## <a name="prerequisites"></a>Krav

Det här är vad Contoso behöver i det här scenariot.

<!-- markdownlint-disable MD033 -->

**Krav** | **Detaljer**
--- | ---
**Azure-prenumeration** | Contoso skapade prenumerationer i en tidigare artikel. Om du inte har någon Azure-prenumeration kan du skapa ett [kostnadsfritt konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Om du skapar ett kostnadsfritt konto är du administratör för din prenumeration och kan utföra alla åtgärder.<br/><br/> Om du använder en befintlig prenumeration och inte är administratör måste du be administratören att ge dig ägar- eller deltagarbehörighet.<br/><br/> Om du behöver mer detaljerade behörigheter läser du [den här artikeln](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Azure-infrastruktur** | Contoso konfigurerar Azure-infrastrukturen enligt beskrivningen i [Azure-infrastruktur för migrering.](./contoso-migration-infrastructure.md)<br/><br/> Läs mer om specifika [nätverks-](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#network) och [lagringskrav](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#storage) för Site Recovery.
**Lokala servrar** | Den lokala vCenter-servern bör köra version 5.5, 6.0 eller 6.5<br/><br/> En ESXi-värd som kör version 5.5, 6.0 eller 6.5<br/><br/> En eller flera virtuella VMware-datorer som körs på ESXi-värden.
**Lokala virtuella datorer** | [Granska kraven för virtuella Linux-datorer](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#replicated-machines) som stöds för migrering med Site Recovery.<br/><br/> Kontrollera att [Linux-filsystemen och Linux-lagringssystemen stöds](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#linux-file-systemsguest-storage).<br/><br/> Virtuella datorer måste uppfylla [kraven för Azure](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#azure-vm-requirements).

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Scenariosteg

Contosos administratörer utför migreringen på följande sätt:

> [!div class="checklist"]
>
> - **Steg 1: Förbered Azure för Site Recovery.** De skapar ett Azure Storage-konto för att lagra replikerade data och skapar ett Recovery Services-valv.
> - **Steg 2: Förbered lokala VMware för Site Recovery.** De förbereder konton för identifiering av virtuella datorer och installation av agenter, och förbereder för att ansluta till virtuella Azure-datorer efter en redundansväxling.
> - **Steg 3: etablera databasen.** I Azure etablerar de en instans av Azure Database for MySQL.
> - **Steg 4: replikera virtuella datorer.** De konfigurerar käll- och målmiljön för Site Recovery, konfigurerar en replikeringsprincip och startar replikeringen av virtuella datorer till Azure Storage.
> - **Steg 5: Migrera databasen.** De konfigurerar migrering med MySQL-verktyg.
> - **Steg 6: migrera de virtuella datorerna med Site Recovery.** Till sist kör de ett redundanstest för att se till att allt fungerar och kör sedan en fullständig redundansväxling för att migrera de virtuella datorerna till Azure.

## <a name="step-1-prepare-azure-for-the-site-recovery-service"></a>Steg 1: Förbered Azure för tjänsten Site Recovery

Contoso behöver ett par Azure-komponenter för Site Recovery:

- Ett virtuellt nätverk där resurser som växlats över finns. Contoso har redan skapat det virtuella nätverket under [distributionen av Azure-infrastrukturen](./contoso-migration-infrastructure.md)
- Ett nytt Azure-lagringskonto för att lagra replikerade data.
- Ett Recovery Services-valv i Azure.

Contosos administratörer skapar ett lagringskonto och valv enligt följande:

1. De skapar ett lagringskonto (**contosovmsacc20180528**) i regionen USA, östra 2.

    - Lagringskontot måste finnas i samma region som Recovery Services-valvet.
    - De använder ett konto för generell användning, med standardlagring och LRS-replikering.

    ![Site Recovery-lagring](./media/contoso-migration-rehost-linux-vm-mysql/asr-storage.png)

2. Med nätverks- och lagringskontot på plats skapar de ett valv (ContosoMigrationVault) och placerar det i resursgruppen **ContosoFailoverRG** i den primära regionen USA, östra 2.

    ![Recovery Services-valv](./media/contoso-migration-rehost-linux-vm-mysql/asr-vault.png)

**Behöver du mer hjälp?**

[Lär dig hur du](https://docs.microsoft.com/azure/site-recovery/tutorial-prepare-azure) konfigurerar Azure för Site Recovery.

## <a name="step-2-prepare-on-premises-vmware-for-site-recovery"></a>Steg 2: Förbered lokala VMware för Site Recovery

Contosos administratörer förbereder den lokala VMware-infrastrukturen på följande sätt:

- De skapar ett konto på vCenter-servern för att automatisera identifieringen av virtuella datorer.
- De skapar ett konto som tillåter automatisk installation av Mobility Service på virtuella VMware-datorer som ska replikeras.
- De förbereder lokala virtuella datorer så att de kan ansluta till virtuella Azure-datorer när de skapas efter migreringen.

### <a name="prepare-an-account-for-automatic-discovery"></a>Förbereda ett konto för automatisk identifiering

Site Recovery måste ha åtkomst till VMware-servrarna för att:

- Identifiera automatiskt virtuella datorer. Minst ett skrivskyddat konto krävs.
- Samordna replikering, redundans och återställning efter fel. Du behöver ett konto som kan skapa och ta bort diskar, starta virtuella datorer och utföra liknande åtgärder.

Contosos administratörer konfigurerar kontot så här:

1. De skapar en roll på vCenter-nivå.
2. De tilldelar sedan rollen de behörigheter som krävs.

### <a name="prepare-an-account-for-mobility-service-installation"></a>Förbereda ett konto för installation av mobilitetstjänsten

Mobility Service måste installeras på varje virtuell dator som Contoso vill migrera.

- Site Recovery kan utföra en automatisk push-installation av komponenten när du aktiverar replikering av de virtuella datorerna.
- För automatisk installation. Site Recovery behöver ett konto med behörighet att komma åt den virtuella datorn.
- Kontoinformationen anges när replikeringen konfigureras.
- Kontot kan vara ett domänkonto eller ett lokalt konto, så länge det har installationsbehörighet.

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Förbereda för att ansluta till virtuella Azure-datorer efter en redundansväxling

Efter redundansväxlingen till Azure vill Contoso kunna ansluta till de virtuella Azure-datorerna. Contosos administratörer måste göra följande för att göra detta:

- För att få åtkomst via Internet aktiverar de SSH på den lokala virtuella Linux-datorn innan migreringen. För Ubuntu kan detta utföras med hjälp av följande kommando: **sudo apt – Hämta ssh install-y**.
- Efter redundansväxlingen bör de kontrollera **startdiagnostiken** för att visa en skärmbild av den virtuella datorn.
- Om detta inte fungerar måste de kontrollera att den virtuella datorn körs och gå igenom [de här felsökningstipsen](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

**Behöver du mer hjälp?**

- [Lär dig](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-automatic-discovery) hur du skapar och tilldelar en roll för automatisk identifiering.
- [Lär dig](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-mobility-service-installation) hur du skapar ett konto för push-installation av Mobility Service.

## <a name="step-3-provision-azure-database-for-mysql"></a>Steg 3: etablera Azure Database for MySQL

Contosos administratörer etablerar en MySQL-databasinstans i den primära regionen USA, östra 2.

1. På Azure-portalen skapar de en Azure Database for MySQL-resursen.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-1.png)

2. De lägger till namnet **contosoosticket** för Azure-databasen. De lägger till databasen i produktionsresursgruppen **ContosoRG** och anger autentiseringsuppgifter för den.
3. Den lokala MySQL-databasen är version 5.7, så de väljer den här versionen för kompatibilitet. De använder standardstorlekarna som matchar deras databaskrav.

     ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-2.png)

4. Som **redundansalternativ för säkerhetskopiering** väljer de att använda **geo-redundant**. Med det här alternativet kan de återställa databasen i den sekundära regionen, USA, centrala, om ett avbrott inträffar. De kan bara konfigurera det här alternativet när de etablerar databasen.

     ![Redundans](./media/contoso-migration-rehost-linux-vm-mysql/db-redundancy.png)

5. I **VNET-PROD-EUS2**-nätverket > **Tjänstslutpunkter** lägger de till en tjänstslutpunkt (ett databasundernät) för SQL-tjänsten.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-3.png)

6. När de har lagt till undernätet skapar de en regel för virtuella nätverk som tillåter åtkomst från databasundernätet i produktionsnätverket.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-4.png)

## <a name="step-4-replicate-the-on-premises-vms"></a>Steg 4: replikera lokala virtuella datorer

Innan de kan migrera den virtuella webbdatorn till Azure måste Contosos administratörer konfigurera och aktivera replikering.

### <a name="set-a-protection-goal"></a>Ange ett skyddsmål

1. I valvet, under valvnamnet (ContosoVMVault), definierar de ett replikeringsmål (**Komma igång** > **Site Recovery** > **Förbered infrastruktur**.
2. De anger att deras datorer finns lokalt, att de är virtuella VMware-datorer och att de vill replikera till Azure.

    ![Replikeringsmål](./media/contoso-migration-rehost-linux-vm-mysql/replication-goal.png)

### <a name="confirm-deployment-planning"></a>Bekräfta distributionsplanering

För att fortsätta bekräftar de att distributionsplaneringen är klar genom att välja **Ja, det har jag gjort**. Contoso migrerar bara en enskild virtuell dator i det här scenariot och behöver ingen distributionsplanering.

### <a name="set-up-the-source-environment"></a>Konfigurera källmiljön

Nu konfigurerar Contosos administratörer källmiljön. Det gör de genom att använda en OVF-mall för att distribuera en Site Recovery-konfigurationsserver som en virtuell VMware-dator med hög tillgänglig. När konfigurationsservern är igång registrerar de den i valvet.

Konfigurationsservern kör flera komponenter:

- Konfigurationsserverkomponenten som samordnar kommunikationen mellan den lokala miljön och Azure och hanterar datareplikering.
- Processervern som fungerar som en replikeringsgateway. Den tar emot replikeringsdata, optimerar dem med cachelagring, komprimering och kryptering och skickar dem till Azure Storage.
- Processervern installerar också mobilitetstjänsten på de virtuella datorer du vill replikera, samt utför automatisk identifiering av lokala virtuella VMware-datorer.

Contosos administratörer gör detta på följande sätt:

1. De laddar ned OVF-mallen från **Förbered infrastruktur** > **Källa** > **Konfigurationsserver**.

    ![Ladda ned OVF](./media/contoso-migration-rehost-linux-vm-mysql/add-cs.png)

2. De importerar mallen till VMware för att skapa och distribuera den virtuella datorn.

    ![OVF-mall](./media/contoso-migration-rehost-linux-vm-mysql/vcenter-wizard.png)

3. När de aktiverar den virtuella datorn för första gången startar den i en installationsmiljö för Windows Server 2016. De godkänner licensavtalet och anger ett administratörslösenord.
4. När installationen är klar loggar de in på den virtuella datorn som administratörer. Vid första inloggningen körs Azure Site Recovery-konfigurationsverktyget som standard.
5. I verktyget anger de ett namn som ska användas för att registrera konfigurationsservern i valvet.
6. Verktyget kontrollerar att den virtuella datorn kan ansluta till Azure.
7. När anslutningen har upprättats loggar de in i Azure-prenumerationen. Autentiseringsuppgifterna måste ha åtkomst till det valv där de vill registrera konfigurationsservern.

    ![Registrera konfigurationsservern](./media/contoso-migration-rehost-linux-vm-mysql/config-server-register2.png)

8. Verktyget utför vissa konfigurationsåtgärder och startar sedan om datorn.
9. De loggar in på datorn igen och guiden Konfigurera serverhantering startar automatiskt.
10. I guiden väljer de det nätverkskort som ska ta emot replikeringstrafik. Det går inte att ändra den här inställningen när den har konfigurerats.
11. De väljer den prenumeration, den resursgrupp och det valv som konfigurationsservern ska registreras i.

    ![Välja Recovery Services-valv](./media/contoso-migration-rehost-linux-vm-mysql/cswiz1.png)

12. Nu laddar de ned och installerar MySQL Server och VMware PowerCLI.
13. Efter verifieringen anger de FQDN eller IP-adressen för vCenter-servern eller vSphere-värden. De lämnar standardporten och anger ett eget namn för vCenter-servern.
14. De anger kontot som de skapade för automatisk identifiering och de autentiseringsuppgifter som Site Recovery ska använda för att installera Mobility Service automatiskt.

    ![vCenter](./media/contoso-migration-rehost-linux-vm-mysql/cswiz2.png)

15. När registreringen är klar på Azure-portalen kontrollerar de att konfigurationsservern och VMware-servern visas på sidan **Källa** i valvet. Identifieringen kan ta minst 15 minuter.
16. När allt är klart ansluter Site Recovery till VMware-servrar och identifierar virtuella datorer.

### <a name="set-up-the-target"></a>Konfigurera målet

Nu anger Contosos administratörer inställningar för målreplikeringen.

1. De klickar på **Förbered infrastruktur** > **Mål** och välj målinställningarna.
2. Site Recovery kontrollerar att det finns ett Azure-lagringskonto och nätverk på det angivna målet.

### <a name="create-a-replication-policy"></a>Skapa replikeringsprincip

Med käll- och målkonfigurationen är Contosos administratörer redo att skapa en replikeringsprincip.

1. I **Förbered infrastruktur** > **Replikeringsinställningar** > **Replikeringsprincip** >  **Skapa och associera** skapar de principen **ContosoMigrationPolicy**.

2. De använder standardinställningarna:
    - Återställnings **tröskel:** Standardvärdet är 60 minuter. Det här värdet anger hur ofta återställningspunkter skapas. En avisering genereras när den kontinuerliga replikeringen överskrider den här gränsen.
    - **Kvarhållning av återställnings punkter:** Standardvärdet är 24 timmar. Det här värdet anger kvarhållningsperioden för varje återställningspunkt. Replikerade virtuella datorer kan återställas till valfri punkt i ett fönster.
    - **Frekvens för programkonsekventa ögonblicks bilder:** Standardvärdet en timme. Det här värdet anger med vilken frekvens programkonsekventa ögonblicksbilder skapas.

        ![Skapa replikeringsprincip](./media/contoso-migration-rehost-linux-vm-mysql/replication-policy.png)

3. Principen associeras automatiskt med konfigurationsservern.

    ![Associera replikeringsprincipen](./media/contoso-migration-rehost-linux-vm-mysql/replication-policy2.png)

**Behöver du mer hjälp?**

- En fullständig genomgång av de här stegen finns i [Konfigurera haveriberedskap för lokala virtuella VMware-datorer](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial).
- Där finns detaljerade anvisningar som hjälper dig att [konfigurera källmiljön](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-source), [distribuera konfigurationsservern](https://docs.microsoft.com/azure/site-recovery/vmware-azure-deploy-configuration-server) och [konfigurera replikeringsinställningar](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-replication).
- [Lär dig mer](https://docs.microsoft.com/azure/virtual-machines/extensions/agent-linux) om Azures gästagent för Linux.

### <a name="enable-replication-for-the-web-vm"></a>Aktivera replikering för den virtuella webbdatorn

Nu kan Contosos administratörer starta replikeringen av den virtuella datorn **OSTICKETWEB**.

1. I **Replikera program** > **Källa** >  **+Replikera** väljer de källinställningarna.
2. De väljer att aktivera virtuella datorer och väljer källinställningarna, inklusive vCenter-servern och konfigurationsservern.

    ![Aktivera replikering](./media/contoso-migration-rehost-linux-vm-mysql/enable-replication-source.png)

3. Nu anger de målinställningarna. Exempel på dessa är resursgruppen och nätverket där den virtuella Azure-datorn placeras efter redundansväxlingen och lagringskontot där replikerade data ska lagras.

     ![Aktivera replikering](./media/contoso-migration-rehost-linux-vm-mysql/enable-replication2.png)

4. De väljer **OSTICKETWEB** för replikering.

    ![Aktivera replikering](./media/contoso-migration-rehost-linux-vm-mysql/enable-replication3.png)

5. I egenskaperna för den virtuella datorn väljer de det konto som ska användas för att automatiskt installera Mobility Service på den virtuella datorn.

     ![Mobilitetstjänsten](./media/contoso-migration-rehost-linux-vm-mysql/linux-mobility.png)

6. I **Replikeringsinställningar** > **Konfigurera replikeringsinställningar** kontrollerar de att rätt replikeringsprincip används och väljer **Aktivera replikering**. Mobility Service installeras automatiskt.
7. De spårar replikeringens förlopp i **Jobb**. När jobbet **Slutför skydd** har körts är datorn redo för redundans.

**Behöver du mer hjälp?**

En fullständig genomgång av de här stegen finns i [Aktivera replikering](https://docs.microsoft.com/azure/site-recovery/vmware-azure-enable-replication).

## <a name="step-5-migrate-the-database"></a>Steg 5: Migrera databasen

Contosos administratörer migrerar databasen med hjälp av säkerhetskopiering och återställning, med MySQL-verktyg. De installerar MySQL Workbench, säkerhetskopierar databasen från OSTICKETMYSQL och återställer den sedan till Azure Database for MySQL Server.

### <a name="install-mysql-workbench"></a>Installera MySQL Workbench

1. De kontrollerar [kraven och laddar ned MySQL Workbench](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).
2. De installerar MySQL Workbench för Windows i enlighet med [installationsanvisningarna](https://dev.mysql.com/doc/workbench/en/wb-installing.html).
3. I MySQL Workbench skapar de en MySQL-anslutning till OSTICKETMYSQL.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench1.png)

4. De exporterar databasen som **osTicket** till en lokal, självständig fil.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench2.png)

5. När databasen har säkerhetskopierats lokalt skapas en anslutning till Azure Database for MySQL-instansen.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench3.png)

6. Nu kan de importera (återställa) databasen i Azure Database for MySQL-instansen från den självständiga filen. Ett nytt schema (osTicket) skapas för instansen.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench4.png)

## <a name="step-6-migrate-the-vms-with-site-recovery"></a>Steg 6: migrera de virtuella datorerna med Site Recovery

Slutligen kör Contosos administratörer en snabb testning av redundansen och migrerar sedan den virtuella datorn.

### <a name="run-a-test-failover"></a>Köra ett redundanstest

Genom att köra ett redundanstest kan de vara säkra på att allt fungerar som förväntat innan de genomför migreringen.

1. De kör ett redundanstest till den senaste tillgängliga tidpunkten (**Senast bearbetade**).
2. De väljer **Stäng datorn innan du påbörjar redundans**, så att Site Recovery försöker stänga av den virtuella källdatorn innan redundansväxlingen utlöses. Redundansväxlingen fortsätter även om avstängningen misslyckas.
3. Redundanstest:

    - En kravkontroll körs för att säkerställa att alla villkor som krävs för migreringen är uppfyllda.
    - Redundansprocessen bearbetar data så att du kan skapa en virtuell Azure-dator. Om du väljer den senaste återställningspunkten skapas en återställningspunkt utifrån tillgängliga data.
    - En virtuell Azure-dator skapas med hjälp av de data som behandlas i föregående steg.

4. När redundansväxlingen är klar visas repliken av den virtuella Azure-datorn på Azure-portalen. De kontrollerar att den virtuella datorn har rätt storlek, att den är ansluten till rätt nätverk och att den körs.
5. Efter verifieringen rensar de redundansväxlingen och registrerar och sparar eventuella observationer.

### <a name="migrate-the-vm"></a>Migrera den virtuella datorn

För att migrera den virtuella datorn skapar Contosos administratörer en återställningsplan som innehåller den virtuella datorn och växlar över planen till Azure.

1. De skapar en plan och lägger till **OSTICKETWEB** i den.

    ![Återställningsplan](./media/contoso-migration-rehost-linux-vm-mysql/recovery-plan.png)

2. De kör en redundansväxling mot planen. De väljer den senaste återställningspunkten och anger att Site Recovery ska försöka stänga av den lokala virtuella datorn innan redundansväxlingen utlöses. De kan följa redundansförloppet på sidan **Jobb**.

    ![växling vid fel](./media/contoso-migration-rehost-linux-vm-mysql/failover1.png)

3. Under redundansväxlingen skickar vCenter Server kommandon för att stoppa de två virtuella datorerna som körs på ESXi-värden.

    ![växling vid fel](./media/contoso-migration-rehost-linux-vm-mysql/vcenter-failover.png)

4. Efter redundansen kontrollerar de att den virtuella Azure-datorn visas som förväntat i Azure-portalen.

    ![växling vid fel](./media/contoso-migration-rehost-linux-vm-mysql/failover2.png)

5. När de har kontrollerat den virtuella datorn slutför de migreringen. Nu stoppas replikeringen för den virtuella datorn och Site Recovery-debiteringen för den virtuella datorn.

    ![växling vid fel](./media/contoso-migration-rehost-linux-vm-mysql/failover3.png)

**Behöver du mer hjälp?**

- [Lär dig](https://docs.microsoft.com/azure/site-recovery/tutorial-dr-drill-azure) hur du kör ett redundanstest.
- [Lär dig](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans) hur du skapar en återställningsplan.
- [Lär dig](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover) hur du redundansväxlar till Azure.

### <a name="connect-the-vm-to-the-database"></a>Ansluta den virtuella datorn till databasen

Som det sista steget i migreringsprocessen uppdaterar Contosos administratörer anslutningssträngen för appen så att den pekar på Azure Database for MySQL.

1. De skapar en SSH-anslutning till den virtuella datorn OSTICKETWEB med hjälp av Putty eller en annan SSH-klient. Eftersom den virtuella datorn är privat ansluter de med hjälp av den privata IP-adressen.

    ![Ansluta till databasen](./media/contoso-migration-rehost-linux-vm-mysql/db-connect.png)

    ![Ansluta till databasen](./media/contoso-migration-rehost-linux-vm-mysql/db-connect2.png)

2. De uppdaterar inställningarna så att den virtuella datorn **OSTICKETWEB** kan kommunicera med **OSTICKETMYSQL**-databasen. Konfigurationen är för närvarande hårdkodad med den lokala IP-adressen 172.16.0.43.

    **Före uppdateringen:**

    ![Uppdatera IP-adressen](./media/contoso-migration-rehost-linux-vm-mysql/update-ip1.png)

    **Efter uppdateringen:**

    ![Uppdatera IP-adressen](./media/contoso-migration-rehost-linux-vm-mysql/update-ip2.png)

    ![Uppdatera IP-adressen](./media/contoso-migration-rehost-linux-vm-mysql/update-ip3.png)

3. De startar om tjänsten med **systemctl restart apache2**.

    ![Starta om](./media/contoso-migration-rehost-linux-vm-mysql/restart.png)

4. Slutligen uppdaterar de DNS-posterna för **OSTICKETWEB** på en av Contosos domänkontrollanter.

    ![Uppdatera DNS](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

## <a name="clean-up-after-migration"></a>Rensa efter migrering

När migreringen är klar körs osTicket-appens nivåer på virtuella Azure-datorer.

Nu måste Contoso göra följande:

- Ta bort de virtuella VMware-datorerna från vCenter-lagret.
- Ta bort de lokala virtuella datorerna från lokala säkerhetskopieringsjobb.
- Uppdatera intern dokumentation med de nya platserna och IP-adresserna.
- Granska alla resurser som interagerar med de lokala virtuella datorerna och uppdatera alla relevanta inställningar eller dokumentation så att de överensstämmer med den nya konfigurationen.
- Contoso använde Azure Migrate-tjänsten med beroendemappning för att utvärdera den virtuella datorn **OSTICKETWEB** för migrering. De bör nu ta bort agenterna (Microsoft Monitoring Agent och Microsofts beroende agent) som de har installerat för detta ändamål från den virtuella datorn.

## <a name="review-the-deployment"></a>Granska distributionen

Nu när appen körs måste Contoso operationalisera och säkra den nya infrastrukturen.

### <a name="security"></a>Säkerhet

Contosos säkerhetsteam granskar den virtuella datorn och databasen för att fastställa eventuella säkerhetsproblem.

- De granskar nätverkssäkerhetsgrupperna (NSG:er) för den virtuella datorn för att kontrollera åtkomsten. Nätverkssäkerhetsgrupper används för att säkerställa att endast trafik som tillåts för programmet kan passera.
- De kan skydda data på de virtuella datordiskarna med diskkryptering och Azure Key Vault.
- Kommunikationen mellan den virtuella datorn och databasinstansen har inte konfigurerats för SSL. De måste göra detta för att säkerställa att databastrafiken inte kan hackas.

Mer information finns i [rekommenderade säkerhets metoder för IaaS-arbetsbelastningar i Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

### <a name="bcdr"></a>Affärskontinuitet och haveriberedskap

För affärskontinuitet och haveriberedskap vidtar Contoso följande åtgärder:

- **Skydda data.** Contoso säkerhetskopierar dessa data på den virtuella datorn för appen med hjälp av Azure Backup-tjänsten. [Läs mer](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). De behöver inte konfigurera säkerhetskopiering för databasen. Azure Database for MySQL skapar och lagrar automatiskt serversäkerhetskopior. De valde att använda geo-redundans för databasen, så den är elastisk och produktionsklar.
- **Undvika avbrott i apparna.** Contoso replikerar de virtuella datorerna för appen i Azure till en sekundär region med hjälp av Site Recovery. [Läs mer](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Licensierings- och kostnadsoptimering

- När de har distribuerat resurser tilldelar Contoso Azure-taggar, i enlighet med beslut som de fattade under [distributionen av Azure-infrastrukturen](./contoso-migration-infrastructure.md#set-up-tagging).
- Det finns inga licensproblem för Contoso Ubuntu-servrarna.
- Contoso aktiverar Azure Cost Management som licensieras av Cloudyn, ett Microsoft-dotterbolag. Det är en kostnadshanteringslösning med flera moln som hjälper dig att använda och hantera Azure och andra molnresurser. [Läs mer](https://docs.microsoft.com/azure/cost-management/overview) om Azure Cost Management.
