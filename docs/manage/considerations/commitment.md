---
title: Affärs engagemang i moln hantering
description: Beräkna framtida resultat från klassificeringen och effekten av avbrott i olika arbets belastningar för att fatta bättre affärs beslut och åtaganden.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: ef06eca77f253bab2d743c7df44286f51f531606
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80430314"
---
# <a name="business-commitment-in-cloud-management"></a>Affärs engagemang i moln hantering

Att definiera _affärs engagemang_ är en övning för att balansera prioriteringar. Målet är att justera rätt nivå för drifts hanteringen vid en acceptabel drifts kostnad. Att hitta detta saldo kräver några data punkter och beräkningar som vi har lagt till i den här artikeln.

![Balansera kostnad och återhämtning](../../_images/manage/business-commitment-scale.png)

Åtaganden för affärs stabilitet, via teknisk återhämtning eller annat service avtal (SLA), är ett affärs justerings beslut. För de flesta arbets belastningar i en miljö räcker det med en bas linje nivå för moln hantering. För andra är en 2x till 4x-prisökning enkelt justerad på grund av den potentiella effekten av eventuella affärs avbrott.

I föregående artiklar i den här serien får du hjälp att förstå klassificeringen och effekten av avbrott i olika arbets belastningar. Den här artikeln hjälper dig att beräkna returer. Som illustreras i föregående bild, har varje nivå av moln hantering Bryt poäng där kostnaden kan öka snabbare än ökad återhämtning. Dessa Bryt punkter kommer att uppmana detaljerade affärs beslut och affärs åtaganden.

## <a name="determine-a-proper-commitment-with-the-business"></a>Fastställ ett lämpligt åtagande för verksamheten

För varje arbets belastning i portföljen bör moln drifts teamet och moln strategi gruppen Justera på den hanterings nivå som tillhandahålls direkt av moln drifts teamet.

När du skapar ett åtagande med verksamheten finns det några viktiga aspekter att justera:

- Krav för IT-åtgärder
- Hanterings ansvar
- Moln innehav
- Mjuka kostnads faktorer
- ROI för att undvika förlust
- Validering av hanterings nivå

För att hjälpa dig i besluts processen beskriver resten av den här artikeln var och en av dessa aspekter i större detalj.

## <a name="it-operations-prerequisites"></a>Krav för IT-åtgärder

Hanterings [guiden för Azure](../azure-management-guide/index.md) beskriver de hanterings verktyg som är tillgängliga i Azure. Innan företaget uppnår sitt åtagande bör det fastställas en acceptabel hanterings bas linje på standard nivå som ska tillämpas på alla hanterade arbets belastningar. DEN beräknar sedan en standard hanterings kostnad för var och en av de hanterade arbets belastningarna i IT-portföljen, baserat på antalet processor kärnor, disk utrymme och andra variabler som är relaterade till till gångar. Det skulle också uppskatta ett sammansatt service avtal för varje arbets belastning, baserat på arkitekturen.

> [!TIP]
> IT-avdelningen använder ofta ett minimum av 99,9 procents drift tid för det första sammansatta service avtalet. De kan också välja att normalisera hanterings kostnader baserat på den genomsnittliga arbets belastningen, särskilt för lösningar med minimala loggnings-och lagrings behov. Genomsnitts kostnaden för ett fåtal arbets belastningar med medelhög allvarlighets grad kan ge en start punkt för inledande konversationer.

<!-- -->

> [!TIP]
> Om du använder [arbets boken för OPS-hantering](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) för att planera för moln hantering, ska Ops Management-fälten uppdateras för att avspegla dessa krav. Fälten omfattar _åtagande nivå_, _sammansatt service avtal_och _månatlig kostnad_. Månads kostnaden bör motsvara kostnaden för de tillagda operativa hanterings verktygen varje månad.

Bas linjen för Operations Management fungerar som en första start punkt som verifieras i vart och ett av följande avsnitt.

