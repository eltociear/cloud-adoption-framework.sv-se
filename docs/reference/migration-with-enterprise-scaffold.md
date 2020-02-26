---
title: Azure Enterprise-kodskelett
description: Beskriver ett företags-Autogenerera som kan hjälpa till att säkerställa en säker och hanterbar miljö.
author: rdendtler
ms.author: rodend
ms.date: 09/22/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: reference
ROBOTS: NOINDEX
ms.openlocfilehash: dd4f60eafed3281d5d4e67285c413b9f969793e3
ms.sourcegitcommit: 10f687bb1316db509fc1a3dbde72e107a467d72a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/26/2020
ms.locfileid: "77629257"
---
# <a name="azure-enterprise-scaffold-prescriptive-subscription-governance"></a>Azure Enterprise-Autogenerera: handskriven prenumerations styrning

> [!NOTE]
> Azure Enterprise-ramverk har integrerats i Microsoft Cloud adoptions ramverket. Innehållet i den här artikeln visas nu i avsnittet [klart](../ready/index.md) i det nya ramverket. Den här artikeln är inaktuell i början av 2020. För att börja använda den nya processen, se [färdig översikt](../ready/index.md), [skapa din första landnings zon](../ready/azure-setup-guide/migration-landing-zone.md)och [överväganden vid landnings zon](../ready/considerations/index.md).

Företag kan i allt större utsträckning använda det offentliga molnet för att bli flexibelt och flexibelt. De förlitar sig på molnets hållfasthet för att skapa intäkter och optimera resursanvändningen för verksamheten. Microsoft Azure tillhandahåller en mängd tjänster och funktioner som företag sätter samman som bygg stenar för att hantera en mängd olika arbets belastningar och program.

Att välja att använda Microsoft Azure är bara det första steget för att uppnå molnets fördel. Det andra steget är att förstå hur företaget effektivt kan använda Azure och identifiera de grundläggande funktioner som behövs för att lösa frågor som:

- "Jag är bekymrad om data suveränitet; Hur kan jag se till att mina data och system uppfyller våra myndighets krav? "
- "Hur gör jag för att vet vad varje resurs stöder så att jag kan ta hänsyn till den och fakturera den korrekt?"
- "Jag vill vara säker på att allt vi distribuerar eller gör i det offentliga molnet börjar med tänkesätt av säkerhet först, hur gör jag för att hjälpa till att under lätta det?"

Den potentiella kunden för en tom prenumeration utan guardrails är avskräckande. Det tomma utrymmet kan hindra din flytt till Azure.

Den här artikeln ger en utgångs punkt för tekniska experter som kan hantera behovet av styrning och balansera det med behovet av smidighet. Den introducerar begreppet företags-Autogenerera som hjälper organisationer att implementera och hantera sina Azure-miljöer på ett säkert sätt. Det tillhandahåller ramverket för att utveckla effektiva och effektiva kontroller.

## <a name="need-for-governance"></a>Behov av styrning

När du flyttar till Azure måste du hantera avsnittet av styrningen tidigt för att säkerställa att molnet används i företaget. Tids-och bureaucracy för att skapa ett omfattande styrnings system innebär tyvärr att vissa affärs grupper går direkt till leverantörer utan att det ingår i företaget. Den här metoden kan lämna företaget öppet för att kompromettera om resurserna inte hanteras korrekt. Egenskaperna hos det offentliga molnet&mdash;flexibilitet, flexibilitet och konsumtions prissättnings&mdash;är viktiga för affärs grupper som snabbt behöver uppfylla kundernas krav (både interna och externa). Men företags IT måste se till att data och system är effektivt skyddade.

När du skapar en byggnad används ramverk för att skapa en grund för en struktur. Autogenerera vägleder den allmänna dispositionen och tillhandahåller fäst punkter för att frigöra permanenta system som ska monteras. En Enterprise-Autogenerera är detsamma: en uppsättning flexibla kontroller och Azure-funktioner som ger en struktur till miljön och ankare för tjänster som bygger på det offentliga molnet. Det ger byggare (IT-och affärs grupper) en grund för att skapa och ansluta nya tjänster som håller leverans hastigheten i åtanke.

Autogenerera bygger på praxis som vi har samlat in från många engagemang med klienter av olika storlekar. Dessa klienter sträcker sig från små organisationer som utvecklar lösningar i molnet till stora multinationella företag och oberoende program varu leverantörer som migrerar arbets belastningar och utvecklar molnbaserade lösningar. Enterprise-Autogenerera är "Purpose-byggd" för att vara flexibel för att stödja både traditionella IT-arbetsbelastningar och Agile-arbetsbelastningar, till exempel utvecklare som skapar program vara som en tjänst (SaaS) som baseras på Azures plattforms funktioner.

Företags-Autogenerera kan fungera som grund för varje ny prenumeration i Azure. Det gör det möjligt för administratörer att se till att arbets belastningarna uppfyller minimi kraven för styrning av en organisation utan att hindra affärs grupper och utvecklare från att snabbt möta sina egna mål. Vår erfarenhet visar att det här ökar avsevärt, i stället för att förhindra att offentliga moln växer.

