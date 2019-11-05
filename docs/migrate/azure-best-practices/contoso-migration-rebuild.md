---
title: Lägga till ett lokalt program till Azure Active Directory
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig hur Contoso bygger om en app i Azure med hjälp av Azure App Service, Azure Kubernetes Service, Cosmos DB, Azure Functions och Azure Cognitive Services.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 6a7c27e1c2e4bf0bdf4a4ef9104bf13bf221f4e0
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73566598"
---
# <a name="rebuild-an-on-premises-app-on-azure"></a>Bygga om en lokal app i Azure

Den här artikeln beskriver hur det fiktiva företaget Contoso bygger om en Windows .NET-app med två nivåer som körs på virtuella VMware-datorer som en del av en migrering till Azure. Contoso migrerar appens virtuella dator på klientsidan till en Azure App Service-webbapp. Serverdelen för appen skapas med mikrotjänster som distribueras till containrar som hanteras av Azure Kubernetes Service (AKS). Webbplatsen interagerar med Azure Functions för att tillhandahålla en funktion för bilder på husdjur.

SmartHotel360-appen som används i det här exemplet tillhandahålls som öppen källkod. Om du vill använda den i ett eget test kan du ladda ned den från [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Affärsdrivande faktorer

IT-ledningsgruppen har arbetat tillsammans med affärspartner för att komma fram till vad man vill uppnå med migreringen:

- **Hantera företagets tillväxt.** Contoso växer och vill erbjuda differentierade upplevelser för kunder på Contosos webbplatser.
- **Öka flexibiliteten.** Contoso måste kunna reagera snabbare än förändringarna på marknaden för att företaget ska lyckas i en global ekonomi.
- **Skala.** När företagets verksamhet växer måste Contosos IT-team tillhandahålla system som kan växa i samma takt.
- **Minska kostnaderna.** Contoso vill minimera licenskostnaderna.

## <a name="migration-goals"></a>Migreringsmål

Contosos molnteam har fastställt viktiga appkrav för migreringen. Kraven användes för att komma fram till den lämpligaste migrationsmetoden:

- Appen i Azure är fortfarande lika viktig som den är i dag. Den måste fungera bra och kunna skalas enkelt.
- Appen ska inte använda IaaS-komponenter. Allt ska vara utformat för PaaS eller serverlösa tjänster.
- Alla appbyggen ska köras i molntjänster och containrar ska finnas i ett privat företagsomfattande containerregister i molnet.
- API-tjänsten som används för bilderna på husdjur måste vara relevant och praktiskt tillämpbar eftersom beslut som fattas av appen respekteras av deras hotell. Alla husdjur som godkänns får stanna på hotellen.
- För att uppfylla kraven för en DevOps-pipeline använder Contoso Azure DevOps för källkodshantering, med Git-databaser. Automatiserade byggen och distributioner används för att skapa kod och distribuera till Azure App Service, Azure Functions och AKS.
- Olika CI/CD-pipelines behövs för mikrotjänster på serversidan och för webbplatsen på klientsidan.
- Tjänsterna på serversidan och webbappen på klientsidan har olika versionscykler. För att uppfylla detta krav distribueras två olika DevOps-pipelines.
- Contoso behöver ledningens godkännande för all distribution på klientsidan, vilket CI/CD-pipelinen måste tillhandahålla.

## <a name="solution-design"></a>Lösningsdesign

Efter att ha fastställt målen och kraven kan Contoso utforma och utvärdera en distributionslösning och identifiera migreringsprocessen, inklusive de Azure-tjänster som ska användas för migreringen.

### <a name="current-app"></a>Aktuell app

- Den lokala appen SmartHotel360 delas in i nivåer på två virtuella datorer (WEBVM och SQLVM).
- De virtuella datorerna finns på VMware ESXi-värden **contosohost1.contoso.com** (version 6.5)
- VMware-miljön hanteras av vCenter Server 6.5 (**vcenter.contoso.com**), som körs på en virtuell dator.
- Contoso har ett lokalt datacenter (contoso-datacenter) med en lokal domänkontrollant (**contosodc1**).
- De lokala, virtuella datorerna i Contoso-datacentret kommer att inaktiveras när migreringen är färdig.

### <a name="proposed-architecture"></a>Föreslagen arkitektur

- Klientdelen för appen distribueras som en Azure App Service-webbapp i den primära Azure-regionen.
- En Azure-funktion hanterar uppladdningen av bilder på husdjur, och webbplatsen interagerar med den här funktionen.
- Funktionen för husdjursbilderna använder API:et för Azure Cognitive Services Vision och Cosmos DB.
- Serverdelen för webbplatsen bygger på mikrotjänster. Dessa distribueras till containrar som hanteras i Azure Kubernetes Service (AKS).
- Containrar skapas med Azure DevOps och skickas till Azure Container Registry (ACR).
- Den här gången distribuerar Contoso webbappen och funktionskoden manuellt med hjälp av Visual Studio.
- Mikrotjänster distribueras med hjälp av ett PowerShell-skript som anropar Kubernetes kommandoradsverktyg.

    ![Scenariots arkitektur](./media/contoso-migration-rebuild/architecture.png)

### <a name="solution-review"></a>Lösningsgranskning

Contoso utvärderar den föreslagna designen genom att skapa en lista med för- och nackdelar.

<!-- markdownlint-disable MD033 -->

**Övervägande** | **Detaljer**
--- | ---
**Fördelar** | Användningen av PaaS och serverlösa lösningar för distribution från slutpunkt till slutpunkt minskar avsevärt hanteringstiden för Contoso.<br/><br/> Genom att flytta till en arkitektur för mikrotjänster kan Contoso enkelt utöka lösningen med tiden.<br/><br/> Nya funktioner kan tas online utan att kodbasen för befintliga lösningar påverkas.<br/><br/> Webbappen konfigureras med flera instanser utan någon enskild felpunkt.<br/><br/> Autoskalning aktiveras så att appen kan hantera olika trafikvolymer.<br/><br/> Med flytten till PaaS Services kan Contoso ta bort inaktuella lösningar som körs på Windows Server 2008 R2-operativsystem.<br/><br/> Cosmos DB har inbyggd feltolerans, vilket inte kräver någon konfiguration av Contoso. Detta innebär att datanivån inte längre är en felkritisk systemdel.
**Nackdelar** | Containrar är mer komplexa än andra migreringsalternativ. Inlärningskurvan kan vara ett problem för Contoso. De medför komplexitet på en ny nivå, som ger stort värde trots kurvan.<br/><br/> Driftteamet på Contoso måste lära sig mer om Azure, containrar och mikrotjänster för appen.<br/><br/> Contoso har inte helt implementerat DevOps för hela lösningen. Contoso måste överväga det för distributionen av tjänster till AKS, Azure Functions och Azure App Service.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Migreringsprocessen

1. Contoso etablerar ACR, AKS och Cosmos DB.
2. De etablerar infrastrukturen för distributionen, inklusive webbappen, lagringskontot, funktionen och API:et för Azure App Service.
3. När infrastrukturen är på plats bygger de avbildningar av mikrotjänsternas containrar med hjälp av Azure DevOps, som skickar dem till ACR.
4. Contoso distribuerar dessa mikrotjänster till AKS med hjälp av ett PowerShell-skript.
5. Slutligen distribuerar de funktionen och webbappen.

    ![Migreringsprocessen](./media/contoso-migration-rebuild/migration-process.png)

### <a name="azure-services"></a>Azure-tjänster

**Tjänst** | **Beskrivning** | **Kostnad**
--- | --- | ---
[AKS](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Förenklar hanteringen, distributionen och åtgärderna för Kubernetes. Tillhandahåller en fullständigt hanterad orkestreringstjänst för Kubernetes-containrar. | AKS är en kostnadsfri tjänst. Betala bara för de virtuella datorerna och de associerade lagrings- och nätverksresurser som förbrukas. [Läs mer](https://azure.microsoft.com/pricing/details/kubernetes-service).
[Azure Functions](https://azure.microsoft.com/services/functions) | Utveckla snabbare med en händelsedriven miljö för databearbetning utan server. Skala på begäran. | Betala endast för de resurser du använder. Planen faktureras baserat på resursanvändning och körningar per sekund. [Läs mer](https://azure.microsoft.com/pricing/details/functions).
[Azure Container Registry](https://azure.microsoft.com/services/container-registry) | Lagrar avbildningar för alla typer av containerdistributioner. | Kostnad baserad på funktioner, lagring och användningstid. [Läs mer](https://azure.microsoft.com/pricing/details/container-registry).
[Azure Apptjänst](https://azure.microsoft.com/services/app-service/containers) | Skapa, distribuera och skala snabbt webb-, mobil- och API-appar i företagsklass som körs på valfri plattform. | App Service-planer faktureras per sekund. [Läs mer](https://azure.microsoft.com/pricing/details/app-service/windows).

## <a name="prerequisites"></a>Krav

Det här är vad Contoso behöver i det här scenariot:

<!-- markdownlint-disable MD033 -->

**Krav** | **Detaljer**
--- | ---
**Azure-prenumeration** | Contoso skapade prenumerationer i en tidigare artikel. Om du inte har någon Azure-prenumeration kan du skapa ett [kostnadsfritt konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Om du skapar ett kostnadsfritt konto är du administratör för din prenumeration och kan utföra alla åtgärder.<br/><br/> Om du använder en befintlig prenumeration och inte är administratör måste du be administratören att ge dig ägar- eller deltagarbehörighet.
**Azure-infrastruktur** | [Läs om hur](./contoso-migration-infrastructure.md) Contoso konfigurerar en Azure-infrastruktur.
**Krav för utvecklare** | Contoso behöver följande verktyg på en arbetsstation för utvecklare:<br/><br/> - [Visual Studio 2017 Community Edition: Version 15,5](https://www.visualstudio.com)<br/><br/> .NET-arbetsbelastning aktiverad.<br/><br/> [Git](https://git-scm.com)<br/><br/> [Azure PowerShell](https://azure.microsoft.com/downloads)<br/><br/> [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)<br/><br/> [Docker CE (Windows 10) eller Docker EE (Windows Server)](https://docs.docker.com/docker-for-windows/install) konfigurerat att använda Windows-containrar.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Steg i scenariot

Contoso genomför migreringen på följande sätt:

> [!div class="checklist"]
>
> - **Steg 1: etablera AKS och ACR.** Contoso etablerar det hanterade AKS-klustret och Azure Container Registry med hjälp av PowerShell.
> - **Steg 2: Bygg Docker-behållare.** De konfigurerar CI för Docker-containrar med hjälp av Azure DevOps och push-överför dem till ACR.
> - **Steg 3: Distribuera Server dels mikrotjänster.** De distribuerar resten av infrastrukturen som ska användas av mikrotjänster på serversidan.
> - **Steg 4: Distribuera klient dels infrastruktur.** De distribuerar infrastrukturen på klientsidan, inklusive bloblagring för husdjurbilderna, Cosmos-databasen och API:et för Visuellt innehåll.
> - **Steg 5: Migrera Server delen.** De distribuerar mikrotjänster och använder AKS för att migrera serverdelen.
> - **Steg 6: publicera klient delen.** De publicerar SmartHotel360-appen till App Service, och funktionsappen som ska anropas av husdjurstjänsten.

## <a name="step-1-provision-back-end-resources"></a>Steg 1: etablera Server dels resurser

Contosos administratörer kör ett distributionsskript för att skapa det hanterade Kubernetes-klustret med AKS och ACR (Azure Container Registry).

- I anvisningarna i det här avsnittet används lagringsplatsen **SmartHotel360-Azure-backend**.
- GitHub-lagringsplatsen **SmartHotel360-Azure-backend** innehåller all programvara för den här delen av distributionen.  

### <a name="prerequisites"></a>Krav

1. Innan de börjar ser contoso-administratörer till att all nödvändig program vara installeras på den utvecklings dator som de använder för distributionen.
2. De klonar lagringsplatsen lokalt till utvecklingsdatorn med Git: `git clone https://github.com/Microsoft/SmartHotel360-Azure-backend.git`

### <a name="provision-aks-and-acr"></a>Etablera AKS och ACR

Contosos administratörer etablerar enligt följande:

1. de öppnar mappen med Visual Studio Code och flyttar till katalogen **/Deploy/K8s** som innehåller skriptet **gen-AKS-ENV. ps1**.
2. De kör skriptet för att skapa det hanterade Kubernetes-klustret med hjälp av AKS och ACR.
    ![AKS](./media/contoso-migration-rebuild/aks1.png)
3. När filen är öppen uppdaterar de $location-parametern till **eastus2**och sparar filen.
    ![AKS](./media/contoso-migration-rebuild/aks2.png)
4. De väljer **Visa** > **Integrerad terminal** för att öppna den integrerade terminalen i Visual Studio Code.
    ![AKS](./media/contoso-migration-rebuild/aks3.png)
5. I den PowerShell-integrerade terminalen loggar de in i Azure med kommandot Connect-AzureRmAccount. [Lär dig mer](https://docs.microsoft.com/powershell/azure/get-started-azureps) om hur du kommer igång med PowerShell.
    ![AKS](./media/contoso-migration-rebuild/aks4.png)
6. De autentiserar Azure CLI genom att köra kommandot `az login` och följa instruktionerna för att autentisera med hjälp av webbläsaren. [Lär dig mer](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest) om hur du loggar in med Azure CLI.
    ![AKS](./media/contoso-migration-rebuild/aks5.png)
7. De kör följande kommando och skickar resursgruppens namn, ContosoRG, namnet på AKS-klustret, smarthotel-aks-eus2, och det nya registernamnet.

    ```PowerShell
    .\gen-aks-env.ps1  -resourceGroupName ContosoRg -orchestratorName smarthotelakseus2 -registryName smarthotelacreus2
    ```

    ![AKS](./media/contoso-migration-rebuild/aks6.png)

8. Azure skapar en annan resursgrupp som innehåller resurserna för AKS-klustret.

    ![AKS](./media/contoso-migration-rebuild/aks7.png)

9. När distributionen är färdig installerar de kommandoradsverktyget **kubectl**. Verktyget är redan installerat i Azure CloudShell.

    ```console
    az aks install-cli
    ```

10. De verifierar anslutningen till klustret genom att köra kommandot **kubectl get nodes**. Noden har samma namn som den virtuella datorn i den automatiskt skapade resursgruppen.

    ![AKS](./media/contoso-migration-rebuild/aks8.png)

11. De kör följande kommando för att starta Kubernetes-instrumentpanelen:

    ```console
    az aks browse --resource-group ContosoRG --name smarthotelakseus2
    ```

12. En webbläsarflik öppnas med instrumentpanelen. Detta är en tunnelanslutning som använder Azure CLI.

    ![AKS](./media/contoso-migration-rebuild/aks9.png)

## <a name="step-2-configure-the-back-end-pipeline"></a>Steg 2: Konfigurera backend-pipeline

### <a name="create-an-azure-devops-project-and-build"></a>Skapa ett Azure DevOps-projekt och -bygge

Contoso skapar ett Azure DevOps-projekt och konfigurerar ett CI-bygge för att skapa containern och push-överför den sedan till ACR. Anvisningarna i det här avsnittet använder lagringsplatsen [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend).

1. Från VisualStudio.com skapar de en ny organisation (**contosodevops360.visualstudio.com**) och konfigurerar den för att använda Git.

2. De skapar ett nytt projekt (**SmartHotelBackend**) med hjälp av Git för versionskontroll och Agile för arbetsflödet.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts1.png)

3. De importerar [GitHub-lagringsplatsen](https://github.com/Microsoft/SmartHotel360-Backend).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts2.png)

4. I **Pipelines** väljer de **Bygge** och skapar en ny pipeline med Azure-lagringsplatsen på Git som källan, från lagringsplatsen.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts3.png)

5. De väljer att starta med ett tomt jobb.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts4.png)

6. De väljer **Hosted Linux Preview** för att skapa pipelinen.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts5.png)

7. I **Fas 1** lägger de till en **Docker Compose**-aktivitet. Den här aktiviteten bygger Docker Compose.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts6.png)

8. De upprepar och lägger till en till **Docker Compose**-aktivitet. Den här aktiviteten push-överför containrar till ACR.

     ![Azure DevOps](./media/contoso-migration-rebuild/vsts7.png)

9. De väljer den första aktiviteten (för att bygga) och konfigurerar bygget med Azure-prenumerationen, auktoriseringen och ACR.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts8.png)

10. De anger sökvägen för filen **docker-compose.yaml** i mappen **src** i databasen. De väljer att skapa tjänstavbildningar och lägger till den senaste taggen. När åtgärden ändras till **Build service images** (Skapa tjänstavbildningar) ändras namnet på Azure DevOps-aktiviteten till **Build services automatically** (Skapa tjänster automatiskt).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts9.png)

11. Nu konfigurerar de den andra Docker-aktiviteten (push-överföringen). De väljer prenumerationen och Azure-containerregistret **smarthotelacreus2**.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts10.png)

12. Återigen anger de filen till docker-compose. yaml-filen, väljer **Push service images** (Push-överför tjänstavbildningar) och lägger till den senaste taggen. När åtgärden ändras till **Push service images** (Push-överför tjänstavbildningar) ändras namnet på Azure DevOps-aktiviteten till **Push services automatically** (Push-överför tjänster automatiskt).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts11.png)

13. När Azure DevOps-aktiviteterna har konfigurerats sparar Contoso bygg-pipelinen och startar byggprocessen.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts12.png)

