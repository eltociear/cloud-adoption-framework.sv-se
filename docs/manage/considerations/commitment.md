---
title: Verksamhets kritiskhet – moln hantering och åtgärder
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Verksamhets kritiskhet – moln hantering och åtgärder
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 7e7618163b15d17eab51571779e573dd9acb726e
ms.sourcegitcommit: 73dbedf580951f25bf4b5544b83451cb075b1fa1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/23/2019
ms.locfileid: "72805816"
---
# <a name="business-commitment-in-cloud-management"></a>Affärs engagemang i moln hantering

Att definiera ett affärs åtagande är en övning för att balansera prioriteringar. Målet är att justera rätt nivå för drifts hanteringen vid en acceptabel drifts kostnad. Att hitta detta saldo kräver några data punkter och beräkningar som beskrivs i följande avsnitt.

![Balansera kostnad och återhämtning](../../_images/manage/business-commitment-scale.png)

Åtaganden för affärs stabilitet (via teknisk återhämtning eller andra service avtals konsekvenser) är ett affärs justerings beslut. För de flesta arbets belastningar i en miljö räcker det med en bas linje nivå för moln hantering. För andra är en 2 &ndash;4x kostnads ökning lätt att motivera på grund av den potentiella effekten av eventuella affärs avbrott. Föregående artiklar i det här serie stödet för att förstå klassificeringen och effekten av avbrott i olika arbets belastningar. I den här artikeln får du hjälp med att beräkna returer. Som beskrivs i följande bild, på varje nivå av moln hantering, finns det Bryt punkter där kostnaden kan öka snabbare än ökad återhämtning. Dessa Bryt punkter kommer att uppmana detaljerade affärs beslut och affärs åtaganden.

## <a name="determining-a-proper-commitment-with-the-business"></a>Fastställa ett lämpligt åtagande för verksamheten

För varje arbets belastning i portföljen bör moln drifts teamet och moln strategi gruppen Justera på den hanterings nivå som tillhandahålls direkt av moln drifts teamet.

Följande är viktiga aspekter som du kan justera när du skapar ett åtagande i företaget:

- Krav för IT-åtgärder
- Hanterings ansvar
- Moln innehav
- Mjuka kostnads faktorer
- ROI för att undvika förlust
- Verifiera hanterings nivå

Resten av den här artikeln beskriver var och en av dessa kriterier för att hjälpa till med att fatta ett beslut.

## <a name="it-operations-prerequisites"></a>Krav för IT-åtgärder

Hanterings [guiden för Azure](../azure-management-guide/index.md) beskriver de hanterings verktyg som finns tillgängliga i Azure. Innan företaget uppnår sitt åtagande bör det fastställas en acceptabel bas linje för hantering av standard nivåer som ska tillämpas på alla hanterade arbets belastningar. DEN beräknar sedan en standard hanterings kostnad för var och en av de hanterade arbets belastningarna i IT-portföljen, baserat på antalet processor kärnor, disk utrymme och andra variabler som är relaterade till till gångar. Det skulle också uppskatta ett sammansatt service avtal för varje arbets belastning baserat på arkitekturen.

> [!TIP]
> IT-avdelningen använder ofta minst 99,9% drift tid för det första sammansatta service avtalet. De kan också välja att normalisera hanterings kostnader baserat på den genomsnittliga arbets belastningen, särskilt för lösningar med minimala loggnings-och lagrings behov. Genomsnitts kostnaden för ett fåtal arbets belastningar med medelhög allvarlighets grad kan ge en start punkt för inledande konversationer.

> [!TIP]
> För läsare som använder [arbets boken för OPS-hantering](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) för att planera för moln hantering, ska Ops-fälten uppdateras för att avspegla dessa krav. Fälten omfattar åtagande nivå, sammansatt service avtal och månatlig kostnad. Månads kostnaden bör motsvara kostnaden för de tillagda operativa hanterings verktygen varje månad.

