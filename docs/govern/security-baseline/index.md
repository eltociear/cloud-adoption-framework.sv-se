---
title: Översikt över området säkerhetsbaslinje
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Översikt över området säkerhetsbaslinje
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: a0b0ed642e11fc3ffc81db7fd1095853a5458b1d
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565948"
---
# <a name="security-baseline-discipline-overview"></a>Översikt över området säkerhetsbaslinje

Säkerhetsbaslinje är ett av de [fem områdena för molnstyrning](../governance-disciplines.md) i [Cloud Adoption Framework-styrningsmodellen](../index.md). Säkerhet ingår i alla IT-distributioner, och molnet medför unika säkerhetsutmaningar. Många företag omfattas av regelkrav som gör skydd av känsliga data till en stor organisationsprioritering vid övervägandet av en molnomvandling. Identifiering av potentiella säkerhetshot mot molnmiljön och etablering av processer och procedurer för att åtgärda dessa hot bör prioriteras av IT-säkerhetsteam eller cybersäkerhetsteam. Området säkerhetsbaslinje säkerställer att tekniska krav och säkerhetsbegränsningar tillämpas konsekvent på molnbaserade miljöer allt eftersom dessa krav mognar.

> [!NOTE]
> Styrning av säkerhetsbaslinje ersätter inte de befintliga IT-team, processer och procedurer som din organisation använder för att skydda molndistribuerade resurser. Huvudsyftet med det här området är att identifiera säkerhetsrelaterade affärsrisker och ge vägledning om riskminimering till den IT-personal som ansvarar för säkerhetsinfrastrukturen. När du utvecklar styrningsprinciper och -processer bör du se till att relevanta IT-team deltar i processerna för planering och granskning.

I den här artikeln beskrivs metoden för att utveckla ett säkerhetsbaslinjeområde som en del av din strategi för molnstyrning. Den primära målgruppen för den här vägledningen är din organisations molnarkitekter och andra medlemmar i teamet för molnstyrning. Dock bör de beslut, policyer och processer som härrör från det här området omfatta engagemang från och diskussioner med relevanta medlemmar i dina IT- och säkerhetsteam, särskilt de tekniska ledare som ansvarar för implementering av tjänster för nätverk, kryptering och identitet.

Att fatta rätt säkerhetsbeslut är mycket viktigt för lyckade molndistributioner och företagets framgång överlag. Om din organisation saknar lokal kompetens inom cybersäkerhet bör du överväga att anlita externa säkerhetskonsulter som en del av detta område. Överväg även att använda [Microsoft Consulting Services](https://www.microsoft.com/enterprise/services), molnimplementeringstjänsten [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) eller andra externa experter på molnimplementering för att diskutera frågor kring det här området.

## <a name="policy-statements"></a>Principrapporter

Åtgärdsinriktade principrapporter och de resulterande arkitekturkraven utgör grunden för ett säkerhetsbaslinjeområde. Exempel med principframställning finns i artikeln om [principframställningar för säkerhetsbaslinjeområde](./policy-statements.md). Dessa exempel kan fungera som en startpunkt för organisationens styrningsprinciper.

> [!CAUTION]
> Exempelprinciperna kommer från vanliga kundupplevelser. För att bättre kunna inrikta dessa principer med specifika molnstyrningsbehov genomför du följande steg och skapar principframställningar som uppfyller dina unika affärsbehov.

## <a name="develop-governance-policy-statements"></a>Utveckla principframställningar för styrning

Följande sex steg erbjuder exempel och potentiella alternativ att överväga när du utvecklar styrning av säkerhetsbaslinje. Använd varje steg som utgångspunkt för diskussioner inom molnstyrningsteamet och med berörda verksamheter samt IT- och säkerhetsteam i organisationen för att upprätta de principer och processer som behövs för att hantera risker relaterade till säkerhet.

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
                        <h3>Mall för säkerhetsbaslinje</h3>
                        <p class="x-hidden-focus">Ladda ned mallen för att dokumentera ett säkerhetsbaslinjeområde</p>
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
                        <p class="x-hidden-focus">Förstå skäl och risker som vanligtvis associeras med säkerhetsbaslinjeområdet.</p>
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
                        <p class="x-hidden-focus">Indikatorer för att förstå om det är rätt tid att investera i säkerhetsbaslinjeområdet.</p>
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
                        <p class="x-hidden-focus">Föreslagna processer för att stödja principefterlevnad i säkerhetsbaslinjeområdet.</p>
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
                        <p class="x-hidden-focus">Azure-tjänster som kan implementeras för att stödja säkerhetsbaslinjeområdet.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Nästa steg

Kom igång genom att utvärdera affärsrisker i en viss miljö.

> [!div class="nextstepaction"]
> [Förstå affärsrisker](./business-risks.md)
