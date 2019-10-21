---
title: Affärs justering – moln hantering och åtgärder
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Affärs justering – moln hantering och åtgärder
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 9c6884d57b9238f58921b14ec3ddbbe3623506af
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558147"
---
# <a name="create-business-alignment-in-cloud-management"></a>Skapa affärs justering i moln hantering

I lokala miljöer hanteras IT-tillgångar (program, virtuella datorer, VM-värdar, disk, servrar, enheter och data källor) av IT-avdelningen för att stödja arbets belastnings åtgärder. I det här fallet är en arbets belastning en samling av IT-tillgångar som har stöd för en speciell affärs åtgärd. I lokala miljöer levererar IT-hanteringen process design för att minimera störningar på dessa IT-tillgångar, i ett försök att minimera avbrott i support verksamheten. När du flyttar till molnet byter hantering och åtgärder en bit, vilket skapar en möjlighet att utveckla bättre affärs anpassning.

## <a name="business-vernacular"></a>Affärs vernacular

Det första steget när du skapar affärs justering är term justering. IT-hanteringen, som de flesta tekniska yrkes grupper, innehåller en rättvis jargong eller mycket tekniska villkor. Dessa villkor kan leda till förvirring för affärs intressenter och göra det svårt att mappa hanterings tjänster till affärs värde.

Som tur är, processerna för att utveckla en strategi för moln införande och en implementerings plan för molnet, skapar en idé situation för ommappningen av villkor. Det skapar också en bra möjlighet att omtänkaa åtaganden till drifts hantering, i partnerskap med verksamheten. I följande artikel serie beskrivs den nya metoden i tre olika termer som kan förbättra konversationer med affärs intressenter:

- **[Allvarlighets grad](./criticality.md)** : mappa arbets belastningar till affärs processer. Rangordna kritiskhet för att fokusera investeringar.
- **[Påverkan](./impact.md)** : förstå effekten av potentiella avbrott för att utvärdera avkastningen på investeringar för moln hantering.
- **[Åtagande](./commitment.md)** : utveckla sanna partnerskap, genom att skapa och dokumentera avtal **med verksamheten**.

> [!NOTE]
> Under var och en av dessa termer är klassiska IT-termer som SLA, RTO och återställnings punkt. Kart läggning av affärs-och IT-villkor beskrivs i detalj i artikeln om åtagande.

## <a name="ops-management-planning-workbook"></a>Planera arbets bok för OPS Management

För att hjälpa till att samla in beslut till följd av den här konversationen finns en [arbets bok för OPS Management](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) i vår GitHub-lagrings platsen. Den här arbets boken utför inte SLA-eller kostnads beräkningar. Den fungerar bara som en vägledning för att samla in dessa åtgärder och prognostiserad Räntabilitet för att undvika åtgärder.

Alternativt kan dessa arbets belastningar och tillhör Ande till gångar taggas direkt i Azure, om lösningarna redan har distribuerats till molnet.

## <a name="next-steps"></a>Nästa steg

Börja skapa affärs anpassning genom att definiera [arbets belastnings kritiskhet](./criticality.md).

> [!div class="nextstepaction"]
> [Definiera belastnings kritiskhet](./criticality.md)
