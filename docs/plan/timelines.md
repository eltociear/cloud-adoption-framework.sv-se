---
title: Tids linjer i en moln implementerings plan
description: Tids linjer i en moln implementerings plan
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 4918c5e4c9efefdd8785586bf8fb309684b654a7
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76800065"
---
# <a name="timelines-in-a-cloud-adoption-plan"></a>Tids linjer i en moln implementerings plan

I föregående artikel i den här serien tilldelade arbets belastningar och uppgifter till [versioner och iterationer](./iteration-paths.md). Tilldelningarna kommer att matas in i beräkningen av tids linjen i den här artikeln.

Arbets struktur strukturer används ofta i sekventiella projekt hanterings verktyg. De visar hur beroende aktiviteter kommer att slutföras över tid. Dessa strukturer fungerar bra när uppgifter är sekventiella av typen. Beroenden i aktiviteter som påträffades i moln implementeringen gör det svårt att hantera dessa strukturer. För att kunna fylla i detta mellanrum kan du uppskatta tids linjer baserat på iteration-vägs tilldelningar genom att dölja komplexitet.

## <a name="estimate-timelines"></a>Uppskatta tidslinjer

Börja med versioner för att utveckla en tids linje. De här lanserings målen skapar ett mål datum för eventuell företags påverkan. Iterationer ger stöd för att justera dessa versioner med angivna tids perioder.

Om mer detaljerade mil stolpar krävs i tids linjen använder du upprepnings tilldelning för att indikera mil stolpar. Om du vill utföra den här tilldelningen antar du att den sista instansen av en arbets belastnings åtgärd kan fungera som den sista mil stolpen. Teamen brukar också tagga den sista uppgiften som en mil stolpe.

Använd den sista dagen i upprepningen som datum för varje mil stolpe för alla nivåer av granularitet. Detta kopplar slut på arbets belastnings införande till ett visst datum. Du kan spåra datumet i ett kalkyl blad eller ett sekventiellt projekt hanterings verktyg som Microsoft Project.

## <a name="delivery-plans-in-azure-devops"></a>Leverans planer i Azure DevOps

Om du använder Azure DevOps för att hantera din implementerings plan för molnet kan du överväga att använda [Microsoft Delivery Plans](https://marketplace.visualstudio.com/items?itemName=ms.vss-plans) -tillägget. Det här tillägget kan snabbt skapa en visuell representation av tids linjen som baseras på iteration-och publicerings tilldelningar.
