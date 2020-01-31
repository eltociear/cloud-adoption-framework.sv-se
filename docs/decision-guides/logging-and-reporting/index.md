---
title: Beslutsguide för loggning och rapportering
description: Lär dig om loggning, rapportering och övervakning som centrala tjänster i Azure-migreringar.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 038137088abe02160fd199cef468ecc5d5756281
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806772"
---
# <a name="logging-and-reporting-decision-guide"></a>Beslutsguide för loggning och rapportering

Alla organisationer behöver mekanismer för att meddela IT-team om prestanda, drifttid och säkerhetsfrågor innan de blir till allvarliga problem. En lyckad övervakningsstrategi gör att du kan förstå hur de enskilda komponenter som utgör dina arbetsbelastningar och din nätverksinfrastruktur presterar. Inom ramen för en offentlig molnmigrering är det mycket viktigt att integrera loggning och rapportering med befintliga övervakningssystem och informera lämplig IT-personal om viktiga händelser och mått, detta för att säkerställa att organisationen uppnår målen gällande drifttid, säkerhet och policyefterlevnad.

![Alternativ för loggning, rapportering och övervakning ordnade från minst till mest komplext, inriktat med direktlänkar nedan](../../_images/decision-guides/decision-guide-logging-and-reporting.png)

Hoppa till: [Planera övervakningsinfrastrukturen](#plan-your-monitoring-infrastructure) | [Molnbaserat](#cloud-native) | [Lokal utökning](#on-premises-extension) | [Gateway-sammansättning](#gateway-aggregation) | [Hybridövervakning (lokal)](#hybrid-monitoring-on-premises) | [Hybridövervakning (molnbaserad)](#hybrid-monitoring-cloud-based) | [Flera moln](#multicloud) | [Läs mer](#learn-more)

Brytpunkten när du fastställer en strategi för molnloggning och rapportering baseras främst på befintliga investeringar som din organisation har gjort inom driftsprocesser samt till viss del på eventuella krav som du har för att stödja en strategi för flera moln.

Aktiviteter i molnet kan loggas och rapporteras på flera sätt. Molnbaserad och centraliserad loggning är två vanligt alternativ för hanterade tjänster, som drivs av prenumerationsdesignen och antalet prenumerationer.

## <a name="plan-your-monitoring-infrastructure"></a>Planera övervakningsinfrastrukturen

När du planerar distributionen behöver du tänka på var loggningsdata lagras och hur du kommer att integrera molnbaserade rapporterings- och övervakningstjänster med dina befintliga processer och verktyg.

| Fråga | Molnbaserat | Lokal utökning | Hybridövervakning | Gateway-sammansättning |
|-----|-----|-----|-----|-----|
| Har du en befintlig lokal övervakningsinfrastruktur? | Inga | Ja | Ja |  Inga |
| Har du krav som förhindrar lagring av loggdata på externa lagringsplatser? | Inga | Ja | Inga | Inga |
| Behöver du integrera molnövervakning med lokala system? | Inga | Inga | Ja | Inga |
Behöver du bearbeta eller filtrera telemetridata innan de skickas till dina övervakningssystem? | Inga | Inga | Inga | Ja |

### <a name="cloud-native"></a>Molnbaserat

Om din organisation för närvarande saknar etablerade loggnings- och rapporteringssystem, eller om din planerad distribution inte behöver integreras med befintliga lokala eller andra externa övervakningssystem, är en molnbaserad SaaS-lösning såsom [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) det enklaste valet.

I det här scenariot registreras och lagras alla loggdata i molnet medan de verktyg för loggning och rapportering som bearbetar och visar information för IT-personalen tillhandahålls av Azure-plattformen och Azure Monitor.

Anpassade Azure Monitor-baserade loggningslösningar kan implementeras ad hoc för varje prenumeration eller arbetsbelastning i mindre eller experimentella distributioner, samt organiseras på ett centraliserat sätt för att övervaka loggdata i hela din molnmiljö.

**Molnautentiska antaganden:** Användning av ett molnbaserat system för loggning och rapportering förutsätter följande:

- Du behöver inte integrera loggdata från dina molnarbetsbelastningar till befintliga lokala system.
- Du kommer inte att använda dina molnbaserade rapporteringssystem för att övervaka lokala system.

### <a name="on-premises-extension"></a>Lokal utökning

Det kan kräva betydande nyutvecklingsarbete för att program och tjänster som migreras till molnet ska kunna dra nytta av molnbaserade lösningar för loggning och rapportering såsom Azure Monitor. I dessa fall kan du överväga att tillåta att dessa arbetsbelastningar fortsätter att skicka telemetridata till befintliga lokala system.

För att stödja den här metoden behöver dina molnresurser kunna kommunicera direkt med dina lokala system via en kombination av [hybridnätverk](../software-defined-network/hybrid.md) och [molnhanterade domäntjänster](../identity/index.md#cloud-hosted-domain-services). När detta sker fungerar det virtuella molnnätverket som en nätverksutökning av den lokala miljön. Därför kan molnhanterade arbetsbelastningar kommunicera direkt med ditt lokala system för loggning och rapportering.

Den här metoden drar nytta av din befintliga investering i övervakningsverktyg med begränsade ändringar av molndistribuerade program eller tjänster. Det här är ofta den snabbaste metoden för att stödja övervakning under en lift and shift-migrering. Däremot registrerar den inte loggdata som produceras av molnbaserade PaaS- och SaaS-resurser, och den utelämnar VM-relaterade loggar som genereras av själva molnplattformen, till exempel VM-status. Därför bör det här mönstret vara en tillfällig lösnings tills en mer omfattande hybridövervakningslösning implementeras.

Antaganden gällande endast lokalt:

- Du behöver endast underhålla loggdata i din miljö som är helt lokal, antingen för att uppfylla tekniska krav eller på grund av regel- eller policykrav.
- Dina lokala system stöder inte hybridloggning och rapportering eller lösningar för gateway-sammansättning.
- Dina molnbaserade program kan skicka telemetri direkt till dina lokala loggningssystem, eller så kan övervakningsagenter som skickar till lokala miljöer distribueras till virtuella arbetsbelastningsdatorer.
- Dina arbetsbelastningar blir inte beroende av PaaS- eller SaaS-tjänster som kräver molnbaserad loggning och rapportering.

### <a name="gateway-aggregation"></a>Gateway-sammansättning

För scenarier med stora mängder molnbaserade telemetri eller där befintliga lokala övervakningssystem behöver ändra loggdata innan de kan bearbetas kan en [gateway-sammansättningstjänst](https://docs.microsoft.com/azure/architecture/patterns/gateway-aggregation) för loggdata komma att krävas.

En gateway-tjänst distribueras till din molnleverantör. Sedan konfigureras relevanta program och tjänster för att skicka telemetridata till gatewayen i stället för ett standardmässigt loggningssystem. Gatewayen kan sedan bearbeta data genom att aggregera, kombinera eller på annat sätt formatera dem innan de skickas till din övervakningstjänst för datainmatning och analys.

En gateway kan dessutom användas för att aggregera och förbearbeta telemetridata som är kopplade till molnbaserade system eller hybridsystem.

Antaganden gällande gateway-sammansättning:

- Du förväntar dig stora mängder telemetridata från dina molnbaserade program eller tjänster.
- Du behöver bearbeta eller på annat sätt optimera telemetridata innan de skickas till dina övervakningssystem.
- Dina övervakningssystem har API:er eller andra mekanismer som kan mata in loggdata efter bearbetning av gatewayen.

### <a name="hybrid-monitoring-on-premises"></a>Hybridövervakning (lokalt)

En lösning för hybridövervakning kombinerar loggdata från både dina lokala och molnbaserade resurser för att ge en integrerad vy av din IT-egendoms driftstatus.

Om du har en befintlig investering i lokala övervakningssystem som skulle vara svår eller dyr att ersätta kan du behöva integrera telemetri från dina molnarbetsbelastningar till befintliga lokala övervakningslösningar. I ett lokalt hybridövervakningssystem fortsätter lokala telemetridata att använda det befintliga lokala övervakningssystemet. Antingen skickas molnbaserade telemetridata skickas direkt till det lokala övervakningssystemet, eller så skickas data till Azure Monitor och kompileras och matas därefter regelbundet in i det lokala systemet.

**Antaganden gällande lokal hybridövervakning:** Användning av ett lokalt system för loggning och rapportering för hybridövervakning förutsätter följande:

- Du behöver använda befintliga lokala rapporteringssystem för att övervaka molnarbetsbelastningar.
- Du behöver upprätthålla ägarskap för loggdata lokalt.
- Dina lokala hanteringssystem har API:er eller andra mekanismer för att mata in loggdata från molnbaserade system.

> [!TIP]
> Som en del av den iterativa egenskapen hos molnmigrering är en övergång från utpräglat molnbaserad och lokal övervakning till en delvis hybridbaserad metod trolig i takt med att integreringen av molnbaserade resurser och tjänster till din övergripande IT-egendom mognar.

### <a name="hybrid-monitoring-cloud-based"></a>Hybridövervakning (molnbaserad)

Om du inte har ett starkt behov av att underhålla ett lokalt övervakningssystem, eller om du vill ersätta lokala övervakningssystem med en centraliserad molnbaserad lösning, kan du även välja att integrera lokala loggdata med Azure Monitor för att få ett centraliserat molnbaserat övervakningssystem.

På ett sätt som liknar den lokala metoden skulle molnbaserade arbetsbelastningar i det här scenariot skicka telemetri direkt till Azure Monitor, och lokala program och tjänster skulle antingen skicka telemetri direkt till Azure Monitor eller aggregera dessa data lokalt för regelbunden datainmatning till Azure Monitor. Azure Monitor skulle då fungera som ditt primära övervaknings- och rapporteringssystem för hela IT-egendomen.

Antaganden gällande molnbaserad hybridövervakning: Användning av molnbaserade loggnings- och rapporteringssystem för hybridövervakning förutsätter följande:

- Du är inte beroende av befintliga lokala övervakningssystem.
- Dina arbetsbelastningar omfattas inte av regel- eller policykrav för lagring av loggdata lokalt.
- Dina molnbaserade övervakningssystem har API:er eller andra mekanismer för att mata in loggdata från lokala program och tjänster.

### <a name="multicloud"></a>Flera moln

Integrering av loggnings- och rapporteringsfunktioner på en plattform för flera moln kan vara komplicerat. Tjänster som erbjuds mellan plattformarna är ofta inte direkt jämförbara, och även funktioner för loggning och telemetri som erbjuds av dessa tjänster skiljer sig åt.
Stöd för loggning med flera moln kräver ofta användning av gateway-tjänster för att bearbeta loggdata till ett gemensamt format innan data skickas till en hybridloggningslösning.

## <a name="learn-more"></a>Läs mer

[Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) är standardtjänsten för rapportering och övervakning för Azure. Den tillhandahåller:

- En enhetlig plattform för insamling av apptelemetri, värdhantering av telemetri (till exempel virtuella datorer), containermått, Azure-plattformsmått samt händelseloggar.
- Visualisering, frågor, aviseringar och analysverktyg. Den kan ge insikter om virtuella datorer, gästoperativsystem, virtuella nätverk och händelser för arbetsbelastningsprogram.
- [REST API:er](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-rest-api-walkthrough) för integrering med externa tjänster och automation av övervaknings- och aviseringstjänster.
- [Integrering](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-partners) med många populära tredjepartsleverantörer.

## <a name="next-steps"></a>Nästa steg

Loggning och rapportering är bara en av huvudkomponenterna för infrastruktur som kräver arkitektoniska beslut under en process för att implementera moln. Gå till [översikten över beslutsguider](../index.md) om vill veta mer om alternativa mönster eller modeller som används vid utformningsbeslut för andra typer av infrastrukturer.

> [!div class="nextstepaction"]
> [Beslutsguider för arkitektur](../index.md)
