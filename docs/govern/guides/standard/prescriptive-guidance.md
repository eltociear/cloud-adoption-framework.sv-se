---
title: 'Standard Enterprise-guide: Vägledning förklaring'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig mer om vägledning för styrning i standard företag.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 8cc3c5564d51a096f2794ec62e50c19a2a8e740c
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031053"
---
# <a name="standard-enterprise-guide-prescriptive-guidance-explained"></a>Standard Enterprise-guide: Vägledning förklaring

Styrnings guiden börjar med en uppsättning inledande [företags principer](./initial-corporate-policy.md). Dessa principer används för att upprätta en styrnings MVP som återspeglar [rekommenderade metoder](./index.md).

I den här artikeln diskuterar vi de övergripande strategier som krävs för att skapa en styrnings MVP. Kärnan i styrnings MVP är [distributions accelerations](../../deployment-acceleration/index.md) disciplin. Verktygen och mönstren som används i det här skedet aktiverar de stegvisa förbättringar som krävs för att utöka styrningen i framtiden.

## <a name="governance-mvp-initial-governance-foundation"></a>Styrnings-MVP (inledande styrnings grund)

Snabbt införande av styrning och företags policy kan uppnås, tack vare några enkla principer och molnbaserad styrnings verktyg. Detta är de tre första ämnes områden som används för att gå vidare till styrnings processen. Varje disciplin beskrivs ytterligare i den här artikeln.

För att skapa start punkten diskuterar den här artikeln de övergripande strategierna bakom identitets bas linje, säkerhets bas linje och distributions acceleration som krävs för att skapa en styrnings-MVP som fungerar som grund för all införande.

![Exempel på en MVP för inkrementell styrnings](../../../_images/govern/governance-mvp.png)

## <a name="implementation-process"></a>Implementerings process

Implementeringen av styrnings-MVP: en har beroenden av identitet, säkerhet och nätverk. När beroenden har lösts bestämmer moln styrnings teamet några aspekter av styrningen. Besluten från moln styrnings teamet och från stöd team kommer att implementeras genom ett enda paket av verk ställande till gångar.

![Exempel på en MVP för inkrementell styrnings](../../../_images/govern/governance-mvp-implementation-flow.png)

Den här implementeringen kan också beskrivas med en enkel check lista:

1. Begär beslut angående kärn beroenden: Identitet, nätverk, övervakning och kryptering.
2. Bestäm vilket mönster som ska användas vid tillämpning av företags principen.
3. Fastställ lämpliga styrnings mönster för resurs konsekvens, resurs märkning och loggnings-och rapporterings disciplin.
4. Implementera styrnings verktygen som är justerade med det valda princip tillämpnings mönstret för att tillämpa de beroende besluten och styrnings besluten.

[!INCLUDE [implementation-process](../../../../includes/implementation-process.md)]

## <a name="application-of-governance-defined-patterns"></a>Program för styrnings definierade mönster

Moln styrnings teamet ansvarar för följande beslut och implementeringar. Många kräver indata från andra team, men moln styrnings teamet är sannolikt att äga både beslutet och implementeringen. I följande avsnitt beskrivs de beslut som fattas i det här användnings fallet och information om varje beslut.

### <a name="subscription-design"></a>Prenumerationsdesign

