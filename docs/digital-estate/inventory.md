---
title: Samla in inventerings data för en digital egendom
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Så här samlar du in inventering för en digital egendom.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 5ecf69235c27fbb45ad109609d8fd733dfc6187c
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753282"
---
# <a name="gather-inventory-data-for-a-digital-estate"></a>Samla in inventerings data för en digital egendom

Det första steget i [planeringen av digital auktion](./index.md)är att utveckla en inventering. I den här processen samlas en lista över IT-tillgångar som stöder specifika affärs funktioner för senare analys-och rationalisering. Den här artikeln förutsätter att en nedrullningsbar metod för analys är lämpligast för planering. Mer information finns i [metoder för planering av digital auktion](./approach.md).

## <a name="take-inventory-of-a-digital-estate"></a>Ta förteckningen över en digital egendom

Det lager som stöder en digital egendom ändras beroende på önskad digital omvandling och motsvarande omvandlings resa.

- **Molnbaserad migrering:**  Vi rekommenderar ofta att du under en molnbaserad migrering samlar in inventeringen från genomsöknings verktyg som skapar en centraliserad lista över alla virtuella datorer och servrar. Vissa verktyg kan också skapa nätverks mappningar och beroenden som hjälper dig att definiera arbets belastnings justering.

- **Program innovation:** Inventering under en molnbaserad program Innovations ansträngning börjar med kunden. Det är en bra plats att börja med att mappa kund upplevelsen från början till slut. Genom att justera mappningen till program, API: er, data och andra till gångar skapas en detaljerad inventering för analys.

- **Data innovation:** Cloud-aktiverade data innovation fokuserar på produkten eller tjänsten. En inventering innehåller också en mappning av möjligheterna för att störa marknaden samt de funktioner som behövs.

- **Säkerhet:** Inventering ger säkerhet för att hjälpa till att utvärdera, skydda och övervaka organisationens till gångar.

## <a name="accuracy-and-completeness-of-an-inventory"></a>En inventerings precision och fullständighet

En inventering är sällan slutförd i den första iterationen. Vi rekommenderar starkt att moln strategi teamet justerar intressenter och privilegierade användare att validera inventeringen. När det är möjligt kan du använda ytterligare verktyg som nätverks-och beroende analyser för att identifiera till gångar som skickas till trafik, men som inte finns i inventeringen.

## <a name="next-steps"></a>Nästa steg

När en inventering har kompilerats och verifierats kan det vara rationellt. Inventory rationalisering är nästa steg till planeringen av digital auktion.

> [!div class="nextstepaction"]
> [Rationalisera digital egendom](./rationalize.md)
