---
title: Upprätta team strukturer
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Upprätta team strukturer
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: d87109d36075fb3d196b7bc681073141b6c1f44a
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/11/2019
ms.locfileid: "70906169"
---
# <a name="establish-team-structures"></a>Upprätta team strukturer

Alla moln funktioner tillhandahålls av någon under varje moln implementerings ansträngning. Dessa tilldelningar och team strukturer kan utvecklas ekologiskt, eller så kan de avsiktligt konstrueras för att matcha en definierad team struktur.

I takt med att implementeringen behöver växa, så behöver du bara balansera och strukturera. Den här artikeln innehåller exempel på vanliga team strukturer i olika faser av organisationens förfallo tid. Följande bild och lista visar en översikt över de strukturer som baseras på typiska mognads steg. Använd de här exemplen för att hitta den organisations struktur som bäst passar dina operativa behov.

![Mognadscykel för organisationer](../_images/ready/org-ready-maturity.png)

Organisations strukturer tenderar att gå igenom den gemensamma förfallo modellen som beskrivs här:

1. [Endast moln antagande team](#cloud-adoption-team-only)
2. [Bästa praxis för MVP](#best-practice-minimum-viable-product-mvp)
3. [Centrala IT](#central-it)
4. [Strategisk justering](#strategic-alignment)
5. [Drift justering](#operational-alignment)
6. [Expert Center i molnet (CCoE)](#cloud-center-of-excellence)

De flesta företag börjar med lite mer än ett *moln antagande team*. Vi rekommenderar dock att du upprättar en organisations struktur som liknar den [bästa övnings](#best-practice-minimum-viable-product-mvp) strukturen i MVP.

## <a name="cloud-adoption-team-only"></a>Endast moln antagande team

Nucleus av alla moln införande ansträngningar är moln implementerings teamet. Det här teamet styr de tekniska ändringar som möjliggör införande. Beroende på målen för implementerings ansträngningen kan det här teamet innehålla en mängd olika team medlemmar som hanterar en bred uppsättning tekniska och affärs uppgifter.

![Moln implementerings team med styrnings-och säkerhets team](../_images/ready/org-ready-adoption-only.png)

För användnings ansträngningar i små eller tidiga faser kan det här teamet vara så litet som en person. I större skala eller i sena steg är det vanligt att ha flera moln implementerings grupper, var och en med runt sex tekniker. Oavsett storlek eller uppgifter är den konsekventa aspekten av alla moln antagande team att det ger möjlighet att integrera lösningar i molnet. För vissa organisationer kan det vara en tillräckligt organisations struktur. I artikeln om [moln antagande teamet](./cloud-adoption.md) får du mer information om strukturen, sammansättningen och funktionerna i moln implementerings teamet.

> [!WARNING]
> *Endast* ett moln antagande team (eller flera moln antagande team) betraktas som ett antimönster och bör undvikas. Överväg att minst använda [bästa praxis för MVP](#best-practice-minimum-viable-product-mvp).

## <a name="best-practice-minimum-viable-product-mvp"></a>Bästa praxis: minimal livskraftig produkt (MVP)

Vi rekommenderar att du har två team för att skapa balans mellan moln införande aktiviteter. De här två teamen är ansvariga för olika funktioner under implementerings arbetet.

- **Molnimplementeringsteamet:** Det här teamet är ett konto för tekniska lösningar, affärs anpassning, projekt hantering och åtgärder för lösningar som antas.
- **Team för moln styrning:** För att balansera moln implementerings teamet är ett moln styrnings team dedikerat för att säkerställa en expert i de lösningar som antas. Moln styrnings teamet är ett konto för plattforms förfallo tid, plattforms åtgärder, styrning och automatisering.

![Moln införande med moln styrning counterbalance](../_images/ready/org-ready-best-practice.png)

Den här beprövade metoden betraktas som en MVP eftersom det kanske inte är hållbart. Varje lag har många tak, enligt beskrivningen i de [ *ansvariga, konto* bara, raci-diagram](./raci-alignment.md).

I följande avsnitt beskrivs en fullständigt bemannad, beprövad organisations struktur tillsammans med metoder för att anpassa en lämplig struktur till din organisation.

## <a name="central-it"></a>Centrala IT

I takt med att implementeringen skalas kan moln styrnings teamet ha svårt att hålla jämna steg med Innovations flödet från flera moln antagande team. Detta gäller särskilt i miljöer som har tung efterlevnad, åtgärder eller säkerhets krav. I det här skedet är det vanligt för företag att flytta moln ansvar till en befintlig central IT-grupp. Om teamet kan utvärdera verktyg, processer och personer för att få bättre stöd för moln användning i stor skala, och det centrala IT-teamet kan lägga till betydande värde. Att samla in experter från åtgärder, automatisering, säkerhet och administration till modernisera central IT kan driva effektiva operativa innovationer.

![Moln införande med en central IT-modell](../_images/ready/org-ready-central-it.png)

Tyvärr kan den centrala IT-fasen vara en av de riskiest faserna i organisationens mognad. Det centrala IT-teamet måste komma till tabellen med ett starkt ökande tänkesätt. Om teamet visar molnet som en möjlighet att växa och anpassa sina funktioner, kan det ge bra värde under hela processen. Men om det centrala IT-teamet tittar på moln införande främst som ett hot mot deras befintliga modell, blir det centrala IT-teamet ett hinder för moln implementerings teamen och de affärs mål som de har stöd för. Vissa centrala IT-team har tillbringat månader eller ännu år som försöker tvinga molnet att justeras med lokala metoder, med endast negativa resultat. Molnet kräver inte att allt förändras i Central IT, men det kräver ändring. Om motstånds kraft mot ändring är vanligt i det centrala IT-teamet kan den här fasen av mognaden snabbt bli ett kulturellt antimönster.

Moln implementerings planer är mycket fokuserade på PaaS (Platform as a Service), DevOps eller andra lösningar som kräver mindre drifts stöd är mindre sannolika för att se värdet under den här fasen av förfallo perioden. De här typerna av lösningar är i motsats till det mest sannolika eller blockeras av försöken att centralisera den. En högre förfallo nivå, som ett [moln Center med hög kvalitet (CCoE)](#cloud-center-of-excellence), är mer sannolikt att ge positiva resultat för dessa typer av bildning. Information om skillnaderna mellan centrala IT i molnet och en CCoE finns i [moln Center](./cloud-center-excellence.md).

## <a name="strategic-alignment"></a>Strategisk justering

Eftersom investeringen i moln implementeringen växer och affärs värden realiseras, blir affärs intressenter ofta mer engagerade. Ett definierat moln strategi team, som följande bild illustrerar, justerar dessa affärs intressenter för att maximera värdet som realiseras av moln införande investeringar.

![Lägg till ett definierat moln strategi team](../_images/ready/org-ready-strategy-aligned.png)

När förfallo tiden sker ekologiskt, till följd av IT-indikatorn för moln införande, kommer strategisk justering vanligt vis föregås av en styrning eller en central IT-grupp. När molnet antas leda till verksamhet är fokus på drifts modell och organisation att ske tidigare. När det är möjligt bör affärs resultat och moln strategi teamet båda definieras tidigt i processen.

## <a name="operational-alignment"></a>Drift justering

Att realisera affärs värde från moln implementerings ansträngningar kräver stabila åtgärder. Åtgärder i molnet kan kräva nya verktyg, processer eller kunskaper. När stabil IT-verksamhet krävs för att uppnå affärs resultat är det viktigt att lägga till ett definierat moln drifts team, som du ser här.

![Lägg till en definierad moln åtgärds grupp](../_images/ready/org-ready-operations-aligned.png)

Moln åtgärder kan levereras av de befintliga IT-drifts rollerna. Men det är inte ovanligt att moln åtgärder delegeras till andra parter utanför IT-verksamheten. Leverantörer av hanterade tjänster, DevOps-team och affär senheter förutsätter ofta ansvar som är kopplade till moln drift, med support och guardrails som tillhandahålls av IT-avdelningen. Detta är allt vanligare för moln implementerings ansträngningar som fokuserar på DevOps-eller PaaS-distributioner.

## <a name="cloud-center-of-excellence"></a>Molncenter för utmärkthet

Med högsta möjliga mognad är ett moln Center med hög expert att justera team runt en moln-första operativ modell. Den här metoden ger centrala IT-funktioner som styrning, säkerhet, plattform och automatisering.

![Molncenter för utmärkthet](../_images/ready/org-ready-ccoe.png)

Den främsta skillnaden mellan den här strukturen och den centrala IT-strukturen ovan är fokus på självbetjäning. Teamen i den här strukturen organiseras med avsikten att delegera kontroll så mycket som möjligt. Anpassning av styrning och efterlevnad till molnbaserade lösningar skapar guardrails och skydds metoder. Till skillnad från den centrala IT-modellen maximerar den molnbaserade metoden innovation och minimerar drifts kostnaderna. För att den här modellen ska kunna antas krävs ett ömsesidigt avtal för att modernisera IT-processer från företag och IT-ledande. Den här modellen är osannolik och kräver ofta support av chefer.

## <a name="next-steps"></a>Nästa steg

När du har justerat till en viss fas av organisationens struktur mognad kan du använda [raci-diagram](./raci-alignment.md) för att justera ansvar och ansvar i varje team.

> [!div class="nextstepaction"]
> [Justera lämpligt RACI-diagram](./raci-alignment.md)
