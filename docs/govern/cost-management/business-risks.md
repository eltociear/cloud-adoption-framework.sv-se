---
title: Cost Management motivation och affärs risker
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Cost Management motivation och affärs risker
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 328352ac7ccd8cacbc92cc09ce0c07e2843afcf1
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031068"
---
# <a name="cost-management-motivations-and-business-risks"></a>Cost Management motivation och affärs risker

I den här artikeln beskrivs orsakerna till att kunderna vanligt vis antar en Cost Managements disciplin i en strategi för moln styrning. Det innehåller också några exempel på affärs risker som enhets princips instruktioner.

<!-- markdownlint-disable MD026 -->

## <a name="is-cost-management-relevant"></a>Är Cost Management relevant?

När det gäller kostnads styrning skapar moln införande en paradigm SKIFT. Hantering av kostnader i en traditionell lokal värld baseras på uppdaterings cykler, data Center förvärv, värd förnyelser och återkommande underhålls problem. Du kan prognostisera, planera och förfina var och en av dessa kostnader så att de överensstämmer med årliga kapital utgifts budgetar.

För moln lösningar tenderar många företag att ta en mer reaktiv metod för Cost Management. I många fall kommer företag att förköpa eller allokera till användning, en uppsättning moln tjänster. Den här modellen förutsätter att maximera rabatterna, baserat på hur mycket affärs planer det kostar med en speciell moln leverantör, och skapar en uppfattning om en proaktiv, planerad kostnads cykel. Den uppfattningen kommer dock endast att bli en verklighet om verksamheten också implementerar vuxen Cost Managements discipliner.

Molnet erbjuder självbetjänings funktioner som tidigare inte har funnits med i traditionella lokala data Center. De här nya funktionerna gör det möjligt för företag att vara mer flexibla, mindre restriktiva och mer öppna för att införa nya tekniker. Nack delen med självbetjäning är dock att slutanvändarna kan ta reda på mer än fördelade budgetar. Å andra sidan kan samma användare uppleva en förändring i planer och inte heller använda moln tjänsternas beräknade belopp. Risken för Skift i båda riktningarna motiverar investeringar i en Cost Management disciplin i styrnings teamet.

## <a name="business-risk"></a>Affärs risk

Cost Management disciplinen försöker lösa kärn affärs risker relaterade till utgifter som uppstår vid värdbaserade molnbaserade arbets belastningar. Arbeta med din verksamhet för att identifiera dessa risker och övervaka var och en av dem efter relevans när du planerar för och implementerar dina moln distributioner.

Riskerna varierar mellan olika organisationer, men följande fungerar som vanliga kostnads relaterade risker som du kan använda som utgångs punkt för diskussioner i din moln styrnings grupp:

- **Budget kontroll:** Att inte kontrol lera budgeten kan leda till orimliga utgifter med en moln leverantör.
- **Förlust av användning:** För-inköp eller för åtaganden som inte används kan leda till onödigt investeringar.
- **Utgifts avvikelser:** Oväntade toppar i båda riktningarna kan vara indikatorer för felaktig användning.
- **Överetablerade till gångar:** När till gångar distribueras i en konfiguration som överskrider behovet av ett program eller en virtuell dator (VM) kan de öka kostnaderna och skapa ett avfall.

## <a name="next-steps"></a>Nästa steg

Använd [moln hanterings mal len](./template.md)för att dokumentera affärs risker som sannolikt kommer att introduceras av den aktuella moln implementerings planen.

När en förståelse av realistiska affärs risker har upprättats är nästa steg att dokumentera affärs toleransen för risker och indikatorer och viktiga mått för att övervaka den toleransen.

> [!div class="nextstepaction"]
> [Förstå indikatorer, mått och risk tolerans](./metrics-tolerance.md)
