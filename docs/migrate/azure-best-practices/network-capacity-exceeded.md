---
title: Nätverkskapaciteten har överskridits
description: Data kraven överskrider nätverks kapaciteten under en migrering.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 5c410527182d7185a052bc99826ea06154fdae5f
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80429638"
---
<!-- cSpell:ignore HDFS databox VHDX -->

# <a name="data-requirements-exceed-network-capacity-during-a-migration-effort"></a>Data kraven överskrider nätverks kapaciteten under en migrering

Under en molnmigrering replikeras och synkroniseras tillgångar över nätverket mellan det befintliga datacentret och molnet. Det är inte ovanligt att datakraven för olika arbetsbelastningar överskrider nätverkskapaciteten. Om så är fallet kan migreringen gå mycket långsammare eller i vissa fall stoppas helt. Följande riktlinjer utökar [migrationsguiden för Azure](../azure-migration-guide/index.md) med en lösning som kringgår nätverksbegränsningar.

## <a name="general-scope-expansion"></a>Allmän omfångsutökning

Det mesta av arbetet som krävs för denna utökning sker under förutsättnings-, utvärderings- och migreringsprocesserna för migreringen.

## <a name="suggested-prerequisites"></a>Föreslagna förutsättningar

**Verifiera nätverks kapacitets risker:** [digital egendom rationalisering](../../digital-estate/rationalize.md) är ett starkt rekommenderat krav, särskilt om det rör sig om överbelastning av den tillgängliga nätverks kapaciteten. Under en rationalisering av digital egendom görs en [inventering av digitala tillgångar](../../digital-estate/inventory.md). Inventeringen ska inkludera befintliga lagringsbehov över den digitala egendomen. Som beskrivs i [replikerings risker: fysik över replikeringen](../migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication)kan användas för att uppskatta **Total storlek för migrering**, som kan jämföras med den totala **tillgängliga bandbredden för migrering**. Om denna jämförelse inte faller inom den **tid till verksamhetsförändring** som krävs kan denna artikel hjälpa till att öka migreringshastigheten och minska den tid som krävs för att migrera datacentret.

**Offline-överföring av oberoende data lager:** Bilden i diagrammet nedan är exempel på data överföringar online och offline med Azure Data Box. Dessa metoder kan användas för att överföra stora datavolymer till molnet innan migreringen av arbetsbelastningen. Vid en offline-dataöverföring kopieras källdata till Azure Data Box, som sedan skickas fysiskt till Microsoft för överföring till ett Azure storage-konto som en fil eller blob. Denna process kan användas för att överföra data som inte hör direkt till en viss arbetsbelastning innan migreringen sker. Det minskar mängden data som behöver överföras över nätverket för att kunna genomföra migreringen med de tillgängliga nätverksresurserna.

Den här metoden kan användas för att överföra data från HDFS, säkerhets kopior, arkiv, fil servrar och program. Befintlig teknisk vägledning förklarar hur du använder denna metod för att överföra data från [ett HDFS-lager](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) eller från diskar med [SMB](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data), [NFS](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-nfs), [REST](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-rest) eller en [datakopieringstjänst](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-copy-service) till Data Box.

Det finns även [lösningar från tredje part](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box) som använder Azure Data Box för en typ av migrering där stora datavolymer överförs offline och sedan synkroniseras över nätverket.

![Dataöverföring offline och online med Azure Data Box](../../_images/migrate/databox.png)

## <a name="assess-process-changes"></a>Utvärdera processändringar

Om lagringsbehovet för en arbetsbelastning (eller flera arbetsbelastningar) överskrider nätverkskapaciteten kan Azure Data Box fortfarande användas vid en dataöverföring offline.

Nätverks överföring är den rekommenderade metoden om inte nätverket är tillgängligt. Hastigheten för överföring av data över nätverket, även om bandbredden är begränsad, är vanligt vis snabbare än att fysiskt leverera samma mängd data med hjälp av en mekanism för offline-överföring, till exempel Data Box-enhet.

Om anslutning till Azure är tillgänglig ska en analys genomföras innan Data Box används, särskilt om migreringen av arbetsbelastningen är tidskänslig. Data Box rekommenderas bara när tiden för att överföra nödvändiga data överskrider tiden för att läsa in, transportera och återställa data med Data Box.

