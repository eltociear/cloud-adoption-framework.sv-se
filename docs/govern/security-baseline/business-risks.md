---
title: Säkerhets bas linje affärs risker
description: Förstå och se exempel på typisk kund införande av en säkerhets bas linje disciplin i en moln styrnings strategi.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3bef524646e6be5ca6cd0b638b9614af389972f9
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77709030"
---
# <a name="security-baseline-motivations-and-business-risks"></a>Motiveringar och affärs risker för säkerhets bas linjer

I den här artikeln beskrivs orsakerna till att kunderna vanligt vis antar en säkerhets bas linjes disciplin i en strategi för moln styrning. Det innehåller också några exempel på potentiella affärs risker som kan användas för att köra princip satser.

<!-- markdownlint-disable MD026 -->

## <a name="security-baseline-relevancy"></a>Säkerhets bas linje relevanta

Säkerhet är ett viktigt problem för alla IT-organisationer. Moln distributioner är mycket av samma säkerhets risker som arbets belastningar som finns i traditionella lokala data Center. De offentliga moln plattformarna, som saknar direkt ägande rätt för den fysiska maskin varan som lagrar och kör dina arbets belastningar, innebär dock att moln säkerhet kräver en egen princip och sina processer.

Ett av de viktigaste sakerna som anger att säkerhets styrning i molnet skiljer sig från den traditionella säkerhets policyn är en över gång till vilka resurser som kan skapas, vilket kan leda till sårbarheter om säkerheten inte anses före distributionen. Flexibiliteten som teknik som t. ex. [SDN (Software Defined Networking)](../../decision-guides/software-defined-network/index.md) ger dig möjlighet att snabbt ändra din molnbaserade nätverkstopologi kan också enkelt ändra den övergripande nätverks attack ytan på oförutsebara sätt. Cloud Platforms tillhandahåller också verktyg och funktioner som kan förbättra dina säkerhetsfunktioner på sätt som inte alltid är möjliga i lokala miljöer.

Det belopp som du investerar i säkerhets policyn och processerna är beroende av moln distributionens natur. Inledande test distributioner kanske bara behöver de mest grundläggande säkerhets principerna på plats, medan en verksamhets kritisk arbets belastning kommer att innebära komplexa och omfattande säkerhets behov. Alla distributioner måste kommunicera med disciplinen på vissa nivåer.

Säkerhets bas linje disciplinen täcker företagets principer och manuella processer som du kan vidta för att skydda din moln distribution mot säkerhets risker.

> [!NOTE]
>Även om det är viktigt att förstå [identitets bas](../identity-baseline/index.md) linjen i kontexten för säkerhets bas linjen och hur det är relaterat till Access Control, kan de [fem disciplinerna i moln styrningen](../index.md) ringa ut [identitets bas linjen](../identity-baseline/index.md) som en egen disciplin, separat från säkerhets bas linjen.

## <a name="business-risk"></a>Affärs risk

Säkerhets bas linje disciplinen försöker hantera kärn säkerhets relaterade affärs risker. Arbeta med din verksamhet för att identifiera dessa risker och övervaka var och en av dem efter relevans när du planerar för och implementerar dina moln distributioner.

Riskerna varierar mellan olika organisationer, men följande fungerar som vanliga säkerhetsrelaterade risker som du kan använda som utgångs punkt för diskussioner i din moln styrnings grupp:

- **Data intrång:** Oavsiktlig exponering eller förlust av känsliga molnbaserade data kan leda till förlust av kunder, avtals ärenden eller rättsliga följder.
- **Avbrott i tjänsten:** Avbrott och andra prestanda problem på grund av osäker infrastruktur avbryter normal drift och kan leda till förlorad produktivitet eller förlorad verksamhet.

## <a name="next-steps"></a>Nästa steg

Använd [moln hanterings mal len](./template.md)för att dokumentera affärs risker som sannolikt kommer att introduceras av den aktuella moln implementerings planen.

När en förståelse av realistiska affärs risker har upprättats är nästa steg att dokumentera affärs toleransen för risker och indikatorer och viktiga mått för att övervaka den toleransen.

> [!div class="nextstepaction"]
> [Förstå indikatorer, mått och risk tolerans](./metrics-tolerance.md)
