---
title: 'Azure-innovation: Engagera via appar'
description: Lär dig om Azure-tjänster som hjälper dig att enkelt modernisera dina befintliga webb- och API-appar och bygga appar i molnet.
author: billyclaymyersmsft
ms.author: wimyers
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: ad638c667a75561dfbdb9827413249ebc93fd9dc
ms.sourcegitcommit: 10637acba8c857a6f5aa8c4a80c0649903f60402
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/28/2020
ms.locfileid: "78171080"
---
::: zone target="docs"

# <a name="azure-innovation-guide-engage-customers-through-apps"></a>Guide till Azure-innovation: Engagera kunder via appar

::: zone-end

::: zone target="chromeless"

# <a name="engage-customers-through-apps"></a>Engagera kunder via appar

::: zone-end

Innovation med appar omfattar både att modernisera befintliga lokala appar och att skapa molnbaserade appar med hjälp av containrar eller serverlösa tekniker. Azure tillhandahåller olika PaaS-tjänster, till exempel Azure App Service, som hjälper dig att enkelt modernisera dina befintliga webb- och API-appar som skrivits i .NET, .NET Core, Java, Node.js, Ruby, Python eller PHP för distribution i Azure.

Med en containermodell med öppen standard är det enkelt att skapa mikrotjänster eller använda containrar för befintliga appar och distribuera dem i Azure med hanterade tjänster som Azure Kubernetes Services, Azure Container Instances och Web App for Containers. Serverlösa tekniker som Azure Functions och Azure Logic Apps har en förbrukningsmodell (betala för det du använder) så att du kan fokusera på att skapa ditt program i stället för att distribuera och hantera infrastruktur.

<!-- markdownlint-disable MD025 -->

# <a name="deliver-value-faster"></a>[Leverera värde snabbare](#tab/DeliverValueFaster)

En av fördelarna med molnbaserade lösningar är att du kan samla feedback snabbare och börja leverera värde till dina användare. Oavsett om användaren är en extern kund eller en användare i ditt företag är det bättre ju snabbare du kan få feedback om dina program.

## <a name="azure-app-service"></a>Azure App Service

Azure App Service tillhandahåller en värdmiljö för dina program som gör att du slipper ägna tid och resurser åt infrastrukturhantering och uppdatering av operativsystem. Skalningen sker automatiskt efter användarnas behov, men du anger gränser för att hålla koll på kostnaderna.

Azure App Service har förstklassigt stöd för språk som ASP.NET, ASP.NET Core, Java, Ruby, Node.js, PHP och Python. Om du behöver vara värd för en annan körningsstack kan du snabbt och enkelt ha en Docker-container i App Service med Webb App for Containers. Det innebär att du kan vara värd för en egen kodstack i en miljö utan att ha egna servrar.

### <a name="action"></a>Åtgärd

Konfigurera eller övervaka Azure App Service-distributioner:

1. Gå till **App Services**.
2. Konfigurera en ny tjänst: Välj **Lägg till** och följ anvisningarna.
3. Hantera befintliga tjänster: Välj önskad app i listan över värdbaserade program.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites]" submitText="Go to App Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-cognitive-services"></a>Azure Cognitive Services

Med Azure Cognitive Services kan du integrera avancerad intelligens direkt i ditt program via en uppsättning API:er, och dra nytta av AI- och maskininlärningsalgoritmer som stöds av Microsoft.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Åtgärd

Så här konfigurerar eller övervakar du Azure Cognitive Services-distributioner:

1. Gå till **Cognitive Services**.
2. Konfigurera en ny tjänst: Välj **Lägg till** och följ anvisningarna.
3. Hantera befintliga tjänster: Välj önskad tjänst i listan över värdbaserade tjänster.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-bot-service"></a>Azure Bot Service

Azure Bot Services utökar ditt program med ett naturligt robotgränssnitt som använder AI och maskininlärning och skapar ett nytt sätt att interagera med dina kunder.

### <a name="action"></a>Åtgärd

Konfigurera eller övervaka Azure App Service-distributioner:

1. Gå till **Bot Services**.
2. Konfigurera en ny tjänst: Välj **Lägg till** och följ anvisningarna.
3. Hantera befintliga tjänster: Välj önskad robot i listan över värdbaserade tjänster.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.BotService%2FbotServices]" submitText="Go to Bot Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-devops"></a>Azure DevOps

