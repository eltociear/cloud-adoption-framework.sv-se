---
title: Översikt över området distributionsacceleration
description: Använd Cloud Adoption Framework för Azure för att förstå distributionsacceleration i relation till molnstyrning.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 3c83e40ab6d08b461095385ac58cf64d74da86a9
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77708979"
---
# <a name="deployment-acceleration-discipline-overview"></a>Översikt över området distributionsacceleration

Distributionsacceleration är ett av de [fem områdena för molnstyrning](../governance-disciplines.md) i [Cloud Adoption Framework-styrningsmodellen](../index.md). Det här området handlar om metoder för att upprätta principer för styrning av tillgångskonfiguration eller -distribution. I de fem områdena för molnstyrning omfattar distributionsacceleration distribution, konfigurationsinriktning och återanvändbarhet för skript. Detta kan ske via manuella aktiviteter eller helt automatiserade DevOps-aktiviteter. I båda fallen är principerna i stort sett desamma. I takt med att det här området mognar kan teamet för molnstyrning agera partner i DevOps- och utvecklingsstrategier genom att accelerera distributioner och ta bort hinder för molnimplementering via tillämpningen av återanvändbara tillgångar.

Den här artikeln beskriver processen för den distributionsacceleration som ett företag erfar under faserna för planering, byggande, implementering och drift av en molnlösning. Det går inte att täcka alla krav för ett företag i ett enda dokument. Därför beskriver varje avsnitt i den här artikeln föreslagna minsta och potentiella aktiviteter. Målet med dessa aktiviteter är att hjälpa dig skapa en [princip-MVP](../policy-compliance/index.md#minimum-viable-product-mvp-for-policy), men även att upprätta ett ramverk för [inkrementella principförbättringar](../policy-compliance/index.md#incremental-policy-growth). Molnstyrningsteamet bör besluta hur mycket som ska investeras i dessa aktiviteter i syfte att förbättra distributionsaccelerationen.

> [!NOTE]
> Området distributionsacceleration ersätter inte befintliga IT-team, processer och procedurer som gör att din organisation effektivt kan distribuera och konfigurera molnbaserade resurser. Huvudsyftet med det här området är att identifiera potentiella affärsrisker och ge vägledning om riskminimering till den IT-personal som ansvarar för hantering av dina resurser i molnet. När du utvecklar styrningsprinciper och -processer bör du se till att relevanta IT-team deltar i processerna för planering och granskning.

Den primära målgruppen för den här vägledningen är din organisations molnarkitekter och andra medlemmar i teamet för molnstyrning. Dock bör de beslut, policyer och processer som härrör från det här området omfatta engagemang från och diskussioner med relevanta medlemmar i dina affärs- och IT-team, särskilt de ledare som ansvarar för distribution och konfiguration av molnbaserade arbetsbelastningar.

## <a name="policy-statements"></a>Principrapporter

Åtgärdsinriktade principrapporter och de resulterande arkitekturkraven utgör grunden för ett distributionsaccelerationsområde. Exempel med principframställning finns i artikeln om [principframställningar för distributionsacceleration](./policy-statements.md). Dessa exempel kan fungera som en startpunkt för organisationens styrningsprinciper.

> [!CAUTION]
> Exempelprinciperna kommer från vanliga kundupplevelser. För att bättre kunna inrikta dessa principer med specifika molnstyrningsbehov genomför du följande steg och skapar principframställningar som uppfyller dina unika affärsbehov.

## <a name="develop-governance-policy-statements"></a>Utveckla principframställningar för styrning

Följande sex steg hjälper dig att definiera styrningsprinciper för att kontrollera distribution och konfiguration av resurser i din molnmiljö.

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
                        <h3>Mall för distributionsacceleration</h3>
                        <p class="x-hidden-focus">Ladda ned mallen för att dokumentera ett distributionsaccelerationsområde</p>
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
                        <p class="x-hidden-focus">Förstå skäl och risker som vanligtvis associeras med distributionsaccelerationsområdet.</p>
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
                        <p class="x-hidden-focus">Indikatorer för att förstå om det är rätt tid att investera i distributionsaccelerationsområdet.</p>
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
                        <p class="x-hidden-focus">Föreslagna processer för att stödja principefterlevnad i distributionsaccelerationsområdet.</p>
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
                        <p class="x-hidden-focus">Azure-tjänster som kan implementeras för att stödja distributionsaccelerationsområdet.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

## <a name="next-steps"></a>Nästa steg

Kom igång genom att utvärdera [affärsrisker](./business-risks.md) i en viss miljö.

> [!div class="nextstepaction"]
> [Förstå affärsrisker](./business-risks.md)

<!-- markdownlint-enable MD033 -->
