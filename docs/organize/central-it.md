---
title: Centrala IT-funktioner
description: Lär dig mer om bildande av centrala IT-funktioner.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: c5dc7212fc20914fddaa7bd8777a5fec5f49e811
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78225408"
---
# <a name="central-it-capabilities"></a>Centrala IT-funktioner

Som en skalning i molnet kanske moln styrnings funktioner inte räcker till för att reglera antagande ansträngningar. När antagandet är gradvis, tenderar teamen att utveckla de kunskaper och processer som behövs för molnet över tid.

Men när ett moln antagande team använder molnet för att uppnå affärs resultat med hög profil, är den gradvisa användningen sällan. Lyckades efter lyckad. Detta gäller även för moln införande, men det sker i moln skala. När moln införande utökas från ett team till flera team relativt snabbt, krävs ytterligare support från befintlig IT-personal. Dessa personal medlemmar kan dock sakna den utbildning och erfarenhet som krävs för att stödja molnet med molnbaserade IT-verktyg. Detta driver ofta bildande av ett centralt IT-team som styr molnet.

> [!CAUTION]
> Även om det här är ett vanligt förfallo steg, kan det utgöra en hög risk för att anta, eventuellt blockera innovationer och migrering av migrering om de inte hanteras effektivt. Se avsnittet risk nedan för att lära dig hur du kan minska risken för att centralisering blir ett kulturellt antimönster.

## <a name="possible-sources-for-central-it-expertise"></a>Möjliga källor för centrala IT-kunskaper

De kunskaper som krävs för att tillhandahålla centraliserade IT-funktioner kan tillhandahållas av:

- En befintlig central IT-grupp
- Enterprise-arkitekter
- IT-åtgärder
- IT-styrning
- IT-infrastruktur
- Nätverk
- Identitet
- Virtualisering
- Affärskontinuitet och haveriberedskap
- Program ägare i det

> [!WARNING]
> Central IT bör endast tillämpas i molnet när befintliga lokala leveranser baseras på en central IT-modell. Om den aktuella lokala modellen baseras på delegerad kontroll, bör du överväga ett CCoE-system (Cloud Center of expert) för ett mer kompatibelt alternativ.

## <a name="key-responsibilities"></a>Viktiga ansvars områden

Anpassa befintliga IT-rutiner för att se till att implementeringen leder till resultat i välstyrda och välhanterade miljöer i molnet.

Följande aktiviteter körs vanligt vis regelbundet:

### <a name="strategic-tasks"></a>Strategiska uppgifter

- Beakta
  - [affärs resultat](../strategy/business-outcomes/index.md)
  - [finansiella modeller](../strategy/financial-models.md)
  - [motivation för moln införande](../strategy/motivations.md)
  - [affärs risker](../govern/policy-compliance/risk-tolerance.md)
  - [rationalisering av den digitala fastigheten](../digital-estate/index.md)
- Övervaka implementerings planer och framsteg mot den [prioriterade migreringen](../migrate/migration-considerations/assess/release-iteration-backlog.md).
- Identifiera och prioritera plattforms ändringar som krävs för att stödja efter släpning i migreringen.
- Agera som mellanhand eller översättnings lager mellan moln implementerings behov och befintliga IT-team.
- Utnyttja befintliga IT-team för att påskynda plattforms funktionerna och aktivera införande.

### <a name="technical-tasks"></a>Tekniska uppgifter

- Bygg och underhålla moln plattformen för att stödja lösningar.
- Definiera och implementera plattforms arkitekturen.
- Använda och hantera moln plattformen.
- Förbättra plattformen kontinuerligt.
- Håll dig uppdaterad med nya innovationer i moln plattformen.
- Leverera nya moln funktioner som stöder skapande av affärs värde.
- Föreslå självbetjänings lösningar.
- Se till att lösningarna uppfyller befintliga styrnings-och efterlevnads krav.
- Skapa och validera distribution av plattforms arkitektur.
- Granska versions planer för källor med nya plattforms krav.

## <a name="meeting-cadence"></a>Mötes takt

