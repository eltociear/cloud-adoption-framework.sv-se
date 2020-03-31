---
title: Beslutsguide för prenumerationer
description: Organisera dina Azure-resurser med effektiva strategier för prenumerationsdesign och en hierarki för hanteringsgrupper.
author: alexbuckgit
ms.author: abuck
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 2f50efb6e73f59affa8c2b463d363644a026b32c
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80431167"
---
# <a name="subscription-decision-guide"></a>Beslutsguide för prenumerationer

En effektiv prenumerationsdesign hjälper organisationer att på ett strukturerat sätt organisera och hantera resurser i Azure under övergången till molnet. Den här guiden hjälper dig att avgöra när du behöver skapa ytterligare prenumerationer och expandera hierarkin för hanteringsgrupper för att uppfylla dina affärsbehov.

## <a name="prerequisites"></a>Krav

När du implementerar Azure börjar du med att skapa en Azure-prenumeration, associera den med ett konto och distribuera resurser såsom virtuella datorer och databaser till prenumerationen. En översikt av de här koncepten finns i [Grundläggande Azure-begrepp](../../ready/considerations/fundamental-concepts.md).

- [Skapa dina första prenumerationer.](../../ready/azure-best-practices/initial-subscriptions.md)
- [Skapa ytterligare prenumerationer](../../ready/azure-best-practices/scale-subscriptions.md) för att skala din Azure-miljö.
- [Organisera och hantera dina prenumerationer](../../ready/azure-best-practices/organize-subscriptions.md) med hjälp av Azure-hanteringsgrupper.

## <a name="modeling-your-organization"></a>Modellera din organisation

Eftersom alla organisationer är olika, så är Azure-hanteringsgrupperna utformade för att vara flexibla. Modellera ditt molninnehåll så att det återspeglar organisationens hierarki och hjälper dig att definiera och tillämpa principer på högre nivåer i hierarkin, och förlita dig på arv när det gäller att se till att dessa principer tillämpas automatiskt på hanteringsgrupper lägre ned i hierarkin. Även om prenumerationer kan flyttas mellan olika hanteringsgrupper, är det bra att designa en grupphierarki för en initial hanteringsgruppshierarki som återspeglar dina förväntade organisationsbehov.

Innan du slutför din prenumerationsdesign kan du även överväga hur överväganden om [resurskonsekvens](../resource-consistency/index.md) kan påverka dina designval.

> [!NOTE]
> Med Azure Enterprise-avtal (EA) kan du definiera en annan organisationshierarki i faktureringssyfte. Den här hierarkin skiljer sig från din hanteringsgruppshierarki, vilken fokuserar på att tillhandahålla en arvsmodell för att underlätta tillämpning av lämpliga principer och åtkomstkontroller på dina resurser.

## <a name="subscription-design-strategies"></a>Strategier för prenumerationsdesign

Överväg att använda följande strategier för prenumerationsdesign för att uppfylla dina affärsbehov.

### <a name="workload-separation-strategy"></a>Strategi för separata arbetsbelastningar

När en organisation lägger till nya arbetsbelastningar i molnet kan olika ägarskap till prenumerationer eller grundläggande ansvarsseparation resultera i flera prenumerationer i hanteringsgrupper för såväl produktion som icke-produktion. Även om den här metoden ger grundläggande arbetsbelastningsseparation, så drar den inga större fördelar av arvsmodellen för att automatiskt tillämpa principer på en delmängd av dina prenumerationer.

![Strategi för separata arbetsbelastningar](../../_images/ready/management-group-hierarchy-v2.png)

### <a name="application-category-strategy"></a>Strategi för programkategorier

I takt med att en organisations molnfotavtryck växer så skapas normalt ytterligare prenumerationer för att stödja program som har fundamentala skillnader vad gäller affärskritiskhet, efterlevnadskrav, åtkomstkontroller och dataskyddsbehov. Utifrån de ursprungliga prenumerationerna för produktion och icke-produktion ordnas de prenumerationer som stöder dessa programkategorier under tillämpliga hanteringsgrupper för produktion eller icke-produktion. De här prenumerationerna ägs och hanteras vanligtvis av central IT-personalstyrka.

![Strategi för programkategorier](../../_images/infra-subscriptions/application.png)

Varje organisation kategoriserar sina program på olika sätt och separerar ofta prenumerationer baserat på specifika program eller tjänster eller utefter programarketyper. Den här kategoriseringen är ofta utformad för att stödja arbetsbelastningar som förväntas förbruka de flesta av resursgränserna för en prenumeration, eller för att separera verksamhetskritiska arbetsbelastningar så att de inte konkurrerar med andra arbetsbelastningar under dessa begränsningar. Exempel på arbetsbelastningar som kan motivera en separat prenumeration:

- Verksamhetskritiska arbetsbelastningar.
- Program som är en del av ”kostnader för sålda varor” (KSV) i företaget. Exempel: Varje instans av företagets X-widget innehåller en Azure IoT-modul som skickar telemetri. Detta kan kräva en dedikerad prenumeration för redovisnings-/styrningsändamål som en del av KSV.
- Program som omfattas av regelkrav, till exempel HIPAA eller FedRAMP.

### <a name="functional-strategy"></a>Funktionell strategi

I en funktionell strategi organiseras prenumerationer och konton längs en funktionell linje, t.ex. för ekonomi, försäljning eller IT-support, med hjälp av en hanteringsgruppshierarki.

### <a name="business-unit-strategy"></a>Affärsenhetsstrategi

I en affärsenhetsstrategi grupperas prenumerationer och konton baserat på vinst- och förlustkategori, affärsenhet, division, resultatenheter eller liknande affärsstrukturer med hjälp av en hanteringsgruppshierarki.

### <a name="geographic-strategy"></a>Geografisk strategi

Organisationer med global verksamhet kan använda en geografisk strategi som grupperar prenumerationer och konton utifrån geografiska regioner med hjälp av en hanteringsgruppshierarki.

## <a name="mixing-subscription-strategies"></a>Blanda prenumerationsstrategier

Hanteringsgruppshierarkier kan ha ett djup på upp till sex nivåer. Detta ger dig flexibiliteten att skapa en hierarki som kombinerar flera av dessa strategier för att uppfylla organisationens behov. Diagrammet nedan visar exempelvis en organisationshierarki som kombinerar en affärsenhetsstrategi med en geografisk strategi.

![Blandad prenumerationsstrategi](../../_images/infra-subscriptions/mixed.png)

## <a name="related-resources"></a>Relaterade resurser

- [Åtkomsthantering av resurser i Azure](../../govern/resource-consistency/resource-access-management.md)
- [Flera styrningsnivåer i stora företag](../../govern/guides/complex/multiple-layers-of-governance.md)
- [Flera geografiska områden](../../migrate/azure-best-practices/multiple-regions.md)

## <a name="next-steps"></a>Nästa steg

Prenumerationsdesign är bara en av huvudkomponenterna för infrastruktur som kräver arkitektoniska beslut under en process för att implementera moln. Gå till [översikten över beslutsguider](../index.md) och lär dig mer om ytterligare strategier som används för att fatta designbeslut för andra typer av infrastrukturer.

> [!div class="nextstepaction"]
> [Beslutsguider för arkitektur](../index.md)
