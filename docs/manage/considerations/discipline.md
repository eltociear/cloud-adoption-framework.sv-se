---
title: Hanterings nivåer i moln hanterings ämnes områden
description: I den här artikeln beskrivs hanterings utjämning i moln hanterings ämnes områden.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: d6bd93d65c7db0972a6b2a0b55c8ee9bef1417f3
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807826"
---
# <a name="management-leveling-across-cloud-management-disciplines"></a>Hanterings nivåer i moln hanterings ämnes områden

Nycklarna till korrekt hantering i vilken miljö som helst är konsekvens och upprepnings bara processer. Det finns oändliga alternativ för de saker som kan göras i Azure. På samma sätt finns det oräkneliga metoder för moln hantering. För att tillhandahålla konsekvens och repeterbarhet är det viktigt att begränsa de alternativen till en konsekvent uppsättning hanterings processer och verktyg som kommer att erbjudas för arbets belastningar som finns i molnet.

## <a name="suggested-management-levels"></a>Föreslagna hanterings nivåer

Eftersom arbets belastningarna i din IT-portfölj varierar är det osannolikt att en enda hanterings nivå är tillräcklig för varje arbets belastning. För att hjälpa dig att stödja en mängd arbets belastningar och affärs åtaganden rekommenderar vi att du skapar ett antal nivåer av drift hantering i moln drifts teamet eller plattforms åtgärds teamet.

![Hantera hanterings nivåer och förfallo tid i moln införande ramverket](../../_images/manage/cloud-management-maturity.png)

Som start punkt bör du överväga att upprätta de hanterings nivåer som visas i föregående diagram och föreslås i följande lista:

- **Hanterings bas linje:** En moln hanterings bas linje (eller hanterings bas linje) är en definierad uppsättning verktyg, processer och konsekvent prissättning som fungerar som grund för all moln hantering i Azure. Om du vill upprätta en moln hanterings bas linje och bestämma vilka verktyg som ska ingå i bas linje erbjudandet för ditt företag, granskar du listan i avsnittet "Cloud Management-discipliner".
- **Förbättrad bas linje:** Ett antal arbets belastningar kan kräva förbättringar av bas linjen som inte nödvändigt vis är beroende av en enskild plattform eller arbets belastning. Även om dessa förbättringar inte är kostnads effektiva för varje arbets belastning, bör det finnas gemensamma processer, verktyg och lösningar för alla arbets belastningar som kan motivera kostnaden för det extra hanterings stödet.
- **Plattforms-specialisering:** I en viss miljö används vissa vanliga plattformar av olika arbets belastningar. Den här allmänna arkitekturen förändras inte när företag antar molnet. Platform specialisering är en förhöjd hanterings nivå som använder data och arkitektur av ämnes experter för att ge en högre drifts nivå. Exempel på plattforms-specialisering skulle omfatta hanterings funktioner som är speciella för SQL Server, behållare, Active Directory eller andra tjänster som kan hanteras bättre genom konsekventa, upprepnings bara processer, verktyg och arkitekturer.
- **Specialisering för arbets belastning:** För arbets belastningar som verkligen är verksamhets kritiska kan det vara en kostnads motivering att gå mycket djupare i hanteringen av arbets belastningen. Arbets belastnings specialisering använder telemetri för arbets belastning för att fastställa mer avancerade metoder för daglig hantering. Samma data identifierar ofta automatisering, distribution och design förbättringar som skulle leda till högre stabilitet, tillförlitlighet och återhämtning utöver vad som är möjligt med enbart drifts hantering.
- **Stöds inte:** Det är lika viktigt att kommunicera vanliga hanterings processer som inte levereras via moln hanterings ämnes områden för arbets belastningar som klassificeras som icke-kompatibla eller inte kritiska.

Organisationer kan också välja att [Hantera funktioner som är relaterade till en eller flera av dessa hanterings nivåer till en tjänst leverantör](https://www.microsoft.com/cloud-adoption-framework-offers?ot=manage). Dessa tjänst leverantörer kan använda [Azure-Lighthouse](https://azure.com/lighthouse) för att ge bättre precision och öppenhet.

De återstående artiklarna i serien visar ett antal processer som ofta finns i var och en av dessa ämnes områden.
I parallellt visar [Azures hanterings guide](../azure-management-guide/index.md) de verktyg som har stöd för var och en av dessa processer. Om du vill ha hjälp med att skapa en hanterings bas linje börjar du med Azures hanterings guide. När du har upprättat bas linjen kan den här artikel serien och de medföljande metod tipsen hjälpa till att utöka den bas linjen och definiera andra nivåer av hanterings stöd.

## <a name="cloud-management-disciplines"></a>Moln hanterings ämnes områden

Varje rekommenderad hanterings nivå kan anropas på flera olika moln hanterings områden. Mappningen är dock utformad för att göra det lättare att hitta de föreslagna processerna och verktygen för att leverera på lämplig nivå av moln hantering.

I de flesta fall består den tidigare diskuterade *nivån av hanterings bas linjer* för processer och verktyg från följande ämnes områden. I varje fall markeras några processer och verktyg för att demonstrera *förbättrade bas linje funktioner*.

- **Inventering och synlighet:** En hanterings bas linje bör minst innehålla ett sätt att inventera till gångar och skapa insyn i körnings tillstånd för varje till gång.
- **Operativa krav:** Regelbunden hantering av konfiguration, storlek, kostnad och prestanda för till gångar är nyckel för att underhålla prestanda förväntningar och en hanterings bas linje.
- **Skydda och återställa:** Att minimera drift avbrott och påskynda återställningen kan hjälpa dig att undvika prestanda förluster och inkomst påverkan. Identifiering och återställning är viktiga aspekter av denna disciplin inom någon hanterings bas linje.

Plattformens specialiserings nivå för hantering hämtas från processer och verktyg som är justerade med plattforms åtgärdernas disciplin. På samma sätt hämtar specialisering för arbets belastningen hantering från de processer och verktyg som är justerade med disciplinerna för arbets belastnings åtgärder.

## <a name="next-steps"></a>Nästa steg

Nästa steg för att definiera varje nivå av moln hantering är en förståelse för [inventering och synlighet](./inventory.md).

> [!div class="nextstepaction"]
> [Alternativ för inventering och synlighet](./inventory.md)
