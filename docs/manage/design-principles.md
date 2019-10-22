---
title: Tillämpa design principer och avancerade åtgärder
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Tillämpa design principer och avancerade åtgärder
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 8595dbadf5a10e19303a50f8eead1ae753612586
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683571"
---
# <a name="apply-design-principles-and-advanced-operations"></a>Tillämpa design principer och avancerade åtgärder

De tre första moln hanterings disciplinerna beskriver en hanterings bas linje. En hanterings bas linje bör minst omfatta ett standard affärs åtagande för att minimera affärs avbrott och påskynda återställning om tjänsten avbryts. De flesta hanterings bas linjer omfattar en fokuserad fokus på att underhålla "inventering och synlighet", "operationell efterlevnad" och "skydd och återställning".

Syftet med en hanterings bas linje är att skapa ett enhetligt erbjudande som ger en minimi nivå av affärs åtagande för alla arbets belastningar som stöds. Den här bas linjen med vanliga upprepnings bara hanterings erbjudanden, gör det möjligt för teamet att tillhandahålla en mycket optimerad drift hanterings nivå med minimal avvikelse. Men det är inte säkert att standard erbjudandet ger företaget ett omfattande tillräckligt åtagande. Följande bild-och punkter-disposition tre sätt att gå bortom hanterings bas linjen.

Hanterings bas linjen bör uppfylla minimi kravet på 80% av de lägsta kritiska arbets belastningarna i portföljen. Bas linjen ska inte användas för verksamhets kritiska arbets belastningar. Eller bör inte tillämpas på gemensamma plattformar som delas mellan arbets belastningar. De kräver fokus på design principer och avancerade åtgärder.

## <a name="advanced-operations-options"></a>Avancerade åtgärds alternativ

Det finns tre föreslagna sökvägar för att förbättra affärs åtaganden bortom hanterings bas linjen.

![Avancerade åtgärder](../_images/manage/beyond-the-baseline.png)

## <a name="enhanced-management-baseline"></a>Utökad hanterings bas linje

Som beskrivs i hanterings guiden för Azure använder en förbättrad hanterings bas linje moln inbyggda verktyg för att förbättra drift tiden och minska återställnings tiden. Förbättringarna är betydande, men betydligt mindre än med arbets belastnings-eller plattforms specialisering. Fördelen med en förbättrad hanterings bas linje är den lika stora minskningen av kostnaderna och implementerings tiden.

## <a name="management-specialization"></a>Hanterings specialisering

Aspekter av arbets belastning och plattforms åtgärder kan kräva ändringar i design-och arkitektur principer. Dessa ändringar kan ta tid och leda till ökade drift kostnader. För att minska antalet arbets belastningar som kräver sådana investeringar kan en förbättrad hanterings bas linje tillhandahålla tillräckligt med en förbättring av affärs åtagandet.

För arbets belastningar som garanterar en högre investering för att uppfylla ett affärs åtagande är specialisering av drifts nyckel.

## <a name="areas-of-management-specialization"></a>Områden för hantering av specialisering

Det finns två områden i specialisering:

- **Plattforms-specialisering:** Investera i pågående drift av en delad plattform och distribuera investeringen över flera arbets belastningar.
- **Specialisering för arbets belastning:** Investera i pågående drift av en speciell arbets belastning, vanligt vis reserverat för verksamhets kritiska arbets belastningar.

### <a name="central-it-or-cloud-center-of-excellence-ccoe"></a>Central IT-eller moln Center med hög kvalitet (CCoE)

Beslut mellan plattforms specialisering och arbets belastnings specialisering baseras på den kritiskaheten och effekten av varje arbets belastning. Detta beslut kommer dock också att tyda på ett större kulturellt beslut mellan centrala IT-och CCoE organisations modeller.

Belastnings specialisering utlöser ofta en kulturell förändring. Traditionell IT och central IT skapar både processer som kan ge stöd i stor skala. Skalnings stödet är bättre för repeterbara tjänster som finns i en hanterings bas linje, förbättrad bas linje eller till och med plattforms åtgärder. Arbets belastnings specialisering skalar ofta inte. Denna brist på skalning gör det svårt för en centraliserad IT-organisation att tillhandahålla nödvändig support utan att nå begränsningar för organisations skalning.

Ett annat sätt är att moln centret kan skalas genom ändamålsenlig delegering av ansvar och selektiv centralisering. Arbets belastnings specialiseringen är ett bra sätt att justera med den delegerade ansvars metoden för en CCoE. I följande avsnitt beskrivs den naturliga justeringen av roller i en CCoE. Moln plattforms teamet hjälper till att bygga vanliga plattformar som stöder flera moln antagande team. Cloud Automation-teamet utökar de till distributions bara till gångar i en tjänst katalog. Cloud Management levererar hanterings bas linjen centralt och hjälper till att stödja användningen av tjänst katalogen. Men affär senheten (i form av ett DevOps team eller ett moln antagande team) innehåller ansvar för dagliga åtgärder för arbets belastningen, pipelinen eller prestandan.

När du justerar hanterings områden kan centrala IT-och CCoE-modeller vanligt vis levereras på plattforms-specialisering, med minimal kulturell förändring. Att leverera på arbets belastnings specialisering kan vara lite mer komplext för centrala IT-team.

