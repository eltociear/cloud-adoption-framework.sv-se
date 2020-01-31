---
title: Tillämpa design principer och avancerade åtgärder
description: Tillämpa design principer och avancerade åtgärder
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 16762a0eae366c3bf1cd578faaf52df60e6c97b1
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807690"
---
# <a name="apply-design-principles-and-advanced-operations"></a>Tillämpa design principer och avancerade åtgärder

De tre första molnhanteringsdisciplinerna beskriver en baslinje för hantering. En hanterings bas linje bör minst omfatta ett standard affärs åtagande för att minimera affärs avbrott och påskynda återställning om tjänsten avbryts. De flesta hanterings bas linjer omfattar en fokuserad fokus på att underhålla "inventering och synlighet", "operativa krav" och "skydd och återställning".

Syftet med en hanterings bas linje är att skapa ett enhetligt erbjudande som ger en minimi nivå av affärs åtagande för alla arbets belastningar som stöds. Den här bas linjen för vanliga, upprepnings bara hanterings erbjudanden gör det möjligt för teamet att tillhandahålla en mycket optimerad drift hanterings nivå med minimal avvikelse. Men det är inte säkert att standard erbjudandet ger företaget ett omfattande tillräckligt åtagande.

Diagrammet i nästa avsnitt illustrerar tre sätt att gå förbi hanterings bas linjen.

Hanterings bas linjen bör uppfylla minimi kravet på 80 procent av de lägsta kritiska arbets belastningarna i portföljen. Bas linjen ska inte användas för verksamhets kritiska arbets belastningar. Eller bör inte tillämpas på vanliga plattformar som delas mellan arbets belastningar. Dessa arbets belastningar kräver fokus på design principer och avancerade åtgärder.

## <a name="advanced-operations-options"></a>Avancerade åtgärds alternativ

Det finns tre föreslagna sökvägar för att förbättra affärs åtaganden utanför hanterings bas linjen, som du ser i följande diagram:

![Avancerade åtgärder](../_images/manage/beyond-the-baseline.png)

## <a name="enhanced-management-baseline"></a>Utökad hanterings bas linje

Som beskrivs i hanterings guiden för Azure använder en förbättrad hanterings bas linje molnbaserade verktyg för att förbättra drift tiden och minska återställnings tiderna. Förbättringarna är viktiga, men mindre än med arbets belastnings-eller plattforms specialisering. Fördelen med en förbättrad hanterings bas linje är den lika stora minskningen av kostnaderna och implementerings tiden.

## <a name="management-specialization"></a>Hanterings specialisering

Aspekter av arbets belastning och plattforms åtgärder kan kräva ändringar i design-och arkitektur principer. Dessa ändringar kan ta tid och leda till ökade drifts kostnader. Om du vill minska antalet arbetsbelastningar som kräver sådana investeringar kan en förbättrad baslinje för hantering tillhandahålla en tillräcklig förbättring av åtagandet.

För arbets belastningar som garanterar en högre investering för att uppfylla ett affärs åtagande är specialisering av drifts nyckel.

## <a name="areas-of-management-specialization"></a>Områden för hantering av specialisering

Det finns två områden i specialisering:

- **Plattforms-specialisering:** Investera i pågående drift av en delad plattform och distribuera investeringen över flera arbets belastningar.
- **Specialisering för arbets belastning:** Investera i pågående drift av en speciell arbets belastning, vanligt vis reserverat för verksamhets kritiska arbets belastningar.

### <a name="central-it-or-cloud-center-of-excellence-ccoe"></a>Central IT-eller moln Center med hög kvalitet (CCoE)

Beslut mellan plattforms specialisering och arbets belastnings specialisering baseras på den kritiskaheten och effekten av varje arbets belastning. Dessa beslut är dock också väg LED ande av större kultur beslut mellan centrala IT-och CCoE organisations modeller.

Specialiseringen för arbetsbelastningar utlöser ofta en kulturell förändring. Traditionell IT och central IT skapar både processer som kan ge stöd i stor skala. Skalnings stödet är bättre för repeterbara tjänster som finns i en hanterings bas linje, förbättrad bas linje eller till och med plattforms åtgärder. Arbets belastnings specialisering skalar ofta inte. Denna brist på skalning gör det svårt för en centraliserad IT-organisation att tillhandahålla nödvändig support utan att nå begränsningar för organisations skalning.

Ett moln Center med expert metoder kan skalas genom ändamålsenlig delegering av ansvar och selektiv centralisering. Arbets belastnings specialiseringen är ett bra sätt att justera med den delegerade ansvars metoden för en CCoE.

Den naturliga justeringen av roller i en CCoE beskrivs på följande sätt:

- Moln plattforms teamet hjälper till att bygga vanliga plattformar som stöder flera moln antagande team.
- Cloud Automation-teamet utökar plattformarna till distributions bara till gångar i en tjänst katalog.
- Cloud Management levererar hanterings bas linjen centralt och hjälper till att stödja användningen av tjänst katalogen.
- Men affär senheten (i form av ett DevOps team eller ett moln antagande team) innehåller ansvar för dagliga åtgärder för arbets belastningen, pipelinen eller prestandan.

När det gäller justeringen av hanterings områden kan centrala IT-och CCoE-modeller vanligt vis levereras på plattforms-specialisering, med minimal kulturell förändring. Att leverera på arbets belastnings specialisering kan vara lite mer komplext för centrala IT-team.

