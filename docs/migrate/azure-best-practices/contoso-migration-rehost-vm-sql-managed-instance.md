---
title: Ange en ny värd för en lokal app genom att migrera till virtuella Azure-datorer och Azure SQL Database Managed Instance
description: Lär dig hur Contoso anger en ny värd för en lokal app på virtuella Azure-datorer genom att använda Azure SQL Database Managed Instance.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 7ec95c75d81b93852a59ef137a02cc35d83a1cd3
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78223085"
---
# <a name="rehost-an-on-premises-app-on-an-azure-vm-and-sql-database-managed-instance"></a>Ange en ny värd för en lokal app på en virtuell Azure-dator och SQL Database Managed Instance

Den här artikeln visar hur det fiktiva företaget Contoso migrerar en klientdelsapp i Windows .NET på två nivåer som körs på virtuella VMware-datorer, till en virtuell Azure-dator med hjälp av tjänsten Azure Site Recovery. Den visar också hur Contoso migrerar appens databas till Azure SQL Database Managed Instance.

SmartHotel360-appen som används i det här exemplet tillhandahålls som öppen källkod. Om du vill använda den i ett eget test kan du ladda ned den från [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Affärsdrivande faktorer

Contosos IT-ledningsgrupp har arbetat tillsammans med företagets affärspartners för att förstå vad företaget vill uppnå med migreringen:

- **Hantera företagets tillväxt.** Contoso växer. Det innebär att trycket har ökat på företagets lokala system och infrastruktur.
- **Öka effektiviteten.** Contoso måste ta bort onödiga procedurer och effektivisera processer för utvecklare och användare. Företaget kräver att IT-systemen är snabba och inte slösar tid eller pengar, så att företaget kan agera snabbare på kundernas önskemål.
- **Öka flexibiliteten.** Contosos IT-avdelning måste reagera snabbare på företagets behov. Det måste reagera snabbare än de ändringar som uppstår på marknaden för att företaget ska kunna lyckas i en global ekonomi. IT-verksamheten på Contoso får inte stå i vägen eller förhindra verksamhetens utveckling.
- **Skala.** När företagets verksamhet växer måste Contosos IT-avdelning förse företaget med system som kan växa i samma takt.

## <a name="migration-goals"></a>Migreringsmål

Contosos molnteam har identifierat mål för den här migreringen. Företaget använder migreringsmålen till att fastställa den bästa migreringsmetoden.

- Efter migreringen ska appen i Azure ha samma prestandafunktioner som appen har i dag i Contosos lokala VMware-miljö. Övergången till molnet innebär inte att appens prestanda är mindre viktig.
- Contoso vill inte investera i appen. Appen är kritisk och viktig för verksamheten, men Contoso vill bara flytta appen i sin aktuella form till molnet.
- Databasadministrationen bör minska betydligt när appen har migrerats.
- Contoso vill inte använda en Azure SQL Database för den här appen. Man letar efter alternativ.

## <a name="solution-design"></a>Lösningsdesign

När man har fastställt målen och kraven utformar och granskar Contoso en distributionslösning och identifierar migreringsprocessen, inklusive de Azure-tjänster som ska användas vid migreringen.

### <a name="current-architecture"></a>Nuvarande arkitektur

- Contoso har ett huvuddatacenter (**contoso-datacenter**). Datacentret finns i New York i östra USA.
- Contoso har ytterligare tre lokala avdelningar i USA.
- Huvuddatacentret är anslutet till Internet med en Metro Ethernet-anslutning för fiber (500 Mbit/s).
- Varje avdelning ansluts lokalt till Internet med hjälp av anslutningar i företagsklass med IPsec VPN-tunnlar tillbaka till huvuddatacentret. Konfigurationen innebär att Contosos hela nätverk är permanent anslutet och optimerar Internet-anslutningen.
- Huvuddatacentret är helt virtualiserat med VMware. Contoso har två ESXi 6.5-virtualiseringsvärdar som hanteras av vCenter Server 6.5.
- Contoso använder Active Directory Domain Services för identitetshantering. Contoso använder DNS-servrar i det interna nätverket.
- Contoso har en lokal domänkontrollant (**contosodc1**).
- Domänkontrollanterna körs på virtuella VMware-datorer. Domänkontrollanterna på de lokala avdelningarna körs på fysiska servrar.
- SmartHotel360-appen är nivåindelad över två virtuella datorer (**WEBVM** och **SQLVM**) och finns på VMware ESXi-värden version 6.5 (**contosohost1.contoso.com**).
- VMware-miljön hanteras av vCenter Server 6.5 (**vcenter.contoso.com**) som körs på en virtuell dator.

![Nuvarande Contoso-arkitektur](./media/contoso-migration-rehost-vm-sql-managed-instance/contoso-architecture.png)

### <a name="proposed-architecture"></a>Föreslagen arkitektur

I det här scenariot vill Contoso migrera sin lokala reseapp i två nivåer enligt följande:

- Migrera appens databas (**SmartHotelDB**) till en Azure SQL Database Managed Instance.
- Migrera klientdelens **WebVM** till en virtuell Azure-dator.
- Lokala virtuella datorer i Contosos datacenter kommer att inaktiveras när migreringen är slutförd.

![Scenariots arkitektur](media/contoso-migration-rehost-vm-sql-managed-instance/architecture.png)

### <a name="database-considerations"></a>Databasöverväganden

Som en del av processen för lösningsdesign gjorde Contoso en funktionsjämförelse mellan Azure SQL Database och SQL Server Managed Instance. Nedanstående överväganden hjälpte dem att välja Managed Instance.

- Managed Instance strävar efter att i princip leverera 100 % kompatibilitet med den senaste lokala SQL Server-versionen. Microsoft rekommenderar Managed Instance för kunder som kör SQL Server lokalt eller på virtuella IaaS-datorer som vill migrera sina appar till en fullständigt hanterad tjänst med minimala designändringar.
- Contoso planerar att migrera ett stort antal appar från en lokal plats till IaaS. Många av dessa kommer från oberoende programvaruleverantörer. Contoso inser att användningen av Managed Instance bidrar till att säkerställa databasens kompatibilitet för dessa appar, i stället för att använda SQL Database som kanske inte stöds.
- Contoso kan helt enkelt utföra en hiss och flytta migreringen till en hanterad instans med hjälp av den helt automatiserade Azure Database Migration Service. Med den här tjänsten kan Contoso återanvända den vid framtida databasmigreringar.
- SQL Managed Instance har stöd för SQL Server Agent, vilket är viktigt för SmartHotel360-appen. Contoso behöver denna kompatibilitet, annars måste de göra en ny design av underhållsplanerna som krävs av appen.
- Med Software Assurance kan Contoso byta ut befintliga licenser till rabatterade priser för en SQL Database Managed Instance med hjälp av Azure Hybrid-förmånen för SQL Server. Detta kan innebära att Contoso sparar upp till 30 % på Managed Instance.
- SQL-hanterad instans finns helt i det virtuella nätverket, så den ger bättre isolering och säkerhet för Contosos data. Contoso får fördelarna med det offentliga molnet, samtidigt som miljön hålls isolerad från offentligt Internet.
- Managed Instance stöder många säkerhetsfunktioner, inklusive Always Encrypted, dynamisk datamaskering, säkerhet på radnivå och hotidentifiering.

### <a name="solution-review"></a>Lösningsgranskning

Contoso utvärderar den föreslagna designen genom att skapa en lista med för- och nackdelar.

<!-- markdownlint-disable MD033 -->

**Övervägande** | **Detaljer**
--- | ---
**Fördelar** | WEBVM kommer att flyttas till Azure utan ändringar, vilket gör migreringen enkel.<br/><br/> SQL Managed Instance har stöd för Contosos tekniska krav och mål.<br/><br/> Managed Instance ger 100 % kompatibilitet med den nuvarande distributionen, samtidigt som de kan lämna SQL Server 2008 R2.<br/><br/> De kan dra nytta av sin investering i Software Assurance och använda Azure Hybrid-förmånen för SQL Server och Windows Server.<br/><br/> De kan återanvända Azure Database Migration Service vid ytterligare framtida migreringar.<br/><br/> SQL Managed Instance har inbyggd feltolerans som Contoso inte behöver konfigurera. Detta säkerställer att datanivån inte längre är en felkritisk systemdel.
**Nackdelar** | WEBVM kör Windows Server 2008 R2. Även om det här operativsystemet stöds av Azure, stöds plattformen inte längre. [Läs mer](https://support.microsoft.com/help/956893).<br/><br/> Webbnivån förblir en felkritisk systemdel när endast WEBVM tillhandahåller tjänsterna.<br/><br/> Contoso måste fortsätta stödja appens webbnivå som en virtuell dator i stället för att flytta till en hanterad tjänst, till exempel Azure App Service.<br/><br/> För datanivån kanske Managed Instance inte är den bästa lösningen om Contoso vill anpassa operativsystemet eller databasservern, eller om de vill köra appar från tredje part tillsammans med SQL Server. Att köra SQL Server på en virtuell IaaS-dator skulle kunna ge den här flexibiliteten.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Migreringsprocess

Contoso migrerar webb- och datanivåerna för sin SmartHotel360-app till Azure genom att utföra dessa steg:

1. Contoso har redan sin Azure-infrastruktur på plats, så de behöver bara lägga till ett par olika Azure-komponenter i det här scenariot.
2. Datanivån kommer att migreras med hjälp av Azure Database Migration Service. Den här tjänsten ansluter till den lokala SQL Server VM över en VPN-anslutning från plats till plats mellan Contosos datacenter och Azure. Tjänsten migrerar sedan databasen.
3. Webb nivån kommer att migreras med hjälp av en hiss och Shift-migrering med hjälp av Site Recovery. Processen innebär att förbereda den lokala VMware-miljön, konfigurera och aktivera replikering samt migrera de virtuella datorerna genom att redundansväxla dem till Azure.

     ![Migreringsarkitektur](media/contoso-migration-rehost-vm-sql-managed-instance/migration-architecture.png)

### <a name="azure-services"></a>Azure-tjänster

Tjänst | Beskrivning | Kostnad
--- | --- | ---
[Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Med Azure Database Migration Service kan du migrera sömlöst från flera databaskällor till Azure-dataplattformar med minsta möjliga stilleståndstid. | Lär dig mer om [regioner som stöds](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) och [Database Migration Service- prissättning](https://azure.microsoft.com/pricing/details/database-migration).
[Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) | Managed Instance är en hanterad databastjänst som representerar en fullständigt hanterad SQL Server-instans i Azure-molnet. Den använder samma kod som den senaste versionen av SQL Server Database Engine och innehåller de senaste funktionerna, prestandaförbättringar och säkerhetskorrigeringar. | Om du använder en SQL Database Managed Instance som körs i Azure, debiteras avgifter baserat på kapacitet. Läs mer om [prissättning av Managed Instance](https://azure.microsoft.com/pricing/details/sql-database/managed).
[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery) | Site Recovery-tjänsten dirigerar samt hanterar migrering och haveriberedskap för virtuella Azure-datorer, lokala virtuella datorer och fysiska servrar. | Under replikeringen till Azure debiteras Azure Storage-avgifter. Virtuella Azure-datorer skapas och debiteras när redundans sker. Läs mer om [debitering och prissättning för Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery).

## <a name="prerequisites"></a>Förutsättningar

Contoso och andra användare måste uppfylla följande krav för det här scenariot:

<!-- markdownlint-disable MD033 -->

Krav | Detaljer
--- | ---
**Azure-prenumeration** | Du bör redan ha skapat en prenumeration när du gjorde utvärderingen i den första artikeln i den här serien. Om du inte har någon Azure-prenumeration kan du skapa ett [kostnadsfritt konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Om du skapar ett kostnadsfritt konto är du administratör för din prenumeration och kan utföra alla åtgärder.<br/><br/> Om du använder en befintlig prenumeration och du inte är administratör av prenumerationen, måste du be administratören tilldela dig ägar- eller deltagarbehörighet.<br/><br/> Om du behöver mer detaljerad behörighet kan du läsa mer i [Använda rollbaserad åtkomstkontroll till att hantera Site Recovery-åtkomst](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Azure-infrastruktur** | Contoso konfigurerar Azure-infrastrukturen enligt beskrivningen i [Azure-infrastruktur för migrering.](./contoso-migration-infrastructure.md)
**Site Recovery (lokalt)** | Din lokala vCenter Server-instans måste köra version 5.5, 6.0 eller 6.5<br/><br/> En ESXi-värd som kör version 5.5, 6.0 eller 6.5<br/><br/> En eller flera virtuella VMware-datorer som körs på ESXi-värden.<br/><br/> De virtuella datorerna måste uppfylla [kraven för Azure](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#azure-vm-requirements).<br/><br/> Konfiguration av [nätverk](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#network) och [lagring](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#storage) som stöds.
**Database Migration Service** | För Azure Database Migration Service behöver du en [kompatibel lokal VPN-enhet](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices).<br/><br/> Du måste kunna konfigurera den lokala VPN-enheten. Den måste ha en extern offentlig IPv4-adress. IP-adressen får inte finnas bakom en NAT-enhet.<br/><br/> Kontrollera att du har åtkomst till din lokala SQL Server-databas.<br/><br/> Windows-brandväggen måste ha åtkomst till källdatabasmotorn. Läs om att [konfigurera Windows-brandväggen för databasmotoråtkomst](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).<br/><br/> Om det finns en brandvägg framför din databasdator lägger du till regler som tillåter åtkomst till databasen och filerna via SMB-port 445.<br/><br/> De autentiseringsuppgifter som används för att ansluta till källans SQL Server-instans och som Managed Instance riktar sig mot måste vara medlemmar i serverrollen sysadmin.<br/><br/> Du behöver en nätverksresurs i din lokala databas som Azure Database Migration Service kan använda när källdatabasen säkerhetskopieras.<br/><br/> Kontrollera att tjänstkontot som kör SQL Server-källinstansen har skrivbehörighet till nätverksresursen.<br/><br/> Skriv ned en Windows-användare och ett lösenord som har fullständig kontrollbehörighet till nätverksresursen. Azure Database Migration Service personifierar användarens autentiseringsuppgifter till att ladda upp de säkerhetskopierade filerna till Azure Storage-containern.<br/><br/> Installationsprocessen för SQL Server Express anger TCP/IP-protokollet som **Inaktiverat** som standard. Kontrollera att det är aktiverat.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Steg i scenariot

Så här planerar Contoso att konfigurera distributionen:

> [!div class="checklist"]
>
> - **Steg 1: Konfigurera en SQL Database Hanterad instans.** Contoso behöver en befintlig hanterad instans som den lokala SQL Server-databasen ska migreras till.
> - **Steg 2: Förbered Azure Database Migration Service.** Contoso måste registrera migreringsprovidern för databasen, skapa en instans och sedan skapa ett Azure Database Migration Service-projekt. Contoso måste också konfigurera en signatur för delad åtkomst (SAS) med URI:n (Uniform Resource Identifier) för Azure Database Migration Service. En SAS-URI ger delegerad åtkomst till resurser på Contosos lagringskonto, vilket innebär att Contoso kan bevilja begränsade behörigheter till lagringsobjekt. Contoso konfigurerar en SAS-URI, så att Azure Database Migration Service får åtkomst till lagringskontots container som tjänsten laddar upp SQL Server-säkerhetskopiorna till.
> - **Steg 3: Förbered Azure för Site Recovery.** Contoso måste skapa ett lagringskonto där replikerade data för Site Recovery ska lagras. De måste också skapa ett Azure Recovery Services-valv.
> - **Steg 4: Förbered lokala VMware för Site Recovery.** Contoso förbereder konton för VM-identifiering och agentinstallation för att ansluta till virtuella Azure-datorer efter en redundans.
> - **Steg 5: replikera virtuella datorer.** Contoso konfigurerar replikeringen genom att konfigurera Site Recoverys käll- och målmiljö, konfigurera en replikeringsprincip och börja replikera virtuella datorer till Azure Storage.
> - **Steg 6: Migrera databasen med hjälp av Azure Database Migration Service.** Contoso migrerar databasen.
> - **Steg 7: migrera de virtuella datorerna med hjälp av Site Recovery.** Contoso kör ett redundanstest för att kontrollera att allt fungerar. Contoso kör sedan en fullständig redundans för att migrera de virtuella datorerna till Azure.

## <a name="step-1-prepare-a-sql-database-managed-instance"></a>Steg 1: Förbered en SQL Database Hanterad instans

För att kunna konfigurera en Azure SQL Database Managed Instance måste Contoso ha ett undernät som uppfyller följande krav:

- Undernätet måste vara dedikerat. Det måste vara tomt och får inte innehålla någon annan molntjänst. Undernätet får inte vara ett gatewayundernät.
- När den hanterade instansen har skapats, får Contoso inte lägga till resurser i undernätet.
- Undernätet får inte ha någon associerad nätverkssäkerhetsgrupp.
- Undernätet måste ha en användardefinierad routningstabell. Den enda tilldelade vägen ska vara 0.0.0.0/0 som nästa hopp till Internet.
- Valfri anpassad DNS: om anpassad DNS anges i det virtuella Azure-nätverket måste Azures IP-adress för rekursiva matchare (till exempel 168.63.129.16) läggas till i listan. Lär dig att [konfigurera anpassad DNS för en hanterad instans](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-custom-dns).
- Undernätet får inte ha någon associerad tjänstslutpunkt (lagring eller SQL). Tjänstens slutpunkter ska vara inaktiverade i det virtuella nätverket.
- Undernätet måste ha minst 16 IP-adresser. Lär dig att [ändra storlek på undernätet för den hanterade instansen](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-vnet-configuration).
- I Contosos hybridmiljö krävs anpassade DNS-inställningar. Contoso konfigurerar DNS-inställningarna till att använda en eller flera av företagets Azure DNS-servrar. Läs mer om [DNS-anpassning](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-custom-dns).

### <a name="set-up-a-virtual-network-for-the-managed-instance"></a>Konfigurera ett virtuellt nätverk för den hanterade instansen

Contosos administratörer konfigurerar det virtuella nätverket på följande sätt:

1. De skapar ett nytt virtuellt nätverk (**VNET-SQLMI-EU2**) i den primära regionen USA, östra 2. De lägger till det virtuella nätverket i resursgruppen **ContosoNetworkingRG**.
2. De tilldelar adressutrymmet 10.235.0.0/24. De säkerställer att intervallet inte överlappar andra nätverk i företaget.
3. De lägger till två undernät i nätverket:
    - **SQLMI-DS-EUS2** (10.235.0.0.25)
    - **SQLMI-SAW-EUS2** (10.235.0.128/29). Det här undernätet används för att koppla en katalog till den hanterade instansen.

      ![Managed Instance – Skapa ett virtuellt nätverk](media/contoso-migration-rehost-vm-sql-managed-instance/mi-vnet.png)

4. När det virtuella nätverket och undernäten har distribuerats utför de peering för nätverken enligt följande:

    - Peering av **VNET-SQLMI-EUS2** med **VNET-HUB-EUS2** (hubbens virtuella nätverk för USA, östra 2).
    - Peering av **VNET-SQLMI-EUS2** med **VNET-PROD-EUS2** (produktionsnätverket).

      ![Nätverkspeering](media/contoso-migration-rehost-vm-sql-managed-instance/mi-peering.png)

5. De anger anpassade DNS-inställningar. DNS:en pekar först på Contosos Azure-domänkontrollanter. Azure DNS är sekundär. Contosos Azure-domänkontrollanter finns på följande platser:

    - Finns i undernätet **PROD-DC-EUS2** i produktionsnätverket USA, östra 2 (**VNET-PROD-EUS2**)
    - **CONTOSODC3** -adress: 10.245.42.4
    - **CONTOSODC4** -adress: 10.245.42.5
    - Azure DNS-lösare: 168.63.129.16

      ![Nätverkets DNS-servrar](media/contoso-migration-rehost-vm-sql-managed-instance/mi-dns.png)

**Behöver du mer hjälp?**

- Få en översikt över [SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).
- Lär dig att [skapa ett virtuellt nätverk för en SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-vnet-configuration).
- Lär dig att [konfigurera peering](https://docs.microsoft.com/azure/virtual-network/virtual-network-manage-peering).
- Lär dig att [uppdatera Azure Active Directorys DNS-inställningar](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-getting-started-dns).

### <a name="set-up-routing"></a>Konfigurera routning

Den hanterade instansen placeras i ett privat virtuellt nätverk. Contoso behöver en routningstabell till det virtuella nätverket för att kunna kommunicera med Azure-hanteringstjänsten. Om det virtuella nätverket inte kan kommunicera med den tjänst som hanterar det, går det virtuella nätverket inte att nå.

Contoso överväger följande faktorer:

- Routningstabellen innehåller en uppsättning regler (vägar) som anger hur paket som skickas från den hanterade instansen ska dirigeras i det virtuella nätverket.
- Routningstabellen är kopplad till undernät där hanterade instanser distribueras. Hanteringen av de paket som lämnar ett undernät baseras på den tillhörande routningstabellen.
- Ett undernät kan bara associeras med en routningstabell.
- Det finns inga ytterligare avgifter för att skapa routningstabeller i Microsoft Azure.

 Contosos administratörer gör följande för att konfigurera routningen:

1. De skapar en användardefinierad routningstabell i resursgruppen **ContosoNetworkingRG**.

    ![Routningstabell](media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table.png)

2. För att uppfylla kraven i Managed Instance lägger de till en väg med adressprefixet 0.0.0.0/0 efter att routningstabellen (**MIRouteTable**) har distribuerats. Alternativet **Nästa hopptyp** är inställt på **Internet**.

    ![Prefix för routningstabell](media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-prefix.png)

3. De kopplar routningstabellen till undernätet **SQLMI-DB-EUS2** (i nätverket **VNET-SQLMI-EUS2**).

    ![Undernät för routningstabell](media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-subnet.png)

**Behöver du mer hjälp?**

Lär dig att [konfigurera vägar för en hanterad instans](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-create-tutorial-portal).

### <a name="create-a-managed-instance"></a>Skapa en hanterad instans

Nu kan Contosos administratörer etablera en SQL Database Managed Instance:

1. Eftersom Managed Instance används till en företagsapp, distribuerar de den hanterade instansen i företagets primära region för USA, östra 2. De lägger till den hanterade instansen i resursgruppen **ContosoRG**.
2. De väljer en prisnivå, storleksberäkning och lagring för instansen. Läs mer om [prissättning av Managed Instance](https://azure.microsoft.com/pricing/details/sql-database/managed).

    ![Managed Instance](media/contoso-migration-rehost-vm-sql-managed-instance/mi-create.png)

3. När den hanterade instansen har distribuerats, visas två nya resurser i resursgruppen **ContosoRG**:

    - Ett virtuellt kluster om Contoso har flera hanterade instanser.
    - SQL Server Database Managed Instance.

      ![Managed Instance](media/contoso-migration-rehost-vm-sql-managed-instance/mi-resources.png)

**Behöver du mer hjälp?**

Lär dig att [etablera en hanterad instans](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-create-tutorial-portal).

## <a name="step-2-prepare-the-azure-database-migration-service"></a>Steg 2: Förbered Azure Database Migration Service

Contosos administratörer behöver göra några fler saker för att förbereda Azure Database Migration Service:

- Registrera Azure Database Migration Service-providern i Azure.
- Ange Azure Database Migration Service med åtkomst till Azure Storage för att ladda upp de säkerhetskopierade filer som används när en databas migreras. De skapar en Azure Blob Storage-container för att få åtkomst till Azure Storage. De genererar en SAS-URI för Blob Storage-containern.
- Skapa ett Azure Database Migration Service-projekt.

Sedan utför de följande steg:

1. De registrerar providern för databasmigrering under prenumerationen.
    ![Database Migration Service – Registrera](media/contoso-migration-rehost-vm-sql-managed-instance/dms-subscription.png)

2. De skapar en Blob Storage-container. Contoso genererar en SAS-URI så att Azure Database Migration Service kan komma åt den.

    ![Database Migration Service – Generera en SAS-URI](media/contoso-migration-rehost-vm-sql-managed-instance/dms-sas.png)

3. De skapar en Azure Database Migration Service-instans.

    ![Database Migration Service – Skapa en instans](media/contoso-migration-rehost-vm-sql-managed-instance/dms-instance.png)

4. De placerar Azure Database Migration Service-instansen i undernätet **PROD-DC-EUS2** i det virtuella nätverket **VNET-PROD-DC-EUS2**.
    - Azure Database Migration Service placeras här eftersom tjänsten måste finnas i ett virtuellt nätverk med åtkomst till den lokala SQL Server VM via en VPN-gateway.
    - En peering görs av **VNET-PROD-EUS2** till **VNET-HUB-EUS2** och får behörighet att använda fjärrgatewayer. Alternativet **Använd fjärrgatewayer** säkerställer att Azure Database Migration Service kan kommunicera när det behövs.

        ![Database Migration Service – Konfigurera nätverket](media/contoso-migration-rehost-vm-sql-managed-instance/dms-network.png)

**Behöver du mer hjälp?**

- Lär dig att [konfigurera Azure Database Migration Service](https://docs.microsoft.com/azure/dms/quickstart-create-data-migration-service-portal).
- Lär dig att [skapa och använda SAS](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-shared-access-signature-part-2).

## <a name="step-3-prepare-azure-for-the-site-recovery-service"></a>Steg 3: Förbered Azure för tjänsten Site Recovery

Flera Azure-element krävs för att Contoso ska kunna konfigurera Site Recovery för migrering av den virtuella datorns webbnivå (**WEBMV**):

- Ett virtuellt nätverk där redundansväxlade resurser finns.
- Ett lagringskonto där replikerade data kan lagras.
- Ett Recovery Services-valv i Azure.

Contosos administratörer konfigurerar Site Recovery enligt följande:

1. Eftersom den virtuella datorn är en webbklientdel till SmartHotel360-appen växlar Contoso över den virtuella datorn till det befintliga produktionsnätverket (**VNET-PROD-EUS2**) och undernätet **(PROD-FE-EUS2**). Nätverket och undernätet finns i den primära regionen USA, östra 2. Contoso konfigurerade nätverket när [Azure-infrastrukturen distribuerades](./contoso-migration-infrastructure.md).
2. De skapar ett lagringskonto (**contosovmsacc20180528**). Contoso använder ett konto för generell användning. Contoso väljer standardlagring och lokalt redundant lagringsreplikering.

    ![Site Recovery – Skapa ett lagringskonto](media/contoso-migration-rehost-vm-sql-managed-instance/asr-storage.png)

3. När nätverket och lagringskontot finns på plats skapar de ett valv (**ContosoMigrationVault**). Contoso placerar valvet i resursgruppen **ContosoFailoverRG** i den primära regionen USA, östra 2.

    ![Recovery Services – Skapa ett valv](media/contoso-migration-rehost-vm-sql-managed-instance/asr-vault.png)

**Behöver du mer hjälp?**

Lär dig att [konfigurera Azure för Site Recovery](https://docs.microsoft.com/azure/site-recovery/tutorial-prepare-azure).

## <a name="step-4-prepare-on-premises-vmware-for-site-recovery"></a>Steg 4: Förbered lokala VMware för Site Recovery

Contosos administratörer måste utföra följande uppgifter för att VMware ska förberedas för Site Recovery:

- Förbereda ett konto i vCenter Server-instansen eller vSphere ESXi-värden. Kontot automatiserar identifieringen av virtuella datorer.
- Förbereda ett konto som tillåter automatisk installation av Mobility Service på virtuella VMware-datorer som Contoso vill replikera.
- Förbereda lokala virtuella datorer för att ansluta till virtuella Azure-datorer när de har skapats efter en redundans.

### <a name="prepare-an-account-for-automatic-discovery"></a>Förbereda ett konto för automatisk identifiering

Site Recovery måste ha åtkomst till VMware-servrarna för att:

- Identifiera automatiskt virtuella datorer. Minst ett skrivskyddat konto krävs.
- Samordna replikering, redundans och återställning efter fel. Contoso måste ha ett konto som kan köra åtgärder som att till exempel skapa och ta bort diskar samt starta virtuella datorer.

Contosos administratörer konfigurerar kontot genom att utföra följande uppgifter:

1. Skapar en roll på vCenter-nivå.
2. Tilldelar de behörigheter som krävs för rollen.

**Behöver du mer hjälp?**

Lär dig att [skapa och tilldela en roll för automatisk identifiering](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-automatic-discovery).

### <a name="prepare-an-account-for-mobility-service-installation"></a>Förbereda ett konto för installation av Mobility Service

Mobility Service måste installeras på den virtuella dator som Contoso vill replikera. Contoso överväger följande faktorer om Mobility Service:

- Site Recovery kan utföra en automatisk push-installation av komponenten när Contoso aktiverar replikering av den virtuella datorn.
- För att en automatisk push-installation ska kunna användas, måste Contoso förbereda det konto som Site Recovery använder för att komma åt den virtuella datorn.
- Det här kontot anges när replikeringen konfigureras i Azure-konsolen.
- Contoso måste ha en domän eller ett lokalt konto med behörighet för installation på den virtuella datorn.

**Behöver du mer hjälp?**

Läs om att [skapa ett konto för push-installation av Mobility Service](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-mobility-service-installation).

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Förbereda för att ansluta till virtuella Azure-datorer efter en redundansväxling

Efter redundansväxlingen till Azure vill contoso ansluta till de replikerade virtuella datorerna i Azure. Contoso-administratörer måste utföra några uppgifter på den lokala virtuella datorn innan migreringen:

1. För att få åtkomst via Internet aktiverar de RDP på den lokala virtuella datorn före redundansen. De kontrollerar att TCP- och UDP-regler har lagts till för den **offentliga** profilen och att RDP tillåts i **Windows-brandväggen** > **Tillåtna appar** för alla profiler.
2. För att få åtkomst via Contosos plats-till-plats-VPN aktiverar de RDP på den lokala datorn. De tillåter RDP i **Windows-brandväggen** > **Tillåtna appar och funktioner** för nätverken **Domän och Privat**.
3. De anger operativsystemets SAN-princip på den lokala virtuella datorn till **OnlineAll**.

Contosos administratörer måste också kontrollera dessa objekt när de kör en redundans:

- Det får inte finnas några väntande Windows-uppdateringar på den virtuella datorn när en redundans utlöses. Om Windows-uppdateringar väntar kan Contoso-användarna inte logga in på den virtuella datorn förrän uppdateringen är färdig.
- Efter en redundans bör administratörerna kontrollera att **Startdiagnostik** visar en skärmbild av den virtuella datorn. Om de inte kan se startdiagnostiken bör de kontrollera att den virtuella datorn körs och sedan läsa [felsökningstipsen](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

## <a name="step-5-replicate-the-on-premises-vms-to-azure"></a>Steg 5: replikera lokala virtuella datorer till Azure

Innan de kör en migrering till Azure, måste Contosos administratörer konfigurera och aktivera replikering för den lokala virtuella datorn.

### <a name="set-a-replication-goal"></a>Ange ett replikeringsmål

1. De anger ett replikeringsmål i valvet med valvnamnet (**ContosoVMVault**) (**Komma igång** > **Site Recovery** > **Förbered infrastrukturen**).
2. De anger att datorerna finns lokalt och att de är virtuella VMware-datorer som replikerar till Azure.

    ![Förbered infrastrukturen – Skyddsmål](./media/contoso-migration-rehost-vm-sql-managed-instance/replication-goal.png)

### <a name="confirm-deployment-planning"></a>Bekräfta distributionsplanering

Innan de går vidare kontrollerar Contosos administratörer att de har slutfört distributionsplaneringen. De väljer **Ja, det har jag gjort**. I den här distributionen migrerar Contoso bara en virtuell dator, så distributionsplaneringen behövs inte.

### <a name="set-up-the-source-environment"></a>Konfigurera källmiljön

Nu ska Contosos administratörer konfigurera källmiljön. För att konfigurera källmiljön laddar de ned en OVF-mall och använder den för att distribuera konfigurationsservern och dess associerade komponenter som en lokal virtuell VMware-dator med hög tillgänglighet. Komponenterna på servern inkluderar:

- Konfigurationsservern som samordnar kommunikationen mellan den lokala infrastrukturen och Azure. Konfigurationsservern hanterar datareplikering.
- Processervern som fungerar som en replikeringsgateway. Processervern:
  - Tar emot replikeringsdata.
  - Optimerar replikeringsdata med hjälp av cachelagring, komprimering och kryptering.
  - Skickar replikeringsdata till Azure Storage.
- Processervern installerar också Mobility Service på de virtuella datorer som ska replikeras. Processervern utför en automatisk identifiering av lokala virtuella VMware-datorer.
- När konfigurationsserverns virtuella dator har skapats och startats, registrerar Contoso servern i valvet.

Contosos administratörer gör följande för att konfigurera källmiljön:

1. De laddar ned OVF-mallen från Azure-portalen (**Förbered infrastrukturen** > **Källa** > **Konfigurationsserver)** .

    ![Lägga till en konfigurationsserver](./media/contoso-migration-rehost-vm-sql-managed-instance/add-cs.png)

2. De importerar mallen till VMware för att skapa och distribuera den virtuella datorn.

    ![Distribuera OVF-mall](./media/contoso-migration-rehost-vm-sql-managed-instance/vcenter-wizard.png)

3. När de sätter igång den virtuella datorn första gången, startas den i en installationsmiljö för Windows Server 2016. De godkänner licensavtalet och anger ett administratörslösenord.
4. När installationen är klar loggar de in på den virtuella datorn som administratör. Vid den första inloggningen körs Azure Site Recovery-konfigurationsverktyget automatiskt.
5. I konfigurationsverktyget för Site Recovery anger de ett namn som ska användas när konfigurationsservern registreras i valvet.
6. Verktyget kontrollerar den virtuella datorns anslutning till Azure. När anslutningen har upprättats väljer de **Logga in** för att logga in på Azure-prenumerationen. Autentiseringsuppgifterna måste ha åtkomst till det valv där konfigurationsservern är registrerad.

    ![Registrera konfigurationsservern](./media/contoso-migration-rehost-vm-sql-managed-instance/config-server-register2.png)

7. Verktyget utför vissa konfigurationsåtgärder och startar sedan om datorn. De loggar in på datorn igen. Guiden för konfiguration av hanteringsservrar startar automatiskt.
8. I guiden väljer de det nätverkskort som ska ta emot replikeringstrafiken. Det går inte att ändra den här inställningen när den har konfigurerats.
9. De väljer prenumeration, resursgrupp och Recovery Services-valv där konfigurationsservern ska registreras.

    ![Välja Recovery Services-valv](./media/contoso-migration-rehost-vm-sql-managed-instance/cswiz1.png)

10. De laddar ned och installerar MySQL-servern och VMware PowerCLI. Därefter verifierar de serverinställningarna.
11. Efter verifieringen anger de det fullständiga domännamnet eller IP-adressen för vCenter Server-instansen eller vSphere-värden. De lämnar standardporten och anger ett visningsnamn för vCenter Server-instansen i Azure.
12. De anger det konto som skapades tidigare så att Site Recovery automatiskt kan identifiera virtuella VMware-datorer som är tillgängliga för replikering.
13. De anger autentiseringsuppgifter så Mobility Service installeras automatiskt när replikering är aktiverad. I Windows-datorer måste kontot ha lokal administratörsbehörighet på de virtuella datorerna.

    ![Konfigurera vCenter Server](./media/contoso-migration-rehost-vm-sql-managed-instance/cswiz2.png)

14. När registreringen är klar i Azure-portalen kontrollerar de på nytt att konfigurationsservern och VMware-servern visas på sidan **Källa** i valvet. Identifieringen kan ta 15 minuter eller mer.
15. Site Recovery ansluter till VMware-servrar med hjälp av de angivna inställningarna och identifierar virtuella datorer.

### <a name="set-up-the-target"></a>Konfigurera målet

Nu konfigurerar Contosos administratörer målreplikeringens miljö:

1. De klickar på **Förbered infrastruktur** > **Mål** och väljer målinställningarna.
2. Site Recovery kontrollerar att det finns ett lagringskonto och ett nätverk på det angivna målet.

### <a name="create-a-replication-policy"></a>Skapa replikeringsprincip

När källan och målet har konfigurerats skapar Contosos administratörer en replikeringsprincip och associerar principen med konfigurationsservern:

1. I **Förbered infrastrukturen** > **Replikeringsinställningar** > **Replikeringsprincip** >  **Skapa och associera** skapar de principen **ContosoMigrationPolicy**.
2. De använder standardinställningarna:
    - Återställnings **tröskel:** Standardvärdet är 60 minuter. Det här värdet anger hur ofta återställningspunkter skapas. En avisering genereras när den kontinuerliga replikeringen överskrider den här gränsen.
    - **Kvarhållning av återställnings punkter:** Standardvärdet är 24 timmar. Det här värdet anger kvarhållningsperioden för varje återställningspunkt. Replikerade virtuella datorer kan återställas till valfri punkt i ett fönster.
    - **Frekvens för programkonsekventa ögonblicks bilder:** Standardvärdet är 1 timme. Det här värdet anger med vilken frekvens programkonsekventa ögonblicksbilder skapas.

    ![Replikeringsprincip – Skapa](./media/contoso-migration-rehost-vm-sql-managed-instance/replication-policy.png)

3. Principen associeras automatiskt med konfigurationsservern.

    ![Replikeringsprincip – Associera](./media/contoso-migration-rehost-vm-sql-managed-instance/replication-policy2.png)

**Behöver du mer hjälp?**

- Du kan läsa en fullständig genomgång av de här stegen i [Konfigurera haveriberedskap för lokala virtuella VMware-datorer](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial).
- Detaljerade instruktioner finns tillgängliga som hjälper dig att [konfigurera källmiljön](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-source), [distribuera konfigurationsservern](https://docs.microsoft.com/azure/site-recovery/vmware-azure-deploy-configuration-server) och [konfigurera replikeringsinställningar](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-replication).

### <a name="enable-replication"></a>Aktivera replikering

Contosos administratörer kan nu börja replikera WebVM.

1. De väljer källinställningar i **Replikera program** > **Källa** > **Replikera**.
2. De anger att de vill aktivera virtuella datorer, väljer vCenter Server-instansen och ställer in konfigurationsservern.

    ![Aktivera replikering – Källa](./media/contoso-migration-rehost-vm-sql-managed-instance/enable-replication1.png)

3. De anger målinställningarna, inklusive resursgruppen och nätverket där den virtuella Azure-datorn kommer att finnas efter redundansen. De anger det lagringskonto där replikerade data ska lagras.

    ![Aktivera replikering – Mål](./media/contoso-migration-rehost-vm-sql-managed-instance/enable-replication2.png)

4. De väljer **WebVM** för replikeringen. Site Recovery installerar Mobility Service på alla virtuella datorer när replikering är aktiverad.

    ![Aktivera replikering – Välj den virtuella datorn](./media/contoso-migration-rehost-vm-sql-managed-instance/enable-replication3.png)

5. De kontrollerar att rätt replikeringsprincip är vald och aktiverar replikering för **WEBVM**. De spårar replikeringsförloppet i **Jobb**. När jobbet **Slutför skydd** har körts är datorn redo för redundans.

6. De kan se status för de virtuella datorer som replikerar till Azure i **Information** i Azure-portalen:

    ![Infrastrukturvy](./media/contoso-migration-rehost-vm-sql-managed-instance/essentials.png)

**Behöver du mer hjälp?**

En fullständig genomgång av de här stegen finns i [Aktivera replikering](https://docs.microsoft.com/azure/site-recovery/vmware-azure-enable-replication).

## <a name="step-6-migrate-the-database"></a>Steg 6: Migrera databasen

Contosos administratörer måste skapa ett Azure Database Migration Service-projekt och sedan migrera databasen.

### <a name="create-an-azure-database-migration-service-project"></a>Skapa ett Azure Database Migration Service-projekt

1. De skapar ett Azure Database Migration Service-projekt. De väljer **SQL Server** som källservertyp och **Azure SQL Database Managed Instance** som mål.

     ![Database Migration Service – Nytt migreringsprojekt](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-project.png)

2. Migreringsguiden öppnas.

### <a name="migrate-the-database"></a>Migrera databasen

1. I migreringsguiden anger de den virtuella källdator som den lokala databasen finns på. De anger autentiseringsuppgifterna för att få åtkomst till databasen.

    ![Database Migration Service – Källinformation](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-wizard-source.png)

2. De väljer den databas som ska migreras (**SmartHotel.Registration**):

    ![Database Migration Service – Välja källdatabaser](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-wizard-sourcedb.png)

3. Som mål anger de namnet på den hanterade instansen i Azure och autentiseringsuppgifterna för åtkomst.

    ![Database Migration Service – Målinformation](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-target-details.png)

4. I **Ny aktivitet** > **Kör migrering** anger de inställningar för att köra migreringen:
    - Autentiseringsuppgifter för källa och mål.
    - Databasen som ska migreras.
    - Nätverksresursen som skapats på den lokala virtuella datorn. Azure Database Migration Service säkerhetskopierar källan till den här filresursen.
        - Tjänstkontot som kör källans SQL Server-instans måste ha skrivbehörighet på den här filresursen.
        - FQDN-sökvägen till filresursen måste användas.
    - Den SAS-URI som förser Azure Database Migration Service med åtkomst till lagringskontots container, som tjänsten laddar upp säkerhetskopiorna till vid migrering.

        ![Database Migration Service – Konfigurera migreringsinställningar](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-migration-settings.png)

5. De sparar migreringsinställningarna och kör sedan migreringen.
6. I **Översikt** övervakar de migreringens status.

    ![Database Migration Service – Övervaka](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-monitor1.png)

7. När migreringen är klar kontrollerar de att måldatabaserna finns på den hanterade instansen.

    ![Database Migration Service – Verifiera databasmigreringen](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-monitor2.png)

## <a name="step-7-migrate-the-vm"></a>Steg 7: migrera den virtuella datorn

Contosos administratörer kör en snabb testning av redundansen och migrerar sedan den virtuella datorn.

### <a name="run-a-test-failover"></a>Köra ett redundanstest

Innan de migrerar WEBVM kan ett redundanstest hjälpa dem att se att allt fungerar som förväntat. Administratörerna utför följande steg:

1. De kör ett redundanstest till den senaste tillgängliga tidpunkten (**Senast bearbetad**).
2. De väljer **Stäng datorn innan du påbörjar redundans**. När det här alternativet är valt försöker Site Recovery stänga av den virtuella källdatorn innan redundansen utlöses. Redundansen fortsätter även om avstängningen misslyckas.
3. Redundanstestet kör: a. En kravkontroll körs för att säkerställa att alla de villkor som krävs vid migreringen är uppfyllda.
    b. Redundansen bearbetar data så att du kan skapa en virtuell Azure-dator. Om den senaste återställningspunkten väljs, skapas en återställningspunkt från datan.
    c. En virtuell Azure-dator skapas med hjälp av de data som bearbetades i föregående steg.
4. När redundansen är klar visas repliken av den virtuella Azure-datorn i Azure-portalen. De kontrollerar att allt fungerar som det ska: att den virtuella datorn har rätt storlek, att den är ansluten till rätt nätverk och att den körs.
5. När de har verifierat redundanstestet rensar de redundansen och registrerar eventuella observationer.

### <a name="migrate-the-vm"></a>Migrera den virtuella datorn

1. När de har verifierat att redundanstestningen fungerade som förväntat, skapar Contosos administratörer en återställningsplan för migreringen och lägger till WEBVM i planen:

     ![Skapa återställningsplan – Välja objekt](./media/contoso-migration-rehost-vm-sql-managed-instance/recovery-plan.png)

2. De kör en redundans i planen och väljer den senaste återställningspunkten. De anger att Site Recovery ska försöka stänga av den lokala virtuella datorn innan redundansen utlöses.

    ![Redundans](./media/contoso-migration-rehost-vm-sql-managed-instance/failover1.png)

3. Efter redundansväxlingen kontrollerar de att den virtuella Azure-datorn visas som förväntat på Azure-portalen.

   ![Information om återställningsplan](./media/contoso-migration-rehost-vm-sql-managed-instance/failover2.png)

4. När verifieringen är klar slutför de migreringen för att avsluta migreringsprocessen, samt stoppa replikeringen och Site Recovery-faktureringen för den virtuella datorn.

    ![Redundans – Slutföra migrering](./media/contoso-migration-rehost-vm-sql-managed-instance/failover3.png)

### <a name="update-the-connection-string"></a>Uppdatera anslutningssträngen

Som det sista steget i migreringsprocessen uppdaterar Contosos administratörer anslutningssträngen för programmet så att den pekar på den migrerade databas som körs i Contosos hanterade instans.

1. De hittar anslutningssträngen i Azure-portalen genom att välja **Inställningar** > **Anslutningssträngar**.

    ![Anslutningssträngar](./media/contoso-migration-rehost-vm-sql-managed-instance/failover4.png)

2. De uppdaterar strängen med användarnamnet och lösenordet för SQL Database Managed Instance.
3. När strängen har konfigurerats ersätter de den aktuella anslutningssträngen i filen web.config för programmet.
4. När de har uppdaterat filen och sparat den, startar de om IIS på WEBVM genom att köra `IISRESET /RESTART` i kommandotolkens fönster.
5. När IIS har startats om använder appen den databas som körs på SQL Database Managed Instance.
6. Nu kan de stänga av den lokala SQLVM-datorn. Migreringen har slutförts.

**Behöver du mer hjälp?**

- Lär dig att [köra ett redundanstest](https://docs.microsoft.com/azure/site-recovery/tutorial-dr-drill-azure).
- Lär dig att [skapa en återställningsplan](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans).
- Lär dig att [redundansväxla till Azure](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover).

## <a name="clean-up-after-migration"></a>Rensa efter migreringen

När migreringen är klar körs SmartHotel360-appen på en virtuell Azure-dator och SmartHotel360-databasen finns i Azure SQL Database Managed Instance.

Contoso måste nu utföra följande rensning:

- Ta bort WEBVM-datorn från vCenter Server-lagret.
- Ta bort SQLVM-datorn från vCenter Server-lagret.
- Ta bort WEBVM och SQLVM från lokala säkerhetskopieringsjobb.
- Uppdatera den interna dokumentationen med den nya platsen och IP-adressen för WEBVM.
- Ta bort SQLVM från den interna dokumentationen. Contoso kan också ändra dokumentationen till att visa SQLVM som borttagen och inte längre i VM-lagret.
- Granska alla resurser som interagerar med de inaktiverade virtuella datorerna. Uppdatera relevanta inställningar eller dokumentation med den nya konfigurationen.

## <a name="review-the-deployment"></a>Granska distributionen

Med de migrerade resurserna i Azure måste Contoso operationalisera och skydda den nya infrastrukturen.

### <a name="security"></a>Säkerhet

Contosos säkerhetsteam granskar de virtuella Azure-datorerna och SQL Database Managed Instance så att det inte finns några säkerhetsproblem med implementeringen:

- Teamet granskar de nätverkssäkerhetsgrupper som används till att styra åtkomsten för den virtuella datorn. Nätverkssäkerhetsgrupperna säkerställer att endast tillåten trafik kan skickas till appen.
- Contosos säkerhetsteam överväger också att skydda datan på disken med hjälp av Azure Disk Encryption och Azure Key Vault.
- Teamet aktiverar hotidentifiering på den hanterade instansen. Hotidentifieringen skickar en avisering till Contosos säkerhetsteam/support om att öppna ett supportärende ifall ett hot har upptäckts. Läs mer om [hotidentifiering för Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-threat-detection).

     ![Managed Instance-säkerhet – Hotidentifiering](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-security.png)

Mer information om säkerhet för virtuella datorer finns i [Säkerhetsmetodtips för IaaS-arbetsbelastningar i Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

### <a name="bcdr"></a>Affärskontinuitet och haveriberedskap

För affärskontinuitet och haveriberedskap (BCDR) vidtar Contoso följande åtgärder:

- Behåll data säkra: contoso säkerhetskopierar data på de virtuella datorerna med hjälp av tjänsten Azure Backup. [Läs mer](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
- Håll apparna igång: contoso replikerar virtuella app-datorer i Azure till en sekundär region med hjälp av Site Recovery. [Läs mer](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).
- Contoso lär sig mer om att hantera SQL Managed Instance, inklusive [säkerhetskopiering av databaser](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).

### <a name="licensing-and-cost-optimization"></a>Licensierings- och kostnadsoptimering

- Contoso har redan en licens för WEBVM. För att kunna utnyttja Azure Hybrid-förmånen konverterar Contoso den befintliga virtuella Azure-datorn.
- Contoso aktiverar Azure Cost Management som licensieras av Cloudyn, ett dotterbolag till Microsoft. Cost Management är en kostnadshanteringslösning för flera moln som hjälper Contoso att använda och hantera Azure och andra molnresurser på ett bättre sätt. Läs mer om [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview).

## <a name="conclusion"></a>Sammanfattning

I den här artikeln kommer Contoso att ange en ny värd för SmartHotel360-appen i Azure genom att migrera appens virtuella klientdelsdator till Azure med hjälp av Site Recovery-tjänsten. Contoso migrerar den lokala databasen till en Azure SQL Database Managed Instance genom att använda Azure Database Migration Service.
