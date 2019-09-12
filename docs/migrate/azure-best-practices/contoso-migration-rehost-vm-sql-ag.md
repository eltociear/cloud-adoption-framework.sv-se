---
title: Byta värd för en app genom att migrera den till virtuella Azure-datorer och SQL Server AlwaysOn-tillgänglighetsgrupp
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Läs om hur Contoso byter värd för en lokal app genom att migrera den till virtuella Azure-datorer och SQL Server AlwaysOn-tillgänglighetsgrupper.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 32a24f51a44c088331ea47a65a5d71e3d02cedf4
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70820341"
---
# <a name="rehost-an-on-premises-app-on-azure-vms-and-sql-server-always-on-availability-group"></a>Byta värd för en lokal app på virtuella Azure-datorer och SQL Server AlwaysOn-tillgänglighetsgrupp

Den här artikeln beskriver hur det fiktiva företaget Contoso byter värd för en Windows .NET-app med två nivåer som körs på virtuella VMware-datorer som en del av en migrering till Azure. Contoso migrerar appens klientdels-VM till en virtuell Azure-dator och appdatabasen till en Azure SQL Server VM, som körs i ett Windows Server-redundanskluster med SQL Server AlwaysOn-tillgänglighetsgrupper.

SmartHotel360-appen som används i det här exemplet tillhandahålls som öppen källkod. Om du vill använda den i ett eget test kan du ladda ned den från [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Affärsdrivande faktorer

IT-ledningsgruppen har arbetat tillsammans med affärspartner för att komma fram till vad man vill uppnå med migreringen:

- **Hantera företagets tillväxt.** Contoso växer, vilket leder till tryck på lokala system och infrastruktur.
- **Öka effektiviteten.** Contoso måste ta bort onödiga procedurer och effektivisera processer för utvecklare och användare. En snabb IT-lösning som inte slösar tid eller pengar är viktigt för företaget, så att man kan leverera snabbare enligt kundkraven.
- **Öka flexibiliteten.** Contosos IT-avdelning måste reagera snabbare på företagets behov. Den måste kunna reagera snabbare än förändringarna på marknaden för att företaget ska lyckas i en global ekonomi. IT-verksamheten får inte vara i vägen eller bromsa verksamheten.
- **Skala.** När företagets verksamhet växer måste Contosos IT-avdelning tillhandahålla system som kan växa i samma takt.

## <a name="migration-goals"></a>Migreringsmål

Contosos molnteam har fastställt mål för migreringen. Målen användes för att fastställa den bästa migreringsmetoden:

- Efter migreringen ska appen i Azure ha samma prestandafunktioner som den har i dag i VMware. Appen är lika viktig i molnet som den är lokalt.
- Contoso vill inte investera i appen. Den är viktig för verksamheten, men i dess aktuella form vill Contoso bara flytta den till molnet på ett säkert sätt.
- Det har förekommit tillgänglighetsproblem med den lokala databasen för appen. Contoso vill distribuera den i Azure som ett kluster med hög tillgänglighet och redundansfunktioner.
- Contoso vill uppgradera från sin nuvarande SQL Server 2008 R2-plattform till SQL Server 2017.
- Contoso vill inte använda en Azure SQL Database för den här appen och letar efter alternativ.

## <a name="solution-design"></a>Lösningsdesign

När man har fastställt målen och kraven utformar och granskar Contoso en distributionslösning och identifierar migreringsprocessen, inklusive de Azure-tjänster som ska användas vid migreringen.

### <a name="current-architecture"></a>Nuvarande arkitektur

- Appen är nivåindelad på två virtuella datorer (WEBVM och SQLVM).
- De virtuella datorerna finns på VMware ESXi-värden **contosohost1.contoso.com** (version 6.5)
- VMware-miljön hanteras av vCenter Server 6.5 (**vcenter.contoso.com**), som körs på en virtuell dator.
- Contoso har ett lokalt datacenter (contoso-datacenter) med en lokal domänkontrollant (**contosodc1**).

### <a name="proposed-architecture"></a>Föreslagen arkitektur

I det här scenariot:

- Contoso migrerar appens klientdels-WEBVM till en virtuell Azure IaaS-dator.
  - Den virtuella klientdelsdatorn i Azure distribueras i resursgruppen ContosoRG (som används för produktionsresurser).
  - Den finns i Azure-produktionsnätverket (VNET-PROD-EUS2) i den primära regionen USA, östra 2.
- Appdatabasen migreras till en Azure SQL Server VM.
  - Den finns i Contosos Azure-databasnätverk (PROD-DB-EUS2) i den primära regionen USA, östra 2.
  - Den placeras i ett Windows Server-redundanskluster med två noder, som använder SQL Server AlwaysOn-tillgänglighetsgrupper.
  - I Azure distribueras de två SQL Server VM-noderna i klustret i resursgruppen ContosoRG.
  - VM-noderna finns i Azure-produktionsnätverket (VNET-PROD-EUS2) i den primära regionen USA, östra 2.
  - Virtuella datorer kör Windows Server 2016 med SQL Server 2017 Enterprise Edition. Contoso har inga licenser för det här operativsystemet, så de använder en avbildning på Azure Marketplace som tillhandahåller licensen som en avgift på deras Azure EA-åtagande.
  - Förutom unika namn använder båda virtuella datorer samma inställningar.
- Contoso distribuerar en intern lastbalanserare som lyssnar efter trafik i klustret och dirigerar den till lämplig klusternod.
  - Den interna lastbalanseraren distribueras i ContosoNetworkingRG (som används för nätverksresurser).
- De lokala, virtuella datorerna i Contosos datacenter inaktiveras när migreringen är färdig.

![Scenariots arkitektur](media/contoso-migration-rehost-vm-sql-ag/architecture.png)

### <a name="database-considerations"></a>Databasöverväganden

Som en del av processen för lösningsdesign gjorde Contoso en funktionsjämförelse mellan Azure SQL Database och SQL Server. Nedanstående överväganden hjälpte dem att välja en virtuell Azure IaaS-dator som kör SQL Server:

- Användning av en virtuell Azure-dator som kör SQL Server verkar vara en optimal lösning om Contoso behöver anpassa operativsystemet eller databasservern, eller om de vill samlokalisera och köra appar från tredje part på samma virtuella dator.
- Med hjälp av Data Migration Assistant kan Contoso enkelt utvärdera och migrera till en Azure SQL Database.

### <a name="solution-review"></a>Lösningsgranskning

Contoso utvärderar den föreslagna designen genom att sätta samman en lista med för- och nackdelar.

<!-- markdownlint-disable MD033 -->

**Övervägande** | **Detaljer**
--- | ---
**Fördelar** | WEBVM kommer att flyttas till Azure utan ändringar, vilket gör migreringen enkel.<br/><br/> SQL Server-nivån kommer att köras på SQL Server 2017 och Windows Server 2016. Det innebär att deras nuvarande Windows Server 2008 R2-operativsystem tas ur bruk, och SQL Server 2017 kan hantera Contosos tekniska krav och mål. IT ger 100 % kompatibilitet samtidigt som man lämnar SQL Server 2008 R2.<br/><br/> Contoso kan dra nytta av sina investeringar i Software Assurance och använda Azure Hybrid-förmånen.<br/><br/> En SQL Server-distribution med hög tillgänglighet i Azure ger feltolerans så att appdatanivån inte längre är en enskild felpunkt.
**Nackdelar** | WEBVM kör Windows Server 2008 R2. Operativsystemet stöds av Azure för specifika roller (juli 2018). [Läs mer](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).<br/><br/> Appens webbnivå förblir en enskild felpunkt.<br/><br/> Contoso måste fortsätta stödja webbnivån som en virtuell Azure-dator i stället för att flytta till en hanterad tjänst, till exempel Azure App Service.<br/><br/> Med den valda lösningen måste Contoso fortsätta hantera två SQL Server VM i stället för att flytta till en hanterad plattform, till exempel Azure SQL Database Managed Instance. Med Software Assurance kan Contoso dessutom byta ut befintliga licenser till rabatterade priser på Azure SQL Database Managed Instance.

<!-- markdownlint-enable MD033 -->

### <a name="azure-services"></a>Azure-tjänster

**Tjänst** | **Beskrivning** | **Kostnad**
--- | --- | ---
[Data Migration Assistant](/sql/dma/dma-overview?view=ssdt-18vs2017) | DMA körs lokalt från den lokala SQL Server-datorn och migrerar databasen över ett plats-till-plats-VPN till Azure. | DMA är ett kostnadsfritt nedladdningsbart verktyg.
[Azure Site Recovery](/azure/site-recovery) | Site Recovery orkestrerar och hanterar migrering och haveriberedskap för virtuella Azure-datorer, lokala virtuella datorer och fysiska servrar. | Under replikeringen till Azure debiteras Azure Storage-avgifter. Virtuella Azure-datorer skapas och medför kostnader i samband med en redundansväxling. [Läs mer](https://azure.microsoft.com/pricing/details/site-recovery) om avgifter och priser.

## <a name="migration-process"></a>Migreringsprocess

Contosos administratörer migrerar appens virtuella datorer till Azure.

- De migrerar klientdels-VM till en virtuell Azure-dator med hjälp av Site Recovery:
  - Som ett första steg förbereder de och konfigurerar Azure-komponenter och förbereder den lokala VMware-infrastrukturen.
  - Med allt förberett kan de börja replikera den virtuella datorn.
  - När replikeringen har aktiverats och fungerar migrerar de den virtuella datorn genom att redundansväxla till Azure.
- De migrerar databasen till ett SQL Server-kluster i Azure med hjälp av Data Migration Assistant (DMA).
  - Som ett första steg måste de etablera virtuella SQL Server-datorer i Azure, konfigurera klustret och en intern lastbalanserare, och konfigurera AlwaysOn-tillgänglighetsgrupper.
  - Med det på plats kan de migrera databasen.
- Efter migreringen aktiverar de AlwaysOn-skydd för databasen.

![Migreringsprocess](media/contoso-migration-rehost-vm-sql-ag/migration-process.png)

## <a name="prerequisites"></a>Förutsättningar

Det här är vad Contoso behöver göra i det här scenariot.

<!-- markdownlint-disable MD033 -->

**Krav** | **Detaljer**
--- | ---
**Azure-prenumeration** | Contoso har redan skapat en prenumeration i en tidigare artikel i den här serien. Om du inte har någon Azure-prenumeration kan du skapa ett [kostnadsfritt konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Om du skapar ett kostnadsfritt konto är du administratör för din prenumeration och kan utföra alla åtgärder.<br/><br/> Om du använder en befintlig prenumeration och inte är administratör måste du be administratören att ge dig ägar- eller deltagarbehörighet.<br/><br/> Om du behöver mer detaljerade behörigheter läser du [den här artikeln](/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Azure-infrastruktur** | [Läs om](contoso-migration-infrastructure.md) hur Contoso konfigurerade en Azure-infrastruktur.<br/><br/> Läs mer om specifika [nätverks-](/azure/site-recovery/vmware-physical-azure-support-matrix#network) och [lagringskrav](/azure/site-recovery/vmware-physical-azure-support-matrix#storage) för Site Recovery.
**Site Recovery (lokalt)** | Den lokala vCenter-servern bör köra version 5.5, 6.0 eller 6.5<br/><br/> En ESXi-värd som kör version 5.5, 6.0 eller 6.5<br/><br/> En eller flera virtuella VMware-datorer som körs på ESXi-värden.<br/><br/> De virtuella datorerna måste uppfylla [kraven för Azure](/azure/site-recovery/vmware-physical-azure-support-matrix#azure-vm-requirements).<br/><br/> Konfiguration av [nätverk](/azure/site-recovery/vmware-physical-azure-support-matrix#network) och [lagring](/azure/site-recovery/vmware-physical-azure-support-matrix#storage) som stöds.<br/><br/> De virtuella datorerna som du vill replikera måste uppfylla [kraven för Azure](/azure/site-recovery/vmware-physical-azure-support-matrix#azure-vm-requirements).

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Steg i scenariot

Contoso genomför migreringen på följande sätt:

> [!div class="checklist"]
>
> - **Steg 1: Förbereda ett kluster.** Skapa ett kluster för att distribuera två SQL Server VM-noder i Azure.
> - **Steg 2: Distribuera och konfigurera klustret.** Förbered ett Azure SQL Server-kluster. Databaser migreras till det här befintliga klustret.
> - **Steg 3: Distribuera lastbalanseraren.** Distribuera en lastbalanserare för att utjämna trafik till SQL Server-noderna.
> - **Steg 4: Förbereda Azure för Site Recovery.** Skapa ett Azure Storage-konto för att lagra replikerade data och ett Recovery Services-valv.
> - **Steg 5: Förbereda lokala VMware för Site Recovery.** Förbered konton för identifiering av virtuella datorer och agentinstallation. Förbered lokala virtuella datorer så att användare kan ansluta till virtuella Azure-datorer efter migreringen.
> - **Steg 6: Replikera virtuella datorer.** Aktivera VM-replikering till Azure.
> - **Steg 7: Installera DMA.** Ladda ned och installera Data Migration Assistant.
> - **Steg 7: Migrera databasen med DMA.** Migrera databasen till Azure.
> - **Steg 9: Skydda databasen.** Skapa en AlwaysOn-tillgänglighetsgrupp för klustret.
> - **Steg 10: Migrera webbapp-VM.** Kör ett redundanstest för att kontrollera att allt fungerar som förväntat. Kör sedan en fullständig redundansväxling till Azure.

## <a name="step-1-prepare-a-sql-server-always-on-availability-group-cluster"></a>Steg 1: Förbereda ett SQL Server AlwaysOn-tillgänglighetsgruppskluster

Contosos administratörer konfigurerar klustret så här:

1. De skapar två SQL Server VM genom att välja SQL Server 2017 Enterprise Windows Server 2016-avbildning på Azure Marketplace.

    ![SQL VM-SKU](media/contoso-migration-rehost-vm-sql-ag/sql-vm-sku.png)

2. I **guiden Skapa virtuell dator** > **Grunder** konfigurerar de:

    - Namn på de virtuella datorerna: **SQLAOG1** och **SQLAOG2**.
    - Eftersom datorerna är affärskritiska aktiverar de SSD för VM-disktypen.
    - De anger autentiseringsuppgifter för datorerna.
    - De distribuerar de virtuella datorerna i den primära regionen USA, ÖSTRA 2, i resursgruppen ContosoRG.

3. I **Storlek** börjar de med D2s_V3 SKU för båda virtuella datorerna. De skalas senare efter behov.
4. I **Inställningar** gör de följande:

    - Eftersom dessa virtuella datorer är kritiska databaser för appen använder de hanterade diskar.
    - De placerar datorerna i produktionsnätverket i den primära regionen USA, ÖSTRA 2 (**VNET-PROD-EUS2**), i databasundernätet (**PROD-DB-EUS2**).
    - De skapar en ny tillgänglighetsuppsättning: **SQLAOGAVSET**, med två feldomäner och fem uppdateringsdomäner.

      ![SQL VM](media/contoso-migration-rehost-vm-sql-ag/sql-vm-settings.png)

5. I **SQL Server-inställningar** begränsar de SQL-anslutningen till det virtuella nätverket (privat), på standardporten 1433. För autentisering använder de samma autentiseringsuppgifter som de använder på plats (**contosoadmin**).

    ![SQL VM](media/contoso-migration-rehost-vm-sql-ag/sql-vm-db.png)

**Behöver du mer hjälp?**

- [Få hjälp](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#1-configure-basic-settings) med att etablera en SQL Server VM.
- [Läs mer](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-prereq#create-sql-server-vms) om att konfigurera virtuella datorer för olika SQL Server-SKU:er.

## <a name="step-2-deploy-and-set-up-the-cluster"></a>Steg 2: Distribuera och konfigurera klustret

Contosos administratörer konfigurerar klustret så här:

1. De konfigurerar ett Azure Storage-konto så att det fungerar som molnvittne.
2. De lägger till SQL Server VM i Active Directory-domänen i Contosos lokala datacenter.
3. De skapar klustret i Azure.
4. De konfigurerar molnvittnet.
5. Slutligen aktiverar de SQL AlwaysOn-tillgänglighetsgrupper.

### <a name="set-up-a-storage-account-as-cloud-witness"></a>Konfigurera ett lagringskonto som molnvittne

För att konfigurera ett molnvittne behöver Contoso ett Azure Storage-konto som innehåller den blobfil som används för klustermedling. Samma lagringskonto kan användas för att konfigurera molnvittne för flera kluster.

Contosos administratörer skapar ett lagringskonto enligt följande:

1. De anger ett identifierbart namn på kontot (**contosocloudwitness**).
2. De distribuerar ett allmänt konto, med LRS.
3. De placerar kontot i en tredje region – USA, södra centrala. De placerar det utanför den primära och sekundära regionen så att det förblir tillgängligt vid ett regionalt fel.
4. De placerar det i sin resursgrupp som innehåller infrastrukturresurser, **ContosoInfraRG**.

    ![Molnvittne](media/contoso-migration-rehost-vm-sql-ag/witness-storage.png)

5. När de skapar lagringskontot genereras primära och sekundära åtkomstnycklar för det. De behöver den primära åtkomstnyckeln för att skapa molnvittnet. Nyckeln visas under lagringskontots namn > **Åtkomstnycklar**.

    ![Åtkomstnyckel](media/contoso-migration-rehost-vm-sql-ag/access-key.png)

### <a name="add-sql-server-vms-to-contoso-domain"></a>Lägga till SQL Server VM i Contoso-domänen

1. Contoso lägger till SQLAOG1 och SQLAOG2 i domänen contoso.com.
2. På varje virtuell dator installerar de sedan Windows-redundansklusterfunktionen och -verktygen.

### <a name="set-up-the-cluster"></a>Konfigurera klustret

Innan Contosos administratörer konfigurerar klustret tar de en ögonblicksbild av OS-disken på varje dator.

![Ögonblicksbild](media/contoso-migration-rehost-vm-sql-ag/snapshot.png)

1. Sedan kör de ett skript som de har tagit fram för att skapa Windows-redundansklustret.

    ![Skapa kluster](media/contoso-migration-rehost-vm-sql-ag/create-cluster1.png)

2. När de har skapat klustret kontrollerar de att de virtuella datorerna visas som klusternoder.

     ![Skapa kluster](media/contoso-migration-rehost-vm-sql-ag/create-cluster2.png)

## <a name="configure-the-cloud-witness"></a>Konfigurera molnvittnet

1. Contosos administratörer konfigurerar molnvittnet med hjälp av **kvorumkonfigurationsguiden** i Klusterhanteraren för växling vid fel.
2. I guiden väljer de att skapa ett molnvittne med lagringskontot.
3. När molnvittnet har konfigurerats visas det i snapin-modulen Klusterhanteraren för växling vid fel.

    ![Molnvittne](media/contoso-migration-rehost-vm-sql-ag/cloud-witness.png)

### <a name="enable-sql-server-always-on-availability-groups"></a>Aktivera SQL Server AlwaysOn-tillgänglighetsgrupper

Nu kan Contosos administratörer aktivera AlwaysOn:

1. I Konfigurationshanteraren för SQL Server aktiverar de **AlwaysOn-tillgänglighetsgrupper** för tjänsten **SQL Server (MSSQLSERVER)** .

    ![Aktivera AlwaysOn](media/contoso-migration-rehost-vm-sql-ag/enable-alwayson.png)

2. De startar om tjänsten för att ändringarna ska börja gälla.

Med AlwaysOn aktiverat kan Contoso konfigurera den AlwaysOn-tillgänglighetsgrupp som skyddar SmartHotel360-databasen.

**Behöver du mer hjälp?**

- [Läs mer](/windows-server/failover-clustering/deploy-cloud-witness) om molnvittne och att konfigurera ett lagringskonto för det.
- [Få instruktioner](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial) om att konfigurera ett kluster och skapa en tillgänglighetsgrupp.

## <a name="step-3-deploy-the-azure-load-balancer"></a>Steg 3: Distribuera Azure Load Balancer

Contosos administratörer vill nu distribuera en intern lastbalanserare som är placerad framför klusternoderna. Lastbalanseraren lyssnar efter trafik och dirigerar den till lämplig nod.

![Belastningsutjämning](media/contoso-migration-rehost-vm-sql-ag/architecture-lb.png)

De skapar lastbalanseraren enligt följande:

1. I Azure-portalen > **Nätverk** > **Belastningsutjämnare** konfigurerar de en ny intern lastbalanserare: **ILB-PROD-DB-EUS2-SQLAOG**.
2. De placerar lastbalanseraren i produktionsnätverket **VNET-PROD-EUS2**, i databasundernätet **PROD-DB-EUS2**.
3. De tilldelar den en statisk IP-adress: 10.245.40.100.
4. Som ett nätverkselement distribuerar de lastbalanseraren i nätverksresursgruppen **ContosoNetworkingRG**.

    ![Belastningsutjämning](media/contoso-migration-rehost-vm-sql-ag/lb-create.png)

När den interna lastbalanseraren har distribuerats måste de konfigurera den. De skapar en serverdelsadresspool, konfigurerar en hälsoavsökning och konfigurerar en lastbalanseringsregel.

### <a name="add-a-back-end-pool"></a>Lägga till en serverdelspool

För att distribuera trafik till de virtuella datorerna i klustret konfigurerar Contosos administratörer en serverdelsadresspool som innehåller IP-adresserna för de nätverkskort för virtuella datorer som tar emot nätverkstrafik från lastbalanseraren.

1. I lastbalanserarens inställningar i portalen lägger Contoso till en serverdelspool: **ILB-PROD-DB-EUS-SQLAOG-BEPOOL**.
2. De associerar poolen med tillgänglighetsuppsättningen SQLAOGAVSET. De virtuella datorerna i uppsättningen (**SQLAOG1** och **SQLAOG2**) läggs till i poolen.

    ![Serverdelspool](media/contoso-migration-rehost-vm-sql-ag/backend-pool.png)

### <a name="create-a-health-probe"></a>Skapa en hälsoavsökning

Contosos administratörer skapar en hälsoavsökning så att lastbalanseraren kan övervaka appens hälsa. Avsökningen lägger till eller tar bort virtuella datorer dynamiskt från lastbalanserarens rotation, baserat på hur de svarar på hälsokontroller.

De skapar avsökningen enligt följande:

1. I lastbalanserarens inställningar i portalen skapar Contoso en hälsoavsökning: **SQLAlwaysOnEndPointProbe**.
2. De anger att avsökningen ska övervaka virtuella datorer på TCP-port 59999.
3. De anger ett intervall på 5 sekunder mellan avsökningar och ett tröskelvärde på 2. Om två avsökningar misslyckas betraktas den virtuella datorn som inte felfri.

    ![Avsökning](media/contoso-migration-rehost-vm-sql-ag/nlb-probe.png)

### <a name="configure-the-load-balancer-to-receive-traffic"></a>Konfigurera lastbalanseraren för att ta emot trafik

Nu konfigurerar Contosos administratörer en lastbalanseringsregel för att definiera hur trafiken ska distribueras till de virtuella datorerna.

- Klientdelens IP-adress hanterar inkommande trafik.
- Serverdelens IP-pool tar emot trafiken.

De skapar regeln enligt följande:

1. I lastbalanserarens inställningar i portalen lägger de till en ny lastbalanseringsregel: **SQLAlwaysOnEndPointListener**.
2. De anger en klientdelslyssnare för att ta emot inkommande SQL-klienttrafik på TCP 1433.
3. De anger serverdelspoolen som trafiken ska dirigeras till och porten som virtuella datorer lyssnar efter trafik på.
4. De aktiverar flytande IP (direkt serverreturnering). Det krävs alltid för SQL AlwaysOn.

    ![Avsökning](media/contoso-migration-rehost-vm-sql-ag/nlb-probe.png)

**Behöver du mer hjälp?**

- [Få en översikt](/azure/load-balancer/load-balancer-overview) över Azure Load Balancer.
- [Läs mer](/azure/load-balancer/tutorial-load-balancer-basic-internal-portal) om att skapa en lastbalanserare.

## <a name="step-4-prepare-azure-for-the-site-recovery-service"></a>Steg 4: Förbereda Azure för Site Recovery-tjänsten

Här är de Azure-komponenter som Contoso behöver för att distribuera Site Recovery:

- Ett virtuellt nätverk där virtuella datorer ska placeras när de skapas under redundansväxling.
- Ett Azure-lagringskonto för att lagra replikerade data.
- Ett Recovery Services-valv i Azure.

Contosos administratörer konfigurerar dessa så här:

1. Contoso har redan skapat ett nätverk/undernät som de kan använda för Site Recovery när de [distribuerade Azure-infrastrukturen](contoso-migration-rehost-vm-sql-ag.md).

    - SmartHotel360-appen är en produktionsapp och WEBVM migreras till Azure-produktionsnätverket (VNET-PROD-EUS2) i den primära regionen USA, östra 2.
    - WEBVM placeras i resursgruppen ContosoRG, som används för produktionsresurser, och i produktionsundernätet (PROD-FE-EUS2).

2. Contosos administratörer skapar ett Azure-lagringskonto (contosovmsacc20180528) i den primära regionen.

    - De använder ett konto för generell användning, med standardlagring och LRS-replikering.
    - Kontot måste finnas i samma region som valvet.

      ![Site Recovery-lagring](media/contoso-migration-rehost-vm-sql-ag/asr-storage.png)

3. Med nätverket och lagringskontot på plats skapar de nu ett Recovery Services-valv (**ContosoMigrationVault**) och placerar det i resursgruppen **ContosoFailoverRG**, i den primära regionen USA, östra 2.

    ![Recovery Services-valv](media/contoso-migration-rehost-vm-sql-ag/asr-vault.png)

**Behöver du mer hjälp?**

[Lär dig](/azure/site-recovery/tutorial-prepare-azure) hur du konfigurerar Azure för Site Recovery.

## <a name="step-5-prepare-on-premises-vmware-for-site-recovery"></a>Steg 5: Förbereda lokala VMware för Site Recovery

Det här är vad Contosos administratörer förbereder lokalt:

- Ett konto på vCenter-servern eller vSphere ESXi-värden, för att automatisera VM-identifiering.
- Ett konto som tillåter automatisk installation av mobilitetstjänsten på virtuella VMware-datorer som ska replikeras.
- Lokala VM-inställningar, så att Contoso kan ansluta till den replikerade virtuella Azure-datorn efter redundansväxling.

### <a name="prepare-an-account-for-automatic-discovery"></a>Förbereda ett konto för automatisk identifiering

Site Recovery måste ha åtkomst till VMware-servrarna för att:

- Identifiera automatiskt virtuella datorer.
- Samordna replikering, redundans och återställning efter fel.
- Minst ett skrivskyddat konto krävs. Du behöver ett konto som kan skapa och ta bort diskar, starta virtuella datorer och utföra liknande åtgärder.

Contosos administratörer konfigurerar kontot så här:

1. De skapar en roll på vCenter-nivå.
2. De tilldelar sedan rollen de behörigheter som krävs.

### <a name="prepare-an-account-for-mobility-service-installation"></a>Förbereda ett konto för installation av mobilitetstjänsten

Mobilitetstjänsten måste installeras på varje virtuell dator.

- Site Recovery kan utföra en automatisk push-installation av den här komponenten när replikering är aktiverat för den virtuella datorn.
- För push-installationen behöver du ett konto som Site Recovery kan använda för att komma åt den virtuella datorn. Du anger det här kontot när du konfigurerar replikering i Azure-konsolen.
- Kontot kan vara ett domänkonto eller ett lokalt konto, med behörighet att installera på den virtuella datorn.

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Förbereda för att ansluta till virtuella Azure-datorer efter en redundansväxling

Efter redundansväxlingen vill Contoso kunna ansluta till virtuella Azure-datorer. Contosos administratörer gör följande före migreringen för att göra detta:

1. För åtkomst via Internet gör de följande:

   - Aktivera RDP på den lokala virtuella datorn före redundansväxlingen
   - Se till att TCP- och UDP-regler läggs till för den **offentliga** profilen.
   - Kontrollera att RDP tillåts i **Windows-brandväggen** > **Tillåtna appar** för alla profiler.

2. För åtkomst via plats-till-plats-VPN gör de följande:

   - Aktivera RDP på den lokala datorn.
   - Tillåta RDP i **Windows-brandväggen** -> **Tillåtna appar och funktioner**, för nätverken **Domän och Privat**.
   - Ange operativsystemets SAN-princip på den lokala virtuella datorn till **OnlineAll**.

Dessutom måste de kontrollera följande när de kör en redundansväxling:

- Det får inte finnas några väntande Windows-uppdateringar på den virtuella datorn när de utlöser en redundansväxling. Om det finns det kan användarna inte logga in på den virtuella datorn förrän uppdateringen är klar.
- Efter redundansväxlingen kan de kontrollera **Startdiagnostik** för att visa en skärmbild av den virtuella datorn. Om detta inte fungerar bör de kontrollera att den virtuella datorn körs och gå igenom de här [felsökningstipsen](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

**Behöver du mer hjälp?**

- [Lär dig](/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-automatic-discovery) hur du skapar och tilldelar en roll för automatisk identifiering.
- [Lär dig](/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-mobility-service-installation) hur du skapar ett konto för push-installation av mobilitetstjänsten.

## <a name="step-6-replicate-the-on-premises-vms-to-azure-with-site-recovery"></a>Steg 6: Replikera de lokala virtuella datorerna till Azure med Site Recovery

Innan de kan köra en migrering till Azure måste Contosos administratörer konfigurera och aktivera replikering.

### <a name="set-a-replication-goal"></a>Ange ett replikeringsmål

1. I valvet, under valvnamnet (ContosoVMVault), väljer de ett replikeringsmål (**Komma igång** > **Site Recovery** > **Förbered infrastruktur**.
2. De anger att datorerna finns lokalt, körs på VMware och replikeras till Azure.

    ![Replikeringsmål](./media/contoso-migration-rehost-vm-sql-ag/replication-goal.png)

### <a name="confirm-deployment-planning"></a>Bekräfta distributionsplanering

För att fortsätta behöver de bekräfta att distributionsplaneringen är klar genom att välja **Ja, det har jag gjort**. I det här scenariot migrerar Contoso bara en virtuell dator och behöver ingen distributionsplanering.

### <a name="set-up-the-source-environment"></a>Konfigurera källmiljön

Contosos administratörer måste konfigurera källmiljön. För att göra det laddar de ned en OVF-mall och använder den för att distribuera Site Recovery-konfigurationsservern som en lokal virtuell VMware-dator med hög tillgänglighet. När konfigurationsservern är igång registrerar de den i valvet.

Konfigurationsservern kör flera komponenter:

- Konfigurationsserverkomponenten som samordnar kommunikationen mellan den lokala miljön och Azure och hanterar datareplikering.
- Processervern som fungerar som en replikeringsgateway. Den tar emot replikeringsdata, optimerar dem med cachelagring, komprimering och kryptering och skickar dem till Azure Storage.
- Processervern installerar också mobilitetstjänsten på de virtuella datorer du vill replikera, samt utför automatisk identifiering av lokala virtuella VMware-datorer.

Contosos administratörer utför följande steg:

1. I valvet laddar de ned OVF-mallen från **Förbered infrastruktur** > **Källa** > **Konfigurationsserver**.

    ![Ladda ned OVF](./media/contoso-migration-rehost-vm-sql-ag/add-cs.png)

2. De importerar mallen till VMware för att skapa och distribuera den virtuella datorn.

    ![OVF-mall](./media/contoso-migration-rehost-vm-sql-ag/vcenter-wizard.png)

3. När de aktiverar den virtuella datorn för första gången startar den i en installationsmiljö för Windows Server 2016. De godkänner licensavtalet och anger ett administratörslösenord.
4. När installationen är klar loggar de in på den virtuella datorn som administratörer. Vid första inloggningen körs Azure Site Recovery-konfigurationsverktyget som standard.
5. I verktyget anger de ett namn som ska användas för att registrera konfigurationsservern i valvet.
6. Verktyget kontrollerar att den virtuella datorn kan ansluta till Azure. När anslutningen har upprättats loggar de in i Azure-prenumerationen. Autentiseringsuppgifterna måste ha åtkomst till det valv där du vill registrera konfigurationsservern.

    ![Registrera konfigurationsservern](./media/contoso-migration-rehost-vm-sql-ag/config-server-register2.png)

7. Verktyget utför vissa konfigurationsåtgärder och startar sedan om datorn.
8. De loggar in på datorn igen och guiden Konfigurera serverhantering startar automatiskt.
9. I guiden väljer de det nätverkskort som ska ta emot replikeringstrafik. Det går inte att ändra den här inställningen när den har konfigurerats.
10. De väljer den prenumeration, den resursgrupp och det valv som konfigurationsservern ska registreras i.
        ![Valv](./media/contoso-migration-rehost-vm-sql-ag/cswiz1.png)

11. De laddar sedan ned och installerar MySQL Server och VMware PowerCLI.
12. Efter verifieringen anger de FQDN eller IP-adressen för vCenter-servern eller vSphere-värden. De lämnar standardporten och anger ett användarvänligt namn för vCenter-servern.
13. De anger det konto som de har skapat för automatisk identifiering och de autentiseringsuppgifter som används för att installera mobilitetstjänsten automatiskt. I Windows-datorer måste kontot ha lokal administratörsbehörighet på de virtuella datorerna.

    ![vCenter](./media/contoso-migration-rehost-vm-sql-ag/cswiz2.png)

14. När registreringen är klar kontrollerar de i Azure-portalen att konfigurationsservern och VMware-servern visas på sidan **Källa** i valvet. Identifieringen kan ta 15 minuter eller mer.
15. Site Recovery ansluter sedan till VMware-servrar med hjälp av de angivna inställningarna och identifierar virtuella datorer.

### <a name="set-up-the-target"></a>Konfigurera målet

Nu anger Contosos administratörer inställningar för målreplikeringen.

1. De klickar på **Förbered infrastruktur** > **Mål** och väljer målinställningarna.
2. Site Recovery kontrollerar att det finns ett Azure-lagringskonto och nätverk på det angivna målet.

### <a name="create-a-replication-policy"></a>Skapa replikeringsprincip

Nu kan Contosos administratörer skapa en replikeringsprincip.

1. I **Förbered infrastruktur** > **Replikeringsinställningar** > **Replikeringsprincip** >  **Skapa och associera** skapar de principen **ContosoMigrationPolicy**.
2. De använder standardinställningarna:
    - **Tröskelvärde för mål för återställningspunkt:** Standardvärdet är 60 minuter. Det här värdet anger hur ofta återställningspunkter skapas. En avisering genereras när den kontinuerliga replikeringen överskrider den här gränsen.
    - **Kvarhållning av återställningspunkt:** Standardvärdet är 24 timmar. Det här värdet anger kvarhållningsperioden för varje återställningspunkt. Replikerade virtuella datorer kan återställas till valfri punkt i ett fönster.
    - **Appkonsekvent ögonblicksbildsfrekvens:** Standardvärdet är en timme. Det här värdet anger med vilken frekvens programkonsekventa ögonblicksbilder skapas.

        ![Skapa replikeringsprincip](./media/contoso-migration-rehost-vm-sql-ag/replication-policy.png)

3. Principen associeras automatiskt med konfigurationsservern.

    ![Associera replikeringsprincipen](./media/contoso-migration-rehost-vm-sql-ag/replication-policy2.png)

### <a name="enable-replication"></a>Aktivera replikering

Contosos administratörer kan nu börja replikera WebVM.

1. I **Replikera program** > **Källa** >  **+Replikera** väljer de källinställningarna.
2. De anger att de vill aktivera virtuella datorer, väljer vCenter-servern och konfigurationsservern.

    ![Aktivera replikering](./media/contoso-migration-rehost-vm-sql-ag/enable-replication1.png)

3. Nu anger de målinställningarna, inklusive resursgruppen och det virtuella nätverket, samt det lagringskonto där replikerade data ska lagras.

     ![Aktivera replikering](./media/contoso-migration-rehost-vm-sql-ag/enable-replication2.png)

4. De väljer WebVM för replikering, kontrollerar replikeringsprincipen och aktiverar replikering. Site Recovery installerar mobilitetstjänsten på den virtuella datorn när replikering är aktiverad.

    ![Aktivera replikering](./media/contoso-migration-rehost-vm-sql-ag/enable-replication3.png)

5. De spårar replikeringsförloppet i **Jobb**. När jobbet **Slutför skydd** har körts är datorn redo för redundans.
6. De kan se strukturen för de virtuella datorer som replikerar till Azure i **Information** i Azure-portalen.

    ![Infrastrukturvy](./media/contoso-migration-rehost-vm-sql-ag/essentials.png)

**Behöver du mer hjälp?**

- En fullständig genomgång av de här stegen finns i [Konfigurera haveriberedskap för lokala virtuella VMware-datorer](/azure/site-recovery/vmware-azure-tutorial).
- Detaljerade instruktioner finns tillgängliga som hjälper dig att [konfigurera källmiljön](/azure/site-recovery/vmware-azure-set-up-source), [distribuera konfigurationsservern](/azure/site-recovery/vmware-azure-deploy-configuration-server) och [konfigurera replikeringsinställningar](/azure/site-recovery/vmware-azure-set-up-replication).
- Du kan läsa mer om hur du [aktiverar replikering](/azure/site-recovery/vmware-azure-enable-replication).

## <a name="step-7-install-the-data-migration-assistant-dma"></a>Steg 7: Installera Data Migration Assistant (DMA)

Contosos administratörer migrerar SmartHotel360-databasen till den virtuella Azure-datorn **SQLAOG1** med hjälp av DMA. De konfigurerar DMA på följande sätt:

1. De laddar ned verktyget från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595) till den lokala, virtuella SQL Server-datorn (**SQLVM**).
2. De kör installationsprogrammet (DownloadMigrationAssistant.msi) på den virtuella datorn.
3. På sidan **Slutför** väljer de **Starta Microsoft Data Migration Assistant** innan de avslutar guiden.

## <a name="step-8-migrate-the-database-with-dma"></a>Steg 8: Migrera databasen med DMA

1. De kör en ny migrering i DMA, **SmartHotel**.
2. De väljer **Målservertyp** som **SQL Server på Azure Virtual Machines**.

    ![DMA](media/contoso-migration-rehost-vm-sql-ag/dma-1.png)

3. I informationen om migreringen lägger de till **SQLVM** som källserver och **SQLAOG1** som mål. De anger autentiseringsuppgifter för varje dator.

     ![DMA](media/contoso-migration-rehost-vm-sql-ag/dma-2.png)

4. De skapar en lokal resurs för databas- och konfigurationsinformationen. Den måste vara tillgänglig med skrivåtkomst för SQL-tjänstkontot på SQLVM och SQLAOG1.

    ![DMA](media/contoso-migration-rehost-vm-sql-ag/dma-3.png)

5. Contoso väljer de inloggningar som ska migreras och påbörjar migreringen. När den har slutförts visar DMA migreringen som lyckad.

    ![DMA](media/contoso-migration-rehost-vm-sql-ag/dma-4.png)

6. De kontrollerar att databasen körs på **SQLAOG1**.

    ![DMA](media/contoso-migration-rehost-vm-sql-ag/dma-5.png)

DMA ansluter till den lokala SQL Server VM över en VPN-anslutning från plats till plats mellan Contosos datacenter och Azure, och migrerar sedan databasen.

## <a name="step-7-protect-the-database-with-always-on"></a>Steg 7: Skydda databasen med AlwaysOn

När appdatabasen körs på **SQLAOG1** kan Contosos administratörer nu skydda den med hjälp av AlwaysOn-tillgänglighetsgrupper. De konfigurerar AlwaysOn med hjälp av SQL Management Studio och tilldelar sedan en lyssnare med hjälp av Windows-klustring.

### <a name="create-an-always-on-availability-group"></a>Skapa en AlwaysOn-tillgänglighetsgrupp

1. I SQL Management Studio högerklickar de på **Alltid på Hög tillgänglighet** för att starta **guiden Ny tillgänglighetsgrupp**.
2. I **Ange alternativ** ger de tillgänglighetsgruppen namnet **SHAOG**. I **Välj databaser** väljer de SmartHotel360-databasen.

    ![Always On-tillgänglighetsgrupp](media/contoso-migration-rehost-vm-sql-ag/aog-1.png)

3. I **Ange repliker** lägger de till de två SQL-noderna som tillgänglighetsrepliker och konfigurerar dem att tillhandahålla automatisk redundans med synkront genomförande.

     ![Always On-tillgänglighetsgrupp](media/contoso-migration-rehost-vm-sql-ag/aog-2.png)

4. De konfigurerar en lyssnare för gruppen (**SHAOG**) och porten. IP-adressen för den interna lastbalanseraren läggs till som en statisk IP-adress (10.245.40.100).

    ![Always On-tillgänglighetsgrupp](media/contoso-migration-rehost-vm-sql-ag/aog-3.png)

5. I **Välj datasynkronisering** aktiverar de automatisk seeding. Med det här alternativet skapar SQL Server automatiskt de sekundära replikerna för varje databas i gruppen, så Contoso behöver inte säkerhetskopiera och återställa dem manuellt. Efter valideringen skapas tillgänglighetsgruppen.

    ![Always On-tillgänglighetsgrupp](media/contoso-migration-rehost-vm-sql-ag/aog-4.png)

6. Contoso stötte på ett problem när gruppen skapades. De använder inte integrerad Windows-säkerhet i Active Directory, och måste därför bevilja behörighet till SQL-inloggningen för att skapa Windows-redundansklusterrollerna.

    ![Always On-tillgänglighetsgrupp](media/contoso-migration-rehost-vm-sql-ag/aog-5.png)

7. När gruppen har skapats kan Contoso se den i SQL Management Studio.

### <a name="configure-a-listener-on-the-cluster"></a>Konfigurera en lyssnare på klustret

Som ett sista steg i konfigurationen av SQL-distributionen konfigurerar Contosos administratörer den interna lastbalanseraren som lyssnare på klustret och tar lyssnaren online. De använder ett skript för att göra det.

![Klusterlyssnare](media/contoso-migration-rehost-vm-sql-ag/cluster-listener.png)

### <a name="verify-the-configuration"></a>Kontrollera att konfigurationen

När allt är konfigurerat har Contoso nu en fungerande tillgänglighetsgrupp i Azure som använder den migrerade databasen. Administratörer kontrollerar detta genom att ansluta till den interna lastbalanseraren i SQL Management Studio.

![ILB-anslutning](media/contoso-migration-rehost-vm-sql-ag/ilb-connect.png)

**Behöver du mer hjälp?**

- Läs mer om att skapa en [tillgänglighetsgrupp](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial#create-the-availability-group) och [lyssnare](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial#configure-listener).
- [Konfigurera manuellt klustret att använda lastbalanserarens IP-adress](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener#configure-the-cluster-to-use-the-load-balancer-ip-address).
- [Läs mer](/azure/storage/blobs/storage-dotnet-shared-access-signature-part-2) om att skapa och använda SAS.

## <a name="step-8-migrate-the-vm-with-site-recovery"></a>Steg 8: Migrera den virtuella datorn med Site Recovery

Contosos administratörer kör en snabb testning av redundansen och migrerar sedan den virtuella datorn.

### <a name="run-a-test-failover"></a>Köra ett redundanstest

Genom att köra ett redundanstest kan de vara säkra på att allt fungerar som förväntat innan de genomför migreringen.

1. De kör ett redundanstest till den senaste tillgängliga tidpunkten (**Senast bearbetad**).
2. De väljer **Stäng datorn innan du påbörjar redundans**, så att Site Recovery försöker stänga av den virtuella källdatorn innan redundansväxlingen utlöses. Redundansväxlingen fortsätter även om avstängningen misslyckas.
3. Redundanstest:

    - En kravkontroll körs för att säkerställa att alla villkor som krävs för migreringen är uppfyllda.
    - Redundansprocessen bearbetar data så att du kan skapa en virtuell Azure-dator. Om du väljer den senaste återställningspunkten skapas en återställningspunkt utifrån tillgängliga data.
    - En virtuell Azure-dator skapas med hjälp av de data som behandlas i föregående steg.

4. När redundansväxlingen är klar visas repliken av den virtuella Azure-datorn på Azure-portalen. De kontrollerar att den virtuella datorn har rätt storlek, att den är ansluten till rätt nätverk och att den körs.
5. Efter verifieringen rensar de redundansväxlingen och registrerar och sparar eventuella observationer.

### <a name="run-a-failover"></a>Köra en redundansväxling

1. När de har verifierat att redundanstestningen fungerade som förväntat skapar Contosos administratörer en återställningsplan för migreringen och lägger till WEBVM i planen.

     ![Återställningsplan](./media/contoso-migration-rehost-vm-sql-ag/recovery-plan.png)

2. De kör en redundansväxling mot planen. De väljer den senaste återställningspunkten och anger att Site Recovery ska försöka stänga av den lokala virtuella datorn innan redundansväxlingen utlöses.

    ![Redundans](./media/contoso-migration-rehost-vm-sql-ag/failover1.png)

3. Efter redundansväxlingen kontrollerar de att den virtuella Azure-datorn visas som förväntat på Azure-portalen.

    ![Återställningsplan](./media/contoso-migration-rehost-vm-sql-ag/failover2.png)

4. När verifieringen av den virtuella datorn i Azure är klar slutför de migreringen för att avsluta migreringsprocessen, samt stoppa replikeringen och Site Recovery-faktureringen för den virtuella datorn.

    ![Redundans](./media/contoso-migration-rehost-vm-sql-ag/failover3.png)

### <a name="update-the-connection-string"></a>Uppdatera anslutningssträngen

Som sista steg i migreringsprocessen uppdaterar Contosos administratörer programmets anslutningssträng så att den pekar på den migrerade databasen som körs på SHAOG-lyssnaren. Den här konfigurationen ändras på WEBVM som nu körs i Azure. Den här konfigurationen finns i web.config för ASP-programmet.

1. Du hittar filen i C:\inetpub\SmartHotelWeb\web.config. Ändra namnet på servern enligt FQDN för AOG: shaog.contoso.com.

    ![Redundans](./media/contoso-migration-rehost-vm-sql-ag/failover4.png)

2. När de har uppdaterat filen och sparat den, startar de om IIS på WEBVM. Det gör de med IISRESET /RESTART från en	kommandotolk.
3. När IIS har startats om använder programmet nu databasen som körs på SQL MI.

**Behöver du mer hjälp?**

- [Lär dig](/azure/site-recovery/tutorial-dr-drill-azure) hur du kör ett redundanstest.
- [Lär dig](/azure/site-recovery/site-recovery-create-recovery-plans) hur du skapar en återställningsplan.
- [Lär dig](/azure/site-recovery/site-recovery-failover) hur du redundansväxlar till Azure.

## <a name="clean-up-after-migration"></a>Rensa efter migreringen

Efter migreringen körs SmartHotel360-appen på en virtuell Azure-dator och SmartHotel360-databasen finns i Azure SQL-klustret.

Nu måste Contoso utföra följande steg för rensning:

- Ta bort de lokala virtuella datorerna från vCenter-lagret.
- Ta bort de virtuella datorerna från lokala säkerhetskopieringsjobb.
- Uppdatera den interna dokumentationen med de nya platserna och IP-adresserna för virtuella datorer.
- Granska alla resurser som interagerar med de inaktiverade virtuella datorerna och uppdatera alla relevanta inställningar eller dokumentation så att de överensstämmer med den nya konfigurationen.
- Lägga till de två nya virtuella datorerna (SQLAOG1 och SQLAOG2) i produktionsövervakningssystem.

## <a name="review-the-deployment"></a>Granska distributionen

Med de migrerade resurserna i Azure måste Contoso fullständigt operationalisera och skydda sin nya infrastruktur.

### <a name="security"></a>Säkerhet

Contosos säkerhetsteam granskar de virtuella Azure-datorerna WEBVM, SQLAOG1 och SQLAOG2 för att fastställa eventuella säkerhetsproblem.

- Teamet granskar nätverkssäkerhetsgrupperna (NSG:er) för den virtuella datorn för åtkomstkontroll. Nätverkssäkerhetsgrupper används för att säkerställa att endast trafik som tillåts för programmet kan passera.
- Teamet överväger att skydda data på disken med Azure Disk Encryption och Key Vault.
- Teamet bör utvärdera transparent datakryptering (TDE) och sedan aktivera det på SmartHotel360-databasen som körs på den nya SQL-AOG. [Läs mer](/sql/relational-databases/security/encryption/transparent-data-encryption?view=sql-server-2017).

[Läs mer](/azure/security/azure-security-best-practices-vms) om säkerhetsrutiner för virtuella datorer.

## <a name="bcdr"></a>BCDR

 För affärskontinuitet och haveriberedskap (BCDR) vidtar Contoso följande åtgärder:

- Skydda data: Contoso säkerhetskopierar data på de virtuella datorerna WEBVM, SQLAOG1 och SQLAOG2 med hjälp av Azure Backup-tjänsten. [Läs mer](/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
- Contoso får också lära sig hur de använder Azure Storage för att säkerhetskopiera SQL Server direkt till bloblagring. [Läs mer](/azure/virtual-machines/windows/sql/virtual-machines-windows-use-storage-sql-server-backup-restore).
- Undvika avbrott i apparna: Contoso replikerar appens virtuella datorer i Azure till en sekundär region med hjälp av Site Recovery. [Läs mer](/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Licensierings- och kostnadsoptimering

1. Contoso har befintlig licensiering för sin WEBVM och drar nytta av Azure Hybrid-förmånen. Contoso konverterar befintliga virtuella Azure-datorer för att dra nytta av denna prissättning.
2. Contoso aktiverar Azure Cost Management som licensieras av Cloudyn, ett Microsoft-dotterbolag. Det är en kostnadshanteringslösning med flera moln som hjälper dig att använda och hantera Azure och andra molnresurser. [Läs mer](/azure/cost-management/overview) om Azure Cost Management.

## <a name="conclusion"></a>Sammanfattning

I den här artikeln har Contoso angett en ny värd för SmartHotel360-appen i Azure genom att migrera appens virtuella klientdelsdator till Azure med hjälp av Site Recovery-tjänsten. Contoso har migrerat appdatabasen till ett SQL Server-kluster som etablerats i Azure och skyddat den i en SQL Server AlwaysOn-tillgänglighetsgrupp.
