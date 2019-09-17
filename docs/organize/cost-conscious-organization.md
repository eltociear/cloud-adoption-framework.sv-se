---
title: Skapa en kostnads medveten organisation
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig metod tips för att skapa en kostnads medveten organisation.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.openlocfilehash: 88944a786bb783d1a2e4bf651c142b8148b0dd2e
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71029923"
---
# <a name="building-a-cost-conscious-organization"></a>Skapa en kostnads medveten organisation

Som beskrivs i [motivation: Varför flyttar vi till molnet? ](../strategy/motivations.md)finns det många olika ljud orsaker för ett företag att anta molnet. När kostnads minskning är en primär driv rutin är det viktigt att skapa en kostnads medveten organisation.

Att se till att kostnaderna inte är en engångs aktivitet. Precis som andra moln införande ämnen är det iterativt. Följande diagram beskriver den här processen för att fokusera på tre beroende aktiviteter: *synlighet*, *ansvar*och *optimering*. De här processerna spelas upp på makro-och mikronivå, som vi beskriver i detalj i den här artikeln.

![Kostnads medveten process](../_images/ready/cost-optimization-process.png)
*figur 1 – en översikt över den kostnads medvetna organisationen.*

## <a name="general-cost-conscious-processes"></a>Allmänna kostnads medvetna processer

- **Insyn** För att en organisation ska kunna vara medveten om kostnaderna behöver den insyn i dessa kostnader. Insyn i en kostnads medveten organisation kräver konsekvent rapportering för de team som inför molnet, ekonomi team som hanterar budgetar och hanterings team som ansvarar för kostnaderna. Den här synligheten görs genom att upprätta:
  - Rätt rapporterings omfång.
  - Korrekt resurs organisation (hanterings grupper, resurs grupper, prenumerationer).
  - Rensa taggnings strategier.
  - Lämpliga åtkomst kontroller (RBAC).

- **Accountability** Ansvaret är lika viktigt som synligheten. Ansvaret börjar med tydliga budgetar för antagande ansträngningar. Budgetarna bör vara väl upprättade, tydligt kommunicerade och baseras på realistiska förväntningar. Ansvaret kräver en iterativ process och en tillväxt tänkesätt för att driva den rätta ansvars nivån.

- **Optimering** Optimering är den åtgärd som skapar kostnads minskningar. Under optimeringen ändras resurs tilldelningar för att minska kostnaderna för att stödja olika arbets belastningar. Den här processen kräver iteration och experimentering. Varje minskning av kostnaderna minskar prestandan. Att hitta rätt balans mellan kostnads kontroll och prestanda förväntningar för slutanvändare kräver indata från flera parter.

I följande avsnitt beskrivs de roller som *moln strategi teamet*, *moln implementerings teamet,* *moln styrnings*teamet och CCoE ( *Cloud Center of expert* ) spelar för att utveckla en kostnads medveten organisation.

## <a name="cloud-strategy-team"></a>Moln strategi team

Att skapa kostnader för moln implementerings ansträngningar börjar på ledarskaps nivå. För att vara effektiv långsiktig bör [moln strategi teamet](./cloud-strategy.md) omfatta en medlem i ekonomi teamet. Om din finansiella struktur innehåller affärs chefer som är ansvariga för lösnings kostnader bör de inbjudas att ansluta till teamet. Förutom de kärn aktiviteter som vanligt vis tilldelats moln strategi teamet bör alla medlemmar i moln strategi teamet även vara ansvariga för:

- **Insyn** Moln strategi teamet och [moln styrnings teamet](./cloud-governance.md) behöver veta de faktiska kostnaderna för moln implementeringen. Med tanke på den övergripande vyn över det här teamet bör de ha till gång till flera kostnads omfattningar för att analysera utgifts beslut. En chef behöver vanligt vis insyn i den totala kostnaden för alla moln "spendera". Men som aktiva medlemmar i moln strategi teamet bör de också kunna visa kostnader per affär senhet eller per fakturerings enhet för att verifiera showback, åter betalning eller andra [modeller för moln redovisning](../strategy/cloud-accounting.md).

- **Accountability** Budgetarna bör upprättas mellan moln strategin, [moln styrning](./cloud-governance.md)och [moln implementerings](./cloud-adoption.md) team baserat på förväntade införande aktiviteter. När avvikelser från budget inträffar, måste moln strategi teamet och moln styrnings gruppen samar beta för att snabbt fastställa bästa möjliga åtgärd för att åtgärda avvikelser.

- **Optimering** Under optimerings ansträngningar kan moln strategi teamet representera investeringen och returvärdet för särskilda arbets belastningar. Om en arbets belastning har ett strategiskt värde eller finansiell påverkan på verksamheten bör kostnader för kostnads optimering övervakas noga. Om organisationen inte har någon strategisk påverkan och ingen inbyggd kostnad för dåliga prestanda för en arbets belastning kan moln strategi teamet godkänna överoptimering. För att kunna köra dessa beslut måste teamet kunna visa kostnader för en projekt omfattning per projekt.

## <a name="cloud-adoption-team"></a>Moln antagande team

[Moln implementerings teamet](./cloud-adoption.md) är i mitten av alla införande aktiviteter. Därför är de den första försvars linjen mot överförbrukning. Det här teamet har en aktiv roll i alla tre faser av kostnads medvetslöshet.

