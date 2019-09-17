---
title: Justera ansvar mellan team
titleSuffix: Microsoft Cloud adoption Framework for Azure
description: Lär dig att justera ansvars områden mellan team.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 818d2fa74c480b8aee36c4d268ae7a83cb93fab3
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027869"
---
# <a name="align-responsibilities-across-teams"></a>Justera ansvars områden mellan team

Lär dig att justera ansvars områden mellan grupper genom att utveckla en matris för flera grupper som identifierar *ansvariga, konto bara, besökta och välgrundade* (raci) parter. Den här artikeln innehåller ett exempel på en RACI-matris för organisations strukturer som beskrivs i [upprätta team strukturer](./organization-structures.md):

- [Endast moln antagande team](#cloud-adoption-team-only)
- [Bästa praxis för MVP](#best-practice-minimum-viable-product-mvp)
- [Centrala IT](#central-it)
- [Strategisk justering](#strategic-alignment)
- [Drift justering](#operational-alignment)
- [Expert Center i molnet (CCoE)](#cloud-center-of-excellence-ccoe)

Hämta och ändra [kalkyl blads mal len raci](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx)om du vill spåra beslut om organisations struktur över tid.

I exemplen i den här artikeln anges dessa RACI-konstruktioner:

- Det team som är ett *konto* för en funktion.
- De team som är *ansvariga* för resultatet.
- Team som bör *konsulteras* under planeringen.
- De team som bör *informeras* när arbetet har slutförts.

Den sista raden i varje tabell (förutom den första) innehåller en länk till den mest justerade moln kapaciteten för ytterligare information.

## <a name="cloud-adoption-team-only"></a>Endast moln antagande team

|  |Lösnings leverans  |Affärs justering  |Ändringshantering  |Lösnings åtgärder  |Styrning |Plattforms förfallo tid  |Plattforms åtgärder  |Plattforms automatisering  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Moln antagande team |Accountable|Accountable|Accountable|Accountable|Accountable|Accountable|Accountable|Accountable|

## <a name="best-practice-minimum-viable-product-mvp"></a>Bästa praxis: minimal livskraftig produkt (MVP)

|  |Lösnings leverans  |Affärs justering  |Ändringshantering  |Lösnings åtgärder  |Styrning |Plattforms förfallo tid  |Plattforms åtgärder  |Plattforms automatisering  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Moln antagande team|Accountable|Accountable|Accountable|Accountable|Konsulterad|Konsulterad|Konsulterad|Uppdaterad|
|Team för moln styrning|Konsulterad|Uppdaterad|Uppdaterad|Uppdaterad|Accountable|Accountable|Accountable|Accountable|
||||||||||
|Justerad moln kapacitet|[Moln införande](./cloud-adoption.md)|[Moln strategi](./cloud-strategy.md)|[Moln strategi](./cloud-strategy.md)|[Moln åtgärder](./cloud-operations.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud-styrning](./cloud-governance.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud Platform](./cloud-platform.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud Platform](./cloud-platform.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud Automation](./cloud-automation.md)|

## <a name="central-it"></a>Central IT

| |Lösnings leverans  |Affärs justering  |Ändringshantering  |Lösnings åtgärder  |Styrning |Plattforms förfallo tid  |Plattforms åtgärder  |Plattforms automatisering  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Moln antagande team  |Accountable|Accountable|Skyldighet    |Skyldighet|Uppdaterad   |Uppdaterad   |Uppdaterad   |Uppdaterad   |
|Team för moln styrning|Konsulterad  |Uppdaterad   |Uppdaterad   |Uppdaterad   |Accountable|Konsulterad  |Skyldighet|Uppdaterad   |
|Central IT           |Konsulterad  |Uppdaterad   |Accountable   |Accountable   |Skyldighet  |Accountable|Accountable|Accountable|
||||||||||
|Justerad moln kapacitet|[Moln införande](./cloud-adoption.md)|[Moln strategi](./cloud-strategy.md)|[Moln strategi](./cloud-strategy.md)|[Moln åtgärder](./cloud-operations.md)|[Molnstyrning](./cloud-governance.md)|[Centrala IT](./central-it.md)|[Centrala IT](./central-it.md)|[Centrala IT](./central-it.md)|

## <a name="strategic-alignment"></a>Strategisk justering

|  |Lösnings leverans  |Affärs justering  |Ändringshantering  |Lösnings åtgärder  |Styrning |Plattforms förfallo tid  |Plattforms åtgärder  |Plattforms automatisering  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Moln strategi team  |Konsulterad  |Accountable|Accountable|Konsulterad  |Konsulterad  |Uppdaterad   |Uppdaterad   |Uppdaterad   |
|Moln antagande team  |Accountable|Konsulterad  |Skyldighet|Accountable|Uppdaterad   |Uppdaterad   |Uppdaterad   |Uppdaterad   |
|CCoE-modell RACI      |Konsulterad  |Uppdaterad   |Uppdaterad   |Uppdaterad   |Accountable|Accountable|Accountable|Accountable|
||||||||||
|Justerad moln kapacitet|[Moln införande](./cloud-adoption.md)|[Moln strategi](./cloud-strategy.md)|[Moln strategi](./cloud-strategy.md)|[Moln åtgärder](./cloud-operations.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud-styrning](./cloud-governance.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud Platform](./cloud-platform.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud Platform](./cloud-platform.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud Automation](./cloud-automation.md)|

## <a name="operational-alignment"></a>Drift justering

|  |Lösnings leverans  |Affärs justering  |Ändringshantering  |Lösnings åtgärder  |Styrning |Plattforms förfallo tid  |Plattforms åtgärder  |Plattforms automatisering  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Moln strategi team  |Konsulterad  |Accountable|Accountable|Konsulterad  |Konsulterad  |Uppdaterad   |Uppdaterad   |Uppdaterad   |
|Moln antagande team  |Accountable|Konsulterad  |Skyldighet|Konsulterad  |Uppdaterad   |Uppdaterad   |Uppdaterad   |Uppdaterad   |
|Moln drifts team|Konsulterad  |Konsulterad  |Skyldighet|Accountable|Konsulterad  |Uppdaterad   |Accountable|Konsulterad  |
|CCoE-modell RACI      |Konsulterad  |Uppdaterad   |Uppdaterad   |Uppdaterad   |Accountable|Accountable|Skyldighet|Accountable|
||||||||||
|Justerad moln kapacitet|[Moln införande](./cloud-adoption.md)|[Moln strategi](./cloud-strategy.md)|[Moln strategi](./cloud-strategy.md)|[Moln åtgärder](./cloud-operations.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud-styrning](./cloud-governance.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud Platform](./cloud-platform.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud Platform](./cloud-platform.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud Automation](./cloud-automation.md)|

## <a name="cloud-center-of-excellence-ccoe"></a>Expert Center i molnet (CCoE)

|  |Lösnings leverans  |Affärs justering  |Ändringshantering  |Lösnings åtgärder  |Styrning |Plattforms förfallo tid  |Plattforms åtgärder  |Plattforms automatisering  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Moln strategi team  |Konsulterad  |Accountable|Accountable|Konsulterad  |Konsulterad  |Uppdaterad   |Uppdaterad   |Uppdaterad   |
|Moln antagande team  |Accountable|Konsulterad  |Skyldighet|Konsulterad  |Uppdaterad   |Uppdaterad   |Uppdaterad   |Uppdaterad   |
|Moln drifts team|Konsulterad  |Konsulterad  |Skyldighet|Accountable|Konsulterad  |Uppdaterad   |Accountable|Konsulterad  |
|Team för moln styrning|Konsulterad  |Uppdaterad   |Uppdaterad   |Konsulterad  |Accountable|Konsulterad  |Skyldighet|Uppdaterad   |
|Moln plattforms team  |Konsulterad  |Uppdaterad   |Uppdaterad   |Konsulterad  |Konsulterad  |Accountable|Skyldighet|Skyldighet|
|Cloud Automation-team|Konsulterad  |Uppdaterad   |Uppdaterad   |Uppdaterad   |Konsulterad  |Skyldighet|Skyldighet|Accountable|
||||||||||
|Justerad moln kapacitet|[Moln införande](./cloud-adoption.md)|[Moln strategi](./cloud-strategy.md)|[Moln strategi](./cloud-strategy.md)|[Moln åtgärder](./cloud-operations.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud-styrning](./cloud-governance.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud Platform](./cloud-platform.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud Platform](./cloud-platform.md)|[](./cloud-center-of-excellence.md)CCoE-[Cloud Automation](./cloud-automation.md)|

## <a name="next-steps"></a>Nästa steg

Hämta och ändra [kalkyl blads mal len raci](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx)för att spåra beslut om organisations struktur över tid. Kopiera och ändra det bäst justerade exemplet från RACI-matriser i den här artikeln.

> [!div class="nextstepaction"]
> [Ladda ned RACI-kalkylbladsmallen](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx)