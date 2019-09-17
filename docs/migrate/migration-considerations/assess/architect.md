---
title: Beräkna arbetsbelastningar före migrering
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Beräkna arbetsbelastningar före migrering
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: d62b2f5957dc5cee19f462e3c7d74c85672eadfe
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70819509"
---
# <a name="architect-workloads-prior-to-migration"></a>Beräkna arbetsbelastningar före migrering

Denna artikel utökar utvärderingsprocessen genom att granska aktiviteter som är relaterade till att definiera arkitekturen för en arbetsbelastning i en viss iteration. Som diskuterats i artikeln om [inkrementell rationalisering](../../../digital-estate/rationalize.md) görs en del arkitekturrelaterade antaganden under alla verksamhetsförändringar som kräver en migrering. Denna artikel förtydligar dessa antaganden, nämner en del hinder som kan undvikas och identifierar möjligheter att snabbare uppnå affärsvärde genom att utmana dessa antaganden. Denna inkrementella modell för arkitektur gör att team kan arbeta snabbare och nå affärsmål tidigare.

## <a name="architecture-assumptions-prior-to-migration"></a>Arkitekturantaganden innan migrering

Följande arkitekturantaganden är typiska för alla migreringar:

- **IaaS.** Det antas normalt att migrering av arbetsbelastningar i huvudsak består av förflyttning av virtuella maskiner från ett fysiskt datacenter till ett molndatacenter via en IaaS-migrering, vilket kräver minsta möjliga utveckling och omkonfiguration. Detta är känt som en Lift and shift-migrering. (Undantag nedan.)
- **Arkitekturkonsekvens.** Ändringar av grundläggande arkitektur under en migrering ökar i hög grad komplexiteten. Felsökning av ett ändrat system på en ny plattform inför många variabler som kan vara svåra att isolera. Av detta skäl ska arbetsbelastningar bara genomgå smärre förändringar under migrering och alla ändringar ska testas noggrant.
- **Indragningstest.** Migreringar och att vara värd för tillgångar förbrukar driftskostnader och potentiella kapitalutgifter. Det antas att alla arbetsbelastningar som migreras har granskats för att validera fortsatt användning. Att kunna dra in oanvända tillgångar ger omedelbara kostnadsbesparingar.
- **Storleksförändra tillgångar.** Det antas att få lokala tillgångar fullt ut använder de tilldelade resurserna. Innan migrering antas det att storleken på tillgångar kommer att anpassas för att bäst passa verklig användning.
- **Krav på affärskontinuitet och haveriberedskap (BCDR).** Det antas att ett serviceavtal för arbetsbelastningen förhandlats fram med företaget innan planering för frisläppande. Dessa krav leder antagligen till mindre arkitekturförändringar.
- **Stilleståndstid vid migrering.** Även stilleståndstid för att överföra arbetsbelastningen till produktion kan påverka verksamheten negativt. Ibland kan lösningar som måste komma i drift med minimal stilleståndstid kräva arkitekturändringar. Det antas att en allmän överenskommelse vad gäller kraven för stilleståndstid har upprättats innan planering för frisläppande.

## <a name="roadblocks-that-can-be-avoided"></a>Hinder som kan undvikas

De antaganden som beskrivits kan skapa hinder som kan sakta ner framsteg eller orsaka problem längre fram. Det här är några hinder att se upp med innan frisläppandet:

- **Betala tekniska skulder.** En del äldre arbetsbelastningar har en hög nivå av teknisk skuld. Detta kan leda till långvariga utmaningar genom att öka värdkostnaden oavsett molnleverantör. När teknisk skuld på ett onaturligt sätt ökar värdkostnaderna ska alternativa arkitekturer utvärderas.
- **Mönster för användartrafik.** Befintliga lösningar kan vara avhängiga av befintliga routingmönster. Dessa mönster kan allvarligt påverka prestanda. Dessutom kan införande av nya lösningar som bygger på hybrid-WAN ta veckor eller till och med månader. Förbered för dessa hinder tidigt i arkitekturprocessen genom att ta hänsyn till trafikmönster och ändringar i grundläggande infrastrukturtjänster.

## <a name="accelerating-business-value"></a>Skapa affärsvärde snabbare

En del scenarion kan kräva en annan arkitektur än den IaaS-strategi med byte av värd som förutsatts. Detta är några exempel:

- PaaS-alternativ. PaaS kan minska värdkostnader samt den tid som krävs för att migrera vissa arbetsbelastningar. En lista med tillvägagångssätt som kan dra fördel av en PaaS-konvertering finns i artikeln [utvärdera tillgångar](./evaluate.md).
- Skriptat införande/DevOps. Om en arbetsbelastning har en befintlig DevOps-installation eller andra former av skriptat införande kan kostnaden för att ändra dessa skript vara lägre än för att migrera tillgången.
- Avhjälpningsåtgärder. De avhjälpningsåtgärder som krävs för att förbereda en arbetsbelastning för migrering kan vara omfattande. I vissa fall är det bättre att modernisera lösningen än att avhjälpa underliggande kompatibilitetsproblem.

I alla dessa scenarion kan en alternativ arkitektur vara den bästa lösningen.

## <a name="next-steps"></a>Nästa steg

När den nya arkitekturen definierats kan [korrekta kostnadsberäkningar göras](./estimate.md).

> [!div class="nextstepaction"]
> [Beräkna molnkostnader](./estimate.md)