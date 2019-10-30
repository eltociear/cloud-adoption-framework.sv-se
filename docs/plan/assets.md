---
title: Justera till gångar till prioriterade arbets belastningar
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Justera till gångar till prioriterade arbets belastningar
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: ef5ffecd998bbe4e5adadd30cf24fe965e22b703
ms.sourcegitcommit: 7ffb0427bba71177f92618b2f980e864b72742f4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/29/2019
ms.locfileid: "73048271"
---
# <a name="align-assets-to-prioritized-workloads"></a>Justera till gångar till prioriterade arbets belastningar

Arbets belastning är en konceptuell Beskrivning av en samling till gångar: virtuella datorer, program och data källor. Föregående artikel, [prioritera och definiera arbets belastningar](./workloads.md)och ger vägledning om hur du samlar in de data som ska definiera arbets belastningen. Innan migreringen kräver några av de tekniska inmatningarna i listan ytterligare verifiering. Den här artikeln hjälper till med verifiering av följande indata:

- **Program:** Visa en lista över program som ingår i den här arbets belastningen.
- **Virtuella datorer och servrar:** Lista över virtuella datorer eller servrar som ingår i arbets belastningen.
- **Data Källor:** Lista alla data källor som ingår i arbets belastningen.
- **Beroenden:** Lista de till gångs beroenden som inte ingår i arbets belastningen.

Det finns flera alternativ för att montera dessa data. Följande är några av de vanligaste metoderna.

## <a name="alternative-inputs-migrate-modernize-innovate"></a>Alternativa indata: migrera, modernisera, förnya

Målet med föregående data punkter är att samla in relativt teknisk ansträngning och beroenden som ett stöd för prioritering. Beroende på vilken över gång du vill ha kan du behöva samla in alternativa data punkter för att ge stöd för korrekt prioritering.

**Migrera:** För rena migreringar fungerar befintliga inventerings-och till gångs beroenden som ett rimligt mått på relativ komplexitet.

**Modernisera:** När målet för en arbets belastning är att modernisera program eller andra till gångar är dessa data punkter fortfarande fasta mått på komplexitet. Det kan dock vara bra att lägga till inmatade modernisering-möjligheter i arbets belastnings dokumentationen.

**Förnya:** När data eller affärs logik genomgår väsentlig förändring under en moln implementering, betraktas det som en *förnyad* typ av omvandling. Samma sak gäller när du skapar nya data eller en ny affärs logik. Vid eventuella förnyade scenarier representerar migreringen av till gångar troligt vis den minsta mängden arbete som krävs. I dessa scenarier bör teamet utforma en uppsättning tekniska data inmatningar för att mäta relativ komplexitet.

## <a name="azure-migrate"></a>Azure Migrate

Azure Migrate innehåller en uppsättning grupperings funktioner som kan påskynda sammanställningen av program, virtuella datorer, data källor och beroenden. När arbets belastningar har definierats konceptuellt kan de användas som underlag för att gruppera till gångar baserat på beroende mappning.

Azure Migrate dokumentationen ger vägledning om [hur du grupperar datorer baserat på beroenden](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies).

## <a name="configuration-management-database"></a>Konfiguration – hanterings databas

Vissa organisationer har en väl underunderhållen konfigurations hanterings databas (CMDB) i befintliga verktyg för Operations Management. De kan använda CMDB för att ange de indata punkter som diskuteras tidigare.

## <a name="next-steps"></a>Nästa steg

[Granska rationalisering-beslut](./review-rationalization.md) baserat på till gångs justering och arbets belastnings definitioner.

> [!div class="nextstepaction"]
> [Granska rationalisering-beslut](./review-rationalization.md)