Hanterings bas linjen för Operations Management fungerar som en första start punkt som ska verifieras i vart och ett av följande avsnitt.

## <a name="management-responsibility"></a>Hanterings ansvar

I en traditionell lokal miljö förutsätts kostnaden för att hantera miljön ofta vara en sunk kostnad som ägs av IT-avdelningen. I molnet är hanteringen ett ändamålsenlig-beslut med direkt budget påverkan. Kostnaderna för varje hanterings funktion kan direkt attributas till varje arbets belastning som distribueras till molnet. Den här metoden ger bättre kontroll, men det skapar ett krav för moln drifts grupper och moln strategi team för att först kunna genomföra ett avtal angående ansvars områden.

Organisationer kan också välja att få ut [vissa av de kontinuerliga hanterings funktionerna till en tjänst leverantör](https://www.microsoft.com/cloud-adoption-framework-offers?ot=manage). Dessa tjänst leverantörer kan använda [Azure-Lighthouse](https://azure.com/lighthouse) för att ge organisationer mer precision och kontroll över att bevilja åtkomst till sina resurser, tillsammans med större insyn i de åtgärder som utförs av tjänst leverantörerna.

**Delegerat ansvar:** Eftersom det inte finns något behov av att centralisera och ta hänsyn till drifts hanterings kostnader, kommer IT-avdelningen för många organisationer att ta upp nya metoder. Ett vanligt sätt kallas delegerat ansvar. I ett moln Center med en expert modell tillhandahåller plattforms åtgärder och plattforms automatisering självbetjänings hanterings verktyg som kan användas av affärs LED ande drifts grupper, oberoende av en central IT-grupp. Den här metoden ger affärs intressenterna fullständig kontroll över förvaltnings-relaterade budgetar. Det gör det också möjligt för CCoE att säkerställa att en minsta uppsättning guardrails implementeras korrekt. I den här modellen fungerar det som en Service Broker och en guide för att hjälpa verksamheten fatta beslut. Affärs åtgärder övervakar dagliga åtgärder för beroende arbets belastningar.

**Centraliserat ansvar:** Krav på efterlevnad, tekniska komplexitet och vissa delade tjänst modeller kan kräva en central IT-modell. I den här modellen fortsätter den att underhålla åtgärds hanterings ansvars områden. Därför kan miljö design, hanterings kontroller och styrnings verktyg hanteras centralt och kontrol leras, vilket begränsar affärs intressenternas roll när de gör förvaltnings åtaganden. Men när det gäller moln metoder i molnet är det mycket enklare för dig att göra det enklare att kommunicera kostnaderna och hanterings nivån för varje arbets belastning.

**Blandad modell:** Klassificeringen är i hjärtat av en blandad modell för hanterings ansvar. Företag som är i pågående för en omvandling från en lokal plats till molnet kan kräva en lokal-första drift modell för ett tag. Andra företag som har strikta krav på efterlevnad eller som är beroende av långsiktiga avtal med IT-leverantörer, kan kräva en central drifts modell. Trots dessa typer av begränsningar har företag ett behov av att förnya. När snabb innovation måste Flourish, i pågående för en central IT-ansvarig, kan klassificering och en blandad modell tillhandahålla balans. I den här metoden tillhandahåller central IT en centraliserad operativ modell för alla arbets belastningar som är verksamhets kritiska eller innehåller känslig information. Alla andra klassificeringar av arbets belastningar kan dock placeras i en moln miljö som är utformad för delegerade ansvars områden. Den centraliserade ansvars metoden fungerar som den allmänna drifts modellen. Företaget har sedan flexibiliteten att utnyttja en specialiserad operativ modell, baserat på den support nivå och känslighet som krävs.

Det första steget är att genomföra en ansvars metod som formar följande åtaganden.

**Vilken organisation kommer att vara ansvarig för daglig drifts hantering för den här arbets belastningen?**

## <a name="cloud-tenancy"></a>Moln innehav

För de flesta företag är hanteringen enklare när alla till gångar finns i en enda klient. Vissa organisationer kan dock behöva underhålla flera klienter. I artikeln om hur du [centraliserar hanterings åtgärder med Azure Lighthouse](../centralize-operations.md) får du några exempel där företag kan behöva Azure-miljöer med flera innehavare.

**Kommer den här arbets belastningen finnas i en enda Azure-klient, tillsammans med alla andra arbets belastningar?**

## <a name="soft-cost-factors"></a>Mjuka kostnads faktorer

Nästa avsnitt i den här artikeln beskriver en metod för jämför ande returer som är associerade med nivåer av hanterings processer och verktyg. I slutet av avsnittet mäter varje arbets belastning som analyseras kostnaden för hantering i förhållande till den prognostiserade effekten av verksamhets avbrott. Den metoden kommer att ge ett relativt enkelt sätt att förstå om investeringen i bättre hanterings metoder är motiverad.

Innan du kör siffrorna är det viktigt att titta på faktorerna med mjuka kostnader. Mjuka kostnads faktorer ger upphov till en retur, men det kan vara svårt att mäta genom direkt besparingar som skulle synas i en vinst-och förlust rapport. Faktorer med mjuka kostnader är viktiga eftersom de kan tyda på ett behov av att investera i en högre hanterings nivå än vad som är trygg.

Några exempel på dessa faktorer är:

- Daglig användning av en arbets belastning av tavlan eller VD: n.
- Användning av en arbets belastning med de _x främsta%_ av kunderna som leder till högre inkomst påverkan någon annan stans.
- Påverkan på nöjda anställda.

Nästa data punkt som krävs för att göra åtagandet är en lista över mjuka kostnads faktorer. De behöver inte dokumenteras i det här skedet, men företags från intressenter bör vara medvetna om betydelsen av dessa faktorer och deras undantag från följande beräkningar.

## <a name="calculate-loss-avoidance-roi"></a>Beräkna ROI för att undvika förlust

När du beräknar den relativa avkastningen på Operations Management-kostnader bör IT-teamet som ansvarar för moln åtgärder slutföra kraven ovan och anta en lägsta hanterings nivå för alla arbets belastningar.

Nästa åtagande att göras är ett godkännande av verksamheten för de kostnader som är förknippade med det grundläggande erbjudandet.

**Är företaget enigt om att investera i bas linje erbjudandet för att uppfylla minimi kraven för moln drift?**

Om företaget inte samtycker till den nivån av hantering måste en lösning skapas som gör det möjligt för verksamheten att fortsätta, utan att väsentligt påverka moln driften för andra arbets belastningar.

Om företaget vill ha mer än standard nivån, kommer resten av det här avsnittet att hjälpa dig att validera investeringen och de associerade returerna (i form av förlust).

### <a name="increased-levels-of-management-design-principles-and-service-catalog"></a>Förbättrade hanterings nivåer: design principer och tjänst katalog

För hanterade lösningar finns det flera design principer och mall-lösningar som kan tillämpas utöver hanterings bas linjen. Var och en av design principerna för tillförlitlighet och återhämtning ökar drifts kostnaderna för arbets belastningen. För IT och verksamheten att enas om dessa ytterligare åtaganden är det viktigt att förstå potentiella förluster som kan undvikas genom den ökade investeringen.

Följande beräkningar går igenom formler för att bättre förstå jämförelsen mellan förluster och ökade hanterings investeringar. Vägledning för att beräkna kostnaden för ökad hantering finns i artiklarna om automatisering av [arbets belastning](./workload.md) och [plattforms automatisering](./platform.md).

> [!TIP]
> För läsare som använder [arbets boken för OPS-hantering](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) för att planera för moln hantering, bör Ops-hanterings fälten uppdateras för att avspegla varje konversation. Fälten omfattar åtagande nivå, sammansatt service avtal och månatlig kostnad. Månads kostnaden bör motsvara kostnaden för de tillagda operativa hanterings verktygen varje månad. När de har uppdaterats uppdaterar dessa fält ROI-formlerna och vart och ett av följande fält.

### <a name="estimate-outage-hours-per-year"></a>Uppskatta avbrott (timmar per år)

Det "sammansatta service avtalet" är service nivå avtalet baserat på distributionen av varje till gång i arbets belastningen. Det fältet kommer att driva "uppskattat avbrott" (med etiketten Est. Avbrott * * * i arbets boken). Om du vill beräkna uppskattat avbrott i timmar per år utan att använda arbets boken, använder du följande formel:

**Uppskattat avbrott = (1 – sammansatt SLA-procent)/* antal timmar under ett år* *

I arbets boken används standardvärdet 8 760 timmar per år.

### <a name="standard-loss-impact"></a>Standard förlust påverkan

Standard förlust påverkan (med rubriken "standard påverkan" i arbets boken) uppskattar den finansiella effekten av eventuella avbrott, under förutsättning att förutsägelsen för "uppskattat avbrott" visar sig vara korrekt. Om du vill beräkna den här prognosen utan att använda arbets boken, använder du följande formel:

**Standard påverkan = uppskattat avbrott @ tre nio av drift tid/* tid/värde-effekt* *

Detta fungerar som en bas linje för kostnader, om affärs intressenterna väljer att investera i en högre hanterings nivå.

### <a name="composite-sla-impact"></a>Sammansatt SLA-påverkan

Sammansatta SLA-effekter (med rubriken "åtagande nivå påverkan" i arbets boken) tillhandahåller uppdaterad räkenskaps påverkan utifrån ändringarna i SLA för drift tid. På så sätt kan du jämföra de båda alternativen med den beräknade ekonomiska effekten. Använd följande formel för att beräkna den här prognostiserade påverkan utan kalkyl bladet.

**Sammansatt SLA-effekt = uppskattat avbrott/* tid/värde-effekt* *

Värdet representerar potentiella förluster som undviks av den ändrade åtagande nivån och det nya sammansatta service avtalet.

### <a name="comparison-basis"></a>Jämförelse bas

Jämförelse bas utvärderar standard effekter och sammansatt SLA-påverkan för att avgöra vilket som är lämpligast i kolumnen Return.

### <a name="return-on-loss-avoidance"></a>Undvika förlust av förlust

Om kostnaden för att hantera en arbets belastning överskrider potentiella förluster kan den föreslagna investeringen i moln hantering inte vara täten. Om du vill jämföra "Räntabilitet" för att undvika förlust, se kolumnen "årlig ROI * * * *". Använd följande formel för att beräkna den här kolumnen manuellt:

**Att undvika förlust av förlust = (jämförelse bas – (månatlig kostnad/* 12))//(månatlig kostnad/* 12)) **

Om det inte finns andra mjuka kostnads faktorer att överväga kan denna jämförelse snabbt föreslå om det bör finnas en djupare investering i moln drift, återhämtning, tillförlitlighet eller andra områden.

## <a name="validate-the-commitment"></a>Validera åtagandet

I processen har åtaganden gjorts: centraliserat eller delegerat ansvar, Azure-innehav och åtagande nivå.
Varje åtagande bör val IDE ras och dokumenteras för att säkerställa att moln drifts teamet, moln strategi teamet och affärs intressenterna är justerade på detta åtagande för att hantera arbets belastningen.

## <a name="next-steps"></a>Nästa steg

När åtaganden har gjorts kan de ansvariga drifts teamen Starta konfigurationen för arbets belastningen i fråga. Kom igång genom att utvärdera olika metoder för [inventering och synlighet](./inventory.md).

> [!div class="nextstepaction"]
> [Alternativ för inventering och synlighet](./inventory.md)
