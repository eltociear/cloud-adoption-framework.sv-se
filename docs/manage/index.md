---
title: Molnhantering
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Molnhantering i Cloud Adoption Framework
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: operate
layout: LandingPage
ms.openlocfilehash: 1e54fdc30e0db1ed1cecf01156bb9c25368a8457
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565023"
---
# <a name="cloud-management-in-the-cloud-adoption-framework"></a>Molnhantering i Cloud Adoption Framework

För att en [molnstrategi](../strategy/index.md) ska lyckas krävs det en gedigen planering, beredskap och implementering. Det är dock den kontinuerliga driften av de digitala tillgångarna som ger mätbara affärsresultat. Utan en plan för en tillförlitlig och välhanterad drift av molnlösningarna kommer du inte få ut mycket av dina ansträngningar. I följande övningar får du hjälp att utveckla de verksamhetsmässiga och tekniska metoder som krävs vid en molnhantering av den kontinuerliga driften.

## <a name="getting-started"></a>Komma igång

Om du vill förbereda dig för den här fasen av molnimplementeringens livscykel rekommenderar ramverket följande övningar:

<!-- markdownlint-disable MD033 -->
<ul class="panelContent cardsF">
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-management-guide/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/1.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Upprätta en baslinje för hanteringen</h3>
Definiera de kritiska klassificeringar, molnhanteringsverktyg och processer som krävs för att du ska kunna leverera grundåtagandet till drifthanteringen.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./considerations/business-alignment.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/2.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Definiera verksamhetsåtaganden</h3>
Dokumentera vilka arbetsbelastningar som stöds och upprätta driftsåtaganden för verksamheten och kom överens om vilka investeringar i molnhanteringen som ska göras för respektive arbetsbelastning.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./best-practices.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/3.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Utöka baslinjen för hantering</h3>
Utgå från besluten kring verksamhetsåtaganden och driften och använd metodtipsen till att implementera de verktyg som behövs för molnhanteringen.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./design-principles.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/4.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Avancerade principer för drift och design</h3>
För plattformar och arbetsbelastningar som behöver större verksamhetsåtaganden kan du behöva granska arkitekturen närmare för att förbättra stabiliteten och tillförlitligheten.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>
<!-- markdownlint-enable MD033 -->

## <a name="scalable-cloud-management-methodology"></a>Metod för skalbar molnhantering

Föregående steg är ett praktiskt genomförbart sätt att använda hanteringsmetoden i Cloud Adoption Framework.

![Hanteringsmetoden i Cloud Adoption Framework](../_images/manage/caf-manage.png)

## <a name="create-a-balanced-cloud-portfolio"></a>Skapa en balanserad molnportfölj

Precis som det står i artikeln om [anpassning av verksamheten](./considerations/business-alignment.md) så är inte alla arbetsbelastningar verksamhetskritiska. Alla portföljer innehåller olika viktiga arbetsbelastningar. Verksamhetsanpassningen handlar om att fånga upp den här faktorn och att anpassa hanteringskostnaderna efter verksamheten, så att bästa möjliga processer och verktyg används i driftshanteringen.

## <a name="objective-of-this-content"></a>Det här innehållets mål

Riktlinjerna i det här avsnittet om Cloud Adoption Framework har två syften:

- Ge exempel på praktiskt tillämpbara metoder för driftshantering som motsvarar vanliga kundscenarier.
- Hjälpa dig att skapa anpassade hanteringslösningar baserade på dina verksamhetsåtaganden.

Det här innehållet är avsett för teamet som ansvarar för molndriften. Det är även relevant för molnarkitekter som behöver förbättra sin kompetens inom molndrift och molndesign.

## <a name="intended-audience"></a>Målgrupp

Innehållet i Cloud Adoption Framework berör verksamheten, tekniken och kulturen hos företag. Det här avsnittet av Cloud Adoption Framework är nära knutet till IT-drift, IT-styrning, ekonomi, verksamhetschefer, nätverk, identiteter och teamen för molnimplementering. Eftersom de här personalgrupperna ofta är beroende av varandra, måste molnarkitekterna använda en process med stor delaktighet. Den här delaktigheten är sällan en engångsföreteelse.

Molnarkitekten fungerar som strateg och ledare när de här personalgrupperna sammanförs. Innehållet i den här samlingen guider är utformat för att hjälpa molnarkitekten att leda diskussionen så att rätt beslut kan fattas. När det gäller affärsomvandlingar som drivs av molnet måste molnarkitekten ge beslutsstöd till både IT och verksamheten i stort.

**Molnarkitektsspecialisering i det här avsnittet:** Varje avsnitt av Cloud Adoption Framework representerar en viss specialisering eller variant av molnarkitektens roll. Det här avsnittet av Cloud Adoption Framework är utformat för molnarkitekter med intresse för drift och hantering av distribuerade lösningar. I det här sammanhanget kallas dessa specialister ofta för *molndriften*, eller kollektivt som *molndriftteamet*.

## <a name="use-this-guide"></a>Använd den här guiden

Om du vill följa guiden från början till slut så får du hjälp att utveckla en robust strategi för molndriften. Vägledningen guidar dig genom teori och implementering av en sådan strategi.

<!-- For a crash course on the theory and quick access to Azure implementation, get started with the [governance guides overview](./guide/index.md). Using this guidance, you can start small and iteratively improve your governance needs in parallel with cloud adoption efforts. -->

## <a name="next-steps"></a>Nästa steg

Använd metoden till att upprätta tydliga verksamhetsåtaganden.

> [!div class="nextstepaction"]
> [Upprätta tydliga verksamhetsåtaganden](./considerations/business-alignment.md)
