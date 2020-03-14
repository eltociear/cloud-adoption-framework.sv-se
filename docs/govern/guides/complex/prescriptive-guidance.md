---
title: 'Komplex företags styrning: metod tips förklaras'
description: Använd ramverket för moln införande för Azure för att upprätta en minimal livskraftig produkt (MVP) för styrning som återspeglar bästa praxis för ett komplext företag.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 74f81e139e7eacc7445321592eab4027a40a8c56
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79312390"
---
# <a name="governance-guide-for-complex-enterprises-best-practices-explained"></a>Styrnings guide för komplexa företag: bästa praxis förklaras

Styrnings guiden börjar med en uppsättning inledande [företags principer](./initial-corporate-policy.md). Dessa principer används för att upprätta en minimal livskraftig produkt (MVP) för styrning som återspeglar [bästa praxis](./index.md).

I den här artikeln diskuterar vi de övergripande strategier som krävs för att skapa en styrnings MVP. Kärnan i styrnings MVP är [distributions accelerations](../../deployment-acceleration/index.md) disciplin. Verktygen och mönstren som används i det här skedet aktiverar de stegvisa förbättringar som krävs för att utöka styrningen i framtiden.

## <a name="governance-mvp-initial-governance-foundation"></a>Styrnings-MVP (inledande styrnings grund)

Snabbt införande av styrning och företags policy kan uppnås, tack vare några enkla principer och molnbaserad styrnings verktyg. Det här är den första av de tre styrnings disciplinerna för att gå till tillvägagångs sättet för styrnings processer. Varje disciplin förklaras ytterligare i den här artikeln.

För att skapa start punkten diskuterar den här artikeln de övergripande strategierna bakom identitets bas linje, säkerhets bas linje och distributions acceleration som krävs för att skapa en styrnings-MVP som fungerar som grund för all införande.

![Exempel på en MVP för inkrementell styrnings](../../../_images/govern/governance-mvp.png)

## <a name="implementation-process"></a>Implementerings process

Implementeringen av styrnings-MVP: en har beroenden av identitet, säkerhet och nätverk. När beroenden har lösts bestämmer moln styrnings teamet några aspekter av styrningen. Besluten från moln styrnings teamet och från stöd team kommer att implementeras genom ett enda paket av verk ställande till gångar.

![Exempel på en MVP för inkrementell styrnings](../../../_images/govern/governance-mvp-implementation-flow.png)

Den här implementeringen kan också beskrivas med en enkel check lista:

1. Begär beslut angående kärn beroenden: identitet, nätverk och kryptering.
1. Bestäm vilket mönster som ska användas vid tillämpning av företags principen.
1. Fastställ lämpliga styrnings mönster för resurs konsekvens, resurs märkning och loggnings-och rapporterings disciplin.
1. Implementera styrnings verktygen som är justerade med det valda princip tillämpnings mönstret för att tillämpa de beroende besluten och styrnings besluten.

[!INCLUDE [implementation-process](../../../../includes/implementation-process.md)]

## <a name="application-of-governance-defined-patterns"></a>Program för styrnings definierade mönster

Moln styrnings teamet kommer att ansvara för följande beslut och implementeringar. Många kräver indata från andra team, men moln styrnings teamet kan förmodligen äga både beslutet och implementeringen. I följande avsnitt beskrivs de beslut som fattas i det här användnings fallet och information om varje beslut.

### <a name="subscription-design"></a>Prenumerationsdesign