### <a name="suggested-action-during-the-assess-process"></a>Föreslagna åtgärder under utvärderingsprocessen

**Analys av nätverks kapacitet:** När krav på arbets belastnings data överföring är utsatta för att överskrida nätverks kapaciteten skulle moln antagande teamet lägga till en ytterligare analys aktivitet i utvärderings processen, som kallas analys av nätverks kapacitet. Under denna analys uppskattar en medlem i teamet med ämneskunskaper om det lokala nätverket och nätverksanslutningen den tillgängliga nätverkskapaciteten och den dataöverföringstid som krävs. Den tillgängliga kapaciteten jämförs med lagringskraven för alla tillgångar som ska migreras för den aktuella versionen. Om lagringskraven överskrider tillgänglig bandbredd överförs de tillgångar som understödjer arbetsbelastningen med offline-överföring.

> [!IMPORTANT]
> Efter analysen kan versionsplanen behöva uppdateras för att spegla den tid som krävs för att transportera, återställa och synkronisera de tillgångar som ska överföras offline.

**Avvikelse analys:** Varje till gång som ska överföras offline bör analyseras för lagrings-och konfigurations avvikelser. Lagringsavvikelse är mängden förändring i den underliggande lagringen över tid. Konfigurationsavvikelse är konfigurationsförändringar hos tillgången över tid. Från tiden lagringen kopieras till den tid då tillgången befordras till produktion kan avvikelser förloras. Om dessa avvikelser måste speglas i den migrerade tillgången behövs någon form av synkronisering mellan den lokala tillgången och den migrerade tillgången. Detta bör flaggas för analys vid utförande av migreringen.

## <a name="migrate-process-changes"></a>Migrering av processändringar

Vid användning av överföring offline krävs oftast inte [replikeringsprocesser](../migration-considerations/migrate/replicate.md). [Synkroniseringsprocesser](../migration-considerations/migrate/replicate.md) kan dock fortfarande vara nödvändiga. Genom att förstå resultaten från den avvikelseanalys som genomförs under utvärderingsprocessen kan åtgärderna vid migreringen anpassas om en tillgång överförs offline.

### <a name="suggested-action-during-the-migrate-process"></a>Föreslagna åtgärder under migreringsprocessen

**Kopierings lagring:** Den här metoden kan användas för att överföra data från HDFS, säkerhets kopior, arkiv, fil servrar eller program. Befintlig teknisk vägledning förklarar hur du använder denna metod för att överföra data från [ett HDFS-lager](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) eller från diskar med [SMB](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data), [NFS](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-nfs), [REST](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-rest) eller en [datakopieringstjänst](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-copy-service) till Data Box.

Det finns även [lösningar från tredje part](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box) som använder Azure Data Box för en typ av migrering där stora datavolymer överförs offline och sedan synkroniseras över nätverket.

**Leverera enheten:** När data har kopierats kan enheten [levereras till Microsoft](https://docs.microsoft.com/azure/databox/data-box-deploy-picked-up). När det tagits emot och importerats är data tillgängliga i ett Azure storage-konto.

**Återställa till gången:** [kontrol lera att data](https://docs.microsoft.com/azure/databox/data-box-deploy-picked-up#verify-data-upload-to-azure) är tillgängliga i lagrings kontot. När det kontrollerats kan data användas som en blob eller i Azure Files. Om data är i en VHD/VHDX-fil kan filen omvandlas till hanterade diskar. Dessa hanterade diskar kan sedan användas för att skapa en instans av en virtuell dator vilket skapar en kopia av den ursprungliga lokalt installerade tillgången.

**Synkronisering:** Om synkronisering av drivgarn är ett krav för en migrerad till gång, kan en av [partner lösningarna från tredje part](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box) användas för att synkronisera filerna tills till gången återställs.

## <a name="optimize-and-promote-process-changes"></a>Optimera och höja upp processändringar

Optimeringsaktiviteterna påverkas troligen inte av denna förändring i omfattning.

## <a name="secure-and-manage-process-changes"></a>Skydda och hantera processändringar

Aktiviteterna för att skydda och hantera påverkas troligen inte av denna förändring i omfattning.

## <a name="next-steps"></a>Nästa steg

Gå tillbaka till [checklistan för utökat omfång](./index.md) och se till att din migreringsmetod är helt anpassad till kraven.

> [!div class="nextstepaction"]
> [Utökad checklista](./index.md)
