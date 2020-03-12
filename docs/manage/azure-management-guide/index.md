---
title: Översikt över Azure-hantering
description: Lär dig mer om Cloud Adoption Framework för Azure med den här informationen om de grundläggande verktyg som behövs för att hantera Azures produktionsmiljöer.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: b6d17a410c1903d984b5a1c756f51f7c5145ff9c
ms.sourcegitcommit: 388e32dd4861039149c846c926c0e9230cf28ae3
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/12/2020
ms.locfileid: "79140294"
---
::: zone target="docs"

# <a name="azure-management-guide-before-you-start"></a>Guide till Azure-hantering: Innan du börjar

> [!NOTE]
> Den här guiden är en utgångspunkt för vägledningen kring innovation i Cloud Adoption Framework. Du hittar den även i Azures snabbstartscenter. I tipset senare i artikeln finns en länk till Azures snabbstartscenter.

::: zone-end

::: zone target="chromeless"

# <a name="before-you-start"></a>Innan du börjar

::: zone-end

Azure-hanteringsguiden hjälper Azure-kunderna att skapa en baslinje för hanteringen, så att resurserna i Azure hanteras konsekvent. Den här guiden beskriver de grundläggande verktyg som behövs för en produktionsmiljö i Azure, särskilt om miljön innehåller känsliga data. Mer information, metodtips och överväganden när det gäller att förbereda din molnmiljö finns i avsnittet om [Cloud Adoption Framework-beredskap](../index.md).

## <a name="scope-of-this-guide"></a>Guidens omfång

I den här guiden får du lära dig att etablera verktyg till en baslinje för hanteringen. Den beskriver också hur du kan utöka baslinjen och bygga upp ytterligare stabilitet.

> [!div class="checklist"]
>
> - **Inventering och synlighet:** Skapa en förteckning över tillgångarna i flera moln. Utveckla insyn i körningen av respektive tillgång.
> - **Verksamhetsefterlevnad:** Upprätta kontroller och processer för att se till att alla tillstånd är korrekt konfigurerade och körs i en väl reglerad miljö.
> - **Skydda och återställa:** Se till att alla hanterade tillgångar är skyddade och kan återställas med hjälp av baslinjen för hanteringen.
> - **Alternativ för en utökad baslinje:** Utvärdera vanliga tillägg till baslinjen som kan uppfylla affärsbehoven.
> - **Plattformsdrift:** Utöka baslinjen för hantering med en väldefinierad tjänstkatalog och centralt hanterade plattformar.
> - **Arbetsbelastningsåtgärder:** Utöka baslinjen för hantering med fokus på verksamhetskritiska arbetsbelastningar.

## <a name="management-baseline"></a>Baslinje för hantering

En baslinje för hanteringen är den minsta uppsättning verktyg och processer som ska användas för alla tillgångar i miljön. Du kan ta med flera ytterligare alternativ i hanteringsbaslinjen. I de kommande artiklarna effektiviserar vi molnhanteringen genom att fokusera på den minsta uppsättning alternativ som krävs, i stället för alla tillgängliga alternativ.

::: zone target="docs"

> [!TIP]
> Visa den här guiden i Azure-portalen om du vill ha en interaktiv upplevelse. Gå till [Azures snabbstartcenter](https://portal.azure.com/?feature.quickstart=true#blade/Microsoft_Azure_Resources/QuickstartCenterBlade) i Azure-portalen och välj **Azures hanteringsguide**. Följ sedan instruktionerna.

Nästa steg är [Inventering och synlighet](./inventory.md).

::: zone-end

::: zone target="chromeless"

Den här guiden innehåller interaktiva steg där du kan prova funktionerna i takt med att de introduceras. Om du vill börja om där du slutade använder du navigeringslänken.

::: zone-end
