---
title: 'Moln innovation: Azure Database Migration Service'
description: Cloud innovation – Azure Database Migration Service
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 44ebe7e28eea56d1b7e61b5926a9588f4c985ae1
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808676"
---
# <a name="collect-data-through-the-migration-and-modernization-of-existing-data-sources"></a>Samla in data genom migreringen och modernisering av befintliga data källor

Företag har ofta olika typer av befintliga data som de kan [demokratisera identifieringen av](../considerations/data.md). När en kund hypotes kräver att befintliga data används för att skapa moderna lösningar kan ett första steg vara migreringen och modernisering av data för att förbereda för uppfinningar och innovationer. Om du vill justera med befintliga migreringar inom en moln implementerings plan kan du enklare göra migreringen och modernisering inom [migrerings metodiken](../../migrate/index.md).

## <a name="use-of-this-article"></a>Användning av den här artikeln

Den här artikeln beskriver en serie metoder som överensstämmer med migreringen. Du kan justera dessa metoder på bästa sätt för att migrera standard-verktygskedjan.

Under utvärderings processen inom migreringen bedömer ett moln antagande team det aktuella tillstånd och önskade framtida tillstånd för den migrerade till gången. När processen är en del av en Innovations ansträngning kan både moln implementerings teamen använda den här artikeln för att göra dessa bedömningar.

## <a name="primary-toolset"></a>Primära verktyg

När du migrerar och modernisera lokala data är det vanligaste valet av Azure-verktyg [Azure Database migration service](https://docs.microsoft.com/azure/dms). Den här tjänsten är en del av den bredare [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) verktygskedjan. För befintliga SQL Server data källor kan [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview) hjälpa dig att utvärdera och migrera ett litet antal data strukturer.

För att stödja Oracle-och NoSQL-migreringar kan du också använda [Database migration service](https://docs.microsoft.com/azure/dms) för vissa typer av käll-till-mål-databaser. Exempel på detta är Oracle till PostgreSQL och MongoDB för Cosmos DB. Det vanligaste är att implementerings team använder partner verktyg eller anpassade skript för att migrera till Azure Cosmos DB, Azure HDInsight eller virtuella dator alternativ baserat på infrastruktur som en tjänst (IaaS).

## <a name="considerations-and-guidance"></a>Överväganden och vägledning

När du använder Azure Database Migration Service för migrering och modernisering av data är det viktigt att förstå:

- Den aktuella plattformen för att vara värd för data källan.
- Den aktuella versionen.
- Den framtida plattform och version som bäst stöder kunden hypotes eller mål.

I följande tabell visas käll-och mål par som kan granskas med migrations teamet. Varje par innehåller ett verktygs val och en länk till en relaterad guide.

### <a name="migration-type"></a>Typ av migrering

Med en offlinemigrering startar programmets frånkopplade tillstånd när migreringen startar. Med onlinemigrering begränsas det frånkopplade tillståndet till tiden för att genomföra snabb migrering vid slutet av migreringen.

Vi rekommenderar att du bestämmer dig för den acceptabla stillestånds tiden för verksamheten och testar en migrering offline. Det gör du för att kontrol lera om återställnings tiden uppfyller de acceptabla stillestånds tiden. Om återställnings tiden är oacceptabelt gör du en online-migrering.

|Källa  |Målinrikta  |Verktyg  |Typ av migrering  |Vägledning  |
|---------|---------|---------|---------|---------|
|SQL Server|Azure SQL Database|Database Migration Service|Offline|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|SQL Server|Azure SQL Database|Database Migration Service|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|SQL Server|Azure SQL Database Managed Instance|Database Migration Service|Offline|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|SQL Server|Azure SQL Database Managed Instance|Database Migration Service|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|RDS-SQL Server|Azure SQL Database eller Azure SQL Database Hanterad instans|Database Migration Service|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|
|MySQL|Azure-databas för MySQL|Database Migration Service|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online)|
|PostgreSQL|Azure-databas för PostgreSQL|Database Migration Service|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online)|
|MongoDB|Azure Cosmos DB Mongo-API|Database Migration Service|Offline|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db)|
|MongoDB|Azure Cosmos DB Mongo-API|Database Migration Service|Online|[Självstudie](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db-online)|
|Oracle|Olika plattform som en tjänst (PaaS) och IaaS-alternativ|En partners verktyg eller Azure Migrate|Offline eller online|[Besluts träd](../../migrate/expanded-scope/data-oracle-migration.md)|
|Olika NoSQL DB-alternativ|Alternativ för Cosmo DB eller IaaS|Stegvisa migreringar eller Azure Migrate|Offline eller online|[Besluts träd](../../migrate/expanded-scope/data-no-sql-migration.md)|