- **Insyn**

  - **Medvetenhet** Det är viktigt att moln implementerings teamet har insyn i de kostnads besparande målen i arbetet. Genom att bara ange att moln implementerings ansträngningen bidrar till att minska kostnaderna är ett recept för fel. En *speciell* synlighet är viktig. Om målet till exempel är att minska Data Center TCO med 3 procent eller årliga drifts kostnader med 7 procent, avslöja dessa mål tidigt och tydligt.
  - **Telemetridata** Det här teamet behöver insyn i konsekvenserna av sina beslut. Under migrerings-eller Innovations aktiviteter har deras beslut direkt påverkan på kostnader och prestanda. Teamet måste balansera dessa två konkurrerande faktorer. Prestanda övervakning och kostnads övervakning som är begränsade till teamets aktiva projekt är viktiga för att tillhandahålla nödvändig synlighet.

- **Accountability** Moln implementerings gruppen måste vara medveten om alla förinställda budgetar som är associerade med deras antagande ansträngningar. När verkliga kostnader inte överensstämmer med budgeten, finns det en möjlighet att skapa ansvar. Ansvars skyldigheten är inte lika med att göra gruppen för antagande för att överskrida budgeten, eftersom budget överskott kan orsakas av nödvändiga beslut. Ansvaret innebär i stället att utbilda teamet om målen och hur deras beslut påverkar dessa mål. Ansvaret innehåller dessutom en dialog ruta där teamet kan kommunicera om beslut som ledde till överförbrukning. Om dessa beslut är feljusterade med målen för projektet ger denna ansträngning en bra möjlighet att samar beta med moln strategi teamet för att fatta bättre beslut.

- **Optimering** Den här ansträngningen är en balanserings åtgärd eftersom resursernas optimering kan minska prestandan för de arbets belastningar som de stöder. Ibland kan förväntade eller budgeterade besparingar inte realiseras för en arbets belastning eftersom arbets belastningen inte presterar tillräckligt med de budgeterade resurserna. I dessa fall måste moln antagande teamet fatta beslut och rapportera ändringar i moln strategi teamet och moln styrnings teamet så att budget eller optimerings beslut kan åtgärdas.

## <a name="cloud-governance-team"></a>Team för moln styrning

I allmänhet ansvarar [moln styrnings teamet](./cloud-governance.md) för kostnads hantering i hela molnet. Som beskrivs i avsnittet om [kostnad för hanterings disciplin](../govern/cost-management/index.md) i moln implementerings ramverkets styrnings metod är Cost Management det första av de fem disciplinerna i moln styrningen. De här artiklarna beskriver en serie djupare ansvar för gruppen för moln styrning.

Den här ansträngningen fokuserar på följande aktiviteter som är relaterade till utvecklingen av en kostnads medveten organisation:

- **Insyn** Moln styrnings teamet fungerar som en peer i moln strategi teamet för att planera moln införande budgetar. Dessa två team arbetar också tillsammans för att regelbundet granska faktiska kostnader. Moln styrnings teamet ansvarar för att säkerställa konsekvent, tillförlitlig kostnads rapportering och prestanda telemetri.

- **Accountability** När budget avvikelser inträffar måste moln strategi teamet och moln styrnings gruppen samar beta för att snabbt fastställa bästa möjliga åtgärd för att åtgärda avvikelser. I allmänhet kommer moln styrnings teamet att agera på dessa beslut. Ibland kan åtgärden vara enkel omskolning för det berörda [moln antagande teamet](./cloud-adoption.md). Moln styrnings teamet kan också hjälpa till att optimera distribuerade till gångar, ändra rabatt alternativ, eller till och med implementera alternativ för automatisk kostnads kontroll som att blockera distribution av oplanerade till gångar.

- **Optimering** När till gångar har migrerats till eller skapats i molnet kan du använda övervaknings verktyg för att utvärdera prestanda och användning av dessa till gångar. Korrekt övervaknings-och prestanda data kan identifiera till gångar som ska optimeras. Moln styrnings teamet ansvarar för att säkerställa att övervaknings-och kostnads rapporterings verktygen distribueras konsekvent. De kan också hjälpa implementerings teamen att identifiera möjligheter att optimera utifrån prestanda och kostnads telemetri.

## <a name="cloud-center-of-excellence"></a>Molncenter för utmärkthet

Även om det vanligt vis inte är ansvarigt för kostnads hantering kan CCoE ha stor inverkan på kostnadsmedvetna organisationer. Många grundläggande IT-beslut påverkar kostnader i stor skala. När CCoE gör sin del kan kostnader minskas för flera olika moln införande åtgärder.

- **Insyn** Alla hanterings grupper eller resurs grupper som är hus kärnor i IT-tillgångar bör vara synliga för CCoE-teamet. Teamet kan använda dessa data för att optimera affärs möjligheter.

- **Accountability** Även om det vanligt vis inte är ett konto för kostnad, kan CCoE inneha sig självt för att skapa upprepnings bara lösningar som minimerar kostnaderna och maximerar prestandan.

- **Optimering** Med tanke på CCoE synlighet för flera distributioner, är teamet i ett idealiskt läge för att föreslå optimerings tips och för att bidra till att förbättra till gångar.

## <a name="next-steps"></a>Nästa steg

Att under lätta dessa ansvars områden på varje nivå i verksamheten hjälper till att driva en kostnads medveten organisation. För att komma igång med den här vägledningen granskar du [organisationens beredskap](./index.md) för att hjälpa till att identifiera rätt team strukturer.

> [!div class="nextstepaction"]
> [Identifiera rätt team strukturer](./index.md)