Alla innovationsvägar leder till DevOps. Microsoft har länge haft en lokal produkt som heter Team Foundation Server (TFS). Under vår egen innovationsresa utvecklade vi Azure DevOps, en molnbaserad tjänst som tillhandahåller verktyg för skapande och publicering som stöder flera språk och mål för dina versioner. Mer information finns i [Azure DevOps](https://docs.microsoft.com/azure/devops).

## <a name="visual-studio-app-center"></a>Visual Studio App Center

I och med att mobilappar blir allt populärare ökar behovet av en plattform som tillhandahåller automatiserade tester på verkliga enheter med olika konfigurationer. Visual Studio App Center erbjuder mer än en plats där du kan testa dina program i iOS, Android, Windows och macOS. Det är också en övervakningsplattform där du snabbt och enkelt kan analysera din telemetri med Azure Application Insights. Mer information finns i [Översikt över Visual Studio App Center](https://docs.microsoft.com/appcenter).

Visual Studio App Center har också en meddelandetjänst som gör att du kan skicka meddelanden till ditt program på olika plattformar med ett enda anrop utan att du behöver ha kontakt med varje enskild meddelandetjänst. Mer information finns i [Visual Studio App Center Push (ACP)](https://docs.microsoft.com/appcenter/push).

### <a name="learn-more"></a>Läs mer

- [Översikt över App Service](https://docs.microsoft.com/azure/app-service/overview)
- [Web App for Containers: Köra en anpassad container](https://docs.microsoft.com/azure/app-service/containers/quickstart-docker)
- [En introduktion till Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview)
- [Azure för .NET- och .NET Core-utvecklare](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet)
- [Dokumentation om Azure SDK för Python](https://docs.microsoft.com/azure/python)
- [Azure för Java-molnutvecklare](https://docs.microsoft.com/azure/java/?view=azure-java-stable)
- [Skapa en PHP-webbapp i Azure](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-php)
- [Dokumentation om Azure SDK för Java Script](https://docs.microsoft.com/azure/javascript)
- [Dokumentation om Azure SDK för Go](https://docs.microsoft.com/azure/go)
- [DevOps-lösningar](https://azure.microsoft.com/solutions/devops)

# <a name="create-cloud-native-apps"></a>[Skapa molnbaserade program](#tab/CloudNative)

<!-- markdownlint-disable MD026 -->

## <a name="what-are-cloud-native-applications"></a>Vad är molnbaserade program?

Molnbaserade program utvecklas från grunden med optimal skalning och prestanda för molnet. De är löst kopplade och baseras på mikrotjänstarkitekturer, använder hanterade tjänster, kan vara observerbara och drar nytta av kontinuerlig leverans för att uppnå hög tillförlitlighet och snabbare tid till marknad. De är vanligtvis flyttbara och kan köras i dynamiska miljöer som offentliga moln, privata moln och hybridmoln. Molnbaserade program skapas vanligtvis med en eller flera av följande metoder:

- Mikrotjänster
- Utan server
- Containrar

## <a name="microservices"></a>Mikrotjänster

Mikrotjänster är en typ av programarkitektur i vilken programmen skapas av små fristående moduler som kommunicerar med varandra via väldefinierade API-kontrakt. Dessa tjänstmoduler är väl isärkopplade byggstenar som är tillräckligt små för att implementera en enskild funktion. Mikrotjänster hjälper dig att:

- Skapa tjänster oberoende av varandra.
- Skala tjänster autonomt.
- Använda de lämpligaste metoderna för distribution och programmeringsspråk.
- Isolera felpunkter.
- Leverera värde snabbare.

### <a name="azure-kubernetes-service-aks"></a>Azure Kubernetes Service (AKS)

Använd en fullständigt hanterad Kubernetes-tjänst för att hantera etablering, uppgradering och skalning av klusterresurser på begäran. Med AKS kan du enkelt att distribuera och hantera program i containrar. AKS erbjuder serverlös Kubernetes, en integrerad kontinuerlig integrering och kontinuerlig leveransupplevelse (CI/CD) samt säkerhet och styrning på företagsnivå. Förena utvecklings- och driftsteamen på en enda plattform och skapa, leverera och skala program snabbt och tryggt.

#### <a name="action"></a>Åtgärd

Så här konfigurerar och övervakar du en Azure Kubernetes-tjänst:

1. Gå till **Azure Kubernetes Services**.
2. Konfigurera en ny tjänst: Välj **Lägg till** och följ anvisningarna.
3. Hantera befintliga tjänster: Välj önskad Kubernetes-tjänst i listan.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.ContainerService%2FmanagedClusters]" submitText="Go to Azure Kubernetes services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="event-based-solutions"></a>Händelsebaserade lösningar

### <a name="azure-functions"></a>Azure Functions

Med Azure Functions får du en plattform för att köra små kodenheter eller funktioner i molnet. Functions kan vara ett sätt att börja omstrukturera din kod till en mikrotjänstbaserad arkitektur.

Körmiljön för Azure Functions stöder många språk, till exempel C#, Java, JavaScript och Python. En fullständig lista finns i [Språk som stöds i Azure Functions](https://docs.microsoft.com/azure/azure-functions/supported-languages).

En annan fördel med funktioner är att de kan utlösas av andra åtgärder och händelser som HTTPTriggers, TimerTriggers och utlösare från andra Azure-tjänster som Blob Storage, EventGrid och ServiceBus. Mer information om utlösare och bindningar finns i [Utlösare och bindningar i Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).

#### <a name="action"></a>Åtgärd

Så här konfigurerar och övervakar du Azure Functions-distributioner:

1. Gå till **Funktionsapp**.
2. Konfigurera en ny app: Välj **Lägg till** och följ anvisningarna.
3. Hantera befintliga appar: Välj önskad app i listan över funktionsappar.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites/kind/functionapp]" submitText="Go to Azure Functions" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="serverless-solutions"></a>Serverlösa lösningar

Skapa molnbaserade appar utan att etablera och hantera någon infrastruktur med hjälp av en helt hanterad plattform där skalning, tillgänglighet och prestanda hanteras åt dig. Fördelar med Azures serverlösa lösningar:

- Ökar utvecklarhastigheten.
- Förbättrar teamets prestation.
- Förbättrar organisationspåverkan.

### <a name="azure-logic-apps"></a>Azure Logic Apps

Integrera data och appar istället för att skriva komplex integrationskod mellan olika system. Skapa serverlösa arbetsflöden visuellt med Azure Logic Apps och använd dina egna API:er, serverlösa funktioner eller färdiga SaaS-anslutningsappar, som Salesforce, Microsoft Office 365 och Dropbox.

#### <a name="action"></a>Åtgärd

Så här konfigurerar eller övervakar du Azure Logic Apps:

1. Gå till **Logic Apps**.
2. Konfigurera en ny app: Välj **Lägg till** och följ anvisningarna.
3. Hantera befintliga appar: Välj önskad logikapp i listan.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Logic%2Fworkflows]" submitText="Go to Azure Logic Apps" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="serverless-api-management"></a>Serverlös API-hantering

Publicera, säkra, transformera, underhåll och övervaka API:er med hjälp av Azure API Management, en fullständigt hanterad tjänst som ger en användningsmodell utformad och implementerad för att fungera på ett naturligt sätt med serverlösa program.

#### <a name="action"></a>Åtgärd

Så här konfigurerar eller övervakar du API Management-tjänster:

1. Gå till **API Management-tjänster**.
2. Konfigurera en ny tjänst: Välj **Lägg till** och följ anvisningarna.
3. Hantera befintliga tjänster: Välj önskad tjänst i listan.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice]" submitText="Go to API Management services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="containers"></a>Containrar

Med Azure kan du modernisera din programportfölj med hjälp av olika containertjänster. Med tjänsterna kan du migrera dina befintliga program till containrar och skapa molnbaserade mikrotjänstprogram för att snabbare leverera värde till dina användare. Använd CI/CD-verktyg från slutpunkt till slutpunkt för att utveckla, uppdatera och distribuera dina containerprogram. Hantera cointainrar i stor skala med en fullständigt hanterad Kubernetes-containerorkestreringstjänst som kan integreras med Azure Active Directory. Oavsett var du befinner dig i din appmodernisering får du snabbare programutveckling med containrar samtidigt som du uppfyller dina säkerhetskrav.

### <a name="azure-container-instances"></a>Azure Container Instances

Kör Docker-containrar på begäran i en hanterad serverlös Azure-miljö. Azure Container Instances är en lösning för alla scenarier som kan användas i isolerade containrar, utan orkestrering. När du kör dina arbetsbelastningar i Container Instances kan du fokusera på att utforma och skapa program i stället för att hantera infrastrukturen som kör dem.

### <a name="action"></a>Åtgärd

Så här konfigurerar och övervakar du containerinstanser:

1. Gå till **Containerinstanser**.
2. Så här konfigurerar du en ny containerinstans: Välj **Lägg till** och följ anvisningarna.
3. Hantera befintliga containerinstanser: Välj den önskade containerinstansen i listan.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ContainerInstance%2FcontainerGroups]" submitText="Go to Container instances" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="azure-red-hat-openshift"></a>Azure Red Hat OpenShift

Med Azure Red Hat OpenShift kan du på egen hand flexibelt distribuera helt hanterade OpenShift-kluster. Tjänsten gör det möjligt för dig att fortsätta att efterleva gällande regler och fokusera på att utveckla program, eftersom både Microsoft och Red Hat sköter korrigering, uppdatering och övervakning av masterenheter, infrastruktur och programnoder åt dig. Välj dina egna register-, nätverks-, lagrings eller CI/CD-lösningar. Eller kom snabbt igång med hjälp av inbyggda lösningar som har automatisk källkodshantering, containrar och programversioner, distribution, skalning, tillståndshantering och mycket annat.

**Gå till [Azure Red Hat OpenShift](https://docs.microsoft.com/azure/openshift/intro-openshift)**

# <a name="isolate-points-of-failure"></a>[Isolera felpunkter](#tab/IsolatePointsOfFailure)

När du börjar övergå från den första testfasen kan du utvärdera hur du kan isolera och ta bort felpunkter. Eftersom Azure-molnplattformen har en distribuerad karaktär kan du utforma ditt program för att minimera fel och öka prestanda.

## <a name="azure-front-door-service"></a>Azure Front Door Service

Med Azure Front Door Service får du en skalbar och säker startpunkt för att leverera ditt program över hela världen. Azure Front Door Service kombinerar optimering av trafik för bästa prestanda och omedelbar global redundans. Använd Azure Front Door Service i stället för Azure Traffic Manager om du behöver TLS-avslut (Transport Layer Security) (”SSL-avlastning”) eller bearbetning på programnivå för enskilda HTTP/HTTPS-begäranden.

### <a name="action"></a>Åtgärd

Så här konfigurerar eller övervakar du ytterdörrar:

1. Gå till **Ytterdörrar**.
2. Konfigurera en ny ytterdörr: Välj **Lägg till** och följ anvisningarna.
3. Hantera befintliga ytterdörrar: Välj önskad ytterdörr i listan.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2Ffrontdoors]" submitText="Go to Front Doors" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="traffic-manager"></a>Traffic Manager

Traffic Manager tillhandahåller DNS-baserad belastningsutjämning som kan dirigeras baserat på olika regler. Denna funktion hjälper till att säkerställa återhämtning om det uppstår fel i en distribuerad tjänst. Du kan också stapla Traffic Manager om du vill använda både felbaserad dirigering och prestandabaserad dirigering för att tillhandahålla bästa möjliga upplevelse baserat på geografisk plats.

### <a name="action"></a>Åtgärd

Så här konfigurerar eller övervakar du Traffic Manager-profiler:

1. Gå till **Traffic Manager-profiler**.
2. Konfigurera en ny profil: Välj **Lägg till** och följ anvisningarna.
3. Hantera befintliga profiler: Välj önskad profil i listan.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2Ftrafficmanagerprofiles]" submitText="Go to Traffic Manager profiles" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-content-delivery-network"></a>Azure Content Delivery Network

Azure erbjuder ett distribuerat Content Delivery Network (CDN) som säkerställer att dina tillgångar levereras i tid genom att de cachelagras nära användarna. Cachelagringen hjälper till att förbättra kundernas upplevelse. Vid nedladdning av innehåll förhindrar den också problem som orsakas av nätverksproblem mellan CDN-slutpunkten och det datacenter som är värd för ditt program. Content Delivery Network kan också användas av program som inte finns i Azure.

### <a name="action"></a>Åtgärd

Så här konfigurerar eller övervakar du Content Delivery Network-profiler:

1. Gå till **CDN-profiler**.
2. Konfigurera en ny profil: Välj **Lägg till** och följ anvisningarna.
3. Hantera befintliga profiler: Välj önskad profil i listan.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.cdn%2Fprofiles]" submitText="Go to CDN profiles" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="learn-more"></a>Läs mer

- [Azure Front Door](https://docs.microsoft.com/azure/frontdoor/front-door-overview)
- [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager)
- [Content Delivery Network](https://docs.microsoft.com/azure/cdn)