## <a name="management-specialization-processes"></a>Hantering av specialiserings processer

I varje specialisering levereras följande fyra stegs process i en disciplin, iterativ metod. Den här metoden kräver partnerskap med moln införande, moln plattform, moln automatisering och moln hanterings experter för att skapa en livskraftig och välgrundad feedback-slinga.

- **Förbättra system design:** Förbättra utformningen av vanliga system (plattformar) eller vissa arbets belastningar för att effektivt minimera avbrott.
- **Automatiserad reparation:** Vissa förbättringar är inte kostnads effektiva. I sådana fall kan det vara mer meningsfullt att automatisera reparationen och minska effekten av avbrott.
- **Skala lösningen:** När system design och automatiserad reparation förbättras, kan dessa ändringar skalas över hela miljön via tjänst katalogen.
- **Kontinuerlig förbättring:** Olika övervaknings verktyg kan användas för att upptäcka stegvisa förbättringar som kan åtgärdas i nästa steg av system design, automation och Scale.

### <a name="improve-system-design"></a>Förbättra system design

Att förbättra system Designen är den mest effektiva metoden för att förbättra driften av en gemensam plattform. Genom förbättringar av system design kan stabiliteten öka och affärs avbrott minska. Utformningen av enskilda system ligger utanför omfånget för den miljömässiga vy som tas i moln införande ramverket. Som komplement till det här ramverket innehåller Azure Architecture Framework metod tips för att förbättra återhämtning och utformningen av ett särskilt system. Dessa design förbättringar kan tillämpas på system utformningen av en plattform eller en speciell arbets belastning.

Azure Architecture Framework fokuserar på förbättringar i fem pelare i system design:

- **Skalbarhet:** Skala vanliga plattforms till gångar för att hantera ökad belastning.
- **Tillgänglighet:** Minska affärs avbrott genom att förbättra drift tiden.
- **Återhämtning:** Förbättra återställnings tiden för att minska tiden för avbrott.
- **Säkerhet:** Skydda program och data från externa hot.
- **Hantering:** Åtgärder som är speciella för dessa vanliga plattforms till gångar.

De flesta affärs avbrott motsvarar någon form av teknisk skuld eller brist i arkitekturen. För befintliga distributioner kan system design förbättringar visas som betalningar mot befintlig teknisk skuld. För nya distributioner kan system design förbättringar visas som en snedvridning av den tekniska skulden. Nästa flik, "automatiserad reparation", ser ut på olika sätt att åtgärda tekniska skulder som inte kan eller behöver åtgärdas.

Lär dig mer om [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/guide/pillars) för att förbättra system Designen. När system Designen förbättras kan du gå tillbaka till den här artikeln för att hitta nya möjligheter att förbättra och skala förbättringarna i din miljö.

### <a name="automated-remediation"></a>Automatiserad reparation

En del teknisk skuld kan inte (eller borde) åtgärdas. Det kan vara dyrt att lösa problemet. Matchningen kan planeras, men har en lång projekt varaktighet. Det kan bero på att affärs avbrott inte har en betydande inverkan på verksamheten eller att affärs prioriteten kan återställas snabbt i stället för att investera i återhämtning.

När en lösning på teknisk skuld inte är den önskade sökvägen är den automatiserade reparationen vanligt vis det önskade nästa steget. Använd Azure Automation och Azure Monitor för att identifiera trender och tillhandahålla automatiserad reparation är den vanligaste metoden för automatisk reparation.

Vägledning om automatiserad reparation finns i den här artikeln om [Azure Automation och aviseringar](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

### <a name="scale-the-solution-with-a-service-catalog"></a>Skala lösningen med en tjänst katalog

Den viktigaste plattformen för plattforms-och plattforms åtgärder är en väl hanterad tjänst katalog. Detta är hur förbättringar av system design och reparationer skalas ut i en miljö. Moln plattforms teamet och moln automatiserings teamet anpassas för att skapa upprepnings bara lösningar för de vanligaste plattformarna i valfri miljö. Men om dessa lösningar inte ständigt utnyttjas kan moln hantering tillhandahålla lite mer än ett bas linje erbjudande.

För att maximera införandet och minimera underhålls kostnaderna för en optimerad plattform bör plattformen läggas till i en tjänst katalog. Varje program i katalogen kan distribueras för intern användning via tjänst katalogen eller som ett Marketplace-erbjudande för externa konsumenter.

Anvisningar om hur du publicerar till en tjänst katalog finns i artikel serien om [att publicera till en tjänst katalog](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="continuous-improvement"></a>Kontinuerlig förbättring

Plattforms-och plattforms åtgärder är både beroende av starka feedback-slingor mellan antagande, plattform, automatisering och hanterings team. Genom att lägga till dessa återkopplings slingor i data kan varje team fatta beslut. För plattforms åtgärder för långsiktiga affärs åtaganden är det viktigt att utnyttja insikter som är specifika för den centraliserade plattformen. Eftersom behållare och SQL Server är de två vanligaste centralt hanterade plattformarna, är följande artiklar som hjälper dig att komma igång med data insamling för kontinuerlig förbättring.

Prestanda för [Container](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview) 
[PaaS Database Performance](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql) 
[IaaS Database Performance](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