Centrala IT-kunskaper kommer vanligt vis från en arbets grupp. Vi förväntar sig att deltagarna genomför mycket av sina dagliga scheman för att justera insatserna. Bidragen är inte begränsade till möten och feedback-cykler.

## <a name="central-it-risks"></a>Centrala IT-risker

Var och en av moln funktionerna och faserna i organisationens mognad är prefixet "Cloud". Central IT är det enda undantaget. Den centrala IT-avdelningen blev vanligare när alla IT-tillgångar skulle kunna lagras på några platser, hanteras av ett litet antal team och styras via en enda Operations Management-plattform. Globala affärs metoder och den digitala ekonomin har i stort sett färre instanser av de centralt hanterade miljöerna.

I den moderna vyn av IT är till gångar globalt distribuerade. Ansvars områden delegeras. Drift hantering levereras av en blandning av intern personal, hanterade tjänste leverantörer och moln leverantörer. I den digitala ekonomin övergår IT-hanterings praxis till en modell av självbetjänings-och delegerad kontroll med Clear guardrails för att genomdriva styrning. Central IT kan vara en värdefull bidrags givare till moln implementeringen genom att bli en moln hanterare och en partner för innovation och affärs flexibilitet.

Den centrala IT-funktionen är väl placerad för att ta värdefull kunskap och praxis från befintliga lokala modeller och tillämpa dessa metoder på moln leverans. Den här processen kommer dock att kräva ändringar. Nya processer, nya kunskaper och nya verktyg krävs för att stödja moln införande i stor skala. När centrala IT-anpassningar blir det en viktig partner i moln implementerings ansträngningar. Men om centrala IT inte anpassar sig till molnet, eller försöker använda molnet som en katalysator för täta kärnor, blir centrala IT-blocket snabbt till en blockerare att införa, innovation och migrering.

Måtten på denna risk är snabba och flexibla. Molnet gör det enklare att snabbt använda nya tekniker. När nya moln funktioner kan distribueras inom några minuter, men centrala IT-recensioner lägger till veckor eller månader i distributions processen, blir dessa centraliserade processer ett stort hinder för affärs framgångar. När den här indikatorn har påträffats bör du överväga alternativa strategier för IT-leverans.

### <a name="exceptions"></a>Undantag

Många branscher kräver en stelhet mot tredje parts efterlevnad. Vissa krav på efterlevnaden kräver fortfarande central IT-kontroll. Genom att leverera dessa efterlevnad kan du lägga till tid till distributions processer, särskilt för nya tekniker som inte har använts på ett brett sätt. I dessa scenarier förväntas förseningar i distributionen under de tidiga stegen som antas. Liknande situationer finns mitt för företag som hanterar känslig kund information, men som kanske inte styrs av ett krav för en tredje part.

### <a name="operate-within-the-exceptions"></a>Arbeta inom undantagen

När centraliserade IT-processer krävs och dessa processer skapar lämpliga kontroll punkter för att införa nya tekniker, kan dessa Innovations kontroll punkter fortfarande åtgärdas snabbt. Krav på styrning och efterlevnad är utformade för att skydda de saker som är känsliga, inte att skydda allt. Molnet innehåller enkla mekanismer för att förvärva och distribuera isolerade resurser samtidigt som du behåller rätt guardrails.

En vuxen central IT-grupp har nödvändiga skydd, men förhandlar om praxis som fortfarande aktiverar innovation. Att demonstrera den här nivån av förfallo nivåer beror på lämplig klassificering och isolering av resurser.

### <a name="example-narrative-of-operating-within-exceptions-to-empower-adoption"></a>Exempel på olika slag av drift inom undantag för att kunna införas

Det här exemplet illustrerar den metod som en vuxen central IT-grupp har vidtagit för att kunna vidta åtgärder.

Contoso har LLC infört en central IT-modell för support för företagets moln resurser. För att leverera den här modellen har de implementerat tätt kontroller för olika delade tjänster, t. ex. inkommande nätverks anslutningar. Den här åtgärden förminskar exponeringen för moln miljön och tillhandahöll en enda "Break-glas"-enhet för att blockera all trafik i händelse av en överträdelse. Deras principer för säkerhets bas linjen är att all inkommande trafik måste komma via en delad enhet som hanteras av centrala IT-teamet.

