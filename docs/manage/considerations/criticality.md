---
title: Affärs kritiskhet i moln hantering
description: Använd ramverket för moln införande för Azure för att förstå arbets Belastningens kritiskahet och förhindra negativ inverkan på intäkter och lönsamhet.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 2c3d5a71025e821b9554e2a8d99223c7e6b0712b
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341461"
---
# <a name="business-criticality-in-cloud-management"></a>Affärs kritiskhet i moln hantering

För alla företag finns det ett litet antal arbets belastningar som är för viktiga för att kunna fungera. Dessa arbets belastningar betraktas som verksamhets kritiska. När dessa arbets belastningar drabbas av avbrott eller prestanda försämringar kan den negativa påverkan på intäkter och lönsamhet tas ur drift över hela företaget.

I andra änden av spektrumet kan vissa arbets belastningar gå i månader i taget utan att användas. Dåliga prestanda eller avbrott för dessa arbets belastningar är inte önskvärda, men påverkan är isolerad och begränsad.

Att förstå allvarlighets graden för varje arbets belastning i IT-portföljen är det första steget mot att upprätta ömsesidiga åtaganden till moln hantering.
Följande diagram illustrerar en gemensam justering mellan den kritiska skalan som följer och de standard åtaganden som gjorts av verksamheten.

![Justering av viktighets grad och hanterings nivå](../../_images/manage/cloud-criticality-alignment.png)

## <a name="criticality-scale"></a>Kritisk skala

Det första steget i alla affärs kritiska anpassningar är att skapa en kritisk skala. I följande tabell visas en exempel skala som ska användas som referens, eller mall för att skapa en egen skala.

| Allvarlighets grad | Vyn företag |
| --------- | --------- |
| Verksamhetskritiskt |  Påverkar företagets uppdrag och kan påverka företagets vinst-och förlust rapporter märkbart. |
| Enhets kritisk | Påverkar uppdraget för en speciell affär senhet och dess vinst-och förlust uttryck. |
| Hög | Kanske inte hindrar uppdraget, utan påverkar processer med hög prioritet. Mätbara förluster kan kvantifieras i händelse av avbrott. |
| Medel | Påverkan på processer är förmodligen. Förlusten är låg eller immeasurable, men varumärkes skada eller uppströms förlust är troligt vis. |
| Låg | Påverkan på affärs processer är inte mätbart. Varken varumärkes skada eller överordnad förlust är troligt vis. En lokaliserad inverkan på ett enda team är förmodligen. |
| Stöd saknas | Ingen företags ägare, grupp eller process som är associerad med den här arbets belastningen kan motivera alla investeringar i den pågående hanteringen av arbets belastningen. |

Det är vanligt för företag att inkludera ytterligare kritiska klassificeringar som är specifika för deras bransch, vertikala eller specifika affärs processer. Exempel på ytterligare klassificeringar är:

- **Kompatibilitet – kritiskt:** I kraftigt reglerat branscher kan vissa arbets belastningar vara kritiska som en del av en ansträngning för att upprätthålla kraven på efterlevnad.
- **Säkerhets kritiskt:** Vissa arbets belastningar kanske inte är verksamhets kritiska, men avbrott kan leda till förlust av data eller oavsiktlig åtkomst till skyddad information.
- **Säkerhets kritiskt:** När livet eller den fysiska säkerheten för anställda och kunder är utsatt för risk under ett avbrott, kan det vara klokt att klassificera arbets belastningar som säkerhets kritiska.

## <a name="importance-of-accurate-criticality"></a>Prioritet för korrekt allvarlighets grad

Senare i moln implementerings processen använder moln hanterings teamet denna klassificering för att fastställa hur mycket ansträngning som krävs för att uppfylla de justerade kritiska nivåerna. I lokala miljöer köps drifts hanteringen ofta centralt och behandlas som en nödvändig affärs börda, med lite eller inga ytterligare drift kostnader. I molnet har Operations Management (till exempel hela molnet) köpts per till gång som månatlig drifts kostnad.

Eftersom det finns en klar och direkt kostnad för drifts hantering i molnet är det viktigt att justera kostnader och önskade kritiska skalor på rätt sätt.

## <a name="select-a-default-criticality"></a>Välj en standard allvarlighets grad

En inledande granskning av alla arbets belastningar i portföljen kan ta lång tid. För att säkerställa att den här ansträngningen inte blockerar din bredare moln strategi rekommenderar vi att dina team samtycker till en standard kritiskhet som gäller för alla arbets belastningar.

Baserat på föregående kritiskt skalnings tabell, rekommenderar vi att du antar *medelhög* allvarlighets grad som standard. På så sätt kan moln strategi teamet snabbt identifiera arbets belastningar som kräver en högre viktighets grad.

## <a name="use-the-template"></a>Använd mallen

Följande steg gäller om du använder [arbets boken för OPS-hantering](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) för att planera för moln hantering.

1. Anteckna den kritiska skalan på fliken **skala** i arbets boken.
2. Uppdatera varje arbets belastning i *exemplet* eller den *rensade mallen* så att den återspeglar standard allvarlighets graden i kolumnen *allvarlighets grad* .
3. Företaget bör ange rätt värden för att avspegla eventuella avvikelser från standard kritiskaheten.

## <a name="next-steps"></a>Nästa steg

När ditt team har definierat affärs kritiskhet kan du [Beräkna och registrera företags påverkan](./impact.md).

> [!div class="nextstepaction"]
> [Beräkna och registrera företags påverkan](./impact.md)
