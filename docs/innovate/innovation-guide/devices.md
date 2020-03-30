---
title: 'Azure-innovation: Interagera via enheter'
description: Lär dig mer om hur Azure ger ett ramverk för att skapa avancerade och effektiva affärslösningar via anslutna och perceptiva gränsenheter.
author: umarmohamedusman
ms.author: umarm
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 113fb918e24afd6356eb9eafe840dd97429e044e
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80356621"
---
<!-- cSpell:ignore umarmohamedusman umarm Moovit -->

::: zone target="docs"

# <a name="azure-innovation-guide-interact-through-devices"></a>Guide till Azure-innovation: Interagera via enheter

::: zone-end

::: zone target="chromeless"

# <a name="interact-through-devices"></a>Interagera via enheter

::: zone-end

Förnya genom tillfälligt anslutna och perceptiva gränsenheter. Samordna miljontals sådana enheter, inhämta och bearbeta obegränsade data och dra nytta av ett växande antal upplevelser för flera sensorer och flera enheter. För enheter i nätverkets utkant ger Azure ett ramverk för att skapa avancerade och effektiva affärslösningar. Med ubik datateknik, som du får när du använder Azure i kombination med tekniker för artificiell intelligens (AI), kan du skapa alla typer av intelligenta program och system du kan föreställa dig.

Azure-kunder använder en ständigt expanderande uppsättning med anslutna system och enheter som samlar in och analyserar data – i nära anslutning till sina användare, data eller både och. Användare får insikter och upplevelser i realtid som levereras av mycket responsiva och sammanhangsmedvetna program. När du flyttar delar av arbetsbelastningen till nätverksgränsen går det åt mindre tid till att skicka meddelanden till molnet och dina enheter reagerar snabbare på rumsliga händelser.

> [!div class="checklist"]
>
> - Industritillgångar
> - HoloLens 2
> - Azure Sphere
> - Kinect DK
> - Drones
> - Azure SQL Database Edge
> - IoT Plug and Play

<!-- markdownlint-disable MD025 -->

## <a name="global-scale-iot-service"></a>[IoT-tjänst i global skala](#tab/IoTHub)

<!-- markdownlint-enable MD025 -->

Arkitektlösningar som utövar dubbelriktad kommunikation med miljarder IoT-enheter. Använd färdiga telemetridata från enhet till moln för att få bättre förståelse för dina enheters tillstånd och definiera meddelanderutter till andra Azure-tjänster endast via konfiguration. Genom att använda meddelanden från moln till enhet kan du tillförlitligt skicka kommandon och meddelanden till anslutna enheter och spåra meddelandeleveransen med bekräftelsekvitton. Och du kan automatiskt skicka enhetsmeddelanden på nytt om det behövs vid tillfälliga anslutningar.

Här är några av funktionerna som finns:

- **Säkerhetsoptimerad kommunikationskanal** för överföring av data till och från IoT-enheter.
- **Inbyggd enhetshantering** och etablering för anslutning till och hantering av IoT-enheter i stor skala.
- **Fullständig integrering med Event Grid** och serverlös beräkning för enklare utveckling av IoT-tillämpningar.
- **Kompatibilitet med Azure IoT Edge** för utveckling av IoT-hybridtillämpningar.

::: zone target="docs"

**Gå till [IoT Hub](https://docs.microsoft.com/azure/iot-hub)**

**Gå till [Enhetsetableringstjänster](https://docs.microsoft.com/azure/iot-dps)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Åtgärd

Så här skapar du en IoT-hubb:

1. Gå till **IoT Hub**.
2. Välj **Skapa IoT-hubb**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Devices%2FIotHubs]" submitText="Go to IoT Hub" :::

<!-- markdownlint-enable DOCSMD001 -->

IoT Hub Device Provisioning Service är en hjälptjänst för IoT Hub som möjliggör zero-touch och just-in-time-etablering.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Åtgärd

Så här skapar du IoT Hub Device Provisioning Services:

1. Gå till **IoT Hub Device Provisioning Services**.
2. Välj **Create Device Provisioning Services** (Skapa enhetsetableringstjänster).

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Devices%2FProvisioningServices]" submitText="Go to Device Provisioning Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

<!-- markdownlint-disable MD025 -->

## <a name="azure-digital-twins"></a>[Azure Digital Twins](#tab/DigitalTwins)

Skapa återanvändningsbara, mycket skalbara, rumsligt medvetna upplevelser som länkar strömmande data i hela den digitala och fysiska världen. Förbättra kundengagemanget med hjälp av omfattande modeller av fysiska miljöer. Generera diagram för rumslig intelligens för att modellera relationer och interaktioner mellan människor, platser och enheter. Skicka dataförfrågningar från ett fysiskt utrymme i stället för olika sensorer.

**Azure Digital Twins-objektmodeller:** En ontologi som beskriver regioner, lokaler, våningar, kontor, zoner, konferensrum och fokusrum i en smart byggnad, eller olika kraftverk, understationer, energiresurser och kunder i ett energinät, kan modelleras med hjälp av Digital Twins-objektmodeller och ontologier.

