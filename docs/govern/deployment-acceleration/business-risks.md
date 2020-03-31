---
title: Affärs risker för distributions acceleration
description: Använd ramverket för moln införande för Azure för att förstå affärs risker med distributions accelerations disciplin, som kan användas i styrnings strategin.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a4f022d995cf4dca25cfd5369ce92dd4496e8687
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434598"
---
# <a name="deployment-acceleration-motivations-and-business-risks"></a>Drift sättnings motivation och affärs risker

Den här artikeln beskriver orsakerna till att kunderna vanligt vis antar en distributions accelerations disciplin i en strategi för moln styrning. Det innehåller också några exempel på affärs risker som enhets princips instruktioner.

<!-- markdownlint-disable MD026 -->

## <a name="deployment-acceleration-relevancy"></a>Relevanta för distributions acceleration

Lokala system distribueras ofta med hjälp av bas linje avbildningar eller installations skript. Ytterligare konfiguration krävs vanligt vis, vilket kan omfatta flera steg eller mänskligt ingripande. Dessa manuella processer är fel känsliga och leder ofta till "konfigurations avvikelse", vilket kräver tids krävande fel söknings-och reparations åtgärder.

De flesta Azure-resurser kan distribueras och konfigureras manuellt via Azure Portal. Den här metoden kan vara tillräcklig för dina behov när det bara finns några få resurser att hantera. När din moln egendom växer, bör dock din organisation börja integrera automatisering i distributions processerna för att se till att dina moln resurser undviker konfigurations drift eller andra problem som kan uppstå vid manuella processer. Det bästa sättet att använda en DevOps-eller [DevSecOps](https://www.microsoft.com/en-us/securityengineering/devsecops) -metod är ofta det bästa sättet att hantera dina distributioner när du förväntar dig moln implementerings ansträngningar.

<!-- "en-us" location is required for the URL above. -->

En robust distributions accelerations plan säkerställer att dina moln resurser distribueras, uppdateras och konfigureras på rätt sätt och är på samma sätt. Förstoringen av distributions accelerations strategin kan också vara en viktig faktor i din [Cost Management strategi](../cost-management/index.md). Med automatiserad etablering och konfiguration av moln resurser kan du skala ned eller frigöra resurser när efter frågan är låg eller tidsbegränsad, så du betalar bara för resurser när du behöver dem.

## <a name="business-risk"></a>Affärs risk

Distributions accelerations disciplinen försöker lösa följande affärs risker. Under moln implementeringen övervakar du vart och ett av följande för relevans:

- **Avbrott i tjänsten:** Brist på förutsägbara upprepnings bara distributions processer eller ohanterade ändringar i systemkonfigurationer kan störa normala åtgärder och kan leda till förlorad produktivitet eller förlorad verksamhet.
- **Kostnads överskridningar:** Oväntade ändringar i konfigurationen av system resurser kan göra det svårare att identifiera rotor saken till problem, vilket höjer kostnaderna för utveckling, åtgärder och underhåll.
- **Organisations ineffektivitet:** Hinder mellan utvecklings-, drift-och säkerhets team kan orsaka flera utmaningar för att effektivt införa moln teknologier och utveckla en enhetlig miljö styrnings modell.

## <a name="next-steps"></a>Nästa steg

Använd [moln hanterings mal len](./template.md)för att dokumentera affärs risker som sannolikt kommer att introduceras av den aktuella moln implementerings planen.

När en förståelse av realistiska affärs risker har upprättats är nästa steg att dokumentera affärs toleransen för risker och indikatorer och viktiga mått för att övervaka den toleransen.

> [!div class="nextstepaction"]
> [Mått, indikatorer och risk tolerans](./metrics-tolerance.md)