14. De väljer byggjobbet för att kontrollera förloppet.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts13.png)

15. När bygget är klart visar ACR de nya databaserna, som innehåller containrarna som används av mikrotjänsterna.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts14.png)

### <a name="deploy-the-back-end-infrastructure"></a>Distribuera backend-infrastrukturen

När AKS-klustret har skapats och Docker-avbildningarna har byggts distribuerar Contosos administratörer resten av infrastrukturen som ska användas av backend-mikrotjänster.

- I anvisningarna i avsnittet används lagringsplatsen [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend).
- I mappen **/deploy/k8s/arm** finns det ett enda skript för att skapa alla objekt.

De distribueras på följande sätt:

1. De öppnar en kommandotolk för utvecklare och använder kommandot az login för Azure-prenumerationen.
2. De använder filen deploy.cmd för att distribuera Azure-resurser i resursgruppen ContoRG och regionen EUS2 genom att skriva följande kommando:

    ```console
    .\deploy.cmd azuredeploy ContosoRG -c eastus2
    ```

    ![Distribuera serverdelen](./media/contoso-migration-rebuild/backend1.png)

3. På Azure-portalen hämtar de anslutningssträngen för varje databas, som ska användas senare.

    ![Distribuera serverdelen](./media/contoso-migration-rebuild/backend2.png)

