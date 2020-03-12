---
title: Replikeringsalternativ
description: Använd ramverket för moln införande för Azure för att förstå den replikerade processen och varför du behöver replikering för migrering av molnet.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 790ef71ed6a3880b23a851adc0054666e16c0dde
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092843"
---
# <a name="replication-options"></a>Replikeringsalternativ

Innan du migrerar bör du se till att de primära systemen är säkra och kommer att fortsätta köras utan problem. Om det förekommer avbrottstid störs användare eller kunder, vilket kostar både tid och pengar. Det går inte att utföra migrering genom att bara stänga av de virtuella datorerna lokalt och kopiera dem till Azure. Migreringsverktyg måste ta hänsyn till asynkron eller synkron replikering för att säkerställa att system i drift kan kopieras till Azure utan avbrott. Viktigast av allt är att systemen måste vara helt synkroniserade med de lokala motsvarigheterna. Det kan vara bra att testa migrerade resurser i isolerade partitioner i Azure för att säkerställa att arbetsbelastningarna fungerar som väntat.

Innehållet i ramverket för molnimplementering förutsätter att Azure Migrate (eller Azure Site Recovery) är det lämpligaste verktyget för att replikera tillgångar till molnet. Det finns dock andra tillgängliga alternativ. I den här artikeln beskrivs de alternativen i syfte att underlätta beslutsfattande.

## <a name="azure-site-recovery-also-known-as-azure-migrate"></a>Azure Site Recovery (kallas även Azure Migrate)

[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) orkestrerar och hanterar haveriberedskap för virtuella Azure-datorer, lokala virtuella datorer och fysiska servrar. Du kan även använda Site Recovery för att hantera migrering av lokala datorer och sådana som finns hos andra molnleverantörer till Azure. Replikera lokala datorer till Azure eller virtuella Azure-datorer till en sekundär region. Sedan redundansväxlar du den virtuella datorn från den primära platsen till den sekundära och slutför migreringsprocessen. Med Azure Site Recovery kan du genomföra olika scenarier för migrering:

- **Migrera från lokal plats till Azure.** Migrera lokala virtuella VMware-datorer, virtuella Hyper-V-datorer samt fysiska servrar till Azure. Det gör du genom att utföra nästan samma steg som för fullständig haveriberedskap. Skillnaden är att du inte redundansväxlar datorer tillbaka från Azure till den lokala platsen.
- **Migrera mellan Azure-regioner.** Migrera virtuella Azure-datorer från en Azure-region till en annan. När migreringen är klar konfigurerar du haveriberedskap för de virtuella Azure-datorerna nu i den sekundära region som du migrerade till.
- **Migrera från ett annat moln till Azure.** Du kan migrera dina beräkningsinstanser som tillhandahålls hos andra molnleverantörer till virtuella Azure-datorer. Site Recovery behandlar de instanserna som fysiska servrar i migreringssyfte.

![Azure Site Recovery](../../../_images/migrate/asr-replication-image.png)
*Azure Site Recovery flytta tillgångar till Azure eller andra moln*

När du har utvärderat lokal och molnbaserad infrastruktur för migrering bidrar Azure Site Recovery till din migreringsstrategi genom att replikera lokala datorer. Med följande enkla steg kan du konfigurera migrering av lokala virtuella datorer, fysiska servrar och instanser av virtuella molndatorer till Azure:

- Kontrollera förutsättningarna.
- Förbereda Azure-resurser.
- Förbered instanser av lokala eller molnbaserade virtuella datorer för migrering.
- Distribuera en konfigurationsserver.
- Aktivera replikering för virtuella datorer.
- Testa redundansväxling för att kontrollera att allt fungerar.
- Köra en engångsredundansväxling till Azure.

## <a name="azure-database-migration-service"></a>Azure Database Migration Service

Den här tjänsten förenklar molnmigreringen genom att använda en enda omfattande tjänst i stället för flera olika verktyg. [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) är utformad som en smidig och komplett lösning för att flytta lokala SQL Server-databaser till molnet. Det är en fullständigt hanterad tjänst som gör att du kan migrera sömlöst från flera databaskällor till Azure-dataplattformar med minsta möjliga avbrottstid. Den integrerar några av funktionerna från befintliga verktyg och tjänster, vilket ger kunderna en omfattande lösning med hög tillgänglighet.

Tjänsten använder Data Migration Assistant för att skapa utvärderingsrapporter som ger rekommendationer som vägleder dig genom de ändringar som krävs innan du utför en migrering. Det är upp till dig att utföra eventuellt nödvändig reparation. När du är redo att påbörja migreringsprocessen utför Azure Database Migration Service alla tillhörande steg. Du kan tryggt starta och sedan glömma dina migreringsprojekt i vetskap om att processen sker enligt Microsofts bästa praxis.

## <a name="next-steps"></a>Nästa steg

När replikeringen är klar kan [mellanlagringsaktiviteterna](./stage.md) påbörjas.

> [!div class="nextstepaction"]
> [Mellanlagringsaktiviteter under en migrering](./stage.md)
