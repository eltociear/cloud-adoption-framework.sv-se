---
title: Utvärdera lokala arbetsbelastningar för migrering till Azure
description: Läs om hur Contoso utvärderar sina lokala datorer inför migrering till Azure genom att använda Azure Migrate och Data Migration Assistant.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 78d33031879a49bd70a6dcfb01be604ca4371e49
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78228423"
---
<!-- cSpell:ignore WEBVM SQLVM OSTICKETWEB OSTICKETMYSQL CONTOSODC contosohost vcenter prereqs ctypes ctypeslib smarthotelapp -->

# <a name="assess-on-premises-workloads-for-migration-to-azure"></a>Utvärdera lokala arbetsbelastningar för migrering till Azure

Den här artikeln visar hur det fiktiva företaget Contoso utvärderar en lokal app inför migrering till Azure. I exempelscenariot körs Contosos lokala app SmartHotel360 på VMware. Contoso utvärderar virtuella appdatorer med hjälp av Azure Migrate-tjänsten och SQL Server-appdatabasen med hjälp av Data Migration Assistant.

## <a name="overview"></a>Översikt

När Contoso överväger att migrera till Azure behöver företaget en teknisk och ekonomisk utvärdering för att avgöra om dess lokala arbetsbelastningar är lämpliga kandidater för migrering till molnet. Contoso-teamet vill särskilt bedöma dator- och databaskompatibiliteten för migrering. De vill uppskatta kapaciteten och kostnaderna för att köra Contosos resurser i Azure.

För att komma igång och bättre förstå tekniken som ska användas utvärderar Contoso två av sina lokala appar, som sammanfattas i följande tabell. Företaget utför utvärderingen för migreringsscenarier som byter värd och omstrukturerar apparna. Läs mer om hur du byter värd och omstrukturerar i [översikten för migreringsexempel](../migrate/azure-best-practices/contoso-migration-overview.md).

<!-- markdownlint-disable MD033 -->