### <a name="create-the-back-end-release-pipeline"></a>Skapa serverdelens distributionspipeline

Contosos administratörer gör nu följande:

- Distribuera Ingress-kontrollanten NGINX för att tillåta inkommande trafik till tjänsterna.
- Distribuera mikrotjänsterna till AKS-klustret.
- Som ett första steg uppdaterar de anslutningssträngarna till mikrotjänsterna med hjälp av Azure DevOps. De konfigurerar sedan en ny distributionspipeline för Azure DevOps för distribution av mikrotjänsterna.
- I anvisningarna i det här avsnittet används lagringsplatsen [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend).
- Några av konfigurations inställningarna (till exempel Active Directory B2C) beskrivs inte i den här artikeln. Mer information om de här inställningarna finns i lagrings platsen ovan.

De skapar pipelinen:

1. Med hjälp av Visual Studio uppdaterar de filen **/deploy/k8s/config_local.yml** med informationen om databasanslutningen som de skrev ned tidigare.

    ![DB-anslutningar](./media/contoso-migration-rebuild/back-pipe1.png)

2. De öppnar Azure DevOps och väljer **+Ny pipeline** i **Versioner** i SmartHotel360-projektet.

    ![Ny pipeline](./media/contoso-migration-rebuild/back-pipe2.png)

