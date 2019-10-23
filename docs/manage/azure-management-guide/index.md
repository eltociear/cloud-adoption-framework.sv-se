---
title: 'Guide till Azure-hantering: Innan du börjar'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig hur du hanterar dina Azure-åtgärder med stegvis vägledning.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 58a01e02abad2de68fac9a94d2a2aa3ad22d32a1
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769151"
---
::: zone target="docs"

# <a name="azure-management-guide-before-you-start"></a>Guide till Azure-hantering: Innan du börjar

> [!NOTE]
> Den här guiden är en utgångspunkt för vägledningen kring innovation i Cloud Adoption Framework. Du hittar den även i Azures Snabbstartscenter. I tipset senare i artikeln finns en länk till Azures snabbstartscenter.

::: zone-end

::: zone target="chromeless"

# <a name="before-you-start"></a>Innan du börjar

::: zone-end

Azure-hanteringsguiden är utformad för att hjälpa aktiva Azure-kunder att skapa en grund till hanteringen så att resurserna i Azure hanteras konsekvent. Den här guiden beskriver de grundläggande verktyg du behöver för en produktionsmiljö i Azure, särskilt om miljön innehåller känsliga data. Mer information, metodtips och överväganden när det gäller att förbereda din molnmiljö finns i avsnittet om [Cloud Adoption Framework-beredskap](../index.md).

## <a name="scope-of-this-guide"></a>Guidens omfång

I den här guiden får du lära dig att etablera verktyg för en baslinje för hanteringen. Den beskriver också hur du kan utöka baslinjen och bygga upp ytterligare stabilitet.

> [!div class="checklist"]
>
> - **Inventering och synlighet:** Skapa en förteckning över tillgångarna i flera moln. Utveckla insyn i körningen av respektive tillgång.
> - **Verksamhetsefterlevnad:** Upprätta kontroller och processer för att se till att alla tillstånd är korrekt konfigurerade och körs i en väl reglerad miljö.
> - **Skydda och återställa:** Se till att alla hanterade tillgångar är skyddade och kan återställas med hjälp av baslinjen för hanteringen.
> - **Alternativ för en utökad baslinje:** Utvärdera vanliga tillägg till baslinjen som kan uppfylla olika affärsbehov.
> - **Plattformsdrift:** Utöka baslinjen för hantering med en väldefinierad katalog tjänster och centralt hanterade plattformar.
> - **Arbetsbelastningsåtgärder:** Utöka baslinjen för hantering så att den omfattar en inriktning på verksamhetskritiska arbetsbelastningar.

## <a name="management-baseline"></a>Baslinje för hantering

En baslinje för hanteringen är den minsta uppsättning verktyg och processer som ska användas för alla tillgångar i miljön. Du kan ta med flera ytterligare alternativ i hanteringsbaslinjen. I de kommande artiklarna effektiviserar vi molnhanteringen genom att fokusera på den minsta uppsättning alternativ som krävs snarare än alla tillgängliga alternativ.

::: zone target="docs"

> [!TIP]
> Visa den här guiden i Azure-portalen om du vill ha en interaktiv upplevelse. Gå till [Azures snabbstartcenter](https://portal.azure.com/?feature.quickstart=true#blade/Microsoft_Azure_Resources/QuickstartCenterBlade) i Azure-portalen och välj **Guide till Azure-hantering**. Följ sedan instruktionerna.

Nästa steg: [Inventering och synlighet](./inventory.md)

::: zone-end

::: zone target="chromeless"

Den här guiden innehåller interaktiva steg där du kan prova funktionerna i takt med att de introduceras. Om du vill börja om där du slutade använder du navigeringslänken.

::: zone-end
