---
title: Nätverkskapaciteten har överskridits
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lagringskraven överskrider nätverkskapaciteten under ett migreringsprojekt.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 9b1078cbb6b7ca40b7a38ea56ae803fd61e67449
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024754"
---
# <a name="storage-requirements-exceed-network-capacity-during-a-migration-effort"></a>Lagringskraven överskrider nätverkskapaciteten under ett migreringsprojekt

Under en molnmigrering replikeras och synkroniseras tillgångar över nätverket mellan det befintliga datacentret och molnet. Det är inte ovanligt att datakraven för olika arbetsbelastningar överskrider nätverkskapaciteten. Om så är fallet kan migreringen gå mycket långsammare eller i vissa fall stoppas helt. Följande riktlinjer utökar [migrationsguiden för Azure](../azure-migration-guide/index.md) med en lösning som kringgår nätverksbegränsningar.

## <a name="general-scope-expansion"></a>Allmän omfångsutökning

Det mesta av arbetet som krävs för denna utökning sker under förutsättnings-, utvärderings- och migreringsprocesserna för migreringen.

## <a name="suggested-prerequisites"></a>Föreslagna förutsättningar

**Validera risker för nätverkskapacitet:** [Rationalisering av digital egendom](../../digital-estate/rationalize.md) rekommenderas starkt som en förutsättning, särskilt om det finns en möjlighet att den tillgängliga nätverkskapaciteten inte kommer att räcka till. Under en rationalisering av digital egendom görs en [inventering av digitala tillgångar](../../digital-estate/inventory.md). Inventeringen ska inkludera befintliga lagringsbehov över den digitala egendomen. Som beskrivet i [replikeringsrisker: Hur replikering fungerar](../migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication), kan denna inventering användas för att uppskatta **total datastorlek för migrering** som sedan kan jämföras med total **tillgänglig bandbredd för migrering**. Om denna jämförelse inte faller inom den **tid till verksamhetsförändring** som krävs kan denna artikel hjälpa till att öka migreringshastigheten och minska den tid som krävs för att migrera datacentret.

**Offline-överföring av oberoende datalager:** I diagrammet nedan visas exempel på dataöverföring online och offline med Azure Data Box. Dessa metoder kan användas för att överföra stora datavolymer till molnet innan migreringen av arbetsbelastningen. Vid en offline-dataöverföring kopieras källdata till Azure Data Box, som sedan skickas fysiskt till Microsoft för överföring till ett Azure storage-konto som en fil eller blob. Denna process kan användas för att överföra data som inte hör direkt till en viss arbetsbelastning innan migreringen sker. Det minskar mängden data som behöver överföras över nätverket för att kunna genomföra migreringen med de tillgängliga nätverksresurserna.

Denna metod kan användas för att överfara data-HDFS, säkerhetskopior, arkiv, filservrar, program osv. Befintlig teknisk vägledning förklarar hur du använder denna metod för att överföra data från [ett HDFS-lager](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) eller från diskar med [SMB](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data), [NFS](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-nfs), [REST](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-rest) eller en [datakopieringstjänst](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-copy-service) till Data Box.

Det finns även [lösningar från tredje part](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box) som använder Azure Data Box för en typ av migrering där stora datavolymer överförs offline och sedan synkroniseras över nätverket.

![Dataöverföring offline och online med Azure Data Box](../../_images/migrate/databox.png)

## <a name="assess-process-changes"></a>Utvärdera ändringar i processen

Om lagringsbehovet för en arbetsbelastning (eller flera arbetsbelastningar) överskrider nätverkskapaciteten kan Azure Data Box fortfarande användas vid en dataöverföring offline.

Microsofts inställning är att nätverksöverföring är det rekommenderade alternativet, om inte nätverket är otillgängligt. Detta förslag bygger på överföringshastigheten. Att överföra data via nätverket (även när bandbredden är begränsad) är normalt snabbare än att fysiskt överföra samma mängd data med en offline-metod, som Data Box.

Om anslutning till Azure är tillgänglig ska en analys genomföras innan Data Box används, särskilt om migreringen av arbetsbelastningen är tidskänslig. Data Box rekommenderas bara när tiden för att överföra nödvändiga data överskrider tiden för att läsa in, transportera och återställa data med Data Box.

### <a name="suggested-action-during-the-assess-process"></a>Föreslagna åtgärder under utvärderingsprocessen