## <a name="management-specialization-processes"></a>Hantering av specialiserings processer

I varje specialisering levereras följande fyra stegs process i en disciplin, iterativ metod. Den här metoden kräver samarbete mellan moln införande, moln plattform, moln automatisering och moln hanterings experter för att skapa en livskraftig och välgrundad feedback-slinga.

- **Förbättra system design:** Förbättra utformningen av vanliga system (plattformar) eller vissa arbets belastningar för att effektivt minimera avbrott.
- **Automatiserad reparation:** Vissa förbättringar är inte kostnads effektiva. I sådana fall kan det vara mer meningsfullt att automatisera reparationen och minska effekten av avbrott.
- **Skala lösningen:** När system design och automatiserad reparation har förbättrats kan du skala dessa ändringar i miljön via tjänst katalogen.
- **Kontinuerlig förbättring:** Du kan använda olika övervaknings verktyg för att upptäcka stegvisa förbättringar av hur du kan lösa det i nästa steg av system design, automatisering och skalning.

### <a name="improve-system-design"></a>Förbättra systemdesignen

Att förbättra systemdesignen är den mest effektiva metoden för att förbättra driften av en plattform. Förbättringar av system design hjälper till att öka stabiliteten och minska affärs avbrott. Utformningen av enskilda system ligger utanför omfånget för det miljöperspektiv som utgör utgångspunkten i Cloud Adoption Framework. Som komplement till det här ramverket innehåller Azure-arkitekturramverket metodtips för att förbättra återhämtningen för och utformningen av ett särskilt system. Du kan använda dessa design förbättringar i system Designen för en plattform eller en speciell arbets belastning.

Azure-arkitekturramverket fokuserar på förbättringar inom fem pelare för systemdesign:

- **Skalbarhet:** Skala vanliga plattforms till gångar för att hantera ökad belastning.
- **Tillgänglighet:** Minska affärs avbrott genom att förbättra drift tiden.
- **Återhämtning:** Förbättra återställnings tiderna för att minska tiden för avbrott.
- **Säkerhet:** Skydda program och data från externa hot.
- **Hantering:** Åtgärder som är speciella för dessa vanliga plattforms till gångar.

De flesta driftavbrotten beror på någon form av teknisk skuld eller brist i arkitekturen. För befintliga distributioner kan förbättringar av systemdesignen ses som ett sätt att betala av den tekniska skulden. För nya distributioner kan förbättringar av systemdesignen ses som ett sätt att undvika att hamna i teknisk skuld. Nästa avsnitt, "automatiserad reparation", ser ut på olika sätt att åtgärda tekniska skulder som inte kan eller behöver åtgärdas.

Läs mer om [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/guide/pillars)för att hjälpa till att förbättra system Designen. När system Designen förbättras kan du gå tillbaka till den här artikeln för att hitta nya möjligheter att förbättra och skala förbättringarna i din miljö.

### <a name="automated-remediation"></a>Automatiserad reparation

Vissa tekniska skulder får eller behöver inte åtgärdas. Det kan vara för dyrt att lösa problemet. Det kan planeras, men det kan vara en lång projekt varaktighet. Affärs avbrott kanske inte har en betydande inverkan på verksamheten, eller så är affärs prioriteten att återställa snabbt i stället för att investera i återhämtning.

Om en lösning av den tekniska skulden inte är önskad väg att gå är automatiserad reparation ett vanligt nästa steg. Att använda Azure Automation och Azure Monitor för att identifiera trender och tillhandahålla automatiserad reparation är den vanligaste metoden när det gäller automatisk reparation.

Vägledning om automatiserad reparation finns i [Azure Automation och aviseringar](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

### <a name="scale-the-solution-with-a-service-catalog"></a>Skala lösningen med en tjänstkatalog

Hörnstenen för plattformsspecialisering och plattformsdrift är en välhanterad tjänstkatalog. Det är så förbättringar av systemdesignen och reparationer skalas ut i en miljö. Molnplattformsteamet och molnautomatiseringsteamet samarbetar för att skapa upprepningsbara lösningar för vanliga plattformar i alla miljöer. Men om dessa lösningar inte används konsekvent, kan moln hantering tillhandahålla lite mer än ett bas linje erbjudande.

För att maximera införandet och minimera underhålls kostnaderna för en optimerad plattform bör plattformen läggas till i en tjänst katalog. Varje program i katalogen kan distribueras för intern användning via tjänstkatalogen eller som ett Marketplace-erbjudande för externa konsumenter.

Information om hur du publicerar till en tjänst katalog finns i serien om [publicering till en tjänst katalog](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="continuous-improvement"></a>Kontinuerliga förbättringar

Plattformsspecialiseringen och plattformsdriften är båda beroende av starka feedbackslingor mellan införande-, plattforms-, automatiserings- och hanteringsteamen. Genom att lägga till dessa feedbackslingor i data får varje team möjlighet att fatta kloka beslut. För plattforms åtgärder för långsiktiga affärs åtaganden är det viktigt att dra nytta av insikter som är specifika för den centrala plattformen. Eftersom behållare och SQL Server är de två vanligaste centralt hanterade plattformarna bör du tänka på att komma igång med data insamling för kontinuerlig förbättring genom att läsa följande artiklar:

- [Prestanda för containrar](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview)
- [Prestanda för PaaS-databaser](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql)
- [Prestanda för IaaS-databaser](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
