---
title: De fem teorierna om molnstyrning
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig mer om de fem disciplinerna i moln styrning i ramverket för moln införande.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: e162dd4aad284d7de430a2483ccda04b99e21dd3
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030372"
---
# <a name="the-five-disciplines-of-cloud-governance"></a>De fem teorierna om molnstyrning

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsI">
    <li style="display: flex; flex-direction: column;">
        <div class="cardSize">
            <div class="cardPadding" style="padding-bottom:10px;">
                <div class="card" style="padding-bottom:10px;">
                    <div class="cardText" style="padding-left:0px;">
Alla ändringar av affärs processer eller teknik plattformar introducerar risker. Team styrnings grupper, vars medlemmar ibland kallas för moln förmyndare komponenter, har en aktivitet som minimerar dessa risker och säkerställer minimalt avbrott i syfte att vidta eller Innovations insatser.<br/><br/>Organisations modellen för moln införande ramverk styr dessa beslut (oberoende av vald moln plattform) genom att fokusera på <a href="./corporate-policy.md">utvecklingen av företags policyn</a> och de <a href="#disciplines-of-cloud-governance">fem disciplinerna i moln styrning</a>. <a href="./guides/index.md">Redigerings bara design guider</a> demonstrerar den här modellen med hjälp av Azure-tjänster. Lär dig mer om de olika ämnes områden som styr modellen för moln införande ramverk nedan.
                    </div>
                </div>
            </div>
        </div>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="../_images/operational-transformation-govern-highres.png" style="display: flex; flex-direction: column; flex: 1 0 auto;">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardText" style="padding-left:0px;">
    <img src="../_images/operational-transformation-govern-highres.png" alt="Diagram of the Cloud Adoption Framework governance model: Corporate policy and governance disciplines">
    <br>
    <i>Figur 1 – diagram över företags policy och de fem disciplinerna i moln styrning.</i>
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="disciplines-of-cloud-governance"></a>Ämnes områden för moln styrning

Med valfri moln plattform finns det gemensamma styrnings discipliner som hjälper till att informera principer och justera verktygs kedjor. Dessa ämnes områden hjälper dig att fatta beslut om rätt nivå på automatisering och verk ställande av företagets policy i moln plattformarna.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsA">
<li style="display: flex; flex-direction: column;">
    <a href="./cost-management/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/cost-management.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Cost Management</h3>
                        <p>Kostnaden är ett primärt problem för moln användare. Utveckla principer för kostnads kontroll för alla moln plattformar.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./security-baseline/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/security-baseline.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Grundläggande säkerhet</h3>
                        <p>Säkerhet är ett komplext ämne som är unikt för varje företag. När säkerhets kraven har upprättats tillämpar moln styrnings principer och tvång dessa krav i nätverk, data och till gångs konfigurationer.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./identity-baseline/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/identity-baseline.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Grundläggande identitet</h3>
                        <p>Inkonsekvenser i tillämpningen av identitets krav kan öka risken för intrång. Identitets bas disciplin fokuserar på att se till att identiteten appliceras konsekvent i moln implementerings ansträngningar.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./resource-consistency/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/resource-consistency.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Resurskonsekvens</h3>
                        <p>Moln åtgärder beror på konsekvent resurs konfiguration. Genom styrnings verktyget kan resurser konfigureras konsekvent för att hantera risker relaterade till onboarding, drift, identifiering och återställning.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./deployment-acceleration/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/deployment-acceleration.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Distributionsacceleration</h3>
                        <p>Centralisering, standardisering och konsekvens i metoder för distribution och konfiguration förbättrar styrnings metoderna. När de tillhandahålls via molnbaserad styrnings verktyg skapar de en moln faktor som kan påskynda distributions aktiviteter.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->
