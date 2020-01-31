---
title: Översikt över området identitetsbaslinje
description: Förklaring av identitetsbaslinje i förhållande till molnstyrning
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 1ac3041abc6e4721366f8270ce37d6bf6885b140
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806194"
---
# <a name="identity-baseline-discipline-overview"></a>Översikt över området identitetsbaslinje

Identitetsbaslinje är ett av de [fem områdena för molnstyrning](../governance-disciplines.md) i [Cloud Adoption Framework-styrningsmodellen](../index.md). Identitet anses alltmer vara den primära säkerhetsperimetern i molnet, vilket är en förändring jämfört med det traditionella fokuset på nätverkssäkerhet. Identitetstjänster tillhandahåller de centrala mekanismer som stöder åtkomstkontroll och organisering i IT-miljöer, och området identitetsbaslinje kompletterar [området säkerhetsbaslinje](../security-baseline/index.md) genom att konsekvent tillämpa autentiserings- och autentiseringskrav över olika projekt för molnimplementering.

> [!NOTE]
> Styrning av identitetsbaslinje ersätter inte de befintliga IT-team, processer och procedurer som gör att din organisation kan hantera och skydda identitetstjänster. Huvudsyftet med det här området är att identifiera potentiella identitetsrelaterade affärsrisker och ge vägledning om riskminimering till den IT-personal som ansvarar för implementering, underhåll och drift av din infrastruktur för identitetshantering. När du utvecklar styrningsprinciper och -processer bör du se till att relevanta IT-team deltar i processerna för planering och granskning.

I det här avsnittet av Cloud Adoption Framework beskrivs metoden för att utveckla ett identitetsbaslinjeområde som en del av din strategi för molnstyrning. Den primära målgruppen för den här vägledningen är din organisations molnarkitekter och andra medlemmar i teamet för molnstyrning. Dock bör de beslut, policyer och processer som härrör från det här området omfatta engagemang från och diskussioner med relevanta medlemmar i de IT-team som ansvarar för implementering och hantering av organisationens lösningar för identitetshantering.

Om din organisation saknar lokal kompetens inom identitetsbaslinje och säkerhet bör du överväga att anlita externa konsulter som en del av detta område. Överväg även att använda [Microsoft Consulting Services](https://www.microsoft.com/enterprise/services), molnimplementeringstjänsten [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) eller andra externa partner inom molnimplementering för att diskutera frågor kring det här området.

## <a name="policy-statements"></a>Principrapporter

Åtgärdsinriktade principrapporter och de resulterande arkitekturkraven utgör grunden för ett identitetsbaslinjeområde. Exempel med principframställning finns i artikeln om [principframställningar för identitetsbaslinje](./policy-statements.md). Dessa exempel kan fungera som en startpunkt för organisationens styrningsprinciper.

> [!CAUTION]
> Exempelprinciperna kommer från vanliga kundupplevelser. För att bättre kunna inrikta dessa principer med specifika molnstyrningsbehov genomför du följande steg och skapar principframställningar som uppfyller dina unika affärsbehov.

## <a name="develop-governance-policy-statements"></a>Utveckla principframställningar för styrning

Följande sex steg erbjuder exempel och potentiella alternativ att överväga när du utvecklar styrning av identitetsbaslinje. Använd varje steg som utgångspunkt för diskussioner inom teamet för molnstyrning och med berörda verksamheter samt IT-team i organisationen för att upprätta de principer och processer som behövs för att hantera risker relaterade till identitet.

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
                        <h3>Mall för identitetsbaslinje</h3>
                        <p class="x-hidden-focus">Ladda ned mallen för att dokumentera ett identitetsbaslinjeområde</p>
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
                        <p class="x-hidden-focus">Förstå skäl och risker som vanligtvis associeras med identitetsbaslinjeområdet.</p>
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
                        <p class="x-hidden-focus">Indikatorer för att förstå om det är rätt tid att investera i identitetsbaslinjeområdet.</p>
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
                        <p class="x-hidden-focus">Föreslagna processer för att stödja principefterlevnad i identitetsbaslinjeområdet.</p>
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
                        <p class="x-hidden-focus">Azure-tjänster som kan implementeras för att stödja identitetsbaslinjeområdet.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Nästa steg

Kom igång genom att utvärdera [affärsrisker](./business-risks.md) i en viss miljö.

> [!div class="nextstepaction"]
> [Förstå affärsrisker](./business-risks.md)
