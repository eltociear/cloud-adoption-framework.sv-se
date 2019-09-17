---
title: Genomför en granskning av moln principen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig hur du utför en granskning av en moln princip.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 167613bd304505bc53128c2864250e5cae80b281
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028824"
---
<!-- markdownlint-disable MD026 -->

# <a name="conduct-a-cloud-policy-review"></a>Genomför en granskning av moln principen

En moln princip granskning är det första steget mot [styrningens förfallo tid](../index.md) i molnet. Syftet med den här processen är att modernisera befintliga företags IT-principer. När det är klart ger de uppdaterade principerna en motsvarande nivå av riskhantering för molnbaserade resurser. I den här artikeln förklaras gransknings processen för moln policyn och dess betydelse.

## <a name="why-perform-a-cloud-policy-review"></a>Varför ska jag göra en granskning av moln principer?

De flesta företag hanterar det genom att köra processer som är av samma justering med styrnings principer. I små företag kan dessa principer anecdotal och processer lösas lösa. I takt med att företag växer i stora företag brukar principer och processer vara tydligare dokumenterade och utföras på ett konsekvent sätt.

Som företag mogna IT-principer har beroenden för tidigare tekniska beslut en tendens att seep i principer för principer. Till exempel är det gemensamt för att se haveri beredskaps processer en princip som bestämmer externa band säkerhets kopieringar. Detta förutsätter ett beroende på en typ av teknik (band säkerhets kopiering) som kanske inte längre är den mest relevanta lösningen.

Moln omvandlingar skapar en naturlig Bryt punkt för att se över de tidigare princip besluten tidigare. Tekniska funktioner och standard processer förändras avsevärt i molnet, precis som de ärver risker. I föregående exempel har säkerhets kopierings principen för band som har samlats in från risken för en enskild felpunkt genom att lagra data på en plats och företaget behöver minimera risk profilen genom att begränsa risken. I en moln distribution finns det flera alternativ som ger samma risk minskning, med mycket lägre återställnings tid (RTO). Exempel:

- En molnbaserad lösning kan möjliggöra geo-replikering av Azure SQL Database.
- En hybrid lösning kan använda Azure Site Recovery för att replikera en IaaS-arbetsbelastning till flera data Center.

När en moln omvandling körs, styr principerna ofta många av de verktyg, tjänster och processer som är tillgängliga för moln implementerings teamen. Om dessa principer är baserade på äldre tekniker kan de hindra teamets ansträngningar att ändra på enheten. I värsta fall ignoreras viktiga principer helt av migration-teamet för att aktivera lösningar. Inget är ett acceptabelt resultat.

## <a name="the-cloud-policy-review-process"></a>Moln princip gransknings processen

Moln princip granskningar justerar befintlig IT-styrning och IT-säkerhetsprinciper med [fem ämnes områden i moln styrning](../index.md): [Cost Management](../cost-management/index.md), [säkerhets bas linje](../security-baseline/index.md), [identitets bas](../identity-baseline/index.md)linje, [resurs konsekvens](../resource-consistency/index.md)och [distributions acceleration](../deployment-acceleration/index.md).

För var och en av dessa ämnes områden följer gransknings processen följande steg:

1. Granska befintliga lokala principer som är relaterade till den specifika disciplinen, och leta efter två viktiga data punkter: äldre beroenden och identifierade affärs risker.
2. Utvärdera varje affärs risk genom att fråga en enkel fråga: "Finns affärs risken kvar i en moln modell?"
3. Om risken fortfarande finns skriver du om principen genom att dokumentera nödvändig minskning, inte den tekniska lösningen.
4. Granska den uppdaterade principen med moln implementerings teamen för att förstå möjliga lösningar på den nödvändiga lösningen.

## <a name="example-of-a-policy-review-for-a-legacy-policy"></a>Exempel på en princip granskning för en äldre princip

Om du vill ha ett exempel på processen ska vi använda säkerhets kopierings principen för band i föregående avsnitt:

- En företags princip bestämmer externa band säkerhets kopieringar för alla produktions system. I den här principen kan du se två data punkter av intresse:
  - Äldre beroende av en band säkerhets kopierings lösning
  - En förmodad affärs risk som är kopplad till lagringen av säkerhets kopior på samma fysiska plats som produktions utrustningen.
- Finns risken kvar? Ja. Även i molnet, skapar ett beroende på en enskild funktion en risk. Det finns en lägre sannolikhet för denna risk som påverkar verksamheten än vad som fanns i den lokala lösningen, men risken finns kvar.
- Omskrivningen av principen. I händelse av en data Centrals katastrof måste det finnas ett sätt att återställa produktions system inom 24 timmar från avbrottet i ett annat data Center och en annan geografisk plats.
- Granska med moln implementerings teamen. Beroende på vilken lösning som implementeras finns det flera sätt att följa den här resurs konsekvens principen.

## <a name="next-steps"></a>Nästa steg

Lär dig mer om att inkludera data klassificering i din strategi för moln styrning.

> [!div class="nextstepaction"]
> [Dataklassificering](./data-classification.md)