Beslutet om vilken prenumerations design som används avgör hur Azure-prenumerationer blir strukturerade och hur Azure-hanteringsportalen används för att effektivt hantera åtkomst, principer och efterlevnad för den här prenumerationen. I den här rapporten har styrnings teamet valt design mönster för prenumerationen [produktion och ej](../../../decision-guides/subscriptions/index.md#production-and-nonproduction-pattern) produktion.

- Avdelningar är inte troligt vis nödvändiga för det aktuella fokuset. Distributioner förväntas vara begränsade inom en enda fakturerings enhet. Vid antagandet är det inte ens ett företags avtal att centralisera faktureringen. Det är sannolikt att den här nivån av införande hanteras av en enda Azure-prenumeration med betala per användning.
- Oavsett om du använder EA-portalen eller om det finns ett Enterprise-avtal, bör en prenumerations modell fortfarande definieras och överenskommas för att minimera den administrativa administratören över bara faktureringen.
- En gemensam namngivnings konvention bör överenskommas som en del av prenumerations designen, baserat på de två föregående punkterna.

### <a name="resource-consistency"></a>Resurskonsekvens

Resurs konsekvens beslut avgör vilka verktyg, processer och ansträngningar som krävs för att säkerställa att Azure-resurser distribueras, konfigureras och hanteras konsekvent i en prenumeration. I det här avsnittet har **[distributions konsekvens](../../../decision-guides/resource-consistency/index.md#deployment-consistency)** valts som primärt resurs konsekvens mönster.

- Resurs grupper skapas för program som använder livs cykel metoden: allt som skapas tillsammans behålls tillsammans och återdäcken kan finnas i en enda resurs grupp.
- Azure Policy ska tillämpas på alla prenumerationer från den associerade hanterings gruppen.
- Som en del av distributions processen bör Azure Resource Consistency-mallar för resurs gruppen lagras i käll kontrollen.
- Varje resurs grupp är kopplad till en specifik arbets belastning eller ett program baserat på den livs cykel metod som beskrivs ovan.
- Med Azures hanterings grupper kan du uppdatera styrnings design som företags policy vuxen.
- En omfattande implementering av Azure Policy kan överskrida teamets tids åtaganden och kanske inte ger ett bra värde för just nu. En enkel standard princip bör dock skapas och appliceras på varje hanterings grupp för att genomdriva ett litet antal aktuella princip satser för moln styrning. Den här principen definierar implementeringen av särskilda styrnings krav. Dessa implementeringar kan sedan tillämpas på alla distribuerade till gångar.

>[!IMPORTANT]
>När en resurs i en resurs grupp inte längre delar samma livs cykel, bör den flyttas till en annan resurs grupp. Exempel på detta är vanliga databaser och nätverks komponenter. Även om de kan hantera programmet som utvecklas kan de också hantera andra och bör därför finnas i andra resurs grupper.

### <a name="resource-tagging"></a>Resursmärkning

Resurs märknings beslut avgör hur metadata tillämpas på Azure-resurser i en prenumeration för att stödja åtgärder, hantering och redovisnings syfte. I det här avsnittet har **[klassificerings](../../../decision-guides/resource-tagging/index.md#resource-tagging-patterns)** mönstret valts som standard modell för resurs taggning.

- Distribuerade till gångar ska taggas med:
  - Data klassificering
  - Allvarlighets grad
  - SLA
  - Miljö
- De här fyra värdena kommer att driva styrnings-, drift-och säkerhets beslut.
- Om den här styrnings guiden implementeras för en affär senhet eller ett team i ett större bolag bör taggning även innehålla metadata för fakturerings enheten.

### <a name="logging-and-reporting"></a>Loggning och rapportering

Vid loggning och rapportering bestäms hur lagrings logg data och hur övervaknings-och rapporterings verktyg som håller IT-personalen informerad om drifts hälsa är strukturerade. I det här fallet föreslås ett [Cloud-inbyggt mönster](../../../decision-guides/logging-and-reporting/index.md#cloud-native)* * för loggning och rapportering.

## <a name="incremental-improvement-of-governance-processes"></a>Stegvis förbättring av styrnings processer

Som styrnings ändringar kan vissa princip satser inte eller kontrol leras med automatiserade verktyg. Andra principer kommer att leda till insatser av IT-säkerhetsteamet och det lokala identitets hanterings teamet över tid. För att hjälpa till att hantera nya risker kan moln styrnings teamet övervaka följande processer.

**Implementerings acceleration:** Moln styrnings teamet har granskat distributions skript över flera team. De hanterar en uppsättning skript som fungerar som mallar för distribution. De mallarna används av moln antagande-och DevOps-teamen för att definiera distributioner snabbare. Vart och ett av dessa skript innehåller de nödvändiga kraven för att genomdriva en uppsättning styrnings principer utan ytterligare arbete från moln införande tekniker. Som Curators av dessa skript kan moln styrnings teamet snabbare implementera princip ändringar. Som ett resultat av skript hantering visas moln styrnings teamet som en källa för införande acceleration. Detta skapar konsekvens mellan distributioner, utan att det strikta framtvingas.

**Tekniker utbildning:** Moln styrnings teamet erbjuder två månads övningar och har skapat två videor för tekniker. Dessa material hjälper ingenjörerna att snabbt lära sig kulturen för styrning och hur saker utförs under distributioner. Teamet lägger till utbildnings till gångar som visar skillnaden mellan produktions-och distributioner av andra produkter, så att ingenjörerna förstår hur de nya principerna kommer att påverka implementeringen. Detta skapar konsekvens mellan distributioner, utan att det strikta framtvingas.

**Distributions planering:** Innan du distribuerar en till gång som innehåller skyddade data granskar moln styrnings gruppen distributions skript för att validera styrnings justering. Befintliga team med tidigare godkända distributioner kommer att granskas med hjälp av programmerings verktyg.

**Månatlig granskning och rapportering:** I varje månad kör moln styrnings gruppen en granskning av alla moln distributioner för att validera fortsatt justering av principen. När avvikelser upptäcks, dokumenteras de och delas med moln implementerings teamen. När tvång inte riskerar en affärs avbrott eller data läcka tillämpas principerna automatiskt. I slutet av granskningen sammanställer moln styrnings gruppen en rapport för moln strategi teamet och varje moln antagande team för att kommunicera den övergripande principen. Rapporten lagras också för granskning och juridiskt syfte.

**Kvartals vis princip granskning:** I varje kvartal granskar moln styrnings teamet och moln strategi teamet gransknings resultat och föreslår ändringar i företags principen. Många av dessa förslag är resultatet av kontinuerliga förbättringar och observationer av användnings mönster. Godkända princip ändringar är integrerade i styrnings verktyg under efterföljande gransknings cykler.

## <a name="alternative-patterns"></a>Alternativa mönster

Om något av de mönster som valts i den här styrnings guiden inte överensstämmer med läsarens krav, är alternativ till varje mönster tillgängliga:

- [Krypterings mönster](../../../decision-guides/encryption/index.md)
- [Identitets mönster](../../../decision-guides/identity/index.md)
- [Loggnings-och rapporterings mönster](../../../decision-guides/logging-and-reporting/index.md)
- [Princip tillämpnings mönster](../../../decision-guides/policy-enforcement/index.md)
- [Resurs konsekvens mönster](../../../decision-guides/resource-consistency/index.md)
- [Resurs markerings mönster](../../../decision-guides/resource-tagging/index.md)
- [Definierade nätverks mönster för program vara](../../../decision-guides/software-defined-network/index.md)
- [Design mönster för prenumeration](../../../decision-guides/subscriptions/index.md)

## <a name="next-steps"></a>Nästa steg

När den här guiden har implementerats kan varje moln antagande team gå vidare med en sund styrnings bas. Moln styrnings teamet kommer att fungera parallellt för att kontinuerligt uppdatera företags principerna och styrnings disciplinerna.

De två teamen använder tolerans indikatorerna för att identifiera nästa uppsättning förbättringar som krävs för att fortsätta att stödja moln införande. För det fiktiva företaget i den här guiden, förbättrar nästa steg säkerhets bas linjen för att stödja flytt av skyddade data till molnet.

> [!div class="nextstepaction"]
> [Förbättra säkerhets bas linje disciplinen](./security-baseline-improvement.md)
