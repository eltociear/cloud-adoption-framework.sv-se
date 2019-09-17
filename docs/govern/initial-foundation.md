---
title: Upprätta en grund för en första molnbaserad styrning
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Kom igång med moln styrning genom att etablera en första grundläggande Cloud styrnings grund.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 3e1f2c1b54a55a740376ba1d1c45c13dc9e7e26d
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028827"
---
# <a name="establish-an-initial-cloud-governance-foundation"></a>Upprätta en grund för en första molnbaserad styrning

Att upprätta moln styrning är en bred iterativ ansträngning. Det är svårt att träffa en effektiv balans mellan hastighet och kontroll, särskilt under tidiga faser av moln införande. Vägledningen för styrning i moln implementerings ramverket hjälper till att ge detta saldo via en smidig metod för att anta.

Den här artikeln innehåller två alternativ för att upprätta en första grund för styrning. Antingen säkerställer du att styrnings begränsningar kan skalas och expanderas när implementerings planen implementeras och kraven blir tydligare definierade. Som standard förutsätter den inledande grunden en isolerad och kontroll position. Det fokuserar också mer på resurs organisation än på resurs styrningen. Den här lätta start punkten kallas för en _minsta livskraftig produkt (MVP)_ för styrning. Målet med MVP: en minskar barriärer för att upprätta en inledande styrnings position och aktiverar snabbt lagring av lösningen för att lösa en mängd olika typer av konkreta risker.

## <a name="already-using-the-cloud-adoption-framework"></a>Använder redan moln införande ramverket

Om du har följt med ramverket för moln införande kanske du redan har distribuerat en styrnings MVP. Vägledning är en grundläggande aspekt av alla operativ modeller. Den finns under varje fas i moln implementeringens livs cykel. Därför ger moln implementerings [ramverket](../index.md) vägledning för att mata in styrning i aktiviteter relaterade till implementeringen av din [moln](../plan/index.md)implementerings plan. Ett exempel på den här styrnings integrationen är att använda skisser för att distribuera en eller flera landnings zoner som finns i den [färdiga](../ready/index.md) vägledningen. Ett annat exempel är vägledning för att [skala ut prenumerationer](../ready/considerations/scaling-subscriptions.md). Om du har följt någon av dessa rekommendationer är följande MVP-avsnitt helt enkelt en granskning av dina befintliga distributions beslut. När du har en snabb granskning kan du gå vidare till [den första styrnings lösningen och tillämpa bästa praxis kontroller](./foundation-improvements.md).

## <a name="establish-an-initial-governance-foundation"></a>Upprätta en grund för inledande styrning

Följande är två exempel på inledande styrnings stiftelser (kallas även för styrnings MVP: er) för att tillämpa en sund grund för styrning till nya eller befintliga distributioner. Välj den MVP som bäst överensstämmer med företagets behov för att komma igång:

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsZ">
<li style="display: flex; flex-direction: column;">
    <a href="./guides/standard/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Standardguide för styrning</h3>
                        <p>En guide för de flesta organisationer baserat på den rekommenderade modellen med två prenumerationer, som är utformat för distributioner i flera regioner men som inte omfattar offentliga och nationella/myndighetsbaserade moln.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./guides/complex/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Styrningsguide för komplexa företag</h3>
                        <p>En guide för företag som hanteras av flera oberoende IT-affärsenheter eller som omfattar offentliga och nationella/myndighetsbaserade moln.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>
<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Nästa steg

När en styrnings grund är på plats kan du tillämpa lämpliga rekommendationer för att förbättra lösningen och skydda mot konkreta risker.

> [!div class="nextstepaction"]
> [Förbättra den inledande styrnings stiftelsen](./foundation-improvements.md)
