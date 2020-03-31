---
title: Risk tolerans mått och indikatorer för distributions acceleration
description: Använd ramverket för moln införande för Azure för att kvantifiera affärs risk tolerans som är relaterad till distributions acceleration.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 14ae08de4bb0ce82e4ba0d5ce0225c0597ee67b4
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434531"
---
# <a name="deployment-acceleration-metrics-indicators-and-risk-tolerance"></a>Distributions accelerations mått, indikatorer och risk tolerans

I den här artikeln får du hjälp med att kvantifiera affärs risk toleransen när det gäller distributions acceleration. Genom att definiera mått och indikatorer kan du skapa ett affärs ärende för att göra en investering i förgrunden för distributions accelerationens disciplin.

## <a name="metrics"></a>Mått

Distributions accelerations disciplin fokuserar på risker relaterade till hur moln resurser konfigureras, distribueras, uppdateras och underhålls. Följande information är användbar när du inför den här disciplinen för moln styrning:

- **Distributions problem:** Procent andel distributioner som inte fungerar eller resulterar i felkonfigurerade resurser.
- **Tid för distribution:** Hur lång tid det tar att distribuera uppdateringar till ett befintligt system.
- **Överstämmande till gångar:** Antal eller procent av resurser som inte följer de definierade principerna.

## <a name="risk-tolerance-indicators"></a>Risk tolerans indikatorer

Risker som rör distributions acceleration är i stort sett relaterade till antal och komplexitet för molnbaserade system som distribueras för ditt företag. Allteftersom din moln egendom växer ökar antalet system som distribueras och frekvensen för uppdatering av moln resurser. Beroenden mellan resurser förstorar vikten av att säkerställa en korrekt konfiguration av resurser och att utforma system för återhämtning om en eller flera resurser upplever oväntad stillestånds tid.

<!-- "en-us" location is required for the URL below. -->

Traditionella företags IT-organisationer har ofta silon för drift-, säkerhets-och utvecklings grupper som ofta inte samarbetar eller som är till och med adversariala eller som är farliga mot varandra. Att identifiera de här utmaningarna tidigt och integrera viktiga intressenter från var och en av teamen kan hjälpa till att se över din moln användning samtidigt som den är skyddad och väl styrd. Därför bör man överväga att anta en DevOps-eller [DevSecOps](https://www.microsoft.com/en-us/securityengineering/devsecops) organisations kultur tidigt i molnets införande resa.

Arbeta med ditt DevSecOps-team och affärs intressenter för att identifiera [affärs risker](./business-risks.md) som är relaterade till konfigurationen och bestäm sedan en acceptabel bas linje för konfigurations risk tolerans. Det här avsnittet i vägledningen för moln implementerings ramverket innehåller exempel, men de detaljerade riskerna och bas linjerna för ditt företag eller distributioner är förmodligen annorlunda.

När du har en bas linje kan du fastställa de lägsta benchmark-värden som representerar en oacceptabel ökning av dina identifierade risker. Dessa riktmärken fungerar som utlösare för när du behöver vidta åtgärder för att åtgärda dessa risker. Nedan följer några exempel på hur konfigurations relaterade mått, till exempel de som beskrivs ovan, kan motivera en ökad investering i distributions accelerations disciplinen.

- **Konfigurations avvikelse utlösare:** Ett företag som har oväntade ändringar i konfigurationen av viktiga system komponenter, eller fel vid distribution av eller uppdateringar av sina system, bör investera i distributions accelerations disciplinen för att identifiera Rotors Aker och steg för reparation.
- **Utlösare som inte uppfyller kraven:** Om antalet lediga resurser överskrider en definierad tröskel (antingen som ett totalt antal resurser eller en procent andel av det totala antalet resurser), bör ett företag investera i förbättringar av distributions accelerations disciplin för att säkerställa att varje resurs konfiguration förblir i överensstämmelse med hela resursens livs cykel.
- **Projekt schema utlösare:** Om tiden för att distribuera ett företags resurser och program ofta överskrider ett definierat tröskelvärde, bör ett företag investera i sina distributions accelerations processer för att införa eller förbättra automatiserade distributioner för konsekvens och förutsägbarhet. Distributions tider som mäts i dagar eller till och med veckor indikerar vanligt vis en underoptimerad distributions accelerations strategi.

## <a name="next-steps"></a>Nästa steg

Använda [mallen för moln hantering](./template.md), dokument mått och tolerans indikatorer som överensstämmer med den aktuella moln implementerings planen.

Granska exempel på distributions accelerations principer som utgångs punkt för att utveckla principer som åtgärdar specifika affärs risker som överensstämmer med dina moln implementerings planer.

> [!div class="nextstepaction"]
> [Granska exempel principer](./policy-statements.md)
