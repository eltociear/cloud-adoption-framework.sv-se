---
title: Aktivering av moln införande lyckades
description: Använd det kostnads fria, självbetjänings molnets implementerings ramverk och andra verktyg som hjälper dig att fatta beslut om moln införande som gör det möjligt för kunden att lyckas.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: overview
layout: LandingPage
ms.openlocfilehash: 2a6eab51a6254a5f7a2a7cf811b0a3857fd4d852
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80357251"
---
# <a name="enable-success-during-a-cloud-adoption-journey"></a>Aktivera lyckad under en moln införande resa

Ramverket för moln införande är ett kostnads fritt självbetjänings verktyg som vägleder läsarna genom olika moln införande åtgärder. Ramverket hjälper kunder att realisera affärs mål som kan aktive ras med Microsoft Azure. Detta innehåll känner dock också igen att läsaren kan vara riktad mot breda affärs-, kultur-eller tekniska utmaningar och att ibland kan kräva en moln neutral position. Därför börjar varje avsnitt i den här vägledningen med en Azure-första metod och följer sedan med molnbaserad teori som kan skalas över flera affärs-och tekniska beslut.

I det här ramverket är aktivering ett kärn tema. Följande check lista specificerar grundläggande principer för införande av moln som garanterar att en implementerings resa betraktas som lyckad av både IT och verksamheten:

- **Plan:** Upprätta tydliga [affärs resultat](../strategy/business-outcomes/index.md), en tydligt definierad plan för [digital plan](../digital-estate/index.md)och välförståde [implementerings loggar](../migrate/migration-considerations/prerequisites/migration-backlog-review.md).
- **Klart:** Se till att personalen har beredskap genom [kunskaper och utbildnings planer](../ready/suggested-skills.md).
- **Arbeta:** Definiera en hanterbar drifts modell för att hantera aktiviteter under och länge efter införandet.
  - **[Organisera](../organize/index.md):** Justera människor och team för att leverera rätt moln drift och införande.
  - **Styr:** Justera lämpliga [styrnings discipliner](../govern/index.md) för att konsekvent tillämpa kostnads hantering, risk minskning, efterlevnad och säkerhets bas linjer i alla moln införande.
  - **Hantera:** Kontinuerlig [drift hantering](../manage/index.md) av IT-portföljen för att minimera avbrott i affärs processer och säkerställa stabiliteten hos IT-portföljen.
  - **Support:** Justera lämpliga [alternativ för partnerskap och support](../migrate/migration-considerations/assess/partnership-options.md).

Ett annat kärn tema är säkerhet, vilket är ett kritiskt Quality-attribut för ett framgångs rik moln införande. Säkerhet är integrerat i det här ramverket för att tillhandahålla integrerad vägledning om att upprätthålla sekretess, integritet och tillgänglighets garantier för dina moln arbets belastningar.

## <a name="additional-tools"></a>Ytterligare verktyg

Utöver moln implementerings ramverket täcker Microsoft ytterligare ämnen som kan aktivera framgång. I den här artikeln beskrivs några vanliga verktyg som kan förbättra effektiviteten i moln implementerings ramverket markant. Att upprätta moln styrning, elastiska arkitekturer, tekniska kunskaper och en DevOps-metod är var och en som är viktiga för att det ska bli en moln implementerings ansträngning. Bok märke den här sidan som en resurs för att gå tillbaka i alla moln införande resor.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsH">
<li style="display: flex; flex-direction: column;">
    <a href="../govern/guides/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Cloud Adoption Framework governance model" src="../_images/operational-transformation-govern-highres.png" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Moln styrning</h3>
                        <p>Förstå affärs risk, Kartlägg dessa risker med korrekta principer och processer. Genom att använda verktyg för moln styrning och de fem disciplinerna i moln styrning minimerar riskerna och förbättrar sannolikheten för att lyckas. Moln styrning hjälper till att kontrol lera kostnader, skapa konsekvens, förbättra säkerheten och påskynda distributionen.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://docs.microsoft.com/azure/architecture/framework/resiliency/overview" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Resilient architecture" src="https://docs.microsoft.com/azure/architecture/resiliency/images/redundancy.svg" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Tillförlitlig arkitektur (återhämtning)</h3>
                        <p>Att skapa ett tillförlitligt program i molnet skiljer sig från traditionell programutveckling. Förut kan du ha köpt nivåer av redundant högre maskin vara för att minimera risken för att en hel program plattform Miss lyckas. I molnet bekräftar vi att vi kommer fram till att felen inträffar. Målet är att minimera effekten av en enda komponent som havererar snarare än att förhindra fel helt och hållet.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="../ready/suggested-skills.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Build Technical Skills" src="https://docs.microsoft.com/media/learn/Product/Learn/learningpath_graphic.svg" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Utveckling av tekniska kunskaper</h3>
                        <p>Det bästa verktyget för att hjälpa till med implementeringen av molnet är ett välutbildat team. Utöka kunskaperna för befintliga affärs-och teknik grupps medlemmar med hjälp av fokuserade inlärnings vägar.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://docs.microsoft.com/azure/devops/learn/" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Learn DevOps" src="https://docs.microsoft.com/azure/devops/learn/_img/learn-devops.svg" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>DevOps-metod</h3>
                        <p>Microsofts historiska omvandling är uppkopplad ordentligt i en växande tänkesätt-metod till kultur och en DevOps-metod för teknisk körning. Ramverket för moln införande bäddar in både i ramverket. För att påskynda DevOps-implementeringen kan du läsa mer i Learning DevOps-innehållet</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://docs.microsoft.com/azure/architecture/" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Azure Architecture Center" src="https://docs.microsoft.com/azure/architecture/example-scenario/data/media/architecture-data-warehouse.png" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Azure Architecture Center</h3>
                        <p>Arkitektur lösningar, referens arkitekturer, exempel scenarier, metod tips och moln design mönster för att hjälpa till med arkitekturen i lösningar som körs på Azure.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://azure.microsoft.com/pricing/calculator" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Azure Pricing Calculator" src="../_images/calculator-preview.png" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Azure priskalkylator</h3>
                        <p>Beräkna kostnaden för de olika Azure-komponenter som krävs för att skapa eller migrera en vald lösning.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Nästa steg

Med tanke på de viktigaste funktionerna i moln implementerings ramverket är sannolikheten att lyckas i en [migrering](./migrate.md) eller en [förnyad](./innovate.md) ansträngning att vara den mycket högre.

> [!div class="nextstepaction"]
> [Migrera](./migrate.md)
>
> [Utveckla](./innovate.md)

<!-- test:ignoreNextStep -->
