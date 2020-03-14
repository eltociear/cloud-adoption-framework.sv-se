---
title: Spåra kostnader mellan affär senheter och miljöer
description: Använd ramverket för moln införande för Azure för att förstå beslut och implementerings metoder för att skapa spårnings mekanismer.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: b363d43568617d7c58003c2bd278008583870664
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79312689"
---
# <a name="track-costs-across-business-units-environments-or-projects"></a>Spåra kostnader för affärsenheter, miljöer och projekt

[Att skapa en kostnadsmedveten organisation](../../organize/cost-conscious-organization.md) kräver insyn och korrekt definierad åtkomst (eller omfång) till kostnadsrelaterad information. Dessa metodtips beskriver beslutsvägar och implementeringssätt för att skapa spårningsmekanismer.

![Översikt över en kostnadsmedveten process](../../_images/ready/cost-optimization-process.png)

## <a name="establish-a-well-managed-environment-hierarchy"></a>Upprätta en väl hanterad miljöhierarki

Kostnadskontroll, ungefär som styrning och andra hanteringsstrukturer, är beroende av en välhanterad miljö. Att upprätta en sådan miljö (särskilt en komplex sådan) kräver konsekventa processer när tillgångar klassificeras och organiseras.

Till gångar (även kallade resurser) inkluderar alla virtuella datorer, datakällor och program som distribueras till molnet. Azure tillhandahåller flera mekanismer för att klassificera och organisera tillgångar. [Skalning med flera Azure-prenumerationer](../azure-best-practices/scaling-subscriptions.md) beskriver alternativ för att organisera resurser baserat på flera kriterier och därmed skapa en välhanterad miljö. Den här artikeln fokuserar på Azures grundläggande koncept för insyn i molnkostnader.

### <a name="classification"></a>Klassificering

*Taggning* är ett enkelt sätt att klassificera tillgångar. Taggar associerar metadata med en tillgång. Dessa metadata kan användas för att klassificera tillgången baserat på olika datapunkter. När taggar används för att klassificera tillgångar som en del av ett kostnadshanteringsprojekt behöver företag ofta följande taggar: affärsenhet, avdelning, faktureringskod, geografisk plats, miljö, projekt och arbetsbelastning eller "programkategorisering". Azure Cost Management kan använda taggarna för att skapa olika vyer av kostnadsdata.

Taggning är ett grundläggande sätt att förstå data i alla kostnadsrapporter. Det utgör grunden för en välhanterad miljö. Det är också det första steget när du etablerar en lämplig styrning av vilken miljö som helst.

Det första steget i att noggrant spåra kostnadsinformation mellan affärsenheter, miljöer och projekt är att definiera en taggningsstandard. Nästa steg är att se till att taggningsstandarden används konsekvent. Följande artiklar kan hjälpa dig med dessa steg:

- [Utveckla standarder för namngivning och taggning](../azure-best-practices/naming-and-tagging.md)
- [Upprätta ett styrnings-MVP för att tillämpa taggningsstandarder](../../govern/guides/complex/index.md)

### <a name="resource-organization"></a>Resursorganisering

Det finns flera metoder för att organisera tillgångar. Det här avsnittet beskriver bästa praxis baserat på behoven hos ett stort företag med kostnadsstrukturer som är uppdelade i olika affärsenheter, geografiska områden och IT-organisationer. Ett liknande bästa tillvägagångs sätt för en mindre komplex organisation finns i [standard styrnings guiden för Enterprise](../../govern/guides/standard/index.md).

För ett stort företag skapar följande modell en hierarki för hanteringsgrupper, prenumerationer och resursgrupper som gör det möjligt för varje team att ha rätt insynsnivå för att utföra sina uppgifter. När företaget behöver kostnadskontroller för att förhindra budgetöverskridningar kan det använda styrningsverktyg som Azure-skisser eller Azure Policy för att snabbt förhindra framtida kostnadsfel.

![Diagram över resursorganisering för stort företag](../../_images/govern/large-enterprise-resource-organization.png)

I det föregående diagrammet innehåller roten i hanteringsgruppshierarki en nod för varje affärsenhet. I det här exemplet behöver det multinationella företaget insyn i de regionala affärsenheterna. Därför skapar de en geografinod under varje affärsenhet i hierarkin.

Det finns en separat nod för varje geografiskt område för produktions- och icke-produktionsmiljöer för att isolera kostnader, åtkomst och styrnings kontroller. För att möjliggöra mer effektiva drifts-och åtgärds investeringar, använder företaget prenumerationer för att ytterligare isolera produktionsmiljöer med varierande grad av prestandaåtaganden. Slutligen använder företaget resursgrupper för att avbilda distributionsbara enheter för en funktion som kallas program.

