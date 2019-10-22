---
title: 'Utveckling av molnet: data migration service'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Cloud innovation – data migration service
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: c75efe3576bb61ecb116ab22e4946b8d87da3d4a
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683425"
---
# <a name="collect-data-through-the-migration-and-modernization-of-existing-data-sources"></a>Samla in data genom migreringen och modernisering av befintliga data källor

Företag har ofta en mängd olika befintliga data som kan vara [democratized](../considerations/data.md). När kunden hypotesen kräver att befintliga data används för att skapa moderna lösningar kan ett första steg vara migreringen och modernisering av data för att förbereda för uppfinningar och innovationer. För att justera med befintliga migreringar inom en moln implementerings plan kan migreringen och modernisering enklare utföras inom [migreringen](../../migrate/index.md).

## <a name="use-of-this-article"></a>Användning av den här artikeln

Den här artikeln beskriver en serie metoder som överensstämmer med migreringen, men som är bäst justerade till standard-verktygskedjan. Under utvärderings processen inom migreringen skulle moln implementerings teamet bedöma det aktuella läget och vill att det ska gå att migrera till gångens framtida tillstånd. När processen är en del av en Innovations ansträngning kan både moln implementerings teamen använda den här artikeln för att fatta beslut.

## <a name="primary-toolset"></a>Primära verktyg

När du migrerar och bevarar data som är aktuella på lokal, är det vanligaste valet av Azure-verktyg den [data migration service (DMS)](https://docs.microsoft.com/azure/dms) som är en del av den bredare [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) verktygskedjan. För befintliga SQL Server data källor kan [Data Migration Assistant (DMA)](/sql/dma/dma-overview) också hjälpa till med att utvärdera och migrera ett mindre antal data strukturer.

För att stödja Oracle-och NoSQL-migreringar kan du även använda [data migration service (DMS)](https://docs.microsoft.com/azure/dms) för vissa typer av källa till mål databaser, till exempel Oracle till postgresql eller MongoDB för att Cosmos dB. Det är vanligare för att kunna använda verktyg från tredje part eller anpassade migreringsjobb för att migrera till Cosmos DB-, HDInsight-eller IaaS-baserade VM-alternativ.

## <a name="considerations-and-guidance"></a>Överväganden och vägledning

När du använder DMS för migrering och modernisering av data är det viktigt att förstå den aktuella plattformen för att vara värd för data (källa), version och den framtida plattform och version som bäst stöder kund hypotesen (målet). Följande är en lista över käll-och mål par som kan granskas med migration-teamet. Varje inkluderar ett verktygs val och en länk till en guide som baseras på dessa överväganden.

**Migrera typ:** Med en offline-migrering startar Application nedtid när migreringen startar. Med onlinemigrering begränsas det frånkopplade tillståndet till tiden för att genomföra snabb migrering vid slutet av migreringen. Vi rekommenderar att du förstår vad som är acceptabelt för drift avbrott och testar en offline-migrering för att fastställa om återställnings tiden uppfyller detta. om inte, gör du en online-migrering.

|Källa  |Målinrikta  |Verktyg  |Typ av migrering  |Vägledning  |
|---------|---------|---------|---------|---------|
|SQL Server|Azure SQL Database|DMS|Anslutningen|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|SQL Server|Azure SQL Database|DMS|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|SQL Server|Azure SQL Database Managed Instance|DMS|Anslutningen|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|SQL Server|Azure SQL Database Managed Instance|DMS|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|RDS-SQL Server|Azure SQL Database (eller hanterad instans)|DMS|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|
|MySQL|Azure-databas för MySQL|DMS|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online)|
|PostgreSQL|Azure-databas för PostgreSQL|DMS|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online)|
|MondoDB|Azure Cosmos DB Mongo-API|DMS|Anslutningen|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db)|
|MongoDB|Azure Cosmos DB Mongo-API|DMS|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db-online)|
|Oracle|PaaS & IaaS alternativ|Tredje part eller Azure Migrate|Önskade|[Besluts träd](../../migrate/expanded-scope/data-oracle-migration.md)|
|Olika NoSQL-databaser|Alternativ för Cosmo DB eller IaaS|Stegvisa migreringar eller Azure Migrate|Önskade|[Besluts träd](../../migrate/expanded-scope/data-no-sql-migration.md)|
