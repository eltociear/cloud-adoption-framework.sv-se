---
title: Byta värd för en app genom migrering till virtuella Azure-datorer med Azure Site Recovery
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Läs om hur Contoso byter värd för en lokalt installerad app med en lift and shift-migrering av lokala datorer till Azure med Azure Site Recovery-tjänsten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 0bfadba7f6cefc5cd597d002c3cb18b0cfcc8c3d
ms.sourcegitcommit: e0a783dac15bc4c41a2f4ae48e1e89bc2dc272b0
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73058192"
---
# <a name="rehost-an-on-premises-app-to-azure-vms"></a>Byt värd för en lokal app till virtuella Azure-datorer

Den här artikeln beskriver hur det fiktiva företaget Contoso byter värd för en Windows .NET-klientapp med två nivåer som körs på virtuella VMware-datorer genom att migrera appens virtuella datorer till virtuella Azure-datorer.

SmartHotel360-appen som används i det här exemplet tillhandahålls som öppen källkod. Om du vill använda den i ett eget test kan du ladda ned den från [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Affärsdrivande faktorer

IT-ledningsgruppen har arbetat tillsammans med affärspartner för att komma fram till vad man vill uppnå med migreringen:

- **Hantera företagets tillväxt.** Contoso växer, vilket leder till tryck på lokala system och infrastruktur.
- **Begränsa risker.** SmartHotel360-appen är viktig för Contosos verksamhet. De vill flytta appen till Azure utan några risker.
- **Utöka.** Contoso vill inte ändra appen, men måste vara säkra på att den är stabil.

## <a name="migration-goals"></a>Migreringsmål

Contosos molnteam har fastställt mål för migreringen. Målen används för att fastställa den bästa migreringsmetoden:

- Efter migreringen ska appen i Azure ha samma prestandafunktioner som den har i dag i VMware. Appen är lika viktig i molnet som den är lokalt.
- Contoso vill inte investera i den här appen. Den är viktig för verksamheten, men i dess aktuella form vill Contoso bara flytta den till molnet på ett säkert sätt.
- Contoso vill inte ändra driftmodellen för appen. Contoso vill interagera med den i molnet på samma sätt som de gör nu.
- Contoso vill inte ändra några av appens funktioner. Endast appens plats ska ändras.

## <a name="solution-design"></a>Lösningsdesign

När de har fastställt målen och kraven utformar och utvärderar Contoso en distributionslösning och identifierar migreringsprocessen, inklusive de Azure-tjänster som Contoso använder för migreringen.

### <a name="current-app"></a>Aktuell app

- Appen är nivåindelad på två virtuella datorer (**WEBVM** och **SQLVM**).
- De virtuella datorerna finns på VMware ESXi-värden **contosohost1.contoso.com** (version 6.5).
- VMware-miljön hanteras av vCenter Server 6.5 (**vcenter.contoso.com**), som körs på en virtuell dator.
- Contoso har ett lokalt datacenter (contoso-datacenter) med en lokal domänkontrollant (**contosodc1**).

### <a name="proposed-architecture"></a>Föreslagen arkitektur

- Eftersom appen är en produktionsarbetsbelastning kommer de virtuella datorerna för appen i Azure att finnas i produktionsresursgruppen ContosoRG.
- De virtuella datorerna för appen migreras till den primära Azure-regionen (USA, östra 2) och placeras i produktionsnätverket (VNET-PROD-EUS2).
- Den virtuella webbklienten placeras i undernätet för klientdelen (PROD-FE-EUS2) i produktionsnätverket.
- Den virtuella datorn för databasen placeras i undernätet för databaser (PROD-DB-EUS2) i produktionsnätverket.
- De lokala, virtuella datorerna i Contoso-datacentret kommer att inaktiveras när migreringen är färdig.

![Scenariots arkitektur](./media/contoso-migration-rehost-vm/architecture.png)

### <a name="database-considerations"></a>Databasöverväganden

Som en del av processen för lösningsdesign gjorde Contoso en funktionsjämförelse mellan Azure SQL Database och SQL Server. Nedanstående överväganden hjälpte dem att välja SQL Server på en virtuell Azure IaaS-dator:

- Användning av en virtuell Azure-dator som kör SQL Server verkar vara en optimal lösning om Contoso behöver anpassa operativsystemet eller databasservern, eller om de vill samlokalisera och köra appar från tredje part på samma virtuella dator.
- Med Software Assurance kan Contoso i framtiden byta ut befintliga licenser till rabatterade priser för en SQL-databas, hanterad instans med hjälp av Azure Hybrid-förmånen för SQL Server. Detta kan spara upp till 30 % på hanterad instans.

### <a name="solution-review"></a>Lösningsgranskning

Contoso utvärderar den föreslagna designen genom att skapa en lista med för- och nackdelar.

<!-- markdownlint-disable MD033 -->

**Övervägande** | **Detaljer**
--- | ---
**Fördelar** | Båda appens virtuella datorer flyttas till Azure utan ändringar, vilket gör migreringen enkel.<br/><br/> Eftersom Contoso använder ”lift and shift” för båda appens virtuella datorer, behövs ingen speciell konfiguration eller speciella migreringsverktyg för appdatabasen.<br/><br/> Contoso kan dra nytta av sina investeringar i Software Assurance och använda Azure Hybrid-förmånen.<br/><br/> Contoso har fortfarande full kontroll över appens virtuella datorer i Azure.
**Nackdelar** | WEBVM och SQLVM kör Windows Server 2008 R2. Operativsystemet stöds av Azure för specifika roller (juli 2018). [Läs mer](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).<br/><br/> Appens webb- och datanivåer förblir en enskild felpunkt.<br/><br/> SQLVM körs på SQL Server 2008 R2 som inte inkluderas i mainstream-support. Det stöds dock för virtuella Azure-datorer (juli 2018). [Läs mer](https://support.microsoft.com/help/956893).<br/><br/> Contoso måste fortsätta att hantera appen som virtuella Azure-datorer i stället för att flytta till en hanterad tjänst, till exempel Azure App Service och Azure SQL Database.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Migreringsprocessen

Contoso kommer att migrera appens klientdel och virtuella databaser till virtuella Azure-datorer med den agentlösa metoden för Azure Migrate-servermigrering.

- Som ett första steg förbereder och konfigurerar Contoso Azure-komponenter för Azure Migrate-servermigreringen och den lokala VMware-infrastrukturen.
- Contoso har redan [Azure-infrastrukturen](./contoso-migration-infrastructure.md), så de behöver bara lägga till och konfigurera replikeringen av de virtuella datorerna med verktyget för Azure Migrate-servermigrering.
- När allt är förberett kan Contoso börja replikera de virtuella datorerna.
- När replikeringen har aktiverats och fungerar migrerar Contoso den virtuella datorn genom att redundansväxla till Azure.

![Migreringsprocessen](./media/contoso-migration-rehost-vm/migration-process-az-migrate.png)

### <a name="azure-services"></a>Azure-tjänster

**Tjänst** | **Beskrivning** | **Kostnad**
--- | --- | ---
[Azure Migrate-servermigrering](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm) | Tjänsten samordnar och styr migreringen av dina lokala appar och arbetsbelastningar, samt virtuella AWS/GCP-datorinstanser. | Vid replikering till Azure debiteras Azure Storage-avgifter. Virtuella Azure-datorer skapas och medför kostnader i samband med en redundansväxling. [Läs mer](https://azure.microsoft.com/pricing/details/azure-migrate) om avgifter och priser.

## <a name="prerequisites"></a>Krav

Det här behöver Contoso för att köra detta scenario.

<!-- markdownlint-disable MD033 -->

**Krav** | **Detaljer**
--- | ---
**Azure-prenumeration** | Contoso skapade prenumerationer i en tidigare artikel i den här serien. Om du inte har någon Azure-prenumeration kan du skapa ett [kostnadsfritt konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Om du skapar ett kostnadsfritt konto är du administratör för din prenumeration och kan utföra alla åtgärder.<br/><br/> Om du använder en befintlig prenumeration och inte är administratör måste du be administratören att ge dig ägar- eller deltagarbehörighet.<br/><br/> Om du behöver mer detaljerade behörigheter läser du [den här artikeln](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Azure-infrastruktur** | [Läs om hur](./contoso-migration-infrastructure.md) Contoso konfigurerar en Azure-infrastruktur.<br/><br/> Läs mer om specifika [krav](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm#prerequisites) för Azure Migrate-servermigrering.
**Lokala servrar** | De lokala vCenter-servrarna bör köra version 5.5, 6.0 eller 6.5<br/><br/> ESXi-värdar bör köra version 5.5, 6.0 eller 6.5<br/><br/> En eller flera virtuella VMware-datorer ska köras på ESXi-värden.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Steg i scenariot

Contosos administratörer genomför migreringen på följande sätt:

> [!div class="checklist"]
>
> - **Steg 1: Förbered Azure för migrering av Azure Migrate Server.** De lägger till servermigreringsverktyget i sitt Azure Migrate-projekt.
> - **Steg 2: Förbered lokala VMware för Azure Migrate Server-migrering.** De förbereder konton för identifiering av virtuella datorer och för att ansluta till virtuella Azure-datorer efter en redundansväxling.
> - **Steg 3: replikera virtuella datorer.** De konfigurerar replikering och startar replikeringen av virtuella datorer till Azure Storage.
> - **Steg 4: migrera de virtuella datorerna med Azure Migrate Server-migrering.** De kör ett redundanstest för att se till att allt fungerar och kör sedan en fullständig redundansväxling för att migrera de virtuella datorerna till Azure.

## <a name="step-1-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Steg 1: Förbered Azure för verktyget för migrering av Azure Migrate Server

Här är de Azure-komponenter som Contoso behöver för att migrera de virtuella datorerna till Azure:

- Ett virtuellt nätverk där de virtuella Azure-datorerna ska placeras när de skapas under redundansväxling.
- Azure Migrate-servermigreringsverktyget etableras.

De konfigureras så här:

1. Konfigurera ett nätverk – Contoso konfigurerade ett nätverk som de kan använda till Azure Migrate-servermigreringen när de [distribuerade Azure-infrastrukturen](./contoso-migration-infrastructure.md)

    - SmartHotel360-appen är en produktionsapp och de virtuella datorerna migreras till Azure-produktionsnätverket (VNET-PROD-EUS2) i den primära regionen USA, östra 2.
    - Båda de virtuella datorerna placeras i resursgruppen ContosoRG, som används för produktionsresurser.
    - Den virtuella datorn med klientdelen (WEBVM) migreras till undernätet för klientdelen (PROD-FE-EUS2) i produktionsnätverket.
    - Den virtuella datorn med appdatabasen (SQLVM) migreras till undernätet för databaser (PROD-DB-EUS2) i produktionsnätverket.

2. Etablera Azure Migrate-servermigreringsverktyget – Med nätverket och lagringskontot på plats skapar Contoso nu ett Recovery Services-valv (ContosoMigrationVault) och placerar det i resursgruppen ContosoFailoverRG i den primära regionen USA, östra 2.

    ![Azure Migrate-servermigreringsverktyg](./media/contoso-migration-rehost-vm/server-migration-tool.png)

**Behöver du mer hjälp?**

[Läs om att](https://docs.microsoft.com/azure/migrate) konfigurera Azure Migrate-servermigreringsverktyget.

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Förbereda för att ansluta till virtuella Azure-datorer efter en redundansväxling

Efter redundansväxlingen vill Contoso ansluta till de virtuella Azure-datorerna. Contosos administratörer gör följande före migreringen för att göra detta:

1. För åtkomst via Internet gör de följande:

    - Aktivera RDP på den lokala virtuella datorn före redundansväxlingen.
    - Se till att TCP- och UDP-regler läggs till för den **offentliga** profilen.
    - Kontrollera att RDP tillåts i **Windows-brandväggen** > **Tillåtna appar** för alla profiler.

2. För åtkomst via plats-till-plats-VPN gör de följande:

    - Aktivera RDP på den lokala datorn.
    - Tillåta RDP i **Windows-brandväggen** -> **Tillåtna appar och funktioner**, för nätverken **Domän och Privat**.
    - Ange operativsystemets SAN-princip på den lokala virtuella datorn till **OnlineAll**.

Dessutom måste de kontrollera följande när de kör en redundansväxling:

- Det får inte finnas några väntande Windows-uppdateringar på den virtuella datorn när de utlöser en redundansväxling. Om det finns det kan de inte logga in på den virtuella datorn förrän uppdateringen är klar.
- Efter redundansväxlingen kan de kontrollera **Startdiagnostik** för att visa en skärmbild av den virtuella datorn. Om detta inte fungerar bör de kontrollera att den virtuella datorn körs och gå igenom de här [felsökningstipsen](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

**Behöver du mer hjälp?**

- [Läs om](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm#prepare-vms-for-migration) att förbereda virtuella datorer för migrering

## <a name="step-3-replicate-the-on-premises-vms"></a>Steg 3: replikera lokala virtuella datorer

Innan Contosos administratörer kan köra en migrering till Azure måste de konfigurera och aktivera replikering.

När identifieringen är klar kan du påbörja replikeringen av virtuella VMware-datorer till Azure.

1. I Azure Migrate Project >- **servrar** **Azure Migrate: Server-migrering**klickar du på **Replikera**.

    ![Replikera virtuella datorer](./media/contoso-migration-rehost-vm/select-replicate.png)

2. I **Replikera** > **Källinställningar** > **Är dina datorer virtualiserade?** väljer du **Ja, med VMware vSphere**.

3. I **Lokal dator** väljer du namnet på den Azure Migrate-dator som du konfigurerar > **OK**.

    ![Källinställningar](./media/contoso-migration-rehost-vm/source-settings.png)

4. I **Virtuella datorer** väljer du de datorer som du vill replikera.
    - Om du har kört en utvärdering av de virtuella datorerna, kan du tillämpa storleksändring av virtuella datorer och disktypsrekommendationer (premium/standard) från utvärderingsresultaten. Gör detta i **Vill du importera migreringsinställningar från en Azure Migrate-utvärdering?** och välj alternativet **Ja**.
    - Om du inte har kört någon utvärdering, eller om du inte vill använda utvärderingsinställningarna, väljer du alternativet **Nej**.
    - Om du valde att använda utvärderingen väljer du VM-grupp och utvärderingsnamn.

    ![Välj utvärdering](./media/contoso-migration-rehost-vm/select-assessment.png)

5. I **Virtuella datorer** söker du efter önskade datorer och markerar varje virtuell dator som du vill migrera. Klicka sedan på **Nästa: mål inställningar**.

6. I **Målinställningar** väljer du prenumeration och den målregion som du vill migrera till. Ange sedan den resursgrupp där du vill att de virtuella Azure-datorerna ska finnas efter migreringen. I **Virtuellt nätverk** väljer du det Azure VNet/undernät som de virtuella Azure-datorerna ska anslutas till efter migreringen.

7. I **Azure Hybrid-förmån**:

    - Välj **Nej** om du inte vill använda Azure Hybrid-förmånen. Klicka sedan på **Nästa**.
    - Välj **Ja** om du har Windows Server-datorer som omfattas av aktiva Software Assurance- eller Windows Server-prenumerationer och du vill tillämpa förmånen på de datorer som du migrerar. Klicka sedan på **Nästa**.

8. I **Compute** granskar du namnet på den virtuella datorn, storlek, disktyp för operativsystemet och tillgänglighetsuppsättningen. De virtuella datorerna måste följa [Azures krav](https://docs.microsoft.com/azure/migrate/migrate-support-matrix-vmware#agentless-migration-vmware-vm-requirements).

    - **VM-storlek**: om du använder utvärderings rekommendationer kommer List rutan VM-storlek att innehålla den rekommenderade storleken. Annars väljer Azure Migrate en storlek baserat på den närmaste matchningen i Azure-prenumerationen. Du kan också välja en storlek manuellt i **Storlek på virtuell Azure-dator**.
    - **OS-disk**: Ange OS-disken (start) för den virtuella datorn. Operativsystemdisken är den disk där operativsystemets bootloader och installationsprogram finns.
    - **Tillgänglighets uppsättning**: om den virtuella datorn ska finnas i en Azure-tillgänglighets uppsättning efter migreringen anger du uppsättningen. Uppsättningen måste finnas i målets resursgrupp som du anger för migreringen.

9. I **Diskar** anger du om VM-diskarna ska replikeras till Azure och disktypen (standard SSD/HDD eller premiumhanterade diskar) i Azure. Klicka sedan på **Nästa**.
    - Du kan undanta diskar från replikering.
    - Om du undantar diskar kommer de inte att synas i den virtuella Azure-datorn efter migreringen.

10. I **Granska och starta replikering** kontrollerar du inställningarna och klickar på **Replikera** för att påbörja den första replikeringen för servrarna.

> [!NOTE]
> Du kan uppdatera replikeringsinställningarna när du vill innan replikeringen startar i **Hantera** > **Replikera datorer**. Det går inte att ändra inställningarna efter att replikeringen har startat.

## <a name="step-4-migrate-the-vms"></a>Steg 4: migrera de virtuella datorerna

Contosos administratörer kör en snabb testning av redundans och sedan en fullständig redundansväxling för att migrera de virtuella datorerna.

### <a name="run-a-test-failover"></a>Köra ett redundanstest

1. I **mål för migrering**  > **servrar**  > **Azure Migrate: Server migrering**klickar du på **test migrerade servrar**.

     ![Testmigrerade servrar](./media/contoso-migration-rehost-vm/test-migrated-servers.png)

2. Högerklicka på den virtuella dator som ska testas och klicka på **Testmigrera**.

    ![Testmigrera](./media/contoso-migration-rehost-vm/test-migrate.png)

3. I **Testmigrera** väljer du det Azure VNet där den virtuella Azure-datorn kommer att finnas efter migreringen. Vi rekommenderar att du använder ett virtuellt nätverk som inte är för produktion.
4. **Testmigreringen** startas. Övervaka jobbet i portalmeddelanden.
5. När migreringen är klar kan du se den migrerade virtuella Azure-datorn i **Virtual Machines** i Azure Portal. Datornamnet har suffixet **-Test**.
6. När testet är klart högerklickar du på den virtuella Azure-datorn i **Replikera datorer** och klickar på **Rensa upp i testmigreringen**.

    ![Rensa migrering](./media/contoso-migration-rehost-vm/clean-up.png)

### <a name="migrate-the-vms"></a>Migrera de virtuella datorerna

Contosos administratörer kör nu en fullständig redundansväxling för att slutföra migreringen.

1. I Azure Migrate Project >- **servrar**  > **Azure Migrate: Server-migrering**klickar du på **Replikera servrar**.

    ![Servrarna replikeras](./media/contoso-migration-rehost-vm/replicating-servers.png)

2. I **Replikera datorer** högerklickar du på den virtuella datorn > **Migrera**.
3. I **Migrera** > **Stäng av virtuella datorer och utför en planerad migrering utan dataförlust** väljer du **Ja** > **OK**.
    - Som standard stänger Azure Migrate av den lokala virtuella datorn och kör en replikering på begäran som synkroniserar eventuella VM-ändringar som har inträffat sedan den senaste replikeringen utfördes. Detta säkerställer att ingen dataförlust sker.
    - Om du inte vill stänga av den virtuella datorn väljer du **Nej**
4. Ett migreringsjobb startas för den virtuella datorn. Spåra jobbet i Azure-meddelanden.
5. När jobbet är klart kan du se och hantera den virtuella datorn på sidan **Virtual Machines**.

**Behöver du mer hjälp?**

- [Lär dig](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#run-a-test-migration) hur du kör ett redundanstest.
- [Läs mer](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#migrate-vms) om migrering av virtuella datorer till Azure.

## <a name="clean-up-after-migration"></a>Rensa efter migrering

När migreringen är klar körs SmartHotel360-appens nivåer på virtuella Azure-datorer.

Nu måste Contoso utföra följande steg för rensning:

- När migreringen är klar stoppas replikeringen.
- Ta bort WEBVM-datorn från vCenter-lagret.
- Ta bort SQLVM-datorn från vCenter-lagret.
- Ta bort WEBVM och SQLVM från lokala säkerhetskopieringsjobb.
- Uppdatera den interna dokumentationen med de nya platserna och IP-adresserna för de virtuella datorerna.
- Granska alla resurser som interagerar med de virtuella datorerna och uppdatera alla relevanta inställningar eller dokumentation så att de överensstämmer med den nya konfigurationen.

## <a name="review-the-deployment"></a>Granska distributionen

Nu när appen körs måste Contoso operationalisera och säkra den i Azure.

### <a name="security"></a>Säkerhet

Contosos säkerhetsteam granskar de virtuella Azure-datorerna för att fastställa eventuella säkerhetsproblem.

- För åtkomstkontroll granskar teamet nätverkssäkerhetsgrupperna (NSG:er) för de virtuella datorerna. Nätverkssäkerhetsgrupper används för att säkerställa att bara behörig trafik kan nå appen.
- Teamet överväger också att skydda data på disken med Azure Disk Encryption och Key Vault.

Mer information finns i [rekommenderade säkerhets metoder för IaaS-arbetsbelastningar i Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

## <a name="bcdr"></a>Affärskontinuitet och haveriberedskap

För affärskontinuitet och haveriberedskap (BCDR) vidtar Contoso följande åtgärder:

- Behåll data säkra: contoso säkerhetskopierar data på de virtuella datorerna med hjälp av tjänsten Azure Backup. [Läs mer](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
- Håll apparna igång: contoso replikerar virtuella app-datorer i Azure till en sekundär region med hjälp av Site Recovery. [Läs mer](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Licensierings- och kostnadsoptimering

1. Contoso har befintlig licensiering för sina virtuella datorer och drar nytta av Azure Hybrid-förmånen. Contoso konverterar befintliga virtuella Azure-datorer för att dra nytta av denna prissättning.
2. Contoso aktiverar Azure Cost Management som licensieras av Cloudyn, ett Microsoft-dotterbolag. Det är en kostnadshanteringslösning för flera moln som hjälper till att använda och hantera Azure och andra molnresurser. [Läs mer](https://docs.microsoft.com/azure/cost-management/overview) om Azure Cost Management.

## <a name="conclusion"></a>Sammanfattning

I den här artikeln har Contoso angett en ny värd för SmartHotel360-appen i Azure, genom att migrera appens virtuella datorer till virtuella Azure-datorer med hjälp av Azure Migrate-servermigreringsverktyget.