Beslutet om vilken prenumerations design som används avgör hur Azure-prenumerationer blir strukturerade och hur Azure-hanteringsportalen används för att effektivt hantera åtkomst, principer och efterlevnad för den här prenumerationen. I den här gruppen har styrnings teamet valt design mönstret **[blandad](../../../decision-guides/subscriptions/index.md#mixed-patterns)** prenumeration.

- När nya begär Anden för Azure-resurser uppstår, ska en "avdelning" upprättas för varje större affär senhet i varje operativ geografi. I varje avdelning bör prenumerationer skapas för varje program archetype.
- Ett program archetype är ett sätt att gruppera program med liknande behov. Vanliga exempel är: program med skyddade data, styrda program (t. ex. HIPAA eller FedRAMP), låg risk program, program med lokala beroenden, SAP eller andra stordator program i Azure eller program som utökar lokala SAP-eller stordator program. Varje organisation har unika behov baserat på data klassificeringar och de typer av program som stöder verksamheten. Beroende mappning av den digitala fastigheten kan hjälpa till att definiera programmet archetypes i en organisation.
- En gemensam namngivnings konvention bör överenskommas som en del av prenumerations designen, baserat på de två punkterna ovan.

### <a name="resource-consistency"></a>Resurskonsekvens

Resurs konsekvens beslut avgör vilka verktyg, processer och ansträngningar som krävs för att säkerställa att Azure-resurser distribueras, konfigureras och hanteras konsekvent i en prenumeration. I det här avsnittet har **[distributions konsekvens](../../../decision-guides/resource-consistency/index.md#deployment-consistency)** valts som primärt resurs konsekvens mönster.

- Resurs grupper skapas för program som använder livs cykel metoden. Allt som skapas, underhålls och dras tillbaka tillsammans bör finnas i en enda resurs grupp. Mer information om resurs grupper finns [här](../../../decision-guides/resource-consistency/index.md#basic-grouping).
- Azure Policy ska tillämpas på alla prenumerationer från den associerade hanterings gruppen.
- Som en del av distributions processen bör Azure Resource Consistency-mallar för resurs gruppen lagras i käll kontrollen.
- Varje resurs grupp är kopplad till en specifik arbets belastning eller ett program baserat på den livs cykel metod som beskrivs ovan.
- Med Azures hanterings grupper kan du uppdatera styrnings design som företags policy vuxen.
- En omfattande implementering av Azure Policy kan överskrida teamets tids åtaganden och kanske inte ger ett bra värde för just nu. En enkel standard princip bör dock skapas och appliceras på varje hanterings grupp för att genomdriva ett litet antal aktuella princip satser för moln styrning. Den här principen definierar implementeringen av särskilda styrnings krav. Dessa implementeringar kan sedan tillämpas på alla distribuerade till gångar.

>[!IMPORTANT]
>När en resurs i en resurs grupp inte längre delar samma livs cykel, bör den flyttas till en annan resurs grupp. Exempel på detta är vanliga databaser och nätverks komponenter. Även om de kan hantera programmet som utvecklas kan de också hantera andra och bör därför finnas i andra resurs grupper.

### <a name="resource-tagging"></a>Resursmärkning

Resurs märknings beslut avgör hur metadata tillämpas på Azure-resurser i en prenumeration för att stödja åtgärder, hantering och redovisnings syfte. I detta skick har **[redovisnings](../../../decision-guides/resource-tagging/index.md#resource-tagging-patterns)** mönstret valts som standard modell för resurs taggning.

- Distribuerade till gångar ska taggas med värden för:
  - Avdelning/fakturerings enhet
  - Placering
  - Data klassificering
  - Allvarlighets grad
  - SLA
  - Miljö
  - Program archetype
  - Program
  - Program ägare
- Dessa värden tillsammans med hanterings gruppen för Azure och prenumerationen som är kopplade till en distribuerad till gång kommer att driva styrnings-, drift-och säkerhets beslut.

### <a name="logging-and-reporting"></a>Loggning och rapportering

Vid loggning och rapportering bestäms hur lagrings logg data och hur övervaknings-och rapporterings verktyg som håller IT-personalen informerad om drifts hälsa är strukturerade. I den här rapporten föreslås ett **[hybrid övervaknings](../../../decision-guides/logging-and-reporting/index.md)** mönster för loggning och rapportering, men krävs inte för någon utvecklings grupp just nu.

- Inga styrnings krav har angetts för de särskilda data punkter som ska samlas in för loggning eller rapportering. Detta är särskilt för denna fiktiva information och bör betraktas som ett antimönster. Loggnings standarder bör fastställas och framtvingas så snart som möjligt.
- Ytterligare analys krävs före lanseringen av skyddade data eller verksamhets kritiska arbets belastningar.
- Innan du får stöd för skyddade data eller verksamhets kritiska arbets belastningar måste den befintliga lokala lösningen för drift övervakning beviljas åtkomst till arbets ytan som används för loggning. Program krävs för att uppfylla säkerhets-och loggnings krav som är kopplade till användningen av den klienten, om programmet ska stödjas med ett definierat service avtal.

## <a name="incremental-of-governance-processes"></a>Stegvisa styrnings processer

Vissa princip instruktioner får inte eller styras av automatiserade verktyg. Andra principer kräver regelbunden ansträngning från IT-säkerhet och lokala identitets bas grupper. Moln styrnings teamet måste övervaka följande processer för att implementera de sista åtta princip satserna:

**Ändringar i företags princip:** Moln styrnings teamet kommer att göra ändringar i styrnings MVP-designen för att införa de nya principerna. Värdet för styrnings-MVP: t är att det kommer att tillåta automatisk verk ställande av de nya principerna.

**Implementerings acceleration:** Moln styrnings teamet har granskat distributions skript över flera team. De har bevarat en uppsättning skript som fungerar som mallar för distribution. Dessa mallar kan användas av moln implementerings teamen och DevOps team för att snabbt definiera distributioner. Varje skript innehåller kraven för att verkställa styrnings principer och ytterligare insatser från moln införande tekniker behövs inte. Som Curators av dessa skript kan de implementera princip ändringar snabbare. De visas dessutom som acceleratorer för införande. Detta säkerställer konsekventa distributioner utan att det är absolut framtvingande.

**Tekniker utbildning:** Moln styrnings teamet erbjuder två månads övningar och har skapat två videor för tekniker. Båda resurserna hjälper ingenjörer att snabbt komma igång med styrnings kulturen och hur distributioner utförs. Teamet lägger till utbildnings resurser för att demonstrera skillnaden mellan produktions-och distributioner av andra produkter, vilket hjälper ingenjörer att förstå hur de nya principerna påverkar införande. Detta säkerställer konsekventa distributioner utan att det är absolut framtvingande.

**Distributions planering:** Innan du distribuerar en till gång som innehåller skyddade data kommer moln styrnings teamet att ansvara för att granska distributions skript för att validera styrnings justering. Befintliga team med tidigare godkända distributioner kommer att granskas med hjälp av programmerings verktyg.

**Månatlig granskning och rapportering:** I varje månad kör moln styrnings gruppen en granskning av alla moln distributioner för att validera fortsatt justering av principen. När avvikelser upptäcks, dokumenteras de och delas med moln implementerings teamen. När tvång inte riskerar en affärs avbrott eller data läcka tillämpas principerna automatiskt. I slutet av granskningen sammanställer moln styrnings gruppen en rapport för moln strategi teamet och varje moln antagande team för att kommunicera den övergripande principen. Rapporten lagras också för granskning och juridiskt syfte.

**Kvartals vis princip granskning:** Varje kvartal, moln styrnings teamet och moln strategi teamet för att granska gransknings resultat och föreslå ändringar i företags policyn. Många av dessa förslag är resultatet av kontinuerliga förbättringar och observationer av användnings mönster. Godkända princip ändringar är integrerade i styrnings verktyg under efterföljande gransknings cykler.

## <a name="alternative-patterns"></a>Alternativa mönster

Om något av mönstren som valts i den här styrnings guiden inte överensstämmer med läsarens krav, är alternativ till varje mönster tillgängliga:

- [Krypterings mönster](../../../decision-guides/encryption/index.md)
- [Identitets mönster](../../../decision-guides/identity/index.md)
- [Loggnings-och rapporterings mönster](../../../decision-guides/logging-and-reporting/index.md)
- [Princip tillämpnings mönster](../../../decision-guides/policy-enforcement/index.md)
- [Resurs konsekvens mönster](../../../decision-guides/resource-consistency/index.md)
- [Resurs markerings mönster](../../../decision-guides/resource-tagging/index.md)
- [Definierade nätverks mönster för program vara](../../../decision-guides/software-defined-network/index.md)
- [Design mönster för prenumeration](../../../decision-guides/subscriptions/index.md)

## <a name="next-steps"></a>Nästa steg

När den här vägledningen har implementerats kan varje moln antagande team fortsätta med en solid styrnings grund. På samma gång kommer moln styrnings teamet att arbeta kontinuerligt för att kontinuerligt uppdatera företags principerna och styrnings disciplinerna.

Båda teamen använder tolerans indikatorerna för att identifiera nästa uppsättning förbättringar som krävs för att fortsätta att stödja moln införande. Nästa steg för det här företaget är en stegvis förbättring av deras styrnings bas linje för att stödja program med äldre eller tredjeparts Multi-Factor Authentication-krav.

> [!div class="nextstepaction"]
> [Förbättra disciplinen för identitets bas linjer](./identity-baseline-improvement.md)
