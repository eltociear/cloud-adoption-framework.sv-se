---
title: Vilken roll spelar replikering och synkronisering under migreringsprocessen?
description: En process inom molnmigreringen som fokuserar på att överföra arbetsbelastningar till molnet.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 5eaea53e65951cb5fee3d36b2eba472e1048feb2
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78222268"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-role-does-replication-play-in-the-migration-process"></a>Vilken roll spelar replikering under migreringsprocessen?

Lokala datacenter är fulla med fysiska tillgångar såsom servrar, apparater och nätverksenheter. Varje server är dock bara ett fysiskt skal. Det verkliga värdet kommer från den binärkod som körs på servern. Programmen och data är syftet med datacentret. De är den primära binärkod som ska migreras. Bakom dessa program och datalager ligger andra digitala tillgångar och binära källor, till exempel operativsystem, nätverksvägar, filer och säkerhetsprotokoll.

Replikeringen är migreringens arbetshäst. Det är processen för att kopiera en tidpunktsversion av olika binärkod. De binära ögonblicksbilderna kopieras sedan till en ny plattform och distribueras till ny maskinvara i en process som kallas *seeding*. När den seedade kopian av binärkoden körs korrekt bör den bete sig identiskt med den ursprungliga binärkoden på den gamla maskinvaran. Dock är den ögonblicksbilden av binärkoden omedelbart inaktuell och feljusterad med den ursprungliga källan. För att hålla den nya och den gamla binärkoden justerade uppdaterar en process som kallas *synkronisering* kontinuerligt den kopia som lagras på den nya plattformen. Synkroniseringen fortsätter tills tillgången upphöjs i enlighet med den valda upphöjningsmodellen. I det läget avbryts synkroniseringen.

## <a name="required-prerequisites-to-replication"></a>Nödvändiga förutsättningar för replikering

Före replikeringen måste den *nya plattformen* och maskinvaran förberedas för att ta emot de binära kopiorna. I artikeln om [krav](../prerequisites/index.md) beskrivs minimi kraven för miljön för att skapa en säker, robust plattform med hög prestanda för att ta emot de binära replikerna.

*Källbinärkoden* måste också förberedas för replikering och synkronisering. Artiklarna om utvärdering, arkitektur och reparation behandlar de åtgärder som krävs för att säkerställa att källbinärkoden är redo för replikering och synkronisering.

En *verktygskedja* som inriktas med den nya plattformen och binärkoden måste implementeras för att köra och hantera processerna för replikering och synkronisering. I artikeln om [replikeringsalternativ](./replicate-options.md) beskrivs olika verktyg som kan bidra till en migrering till Azure.

## <a name="replication-risks---physics-of-replication"></a>Replikeringsrisker – fysiken bakom replikering

Vid planering för replikeringen av en binär källa till en ny destination finns det några grundläggande lagar att noggrant beakta vid planering och utförande.

- **Ljusets hastighet.** Vid flytt av stora volymer med data är fiber fortfarande det snabbaste alternativet. Tyvärr sker överföringen i dessa kablar bara med två tredjedelar av ljusets hastighet. Det innebär att det inte finns någon metod för omedelbar eller obegränsad datareplikering.
- **Hastigheten för WAN-pipeline.** Mer sekventiella än hastigheten på data förflyttning är bandbredden för överordnad länk, som definierar data mängden per sekund som kan överföras till ett företags befintliga WAN till mål data centret.
- **Utökning av WAN-hastigheten.** Om det finns utrymme i budgeten kan ytterligare bandbredd läggas till i ett företags WAN-lösning. Det kan dock ta flera veckor eller månader att köpa, etablera och integrera ytterligare fiberanslutningar.
- **Hastigheten för diskar.** Även om data kunde flyttas snabbare och det inte hade funnits någon gräns för bandbredden mellan källbinärkoden och destinationen skulle fysiken ändå utgöra en begränsning. Data kan bara replikeras så fort de kan läsas från käll diskar. Det tar tid att läsa varje etta eller nolla från varje snurrande disk i ett datacenter.
- **Hastigheten för mänskliga beräkningar.** Diskar och ljus är snabbare än mänskliga beslutsprocesser. När en grupp människor måste samarbeta och fatta beslut tillsammans sker resultat ännu långsammare. Replikeringen kan aldrig förbigå fördröjningar som rör människors aktiviteter.

Var och en av dessa fysiklagar medför följande risker som ofta påverkar migreringsplaner:

- **Replikeringstid.** Avancerade replikeringsverktyg kan inte förbigå grundläggande fysiklagar – replikering kräver helt enkelt tid och bandbredd. Planer bör innehålla realistiska tidslinjer som återspeglar den tid det tar att replikera binärkod. *Total tillgänglig migreringsbandbredd* är den mängd uppgående bandbredd i megabit per sekund (Mbit/s) eller gigabit per sekund (Gbit/s) som inte används av andra affärsbehov med högre prioritet. *Total migreringslagring* är det totala diskutrymme i gigabyte eller terabyte som krävs för att lagra en ögonblicksbild av alla tillgångar som ska migreras. En inledande tidsuppskattning kan beräknas genom att den *totala migreringslagringen* delas med den *totala tillgängliga migreringsbandbredden*. Observera konverteringen från bitar till byte. En mer exakt beräkning av tiden finns i följande avsnitt, ”Kumulativ effekt av diskförskjutning”.
- **Kumulativ effekt av diskförskjutning.** Från replikering till upphöjning av en tillgång till produktion måste käll- och destinationsbinärkoden förbli synkroniserade. *Förskjutning* i binärkod förbrukar ytterligare bandbredd, eftersom alla ändringar i binärkoden måste replikeras regelbundet. Under synkroniseringen måste all binär förskjutning inkluderas i beräkningen för total migreringslagring. Ju längre tid det tar att höja upp en tillgång till produktion, desto mer kumulativ förskjutning sker det. Ju fler tillgångar som synkroniseras, desto mer bandbredd förbrukas. Varje tillgång som hålls i ett synkroniseringstillstånd gör att ytterligare en mängd av den totala tillgängliga migreringsbandbredden förbrukas.
- **Tid till verksamhetsändring.** Som det framgår i föregående avsnitt, ”Kumulativ effekt av diskförskjutning”, har synkroniseringstid en kumulativ negativ inverkan på migreringshastigheten. Prioritering av listan över kvarvarande uppgifter för migrering samt avancerade förberedelser inför [verksamhetsändringsplanen](../optimize/business-change-plan.md) är mycket viktiga vad gäller migreringshastigheten. Det viktigaste testet av överensstämmelse mellan verksamheten och tekniken under ett migreringsarbete är upphöjningstakten. Ju snabbare en tillgång kan upphöjas till produktion, desto mindre påverkar diskförskjutning bandbredden, och desto mer bandbredd/tid kan allokeras till replikeringen av nästa arbetsbelastning.

## <a name="next-steps"></a>Nästa steg

När replikeringen är klar kan [mellanlagringsaktiviteterna](./stage.md) påbörjas.

> [!div class="nextstepaction"]
> [Mellanlagringsaktiviteter under en migrering](./stage.md)