3. De väljer **Tomt jobb** för att starta pipelinen utan mall.
4. De anger namn på faser och pipelines.

      ![Namn på fas](./media/contoso-migration-rebuild/back-pipe4.png)

      ![Namn på pipeline](./media/contoso-migration-rebuild/back-pipe5.png)

5. De lägger till en artefakt.

     ![Lägg till artefakt](./media/contoso-migration-rebuild/back-pipe6.png)

6. De väljer **Git** som källtyp och anger projekt-, käll- och huvudgrenen för SmartHotel360-appen.

    ![Artefaktinställningar](./media/contoso-migration-rebuild/back-pipe7.png)

7. De väljer aktivitetslänken.

    ![Aktivitetslänk](./media/contoso-migration-rebuild/back-pipe8.png)

8. De lägger till en ny Azure PowerShell-aktivitet så att de kan köra ett PowerShell-skript i en Azure-miljö.

    ![PowerShell i Azure](./media/contoso-migration-rebuild/back-pipe9.png)

9. De väljer Azure-prenumerationen för aktiviteten och väljer sedan skriptet **deploy.ps1** från Git-lagringsplatsen.

    ![Köra skriptet](./media/contoso-migration-rebuild/back-pipe10.png)

10. De lägger till argument i skriptet. Skriptet tar bort allt klusterinnehåll (förutom **Ingress** och **Ingress-kontrollanten**) och distribuerar mikrotjänsterna.

    ![Skriptargument](./media/contoso-migration-rebuild/back-pipe11.png)

