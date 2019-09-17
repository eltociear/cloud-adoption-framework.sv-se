---
title: 'Styrnings guide för komplexa företag: Styrning i flera lager'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Styrnings guide för komplexa företag: Styrning i flera lager'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a0a2674a91b963154d757eb35290b8aeead5c503
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028240"
---
# <a name="governance-guide-for-complex-enterprises-multiple-layers-of-governance"></a>Styrnings guide för komplexa företag: Styrning i flera lager

När stora företag behöver flera olika styrnings nivåer finns det större komplexitets nivåer som måste delas in i styrnings MVP och senare styrnings förbättringar.

Några vanliga exempel på sådana komplexa är:

- Distribuerade styrnings funktioner.
- Företagets IT-avdelning har stöd för affär senhets IT-organisationer.
- Företaget stöder geografiskt distribuerade IT-organisationer.

I den här artikeln lär du dig några sätt att navigera i den här typen av komplexitet.

## <a name="large-enterprise-governance-is-a-team-sport"></a>Stor företags styrning är en grupp sport

Stora etablerade företag har ofta team eller anställda som fokuserar på de ämnes områden som nämns i den här hand boken. Den här guiden visar en metod för att göra styrningen till en team sport.

I många stora företag kan de fem disciplinerna i moln styrning vara Blocker att fatta. Det tar tid att utveckla moln kunskaper om identitet, säkerhet, åtgärder, distributioner och konfiguration i ett företag. Holistiskt implementera IT-styrnings policyn och IT-säkerheten kan sakta av innovationen i månader eller till och med år. Ta en utjämnad verksamhet och de styrnings behov som krävs för att skydda befintliga resurser är Delicate.

De inbyggda funktionerna i molnet kan ta bort Blocker till innovation men ökar riskerna. I den här styrnings guiden visade vi hur exemplet företaget skapade guardrails för att hantera riskerna. I stället för att ta itu med var och en av de ämnes områden som krävs för att skydda miljön, leder moln styrnings gruppen till en riskfylld metod för att styra vad som kan distribueras, medan de andra teamen bygger de nödvändiga moln tiderna. Det viktigaste är att när varje team når molnets förfallo sätt använder styrning sina lösningar holistiskt. Allt eftersom varje team är vuxen och lägger till den övergripande lösningen kan moln styrnings teamet öppna fasor Gates, vilket ger ytterligare innovation och införande på blomstra.

Den här modellen illustrerar tillväxten för ett partnerskap mellan moln styrnings teamet och befintliga företags team (säkerhet, IT-styrning, nätverk, identitet och annat). Guiden börjar med styrnings MVP och växer till ett holistiskt slut tillstånd genom styrnings iterationer.

## <a name="requirements-to-supporting-such-a-team-sport"></a>Krav för att stödja en sådan team sport

Det första kravet för en Multilayer styrnings modell är att förstå styrnings hierarkin. Genom att besvara följande frågor får du hjälp att förstå den allmänna styrnings hierarkin:

- Hur allokeras moln redovisning (fakturering för moln tjänster) mellan affär senheter?
- Hur tilldelas styrnings ansvar för företag och varje affär senhet?
- Vilka typer av miljöer hanterar var och en av dessa enheter?

## <a name="central-governance-of-a-distributed-governance-hierarchy"></a>Central styrning av en distribuerad styrnings hierarki

Verktyg som hanterings grupper gör det möjligt för företag att skapa en hierarkisk struktur som matchar styrnings hierarkin. Verktyg som Azure-ritningar kan använda till gångar till olika lager i den hierarkin. Azure-ritningar kan vara versioner och olika versioner kan tillämpas på hanterings grupper, prenumerationer eller resurs grupper. Var och en av dessa koncept beskrivs i detalj i styrnings MVP.

Den viktiga aspekten av vart och ett av dessa verktyg är möjligheten att tillämpa flera skisser på en hierarki. Detta gör det möjligt för styrning att vara en lager process. Följande är ett exempel på den här hierarkiska program styrningen:

- **Företags IT:** Företags IT skapar en uppsättning standarder och principer som gäller för all moln införande. Detta är materialiserat i en "bas linje"-skiss. Företaget äger sedan hanterings gruppens hierarki, vilket säkerställer att en version av bas linjen tillämpas på alla prenumerationer i hierarkin.
- **Regional eller affär senhet:** Olika IT-team kan använda ett extra lager av styrning genom att skapa sin egen skiss. Dessa ritningar skulle skapa additiva principer och standarder. När företaget har utvecklats kan de använda dessa ritningar för att utföra de aktuella noderna inom hanterings gruppens hierarki.
- **Moln implementerings team:** Detaljerade beslut och implementeringar om program eller arbets belastningar kan göras av varje moln antagande team inom ramen för styrnings krav. Ibland kan teamet även begära ytterligare Azure-resursens konsekvens för att påskynda implementeringen.

Informationen om styrnings implementering på varje nivå kräver samordning mellan varje team. Förbättringarna i styrnings MVP och styrning som beskrivs i den här hand boken kan hjälpa dig att justera samordningen.