Men en av deras moln antagande team kräver nu en miljö med en dedikerad och särskilt konfigurerad ingångs nätverks anslutning för att använda en viss moln teknik. Ett inmogna central IT-team skulle bara neka begäran och prioritera sina befintliga processer vid implementerings behov. Contosos centrala IT-team är annorlunda. De identifierade snabbt en enkel lösning med fyra delar till denna dilemma: klassificering, förhandling, isolering och automatisering.

**Klassificering:** Eftersom moln implementerings teamet var i det tidiga skedet av att skapa en ny lösning och inte hade några känsliga data eller verksamhets kritiska support behov, klassificeras till gångarna i miljön som låg risk och icke-kritisk. En effektiv klassificering är ett tecken på förfallo tid i Central IT. Att klassificera alla till gångar och miljöer gör det möjligt att göra mer tydligare principer.

**Förhandling:** Enbart klassificeringen räcker inte. Delade tjänster implementerades för att konsekvent hantera känsliga och verksamhets kritiska till gångar. Att ändra reglerna skulle påverka styrnings-och efterlevnadsprinciper som har utformats för till gångar som behöver mer skydd. En bättre införande kan inte ske med kostnaden för stabilitet, säkerhet eller styrning. Detta ledde till en förhandling med antagande teamet för att svara på vissa frågor. Kan ett företags LED DevOps-team tillhandahålla drifts hantering för den här miljön? Behöver den här lösningen direkt åtkomst till andra interna resurser? Om moln implementerings teamet är bekväm med dessa kompromisser kan ingångs trafiken vara möjlig.

**Isolering:** Eftersom företaget kan ge sin egen pågående drift hantering, och eftersom lösningen inte förlitar sig på direkt trafik till andra interna till gångar, kan det vara avspärradet i en ny prenumeration. Den prenumerationen läggs också till i en separat nod i den nya hanterings gruppens hierarki.

**Automation:** En annan Sign of mognad i det här teamet är sina automatiserings principer. Teamet använder Azure Policy för att automatisera princip tillämpning. De använder också Azure-ritningar för att automatisera distributionen av vanliga plattforms komponenter och tillämpa den definierade identitets bas linjen. För den här prenumerationen och andra i den nya hanterings gruppen skiljer sig principerna och mallarna något. Principer som blockerar inkommande bandbredd har lyfts upp. De har ersatts av krav för att dirigera trafik genom prenumerationen för delade tjänster, som all inkommande trafik, för att upprätthålla trafik isolering. Eftersom verktyget för lokal Operations Management inte kan komma åt den här prenumerationen, krävs agenter för verktyget inte längre. Alla andra styrnings guardrails som krävs av andra prenumerationer i hanterings gruppens hierarki upprätthålls fortfarande, vilket säkerställer tillräckligt med guardrails.

Den mogna kreativa metoden i Contosos centrala IT-team tillhandahöll en lösning som inte äventyrade styrningen eller efterlevnaden, men som fortfarande uppmuntras att antas. Den här metoden för Broker i stället för att äga molnbaserade metoder för att centralisera det är det första steget för att skapa ett verkligt CCoE (Cloud Center of expert). Att använda den här metoden för att snabbt utveckla befintliga principer ger centraliserad kontroll vid behov och styrning guardrails när mer flexibilitet är acceptabel. Att balansera dessa två saker minimerar riskerna som är kopplade till centrala IT i molnet.

## <a name="next-steps"></a>Nästa steg

Som en central IT-vuxen i molnet är nästa dags-steg vanligt vis en fri koppling av [moln åtgärder](./cloud-operations.md). Tillgängligheten för Cloud-Native Operations Management-verktyg och lägre drifts kostnader för PaaS-första lösningar leder ofta till affärs team (eller mer specifikt DevOps team inom företaget) som förutsätter ansvar för moln drift.

> [!div class="nextstepaction"]
> [Moln drifts funktion](./cloud-operations.md)
