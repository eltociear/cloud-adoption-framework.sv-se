---
title: Inaktivera tillbakadragna tillgångar
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Inaktivera tillbakadragna tillgångar
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: ae2538263af35e8fdb2cf5c861a2c7b0537108d4
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833367"
---
# <a name="decommission-retired-assets"></a>Inaktivera tillbakadragna tillgångar

När en arbetsbelastning upphöjs till produktion behövs inte längre de tillgångar som tidigare värdhanterade produktionsarbetsbelastningen för att stödja affärsverksamheten. Vid det laget anses äldre tillgångar vara tillbakadragna. Tillbakadragna tillgångar kan sedan tas ur bruk, vilket minskar driftskostnaderna. Att ta en resurs ur bruk kan vara så enkelt som att stänga av strömmen till tillgången och kassera den på ett ansvarsfullt sätt. Tyvärr kan inaktivering av resurser ibland medföra oönskade konsekvenser. Följande vägledning kan hjälpa till med korrekt inaktivering av tillbakadragna resurser med minimal störning i verksamheten.

## <a name="cost-savings-realization"></a>Realisering av kostnadsbesparingar

När kostnadsbesparingar är det främsta skälet till en migrering är inaktivering ett viktigt steg. Tills en tillgång är inaktiverad fortsätter den att förbruka ström, miljöstöd och andra resurser som ökar kostnaderna. När tillgången har inaktiverats kan kostnadsbesparingarna börja realiseras.

## <a name="continued-monitoring"></a>Fortsatt övervakning

När en migrerad arbetsbelastning upphöjs bör de tillgångar som dras tillbaka fortsätta att övervakas för att kontrollera att ingen ytterligare produktionstrafik dirigeras till fel tillgångar.

## <a name="testing-windows-and-dependency-validation"></a>Testningsfönster och beroendevalidering

Även med den bästa planeringen kan produktionsarbetsbelastningar fortfarande innehålla beroenden av tillgångar som förmodas vara tillbakadragna. I sådana fall kan inaktivering av en tillbakadragen tillgång orsaka oväntade systemfel. Därför bör avslutningen av alla tillgångar ske på samma robusta sätt som en aktivitet för systemunderhåll. Korrekta testnings- och avbrottsfönster för upprättas för att medge avslutningen av resursen.

## <a name="holding-period-and-data-validation"></a>Kvarhållningsperiod och dataverifiering

Det är inte ovanligt att migreringar missar data under replikeringsprocesser. Detta gäller särskilt för äldre data som inte används regelbundet. När en tillbakadragen tillgång har inaktiverats är det fortfarande klokt att underhålla tillgången under en period som tillfällig säkerhetskopia av data. Företag bör avsätta minst 30 dagar för kvarhållning och testning innan tillbakadragna tillgångar destrueras.

## <a name="next-steps"></a>Nästa steg

När tillbakadragna tillgångar tas ur bruk är migreringen klar. Detta ger en bra möjlighet att förbättra migreringsprocessen, och en [återblick](./retrospective.md) gör att molnimplementeringsteamet kan granska lanseringen i syfte att lära sig och förbättra processen.

> [!div class="nextstepaction"]
> [Återblick](./retrospective.md)
