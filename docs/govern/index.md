---
title: Styrning i Microsoft Cloud Adoption Framework för Azure
description: Använd Cloud Adoption Framework för Azure för att lära dig att utvärdera befintliga principer, skapa en första styrningsgrund och lägga till styrningsverktyg iterativt.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/11/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 75b2269c4db348ab6a110309490187ef44b55f6c
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77706939"
---
# <a name="governance-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Styrning i Microsoft Cloud Adoption Framework för Azure

Molnet skapar nya paradigm för de tekniker som stöder verksamheten. Dessa nya paradigm ändrar även hur teknikerna implementeras, hanteras och styrs. När hela datacenter i princip kan raseras och byggas upp med en enda rad med kod som körs av en obevakad process, kan vi inte längre förlita oss på traditionella strategier. Detta gäller särskilt för styrning.

## <a name="get-started-with-cloud-governance"></a>Kom igång med molnstyrning

Molnstyrning är en iterativ process. För organisationer med befintliga principer som styr lokala IT-miljöer bör molnstyrning komplettera de här principerna. Hur nära företagsprinciperna är integrerade mellan lokala miljöer och molnet varierar beroende på mognaden hos molnstyrningen och den digitala egendomen i molnet. På samma sätt som molnegendomen förändras med tiden förändras även processerna och principerna för molnstyrningen. Följande övningar hjälper dig att skapa en inledande styrningsgrund.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsF">
    <li style="display: flex; flex-direction: column;">
        <a href="./methodology.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/1.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Metodik</h3>
Upprätta grundläggande förståelse för de metoder som används för molnstyrning i Cloud Adoption Framework för att börja tänka igenom lösningen för slutresultatet.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./benchmark.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/2.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Benchmark</h3>
Utvärdera nuvarande och framtida tillstånd så att du kan skapa en vision för hur ramverket ska tillämpas.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./initial-foundation.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/3.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Initial styrningsgrund</h3>
Inled din styrningserfarenhet med en liten lättimplementerad uppsättning styrningsverktyg. Den här inledande styrningsgrunden kallas för en MVP (minsta fungerande produkt).
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./foundation-improvements.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/4.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Förbättra den initiala styrningsgrunden</h3>
Under genomförandet av molnimplementeringsplanen kan du stegvis lägga till styrningskontroller som hanterar påtagliga risker när du närmar dig slutresultatet.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="objective-of-this-content"></a>Det här innehållets mål

Riktlinjerna i det här avsnittet om Cloud Adoption Framework har två syften:

- Ge exempel på praktiskt tillämpbara styrningsguider som representerar vanliga kundscenarier. Varje exempel beskriver affärsrisker, företagsprinciper för riskminimering och designriktlinjer för implementering av tekniska lösningar. Designvägledningen är av nödvändighet specifik för Azure. Allt annat innehåll i dessa guider kan tillämpas som en del av en molnoberoende metod eller en strategi för flera moln.
- Du får hjälp med att skapa egna styrningslösningar som kan uppfylla olika affärsbehov. De här behoven kan handla om styrning av flera offentliga moln genom detaljerad vägledning kring utvecklingen av företagets policyer, processer och verktyg.

Det här innehållet är avsett för molnstyrningsteamet. Det är även relevant för molnarkitekter som behöver förbättra sin kompetens inom molnstyrning.

## <a name="intended-audience"></a>Målgrupp

Innehållet i Cloud Adoption Framework berör verksamheten, tekniken och kulturen hos företag. Det här avsnittet av Cloud Adoption Framework är nära knutet till IT-säkerhet, IT-styrning, ekonomi, verksamhetschefer, nätverk, identiteter och teamen för molnimplementering. Eftersom de här personalgrupperna ofta är beroende av varandra måste molnarkitekterna använda en process med stor delaktighet. Den här delaktigheten kan vara en engångsföreteelse. I vissa fall är interaktionen med dessa personer kontinuerlig.

Molnarkitekten fungerar som strateg och ledare när de här personalgrupperna sammanförs. Innehållet i den här samlingen guider är utformat för att hjälpa molnarkitekten att leda diskussionen så att rätt beslut kan fattas. När det gäller affärsomvandlingar som drivs av molnet måste molnarkitekten ge beslutsstöd till både IT och verksamheten i stort.

**Molnarkitektsspecialisering i det här avsnittet:** Varje avsnitt av Cloud Adoption Framework representerar en viss specialisering eller variant av molnarkitektens roll. Det här avsnittet av Cloud Adoption Framework är utformat för molnarkitekter med intresse för att åtgärda eller minska tekniska risker. Vissa molnleverantörer kallar dessa specialister för *molnansvariga*, men vi föredrar *molnövervakare* eller *teamet för molnstyrning* som ett samlingsnamn. I varje praktiskt tillämpbar styrningsguide beskriver artiklarna hur sammansättningen av och syftet med teamet för molnstyrning kan förändras med tiden.

## <a name="use-this-guide"></a>Använd den här guiden

Om du vill följa guiden från början till slut så får du hjälp att utveckla en robust strategi för molnstyrning parallellt med molnimplementeringen. Vägledningen guidar dig genom teori och implementering av en sådan strategi.

För en snabbkurs om teorin och snabb åtkomst till Azure-implementering kan du börja med [översikten över styrningsguider](./guides/index.md). Med den här vägledningen kan du börja i liten skala och stegvis förbättra styrningsbehoven parallellt med molnimplementeringen.

## <a name="next-steps"></a>Nästa steg

Upprätta grundläggande förståelse för de metoder som används för molnstyrning i Cloud Adoption Framework.

> [!div class="nextstepaction"]
> [Förstå metodiken](./methodology.md)
