---
title: Beslutsguide för prenumerationer
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig om molnplattformsprenumerationer som en central tjänst i Azure-migreringar.
author: alexbuckgit
ms.author: abuck
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: a6ee53355313a0f0c277d7b1c69e77494cdf8e1c
ms.sourcegitcommit: e0a783dac15bc4c41a2f4ae48e1e89bc2dc272b0
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73058726"
---
# <a name="subscription-decision-guide"></a>Beslutsguide för prenumerationer

En effektiv prenumerationsdesign hjälper organisationer att upprätta en struktur för organisera resurser i Azure under en molnanpassning.

Varje resurs i Azure, t.ex. en virtuell dator eller en databas, är kopplad till en prenumeration. Du börjar använda Azure när du skapar en Azure-prenumeration, kopplar den till ett konto och distribuerar resurser till prenumerationen. En översikt av de här koncepten finns i [Grundläggande Azure-begrepp](../../ready/considerations/fundamental-concepts.md).

När din digitala egendom i Azure växer, så behöver du förmodligen skapa ytterligare prenumerationer för att uppfylla dina krav. Med Azure kan du definiera en hierarki av hanteringsgrupper för att organisera dina prenumerationer och enkelt tillämpa rätt princip till rätt resurser. Mer information finns i [Skalning med flera Azure-prenumerationer](../../ready/considerations/scaling-subscriptions.md).

Vissa grundläggande exempel på hur du kan använda hanteringsgrupper för att separera olika arbetsbelastningar:

- **Arbetsbelastningar för produktion kontra icke-produktion:** Vissa företag skapar hanteringsgrupper för att separera sina produktions- och icke-produktionsprenumerationer. Med hanteringsgrupper blir det enklare för dessa kunder att hantera roller och principer. Till exempel kan en icke-produktionsprenumeration ge utvecklare **deltagaråtkomst**, men i produktion har de bara **läsaråtkomst**.
- **Interna tjänster kontra externa tjänster:** Liksom med produktions- respektive icke-produktionsarbetsbelastningar har företag ofta olika krav, principer och roller för interna tjänster jämfört med externa, kundriktade tjänster.

Den här beslutsguiden hjälper dig att överväga olika sätt att ordna din hanteringsgruppshierarki på.

## <a name="subscription-design-patterns"></a>Mönster för prenumerationsdesign

Eftersom alla organisationer är olika, så är Azure-hanteringsgrupperna utformade för att vara flexibla. Modellera ditt molninnehåll så att det återspeglar organisationens hierarki och hjälper dig att definiera och tillämpa principer på högre nivåer i hierarkin, och förlita dig på arv när det gäller att se till att dessa principer tillämpas automatiskt på hanteringsgrupper lägre ned i hierarkin. Även om prenumerationer kan flyttas mellan olika hanteringsgrupper, är det bra att designa en grupphierarki för en initial hanteringsgruppshierarki som återspeglar dina förväntade organisationsbehov.

Innan du slutför din prenumerationsdesign kan du även överväga hur överväganden om [resurskonsekvens](../resource-consistency/index.md) kan påverka dina designval.

> [!NOTE]
> Med Azure Enterprise-avtal (EA) kan du definiera en annan organisationshierarki i faktureringssyfte. Den här hierarkin skiljer sig från din hanteringsgruppshierarki, vilken fokuserar på att tillhandahålla en arvsmodell för att underlätta tillämpning av lämpliga principer och åtkomstkontroller på dina resurser.

Följande prenumerationsalternativ avspeglar en initial förbättring av prenumerationsdesignen, följt av flera mer avancerade hierarkier som kan anpassas till din organisation:

### <a name="single-subscription"></a>Enstaka prenumeration

En enstaka prenumeration per konto räcker kanske för organisationer som behöver distribuera ett litet antal molnhanterade tillgångar. Detta är det första prenumerationsmönster du implementerar i början av molnimplementeringaprocessen för att möjliggöra småskaliga experimentella eller koncepttestbaserade distributioner som hjälper dig att utforska molnets funktioner.

### <a name="production-and-nonproduction-pattern"></a>Mönster för produktion och icke-produktion

När du är redo att distribuera en arbetsbelastning till en produktionsmiljö bör du lägga till ytterligare en prenumeration. Detta hjälper dig att hålla dina produktionsdata och andra tillgångar utanför dina utvecklings- och testningsmiljöer. Du kan också enkelt använda två olika principuppsättningar för resurser i två prenumerationer.