**Analys av nätverkskapacitet:** När behoven av nätverksöverföring för en arbetsbelastning riskerar att överskrida nätverkskapaciteten lägger teamet för molnmigrering till ytterligare en analysuppgift som kallas nätverkskapacitetsanalys till utvärderingsprocessen. Under denna analys uppskattar en medlem i teamet med ämneskunskaper om det lokala nätverket och nätverksanslutningen den tillgängliga nätverkskapaciteten och den dataöverföringstid som krävs. Den tillgängliga kapaciteten jämförs med lagringskraven för alla tillgångar som ska migreras för den aktuella versionen. Om lagringskraven överskrider tillgänglig bandbredd överförs de tillgångar som understödjer arbetsbelastningen med offline-överföring.

> [!IMPORTANT]
> Efter analysen kan versionsplanen behöva uppdateras för att spegla den tid som krävs för att transportera, återställa och synkronisera de tillgångar som ska överföras offline.

**Avvikelseanalys:** Alla tillgångar som ska överföras offline ska analyseras för avvikelser i konfiguration och lagring. Lagringsavvikelse är mängden förändring i den underliggande lagringen över tid. Konfigurationsavvikelse är konfigurationsförändringar hos tillgången över tid. Från tiden lagringen kopieras till den tid då tillgången befordras till produktion kan avvikelser förloras. Om dessa avvikelser måste speglas i den migrerade tillgången behövs någon form av synkronisering mellan den lokala tillgången och den migrerade tillgången. Detta bör flaggas för analys vid utförande av migreringen.

## <a name="migrate-process-changes"></a>Migrering av processändringar

Vid användning av överföring offline krävs oftast inte [replikeringsprocesser](../migration-considerations/migrate/replicate.md). [Synkroniseringsprocesser](../migration-considerations/migrate/replicate.md) kan dock fortfarande vara nödvändiga. Genom att förstå resultaten från den avvikelseanalys som genomförs under utvärderingsprocessen kan åtgärderna vid migreringen anpassas om en tillgång överförs offline.

### <a name="suggested-action-during-the-migrate-process"></a>Föreslagna åtgärder under migreringsprocessen

**Kopiera lagring:** Denna metod kan användas för att överfara data-HDFS, säkerhetskopior, arkiv, filservrar, program osv. Befintlig teknisk vägledning förklarar hur du använder denna metod för att överföra data från [ett HDFS-lager](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) eller från diskar med [SMB](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data), [NFS](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-nfs), [REST](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-rest) eller en [datakopieringstjänst](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-copy-service) till Data Box.

Det finns även [lösningar från tredje part](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box) som använder Azure Data Box för en typ av migrering där stora datavolymer överförs offline och sedan synkroniseras över nätverket.

**Transportera enheten:** När data kopierats kan enheten [levereras till Microsoft](https://docs.microsoft.com/azure/databox/data-box-deploy-picked-up). När det tagits emot och importerats är data tillgängliga i ett Azure storage-konto.

**Återställa tillgången:** [Kontrollera att data](https://docs.microsoft.com/azure/databox/data-box-deploy-picked-up#verify-data-upload-to-azure) är tillgängliga i lagringskontot. När det kontrollerats kan data användas som en blob eller i Azure Files. Om data är i en VHD/VHDX-fil kan filen omvandlas till hanterade diskar. Dessa hanterade diskar kan sedan användas för att skapa en instans av en virtuell dator vilket skapar en kopia av den ursprungliga lokalt installerade tillgången.

**Synkronisering:** Om synkronisering av avvikelser krävs för en migrerad tillgång kan en av [lösningarna från tredje part](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box) användas för att synkronisera filerna tills tillgången återställs.

## <a name="optimize-and-promote-process-changes"></a>Optimera och flytta upp processändringar

Optimeringsaktiviteterna påverkas troligen inte av denna förändring i omfattning.

## <a name="secure-and-manage-process-changes"></a>Skydda och hantera processändringar

Aktiviteterna för att skydda och hantera påverkas troligen inte av denna förändring i omfattning.

## <a name="next-steps"></a>Nästa steg

Gå tillbaka till [checklistan för utökat omfång](./index.md) och se till att din migreringsmetod är helt anpassad till kraven.

> [!div class="nextstepaction"]
> [Checklista för utökat omfång](./index.md)
