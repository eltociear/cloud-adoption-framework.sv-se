---
title: Översikt över området resurskonsekvens
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Översikt över området resurskonsekvens
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: fa82b90981b5621ad3e82176c06bbb4506adfeed
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817374"
---
# <a name="resource-consistency-discipline-overview"></a>Översikt över området resurskonsekvens

Resurskonsekvens är ett av de [fem områdena för molnstyrning](../governance-disciplines.md) i [Cloud Adoption Framework-styrningsmodellen](../index.md). Det här området handlar om metoder för att upprätta principer som rör driftshantering av en miljö, ett program eller en arbetsbelastning. IT-driftsteam tillhandahåller ofta övervakning av prestanda för program, arbetsbelastningar och tillgångar. Dessutom genomför de ofta de uppgifter som krävs för att uppfylla skalningsbehov, åtgärda överträdelser gällande serviceavtal för prestanda samt proaktivt undvika överträdelser gällande serviceavtal för prestanda via automatiserade åtgärder. I de fem områdena för molnstyrning är resurskonsekvens ett område som säkerställer att resurser konfigureras konsekvent på ett sådant sätt att de kan identifieras av IT-åtgärder, omfattas i återställningslösningar och registreras till repeterbara åtgärdsprocesser.

> [!NOTE]
> Styrning av resurskonsekvens ersätter inte de befintliga IT-team, processer och procedurer som gör att din organisation effektivt kan hantera molnbaserade resurser. Huvudsyftet med det här området är att identifiera potentiella affärsrisker och ge vägledning om riskminimering till den IT-personal som ansvarar för hantering av dina resurser i molnet. När du utvecklar styrningsprinciper och -processer bör du se till att relevanta IT-team deltar i processerna för planering och granskning.

I det här avsnittet av Cloud Adoption Framework beskrivs hur du utvecklar ett resurskonsekvensområde som en del av din strategi för molnstyrning. Den primära målgruppen för den här vägledningen är din organisations molnarkitekter och andra medlemmar i teamet för molnstyrning. Dock bör de beslut, policyer och processer som härrör från det här området omfatta engagemang från och diskussioner med relevanta medlemmar i de IT-team som ansvarar för implementering och hantering av organisationens lösningar för resurskonsekvens.

Om din organisation saknar lokal kompetens inom strategier för resurskonsekvens bör du överväga att anlita externa konsulter som en del av detta område. Överväg även att använda [Microsoft Consulting Services](https://www.microsoft.com/enterprise/services), molnimplementeringstjänsten [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) eller andra externa experter på molnimplementering för att diskutera hur dina molnbaserade tillgångar kan organiseras, spåras och optimeras på bästa sätt.

## <a name="policy-statements"></a>Principrapporter

Åtgärdsinriktade principrapporter och de resulterande arkitekturkraven utgör grunden för ett resurskonsekvensområde. Exempel med principframställning finns i artikeln om [principframställningar för resurskonsekvens](./policy-statements.md). Dessa exempel kan fungera som en startpunkt för organisationens styrningsprinciper.

> [!CAUTION]
> Exempelprinciperna kommer från vanliga kundupplevelser. För att bättre kunna inrikta dessa principer med specifika molnstyrningsbehov genomför du följande steg och skapar principframställningar som uppfyller dina unika affärsbehov.

## <a name="developing-resource-consistency-governance-policy-statements"></a>Utveckla principframställningar för styrning av resurskonsekvens

Följande sex steg erbjuder exempel och potentiella alternativ att överväga när du utvecklar styrning av resurskonsekvens. Använd varje steg som utgångspunkt för diskussioner inom teamet för molnstyrning och med berörda verksamheter samt IT-team i organisationen för att upprätta de principer och processer som behövs för att hantera risker relaterade till identitet.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsE">
<li style="display: flex; flex-direction: column;">
    <a href="./template.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/governance/process-template.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Mall för resurskonsekvens</h3>
                        <p class="x-hidden-focus">Ladda ned mallen för att dokumentera ett resurskonsekvensområde</p>
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
                            <img src="../../_images/governance/process-risks.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Affärsrisker</h3>
                        <p class="x-hidden-focus">Förstå skäl och risker som vanligtvis associeras med resurskonsekvensområdet.</p>
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
                            <img src="../../_images/governance/process-metrics.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Indikatorer och mått</h3>
                        <p class="x-hidden-focus">Indikatorer för att förstå om det är rätt tid att investera i resurskonsekvensområdet.</p>
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
                            <img src="../../_images/governance/process-enforce.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Processer för principefterlevnad</h3>
                        <p class="x-hidden-focus">Föreslagna processer för att stödja principefterlevnad i resurskonsekvensområdet.</p>
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
                            <img src="../../_images/governance/process-maturity.png" class="x-hidden-focus"/>
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
                            <img src="../../_images/governance/process-toolchain.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Verktygskedja</h3>
                        <p class="x-hidden-focus">Azure-tjänster som kan implementeras för att stödja resurskonsekvensområdet.</p>
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