Diagrammet visar metodtips men omfattar inte följande alternativ:

- Många företag begränsar sin verksamhet till en enda geopolitisk region. Den metoden minskar behovet av att variera styrningsprinciperna eller kostnadsdata baserat på lokala krav om datasuveränitet. I dessa fall behövs ingen geografisk nod.
- Vissa företag föredrar att ytterligare åtskilja utvecklings-, testnings- och kvalitetskontrollmiljöer i separata prenumerationer.
- När ett företag integrerar ett CCoE-team (Cloud Center of Excellence) kan delade tjänstprenumerationer på varje geografisk nod minska dubblerade tillgångar.
- Mindre implementeringar kan använda en mycket mindre hanteringshierarki. Det är vanligt att se miljöer med en enda rotnod för företags-ID med en enda nivå av underordnade noder i hierarkin. Detta bryter inte mot metodtipsen för en välhanterad miljö. Men det blir svårare att tillhandahålla en åtkomstmiljö med minsta behörighet för kostnadskontroll och andra viktiga funktioner.

Resten av den här artikeln förutsätter att du använder metodtipsen i föregående diagram. Följande artiklar kan dock hjälpa dig att tillämpa metoden på en resursorganisation som passar ditt företag bäst:

- [Skalning med flera Azure-prenumerationer](../azure-best-practices/scaling-subscriptions.md)
- [Distribuera en styrningsMVP för att styra standarder för välhanterad miljö](../../govern/guides/complex/index.md)

## <a name="provide-the-right-level-of-cost-access"></a>Ange rätt nivå för kostnadsåtkomst

Kostnadshantering är en lagaktivitet. Avsnittet om organisationsberedskap i Ramverk för molnimplementering beskriver ett litet antal kärnteam och beskriver hur dessa team möjliggör molnimplementeringen. Den här artikeln expanderar gruppdefinitionerna för att definiera omfången och rollerna som ska tilldelas medlemmar i varje team för att ge rätt nivå av insyn i kostnadshanteringsinformationen.

- *Roller* definierar vad en användare kan göra med olika tillgångar.
- *Omfång* definierar vilka tillgångar (användare, grupp, tjänsthuvudnamn eller hanterad identitet) där användaren får göra dessa saker.

Som tumregel föreslår vi en modell med lägsta möjliga behörighet när du tilldelar personer till roller och omfång.

### <a name="roles"></a>Roller

Azure Cost Management stöder följande inbyggda roller för varje omfång:

