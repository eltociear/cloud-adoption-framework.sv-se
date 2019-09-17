---
title: Förstå effekten av globala marknads beslut
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Förklaring av begreppet globala marknader
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: ca1e18bdc8da300667b721e673bb1fc0388b4bdf
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030406"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-will-global-market-decisions-affect-the-transformation-journey"></a>Hur påverkar globala marknads beslut omvandlings resan?

Molnet öppnar nya möjligheter att utföra en global skala. Hinder för globala åtgärder minskar avsevärt genom att ge företagen möjlighet att distribuera till gångar på marknaden, utan att behöva investera kraftigt i nya data Center. Detta ger dig också en fantastisk komplexitet från tekniska och juridiska perspektiv.

## <a name="data-sovereignty"></a>Data suveränitet

Många politiska regioner har upprättat data suveränitets bestämmelser. Dessa regler begränsar var data kan lagras, vilka data som kan lämna ursprungslandet och vilka data som kan samlas in om medborgare i regionen. Innan du använder en molnbaserad lösning i en utländsk geografi bör du förstå hur moln leverantören hanterar data suveränitet. Mer information om Azures metod för varje geografi finns [här](https://azure.microsoft.com/global-infrastructure/geographies). Mer information om kompatibilitet i Azure finns i [sekretess på Microsoft](https://www.microsoft.com/trustcenter/privacy) i Microsoft säkerhets Center.

I resten av den här artikeln förutsätter sig att juridisk rådgivning har granskat och godkänt åtgärder i ett främmande land.

## <a name="business-units"></a>Affär senheter

Det är viktigt att förstå vilka affär senheter som körs i utländska länder och vilka länder som påverkas. Den här informationen används för att utforma lösningar för värd-, fakturerings-och distributions funktioner till moln leverantören.

## <a name="employee-usage-patterns"></a>Användnings mönster för medarbetare

Det är viktigt att förstå hur globala användare kommer åt program som inte finns i samma land som användaren. Tid för globala WAN-nätverk (Wide Area Network) är ofta väg användare baserade på befintliga nätverks avtal. I en traditionell lokal värld, begränsar vissa begränsningar WAN-design. Dessa begränsningar kan leda till dåliga användar upplevelser om de inte är korrekt tolkade innan du börjar använda molnet.

I en moln modell öppnar Internet även flera nya alternativ. Att kommunicera spridningen av anställda över flera geografiska områden kan hjälpa molnet att utforma WAN-lösningar som skapar positiva användar upplevelser **och** potentiellt minskade nätverks kostnader.

## <a name="external-user-usage-patterns"></a>Användnings mönster för externa användare

Det är lika viktigt att förstå användnings mönstren för externa användare, t. ex. kunder eller partner. I likhet med användnings mönster för anställda kan externa användar mönster påverka prestanda för moln distributioner negativt. När en stor eller verksamhets kritisk användar bas finns i ett främmande land, kan det vara klokt att inkludera en global distributions strategi i den övergripande lösnings designen.

## <a name="next-steps"></a>Nästa steg

När globala marknads beslut har fattats och meddelats är teamet redo att börja [upprätta tekniska standarder](../digital-estate/index.md) mot dessa mått.
Resultatet blir en omvandling efter [släpning eller](..//migrate/migration-considerations/prerequisites/technical-complexity.md)efter släpning för migrering.

> [!div class="nextstepaction"]
> [Utvärdera den digitala fastigheten](../digital-estate/index.md)
