---
title: Beräkna molnkostnader före migreringen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: En förklaring av processen att beräkna molnkostnader före migreringen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: be4fe4616b4f0599075ceac2b9c0838949b350c8
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548481"
---
# <a name="estimate-cloud-costs"></a>Beräkna molnkostnader

Under migreringen finns det flera faktorer som kan påverka beslut och körning. I den här artikeln beskrivs alternativen för att beräkna molnkostnader i olika situationer.

## <a name="digital-estate-size"></a>Storlek på den digitala egendomen

Storleken på din digitala egendom har en direkt påverkan på migreringsbesluten. En migrering av 250 virtuella datorer är enklare att beräkna än en migrering av 10 000 virtuella datorer. Vi rekommenderar starkt att du väljer en mindre arbetsbelastning vid din första migrering. Det ger ditt team en chans att lära sig att beräkna kostnaderna för en enkel migrering innan de försöker beräkna större och mer komplicerade arbetsbelastningsmigreringar.

Men tänk på att en migrering av en mindre arbetsbelastning ändå kan innehålla ett varierande antal stödjande tillgångar. Om migreringen omfattar maximalt 1 000 virtuella datorer räcker det förmodligen med ett verktyg som [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-overview) vid insamlingen av data om lager och beräknade kostnader. Fler alternativ på verktyg för att beräkna kostnader beskrivs i artikeln om [kostnadsberäkningar för digital egendom](../../../digital-estate/calculate.md).

För 1 000 + enhets digitala fastigheter är det fortfarande möjligt att dela upp en uppskattning i fyra eller fem åtgärds bara iterationer, vilket gör uppskattnings processen hanterbar. Vid större egendomar eller när en högre grad av precision krävs i beräkningen, är en mer heltäckande metod (t.ex. den som beskrivs i avsnittet ”[Digital egendom](../../../digital-estate/index.md)” i Cloud Adoption Framework) troligtvis nödvändig.

## <a name="accounting-models"></a>Redovisningsmodeller

Redovisningsmodeller

Om du har arbetat med traditionella IT-upphandlingsprocesser kan en beräkning i molnet verka främmande. När du implementerar molnteknologier ändras anskaffningen från en fast och strukturerad modell för kapitalkostnader till en modell med rörliga driftskostnader. I den traditionella modellen för kapitalkostnader skulle IT-teamet försökt samla köpkraften för flera arbetsbelastningar i olika program till en central pool med delade IT-tillgångar som kunde stödja var och en av dessa lösningar. I molnmodellen för driftskostnader kan kostnaderna kopplas direkt till supportbehoven för enskilda arbetsbelastningar, team eller affärsenheter. Med den här metoden kan man använda en mer direkt tilldelning av kostnader till den interna kund som stöds. När du uppskattar kostnaderna är det viktigt att du först förstår hur mycket av den nya redovisnings kapaciteten som kommer att användas av IT-teamet.

De som vill fortsätta använda den äldre kapitalkostnadsmetoden till redovisningen kan använda utdatan från någon av de metoder som föreslås i avsnittet ”[Storlek på digital egendom](#digital-estate-size)” ovan för att få en årlig kostnadsgrund. Sedan multiplicerar du denna årliga kostnad med företagets typiska maskin varu uppdaterings cykel. Uppdateringscykeln för maskinvara är den hastighet som ett företag ersätter äldre maskinvara med, vanligtvis mätt i år. Den årliga hastigheten för körning multipliceras med uppdateringscykeln för maskinvara och skapar en kostnadsstruktur som liknar ett investeringsmönster för kapitalkostnader.

## <a name="next-steps"></a>Nästa steg

När kostnaderna har beräknats kan migreringen påbörjas. Det är dock klokt att gå igenom [partnerskaps- och supportalternativen](./partnership-options.md) innan någon migrering startas.

> [!div class="nextstepaction"]
> [Förstå partnerskapsalternativ](./partnership-options.md)
