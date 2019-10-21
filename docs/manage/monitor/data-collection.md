---
title: Guide för moln övervakning – samla in rätt data
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Välj när Azure Monitor eller System Center Operations Manager ska användas i Microsoft Azure
author: MGoedtel
ms.author: magoedte
ms.date: 06/26/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 3d8d6b656f6bfe8072b53dccc05a67479aa36f24
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548573"
---
# <a name="cloud-monitoring-guide-collecting-the-right-data"></a>Övervaknings guide för molnet: samla in rätt data

I den här artikeln beskrivs några saker att tänka på när du samlar in övervaknings data i ett moln program.

Om du vill kontrol lera moln lösningens hälso tillstånd och tillgänglighet måste du konfigurera övervaknings verktygen för att samla in en nivå av signaler som baseras på förutsägbara fel tillstånd. Dessa signaler är symptomen på felet, inte orsaken. Övervaknings verktygen använder mått och, om avancerad diagnostik och rotor Saks analys, även använder loggar.

Planera för övervakning och migrering omsorgsfullt. Börja med att ta med övervaknings tjänstens ägare, verksamhets chefen och annan relaterad personal under planerings fasen och fortsätt att engagera dem i utvecklings-och lanserings cykeln. Deras fokus är att utveckla en övervaknings konfiguration som baseras på följande kriterier:

- Vad är tjänstens sammansättning och vilka beroenden som övervakas idag? I så fall, finns det flera verktyg som ingår? Finns det någon möjlighet att konsolidera, utan att introducera risker?
- Vad är service avtalet och hur ska jag mäta och rapportera det?
- Vad ska instrument panelen för tjänsten se ut när en incident höjs? Vad ska instrument panelen se ut för tjänstens ägare och teamet som stöder tjänsten?
- Vilka mått ger resursen som jag behöver övervaka?  
- Hur kommer tjänst ägaren, support teamet och annan personal att söka i loggarna?

Hur du besvarar dessa frågor och kriterierna för aviseringar bestämmer hur du ska använda övervaknings plattformen. Om du migrerar från en befintlig övervaknings plattform eller uppsättning övervaknings verktyg använder du migreringen som en möjlighet att utvärdera de signaler som du samlar in. Detta är särskilt sant eftersom det finns flera kostnads faktorer att överväga när du migrerar eller integrerar med en molnbaserad övervaknings plattform som Azure Monitor. Kom ihåg att övervaknings data måste vara åtgärds bara. Du måste ha optimerade data som samlas in för att ge dig "en 10 000 Foot-vy" av tjänstens övergripande hälso tillstånd. Instrumentation som definieras för att identifiera verkliga incidenter bör vara så enkla, förutsägbara och tillförlitliga som möjligt.

## <a name="develop-a-monitoring-configuration"></a>Utveckla en övervaknings konfiguration

Övervaknings tjänstens ägare och team följer vanligt vis en gemensam uppsättning aktiviteter för att utveckla en övervaknings konfiguration. De här aktiviteterna börjar vid de första planerings faserna, fortsätter att testa och validera i en miljö som inte är en produktion och utökar till att distribueras till produktion. Övervakning av konfigurationer härleds från kända fellägen, test resultatet av simulerade haverier och erfarenheten av flera personer i organisationen (Service Desk, drift, ingenjörer och utvecklare). Sådana konfigurationer förutsätter att tjänsten redan finns, att den migreras till molnet och att den inte har återskapats.

Övervaka hälso tillståndet och tillgängligheten för dessa tjänster tidigt i utvecklings processen, för kvalitets resultat på service nivå. Om du övervakar utformningen av tjänsten eller programmet som en efterhand så blir resultatet inte lika lyckat.

Överväg följande rekommendationer för att driva en snabbare lösning av incidenten:

- Definiera en instrument panel för varje tjänst komponent.
- Använd mått för att hjälpa ytterligare att diagnostisera, för att identifiera en lösning eller lösa problemet om en rotorsak inte kan identifieras.
- Använd funktioner för instrument panels detalj nivå eller stöd för att anpassa vyn för att förfina den.
- Om du behöver utförliga loggar bör måtten ha hjälpt att nå Sök kriterierna. Annars kan du förbättra dina mått för nästa incident.

Genom att använda denna GUID-uppsättning av principer får du nära real tids insikter, samt bättre hantering av tjänsten.

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Aviserings strategi](./alerting.md)
