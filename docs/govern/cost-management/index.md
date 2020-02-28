---
title: Översikt över området kostnadshantering
description: Förstå metoden för att utveckla ett kostnadshanteringsområde som en del av en strategi för molnstyrning.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: ebb0f0899ad8ea4e5f26c43b0486c56560b4dd14
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77708877"
---
# <a name="cost-management-discipline-overview"></a>Översikt över området kostnadshantering

Kostnadshantering är ett av de [fem områdena för molnstyrning](../governance-disciplines.md) i [Cloud Adoption Framework-styrningsmodellen](../index.md). För många kunder är kostnaden för styrning ett stort problem vid implementering av molntekniker. Det kan vara en utmaning att balansera prestandakrav, implementeringshastighet och kostnader för molntjänster. Detta är särskilt relevant under större företagsomvandlingar som implementerar molntekniker. I det här avsnittet beskrivs metoden för att utveckla ett kostnadshanteringsområde som en del av en strategi för molnstyrning.

> [!NOTE]
> Styrning av kostnadshantering ersätter inte de befintliga affärsteam, redovisningsavdelningar och procedurer som är kopplade till din organisations ekonomihantering av IT-relaterade kostnader. Det huvudsakliga syftet med det här området är att identifiera potentiella molnrelaterade risker som rör IT-utgifter och ge vägledning om riskbegränsning till verksamheten och de IT-team som ansvarar för att distribuera och hantera molnresurser.

Den primära målgruppen för den här vägledningen är din organisations molnarkitekter och andra medlemmar i teamet för molnstyrning. Dock bör de beslut, policyer och processer som härrör från det här området omfatta engagemang från och diskussioner med relevanta medlemmar i dina affärs- och IT-team, särskilt de ledare som ansvarar för ägarskap, hantering och betalning för molnbaserade arbetsbelastningar.

## <a name="policy-statements"></a>Principrapporter

Åtgärdsinriktade principrapporter och de resulterande arkitekturkraven utgör grunden för ett kostnadshanteringsområde. Exempel med principframställning finns i artikeln om [principframställningar för kostnadshantering](./policy-statements.md). Dessa exempel kan fungera som en startpunkt för organisationens styrningsprinciper.

> [!CAUTION]
> Exempelprinciperna kommer från vanliga kundupplevelser. För att bättre kunna inrikta dessa principer med specifika molnstyrningsbehov genomför du följande steg och skapar principframställningar som uppfyller dina unika affärsbehov.

## <a name="develop-governance-policy-statements"></a>Utveckla principframställningar för styrning

Följande sex steg hjälper dig att definiera styrningsprinciper för att kontrollera kostnader i din miljö.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsE">
<li style="display: flex; flex-direction: column;">
    <a href="./template.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-template.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Mall för kostnadshantering</h3>
                        <p class="x-hidden-focus">Ladda ned mallen för att dokumentera ett kostnadshanteringsområde</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li><li style="display: flex; flex-direction: column;">
    <a href="./business-risks.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-risks.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Affärsrisker</h3>
                        <p class="x-hidden-focus">Förstå skäl och risker som vanligtvis associeras med kostnadshanteringsområdet.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./metrics-tolerance.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-metrics.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Indikatorer och mått</h3>
                        <p class="x-hidden-focus">Indikatorer för att förstå om det är rätt tid att investera i kostnadshanteringsområdet.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./compliance-processes.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-enforce.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Processer för principefterlevnad</h3>
                        <p class="x-hidden-focus">Föreslagna processer för att stödja principefterlevnad i kostnadshanteringsområdet.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./discipline-improvement.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-maturity.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Mognad</h3>
                        <p class="x-hidden-focus">Justera molnhanteringsmognad med faser för molnimplementering.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./toolchain.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-toolchain.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Verktygskedja</h3>
                        <p class="x-hidden-focus">Azure-tjänster som kan implementeras för att stödja kostnadshanteringsområdet.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

## <a name="next-steps"></a>Nästa steg

Kom igång genom att utvärdera affärsrisker i en viss miljö.

> [!div class="nextstepaction"]
> [Förstå affärsrisker](./business-risks.md)

<!-- markdownlint-enable MD033 -->