> [!NOTE]
> Microsoft har lanserat en ny funktion som kallas [Azure-ritningar](https://docs.microsoft.com/azure/governance/blueprints/overview) som gör att du kan paketera, hantera och distribuera vanliga bilder, mallar, principer och skript över prenumerationer och hanterings grupper. Den här funktionen är bryggan mellan Autogenerera-syftet som referens modell och distribution av modellen till din organisation.
>
Följande bild visar komponenterna i Autogenerera. Stiftelsen förlitar sig på en solid plan för hanterings hierarkin och prenumerationer. Pelaren består av Resource Manager-principer och starka namngivnings standarder. Resten av Autogenerera är kärnan i Azures funktioner och funktioner som möjliggör och ansluter en säker och hanterbar miljö.

![Enterprise-Autogenerera](../_images/reference/scaffoldv2.png)

## <a name="define-your-hierarchy"></a>Definiera hierarkin

Grunden för Autogenerera är hierarkin och relationen för Azure Enterprise-registrering via prenumerationer och resurs grupper. Företags registreringen definierar formen och användningen av Azure-tjänster i företaget från en avtals punkt. I Enterprise-avtal kan du ytterligare dela upp miljön i avdelningar, konton, prenumerationer och resurs grupper för att matcha organisationens struktur.

![Hierarki](../_images/reference/agreement.png)

En Azure-prenumeration är den grundläggande enheten där alla resurser finns. Den definierar också flera gränser i Azure, till exempel antal kärnor, virtuella nätverk och andra resurser. Resurs grupper används för att ytterligare förfina prenumerations modellen och möjliggör en mer naturlig gruppering av resurser.

Alla företag är olika och hierarkin i bilden ovan ger stor flexibilitet i hur Azure organiseras i företaget. Att utforma hierarkin så att den återspeglar företagets fakturerings-, resurs hanterings-och resurs åtkomst behov är det första och viktigaste beslutet som du gör när du startar i det offentliga molnet.

### <a name="departments-and-accounts"></a>Avdelningar och konton

De tre vanligaste mönstren för Azure-registreringar är:

- **Funktions** mönstret:

  ![Funktionella mönster](../_images/reference/functional.png)

- **Affär senhetens** mönster:

  ![Affär senhets mönstret](../_images/reference/business.png)

- Det **geografiska** mönstret:

  ![Det geografiska mönstret](../_images/reference/geographic.png)

Även om var och en av dessa mönster har sitt ställe, är **affär senhets** mönstret allt vanligare för att utforma en organisations kostnads modell och återspegla kontroll. Microsoft Core Engineering och Operations Group har skapat en effektiv delmängd av **affär senhets** mönstret som modelleras på **federala**, **delstatliga**och **lokalt**. Mer information finns i [ordna prenumerationer och resurs grupper i företaget](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise).

### <a name="azure-management-groups"></a>Azure-hanteringsgrupper

Microsoft erbjuder nu ett annat sätt att modellera din hierarki: [Azure-hanterings grupper](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview). Hanterings grupper är mycket mer flexibla än avdelningar och konton, och de kan kapslas upp till sex nivåer. Med hanterings grupper kan du skapa en hierarki som är separat från din fakturerings-hierarki, endast för effektiv hantering av resurser. Hanterings grupper kan spegla din fakturerings-hierarki och ofta företag startar på det sättet. Kraften i hanterings grupper är dock när du använder dem för att modellera din organisation, gruppera relaterade prenumerationer (oavsett var de befinner sig i hierarkin) och tilldela gemensamma roller, principer och initiativ. Några exempel är:

- **Produktion jämfört med ingen produktion.** Vissa företag skapar hanterings grupper för att identifiera sina produktions-och inproduction-prenumerationer. Med hanteringsgrupper blir det enklare för dessa kunder att hantera roller och principer. Till exempel kan en prenumeration som inte är en "deltagare"-åtkomst, men i produktion har endast "läsare"-åtkomst.
- **Interna tjänster jämfört med externa tjänster.** Företag har ofta olika krav, principer och roller för interna tjänster jämfört med kund tjänster.

Väl utformade hanterings grupper är, tillsammans med Azure Policy och initiativ, stamnätet för effektiv styrning av Azure.

### <a name="subscriptions"></a>Prenumerationer

När du bestämmer dig för dina avdelningar och konton (eller hanterings grupper) tittar du främst på hur du delar upp Azure-miljön för att matcha din organisation. Men prenumerationer är den plats där det verkliga arbetet sker och dina beslut kan påverka säkerhet, skalbarhet och fakturering. Många organisationer tittar på följande mönster som stöd linjer:

- **Program/tjänst:** Prenumerationer representerar ett program eller en tjänst (portfölj av program)
- **Livs cykel:** Prenumerationer representerar en livs cykel för en tjänst, till exempel produktion eller utveckling.
- **Avdelning:** Prenumerationer representerar avdelningar i organisationen.

De två första mönstren är de som används oftast och båda rekommenderas. Livs cykel metoden är lämplig för de flesta organisationer. I det här fallet är den allmänna rekommendationen att använda två bas prenumerationer, `Production` och `Nonproduction`, och Använd sedan resurs grupper för att separera miljöerna ytterligare.

### <a name="resource-groups"></a>Resursgrupper

Med Azure Resource Manager kan du ange resurser i meningsfulla grupper för hantering, fakturering eller naturlig tillhörighet. Resurs grupper är behållare för resurser som har en gemensam livs cykel eller delar ett attribut, till exempel "alla SQL-servrar" eller "program A".

Resursgrupper kan inte kapslas, och resurser kan endast tillhöra en enskild resursgrupp. Vissa åtgärder kan tillämpas på alla resurser i en resursgrupp. Om du till exempel tar bort en resurs grupp tas alla resurser i resurs gruppen bort. Precis som prenumerationer finns det vanliga mönster när du skapar resurs grupper och varierar från "traditionella IT"-arbets belastningar till "Agile IT"-arbets belastningar:

- "Traditionell IT"-arbets belastningar grupperas vanligt vis efter objekt inom samma livs cykel, till exempel ett program. Gruppering av program möjliggör hantering av enskilda program.
- "Agile IT"-arbets belastningar tenderar att fokusera på externa program som riktas mot kund. Resurs grupperna återspeglar ofta distributions lagren (till exempel en webb nivå eller app-nivå) och hantering.

> [!NOTE]
> Genom att förstå din arbets belastning kan du utveckla en resurs grupps strategi. Dessa mönster kan vara blandade och matchade. Till exempel en resurs grupp för delade tjänster i samma prenumeration som "Agile" resurs grupper.

## <a name="naming-standards"></a>Namngivningsregler

Den första pelaren i Autogenerera är en konsekvent namngivnings standard. Med väl utformade namngivnings standarder kan du identifiera resurser i portalen, på en faktura och inom skript. Du har förmodligen redan befintliga namngivnings standarder för lokal infrastruktur. När du lägger till Azure i miljön bör du använda samma namngivningsregler för dina Azure-resurser.

> [!TIP]
> För namngivnings konventioner:
>
> - Läs igenom och använd [vägledningen om mönster och praxis](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming) om det är möjligt. Den här vägledningen hjälper dig att bestämma en meningsfull namngivnings standard och ger omfattande exempel.
> - Använda Resource Manager-principer för att säkerställa namngivnings standarder.
>
> Kom ihåg att det är svårt att ändra namnen senare, så några minuter kommer nu att spara problem senare.

Fokusera på dina namngivnings standarder på de resurser som ofta används och söks igenom. Till exempel bör alla resurs grupper följa en stark standard för tydlighetens skull.

### <a name="resource-tags"></a>Resurstaggar

Resurs taggar är tätt justerade med namngivnings standarder. När resurser läggs till i prenumerationer blir det allt viktigt att logiskt kategorisera dem för fakturering, hantering och drift. Mer information finns i [använda taggar för att ordna dina Azure-resurser](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

> [!IMPORTANT]
> Taggar kan innehålla personlig information och kan omfattas av reglerna i GDPR. Planera för hantering av Taggar noggrant. Om du vill ha allmän information om GDPR kan du läsa avsnittet GDPR på [service Trust-portalen](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

Taggar används på många sätt utöver fakturering och hantering. De används ofta som en del av Automation (se senare avsnitt). Detta kan orsaka konflikter om de inte anses vara överst. Det bästa sättet är att identifiera alla vanliga taggar på företags nivå (till exempel ApplicationOwner och CostCenter) och tillämpa dem konsekvent när du distribuerar resurser med Automation.

## <a name="azure-policy-and-initiatives"></a>Azure Policy och initiativ

De andra panelerna i Autogenerera omfattar användning av [Azure policy och initiativ](https://docs.microsoft.com/azure/azure-policy/azure-policy-introduction) för att hantera risker genom att verkställa regler (med effekter) över resurser och tjänster i dina prenumerationer. Azure-initiativ är samlingar med principer som är utformade för att uppnå ett enda mål. Principer och initiativ tilldelas sedan till ett resurs omfång för att börja verkställa dessa principer.

Principer och initiativ är ännu mer kraftfulla när de används med de hanterings grupper som nämns ovan. Hanterings grupper gör det möjligt att tilldela ett initiativ eller en princip till en hel uppsättning prenumerationer.

### <a name="common-uses-of-resource-manager-policies"></a>Vanliga användnings områden för Resource Manager-principer

Principer och initiativ är ett kraftfullt verktyg i Azure Toolkit. Policys gör det möjligt för företag att tillhandahålla kontroller för "traditionella IT"-arbets belastningar som möjliggör den stabilitet som behövs för branschspecifika program samtidigt som de också tillåter "Agile-arbetsbelastningar&mdash;till exempel att utveckla kund program utan att exponera företaget för ytterligare risk. De vanligaste mönstren för principer är:

- **Geo-efterlevnad och data suveränitet.** Azure har en ständigt växande lista över regioner över hela världen. Företag behöver ofta se till att resurser i ett särskilt område finns kvar i en geografisk region för att uppfylla myndighets krav.
- **Undvik att exponera servrar offentligt.** Azure Policy kan förhindra distribution av vissa resurs typer. Det är vanligt att skapa en princip för att neka skapandet av en offentlig IP-adress inom en bestämd omfattning, vilket förhindrar oavsiktlig exponering av en server till Internet.
- **Kostnads hantering och metadata.** Resurs Taggar används ofta för att lägga till viktiga fakturerings data till resurser och resurs grupper som CostCenter, owner och mycket annat. Dessa taggar är inte värdefulla för korrekt fakturering och hantering av resurser. Principer kan tvinga tillämpning av resurs taggar till alla distribuerade resurser, vilket gör det enklare att hantera.

### <a name="common-uses-of-initiatives"></a>Vanliga användnings områden för initiativ

Initiativ ger företag möjlighet att gruppera logiska principer och spåra dem som en enda enhet. Initiativ hjälper företaget att uppfylla både flexibla och traditionella arbets belastningar. Vanliga användnings områden för initiativ är:

- **Aktivera övervakning i Azure Security Center.** Detta är ett standard initiativ i Azure Policy och ett utmärkt exempel på vad initiativ är. Det möjliggör principer som identifierar okrypterade SQL-databaser, sårbarheter för virtuella datorer och fler vanliga säkerhetsrelaterade behov.
- **Reglerande initiativ.** Företag kan ofta gruppera principer som är gemensamma för ett reglerings krav (till exempel HIPAA) så att kontroller och kompatibilitet till kontrollerna spåras effektivt.
- **Resurs typer och SKU: er.** Att skapa ett initiativ som begränsar vilka typer av resurser som kan distribueras samt vilka SKU: er som kan distribueras kan hjälpa till att kontrol lera kostnaderna och se till att din organisation bara distribuerar resurser som ditt team har kunskaps uppsättningen och de procedurer som krävs för att stödja.

> [!TIP]
> Vi rekommenderar att du alltid använder initiativ definitioner i stället för princip definitioner. När du har tilldelat ett initiativ till ett omfång, till exempel prenumeration eller hanterings grupp, kan du enkelt lägga till en annan princip till initiativet utan att behöva ändra några tilldelningar. Detta gör det enklare att förstå vad som används och spåra kompatibiliteten.

### <a name="policy-and-initiative-assignments"></a>Princip-och initiativ tilldelningar

När du har skapat principer och grupperat dem i logiska initiativ måste du tilldela principen till ett omfång, oavsett om det är en hanterings grupp, en prenumeration eller till och med en resurs grupp. Med tilldelningar kan du även undanta ett under omfång från tilldelningen av en princip. Om du t. ex. förhindrar att offentliga IP-adresser skapas i en prenumeration kan du skapa en tilldelning med ett undantag för en resurs grupp som är ansluten till din skyddade DMZ.

Du hittar flera princip exempel som visar hur principer och initiativ kan tillämpas på olika resurser i Azure på den här [GitHub](https://github.com/Azure/azure-policy) -lagringsplatsen.

## <a name="identity-and-access-management"></a>Identitets- och åtkomsthantering

Ett av de första och viktigaste frågorna som du ställer när du börjar med det offentliga molnet är "Vem ska ha åtkomst till resurser?" och "Hur kan jag kontrol lera den här åtkomsten?" Att kontrol lera åtkomsten till Azure Portal och resurser i portalen är avgörande för den långsiktiga säkerheten för dina till gångar i molnet.

För att skydda åtkomsten till dina resurser ska du först konfigurera din identitetsprovider och sedan konfigurera roller och åtkomst. Azure Active Directory (Azure AD), som är ansluten till din lokala Active Directory, är grunden i Azure Identity. I detta fall är Azure AD *inte* detsamma som lokalt Active Directory, och det är viktigt att förstå vad en Azure AD-klient är och hur den är kopplad till din Azure-registrering. Granska tillgänglig [information](../govern/resource-consistency/resource-access-management.md) för att få en solid grund på Azure AD och lokala Active Directory. Installera och konfigurera [Azure AD Connect-verktyget](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) lokalt för att ansluta och synkronisera Active Directory till Azure AD.

![Diagram över AD-arkitektur](../_images/reference/ad-architecture.png)

När Azure ursprungligen släpptes var åtkomst kontroller till en prenumeration grundläggande: administratör eller medadministratör. Åtkomst till en prenumeration i den klassiska modellen underförstådd åtkomst till alla resurser i portalen. Detta brist på detaljerad kontroll ledde till spridningen av prenumerationer för att ge en nivå av rimlig åtkomst kontroll för en Azure-registrering. Den här spridningen av prenumerationer behövs inte längre. Med rollbaserad åtkomst kontroll (RBAC) kan du tilldela användare till standard roller som ger gemensam åtkomst, till exempel "ägare", "deltagare" eller "läsare" eller till och med skapa egna roller.

När du implementerar rollbaserad åtkomst rekommenderas följande:

- Kontrol lera administratören/medadministratören för en prenumeration eftersom rollerna har omfattande behörigheter. Du behöver bara lägga till prenumerations ägaren som en medadministratör om de behöver hanterade klassiska Azure-distributioner.
- Använd hanterings grupper för att tilldela [roller](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview#management-group-access) över flera prenumerationer och minska belastningen på att hantera dem på prenumerations nivå.
- Lägg till Azure-användare i en grupp (till exempel program X-ägare) i Active Directory. Använd den synkroniserade gruppen för att ge grupp medlemmar rätt behörighet för att hantera resurs gruppen som innehåller programmet.
- Följ principen för att bevilja den **minsta behörighet** som krävs för att utföra det förväntade arbetet.

> [!IMPORTANT]
>Överväg att använda [Azure AD Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure), Azure [Multi-Factor Authentication](https://docs.microsoft.com/azure/active-directory/authentication/howto-mfa-getstarted) och funktioner för [villkorlig åtkomst](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) för att ge bättre säkerhet och bättre insyn i de administrativa åtgärderna i dina Azure-prenumerationer. Dessa funktioner kommer från en giltig Azure AD Premium-licens (beroende på funktion) för att ytterligare skydda och hantera din identitet. Azure AD PIM aktiverar "just-in-Time" administrativ åtkomst med arbets flödet för godkännande, samt en fullständig granskning av administratörs aktiveringar och aktiviteter. Azure Multi-Factor Authentication är en viktig funktion och möjliggör tvåstegsverifiering för inloggning till Azure Portal. I kombination med villkorliga åtkomst kontroller kan du effektivt hantera risken för angrepp.

Planera och förbereda för dina identitets-och åtkomst kontroller och följande metod tips för Azure Identity Management ([länk](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices)) är en av de bästa strategierna för risk minskning som du kan använda och bör betraktas som obligatoriska för varje distribution.

## <a name="security"></a>Säkerhet

En av de största blocken till moln implementeringen har traditionellt sett några problem med säkerheten. IT-riskhantering och säkerhets avdelningar måste se till att resurser i Azure är skyddade och säkra som standard. Azure tillhandahåller funktioner som du kan använda för att skydda resurser när du upptäcker och eliminerar hot mot dessa resurser.

### <a name="azure-security-center"></a>Azure Security Center

[Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) ger en enhetlig vy över säkerhets statusen för resurser i din miljö förutom Avancerat skydd. Azure Security Center är en öppen plattform som gör det möjligt för Microsoft-partner att skapa program vara som ansluter till och förbättrar dess funktioner. De grundläggande funktionerna i Azure Security Center (kostnads fri nivå) tillhandahåller utvärdering och rekommendationer som förbättrar din säkerhets position. Dess betalda nivåer möjliggör ytterligare och värdefulla funktioner, till exempel just-in-Time-administratörs åtkomst och anpassningsbara program kontroller (vit listning).

> [!TIP]
>Azure Security Center är ett kraftfullt verktyg som förbättras regelbundet med nya funktioner som du kan använda för att identifiera hot och skydda ditt företag. Vi rekommenderar starkt att du alltid aktiverar Azure Security Center.

### <a name="locks-for-azure-resources"></a>Lås för Azure-resurser

När din organisation lägger till kärn tjänster för prenumerationer blir det allt viktigt att undvika affärs avbrott. Ett vanligt avbrott inträffar när ett skript eller verktyg som körs i en Azure-prenumeration oavsiktligt tar bort en resurs. [Lås](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) begränsar åtgärder på hög värdes resurser där ändringar eller borttagning av dem skulle ha en betydande inverkan. Du kan använda Lås till prenumerationer, resurs grupper eller enskilda resurser. Använd lås till grundläggande resurser, till exempel virtuella nätverk, gateways, nätverks säkerhets grupper och nyckel lagrings konton.

### <a name="secure-devops-kit-for-azure"></a>Secure DevOps kit för Azure

Secure DevOps kit för Azure (AzSK) är en samling skript, verktyg, tillägg och automatiserings funktioner som ursprungligen har skapats av Microsofts egna IT-team och [lanserats som öppen källkod via GitHub](https://github.com/azsk/devopskit-docs). AzSK fokuserar på Azure-prenumerations-och resurs säkerhets behoven från slut punkt till slut punkt för team som använder omfattande automatisering och smidig integrering av säkerhet i interna DevOps-arbetsflöden som gör det lättare att göra säkra DevOps med de sex fokus områdena:

- Skydda prenumerationen
- Aktivera säker utveckling
- Integrera säkerhet i CI/CD
- Kontinuerlig säkerhet
- Avisering och övervakning
- Moln risk styrning

![Översikts diagram över Secure DevOps kit för Azure](../_images/reference/secure-devops-kit.png)

AzSK är en omfattande uppsättning verktyg, skript och information som är en viktig del av en fullständig Azures styrnings plan och som införlivar detta i din Autogenerera är avgörande för att stödja organisationernas risk hanterings mål.

### <a name="azure-update-management"></a>Azure-Uppdateringshantering

En av de viktigaste uppgifterna du kan göra för att skydda din miljö är att se till att dina servrar korrigeras med de senaste uppdateringarna. Även om det finns många verktyg för att åstadkomma detta tillhandahåller Azure [azure uppdateringshantering](https://docs.microsoft.com/azure/automation/automation-update-management) -lösningen för att lösa identifieringen och distributionen av viktiga OS-korrigeringsfiler. Den använder Azure Automation, som beskrivs i avsnittet [Automatisera](#automate) senare i den här hand boken.

## <a name="monitor-and-alerts"></a>Övervaka och aviseringar

Att samla in och analysera telemetri som ger detaljerad information om aktiviteter, prestanda mått, hälso tillstånd och tillgänglighet för de tjänster som du använder i dina Azure-prenumerationer är avgörande för att proaktivt hantera dina program och infrastruktur och är ett grundläggande behov av varje Azure-prenumeration. Varje Azure-tjänst genererar telemetri i form av aktivitets loggar, Mät värden och diagnostikloggar.

- **Aktivitets loggar** beskriver alla åtgärder som utförts på resurser i dina prenumerationer.
- **Mått** är numerisk information som släpps av en resurs som beskriver prestanda och hälsan för en resurs.
- **Diagnostikloggar** genereras av en Azure-tjänst och ger omfattande, frekventa data om driften av tjänsten.

Den här informationen kan visas och åtgärdas på flera nivåer och förbättras kontinuerligt. Azure tillhandahåller **delade**, **grundläggande**och **djup** övervaknings funktioner i Azure-resurser genom de tjänster som beskrivs i diagrammet nedan.

![Övervakning](../_images/reference/monitoring.png)

### <a name="shared-capabilities"></a>Delade funktioner

- **Aviseringar:** Du kan samla in alla logg-, händelse-och mått från Azure-resurser, men utan möjlighet att bli informerad om kritiska villkor och agera, så är dessa data bara användbara för historiska syfte och data utredning. Azure-aviseringar proaktivt meddelar dig om villkor som du definierar i alla dina program och din infrastruktur. Du skapar aviserings regler för loggar, händelser och mått som använder åtgärds grupper för att meddela mottagares uppsättningar. Åtgärds grupper ger också möjlighet att automatisera reparationen med hjälp av externa åtgärder som Webhooks för att köra Azure Automation runbooks och Azure Functions.

- **Instrument paneler:** Med instrument paneler kan du sammanställa övervaknings Visa vyer och kombinera data över resurser och prenumerationer för att ge dig en företagsomfattande vy över telemetri för Azure-resurser. Du kan skapa och konfigurera dina egna vyer och dela dem med andra. Du kan till exempel skapa en instrument panel som består av olika paneler för databas administratörer för att tillhandahålla information över alla Azure Database-tjänster, inklusive Azure SQL DB, Azure DB för PostgreSQL och Azure DB för MySQL.

- **Metrics Explorer:** Mått är numeriska värden som genereras av Azure-resurser (t. ex .% processor-eller disk-I/O) som ger inblick i dina resursers drift och prestanda. Med hjälp av Metrics Explorer kan du definiera och skicka de mått som intresserar dig för att Log Analytics för agg regering och analys.

### <a name="core-monitoring"></a>Kärnövervakning

- **Azure Monitor:** Azure Monitor är den kärn plattforms tjänst som tillhandahåller en enda källa för övervakning av Azure-resurser. Azure Portal-gränssnittet i Azure Monitor ger en centraliserad hopp punkt för alla övervakningsfunktionerna i Azure, inklusive djup övervaknings funktionerna i Application Insights, Log Analytics, nätverks övervakning, hanterings lösningar och Tjänst kartor. Med Azure Monitor kan du visualisera, fråga, cirkulera, arkivera och agera på de mått och loggar som kommer från Azure-resurser i hela din moln egendom. Förutom portalen kan du hämta data genom att övervaka PowerShell-cmdlets, plattforms oberoende CLI eller Azure Monitor REST-API: er.

- **Azure Advisor:** Azure Advisor ständigt övervakar telemetri i dina prenumerationer och miljöer och ger rekommendationer om bästa praxis för hur du optimerar dina Azure-resurser för att spara pengar och förbättra prestanda, säkerhet och tillgänglighet för de resurser som utgör dina program.

- **Service Health:** Azure Service Health identifierar eventuella problem med Azure-tjänster som kan påverka dina program och hjälpa dig att planera för schemalagda underhålls perioder.

- **Aktivitets logg:** Aktivitets loggen beskriver alla åtgärder för resurser i dina prenumerationer. Det ger en Gransknings logg för att avgöra vad, vem och när om det finns några åtgärder för att skapa, uppdatera och ta bort resurser. Händelser i aktivitets loggen lagras i plattformen och är tillgängliga för frågor i 90 dagar. Du kan mata in aktivitets loggar i Log Analytics under längre Retentions perioder och djupare frågor och analys över flera resurser.

### <a name="deep-application-monitoring"></a>Djupgående programövervakning

- **Application Insights:** Med Application Insights kan du samla in programspecifik telemetri och övervaka prestanda, tillgänglighet och användning av program i molnet eller lokalt. Genom att instrumentera ditt program med SDK: er som stöds för flera språk, inklusive .NET, Java Script, JAVA, Node. js, ruby och python. Application Insights händelser matas in i samma Log Analytics data lager som har stöd för infrastruktur-och säkerhetsövervakning så att du kan korrelera och aggregera händelser över tid via ett omfattande frågespråk.

### <a name="deep-infrastructure-monitoring"></a>Djupgående infrastruktursövervakning

- **Log Analytics:** Log Analytics spelar upp en central roll i Azure-övervakning genom att samla in telemetri och andra data från olika källor och tillhandahålla ett frågespråk och analys motor som ger dig insikter om driften av dina program och resurser. Du kan antingen interagera direkt med Log Analytics data via snabba loggs ökningar och vyer, eller så kan du använda analys verktyg i andra Azure-tjänster som lagrar sina data i Log Analytics, till exempel Application Insights eller Azure Security Center.

- **Nätverks övervakning:** Med Azures tjänster för nätverks övervakning kan du få inblick i nätverks trafikflöde, prestanda, säkerhet, anslutning och Flask halsar. En välplanerad nätverks design bör omfatta konfigurering av Azure Network Monitor Services som Network Watcher och ExpressRoute Monitor.

- **Hanterings lösningar:** Hanterings lösningar är paketerade uppsättningar av logik, insikter och fördefinierade Log Analytics frågor för ett program eller en tjänst. De förlitar sig på Log Analytics som grund för att lagra och analysera händelse data. Exempel på hanterings lösningar är övervaknings behållare och Azure SQL Database analys.

- **Tjänstkarta:** Tjänstkarta ger en grafisk vy över dina infrastruktur komponenter, deras processer och beroenden på andra datorer och externa processer. Funktionen integrerar händelser, prestandadata och hanteringslösningar i Log Analytics.

> [!TIP]
> Innan du skapar enskilda aviseringar kan du skapa och underhålla en uppsättning delade åtgärds grupper som kan användas i Azure-aviseringar. På så sätt kan du centralt upprätthålla livs cykeln för dina mottagar listor, leverans metoder för meddelanden (e-post, SMS-telefonnummer) och Webhooks till externa åtgärder (Azure Automation runbooks, Azure Functions och Logic Apps ITSM).

## <a name="cost-management"></a>Kostnadshantering

En av de större ändringarna som du kommer att stöta på när du flyttar från ett lokalt moln till det offentliga molnet är att byta från kapital utgifter (köpa maskin vara) till drifts utgifter (som du betalar för tjänsten när du använder den). Den här växeln kräver också mer noggrann hantering av dina kostnader. Fördelen med molnet är att du kan grundläggande och positivt påverka kostnaden för en tjänst som du använder genom att stänga av eller ändra storlek på den när den inte behövs. Att medvetet hantera dina kostnader i molnet är bästa praxis och en som mogna kunder gör dagligen.

Microsoft tillhandahåller flera verktyg som du kan använda för att visualisera, spåra och hantera dina kostnader. Vi tillhandahåller också en fullständig uppsättning API: er så att du kan anpassa och integrera kostnads hanteringen i dina egna verktyg och instrument paneler. Dessa verktyg är lösta grupperade i Azure Portal funktioner och externa funktioner.

### <a name="azure-portal-capabilities"></a>Azure Portal funktioner

Dessa är verktyg för att ge dig omedelbar information om kostnad samt möjligheten att vidta åtgärder.

- **Prenumerations resurs kostnad:** I portalen för [Azure Cost-analys](https://docs.microsoft.com/azure/cost-management/overview) finns en snabb titt på dina kostnader och information om dagliga utgifter per resurs eller resurs grupp.
- **Azure Cost Management:** Den här produkten är resultatet av köpet av Cloudyn av Microsoft och gör att du kan hantera och analysera dina Azure-utgifter samt vad du lägger på andra offentliga moln leverantörer. Det finns både kostnads fria och betalda nivåer, med en stor mängd funktioner som visas i [översikten](https://docs.microsoft.com/azure/cost-management/overview).
- **Azure-budgetar och åtgärds grupper:** Du vet vad något kostar och gör något om det tills det nyligen har varit en manuell övning. Med introduktionen av Azure-budgetar och dess API: er är det nu möjligt att skapa åtgärder (som visas i [det här exemplet](https://channel9.msdn.com/Shows/Azure-Friday/Managing-costs-with-the-Azure-Budgets-API-and-Action-Groups)) när kostnaderna träffar ett tröskelvärde. Du kan till exempel stänga av resurs gruppen "test" när den når 100% av budgeten eller [ett annat exempel].
- **Azure Advisor** Att veta vad något kostar är bara hälften av slaget. den andra halvan vet vad du ska göra med den informationen. [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) ger dig rekommendationer om åtgärder som ska vidtas för att spara pengar, öka tillförlitligheten eller till och med öka säkerheten.

### <a name="external-cost-management-tools"></a>Verktyg för extern kostnads hantering

- **Power BI Azure Consumption Insights:** Vill du skapa dina egna visualiseringar för din organisation? I så fall är Azure Consumption Insights innehålls paketet för Power BI det verktyg som du väljer. Med hjälp av det här innehålls paketet och Power BI kan du skapa anpassade visualiseringar som representerar din organisation, göra djupare analyser av kostnader och lägga till i andra data källor för ytterligare berikning.

- **Förbruknings-API:** [Förbruknings-API: er](https://docs.microsoft.com/rest/api/consumption) ger dig program mässig åtkomst till kostnader och användnings data utöver information om budgetar, reserverade instanser och Marketplace-avgifter. Dessa API: er är bara tillgängliga för företags registreringar och vissa WebDirect-prenumerationer men de ger dig möjlighet att integrera dina kostnads data i dina egna verktyg och informations lager. Du kan också [komma åt dessa API: er via Azure CLI](https://docs.microsoft.com/cli/azure/consumption?view=azure-cli-latest).

Kunder som är långsiktiga och mogna moln användare följer vissa rekommenderade metoder:

- **Övervaka kostnader aktivt.** Organisationer som är mogna Azure-användare kan ständigt övervaka kostnader och vidta åtgärder när det behövs. Vissa organisationer är till och med att göra analyser och föreslå ändringar i användningen, och dessa personer är mer än betala själva första gången de hittar ett oanvänt HDInsight-kluster som körs för månader.
- **Använd reserverade VM-instanser.** En annan viktig läro sats för att hantera kostnader i molnet är att använda rätt verktyg för jobbet. Om du har en virtuell IaaS-dator som måste ligga dygnet runt, sparar med en reserverad VM-instans dig betydande pengar. Att hitta rätt balans mellan att automatisera avstängningen av virtuella datorer och använda reserverade VM-instanser har erfarenhet och analys.
- **Använd Automation effektivt.** Många arbets belastningar behöver inte köras varje dag. Att stänga av en virtuell dator under en fyra timmars period varje dag kan spara 15% av din kostnad. Automation debiteras snabbt för sig.
- **Använd resurs taggar för synlighet.** Som nämnts i det här dokumentet kan du använda resurs taggar för att få en bättre analys av kostnaderna.

Kostnads hantering är en disciplin som är kärnan till effektiv och effektiv körning av ett offentligt moln. Företag som uppnår framgång kan kontrol lera sina kostnader och matcha dem med deras faktiska efter frågan, i stället för att överköpa och lura efter frågan kommer.

## <a name="automate"></a>Automatisera

En av de många funktionerna som särskiljer förfallo tiden för organisationer som använder moln leverantörer är den nivå av automatisering som de har införlivat. Automation är en process som inte avslutas och när din organisation flyttas till molnet är det något som du behöver för att investera resurser och tid i byggnaden. Automation hanterar många olika sätt, inklusive konsekvent distribution av resurser (där det går direkt till ett annat grundläggande Autogenerera-koncept, mallar och DevOps) för att åtgärda problem. Automation är "kopplings vävnad" i Azure-Autogenerera och länkar varje region tillsammans.

Flera verktyg kan hjälpa dig att bygga ut den här funktionen från första parts verktyg som Azure Automation, Event Grid och Azure CLI till ett stort antal verktyg från tredje part, till exempel terraform, Jenkins, chef och Puppet. Bland verktygen för kärn automatisering ingår Azure Automation, Event Grid och Azure Cloud Shell.

- **Azure Automation** Är en molnbaserad funktion som gör att du kan skapa Runbooks (antingen i PowerShell eller python) och gör att du kan automatisera processer, konfigurera resurser och även använda korrigeringar. [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) har en omfattande uppsättning plattforms oberoende funktioner som är integrerade i din distribution, men som är för omfattande för att täckas i djup här.
- **Event Grid** är ett helt hanterat system för händelse dirigering som gör att du kan reagera på händelser i din Azure-miljö. Precis som Azure Automation är arbets vävnaden för vuxen moln organisationer, [Event Grid](https://docs.microsoft.com/azure/event-grid) är den arbets vävnad som är bra att automatisera. Med hjälp av Event Grid kan du skapa en enkel server åtgärd som skickar ett e-postmeddelande till en administratör när en ny resurs skapas och loggar resursen i en databas. Samma Event Grid kan meddela när en resurs tas bort och ta bort objektet från databasen.
- **Azure Cloud Shell** är ett interaktivt, webbläsarbaserat [gränssnitt](https://docs.microsoft.com/azure/cloud-shell/overview) för att hantera resurser i Azure. Det ger en fullständig miljö för antingen PowerShell eller bash som startas efter behov (och som behålls för dig) så att du har en konsekvent miljö som du kan köra skripten från. Azure Cloud Shell ger åtkomst till ytterligare nyckel verktyg – redan installerat – för att automatisera din miljö, inklusive [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli?view=azure-cli-latest), [terraform](https://docs.microsoft.com/azure/virtual-machines/linux/terraform-install-configure) och en växande lista med ytterligare [verktyg](https://azure.microsoft.com/updates/cloud-shell-new-cli-tools-and-font-size-selection) för att hantera behållare, databaser (SQLCMD) med mera.

Automation är ett heltids jobb och det kommer snabbt bli en av de viktigaste drift uppgifterna i moln teamet. Organisationer som använder metoden "automatisera första" har större framgångar i att använda Azure:

- **Hanterings kostnader:** Söker aktivt efter möjligheter och skapar automatisering för att ändra storlek på resurser, skala upp eller ned och stänga av outnyttjade resurser.
- **Drifts flexibilitet:** Med Automation (tillsammans med mallar och DevOps) får du en nivå av repeterbarhet som ökar tillgängligheten, ökar säkerheten och gör det möjligt för ditt team att fokusera på att lösa affärs problem.

## <a name="templates-and-devops"></a>Mallar och DevOps

Som det är markerat i avsnittet automatisera, bör målet som en organisation vara att etablera resurser via källentiteter och skript och minimera den interaktiva konfigurationen av dina miljöer. Den här metoden för "infrastruktur som kod" tillsammans med en disciplinen DevOps-process för kontinuerlig distribution kan garantera konsekvens och minska driften i dina miljöer. Nästan alla Azure-resurser kan distribueras via [Azure Resource Manager JSON-mallar](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) tillsammans med PowerShell eller Azures plattforms oberoende CLI och verktyg som terraform från Hashicorp (som har första klass support och integrerad i Azure Cloud Shell).

I artikeln, till exempel [metod tips för att använda Azure Resource Manager mallar](https://blogs.msdn.microsoft.com/mvpawardprogram/2018/05/01/azure-resource-manager) , får du en bra diskussion om bästa praxis och lektioner som har lärts att använda en DevOps metod för att Azure Resource Manager mallar med [Azure DevOps](https://docs.microsoft.com/azure/devops/user-guide/?view=vsts) -verktygskedjan. Ta tid och kraft för att utveckla en Core-uppsättning av mallar som är specifikt för din organisations krav och utveckla kontinuerliga leverans pipeliner med DevOps verktygs kedjor (till exempel Azure DevOps, Jenkins, Bamboo, TeamCity och kurser), särskilt för din produktions-och frågor och svars miljöer. Det finns ett stort bibliotek med [Azure snabb starts mallar](https://github.com/Azure/azure-quickstart-templates) på GitHub som du kan använda som utgångs punkt för mallar, och du kan snabbt skapa molnbaserade leverans pipeliner med Azure DevOps.

Som bästa praxis för produktions prenumerationer eller resurs grupper bör målet använda RBAC-säkerhet för att inte tillåta interaktiva användare som standard och använda automatiserade pipeliner för kontinuerlig leverans baserat på tjänstens huvud namn för att etablera alla resurser och leverera all program kod. Ingen administratör eller utvecklare bör röra Azure Portal för att interaktivt konfigurera resurser. Den här nivån av DevOps tar en gemensam ansträngning och använder alla koncepten i Azure-Autogenerera, vilket ger en konsekvent och säkrare miljö som uppfyller organisationens behov av att skala.

> [!TIP]
> När du utformar och utvecklar komplexa Azure Resource Manager mallar använder du [länkade mallar](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-linked-templates) för att ordna och återanvända komplexa resurs relationer från monolitisk JSON-filer. Detta gör att du kan hantera resurser individuellt och göra mallarna mer lättlästa, testable och återanvändbara.

Azure är en storskalig moln leverantör. När du flyttar din organisation från lokala servrar till molnet, förlitar sig på samma koncept som moln leverantörer och SaaS-program använder så att din organisation kan reagera på affärs behoven mycket mer effektivt.

## <a name="core-network"></a>Kärn nätverk

Den sista delen av referens modellen för Azure-Autogenerera är kärnan till hur din organisation får åtkomst till Azure på ett säkert sätt. Åtkomst till resurser kan vara antingen interna (inom företagets nätverk) eller externa (via Internet). Det är enkelt för användare i din organisation att oavsiktligt placera resurser på fel plats och eventuellt öppna dem till skadlig åtkomst. Precis som med lokala enheter måste företag lägga till lämpliga kontroller för att säkerställa att Azure-användare fattar rätt beslut. För prenumerations styrning identifierar vi kärn resurser som ger grundläggande kontroll över åtkomsten. Kärn resurserna består av:

- **Virtuella nätverk** är behållar objekt för undernät. Även om det inte är absolut nödvändigt används det ofta när du ansluter program till interna företags resurser.
- Med **användardefinierade vägar** kan du manipulera routningstabellen i ett undernät så att du kan skicka trafik via en virtuell nätverks installation eller till en fjärran sluten gateway i ett peer-kopplat virtuellt nätverk.
- Med **peering för virtuella nätverk** kan du sömlöst ansluta två eller flera virtuella Azure-nätverk, vilket skapar mer komplexa nav-och eker-designer eller delade tjänst nätverk.
- **Tjänst slut punkter.** Tidigare PaaS tjänster förlitade sig på olika metoder för att skydda åtkomsten till dessa resurser från dina virtuella nätverk. Med tjänst slut punkter kan du skydda åtkomsten till aktiverade PaaS-tjänster från **enbart** anslutna slut punkter, vilket ökar den övergripande säkerheten.
- **Säkerhets grupper** är en omfattande uppsättning regler som ger möjlighet att tillåta eller neka inkommande och utgående trafik till och från Azure-resurser. [Säkerhets grupper](https://docs.microsoft.com/azure/virtual-network/security-overview) består av säkerhets regler som kan utökas med **service märken** (som definierar vanliga Azure-tjänster som Azure Key Vault eller Azure SQL Database) och **program säkerhets grupper** (som definierar och program struktur, till exempel webb servrar eller App-servrar).

> [!TIP]
> Använd tjänst Taggar och program säkerhets grupper i dina nätverks säkerhets grupper för att inte bara förbättra reglerna för läsbarhet&mdash;som är viktiga för att förstå påverkan&mdash;, men även för att möjliggöra effektiv mikrosegmentering inom ett större undernät, vilket minskar tillväxten och ökar flexibiliteten.

### <a name="azure-virtual-datacenter"></a>Azure Virtual Datacenter

Azure tillhandahåller både interna och tredje parts funktioner från vårt omfattande partner nätverk som ger dig en effektiv säkerhets virtualiseringsprodukter från. Det är viktigt att Microsoft tillhandahåller bästa praxis och vägledning i form av [Azure Virtual Data Center (VDC)](./networking-vdc.md). När du flyttar från en enskild arbets belastning till flera arbets belastningar som använder Hybrid funktioner, ger VDC vägledningen "recept" för att möjliggöra ett flexibelt nätverk som kommer att växa när dina arbets belastningar i Azure växer.

## <a name="next-steps"></a>Nästa steg

Styrning är avgörande för att Azure ska lyckas. Den här artikeln är riktad mot den tekniska implementeringen av en Enterprise-Autogenerera, men är bara touch på den bredare processen och relationerna mellan komponenterna. Princip styrningen flödar från toppen och bestäms av vad företaget vill uppnå. I naturlig grad har skapandet av en styrnings modell för Azure en företrädare från IT, men viktigare bör ha stark åter givning från affärs grupps ledare och säkerhets-och riskhanterings hantering. I slutet av företaget är ett företags Autogenerera om att minska affärs risken för att under lätta organisationens uppdrag och mål.

Nu när du har lärt dig om prenumerations styrning är det dags att se dessa rekommendationer i praktiken. Mer information finns i [metod tips för Azure-beredskap](../ready/azure-best-practices/index.md).