Appnamn | Plattform | Appnivåer | Detaljer
--- | --- | --- | ---
SmartHotel360<br/><br/> (hanterar Contosos resebehov) | Körs i Windows med en SQL Server-databas | App med två nivåer. ASP.NET.webbplats för klientdelen som körs på en virtuell dator (**WEBVM**) och en SQL Server som körs på en annan virtuell dator (**SQLVM**). | De virtuella datorerna är VMware som körs på en ESXi-värd som hanteras av vCenter Server.<br/><br/> Du kan hämta exempelappen från [GitHub](https://github.com/Microsoft/SmartHotel360).
osTicket<br/><br/> (Contosos supportapp) | Körs på Linux/Apache med MySQL PHP (LAMP) | App med två nivåer. Klientdelen körs på en PHO-webbplats på en virtuell dator **(OSTICKETWEB)** och MySQL-databasen körs på en annan virtuell dator (**OSTICKETMYSQL**). | Appen används av kundtjänstappar för att spåra problem för medarbetare och kunder.<br/><br/> Du kan hämta exemplet från [GitHub](https://github.com/osTicket/osTicket).

<!-- markdownlint-enable MD033 -->

## <a name="current-architecture"></a>Nuvarande arkitektur

Här är ett diagram som visar Contosos aktuella lokala infrastruktur:

![Nuvarande Contoso-arkitektur](../migrate/azure-best-practices/media/contoso-migration-assessment/contoso-architecture.png)

- Contoso har ett huvuddatacenter. Datacentret finns i New York i östra USA.
- Contoso har ytterligare tre lokala avdelningar i USA.
- Huvuddatacentret är anslutet till Internet med en Metro Ethernet-anslutning för fiber (500 Mbit/s).
- Varje avdelning ansluts lokalt till Internet med hjälp av anslutningar i företagsklass med IPsec VPN-tunnlar tillbaka till huvuddatacentret. Konfigurationen innebär att Contosos hela nätverk är permanent anslutet och optimerar Internet-anslutningen.
- Huvuddatacentret är helt virtualiserat med VMware. Contoso har två ESXi 6.5-virtualiseringsvärdar som hanteras av vCenter Server 6.5.
- Contoso använder Active Directory Domain Services för identitetshantering. Contoso använder DNS-servrar i det interna nätverket.
- Domänkontrollanterna i datacentret körs på virtuella VMware-datorer. Domänkontrollanterna på de lokala avdelningarna körs på fysiska servrar.

## <a name="business-drivers"></a>Affärsdrivande faktorer

Contosos IT-ledningsgrupp har arbetat tillsammans med företagets affärspartners för att förstå vad företaget vill uppnå med migreringen:

- **Hantera företagets tillväxt.** Contoso växer. Det innebär att trycket har ökat på företagets lokala system och infrastruktur.
- **Öka effektiviteten.** Contoso måste ta bort onödiga procedurer och effektivisera processer för utvecklare och användare. Företaget kräver att IT-systemen är snabba och inte slösar tid eller pengar, så att företaget kan agera snabbare på kundernas önskemål.
- **Öka flexibiliteten.** Contosos IT-avdelning måste reagera snabbare på företagets behov. Det måste reagera snabbare än de ändringar som uppstår på marknaden för att företaget ska kunna lyckas i en global ekonomi. IT-verksamheten på Contoso får inte stå i vägen eller förhindra verksamhetens utveckling.
- **Skala.** När företagets verksamhet växer måste Contosos IT-avdelning förse företaget med system som kan växa i samma takt.

## <a name="assessment-goals"></a>Utvärderingsmål

Contosos molnteam har identifierat mål för den här migreringsutvärderingen:

- Efter migreringen ska appen i Azure ha samma prestandafunktioner som appen har i dag i Contosos lokala VMware-miljö. Övergången till molnet innebär inte att appens prestanda är mindre viktig.
- Contoso måste avgöra om deras program och databaser är kompatibla med Azure-krav. Contoso måste också förstå sina värdalternativ i Azure.
- Contosos databasadministration bör vara mindre efter att apparna har flyttats till molnet.
- Contoso vill inte bara förstå migreringsalternativen utan även infrastrukturskostnaderna efter flytten till molnet.

## <a name="assessment-tools"></a>Utvärderingsverktyg

Contoso använder Microsoft-verktyg för sin migreringsutvärdering. Verktygen är anpassade till med företagets mål och bör ge Contoso all information som krävs.

Teknologi | Beskrivning | Kostnad
--- | --- | ---
[Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Contoso kommer att använda Data Migration Assistant för att utvärdera och identifiera kompatibilitetsproblem som kan påverka deras databasfunktioner i Azure. Data Migration Assistant utvärderar funktionspariteten mellan SQL-källor och -mål. Det rekommenderar förbättringar för prestanda och tillförlitlighet. | Data Migration Assistant är ett kostnadsfritt nedladdningsbart verktyg.
[Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-overview) | Contoso använder tjänsten Azure Migrate för att utvärdera sina virtuella VMware-datorer. Azure Migrate bedömer datorernas lämplighet för migrering. Den ger storleks- och kostnadsuppskattningar för körning i Azure. | Från och med maj 2018 är Azure Migrate en kostnadsfri tjänst.
[Tjänstkarta](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-service-map) | Azure Migrate använder Tjänstkarta för att visa beroenden mellan datorer som ska migreras. | Tjänstkarta är en del av Azure Monitor-loggarna. Contoso kan för närvarande använda Tjänstkarta i 180 dagar utan att debiteras.

I det här scenariot laddar Contoso ned och kör Data Migration Assistant för att utvärdera den lokala SQL Server-databasen för sin reseapp. Contoso använder Azure Migrate med beroendemappning för att utvärdera de virtuella datorerna för appen innan de migrerar dem till Azure.

## <a name="assessment-architecture"></a>Utvärderingsarkitektur

![Arkitektur för migreringsutvärdering](../migrate/azure-best-practices/media/contoso-migration-assessment/migration-assessment-architecture.png)

- Contoso är ett fiktivt namn som representerar en typisk företagsorganisation.
- Contoso har ett lokalt datacenter (**contoso-datacenter**) med lokala domänkontrollanter (**CONTOSODC1**, **CONTOSODC2**).
- De virtuella VMware-datorerna finns på VMware ESXi-värdar som kör version 6.5 (**contosohost1.** , **contosohost2**).
- VMware-miljön hanteras av vCenter Server 6.5 (**vcenter.contoso.com**) som körs på en virtuell dator.
- SmartHotel360 Travel-appen har följande egenskaper:
  - Appen är nivåindelad på två virtuella VMware datorer (**WEBVM** och **SQLVM**).
  - De virtuella datorerna finns på VMware ESXi-värden **contosohost1.contoso.com**.
  - De virtuella datorerna kör Windows Server 2008 R2 Data Center med SP1.
- VMware-miljön hanteras av vCenter Server (**vcenter.contoso.com**) som körs på en virtuell dator.
- OsTicket Service Desk-appen:
  - Appen är indelad i nivåer på två virtuella datorer (**OSTICKETWEB** och **OSTICKETMYSQL**).
  - De virtuella datorerna kör Ubuntu Linux server 16.04-LTS.
  - **OSTICKETWEB** kör Apache 2 och php 7.0.
  - **OSTICKETMYSQL** kör MySQL 5.7.22.

## <a name="prerequisites"></a>Förutsättningar

Contoso och andra användare måste uppfylla följande krav för utvärderingen:

- Ägar- eller deltagarbehörigheter för Azure-prenumerationen eller för en resursgrupp i Azure-prenumerationen.
- En lokal vCenter Server-instans som kör version 6.5, 6.0 eller 5.5.
- Ett skrivskyddat konto i vCenter Server eller behörighet att skapa ett sådant.
- Behörighet att skapa en virtuell dator på vCenter Server-instans med hjälp av en .ova-mall.
- Minst en ESXi-värd som kör version 5.5 eller senare.
- Minst två lokala virtuella VMware-datorer, varav en kör en SQL Server-databas.
- Behörighet att installera Azure Migrate-agenter på varje virtuell dator.
- De virtuella datorerna ska ha direkt Internetanslutning.
  - Du kan begränsa Internetåtkomsten till [de URL:er som krävs](https://docs.microsoft.com/azure/migrate/concepts-collector).
  - Om de virtuella datorerna inte har någon Internetanslutning måste Azure [Log Analytics Gateway](https://docs.microsoft.com/azure/azure-monitor/platform/gateway) installeras på dem och agenttrafiken dirigeras genom den.
- Det fullständigt kvalificerade domän namnet (FQDN) för den virtuella dator som kör SQL Server-instansen för databas utvärdering.
- Windows-brandväggen som körs på den virtuella SQL Server-datorn ska tillåta externa anslutningar på TCP-port 1433 (standard). Med den här konfigurationen kan Data Migration Assistant ansluta.

## <a name="assessment-overview"></a>Utvärderingsöversikt

Så här utför Contoso utvärderingen:

> [!div class="checklist"]
>
> - **Steg 1: Ladda ned och installera Data Migration Assistant.** Contoso förbereder Data Migration Assistant för utvärdering av den lokala SQL Server-databasen.
> - **Steg 2: utvärdera databasen med hjälp av Data Migration Assistant.** Contoso kör och analyserar databasutvärderingen.
> - **Steg 3: Förbered för utvärdering av virtuella datorer med hjälp av Azure Migrate.** Contoso konfigurerar lokala konton och justerar VMware-inställningar.
> - **Steg 4: identifiera lokala virtuella datorer med hjälp av Azure Migrate.** Contoso skapar en virtuell dator för Azure Migrate Collector. Contoso kör sedan insamlaren (Collector) för att identifiera virtuella datorer för utvärdering.
> - **Steg 5: förbereda för beroende analys med hjälp av Azure Migrate.** Contoso installerar Azure Migrate-agenter på de virtuella datorerna så att företaget kan se beroendemappningen mellan virtuella datorer.
> - **Steg 6: utvärdera de virtuella datorerna med hjälp av Azure Migrate.** Contoso kontrollerar beroenden, grupperar de virtuella datorerna och kör utvärderingen. När utvärderingen är klar analyserar Contoso den för att förbereda inför migreringen.

    > [!NOTE]
    > Assessments shouldn't just be limited to using tooling to discover information about your environment, you should schedule in time to speak to business owners, end users, other members within the IT department, etc in order to get a full picture of what is happening within the environment and understand things tooling cannot tell you. 

## <a name="step-1-download-and-install-data-migration-assistant"></a>Steg 1: Ladda ned och installera Data Migration Assistant

1. Contoso laddar ned Data Migration Assistant från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595).
    - Data Migration Assistant kan installeras på vilken dator som helst som kan ansluta till SQL Server-instansen. Contoso behöver inte köra den på SQL Server-datorn.
    - Data Migration Assistant bör inte köras på SQL Server-värddatorn.
2. Contoso kör den hämtade installationsfilen (DownloadMigrationAssistant.msi) för att starta installationen.
3. På sidan **Slutför** väljer Contoso **Starta Microsoft Data Migration Assistant** innan de avslutar guiden.

## <a name="step-2-run-and-analyze-the-database-assessment-for-smarthotel360"></a>Steg 2: köra och analysera databas utvärderingen för SmartHotel360

Contoso kan nu köra en utvärdering för att analysera den lokala SQL Server-databasen för SmartHotel360-appen.

1. I Data Migration Assistant väljer Contoso **Ny** > **Utvärdering** och ger sedan utvärderingen ett projektnamn.
2. För **Källservertyp** väljer Contoso **SQL Server** och för **Målservertyp** väljer Contoso **SQL Server på Azure Virtual Machines**

    ![Data Migration Assistant – Välj källa](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-1.png)

    > [!NOTE]
    > För närvarande stöder Data Migration Assistant inte utvärdering för migrering till en hanterad Azure SQL-databasinstans. Som en tillfällig lösning använder Contoso SQL Server på en virtuell Azure-dator som mål för utvärderingen.

3. I **Välj målversion** väljer Contoso SQL Server 2017 som målversion. Contoso måste välja den här versionen eftersom versionen används av den hanterade SQL-databasinstansen.
4. Contoso väljer rapporter som hjälp för att identifiera information om kompatibilitet och nya funktioner:
    - **Kompatibilitetsproblem** anger ändringar som kan bryta migreringen eller som kräver en mindre justering före migreringen. Den här rapporten informerar Contoso om funktioner som används för närvarande och som är föråldrade. Problemen ordnas efter kompatibilitetsnivå.
    - **Nya funktionsrekommendation** informerar om nya funktioner i SQL Server-målplattformen som kan användas för databasen efter migreringen. Nya funktionsrekommendationer ordnas enligt rubrikerna **Prestanda**, **Säkerhet** och **Lagring**.

    ![Data Migration Assistant – Kompatibilitetsproblem och nya funktioner](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-2.png)

5. I **Anslut till en server** anger Contoso namnet på den virtuella dator som kör databasen och autentiseringsuppgifterna för att komma åt den. Contoso väljer **Ha förtroende för servercertifikat** för att se till att den virtuella datorn har åtkomst till SQL Server. Sedan väljer Contoso **Anslut**.

    ![Data Migration Assistant – Anslut till en server](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-3.png)

6. I **Lägg till** lägger Contoso till databasen som de vill utvärdera och väljer sedan **Nästa** för att starta utvärderingen.
7. Utvärderingen skapas.

    ![Data Migration Assistant – Skapa utvärdering](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-4.png)

8. I **Granska resultat** visar Contoso utvärderingsresultaten.

### <a name="analyze-the-database-assessment"></a>Analysera databasutvärderingen

Resultatet visas när de är tillgängliga. Om Contoso åtgärdar problemen måste de välja **Starta om utvärdering** för att köra utvärderingen igen.

1. I rapporten **Kompatibilitetsproblem** kontrollerar Contoso om det finns några problem på varje kompatibilitetsnivå. Kompatibilitetsnivåerna mappar till SQL Server-versioner på följande sätt:

    - 100: SQL Server 2008/Azure SQL Database
    - 110: SQL Server 2012/Azure SQL Database
    - 120: SQL Server 2014/Azure SQL Database
    - 130: SQL Server 2016/Azure SQL Database
    - 140: SQL Server 2017/Azure SQL Database

    ![Data Migration Assistant – Kompatibilitetsproblemrapport](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-5.png)

2. I rapporten **Funktionsrekommendationer** visas prestanda-, säkerhets- och lagringsfunktioner som utvärderingen rekommenderar att Contoso bör konfigurera efter migreringen. En rad olika funktioner rekommenderas, till exempel minnesintern OLTP, Columnstore-index, Stretch Database, alltid krypterad, dynamisk datamaskering och transparent datakryptering.

    ![Data Migration Assistant – rapporten funktionsrekommendationer](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-6.png)

    > [!NOTE]
    > Contoso bör [aktivera transparent datakryptering](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption?view=sql-server-2017) för alla SQL Server-databaser. Detta är ännu viktigare när en databas befinner sig i molnet än när den finns lokalt. Transparent datakryptering bör endast aktiveras efter migrering. Om transparent datakryptering redan har aktiverats måste Contoso flytta certifikatet eller den asymmetriska nyckeln till huvuddatabasen på målservern. Lär dig hur [du flyttar en transparent data krypteringsdatabas till en annan SQL Server-instans](https://docs.microsoft.com/sql/relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server?view=sql-server-2017).

3. Contoso kan exportera utvärderingen i JSON-eller CSV-format.

> [!NOTE]
> För storskaliga utvärderingar:
>
> - Kör flera utvärderingar samtidigt och se tillståndet för utvärderingarna genom att öppna sidan **Alla utvärderingar**.
> - Konsolidera utvärderingarna till en [SQL Server-databas](https://docs.microsoft.com/sql/dma/dma-consolidatereports?view=ssdt-18vs2017).
> - Konsolidera utvärderingarna till en [PowerBI-rapport](https://docs.microsoft.com/sql/dma/dma-powerbiassesreport?view=ssdt-18vs2017).

## <a name="step-3-prepare-for-vm-assessment-by-using-azure-migrate"></a>Steg 3: Förbered för utvärdering av virtuella datorer med hjälp av Azure Migrate

Contoso måste skapa ett VMware-konto som ska användas i Azure Migrate för att automatiskt identifiera virtuella datorer för utvärdering, kontrollera att de har behörighet att skapa en virtuell dator, observera portarna som måste vara öppna och ange nivå för statistikinställningar.

### <a name="set-up-a-vmware-account"></a>Konfigurera ett VMware-konto

Identifiering av virtuella datorer kräver ett skrivskyddat konto i vCenter Server som har följande egenskaper:

- **Användar typ:** Minst en skrivskyddad användare.
- **Behörigheter:** För datacenter-objektet markerar du kryss rutan **Sprid till underordnade objekt** . För **Roll**väljer du **Skrivskyddad**.
- **Information:** Användaren tilldelas på data center nivå med åtkomst till alla objekt i data centret.
- Om du vill begränsa åtkomsten tilldelar du rollen **Ingen åtkomst** med objektet **Sprid till underordnat** objekt till underordnade objekt (vSphere-värdar, data lager, virtuella datorer och nätverk).

### <a name="verify-permissions-to-create-a-vm"></a>Kontrollera behörigheter för att skapa en virtuell dator

Contoso kontrollerar att de har behörighet att skapa en virtuell dator genom att importera en fil i .ova-format. Lär dig att [skapa och tilldela en roll med behörigheter](https://kb.vmware.com/s/article/1023189?other.KM_Utility.getArticleLanguage=1&r=2&other.KM_Utility.getArticleData=1&other.KM_Utility.getArticle=1&ui-comm-runtime-components-aura-components-siteforce-qb.Quarterback.validateRoute=1&other.KM_Utility.getGUser=1).

### <a name="verify-ports"></a>Kontrollera portar

Contoso-utvärderingen använder beroendemappning. Beroendemappning kräver att en agent installeras på de virtuella datorer som ska utvärderas. Agenten måste kunna ansluta till Azure från TCP-port 443 på varje virtuell dator. Läs mer om [anslutningskraven](https://docs.microsoft.com/azure/log-analytics/log-analytics-concept-hybrid).

## <a name="step-4-discover-vms"></a>Steg 4: identifiera virtuella datorer

Contoso skapar ett Azure Migrate-projekt för att identifiera virtuella datorer. Contoso laddar ned och konfigurerar den virtuella datorn för insamlaren. Contoso kör sedan insamlaren (Collector) för att identifiera sina lokala virtuella datorer.

### <a name="create-a-project"></a>Skapa ett projekt

Konfigurera ett nytt Azure Migrate-projekt enligt följande.

1. I Azure-portalen > **Alla tjänster** söker du efter **Azure Migrate**.

1. Under **Tjänster** väljer du **Azure Migrate**.

1. I **Översikt**, under **Upptäck, utvärdera och migrera servrar**, väljer du **utvärdera och migrera servrar**.

    ![Azure Migrate – Skapa migreringsprojekt](../migrate/azure-best-practices/media/contoso-migration-assessment/assess-migrate.png)

1. I **komma igång**väljer du **Lägg till verktyg**.

1. I **Migrera projekt** väljer du din Azure-prenumeration och skapar en resursgrupp om du inte har någon.

1. I **Projektinformation* anger du projektnamnet och geografin där du vill skapa projektet. USA, Asien, Europa, Australien, Storbritannien, Kanada, Indien och Japan stöds.

    - Projektgeografin används bara för att lagra de metadata som samlas in från lokala virtuella datorer.
    - Du kan välja vilken målregion du vill när du kör en migrering.

1. Välj **Nästa**.

1. I **Välj bedömnings verktyg**väljer du **Azure Migrate: Server utvärdering** > **Nästa**.

    ![Azure Migrate – Utvärderingsverktyg](../migrate/azure-best-practices/media/contoso-migration-assessment/assessment-tool.png)

1. I **Välj migreringsverktyg** väljer du **Hoppa över att lägga till ett migreringsverktyg just nu** > **Nästa**.

1. I **Granska + Lägg till verktyg**granskar du inställningarna och väljer sedan **Lägg till verktyg**.

1. Vänta några minuter tills Azure Migrate-projektet har distribuerats. Projektsidan öppnas. Om du inte ser projektet kan du öppna det från **Servrar** i Azure Migrate-instrumentpanelen.

### <a name="download-the-collector-appliance"></a>Hämta insamlingsprogrammet

1. I **mål för migrering** > **servrar** > **Azure Migrate: Server utvärdering**, Välj **identifiera**.

1. I **identifiera datorer** > **dina datorer virtualiserade? väljer du** **Ja, med VMware vSphere hypervisor**.

1. Välj **Ladda ned** för att ladda ned. Filer för embryo-mall.

     ![Azure Migrate – Ladda ned insamlare](../migrate/azure-best-practices/media/contoso-migration-assessment/download-ova-v2.png)

### <a name="verify-the-collector-appliance"></a>Kontrollera insamlingsprogrammet

Innan de distribuerar den virtuella datorn kontrollerar Contoso att den OVA-filen är säker:

1. På den dator där filen hämtades öppnar Contoso ett administratörsfönster i kommandotolken.

1. Contoso kör följande kommando för att generera en hash för OVA-filen:

    `C:\>CertUtil -HashFile <file_location> [Hashing Algorithm]`

    **Exempel:**

    `C:\>CertUtil -HashFile C:\AzureMigrate\AzureMigrate.ova SHA256`

1. Den genererade hashen ska matcha de hash-värden som anges i avsnittet [Verifiera säkerhet](https://docs.microsoft.com/azure/migrate/tutorial-assess-vmware#verify-security) i själv studie kursen [för att utvärdera VMware-datorer för migrering](https://docs.microsoft.com/azure/migrate/tutorial-assess-vmware) .

### <a name="create-the-collector-appliance"></a>Skapa insamlingsprogrammet

Contoso kan nu importera den nedladdade filen till vCenter Server-instansen och etablera den virtuella datorn för insamlingsenheten:

1. I vSphere-klientkonsolen klickar Contoso på **Arkiv** > **Distribuera OVF-mall**.

    ![vSphere-webbklient – Distribuera OVF-mall](../migrate/azure-best-practices/media/contoso-migration-assessment/vcenter-wizard.png)

1. I guiden Distribuera OVF-mall väljer Contoso **Källa** och anger platsen för OVA-filen.

1. I **Namn och plats**anger Contoso ett Visningsnamn för den virtuella datorn för insamlaren. Sedan väljer den en lagerplats som ska vara värd för den virtuella datorn. Contoso anger också den värd eller det kluster som insamlingsprogrammet ska köras i.

1. I **Lagring** anger Contoso en lagringsplats. I **Diskformat** väljer Contoso hur de vill etablera lagringen.

1. I **Nätverksmappning** anger Contoso det nätverk som den virtuella insamlade datorn ska ansluta till. Nätverket måste ha en Internetanslutning för att kunna skicka metadata till Azure.

1. Contoso kontrollerar inställningarna och väljer sedan **Stäng av när distributionen är slutförd** > **Avsluta**. Ett meddelande som bekräftar att det är klart visas när insamlingsprogrammet har skapats.

### <a name="run-the-collector-to-discover-vms"></a>Kör insamlaren för att identifiera virtuella datorer

Contoso kör sedan insamlaren (Collector) för att identifiera virtuella datorer. Insamlaren har endast stöd för **Engelska (USA)** som operativsystemspråk och gränssnittsspråk i insamlaren.

1. I vSphere-klientkonsolen klickar Contoso på **Öppna konsolen**. Contoso godkänner licensvillkoren och lösenordsinställningarna för den virtuella insamlardatorn.

1. På skrivbordet väljer Contoso genvägen **Microsoft Azure-utrustning Configuration Manager**.

    ![vSphere klientkonsol – genväg till insamlare](../migrate/azure-best-practices/media/contoso-migration-assessment/collector-shortcut-v2.png)

1. I Azure Migrate Collector öppnar Contoso **Konfigurera förhandskrav**. Contoso accepterar licensvillkoren och läser informationen från tredje part.

1. Insamlaren kontrollerar att den virtuella datorn är ansluten till internet, att tiden synkroniseras, att insamlartjänsten körs. (Insamlings tjänsten installeras som standard på den virtuella datorn.) Contoso installerar även VMware vSphere Virtual Disk Development Kit.

    > [!NOTE]
    > Vi förutsätter att den virtuella datorn har direkt åtkomst till Internet, utan proxy.

    ![Azure Migrate Collector – Verifiera förutsättningar](../migrate/azure-best-practices/media/contoso-migration-assessment/collector-verify-prereqs-v2.png)

1. Logga in på ditt **Azure**-konto och välj den prenumeration och det migreringsprojekt som du skapade tidigare. Ange ett namn på **enheten** så att du kan identifiera den i Azure Portal.
1. I **Ange vCenter Server-information** anger Contoso namnet (FQDN) eller IP-adressen för vCenter Server-instansen och de skrivskyddade autentiseringsuppgifterna som används för identifiering.
1. Contoso väljer ett omfång för identifiering av virtuella datorer. Insamlaren kan bara identifiera virtuella datorer i angivet omfång. Omfånget kan anges till en viss mapp, ett datacenter eller ett kluster.

    ![Ange vCenter Server-information](../migrate/azure-best-practices/media/contoso-migration-assessment/collector-connect-vcenter.png)

1. Insamlaren börjar att identifiera och samla in information om Contoso-miljön.

    ![Visa insamlingsförloppet](../migrate/azure-best-practices/media/contoso-migration-assessment/migrate-discovery.png)

### <a name="verify-vms-in-the-portal"></a>Verifiera virtuella datorer i portalen

När insamlingen är färdig kontrollerar Contoso att de virtuella datorerna visas i portalen:

1. I Azure Migrate-projektet väljer Contoso **Servrar** > **Identifierade servrar**. Contoso kontrollerar att de virtuella datorerna de vill identifiera visas.

    ![Azure Migrate – Identifierade datorer](../migrate/azure-best-practices/media/contoso-migration-assessment/discovery-complete.png)

1. Observera att Azure Migrate-agenter inte är installerade på datorerna för närvarande. Contoso måste installera agenterna för att kunna visa beroenden.

    ![Azure Migrate – agentinstallation krävs](../migrate/azure-best-practices/media/contoso-migration-assessment/machines-no-agent.png)

## <a name="step-5-prepare-for-dependency-analysis"></a>Steg 5: förbereda för beroende analys

För att visa beroenden mellan de virtuella datorer som det vill utvärdera, hämtar och installerar Contoso agenter på appens virtuella datorer. Contoso installerar agenter på alla virtuella datorer för dess appar, både för Windows och Linux.

### <a name="take-a-snapshot"></a>Ta en ögonblicksbild

För att behålla en kopia av de virtuella datorerna innan de ändrar dem tar Contoso en ögonblicksbild innan agenterna installeras.

![Ögonblicksbild av dator](../migrate/azure-best-practices/media/contoso-migration-assessment/snapshot-vm.png)

### <a name="download-and-install-the-vm-agents"></a>Hämta och installera VM-agenterna

1. I **Datorer**väljer Contoso datorn. I kolumnen **Beroenden** väljer Contoso **Kräver installation**.

1. Följ panelen **Identifiera datorer** gör Contoso följande:
    - Laddar ned Microsoft Monitoring Agent (MMA) och Microsofts beroende agent för varje virtuell Windows-dator.
    - Laddar ned MMA och beroende agent för varje virtuell Linux-dator.

1. Contoso kopierar arbetsytans ID och nyckel. Contoso måste ha arbetsytans ID och nyckel när MMA installeras.

    ![Hämning av agent](../migrate/azure-best-practices/media/contoso-migration-assessment/download-agents.png)

### <a name="install-the-agents-on-windows-vms"></a>Installera agenterna på virtuella Windows-datorer

Contoso kör installationen på varje virtuell dator.

#### <a name="install-the-mma-on-windows-vms"></a>Installera MMA på virtuella Windows-datorer

1. Contoso klickar på den hämtade agenten.

1. På sidan **Målmapp** behåller Contoso standardinstallationsmappen och väljer **Nästa**.

1. I **Installationsalternativ för Agent** väljer Contoso **Anslut agenten till Azure Log Analytics** > **Nästa**.

    ![Microsoft Monitoring Agent-konfiguration – Alternativ för att konfigurera agent](../migrate/azure-best-practices/media/contoso-migration-assessment/mma-install.png)

1. I **Azure Log Analytic** klistrar Contoso in i arbetsytans ID och nyckel som de kopierade från portalen.

    ![Microsoft Monitoring Agent-konfiguration – Azure-logganalys](../migrate/azure-best-practices/media/contoso-migration-assessment/mma-install2.png)

1. I **Klart att installeras** installerar Contoso MMA.

#### <a name="install-the-dependency-agent-on-windows-vms"></a>Installera beroendeagenten på virtuella Windows-datorer

1. Contoso dubbelklickar på den hämtade beroende agenten.

1. Contoso accepterar licensvillkoren och väntar på att installationen ska slutföras.

    ![Dependency Agent installation – installation](../migrate/azure-best-practices/media/contoso-migration-assessment/dependency-agent.png)

### <a name="install-the-agents-on-linux-vms"></a>Installera agenterna på virtuella Linux-datorer

Contoso kör installationen på varje virtuell dator.

#### <a name="install-the-mma-on-linux-vms"></a>Installera MMA på virtuella Linux-datorer

1. Contoso installerar python ctypes-biblioteket på varje virtuell dator med hjälp av följande kommando:

    `sudo apt-get install python-ctypeslib`

1. Contoso måste köra kommandot för att installera MMA-agenten som rot. För att bli rot kör Contoso följande kommando och anger rotlösenordet:

    `sudo -i`

1. Contoso installerar MMA:

    - Contoso anger arbetsytans ID och nyckel i kommandot.
    - Kommandon är för 64-bitars.
    - Arbetsytans ID och primära nyckel finns i arbetsytan logganalys i Azure Portal. Välj **Inställningar** och sedan **Anslutna källor**.
    - Kör följande kommandon för att ladda ned logganalysagenten, validera kontrollsumman och installera och publicera agenten:

    `wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w 6b7fcaff-7efb-4356-ae06-516cacf5e25d -s k7gAMAw5Bk8pFVUTZKmk2lG4eUciswzWfYLDTxGcD8pcyc4oT8c6ZRgsMy3MmsQSHuSOcmBUsCjoRiG2x9A8Mg==`

#### <a name="install-the-dependency-agent-on-linux-vms"></a>Installera beroendeagenten på virtuella Linux-datorer

När MMA har installerats installerar contoso beroende agenten på virtuella Linux-datorer:

1. Beroende agenten är installerad på Linux-datorer med hjälp av InstallDependencyAgent-Linux64. bin, ett gränssnitts skript som har en självextraherande binärfil. Contoso kör filen med hjälp av sh eller lägger till körningsbehörighet till själva filen.

1. Contoso installerar Linux-beroende agenten som rot:

    `wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin && sudo sh InstallDependencyAgent-Linux64.bin -s`

## <a name="step-6-run-and-analyze-the-vm-assessment"></a>Steg 6: köra och analysera VM-utvärderingen

Contoso kan nu kontrollera datorberoenden och skapa en grupp. Sedan körs utvärderingen för gruppen.

### <a name="verify-dependencies-and-create-a-group"></a>Kontrollera beroenden och skapa en grupp

1. För att avgöra vilka datorer som ska analyseras väljer Contoso **Visa beroenden**.

    ![Azure Migrate – Visa datorberoenden](../migrate/azure-best-practices/media/contoso-migration-assessment/view-machine-dependencies.png)

1. För SQLVM visar beroendekartan följande information:

    - Processgrupper eller processer med aktiva nätverksanslutningar som körs på SQLVM under den angivna tidsperioden (en timme som standard).
    - Inkommande (klient) och utgående (server) TCP-anslutningar till och från alla beroende datorer.
    - Beroende datorer med Azure Migrate-agenter installerade visas som separata rutor.
    - Datorer utan agenter installerade visar information om port och IP-adress.

1. För datorer med en installerad agent (WEBVM) väljer Contoso datorrutan för att visa mer information. Informationen omfattar FQDN, operativsystem och MAC-adress.

    ![Azure Migrate – Visa gruppberoenden](../migrate/azure-best-practices/media/contoso-migration-assessment/sqlvm-dependencies.png)

1. Contoso väljer de virtuella datorerna att lägga till i gruppen (SQLVM och WEBVM). Contoso innehåller `Ctrl` nyckel och klickar för att markera flera virtuella datorer.

1. Contoso väljer **Skapa grupp** och anger sedan ett namn (**smarthotelapp**).

    > [!NOTE]
    > Om du vill visa mer detaljerade beroenden kan du expandera tidsintervallet. Du kan välja en viss varaktighet eller start- och slutdatum.

### <a name="run-an-assessment"></a>Köra en utvärdering

1. I **Grupper** öppnar Contoso gruppen (**smarthotelapp**) och väljer sedan **Skapa utvärdering**.

    ![Azure Migrate – Skapa en utvärdering](../migrate/azure-best-practices/media/contoso-migration-assessment/run-vm-assessment.png)

1. För att visa utvärderingen väljer **Contoso Hantera** > **Utvärderingar**.

Contoso har använt standardutvärderingsinställningarna, men du kan [anpassa inställningarna](https://docs.microsoft.com/azure/migrate/how-to-modify-assessment).

### <a name="analyze-the-vm-assessment"></a>Analysera VM-utvärderingen

En Azure Migrate-utvärdering innehåller information om de lokala virtuella datorerna är kompatibla med Azure eller inte, vad som är rätt VM-storlek för att köra den virtuella datorn i Azure samt de beräknade kostnaderna för Azure per månad.

![Azure Migrate – Utvärderingsrapport](../migrate/azure-best-practices/media/contoso-migration-assessment/assessment-overview.png)

#### <a name="review-confidence-rating"></a>Granska säkerhetsomdöme

![Azure Migrate – Utvärderingsvy](../migrate/azure-best-practices/media/contoso-migration-assessment/assessment-display.png)

En utvärdering har ett säkerhetsomdöme från 1 stjärna till 5 stjärnor (1 stjärna är den lägsta och 5 stjärnor är den högsta).

- Säkerhetsomdömet tilldelas en utvärdering baserat på tillgängligheten av datapunkter som behövs för att beräkna utvärderingen.
- Omdömet hjälper dig att beräkna tillförlitligheten för storleksrekommendationer som tillhandahålls av Azure Migrate.
- Säkerhetsomdömen är användbara när du gör *prestandabaserade storleksändringar*. Azure Migrate har kanske tillräckligt med datapunkter för användsbaserade storleksändringar. När storleksändringar av typen *som lokalt”* utförs är säkerhetsomdömet alltid 5 stjärnor eftersom Azure Migrate har tillgång till alla datapunkter som behövs för att sätta rätt storlek på den virtuella datorn.
- Beroende på procentandelen datapunkter som är tillgängliga tillhandahålls säkerhetsomdömet för utvärderingen:

   Tillgänglighet för datapunkter | Säkerhetsomdöme
   --- | ---
   0 %–20 % | 1 stjärna
   21 %–40 % | 2 stjärnor
   41 %–60 % | 3 stjärnor
   61 %–80 % | 4 stjärnor
   81 %–100 % | 5 stjärnor

#### <a name="verify-azure-readiness"></a>Verifiera Azure-beredskap

![Azure Migrate – Utvärderingsstatus](../migrate/azure-best-practices/media/contoso-migration-assessment/azure-readiness.png)

Utvärderingsrapporten visar den information som sammanfattas i tabellen. Observera att om du vill visa prestandabaserad storleksändring behöver Azure Migrate följande information. Om den här informationen inte kan samlas in kan storleksutvärderingen bli felaktig.

- Användningsdata för CPU och minne.
- Lästa/skrivna IOPS och dataflöden för varje disk som är ansluten till den virtuella datorn.
- Inkommande och utgående information för varje nätverkskort som är anslutet till den virtuella datorn.

<!-- markdownlint-disable MD033 -->

Inställning | Indikation | Detaljer
--- | --- | ---
**Azure-beredskap för virtuell dator** | Anger om den virtuella datorn är klar för migrering. | Möjliga tillstånd:<br/><br/>- Redo för Azure<br/><br/>- Redo på vissa villkor <br/><br/>- Ej redo för Azure<br/><br/>- Beredskap okänd<br/><br/> Om en virtuell dator inte är redo visar Azure Migrate några reparationssteg.
**Storlek på Azure-VM** | För virtuella datorer som är redo tillhandahåller Azure Migrate en rekommendation för storleken på de virtuella Azure-datorerna. | Storleksrekommendationerna beror på utvärderingsegenskaperna:<br/><br/>- Om du använde prestandabaserad storleksändring tas de virtuella datorernas prestandahistorik i beaktande.<br/><br/>- Om du använde *Som lokalt* baseras storleksändringen på storleken på de lokala virtuella datorerna och användningsdata använts inte.
**Föreslaget verktyg** | Eftersom Azure-datorer kör agenterna kan Azure Migrate se processerna som körs på datorn. Den identifierar om datorn är en databasdator.
**Information om virtuell dator** | Den här rapporten visar inställningar för den lokala virtuella datorn, inklusive operativsystem, starttyp, disk och lagringsinformation.

<!-- markdownlint-enable MD033 -->

#### <a name="review-monthly-cost-estimates"></a>Granska uppskattad månadskostnad

Den här vyn visar total beräknings- och lagringskostnad för att köra de virtuella datorerna i Azure. Den visar också information för varje dator.

![Azure Migrate – Azure-kostnader](../migrate/azure-best-practices/media/contoso-migration-assessment/azure-costs.png)

- Kostnadsuppskattningarna beräknas med hjälp av storleksrekommendationer för en dator.
- Uppskattade månatliga kostnader för beräkning och lagring sammanställs för alla virtuella datorer i gruppen.

## <a name="clean-up-after-assessment"></a>Rensa efter utvärdering

- När utvärderingen är klar behåller Contoso Azure Migrate-enheten som ska användas för framtida utvärderingar.
- Contoso stänger av den virtuella VMware-datorn. Contoso kommer att använda den igen när framtida virtuella datorer ska användas.
- Contoso lagrar **Contoso Migration**-projektet i Azure. Projektet är för närvarande distribuerat i **resursgruppen ContosoFailoverRG** i Azure-regionen USA, östra.
- Den virtuella insamlaren har en utvärderingslicens på 180 dagar. Om den här gränsen går ut måste Contoso ladda ned insamlaren och konfigurera den igen.

## <a name="conclusion"></a>Sammanfattning

I det här scenariot utvärderar Contoso sin SmartHotel360 app-databas med hjälp av utvärderingsverktyget för Data Migration. De lokala virtuella datorerna utvärderas med hjälp av tjänsten Azure Migrate. Contoso granskar utvärderingarna för att säkerställa att lokala resurser är klara för migrering till Azure.

## <a name="next-steps"></a>Nästa steg

När Contoso bedömer att arbetsbelastningen är en lämplig kandidat för migrering kan de börja förbereda den lokala infrastrukturen och Azure-infrastrukturen för migrering. Se artikeln [Distribuera Azure-infrastruktur](../migrate/azure-best-practices/contoso-migration-infrastructure.md) i avsnittet om metodtips i Ramverk för molnimplementering för ett exempel på hur Contoso utför dessa processer.