**Diagram för rumslig intelligens:** Det hierarkiska diagrammet över platser, enheter och personer som definierats i Digital Twins-objektmodellen som stöder arv, filtrering, bläddring, skalbarhet och utökningsbarhet. Du kan hantera och interagera med diagrammet med den samling REST-API:er som finns i Azure.

::: zone target="docs"

**Gå till [Azure Digital Twins](https://docs.microsoft.com/azure/digital-twins/about-digital-twins)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Åtgärd

Så här skapar du Azure Digital Twins:

1. Välj **Skapa en resurs** i fönstret till vänster.
2. Sök efter **digital twins** och välj **Digital Twins**.
3. Välj **Skapa** för att starta distributionsprocessen.
4. Välj den här knappen om du vill granska befintliga Digital Twins:

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.IoTSpaces%2FGraph]" submitText="Go to Digital Twins" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

<!-- markdownlint-disable MD025 -->

## <a name="location-intelligence"></a>[Platsintelligens](#tab/AzureMaps)

Förutom traditionella platsfunktioner som platser i närheten, trafik och routning kan företag använda tjänsten Azure Maps för att skapa lösningar med platsintelligens i realtid som drivs av våra partner **TomTom** och **Moovit** som erbjuder mobilteknik i världsklass. Integrera enkelt avancerade plats- och mobilitetsfunktioner i dina appar med geospatiala tjänster.

**Data Service Preview:** Ladda upp och lagra geospatiala data för användning med rumsliga åtgärder eller bildkomposition för att minska svarstiden, öka produktiviteten och möjliggöra nya scenarion med dina appar.

**Spatial Operations:** Förbättra platsintelligensen med ett bibliotek med vanliga geospatiala matematiska beräkningar, bland annat geofencing, närmaste punkt, stort cirkelavstånd och buffertar.

**Geoplats:** Identifiera vilket land en IP-adress tillhör. Anpassa innehåll och tjänster beroende på var användaren befinner sig och få insikter kring kundernas geografiska fördelning.

::: zone target="docs"

**Gå till [Azure Maps](https://docs.microsoft.com/azure/azure-maps)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Åtgärd

Så här använder du platsintelligens:

1. Gå till **Azure Maps-konton**.
2. Välj **Skapa Azure Maps-konton**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Maps%2FAccounts]" submitText="Go to Azure Maps Account" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="spatial-experiences"></a>[Rumsupplevelser](#tab/spatial)

Azure Spatial Anchors gör det möjligt för utvecklare att arbeta med plattformar för mixad verklighet för att uppfatta utrymmen, ange exakta platser av intresse och återkalla de platserna av intresse från enheter som stöds.

**Ge verkligheten ett sammanhang:** Ge användarna en bättre förståelse för sina data, var och när de än behöver dem, genom att placera och koppla det digitala innehållet till fysiska platser av intresse.

**Dela hologram på olika enheter:** Uppnå snabbare beslut och resultat genom att erbjuda teamet och kunderna 3D på den enhet de föredrar. Spatial Anchors gör det enkelt för personer på samma plats att delta i program med mixad verklighet för flera användare.

**Engagerande upplevelser:** Koppla samman rumsliga fästpunkter genom att skapa relationer mellan dem, och leverera ett användargränssnitt som kan ha två eller flera platser av intresse som en användare måste interagera med för att slutföra en uppgift. Din app kan låta en användare placera en virtuell artefakt i den verkliga världen. I en industrimiljö kan en användare få sammanhangsbaserad information om en maskin genom att rikta en enhetskamera som stöds mot den.

Azure Spatial Anchors består av en hanterad tjänst och klient-SDK:er för enhetsplattformar som stöds.

::: zone target="docs"

**Gå till [Azure Spatial Anchors](https://azure.microsoft.com/services/spatial-anchors)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Åtgärd

Så här använder du rumsupplevelser:

1. Gå till **Spatial Anchors-konton**.
2. Välj **Skapa Spatial Anchors-konton**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.MixedReality%2FSpatialAnchorsAccounts]" submitText="Go to Spatial Anchors Accounts" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-remote-rendering"></a>[Azure Remote Rendering](#tab/RemoteRender)

Rendera interaktivt 3D-innehåll av hög kvalitet i molnet och strömma det till dina enheter i realtid. Renderingsarbetsbelastningar används ofta för specialeffekter (VFX) inom media och nöjesbranschen. Rendering används också inom flera andra branscher som marknadsföring, detaljhandel, olja och gas samt tillverkning.

Renderingsprocessen är databehandlingsintensiv. Det kan finnas många bilder som ska skapas och varje bild kan ta flera timmar att rendera. Rendering är därför en perfekt arbetsbelastning för satsvis bearbetning som kan använda Azure och Azure Batch för att köra flera renderingar parallellt.

::: zone target="docs"

**Gå till [Azure Remote Rendering](https://azure.microsoft.com/services/remote-rendering)**

**Gå till [Rendering med hjälp av Azure](https://docs.microsoft.com/azure/batch/batch-rendering-service)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Åtgärd

Så här använder du Remote Rendering:

1. Gå till **Batch-konton**.
2. Välj **Skapa Batch-konton**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Batch%2FBatchAccounts]" submitText="Go to Azure Batch" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