## <a name="management-responsibility"></a>Hanterings ansvar

I en traditionell lokal miljö förutsätts kostnaden för att hantera miljön ofta vara en sunk kostnad som ägs av IT-driften. I molnet är hanteringen ett ändamålsenlig-beslut med direkt budget påverkan. Kostnaderna för varje hanterings funktion kan direkt attributas till varje arbets belastning som har distribuerats till molnet. Den här metoden ger bättre kontroll, men det skapar ett krav för moln drifts team och moln strategi team för att först kunna genomföra ett avtal om ansvars områden.

Organisationer kan också välja att [hantera några av de kontinuerliga hanterings funktionerna till en tjänst leverantör](https://www.microsoft.com/cloud-adoption-framework-offers?ot=manage). Dessa tjänst leverantörer kan använda [Azure-Lighthouse](https://azure.com/lighthouse) för att ge organisationer mer exakt kontroll över att bevilja åtkomst till sina resurser, tillsammans med större insyn i de åtgärder som utförs av tjänst leverantörerna.

- **Delegerat ansvar:** Eftersom det inte finns något behov av att centralisera och ta hänsyn till drifts hanterings kostnader, kommer IT-avdelningen för många organisationer att ta upp nya metoder. Ett vanligt sätt kallas _delegerat ansvar_. I ett moln Center med en expert modell tillhandahåller plattforms åtgärder och plattforms automatisering självbetjänings hanterings verktyg som kan användas av affärs LED ande drifts grupper, oberoende av en central IT-grupp. Den här metoden ger affärs intressenter fullständig kontroll över förvaltnings-relaterade budgetar. Det gör det också möjligt för CCoE-teamet (Cloud Center of expert) att se till att en minsta uppsättning guardrails har implementerats korrekt. I den här modellen fungerar det som en Service Broker och en guide för att hjälpa verksamheten fatta beslut. Affärs åtgärder övervakar dagliga åtgärder för beroende arbets belastningar.

- **Centraliserat ansvar:** Krav på efterlevnad, tekniska komplexitet och vissa delade tjänst modeller kan kräva en _Central IT_ -modell. I den här modellen fortsätter den att utöva sitt ansvar för drifts hantering. Miljö design, hanterings kontroller och styrnings verktyg kan hanteras centralt och kontrol leras, vilket begränsar rollen hos affärs intressenter i syfte att hantera åtaganden. Men insynen i moln metodernas kostnad och arkitektur gör det mycket enklare för dig att centralisera IT-kostnaden och hanterings nivån för varje arbets belastning.

- **Blandad modell:** Klassificeringen är kärnan i en _blandad modell_ av hanterings ansvars områden. Företag som befinner sig i pågående av en omvandling från en lokal plats till molnet kan kräva en lokal-första drift modell för ett tag. Företag med strikta krav på efterlevnad eller som är beroende av långsiktiga avtal med IT-leverantörer, kan kräva en central drifts modell.

  Oavsett begränsningar måste dagens företag förnyas. När snabb innovation måste Flourish, i pågående i en central IT-, Central-och ansvars modell, kan en blandad modell metod tillhandahålla balans. I den här metoden tillhandahåller central IT en centraliserad operativ modell för alla arbets belastningar som är verksamhets kritiska eller innehåller känslig information. Samtidigt kan alla andra arbets belastnings klassificeringar placeras i en moln miljö som är utformad för delegerad ansvars tid. Den centraliserade ansvars metoden fungerar som den allmänna drifts modellen. Företaget är sedan flexibelt att använda en specialiserad operativ modell, baserat på den nödvändiga nivån av support och känslighet.

Det första steget är att genomföra en ansvars metod, som sedan formar följande åtaganden.

**Vilken organisation ansvarar för den dagliga driften av drifts hantering för den här arbets belastningen?**

## <a name="cloud-tenancy"></a>Moln innehav

För de flesta företag är hanteringen enklare när alla till gångar finns i en enda klient. Vissa organisationer kan dock behöva underhålla flera klienter. Information om varför en verksamhet kan kräva en Azure-miljö med flera innehavare finns i [centralisera hanterings åtgärder med Azure Lighthouse](../centralize-operations.md).

**Kommer den här arbets belastningen finnas i en enda Azure-klient, tillsammans med alla andra arbets belastningar?**

## <a name="soft-cost-factors"></a>Mjuka kostnads faktorer

Nästa avsnitt beskriver en metod för jämför ande returer som är associerade med nivåer av hanterings processer och verktyg. I slutet av avsnittet mäter varje analyserad arbets belastning kostnaden för hantering i förhållande till prognos effekten av affärs avbrott. Den här metoden är ett relativt enkelt sätt att förstå om en investering i bättre hanterings metoder är motiverad.

Innan du kör numren är det viktigt att titta på faktorerna med mjuka kostnader. Kostnader för mjuka kostnader ger en retur, men det kan vara svårt att mäta genom direkta besparingar av hård kostnad som skulle synas i en vinst-och förlust instruktion. Faktorer med mjuka kostnader är viktiga eftersom de kan tyda på ett behov av att investera i en högre hanterings nivå än vad som är trygg.

Några exempel på mjuka kostnads faktorer är:

- Daglig arbets belastnings användning av tavlan eller VD: n.
- Arbets belastnings användning med de _x främsta procenten_ av kunderna som leder till en större inkomst påverkan någon annan stans.
- Påverkan på nöjda anställda.

Nästa data punkt som krävs för att göra åtagandet är en lista över mjuka kostnads faktorer. Dessa faktorer behöver inte dokumenteras i det här skedet, men affärs intressenter bör vara medvetna om betydelsen av dessa faktorer och deras undantag från följande beräkningar.

## <a name="calculate-loss-avoidance-roi"></a>Beräkna ROI för att undvika förlust

När den relativa avkastningen på Operations Management-kostnader beräknas bör IT-teamet som ansvarar för moln åtgärder slutföra de tidigare nämnda förutsättningarna och anta en lägsta hanterings nivå för alla arbets belastningar.

Nästa åtagande att göras är ett godkännande av verksamheten för de kostnader som är förknippade med det grundläggande erbjudandet.

**Är företaget enigt om att investera i bas linje erbjudandet för att uppfylla minimi kraven för moln drift?**

Om företaget inte samtycker till den nivån av hantering måste en lösning skapas som gör det möjligt för verksamheten att fortsätta, utan att väsentligt påverka moln driften för andra arbets belastningar.

Om företaget vill ha mer än standard hanterings nivån, kommer resten av det här avsnittet att hjälpa dig att validera investeringen och de associerade returerna (i form av förlust).

### <a name="increased-levels-of-management-design-principles-and-service-catalog"></a>Förbättrade hanterings nivåer: design principer och tjänst katalog

För hanterade lösningar kan flera design principer och mall lösningar tillämpas utöver hanterings bas linjen. Var och en av design principerna för tillförlitlighet och återhämtning ökar drifts kostnaderna för arbets belastningen. För IT och verksamheten att enas om dessa ytterligare åtaganden är det viktigt att förstå potentiella förluster som kan undvikas genom den ökade investeringen.

Följande beräkningar går igenom formler för att hjälpa dig att bättre förstå skillnaderna mellan förluster och ökade hanterings investeringar. Vägledning för att beräkna kostnaden för ökad hantering finns i automatisering av [arbets belastning](./workload.md) och [plattforms automatisering](./platform.md).

> [!TIP]
> Om du använder [arbets boken för OPS-hantering](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) för att planera för moln hantering uppdaterar du hanterings fälten för OPS så att de återspeglar varje konversation. Fälten omfattar _åtagande nivå_, _sammansatt service avtal_och _månatlig kostnad_. Månads kostnaden bör motsvara månads kostnaden för de verktyg som har lagts till för drifts hantering. Efter att de har uppdaterats uppdaterar fälten ROI-formlerna och var och en av följande fält.

### <a name="estimate-outage-hours-per-year"></a>Uppskatta avbrott (timmar per år)

Sammansatt service avtal är ett avtal för service nivå som baseras på distributionen av varje till gång i arbets belastningen. Fältet driver _uppskattat avbrott_ (märkt _Est. avbrott_ i arbets boken). Om du vill beräkna uppskattat avbrott i timmar per år utan att använda arbets boken, använder du följande formel:

> _Uppskattat avbrott = (1 – sammansatt SLA &#215; -procent) antal timmar under ett år_

Arbets boken använder standardvärdet _8 760 timmar per år_.

### <a name="standard-loss-impact"></a>Standard förlust påverkan

_Standard förlust påverkan_ (med etiketten _standard påverkan_ i arbets boken) prognoserar den ekonomiska effekten av eventuella avbrott, förutsatt att den _uppskattade avbrotts_ förutsägelsen bevisar korrekt. Om du vill beräkna den här prognosen utan att använda arbets boken, använder du följande formel:

> _Standard påverkan = uppskattat avbrott @ tre nior av &#215; drift tid – värde påverkan_

Detta fungerar som en bas linje för kostnader, om affärs intressenterna väljer att investera i en högre hanterings nivå.

### <a name="composite-sla-impact"></a>Sammansatt SLA-påverkan

_Sammansatta SLA-effekter_ (märkta _åtagande nivåer_ i arbets boken) tillhandahåller uppdaterad räkenskaps påverkan baserat på ändringar i SLA för drift tid. Med den här beräkningen kan du jämföra de båda alternativen med den beräknade ekonomiska effekten. Om du vill beräkna den här prognos effekten utan kalkyl bladet, använder du följande formel:

> _Sammansatt SLA-effekt = uppskattad tid för avbrott &#215; -värde påverkan_

Värdet representerar potentiella förluster som undviks av den ändrade åtagande nivån och det nya sammansatta service avtalet.

### <a name="comparison-basis"></a>Jämförelse bas

_Jämförelse bas_ utvärderar standard effekter och sammansatt SLA-påverkan för att avgöra vilket som är lämpligast i kolumnen Return.

### <a name="return-on-loss-avoidance"></a>Undvika förlust av förlust

Om kostnaden för att hantera en arbets belastning överskrider potentiella förluster kan den föreslagna investeringen i moln hantering vara täten. Information om hur du kan _undvika att förlora avkastningen_finns i kolumnen _årlig ROI * * *_ *. Om du vill beräkna den här kolumnen på egen hand använder du följande formel:

> _Att undvika förlust av förlust = (jämförelse bas – (månatlig kostnad &#215; 12)) &#247; (månatlig kostnad &#215; 12))_

Om det inte finns andra mjuka kostnads faktorer att överväga kan denna jämförelse snabbt föreslå om det bör finnas en djupare investering i moln drift, återhämtning, tillförlitlighet eller andra områden.

## <a name="validate-the-commitment"></a>Validera åtagandet

I processen har åtaganden gjorts: centraliserat eller delegerat ansvar, Azure-innehav och åtagande nivå. Varje åtagande bör val IDE ras och dokumenteras för att säkerställa att moln drifts teamet, moln strategi teamet och affärs intressenterna är justerade på detta åtagande för att hantera arbets belastningen.

## <a name="next-steps"></a>Nästa steg

När åtagandena har gjorts kan de ansvariga Operations teamen börja konfigurera arbets belastningen i fråga. Kom igång genom att utvärdera olika metoder för [inventering och synlighet](./inventory.md).

> [!div class="nextstepaction"]
> [Alternativ för inventering och synlighet](./inventory.md)
