---
title: Nyheter
description: Lär dig mer om de senaste uppdateringarna i Microsoft Cloud adoption Framework för Azure.
author: JanetCThomas
ms.author: janet
ms.date: 03/27/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: c701d49a80ea0ec087f26f792b7ffe8dbd4c061f
ms.sourcegitcommit: 1a4b140f09bdaa141037c54a4a3b5577cda269db
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/30/2020
ms.locfileid: "80392501"
---
<!-- markdownlint-disable MD024 -->

# <a name="whats-new-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Vad är nytt i Microsoft Cloud implementerings ramverk för Azure

Här är en lista över de senaste ändringarna som gjorts i moln införande ramverket.

Det här ramverket är byggt i samarbete med kunder, partner och interna Microsoft-team. Nytt och uppdaterat innehåll släpps när det blir tillgängligt. Med dessa versioner kan du testa, validera och förfina vägledningen tillsammans med oss. Vi rekommenderar att du samarbetar med oss för att bygga ramverket för moln införande för Azure.

## <a name="march-27-2020"></a>27 mars 2020

Vi har lagt till vägledning om de första prenumerationer som du bör skapa när du inför Azure.

### <a name="ready-updates"></a>Klara uppdateringar

| Artikel                                                                                                                 | Beskrivning                                                                                                                                                                                |
|-------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Skapa dina första Azure-prenumerationer](../ready/azure-best-practices/initial-subscriptions.md)                       | **Ny artikel:** Skapa dina första produktions-och ej produktions prenumerationer och bestäm om du vill skapa sandbox-prenumerationer, samt en prenumeration som innehåller delade tjänster. |
| [Skapa ytterligare prenumerationer för att skala din Azure-miljö](../ready/azure-best-practices/scale-subscriptions.md) | Läs om varför du kan skapa ytterligare prenumerationer, flytta resurser mellan prenumerationer och tips för att skapa nya prenumerationer.                                                   |
| [Organisera och hantera flera Azure-prenumerationer](../ready/azure-best-practices/organize-subscriptions.md)             | Skapa en hierarki för hanterings grupper som hjälper dig att organisera, hantera och styra dina Azure-prenumerationer.                                                                                         |

## <a name="march-20-2020"></a>20 mars 2020

Vi har lagt till vägledning som innehåller verktyg, program och innehåll kategoriserade av persona för att driva en lyckad distribution av program på Kubernetes, från koncept bevis till produktion, följt av skalning och optimering.

### <a name="kubernetes"></a>Kubernetes

| Artikel                                                                                     | Beskrivning                                                                                                                                                                           |
|---------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Program utveckling och-distribution](../innovate/kubernetes/application-development.md) | **Ny artikel:** Innehåller check listor, resurser och bästa metoder för att planera program utveckling, konfigurera DevOps-pipelines och implementera site pålitlighet för Kubernetes. |
| [Kluster design och-åtgärder](../innovate/kubernetes/cluster-design-operations.md) | **Ny artikel:** Innehåller check listor, resurser och metod tips för kluster konfiguration, nätverks design, framtida skalbarhet, affärs kontinuitet och haveri beredskap för Kubernetes. |
| [Kluster-och program säkerhet](../innovate/kubernetes/cluster-application-security.md) | **Ny artikel:** Innehåller check listor, resurser och metod tips för Kubernetes säkerhets planering, produktion och skalning. |

## <a name="march-2-2020"></a>2 mars 2020

Som svar på feedback om kontinuitet i migrations metoden genom flera delar av moln implementerings ramverket, inklusive strategi, planera, redo och migrering, har vi gjort följande uppdateringar. Dessa uppdateringar är utformade för att göra det enklare för dig att förstå planering och införande av fin justeringar när du fortsätter med migreringen.

### <a name="strategy-updates"></a>Strategi uppdateringar

| Artikel                                                                       | Beskrivning                                                                                                                                    |
|-------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| [Balansera portföljen](../strategy/balance-the-portfolio.md)                 | Flyttade den här artikeln till tidigare i strategi metoden. Detta ger dig insyn i tanke processen tidigare i livs cykeln. |
| [Balansera&nbsp;konkurrerande&nbsp;prioriteringar](../strategy/balance-competing-priorities.md) | **Ny artikel:** Beskriver balansen mellan metoder för att under lätta din strategi.                                         |

### <a name="plan-updates"></a>Planera uppdateringar

| Artikel                                                             | Beskrivning                                                                                                                                                                           |
|---------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Utvärdering&nbsp;bästa&nbsp;praxis](../plan/contoso-migration-assessment.md) | Flyttade den här artikeln till det nya avsnittet "metod tips" i plan metodiken. Detta ger dig insyn i övningen för att utvärdera lokala miljöer tidigare i livs cykeln. |

### <a name="ready-updates"></a>Klara uppdateringar

| Artikel                                                                   | Beskrivning                                                                                                              |
|---------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| [Vad&nbsp;&nbsp;en&nbsp;landning&nbsp;zon?](../ready/landing-zone/index.md)                 | **Ny artikel:** Definierar periodens landnings zon.                                                                          |
| [Första landnings zon](../ready/landing-zone/first-landing-zone.md)         | **Ny artikel:** Expanderar jämförelsen av olika landnings zoner.                                                     |
| [Migrera landnings zon](../ready/landing-zone/migrate-landing-zone.md)     | Separera definitionen av moln antagande ramverkets skiss från valet av den första landnings zonen.         |
| [Terraform landnings zon](../ready/landing-zone/terraform-landing-zone.md) | Flyttas till den nya avsnittet landnings zon i den färdiga metoden, för att höja terraform i landnings zon konversationen. |

### <a name="migration-updates"></a>Migrerings uppdateringar

| Artikel                                                                                          | Beskrivning                                                                                                                                                             |
|--------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Översikt](../migrate/azure-migration-guide/index.md)                                            | Uppdaterad med en tydligare Beskrivning av guiden och färre steg.                                                                                                        |
| [Beräknas](../migrate/azure-migration-guide/assess.md)                                             | Avsnittet "utmanande antaganden" har lagts till för att demonstrera hur den här utvärderings nivån fungerar med den stegvisa utvärderings metoden som anges i plan metodiken. |
| [Klassificering under utvärderings processer](../migrate/migration-considerations/assess/classify.md) | **Ny artikel:** Beskriver vikten av att klassificera varje till gång och arbets belastning innan migreringen.                                                                    |
| [Migrera](../migrate/azure-migration-guide/migrate.md)                                           | Lade till en referens till UnifyCloud i verktyg från tredje part, som svar på feedback på nivå 1-konferenser.                                                         |
| [Testa,&nbsp;optimera,&nbsp;och&nbsp;befordra](../migrate/azure-migration-guide/optimize-and-transform.md)        | Justera rubriken för den här artikeln med andra förslag på förbättringar av processen.                                                                                           |
| [Utvärderings översikt](../migrate/migration-considerations/assess/index.md)                           | Uppdaterat för att illustrera att utvärderingen i den här fasen fokuserar på att utvärdera den tekniska anpassningen av en speciell arbets belastning och relaterade till gångar.                               |
| [Checklista för planering](../migrate/migration-considerations/prerequisites/planning-checklist.md)    | Uppdaterat för att klargöra vikten av åtgärds justering under planeringen för migreringen för att säkerställa en väl hanterad arbets belastning efter migreringen.                  |

<!-- test:ignoreNextStep -->
