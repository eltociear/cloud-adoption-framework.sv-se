---
title: Affärs anpassning i moln hantering
description: Använd ramverket för moln införande för Azure för att lära dig hur du hanterar moln driften och utvecklar bättre affärs anpassning.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 432e974a304741a64e0cd7da9577ecec5e35d57e
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434055"
---
# <a name="create-business-alignment-in-cloud-management"></a>Skapa affärs justering i moln hantering

I lokala miljöer hanteras IT-tillgångar (program, virtuella datorer, VM-värdar, disk, servrar, enheter och data källor) av IT-avdelningen för att stödja arbets belastnings åtgärder. I det här fallet är en arbets belastning en samling av IT-tillgångar som har stöd för en speciell affärs åtgärd. För att hjälpa till att stödja affärs åtgärder levererar IT-hanteringen processer som är utformade för att minimera störningar på dessa till gångar. När en organisation flyttar till molnet kan hantering och driften flytta en bit, vilket skapar en möjlighet att utveckla bättre affärs anpassning.

## <a name="business-vernacular"></a>Affärs vernacular

Det första steget när du skapar affärs justering är att säkerställa justeringen för termen. IT-hanteringen, som de flesta tekniska yrken, har amassed en samling jargong eller mycket tekniska villkor. Sådana villkor kan leda till förvirring för affärs intressenter och göra det svårt att mappa hanterings tjänster till affärs värde.

Som tur är processen för att utveckla en strategi för moln införande och en implementerings plan för molnet att skapa en perfekt möjlighet att mappa om dessa villkor. Processen skapar också affärs möjligheter för att omtänkaa åtaganden till drifts hantering, i partnerskap med verksamheten. Följande artikel serie vägleder dig genom den här nya metoden för tre specifika villkor som kan hjälpa dig att förbättra konversationer mellan affärs intressenter:

- **[Allvarlighets grad](./criticality.md):** Mappa arbets belastningar till affärs processer. Rangordna kritiskhet för att fokusera investeringar.
- **[Påverkan](./impact.md):** Förstå effekten av potentiella avbrott för att få hjälp med att utvärdera avkastningen på investeringar för moln hantering.
- **[Åtagande](./commitment.md):** utveckla verkliga partnerskap, genom att skapa och dokumentera avtal *med verksamheten*.

> [!NOTE]
> De underliggande villkoren är klassiska IT-villkor som SLA, RTO och återställnings punkt. Att kartlägga specifika affärs-och IT-villkor beskrivs mer detaljerat i [åtagande](./commitment.md) artikeln.

## <a name="ops-management-planning-workbook"></a>Planera arbets bok för OPS Management

För att hjälpa till att samla in beslut som orsakas av den här konversationen om termen justering, finns en [arbets bok för OPS Management](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) på vår GitHub-webbplats. Den här arbets boken utför inte SLA-eller kostnads beräkningar. Det fungerar bara för att hjälpa till att samla in sådana åtgärder och prognostiserad avkastning på åtgärder som kan undvikas.

Alternativt kan dessa arbets belastningar och tillhör Ande till gångar taggas direkt i Azure, om lösningarna redan har distribuerats till molnet.

## <a name="next-steps"></a>Nästa steg

Börja skapa affärs anpassning genom att definiera [arbets belastnings kritiskhet](./criticality.md).

> [!div class="nextstepaction"]
> [Definiera belastnings kritiskhet](./criticality.md)