11. De ställer in önskad Azure PowerShell-version till den senaste och sparar pipelinen.

12. De går tillbaka till sidan **Version** och skapar en ny version manuellt.

    ![Ny version](./media/contoso-migration-rebuild/back-pipe12.png)

13. De väljer den här versionen när de har skapat den och väljer **Distribuera** i **Åtgärder**.

      ![Distribuera version](./media/contoso-migration-rebuild/back-pipe13.png)

14. När distributionen är klar kör de följande kommando för att kontrollera statusen för tjänsterna med hjälp av Azure Cloud Shell: **kubectl get services**.

## <a name="step-3-provision-front-end-services"></a>Steg 3: etablera klient dels tjänster

Contosos administratörer behöver distribuera infrastrukturen som ska användas av programmen på klientsidan. De skapar en bloblagringscontainer för lagring av bilderna på husdjuren; Cosmos-databasen för lagring av dokument med information om husdjuren; och API:et för Visuellt innehåll för webbplatsen.

I anvisningarna i det här avsnittet används lagringsplatsen [SmartHotel360-public-web](https://github.com/Microsoft/SmartHotel360-public-web).

### <a name="create-blob-storage-containers"></a>Skapa bloblagringscontainrar

1. På Azure-portalen öppnar de lagringskontot som skapades och väljer **Blobar**.
2. De skapar en ny behållare, **Pets** (Husdjur), med den offentliga åtkomstnivån inställd på container. Användarna kommer att överföra bilderna på sina husdjur till den här containern.

    ![Lagringsblob](./media/contoso-migration-rebuild/blob1.png)

3. De skapar en till ny container med namnet **settings** (inställningar). En fil med alla inställningar för appen på klientsidan kommer att placeras i den här containern.

    ![Lagringsblob](./media/contoso-migration-rebuild/blob2.png)

4. De samlar in åtkomstinformationen för lagringskontot i en textfil för senare användning.

    ![Lagringsblob](./media/contoso-migration-rebuild/blob2.png)

### <a name="provision-a-cosmos-database"></a>Etablera en Cosmos-databas

Contosos administratörer etablerar en Cosmos-databas som ska användas för information om husdjuren.

1. De skapar en **Azure Cosmos DB-databas** på Azure Marketplace.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos1.png)

2. De anger ett namn (**contosomarthotel**), väljer SQL-API:et och placerar det i produktionsresursgruppen ContosoRG i huvudregionen USA, östra 2.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos2.png)

3. De lägger till en ny samling i databasen med standardkapacitet och standarddataflöde.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos3.png)

4. De noterar anslutningsinformationen för databasen för senare användning.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos4.png)

### <a name="provision-computer-vision"></a>Etablera Visuellt innehåll

Contosos administratörer etablerar API:et för Visuellt innehåll. API:et anropas av funktionen för att utvärdera bilder som laddats upp av användare.

