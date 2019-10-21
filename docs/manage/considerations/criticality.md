---
title: Verksamhets kritiskhet – moln hantering och åtgärder
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Verksamhets kritiskhet – moln hantering och åtgärder
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 6e372156d3fd8d765bcafeeff3a6919aa7f8ead3
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557627"
---
# <a name="business-criticality-in-cloud-management"></a>Affärs kritiskhet i moln hantering

För alla företag finns det ett litet antal arbets belastningar som är för viktiga för att kunna fungera. När dessa arbets belastningar drabbas av avbrott eller prestanda försämring kan en negativ inverkan på intäkterna och lönsamheten beskrivas över hela företaget. Arbets belastningarna anses vara verksamhets kritiska.

I andra änden av spektrumet kan vissa arbets belastningar gå i månader i taget utan att användas. Dåliga prestanda eller avbrott för dessa arbets belastningar är inte önskvärda, men påverkan är isolerad och begränsad.

Att förstå allvarlighets graden för varje arbets belastning i IT-portföljen är det första steget mot ömsesidiga åtaganden till moln hantering.
Bilden nedan beskriver en gemensam justering mellan den kritiska skalan som följer och de standard åtaganden som gjorts av verksamheten.

![Justering av viktighets grad och hanterings nivå](../../_images/manage/cloud-criticality-alignment.png)

## <a name="criticality-scale"></a>Kritisk skala

Det första steget i en justerings insats för affärs kritiska åtgärder är att skapa en kritisk skala. Nedan visas en exempel skala som kan användas som referens, eller en mall för att skapa en egen skala.

|Allvarlighets grad  |Vyn företag  |
|---------|---------|
|Verksamhets kritisk|Påverkar företagets uppdrag och kan märkbart påverka företagets vinst-och förlust rapporter.|
|Enhets kritisk|Påverkar uppdragen för en enskild affär senhet och den vinst-och förlust deklarationen för affärs enheter.|
|Hög|Får inte hindra uppdraget, men påverkar processer med hög prioritet. Mätbara förluster kan kvantifieras i händelse av avbrott.|
|Medium|Påverkan på processer är förmodligen. Förlusten är låg eller immeasurable, men varumärkes skada eller överströms förlust är troligt vis.|
|Låg|Påverkan på affärs processer är immeasurable. Varken varumärkes skada eller överordnad förlust är troligt vis. En lokaliserad inverkan på ett enda team är förmodligen.|
|Stöd saknas|Ingen företags ägare, grupp eller process som är kopplad till den här arbets belastningen kan motivera alla investeringar i pågående hantering av arbets belastningen|

Det är vanligt för företag att inkludera ytterligare kritiska klassificeringar som är specifika för en bransch, lodrät eller specifika affärs processer. Exempel på ytterligare klassificeringar är:

- **Kompatibilitet – kritiskt:** I kraftigt reglerat branscher kan vissa arbets belastningar vara kritiska som en del av en ansträngning för att upprätthålla kraven på efterlevnad.
- **Säkerhets kritiskt:** Vissa arbets belastningar kanske inte är verksamhets kritiska, men avbrott kan leda till förlust av data eller oavsiktlig åtkomst till skyddad information.
- **Säkerhets kritiskt:** När liv eller fysisk säkerhet för anställda och kunder är i fara under ett avbrott, kan det vara klokt att klassificera arbets belastningar som säkerhets kritiska.

## <a name="importance-of-accurate-criticality"></a>Prioritet för korrekt allvarlighets grad

Senare i den här processen kommer moln hanterings teamet att använda den här klassificeringen för att fastställa hur mycket ansträngning som krävs för att uppfylla de justerade kritiska nivåerna. I lokala miljöer har Operations Management ofta köpts centralt och behandlas som en nödvändig affärs börda, med lite/inga ytterligare drifts kostnader. I molnet har Operations Management (till exempel hela molnet) köpts per till gång som månatlig drifts kostnad.

Eftersom det finns en klar och direkt kostnad för drifts hantering i molnet är det viktigt att justera kostnader och önskade kritiska skalor på rätt sätt.

## <a name="select-a-default-criticality"></a>Välj en standard allvarlighets grad

En inledande granskning av alla arbets belastningar i portföljen kan ta lång tid. För att säkerställa att den här ansträngningen inte blockerar den bredare moln strategin rekommenderar vi att den och företaget är eniga om en standard kritiskhet som ska gälla för alla arbets belastningar.

Baserat på den kritiska skalan ovan föreslås det att "medium"-kritiskt används som standard. På så sätt kan moln strategi teamet snabbt identifiera arbets belastningar som kräver en högre viktighets grad.

## <a name="using-the-template"></a>Använda mallen

Följande steg gäller för läsare som använder [arbets boken för OPS-hantering](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) för att planera för moln hantering.

1. Den kritiska skalan kan registreras på fliken skala i arbets boken.
2. Varje arbets belastning i "exempel" eller "Rensa mall" bör uppdateras för att avspegla den förvalda allvarlighets graden i kolumnen "Kritiskitet".
3. Korrigerade värden måste anges av verksamheten för att avspegla eventuella avvikelser från standard kritiskaheten.

## <a name="next-steps"></a>Nästa steg

När du har definierat en allvarlighets grad kan du [Beräkna och registrera företags påverkan](./impact.md).

> [!div class="nextstepaction"]
> [Beräkna och registrera företags påverkan](./impact.md)