![Mönster för produktions- och icke-produktionsprenumeration](../../_images/ready/basic-subscription-model.png)

### <a name="workload-separation-pattern"></a>Mönster för arbetsbelastningsuppdelning

När en organisation lägger till nya arbetsbelastningar i molnet kan olika ägarskap till prenumerationer eller grundläggande ansvarsseparation resultera i flera prenumerationer i hanteringsgrupper för såväl produktion som icke-produktion. Även om den här metoden ger grundläggande arbetsbelastningsseparation, så drar den inga större fördelar av arvsmodellen för att automatiskt tillämpa principer på en delmängd av dina prenumerationer.

![Mönster för arbetsbelastningsuppdelning](../../_images/ready/management-group-hierarchy.png)

### <a name="application-category-pattern"></a>Mönster för programkategori

I takt med att en organisations molnfotavtryck växer så skapas normalt ytterligare prenumerationer för att stödja program som har fundamentala skillnader vad gäller affärskritiskhet, efterlevnadskrav, åtkomstkontroller och dataskyddsbehov. Utifrån prenumerationsmönster för produktion och icke-produktion ordnas de prenumerationer som stöder dessa programkategorier under tillämpliga hanteringsgrupper för produktion eller icke-produktion. De här prenumerationerna ägs och hanteras vanligtvis av central IT-personalstyrka.

![Mönster för programkategori](../../_images/infra-subscriptions/application.png)

Varje organisation kategoriserar sina program på olika sätt och separerar ofta prenumerationer baserat på specifika program eller tjänster eller utefter programarketyper. Den här kategoriseringen är ofta utformad för att stödja arbetsbelastningar som förväntas förbruka de flesta av resursgränserna för en prenumeration, eller för att separera verksamhetskritiska arbetsbelastningar så att de inte konkurrerar med andra arbetsbelastningar under dessa begränsningar. Några arbetsbelastningar som kan motivera en separat prenumeration under det här mönstret är:

- Verksamhetskritiska arbetsbelastningar.
- Program som är en del av ”kostnader för sålda varor” (KSV) i företaget. Exempel: Varje instans av företagets X-widget innehåller en Azure IoT-modul som skickar telemetri. Detta kan kräva en dedikerad prenumeration för redovisnings-/styrningsändamål som en del av KSV.
- Program som omfattas av regelkrav, till exempel HIPAA eller FedRAMP.

### <a name="functional-pattern"></a>Funktionsmönster

Det funktionella mönstret organiserar prenumerationer och konton längs funktionella rader, t.ex. ekonomi, försäljning eller IT-support, med hjälp av en hanteringsgruppshierarki.

### <a name="business-unit-pattern"></a>Affärsenhetsmönster

Affärsenhetsmönstret grupperar prenumerationer och konton baserat på vinst- och förlustkategori, affärsenhet, division, resultatenheter eller liknande affärsstruktur med hjälp av en hanteringsgrupphierarki.

### <a name="geographic-pattern"></a>Geografiskt mönster

För organisationer med global verksamhet grupperar det geografiska mönstret prenumerationer och konton baserat på geografiska regioner med hjälp av en hanteringsgruppshierarki.

## <a name="mixed-patterns"></a>Blandade mönster

Hanteringsgruppshierarkier kan ha ett djup på upp till sex nivåer. Detta ger dig flexibiliteten att skapa en hierarki som kombinerar flera av dessa mönster för att uppfylla organisationens behov. Diagrammet nedan visar exempelvis en organisationshierarki som kombinerar ett affärsenhetsmönster med en geografisk mönster.

![Mönster för blandad prenumeration](../../_images/infra-subscriptions/mixed.png)

## <a name="related-resources"></a>Relaterade resurser

- [Åtkomsthantering av resurser i Azure](../../govern/resource-consistency/resource-access-management.md)
- [Flera styrningsnivåer i stora företag](../../govern/guides/complex/multiple-layers-of-governance.md)
- [Flera geografiska områden](../regions/index.md)

## <a name="next-steps"></a>Nästa steg

Prenumerationsdesign är bara en av huvudkomponenterna för infrastruktur som kräver arkitektoniska beslut under en process för att implementera moln. Gå till [översikten över beslutsguider](../index.md) om vill veta mer om alternativa mönster eller modeller som används vid utformningsbeslut för andra typer av infrastrukturer.

> [!div class="nextstepaction"]
> [Beslutsguider för arkitektur](../index.md)