- [Ägare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner). Kan visa kostnader och hantera allt, inklusive kostnadskonfiguration.
- [Deltagare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor). Kan visa kostnader och hantera allt, inklusive kostnadskonfiguration men inte åtkomst kontroll.
- [Läsare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#reader). Kan visa allt, inklusive kostnadsdata och konfiguration, men kan inte göra ändringar.
- [Cost Management-deltagare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor). Kan visa kostnader och hantera kostnadskonfiguration.
- [Cost Management-läsare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-reader) Kan visa kostnadsdata och konfiguration.

Som en allmän rekommendation bör medlemmar i alla team tilldelas rollen Cost Management-deltagare. Den här rollen beviljar åtkomst till att skapa och hantera budgetar och exporter för att övervaka och rapportera kostnader mer effektivt. Medlemmar i [molnstrategiteamet](../../organize/cloud-strategy.md) bör dock endast vara tilldelas rollen Cost Management-läsare. Det beror på att de inte deltar i att bestämma budgetar i Azure Cost Management-verktyget.

### <a name="scope"></a>Omfång

Följande omfång- och rollinställningar kommer att skapa den insyn som krävs för kostnadshantering. Denna rekommenderade metod kan kräva mindre ändringar för att passa tillgångsorganisationens beslut.

- [Teamet för molnimplementering](../../organize/cloud-adoption.md). Ansvaret för pågående optimeringsändringar innebär att Cost Management-deltagare måste ha åtkomst på resursgruppnivå.

  - **Arbetsmiljö**. Som minst bör molnimplementeringsteamet redan ha [deltagaråtkomst](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) till alla berörda resursgrupper, eller minst de grupper som är relaterade till utveckling/testning eller pågående distributionsaktiviteter. Ingen ytterligare omfångsinställning krävs.
  - **Produktionsmiljöer**. När en korrekt ansvarsfördelning har etablerats behöver molnimplementeringsteamet antagligen inte fortsätta ha åtkomst till resursgrupperna som är relaterade till projekten. Resursgrupperna som ger stöd för produktionsinstanserna i sina arbetsbelastningar behöver ett större omfång så att teamet kan se hur deras beslut inverkar på kostnaderna. Genom att ge produktionsresursgrupperna för teamet omfånget [Cost Management-deltagare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) kan teamet övervaka kostnader och bestämma budgeten baserat på användning och kontinuerlig investering i de arbetsbelastningar som stöds.

- [Teamet för molnstrategi](../../organize/cloud-strategy.md). Ansvar för att spåra kostnader över flera projekt och affärsenheter kräver Cost Management-läsaråtkomst på hanteringsgruppshierarkins rotnivå.

  - Tilldela [Cost Management läsaråtkomst](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-reader) till det här teamet i hanteringsgruppen. Detta säkerställer kontinuerlig insyn i alla distributioner som är associerade med prenumerationer som styrs av den här hanteringsgruppens hierarki.

- [Team för molnstyrning](../../organize/cloud-governance.md). Ansvar för att hantera kostnader, anpassa budgeten och rapportera för alla implementeringar kräver Cost Management-deltagaråtkomst på hanteringsgrupphierarkins rotnivå.

  - I en välhanterad miljö har molnstyrningsteamet förmodligen redan en högre åtkomstnivå, vilket gör ytterligare omfångstilldelning för [Cost Management-deltagare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) överflödigt.

<!-- cSpell:ignore automations -->

- [Molncenter för utmärkthet](../../organize/cloud-center-of-excellence.md). Ansvaret för att hantera kostnader som rör delade tjänster kräver Cost Management-deltagaråtkomst på prenumerationsnivå. Dessutom kan detta team behöva Cost Management-deltagaråtkomst till resursgrupper eller prenumerationer som innehåller tillgångar som distribuerats av CCoE-automatiseringar för att förstå hur dessa automatiseringar påverkar kostnaderna.

  - **Delade tjänster**. När ett moln Center med hög kvalitet är engagerat, föreslår bästa praxis att till gångar som hanteras av CCoE stöds av en centraliserad prenumeration för delade tjänster i en nav-och eker-modell. I det här scenariot har CCoE troligen deltagar- eller ägaråtkomst till den prenumerationen, vilket gör ytterligare omfångstilldelningar för [Cost Management-deltagare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) onödigt.
  - **CCoE-automatisering/kontroller**. CCoE innehåller ofta kontroller och automatiserade distributionsskript för molnimplementeringsteamen. CCoE har ansvar för att förstå hur dessa acceleratorer påverkar kostnader. Teamet behöver [Cost Management-deltagaråtkomst](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) till alla resursgrupper eller prenumerationer som kör dessa acceleratorer för att få insyn.

- **Molndriftsteam**. Ansvaret för att hantera löpande kostnader för produktionsmiljöer kräver Cost Management-deltagaråtkomst till alla produktionsprenumerationer.

  - Den allmänna rekommendationen placerar produktions-och produktions resurser i separata prenumerationer som styrs av noder i hierarkin för hanterings grupper som är kopplade till produktions miljöer. I en välhanterad miljö har medlemmarna i driftsteamet förmodligen ägar- eller deltagaråtkomst till produktionsprenumerationer, vilket gör rollen [Cost Management-deltagare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) överflödig.

## <a name="additional-cost-management-resources"></a>Ytterligare resurser för kostnadshantering

Azure Cost Management är ett väldokumenterat verktyg för att ställa in budgetar och få insyn i molnkostnader för Azure eller AWS. När du har upprättat åtkomst till en välhanterad miljöhierarki kan följande artiklar hjälpa dig att använda verktyget för att övervaka och kontrollera kostnader.

### <a name="get-started-with-azure-cost-management"></a>Kom igång med Azure Cost Management

Mer information om att komma igång med Azure Cost Management finns i [Optimera din molninvestering med Azure Cost Management](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json).

### <a name="use-azure-cost-management"></a>Använd Azure Cost Management

- [Skapa och hantera budgetar](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets)
- [Exportera kostnadsdata](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-export-acm-data)
- [Optimera kostnader baserat på rekommendationer](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations)
- [Övervaka användning och utgifter med hjälp av kostnadsaviseringar](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending)

### <a name="use-azure-cost-management-to-govern-aws-costs"></a>Använd Azure Cost Management för att styra AWS-kostnader

- [Integrering av kostnads- och användningsrapporter från AWS](https://docs.microsoft.com/azure/cost-management-billing/costs/aws-integration-set-up-configure)
- [Hantera AWS-kostnader](https://docs.microsoft.com/azure/cost-management/aws-integration-manage)

### <a name="establish-access-roles-and-scope"></a>Etablera åtkomst, roller och omfång

- [Förstå omfång för kostnadshantering](https://docs.microsoft.com/azure/cost-management/understand-work-scopes)
- [Ange omfång för en resursgrupp](https://docs.microsoft.com/azure/role-based-access-control/quickstart-assign-role-user-portal)
