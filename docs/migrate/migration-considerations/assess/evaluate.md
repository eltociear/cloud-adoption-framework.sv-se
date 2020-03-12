---
title: Utvärdera beredskap för arbetsbelastningar
description: Förstå vad som krävs för att utvärdera beredskap för en arbets belastning för att migrera till molnet. Du lär dig hur du verifierar alla till gångar och associerade beroenden.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 3065dfa39af189c5275f966e758fe49004f4de00
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79094773"
---
# <a name="evaluate-workload-readiness"></a>Utvärdera beredskap för arbetsbelastningar

Den här aktiviteten fokuserar på utvärdering av en arbetsbelastnings beredskap för att migreras till molnet. Under den här aktiviteten verifierar molnimplementeringsteamet alla tillgångar och associerade beroenden är kompatibla med den valda distributionsmodellen och molnleverantören. Under processen dokumenterar teamet allt arbete som krävs för att [reparera](../migrate/remediate.md) kompatibilitetsproblem.

## <a name="evaluation-assumptions"></a>Utvärderingsantaganden

De flesta av Contents-principerna i Cloud adoption Framework är Cloud oberoende. Processen för beredskapsutvärdering måste dock huvudsakligen gälla specifikt för varje enskild molnplattform. Följande vägledning förutsätter en avsikt att migrera till Azure. Den förutsätter även användning av Azure Migrate (som även kallas Azure Site Recovery) för [replikeringsaktiviteter](../migrate/replicate.md). Alternativa verktyg beskrivs i [replikeringsalternativ](../migrate/replicate-options.md).

Den här artikeln fångar inte alla möjliga utvärderings aktiviteter. Det förutsätts att varje miljö och affärsresultat avgör de specifika kraven. För att påskynda skapandet av dessa krav delar resten av den här artikeln några vanliga utvärderingsaktiviteter som rör utvärdering av [infrastruktur](#common-infrastructure-evaluation-activities), [databaser](#common-database-evaluation-activities) och [nätverk](#common-network-evaluation-activities).

## <a name="common-infrastructure-evaluation-activities"></a>Vanliga aktiviteter för utvärdering av infrastruktur

- VMware-krav: [granska Azure Site Recovery krav för VMware](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix).
- Krav för Hyper-V: [granska Azure Site Recoverys kraven för Hyper-v](https://docs.microsoft.com/azure/site-recovery/hyper-v-azure-support-matrix).

Se till att dokumentera eventuella skillnader i värdkonfiguration, konfiguration av replikerade virtuella datorer, lagringskrav eller nätverkskonfiguration.

## <a name="common-database-evaluation-activities"></a>Vanliga aktiviteter för utvärdering av databaser

- Dokumentera målen för återställningspunkt och målen för återställningstid för den aktuella databasdistributionen. Dessa används i [arkitekturaktiviteter](./architect.md) för att underlätta beslutsfattande.
- Dokumentera eventuella krav för konfiguration med hög tillgänglighet. Mer information om SQL Server-krav finns i [guiden för SQL Server-lösningar med hög tillgänglighet](https://docs.microsoft.com/sql/sql-server/failover-clusters/high-availability-solutions-sql-server).
- Utvärdera PaaS-kompatibilitet. [Azure Data Migration guide](https://datamigration.microsoft.com) mappar lokala databaser till kompatibla Azure PaaS-lösningar, t. ex. [Cosmos DB](https://docs.microsoft.com/azure/cosmos-db) eller [Azure DB](https://docs.microsoft.com/azure/sql-database) för [MySQL](https://docs.microsoft.com/azure/mysql), [postgresql](https://docs.microsoft.com/azure/postgresql)eller [MariaDB](https://docs.microsoft.com/azure/mariadb).
- När PaaS-kompatibilitet är en möjlighet utan att reparation krävs bör det team som ansvarar för [arkitekturaktiviteter](./architect.md) rådfrågas. PaaS-migreringar kan ge betydande tidsbesparingar och minska den totala ägandekostnaden (TCO) för de flesta molnlösningar.
- När PaaS-kompatibilitet är en möjlighet men reparation krävs bör de team som ansvarar för [arkitekturaktiviteter](./architect.md) och [reparationsaktiviteter](../migrate/remediate.md) rådfrågas. I många fall kan fördelarna med PaaS-migreringar för databaslösningar väga tyngre än ökningen av reparationstid.
- Dokumentera storleken och ändringsfrekvensen för varje databas som ska migreras.
- När det är möjligt bör alla program eller andra tillgångar som gör anrop till varje databas dokumenteras.

> [!NOTE]
> Synkronisering av tillgångar förbrukar bandbredd under replikeringsprocesserna. En mycket vanlig fälla är att förbise den bandbreddsåtgång som krävs för att hålla tillgångar synkroniserade mellan replikeringen och lanseringen. Databaser är ofta förekommande konsumenter av bandbredd under lanseringscykler, och databaser med stort lagringsutnyttjande eller en hög ändringsfrekvens är särskilt problematiska. Överväg en metod för replikering av datastrukturen med kontrollerade uppdateringar före acceptanstest för användare (UAT) och lansering. I sådana scenarier kan alternativ till Azure Site Recovery vara mer lämpliga. Mer information finns i vägledningen i [guiden för Azure-datamigrering](https://datamigration.microsoft.com).

## <a name="common-network-evaluation-activities"></a>Vanliga aktiviteter för utvärdering av nätverk

- Beräkna den totala lagringen för alla virtuella datorer som ska replikeras under de iterationer som upprepningarna som leder fram till en lansering.
- Beräkna förskjutning eller ändringstakten för lagring för alla virtuella datorer som ska replikeras under de iterationer som upprepningarna som leder fram till en lansering.
- Beräkna de bandbreddskrav som behövs för varje iteration genom att summera total lagring och förskjutning.
- Beräkna oanvänd bandbredd som är tillgänglig i det aktuella nätverket för att validera justering per iteration.
- Dokumentera den bandbredd som krävs för att uppnå förväntad migreringshastighet. Om reparation krävs för att tillhandahålla nödvändig bandbredd ska du meddela det team som ansvarar för [reparationsaktiviteter](../migrate/remediate.md).

> [!NOTE]
> Total lagring påverkar direkt bandbreddskraven under den inledande replikeringen. Lagringsförskjutning fortsätter dock från replikeringen fram till lansering. Det innebär att förskjutning har en kumulativ inverkan på den tillgängliga bandbredden.

## <a name="next-steps"></a>Nästa steg

När utvärderingen av ett system är klar driver resultatet utvecklingen av en ny [molnarkitektur.](./architect.md)

> [!div class="nextstepaction"]
> [Konstruera arbetsbelastningar före migrering](./architect.md)