1. De skapar en instans av **Visuellt innehåll** på Azure Marketplace.

     ![Visuellt innehåll](./media/contoso-migration-rebuild/vision1.png)

2. De etablerar API:et (**smarthotelpets**) i produktionsresursgruppen ContosoRG, i huvudregionen USA, östra 2.

    ![Visuellt innehåll](./media/contoso-migration-rebuild/vision2.png)

3. De sparar anslutningsinställningarna för API:et till en textfil för senare användning.

     ![Visuellt innehåll](./media/contoso-migration-rebuild/vision3.png)

### <a name="provision-the-azure-web-app"></a>Etablera Azure-webbappen

Contosos administratörer etablerar webbappen med hjälp av Azure-portalen.

1. De väljer **Webbapp** på portalen.

    ![Webbapp](media/contoso-migration-rebuild/web-app1.png)

2. De anger ett namn för appen (**smarthotelcontoso**), kör appen i Windows och placerar den i produktionsresursgruppen **ContosoRG**. De skapar en ny Application Insights-instans för övervakning av appar.

    ![Namn på webbapp](media/contoso-migration-rebuild/web-app2.png)

3. När de är klara bläddrar de till appens adress för att kontrollera att appen har skapats.

4. Nu kan de skapa en mellanlagringsplats för koden på Azure-portalen. Pipelinen kommer att distribueras till den här platsen. Detta säkerställer att koden inte flyttas till produktionsmiljön förrän administratörerna väljer att publicera.

    ![Mellanlagringsplats för webbapp](media/contoso-migration-rebuild/web-app3.png)

### <a name="provision-the-azure-function-app"></a>Etablera Azure-funktionsappen

Contosos administratörer etablerar funktionsappen på Azure-portalen.

1. De väljer **Funktionsapp**.

    ![Skapa funktionsappen](./media/contoso-migration-rebuild/function-app1.png)

2. De anger ett namn för appen (**smarthotelpetchecker**). De placerar appen i produktionsresursgruppen **ContosoRG**. De anger värdplatsen till **Consumption Plan** (Förbrukningsplan) och placerar appen i regionen USA, östra 2. Ett nytt lagringskonto skapas, tillsammans med en Application Insights-instans för övervakning.

    ![Funktionsappinställningar](./media/contoso-migration-rebuild/function-app2.png)

3. När appen har distribuerats bläddrar de till appens adress för att kontrollera att appen har skapats.

## <a name="step-4-set-up-the-front-end-pipeline"></a>Steg 4: Konfigurera klient delens pipeline

Contosos administratörer skapar två olika projekt för klientsidan.

1. I Azure DevOps skapar de projektet **SmartHotelFrontend**.

    ![Projektet på klientsidan](./media/contoso-migration-rebuild/function-app1.png)

