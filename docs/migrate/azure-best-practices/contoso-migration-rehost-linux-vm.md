---
title: Byta värd för en lokal Linux-app till virtuella Azure-datorer
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Se hur Contoso byter värd för en lokal Linux-app genom att migrera till virtuella Azure-datorer.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 8b925564b3186e153cdd9a8139499a83a1fd96ff
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/31/2019
ms.locfileid: "73239404"
---
# <a name="rehost-an-on-premises-linux-app-to-azure-vms"></a>Byta värd för en lokal Linux-app till virtuella Azure-datorer

Den här artikeln beskriver hur det fiktiva företaget Contoso byter värd för en Linux-baserad Apache MySQL PHP-app (LAMP) med två nivåer med hjälp av virtuella Azure IaaS-datorer.

osTicket, supportappen som används i det här exemplet, är tillgänglig som öppen källkod. Om du vill använda den i ett eget test kan du ladda ned den från [GitHub](https://github.com/osTicket/osTicket).

## <a name="business-drivers"></a>Affärsdrivande faktorer

IT-ledningsgruppen har arbetat tillsammans med affärspartner för att komma fram till vad man vill uppnå med migreringen:

- **Hantera företagets tillväxt.** Contoso växer, vilket leder till tryck på lokala system och infrastruktur.
- **Begränsa risker.** Supportappen är viktig för Contosos verksamhet. Contoso vill flytta den till Azure utan några risker.
- **Utöka.** Contoso vill inte ändra appen just nu. De vill bara vara säkra på att appen är stabil.

## <a name="migration-goals"></a>Migreringsmål

Molnteamet för Contoso har fastställt mål för migreringen för att avgöra vilken migreringsmetod som är bäst:

- Efter migreringen ska appen i Azure ha samma prestandafunktioner som den har i dag i den lokala VMware-miljön. Appen är lika viktig i molnet som den är lokalt.
- Contoso vill inte investera i den här appen. Den är viktig för verksamheten, men i dess aktuella form vill Contoso bara flytta den till molnet på ett säkert sätt.
- Contoso vill inte ändra driftmodellen för appen. De vill interagera med appen i molnet på samma sätt som de gör nu.
- Contoso vill inte ändra appens funktioner. Endast appens plats ska ändras.
- Efter att ha gjort ett par migreringar av Windows-appar vill Contoso lära sig hur man använder en Linux-baserad infrastruktur i Azure.

## <a name="solution-design"></a>Lösningsdesign

När de har fastställt målen och kraven utformar och utvärderar Contoso en distributionslösning och identifierar migreringsprocessen, inklusive de Azure-tjänster som Contoso använder för migreringen.

### <a name="current-app"></a>Aktuell app

- OSTicket-appen är indelad i nivåer på två virtuella datorer (**OSTICKETWEB** och **OSTICKETMYSQL**).
- De virtuella datorerna finns på VMware ESXi-värden **contosohost1.contoso.com** (version 6.5).
- VMware-miljön hanteras av vCenter Server 6.5 (**vcenter.contoso.com**), som körs på en virtuell dator.
- Contoso har ett lokalt datacenter (**contoso-datacenter**) med en lokal domänkontrollant (**contosodc1**)

### <a name="proposed-architecture"></a>Föreslagen arkitektur

- Eftersom appen är en produktionsarbetsbelastning kommer de virtuella datorerna i Azure att finnas i produktionsresursgruppen **ContosoRG**.
- De virtuella datorerna migreras till den primära regionen (USA, östra 2) och placeras i produktionsnätverket (VNET-PROD-EUS2):
  - Den virtuella webbdatorn placeras i undernätet för klientdelen (PROD-FE-EUS2).
  - Den virtuella databasen placeras i databasens undernät (PROD-DB-EUS2).
- De lokala, virtuella datorerna i Contoso-datacentret kommer att inaktiveras när migreringen är färdig.

![Scenariots arkitektur](./media/contoso-migration-rehost-linux-vm/architecture.png)

### <a name="solution-review"></a>Lösningsgranskning

Contoso utvärderar den föreslagna designen genom att skapa en lista med för- och nackdelar.

<!-- markdownlint-disable MD033 -->

**Övervägande** | **Detaljer**
--- | ---
**Fördelar** | Båda appens virtuella datorer flyttas till Azure utan ändringar, vilket gör migreringen enkel.<br/><br/> Eftersom Contoso använder en hiss och Skift-metod för både virtuella app-datorer behövs inga särskilda konfigurations-eller Migreringsverktyg för app-databasen.<br/><br/> Contoso har fortfarande full kontroll över appens virtuella datorer i Azure. <br/><br/> Appens virtuella datorer kör Ubuntu 16.04-TLS, som är en godkänd Linux-distribution. [Läs mer](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros).
**Nackdelar** | Appens webb- och datanivå förblir en enskild felpunkt. <br/><br/> Contoso måste fortsätta att hantera appen som virtuella Azure-datorer i stället för att flytta till en hanterad tjänst, till exempel Azure App Service och Azure Database for MySQL.<br/><br/> Contoso är medveten om att det är enkelt att göra saker med en hiss och Shift VM-migrering, de har inte fullständig nytta av de funktioner som tillhandahålls av [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) (inbyggd hög tillgänglighet, förutsägbar prestanda, enkel skalning, automatisk säkerhets kopiering och inbyggd säkerhet).

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Migreringsprocessen

Contoso migrerar på följande sätt:

- Som ett första steg förbereder och konfigurerar Contoso Azure-komponenter för Azure Migrate-servermigreringen och den lokala VMware-infrastrukturen.
- Contoso har redan [Azure-infrastrukturen](./contoso-migration-infrastructure.md), så de behöver bara lägga till och konfigurera replikeringen av de virtuella datorerna med verktyget för Azure Migrate-servermigrering.
- När allt är förberett kan Contoso börja replikera de virtuella datorerna.
- När replikeringen har aktiverats och fungerar migrerar Contoso den virtuella datorn genom att redundansväxla till Azure.

![Migreringsprocessen](./media/contoso-migration-rehost-linux-vm/migration-process-az-migrate.png)

### <a name="azure-services"></a>Azure-tjänster

**Tjänst** | **Beskrivning** | **Kostnad**
--- | --- | ---
[Azure Migrate-servermigrering](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm) | Tjänsten samordnar och styr migreringen av dina lokala appar och arbetsbelastningar, samt virtuella AWS/GCP-datorinstanser. | Vid replikering till Azure debiteras Azure Storage-avgifter. Virtuella Azure-datorer skapas och medför kostnader i samband med en redundansväxling. [Läs mer](https://azure.microsoft.com/pricing/details/azure-migrate) om avgifter och priser.

## <a name="prerequisites"></a>Krav

Det här är vad Contoso behöver i det här scenariot.

<!-- markdownlint-disable MD033 -->

**Krav** | **Detaljer**
--- | ---
**Azure-prenumeration** | Contoso skapade prenumerationer i en tidigare artikel i den här serien. Om du inte har någon Azure-prenumeration kan du skapa ett [kostnadsfritt konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Om du skapar ett kostnadsfritt konto är du administratör för din prenumeration och kan utföra alla åtgärder.<br/><br/> Om du använder en befintlig prenumeration och inte är administratör måste du be administratören att ge dig ägar- eller deltagarbehörighet.<br/><br/> Om du behöver mer detaljerade behörigheter läser du [den här artikeln](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Azure-infrastruktur** |  [Läs om hur](./contoso-migration-infrastructure.md) Contoso konfigurerar en Azure-infrastruktur.<br/><br/> Läs mer om specifika [krav](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm#prerequisites) för Azure Migrate-servermigrering.
**Lokala servrar** | Den lokala vCenter-servern bör köra version 5.5, 6.0 eller 6.5<br/><br/> En ESXi-värd som kör version 5.5, 6.0 eller 6.5<br/><br/> En eller flera virtuella VMware-datorer som körs på ESXi-värden.
**Lokala virtuella datorer** | [Granska Linux-datorer](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros) som ska köras i Azure.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Steg i scenariot

Så här slutför Contoso migreringen:

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

1. **Konfigurera ett nätverk:** Contoso har redan konfigurerat ett nätverk som kan användas för Azure Migrate Server-migrering när de [distribuerade Azure-infrastrukturen](./contoso-migration-infrastructure.md)

    - SmartHotel360-appen är en produktionsapp och de virtuella datorerna migreras till Azure-produktionsnätverket (VNET-PROD-EUS2) i den primära regionen USA, östra 2.
    - Båda de virtuella datorerna placeras i resursgruppen ContosoRG, som används för produktionsresurser.
    - Den virtuella datorn med klientdelen (WEBVM) migreras till undernätet för klientdelen (PROD-FE-EUS2) i produktionsnätverket.
    - Den virtuella datorn med appdatabasen (SQLVM) migreras till undernätet för databaser (PROD-DB-EUS2) i produktionsnätverket.

2. **Etablera verktyget för migrering av Azure Migrate Server:** Med nätverket och lagrings kontot på plats skapar Contoso nu ett Recovery Services valv (ContosoMigrationVault) och placerar det i resurs gruppen ContosoFailoverRG i den primära regionen USA, östra 2.

    ![Azure Migrate-servermigreringsverktyg](./media/contoso-migration-rehost-linux-vm/server-migration-tool.png)

**Behöver du mer hjälp?**

[Läs om att](https://docs.microsoft.com/azure/migrate) konfigurera Azure Migrate-servermigreringsverktyget.

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Förbereda för att ansluta till virtuella Azure-datorer efter en redundansväxling

Efter redundansväxlingen till Azure vill Contoso kunna ansluta till de replikerade virtuella datorerna i Azure. Det finns ett par saker som Contosos administratörer behöver göra:

- För att få åtkomst till virtuella Azure-datorer via Internet aktiverar de SSH på den lokala virtuella Linux-datorn innan migreringen. För Ubuntu kan detta utföras med hjälp av följande kommando: **sudo apt – Hämta ssh install-y**.
- När de har kört migreringen (redundansväxling) kan de kontrollera **startdiagnostiken** för att visa en skärmbild av den virtuella datorn.
- Om detta inte fungerar måste de kontrollera att den virtuella datorn körs och gå igenom [de här felsökningstipsen](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

**Behöver du mer hjälp?**

- [Läs om](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm#prepare-vms-for-migration) att förbereda virtuella datorer för migrering

## <a name="step-3-replicate-the-on-premises-vms"></a>Steg 3: replikera lokala virtuella datorer

Innan Contosos administratörer kan köra en migrering till Azure måste de konfigurera och aktivera replikering.

När identifieringen är klar kan du påbörja replikeringen av virtuella VMware-datorer till Azure.

1. I Azure Migrate Project >- **servrar** **Azure Migrate: Server-migrering**klickar du på **Replikera**.

    ![Replikera virtuella datorer](./media/contoso-migration-rehost-linux-vm/select-replicate.png)

2. I **Replikera** > **Källinställningar** > **Är dina datorer virtualiserade?** väljer du **Ja, med VMware vSphere**.
3. I **Lokal dator** väljer du namnet på den Azure Migrate-dator som du konfigurerar > **OK**.

    ![Källinställningar](./media/contoso-migration-rehost-linux-vm/source-settings.png)

4. I **Virtuella datorer** väljer du de datorer som du vill replikera.
    - Om du har kört en utvärdering av de virtuella datorerna, kan du tillämpa storleksändring av virtuella datorer och disktypsrekommendationer (premium/standard) från utvärderingsresultaten. Gör detta i **Vill du importera migreringsinställningar från en Azure Migrate-utvärdering?** och välj alternativet **Ja**.
    - Om du inte har kört någon utvärdering, eller om du inte vill använda utvärderingsinställningarna, väljer du alternativet **Nej**.
    - Om du valde att använda utvärderingen väljer du VM-grupp och utvärderingsnamn.

    ![Välj utvärdering](./media/contoso-migration-rehost-linux-vm/select-assessment.png)

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

     ![Testmigrerade servrar](./media/contoso-migration-rehost-linux-vm/test-migrated-servers.png)

2. Högerklicka på den virtuella dator som ska testas och klicka på **Testmigrera**.

    ![Testmigrera](./media/contoso-migration-rehost-linux-vm/test-migrate.png)

3. I **Testmigrera** väljer du det Azure VNet där den virtuella Azure-datorn kommer att finnas efter migreringen. Vi rekommenderar att du använder ett virtuellt nätverk som inte är för produktion.
4. **Testmigreringen** startas. Övervaka jobbet i portalmeddelanden.
5. När migreringen är klar kan du se den migrerade virtuella Azure-datorn i **Virtual Machines** i Azure Portal. Datornamnet har suffixet **-Test**.
6. När testet är klart högerklickar du på den virtuella Azure-datorn i **Replikera datorer** och klickar på **Rensa upp i testmigreringen**.

    ![Rensa migrering](./media/contoso-migration-rehost-linux-vm/clean-up.png)

### <a name="migrate-the-vms"></a>Migrera de virtuella datorerna

Contosos administratörer kör nu en fullständig redundansväxling för att slutföra migreringen.

1. I Azure Migrate Project >- **servrar**  > **Azure Migrate: Server-migrering**klickar du på **Replikera servrar**.

    ![Servrarna replikeras](./media/contoso-migration-rehost-linux-vm/replicating-servers.png)

2. I **Replikera datorer** högerklickar du på den virtuella datorn > **Migrera**.
3. I **Migrera** > **Stäng av virtuella datorer och utför en planerad migrering utan dataförlust** väljer du **Ja** > **OK**.
    - Som standard stänger Azure Migrate av den lokala virtuella datorn och kör en replikering på begäran som synkroniserar eventuella VM-ändringar som har inträffat sedan den senaste replikeringen utfördes. Detta säkerställer att ingen dataförlust sker.
    - Om du inte vill stänga av den virtuella datorn väljer du **Nej**
4. Ett migreringsjobb startas för den virtuella datorn. Spåra jobbet i Azure-meddelanden.
5. När jobbet är klart kan du se och hantera den virtuella datorn på sidan **Virtual Machines**.

### <a name="connect-the-vm-to-the-database"></a>Ansluta den virtuella datorn till databasen

Som sista steg i migreringsprocessen uppdaterar Contosos administratörer programmets anslutningssträng så att den pekar på programdatabasen som körs på den virtuella datorn **OSTICKETMYSQL**.

1. De skapar en SSH-anslutning till den virtuella datorn **OSTICKETWEB** med hjälp av Putty eller en annan SSH-klient. Eftersom den virtuella datorn är privat ansluter de med hjälp av den privata IP-adressen.

    ![Ansluta till databasen](./media/contoso-migration-rehost-linux-vm/db-connect.png)

    ![Ansluta till databasen](./media/contoso-migration-rehost-linux-vm/db-connect2.png)

2. De måste se till att den virtuella datorn **OSTICKETWEB** kan kommunicera med den virtuella datorn **OSTICKETMYSQL**. Konfigurationen är för närvarande hårdkodad med den lokala IP-adressen 172.16.0.43.

    **Före uppdateringen:**

    ![Uppdatera IP-adressen](./media/contoso-migration-rehost-linux-vm/update-ip1.png)

    **Efter uppdateringen:**

    ![Uppdatera IP-adressen](./media/contoso-migration-rehost-linux-vm/update-ip2.png)

3. De startar om tjänsten med **systemctl restart apache2**.

    ![Starta om](./media/contoso-migration-rehost-linux-vm/restart.png)

4. Slutligen uppdaterar de DNS-posterna för **OSTICKETWEB** och **OSTICKETMYSQL** på en av Contosos domänkontrollanter.

    ![Uppdatera DNS](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

    ![Uppdatera DNS](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

**Behöver du mer hjälp?**

- [Lär dig](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#run-a-test-migration) hur du kör ett redundanstest.
- [Läs mer](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#migrate-vms) om migrering av virtuella datorer till Azure.

## <a name="clean-up-after-migration"></a>Rensa efter migrering

När migreringen är klar körs osTicket-appens nivåer på virtuella Azure-datorer.

Contoso måste rensa upp följande:

- Ta bort de lokala virtuella datorerna från vCenter-lagret.
- Ta bort de lokala virtuella datorerna från lokala säkerhetskopieringsjobb.
- Uppdatera den interna dokumentationen med den nya platsen och IP-adresserna för OSTICKETWEB och OSTICKETMYSQL.
- Granska alla resurser som interagerar med de virtuella datorerna och uppdatera alla relevanta inställningar eller dokumentation så att de överensstämmer med den nya konfigurationen.
- Contoso använde tjänsten Azure Migrate med beroendemappning för att utvärdera de virtuella datorerna för migrering. Administratörer bör ta bort Microsoft Monitoring Agent och Microsofts beroende agent som de har installerat för detta ändamål från den virtuella datorn.

## <a name="review-the-deployment"></a>Granska distributionen

Nu när appen körs måste Contoso operationalisera och säkra den nya infrastrukturen.

### <a name="security"></a>Säkerhet

Contosos säkerhetsteam granskar de virtuella datorerna OSTICKETWEB och OSTICKETMYSQL för att identifiera eventuella säkerhetsproblem.

- Teamet granskar nätverkssäkerhetsgrupperna (NSG:er) för de virtuella datorerna för åtkomstkontroll. Nätverkssäkerhetsgrupper används för att säkerställa att endast trafik som tillåts för programmet kan passera.
- Teamet överväger också att skydda data på de virtuella datordiskarna med diskkryptering och Azure Key Vault.

Mer information finns i [rekommenderade säkerhets metoder för IaaS-arbetsbelastningar i Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

### <a name="bcdr"></a>Affärskontinuitet och haveriberedskap

För affärskontinuitet och haveriberedskap vidtar Contoso följande åtgärder:

- **Skydda data.** Contoso säkerhetskopierar data på de virtuella datorerna med hjälp av Azure Backup-tjänsten. [Läs mer](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
- **Undvika avbrott i apparna.** Contoso replikerar de virtuella datorerna för appen i Azure till en sekundär region med hjälp av Site Recovery. [Läs mer](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Licensierings- och kostnadsoptimering

- När de har distribuerat resurser tilldelar Contoso Azure-taggar på det sätt som definierades när [Azure-infrastrukturen distribuerades](./contoso-migration-infrastructure.md#set-up-tagging).
- Contoso har inga licensproblem med Ubuntu-servrarna.
- Contoso aktiverar Azure Cost Management som licensieras av Cloudyn, ett Microsoft-dotterbolag. Det är en kostnadshanteringslösning med flera moln som hjälper dig att använda och hantera Azure och andra molnresurser. [Läs mer](https://docs.microsoft.com/azure/cost-management/overview) om Azure Cost Management.
