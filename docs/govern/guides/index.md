---
title: Molnstyrningsguider
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig mer om de användbara styrningsguiderna som finns i Cloud Adoption Framework.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: c7d019cc7264ba972252b6182d4f2c10d7b91f43
ms.sourcegitcommit: 945198179ec215fb264e6270369d561cb146d548
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/04/2019
ms.locfileid: "71967595"
---
# <a name="cloud-governance-guides"></a>Molnstyrningsguider

De användbara styrningsguiderna i det här avsnittet illustrerar den inkrementella strategin i Cloud Adoption Framework-styrningsmodellen, baserat på [styrningsmetodiken](../methodology.md) som beskrevs tidigare. Du kan skapa en flexibel metod för molnstyrning som uppfyller kraven i alla tänkbara molnstyrningsscenarier.

## <a name="review-and-adopt-cloud-governance-best-practices"></a>Gå igenom och implementera bästa praxis för molnstyrning

Välj någon av följande styrningsguider för att påbörja din molnimplementeringsresa. Varje guide beskriver en uppsättning metodtips, baserade på ett antal fiktiva kundupplevelser. Om du inte är bekant med den inkrementella strategin i Cloud Adoption Framework-styrningsmodellen rekommenderar vi att du läser igenom introduktionen till styrningskonceptet nedan innan du implementerar bästa praxis.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsZ">
<li style="display: flex; flex-direction: column;">
    <a href="./standard/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
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
    <a href="./complex/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
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

## <a name="an-incremental-approach-to-cloud-governance"></a>En inkrementell molnstyrningsstrategi

## <a name="choosing-a-governance-guide"></a>Välja en styrningsguide

Guiderna visar hur du implementerar en styrnings-MVP. Därifrån visar varje guide hur molnstyrningsteamet, i egenskap av partner, kan bana vägen för molnimplementeringsteamen och påskynda implementeringsarbetet. Cloud Adoption Framework-styrningsmodellen beskriver styrningsimplementeringen från det första steget och genom de efterföljande förbättringarna och utvecklingarna.

Välj något av följande två alternativ för att påbörja en styrningsresa. Alternativen baseras på syntetiserade kundupplevelser. För att underlätta navigeringen baseras titlarna på företagets komplexitet. Läsarens beslut kan dock vara mer komplext. Följande tabeller beskriver skillnaderna mellan de två alternativen.