2. De importerar Git-lagringsplatsen för [SmartHotel360-klientdelen](https://github.com/Microsoft/SmartHotel360-public-web.git) till det nya projektet.
3. För funktionsappen skapar de ett annat Azure DevOps-projekt (SmartHotelPetChecker) och importerar Git-lagringsplatsen [PetChecker](https://github.com/Microsoft/SmartHotel360-PetCheckerFunction ) till det här projektet.

### <a name="configure-the-web-app"></a>Konfigurera webbappen

Nu konfigurerar Contosos administratörer webbappen så att den använder Contoso-resurser.

1. De ansluter till Azure DevOps-projektet och klonar lagringsplatsen lokalt till utvecklingsdatorn.
2. I Visual Studio öppnar de mappen för att visa lagringsplatsens filer.

    ![Lagringsplatsens filer](./media/contoso-migration-rebuild/configure-webapp1.png)

3. De uppdaterar konfigurationsändringarna efter behov.

    - När webbappen startar söker den efter appinställningen **SettingsUrl**.
    - Den här variabeln måste innehålla en URL som pekar på en konfigurationsfil.
    - Som standard är inställningen som används en offentlig slutpunkt.

4. De uppdaterar filen /config-sample.json/sample.json.

    - Det här är konfigurationsfilen för webben när den offentliga slutpunkten används.
    - De redigerar avsnitten **urls** och **pets_config** med värdena för AKS-API:ets slutpunkter, lagringskonton och Cosmos-databas.
    - URL:erna ska matcha DNS-namnet för den nya webbappen som Contoso skapar.
    - För Contoso är detta **smarthotelcontoso.eastus2.cloudapp.azure.com**.

    ![JSON-inställningar](./media/contoso-migration-rebuild/configure-webapp2.png)

5. När filen har uppdaterats byter de namn på den till **smarthotelsettingsurl** och laddar upp den till bloblagringen som de skapade tidigare.

    ![Namnbyte och överföring](./media/contoso-migration-rebuild/configure-webapp3.png)

6. De väljer filen för att hämta URL:en. URL:en används av appen när den hämtar konfigurationsfilerna.

    ![App-URL](./media/contoso-migration-rebuild/configure-webapp4.png)

7. I filen **appsettings.Production.json** uppdaterar de **SettingsURL** till URL:en för den nya filen.

    ![Uppdatera URL](./media/contoso-migration-rebuild/configure-webapp5.png)

### <a name="deploy-the-website-to-azure-app-service"></a>Distribuera webbplatsen till Azure App Service

Nu kan Contosos administratörer publicera webbplatsen.

1. De öppnar Azure DevOps och väljer **+Ny pipeline** i **Builds and Releases** (Byggen och distributioner) i projektet **SmartHotelFrontend**.
2. De väljer **Git-lagringsplatsen för Azure DevOps** som källa.
3. De väljer mallen **ASP.NET Core**.
4. De granskar pipelinen och kontrollerar att **Publicera webbprojekt** och **Zip Published Projects** (ZIP-publicerade projekt) har markerats.

    ![Pipelineinställningar](./media/contoso-migration-rebuild/vsts-publishfront2.png)

5. I **Utlösare** aktiverar de kontinuerlig integrering och lägger till huvudgrenen. Det gör att bygg-pipelinen startar varje gång ny kod checkas in i huvudgrenen för lösningen.

    ![Kontinuerlig integrering](./media/contoso-migration-rebuild/vsts-publishfront3.png)

6. De väljer **Spara och köa** för att starta ett bygge.
7. När bygget är klart konfigurerar de en distributionspipeline med hjälp av en **Azure App Service-distribution**.
8. De anger ett namn för fasen, **Staging** (mellanlagring).

    ![Miljönamn](./media/contoso-migration-rebuild/vsts-publishfront4.png)

9. De lägger till en artefakt och väljer bygget som de precis har konfigurerat.

     ![Lägg till artefakt](./media/contoso-migration-rebuild/vsts-publishfront5.png)

10. De väljer blixtikonen på artefakten och aktiverar kontinuerlig distribution.

    ![Kontinuerlig distribution](./media/contoso-migration-rebuild/vsts-publishfront6.png)
11. I **Miljö** väljer de **1 jobb, 1 uppgift** under **staging** (mellanlagring).
12. När de har valt prenumerationen och appens namn öppnar de aktiviteten **Distribuera Azure App Service**. Distributionen har konfigurerats att använda distributionsplatsen **staging** (mellanlagring). Det innebär att kod för granskning och godkännande skapas automatiskt på den här platsen.

     ![Plats](./media/contoso-migration-rebuild/vsts-publishfront7.png)

13. I **Pipeline** lägger de till en ny fas.

    ![Ny miljö](./media/contoso-migration-rebuild/vsts-publishfront8.png)

14. De väljer **Azure App Service deployment with slot** (Azure App Service-distribution med plats) och ger miljön namnet **Prod** (produktion).
15. De väljer **1 jobb, 2 aktiviteter** och väljer prenumerationen, apptjänstnamnet och **mellanlagringsplatsen**.

    ![Miljönamn](./media/contoso-migration-rebuild/vsts-publishfront10.png)

16. De tar bort **Deploy Azure App Service to Slot** (Distribuera Azure App Service till plats) från pipelinen. Detta placerades där i föregående steg.

    ![Ta bort från pipeline](./media/contoso-migration-rebuild/vsts-publishfront11.png)

17. De sparar pipelinen. I pipelinen väljer de **Post-deployment conditions** (Villkor efter distribution).

    ![Efter distributionen](./media/contoso-migration-rebuild/vsts-publishfront12.png)

18. De aktiverar **Post-deployment approvals** (Godkännanden efter distribution) och lägger till en utvecklingsledare som godkännare.

    ![Godkännande efter distribution](./media/contoso-migration-rebuild/vsts-publishfront13.png)

19. I bygg-pipelinen startar de ett bygge manuellt. Detta utlöser den nya distributionspipelinen, som distribuerar webbplatsen till mellanlagringsplatsen. För Contoso är URL:en för platsen `https://smarthotelcontoso-staging.azurewebsites.net/`.

20. När bygget är klart och distributionen skickas till platsen, skickar Azure DevOps ett e-postmeddelande till utvecklingsledaren för att få dennes godkännande.

21. Utvecklingsledaren väljer **Visa godkännande** och kan godkänna eller avvisa begäran på Azure DevOps-portalen.

    ![E-postmeddelande för godkännande](./media/contoso-migration-rebuild/vsts-publishfront14.png)

22. Utvecklingsledaren lägger till en kommentar och godkänner. Detta utlöser övergången från **staging**-platsen (mellanlagring) till **prod**-platsen (produktion), och bygget flyttas till produktion.

    ![Godkänna och växla](./media/contoso-migration-rebuild/vsts-publishfront15.png)

23. Pipelinen slutför växlingen.

    ![Slutföra växlingen](./media/contoso-migration-rebuild/vsts-publishfront16.png)

24. Teamet kontrollerar **prod**-platsen för att bekräfta att webbappen är i produktion på `https://smarthotelcontoso.azurewebsites.net/`.

### <a name="deploy-the-petchecker-function-app"></a>Distribuera PetChecker-funktionsappen

Contosos administratörer distribuerar appen på följande sätt.

1. De klonar lagringsplatsen lokalt till utvecklingsdatorn genom att ansluta till Azure DevOps-projektet.
2. I Visual Studio öppnar de mappen för att visa lagringsplatsens filer.
3. De öppnar filen **src/PetCheckerFunction/local.settings.json** och lägger till appinställningarna för lagring, Cosmos-databasen och API:et för Visuellt innehåll.

    ![Distribuera funktionsappen](./media/contoso-migration-rebuild/function5.png)

4. De checkar in koden och synkroniserar den med Azure-DevOps så att ändringarna överförs.
5. De lägger till en ny bygg-pipeline och väljer **Git-lagringsplatsen för Azure DevOps** som källa.
6. De väljer mallen **ASP.NET Core (.NET Framework)** .
7. De accepterar standardvärdena för mallen.
8. I **Utlösare** väljer de att **aktivera kontinuerlig integrering** och väljer **Spara och köa** för att starta ett bygge.
9. När bygget är klart skapar de en bygg-pipeline och väljer **Azure App Service deployment with slot** (Azure App Service-distribution med plats).
10. De ger miljön namnet **Prod** (produktion) och väljer prenumerationen. De anger **apptypen** till **Funktionsapp** och apptjänstnamnet till **smarthotelpetchecker**.

    ![Funktionsapp](./media/contoso-migration-rebuild/petchecker2.png)

11. De lägger till ett **artefaktbygge**.

    ![Artefakt](./media/contoso-migration-rebuild/petchecker3.png)

12. De aktiverar **utlösare av kontinuerlig distribution** och väljer **Spara**.
13. De väljer **Köa ny version** för att köra hela CI/CD-pipelinen.
14. När funktionen har distribuerats visas den på Azure-portalen med statusen **Körs**.

    ![Distribuera funktionsappen](./media/contoso-migration-rebuild/function6.png)

15. De bläddrar till appen för att testa att PetChecker-appen fungerar som förväntat på [http://smarthotel360public.azurewebsites.net/Pets](http://smarthotel360public.azurewebsites.net/Pets).
16. De väljer avataren för att ladda upp en bild.
    ![Distribuera funktionen](./media/contoso-migration-rebuild/function7.png)
17. Den första bilden som de vill kontrollera är av en liten hund.
    ![Distribuera funktionen](./media/contoso-migration-rebuild/function8.png)
18. Appen returnerar ett meddelande om godkännande.
    ![Distribuera funktionen](./media/contoso-migration-rebuild/function9.png)

## <a name="review-the-deployment"></a>Granska distributionen

Med de migrerade resurserna i Azure måste Contoso fullständigt operationalisera och skydda sin nya infrastruktur.

### <a name="security"></a>Säkerhet

- Contoso måste se till att de nya databaserna är säkra. [Läs mer](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).
- Appen måste uppdateras för att kunna använda SSL med certifikat. Containerinstansen bör omdistribueras för att svara på 443.
- Contoso bör överväga att använda Key Vault för att skydda hemligheter för deras Service Fabric-appar. [Läs mer](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="backups-and-disaster-recovery"></a>Säkerhetskopiering och haveriberedskap

- Contoso måste granska kraven för säkerhetskopiering för Azure SQL-databasen. [Läs mer](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).
- Contoso bör överväga att implementera SQL-redundansgrupper för att tillhandahålla regional redundans för databasen. [Läs mer](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview).
- Contoso kan använda geo-replikering för ACR Premium SKU. [Läs mer](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication).
- Cosmos DB säkerhetskopieras automatiskt. Contoso kan [lära sig mer](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore) om den här processen.

### <a name="licensing-and-cost-optimization"></a>Licensierings- och kostnadsoptimering

- När alla resurser har distribuerats bör Contoso tilldela Azure-taggar baserat på deras [infrastrukturplanering](./contoso-migration-infrastructure.md#set-up-tagging).
- All licensiering är inbyggd i kostnaden för de PaaS-tjänster som Contoso använder. Detta kommer att dras av från Enterprise-avtalet.
- Contoso aktiverar Azure Cost Management som licensieras av Cloudyn, ett Microsoft-dotterbolag. Det är en kostnadshanteringslösning med flera moln som hjälper dig att använda och hantera Azure och andra molnresurser. [Läs mer](https://docs.microsoft.com/azure/cost-management/overview) om Azure Cost Management.

## <a name="conclusion"></a>Sammanfattning

I den här artikeln bygger Contoso upp SmartHotel360-appen i Azure. Den virtuella datorn för den lokala appen på klientsidan återskapas till Azure App Service-webbappar. Serverdelen för programmet skapas med mikrotjänster som distribueras till containrar som hanteras av Azure Kubernetes Service (AKS). Contoso förbättrade appfunktionerna med en app för husdjursbilder.
