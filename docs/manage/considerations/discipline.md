---
title: Hanterings nivåer i moln hanterings ämnes områden
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Hanterings nivåer i moln hanterings ämnes områden
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 0517816bd01221da8f5b4d97cc40dd39f4599b5e
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557575"
---
# <a name="management-leveling-across-cloud-management-disciplines"></a>Hanterings nivåer i moln hanterings ämnes områden

Nyckeln till korrekt hantering i vilken miljö som helst är konsekvens och upprepnings bara processer. Det finns oändliga alternativ för de saker som kan göras i Azure. På samma sätt finns det oräkneliga metoder för moln hantering. För att tillhandahålla konsekvens och repeterbarhet är det viktigt att begränsa de alternativen till en konsekvent uppsättning hanterings processer och verktyg som kommer att erbjudas för arbets belastningar som finns i molnet.

## <a name="suggested-management-levels"></a>Föreslagna hanterings nivåer

Eftersom arbets belastningarna i din IT-portfölj inte är samma, är det osannolikt att en enda hanterings nivå är tillräcklig för varje arbets belastning. För att stödja olika arbets belastningar och olika affärs åtaganden rekommenderar vi att moln drifts teamet eller plattforms åtgärds teamet upprättar några nivåer av drift hantering.

![Hantera hanterings nivåer och förfallo tid i moln införande ramverket](../../_images/manage/cloud-management-maturity.png)

Följande hanterings nivåer (som också visas ovan) är några föreslagna nivåer som ska fungera som en utgångs punkt:

- **Hanterings bas linje**: en moln hanterings bas linje (eller hanterings bas linje) är den definierade uppsättningen verktyg, processer och konsekvent prissättning som fungerar som grund för all moln hantering i Azure. Om du vill upprätta en bas linje för moln hantering granskar du tabellen i följande avsnitt och avgör vilka verktyg som ska ingå i bas linje erbjudandet för ditt företag.
- **Förbättrad bas linje**: ett antal arbets belastningar kan kräva förbättringar av bas linjen som inte nödvändigt vis är beroende av en enda plattform eller arbets belastning. Dessa förbättringar är inte kostnads effektiva för varje arbets belastning, men det bör finnas gemensamma processer, verktyg och lösningar för arbets belastningar som kan vara till hjälp för att motivera den extra hanterings supporten.
- **Plattforms-specialisering**: i en specifik miljö finns det vanliga plattformar som används av flera olika arbets belastningar. Den här allmänna arkitekturen förändras inte när företag antar molnet. Platform specialisering är en förhöjd hanterings nivå som utnyttjar data och arkitektoniska ämnes expert kunskaper för att tillhandahålla en högre drift hanterings nivå. Exempel på plattforms-specialisering skulle omfatta hanterings funktioner som är speciella för SQL Server, behållare, Active Directory eller andra tjänster som kan hanteras bättre genom konsekventa, upprepnings bara processer, verktyg och arkitekturer.
- **Specialisering av arbets belastning**: för de arbets belastningar som verkligen är verksamhets kritiska kan det vara en kostnads motivering att gå mycket djupare i hanteringen av arbets belastningen. Arbets belastnings specialisering utnyttjar arbets belastnings telemetri för att fastställa fler avancerade metoder för daglig hantering. Samma data identifierar ofta automatisering, distribution och design förbättringar som skulle leda till högre stabilitet, tillförlitlighet och återhämtning utöver vad som är möjligt med enbart drifts hantering.
- **Stöds**inte: det är lika viktigt att kommunicera vanliga hanterings processer som inte levereras via moln hanterings ämnes områden för arbets belastningar som klassificeras som icke-kompatibla eller inte kritiska.

I de återstående artiklarna i serien finns ett antal processer som ofta finns i var och en av dessa ämnes områden.
I parallellt visar [Azures hanterings guide](../azure-management-guide/index.md) de verktyg som har stöd för var och en av dessa processer. Om du vill ha hjälp med att skapa en hanterings bas linje börjar du med Azures hanterings guide. När bas linjen har upprättats kan den här artikel serien och de medföljande metod tipsen hjälpa till att utöka den bas linjen och definiera andra nivåer av hanterings stöd.

## <a name="cloud-management-disciplines"></a>Moln hanterings ämnes områden

Var och en av de föreslagna hanterings nivåerna kan anropa olika ämnes områden för moln hantering. Mappningen är dock utformad för att göra det lättare att hitta de föreslagna processerna och verktygen för att leverera på lämplig nivå av moln hantering.

I de flesta fall består den "hanterings bas linje nivå" som beskrivs ovan av processer och verktyg från följande ämnes områden. I varje fall markeras några processer och verktyg för att demonstrera "förbättrade bas linje funktioner".

- **Inventering och synlighet**: minst en hanterings bas linje bör innehålla ett sätt att inventera till gångar och skapa insyn i körnings tillstånd för varje till gång.
- **Operativa krav:** Regelbunden hantering av konfiguration, storlek, kostnad och prestanda för till gångar är nyckel för att underhålla prestanda förväntningar och en hanterings bas linje.
- **Skydda och återställa:** Minimera drift avbrott och påskynda återställningen av varje hjälp för att undvika prestanda förluster och inkomst påverkan. Identifiering och återställning är viktiga aspekter av denna disciplin inom någon hanterings bas linje.

Plattformens specialiserings nivå för hantering hämtas från processer och verktyg som är justerade med plattforms åtgärdernas disciplin.
På samma sätt hämtar specialisering för arbets belastningen hantering från de processer och verktyg som är justerade mot disciplinerna för arbets belastnings åtgärder.
  
## <a name="next-steps"></a>Nästa steg

Nästa steg för att definiera varje nivå av moln hantering är en förståelse för [inventering och synlighet](./inventory.md).

> [!div class="nextstepaction"]
> [Alternativ för inventering och synlighet](./inventory.md)