> [!WARNING]
> En mer stabil startpunkt för styrningen kan krävas. I sådana fall bör du överväga att [Azure Virtual Datacenter](#azure-virtual-datacenter)-metoden som beskrivs kortfattat [nedan](#azure-virtual-datacenter). Den här metoden rekommenderas ofta för implementeringar i företagsskala, särskilt för implementeringar som överstiger 10 000 tillgångar. Det är också det naturliga valet i komplexa styrningsscenarier när något av följande krävs: omfattande krav på efterlevnad med tredje part, djupgående domänexpertis eller paritet med mogna IT-styrningsprinciper och efterlevnadskrav.

> [!NOTE]
> Det är osannolikt att en guide helt överensstämmer med din situation. Välj den guide som mest liknar din situation och använd den som startpunkt. Ytterligare information ges under hela guiden så att du kan anpassa beslut efter specifika villkor.

### <a name="business-characteristics"></a>Företagsegenskaper

| Egenskap | Standardorganisation | Komplext företag |
|---|---|---|
| Geografiskt område (land eller geopolitisk region) | Kunder eller personal finns huvudsakligen i samma geografiska område | Kunder eller personal finns i flera geografiska områden eller kräver nationella moln. |
| Affärsenheter som påverkas | Affärsenheter som delar en gemensam IT-infrastruktur | Flera affärsenheter som inte delar en gemensam IT-infrastruktur |
| IT-budget | En enda IT-budget | Budget fördelad mellan affärsenheter och valutor |
| IT-investeringar | Kapitalkostnaderna för investeringar planeras årligen och täcker oftast endast grundläggande underhåll. | Kapitalkostnaderna för investeringar planeras årligen och täcker ofta underhåll och en förnyelsecykel på tre till fem år. |

### <a name="current-state-before-adopting-cloud-governance"></a>Tillstånd före implementeringen av molnstyrning

| Status | Standardföretag | Komplext företag |
|---|---|---|
| Datacenter eller utomstående leverantörer av värdtjänster | Mindre än fem datacenter | Fler än fem datacenter |
| Nätverk | Inga WAN- eller 1 &ndash; 2 WAN-leverantörer | Komplext nätverk eller globalt WAN |
| Identitet | En skog, en domän. | Komplext, flera skogar, flera domäner. |

### <a name="desired-future-state-after-incremental-improvement-of-cloud-governance"></a>Önskat tillstånd efter inkrementell förbättring av molnstyrning

| Status | Standardorganisation | Komplext företag |
|---|---|---|
| Kostnadshantering – molnredovisning | Showback-modell. Faktureringen är centraliserad via IT. | Återbetalningsmodell. Faktureringen kan distribueras via IT-inköp. |
| Säkerhetsbaslinje – skyddade data | Finansiella företagsdata och IP. Begränsade kunddata. Inga krav på efterlevnad från tredje part. | Flera samlingar av kunders finansiella och personliga data. Kan behöva tänka på efterlevnadskrav från tredje part. |

## <a name="azure-virtual-datacenter"></a>Azure Virtual Datacenter

Azure Virtual Datacenter är en metod för att få ut det mesta av Azure-molnplattformens funktioner samtidigt som företagets krav på säkerhet och styrning respekteras.

Jämfört med traditionella lokala miljöer gör Azure det möjligt för arbetsbelastningsutvecklingsteam och deras affärspartner att dra nytta av den större distributionsflexibilitet som molnplattformarna erbjuder. Men eftersom molnimplementeringen även omfattar verksamhetskritiska data och arbetsbelastningar kan den här flexibiliteten stå i konflikt med de efterlevnadskrav på säkerhet och principer som företagets IT-team har upprättat. Detta gäller särskilt stora företag som har befintliga avancerade styrnings- och efterlevnadskrav.

Azure Virtual Datacenter-metoden hanterar dessa problem tidigare i implementeringsprocessen genom att tillhandahålla modeller, referensarkitekturer, exempel på automationsartefakter och vägledning för att få balans mellan utvecklar- och IT-styrningskrav under företagets molnintegreringsarbete. Centralt i den här metoden är själva konceptet av ett virtuellt datacenter: implementeringen av isoleringsgränser runt din molninfrastruktur genom tillämpning av åtkomst- och säkerhetskontroller, nätverksprinciper och efterlevnadsövervakning.

Ett virtuellt datacenter kan betraktas som ditt eget isolerade moln inom Azure-plattformen, som integrerar de hanteringsprocesser, regelkrav och säkerhetsprocesser som krävs av din styrningsprinciper. Inom den här virtuella gränsen erbjuder Azure Virtual Datacenter exempelmodeller för att distribuera arbetsbelastningar samtidigt som man säkerställer konsekvent efterlevnad och tillhandahåller grundläggande information om hur organisationen implementerar sina separata roller och ansvarsområden i molnet.

### <a name="azure-virtual-datacenter-assumptions"></a>Antaganden om Azure Virtual Datacenter

Även om mindre team kan ha nytta av de modeller och rekommendationer som Azure Virtual Datacenter erbjuder, är den här metoden avsedd att hjälpa företagets IT-grupper att hantera stora molnmiljöer. Om din organisation uppfyller följande kriterier rekommenderar vi att du tar hjälp av vägledningen för Azure Virtual Datacenter när du utformar din Azure-baserade molninfrastruktur:

- Ditt företag måste uppfylla efterlevnadskrav som kräver centraliserad övervakning och granskningsfunktioner.
- Det är viktigt att du upprätthåller gemensam princip- och styrningsefterlevnad, samt central IT-kontroll över kärntjänster.
- Din bransch är beroende av en avancerad plattform, vilket kräver avancerade kontroller och omfattande domänkunskaper för att styra plattformen. Detta är vanligast i stora företag inom finans, olja och gas, samt tillverkning.
- De befintliga IT-styrningsprinciperna kräver striktare paritet med befintliga funktioner, även tidigt i implementeringsprocessen.

Mer information finns i avsnittet [Azure Virtual Datacenter](../../reference/vdc.md) i Cloud Adoption Framework.

## <a name="next-steps"></a>Nästa steg

Välj någon av dessa guider:

> [!div class="nextstepaction"]
> [Standardguide för styrning av företag](./standard/index.md)
>
> [Styrningsguide för komplexa företag](./complex/index.md)
