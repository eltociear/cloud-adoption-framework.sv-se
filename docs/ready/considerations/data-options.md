---
title: Granska dina data alternativ
description: Använd ramverket för moln införande för Azure för att lära dig hur du avgör vilka data som krävs för att vara värd för dina arbets belastningar.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: c9fa27ac671b17414a114a43f5224dd0e87de9d2
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80432111"
---
<!-- cSpell:ignore HDFS -->

# <a name="review-your-data-options"></a>Granska dina data alternativ

När du förbereder din landningszonmiljö för övergång till molnet måste du avgöra datakraven för att vara värd för dina arbetsbelastningar. Produkter och tjänster för Azure-databaser har stöd för en mängd olika scenarier och funktioner för datalagring. Konfigurationen av din landningszonmiljö i förhållande till dina datakrav beror på din arbetsbelastningsstyrning, samt tekniska och företagsrelaterade krav.

## <a name="identify-data-services-requirements"></a>Identifiera krav för datatjänster

Som del av utvärderingen och förberedelsen av landningszonen måste du identifiera de datalager som din landningszon måste ha stöd för. Processen förutsätter att du bedömer var och ett av de program och tjänster som utgör arbetsbelastningarna för att fastställa datalagrings- och åtkomstkrav. När du har identifierat och dokumenterat dessa krav kan du skapa principer för din landnings zon för att kontrollera tillåtna resurstyper utifrån dina arbetsbelastningsbehov.

För varje program eller tjänst som du distribuerar till din landningszonmiljö använder du följande beslutsträd som utgångspunkt för att hjälpa dig att avgöra vilka datalagringstjänster som ska användas:

![Beslutsträd för Azure-databastjänster](../../_images/ready/data-decision-tree.png)

### <a name="key-questions"></a>Viktiga frågor

Besvara följande frågor om dina arbetsbelastningar för att skapa ett beslutsunderlag baserat på beslutsträdet för Azure-databastjänster:

- **Behöver du fullständig kontroll eller ägarskap av databasens programvara eller värdoperativsystem?** Vissa scenarier kräver att du har en hög grad av kontroll eller ägande av programvarukonfigurationen och värdservrarna för dina databasarbetsbelastningar. I dessa scenarier kan du distribuera virtuella datorer med anpassad infrastruktur som en tjänst (IaaS) för att kontrollera distributionen och konfigurationen av datatjänster fullständigt. Om du inte har dessa förutsättningar kan hanterade databas tjänster med PaaS (plattform som tjänst) sänka kostnaderna för hantering och åtgärder.
- **Använder dina arbetsbelastningar relationsdatabasteknik?** Om ja, vilken teknik planerar du att använda? Azure tillhandahåller hanterade PaaS-databasfunktioner för [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview), [MySQL](https://docs.microsoft.com/azure/mysql/overview), [postgresql](https://docs.microsoft.com/azure/postgresql/overview) och[MariaDB](https://docs.microsoft.com/azure/mariadb/overview).
- **Kommer arbetsbelastningarna att använda SQL Server?** I Azure kan du köra arbetsbelastningarna på den IaaS-baserade [SQLServer på virtuella Azure-datorer](https://azure.microsoft.com/services/virtual-machines/sql-server) eller på den PaaS-baserade [ hanterade Azure SQL-databastjänsten](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview). Att välja vilket alternativ som ska användas handlar i huvudsak om huruvida du vill hantera din databas, tillämpa korrigeringar och göra säkerhetskopior själv eller om du vill delegera dessa åtgärder till Azure. I vissa fall kan kompatibilitetsproblem kräva användning av en SQL Server med IaaS-värd. Mer information om hur du väljer rätt alternativ för dina arbetsbelastningar finns i [Välj rätt SQL Server-alternativ i Azure.](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas)
- **Kommer dina arbetsbelastningar använda nyckel-/värdedatabaslagring?** [Azure Cache för Redis](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-overview) erbjuder en nyckel-/värdelagringslösning med hög prestanda som kan ge snabba, skalbara program. [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) tillhandahåller också nyckel-/värdelagringsfunktioner för allmänt bruk.
- **Kommer dina arbetsbelastningar använda data från dokument eller grafik?** [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) är en databastjänst med flera modeller som stöder en mängd olika datatyper och API:er. Azure Cosmos DB tillhandahåller också funktioner för dokument- och grafikdatabaser.
- **Kommer dina arbetsbelastningar använda data från kolumnfamiljer?** [Apache HBase i Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/hbase/apache-hbase-overview) bygger på Apache Hadoop. Det stöder stora mängder ostrukturerade och delvis strukturerade data i en schema lös databas som är ordnad efter kolumn familjer.
- **Kräver dina arbetsbelastningar hög kapacitet för dataanalys?** Du kan använda [Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) för att effektivt lagra och fråga strukturerade data i storleksordningen petabyte. För ostrukturerade stora dataarbetsbelastningar kan du använda [Azure Data Lake](https://azure.microsoft.com/solutions/data-lake) för att lagra och analysera filer och petabytestorlek och miljardvis med objekt.
- **Kräver dina arbetsbelastningar funktioner för sökmotor?** Du kan använda [Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search) för att bygga AI-förstärkta, molnbaserade sökindex som kan integreras i dina program.
- **Kommer dina arbetsbelastningar att använda tidsseriedata?** [Azure Time Series Insights](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-overview) har utformats för att lagra, visa och fråga stora mängder tidsseriedata, till exempel data som från IoT-enheter.

> [!NOTE]
> Läs mer om hur du kan utvärdera databasalternativ för var och ett av dina program eller [tjänster i Azures](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-comparison) programarkitekturguide.

## <a name="common-database-scenarios"></a>Vanliga databasscenarier

I följande tabell visas några vanliga krav för användningsscenarier och rekommenderade databastjänster för att hantera dem:

| **Scenario**                                                                                                                            | **Datatjänst**                                                                                                                                  |
|-----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| Jag behöver en globalt distribuerad databas för flera modeller, med stöd för NoSQL-val.                                                     | [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction)                                                                        |
| Jag behöver en helt hanterad relationsdatabas som är snabb att etablera, kan skalas efter hand och som har både inbyggd intelligens och säkerhet. | [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)                                               |
| Jag behöver en helt hanterad, skalbar och relationell MySQL-databas med hög tillgänglighet och säkerhet inbyggd utan extra kostnad.           | [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview)                                                                       |
| Jag behöver en helt hanterad och skalbar PostgreSQL-relationsdatabas med hög tillgänglighet och inbyggd säkerhet utan extra kostnad.      | [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/overview)                                                             |
| Jag planerar att vara värd för SQL Server-appar för företag i molnet och ha fullständig kontroll över serverns operativsystem.                                        | [SQL Server på virtuella datorer](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview) |
| Jag behöver ett helt hanterat och flexibelt informationslager med säkerhet på alla nivåer utan extra kostnad.                               | [Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is)                               |
| Jag behöver datasjölagringsresurser som kan stödja Hadoop-kluster eller HDFS-data.                                         | [Azure Data Lake](https://azure.microsoft.com/solutions/data-lake)                                                                                |
| Jag behöver dataåtkomst med stora dataflöden och konsekvent låg fördröjning för mina data för snabba och skalbara program.                           | [Azure Cache for Redis](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-overview)                                                    |
| Jag behöver en helt hanterad och skalbar MariaDB-relationsdatabas med hög tillgänglighet och inbyggd säkerhet utan extra kostnad.         | [Azure Database för MariaDB](https://docs.microsoft.com/azure/mariadb/overview)                                                                   |

## <a name="regional-availability"></a>Regional tillgänglighet

Med Azure kan du leverera tjänster i den skala du behöver för att nå dina kunder och partner,  _var de än är_. En viktig faktor vid planeringen av molndistributionen är att avgöra vilken Azure-region som ska vara värd för dina arbetsbelastningsresurser.

De flesta databastjänster är allmänt tillgängliga i de flesta Azure-regioner. Det finns dock några regioner som främst riktar sig till statskunder och som endast har stöd för en delmängd av dessa produkter. Innan du bestämmer vilka regioner du ska distribuera dina databasresurser till rekommenderar vi att du läser [regionssidan](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=data-factory,sql-server-stretch-database,redis-cache,database-migration,sql-data-warehouse,postgresql,mariadb,cosmos-db,mysql,sql-database) för att kontrollera den senaste statusen för regional tillgänglighet.

Mer information om global infrastruktur för Azure finns på [regionssidan för Azure](https://azure.microsoft.com/global-infrastructure/regions). Du kan också visa [produkter som är tillgängliga](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=all) per region för detaljerad information om de övergripande tjänster som är tillgängliga i varje Azure-region.

## <a name="data-residency-and-compliance-requirements"></a>Krav för dataplacering och efterlevnad

Juridiska krav och avtalskrav som gäller för datalagring gäller vanligtvis för dina arbetsbelastningar. Dessa krav kan variera baserat på din organisations plats, jurisdiktionen för de fysiska tillgångar som är värd för dina datalager eller din aktuella affärssektor. Dataskyldighetsöverväganden omfattar dataklassificering, dataplats och tillämpliga ansvar för dataskydd enligt modellen för gemensamt ansvar. Hjälp med att förstå dessa krav finns i vitboken  [Uppnå datahemvist och säkerhet som följer standard med hjälp av Azure](https://azure.microsoft.com/resources/achieving-compliant-data-residency-and-security-with-azure).

En del av dina krav på efterlevnad kan vara att kontrollera var dina databasresurser är fysiskt placerade. De geografiska Azure-regionerna är ordnade i grupper som kallas områden. Ett geografiskt  [Azure-område](https://azure.microsoft.com/global-infrastructure/geographies) garanterar att krav på dataplacering, landsbaserad placering, efterlevnad och elasticitet stöds inom geografiska och politiska gränser. Om dina arbetsbelastningar är föremål för datasuveränitet eller andra krav på efterlevnad måste du distribuera dina lagringsresurser i en region som ligger i ett kompatibelt Azure-område.

## <a name="establish-controls-for-database-services"></a>Upprätta kontroller för databastjänster

När du förbereder din landningszonmiljö kan du upprätta kontroller som begränsar vilka data som användarna kan distribuera. Kontrollerna kan hjälpa dig att hantera kostnader och begränsa säkerhetsriskerna, samtidigt som utvecklare och IT-team kan distribuera och konfigurera resurser som behövs för att stödja dina arbetsbelastningar.

När du har identifierat och dokumenterat kraven för landningszonen kan du använda [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) för att kontrollera vilka databasresurser användarna kan skapa. Kontroller kan antingen [tillåta eller neka att vissa typer av databasresurstyper skapas.](https://docs.microsoft.com/azure/governance/policy/samples/allowed-resource-types) Du kan till exempel begränsa användarna till att endast kunna skapa Azure SQL-databasresurser. Du kan också använda principer för att kontrollera de alternativ som tillåts när en resurs skapas, t.ex. [genom att begränsa vilka SQL Database SKU:er som kan tillhandahållas](https://docs.microsoft.com/azure/governance/policy/samples/allowed-sql-db-skus) eller [bara tillåta att vissa versioner av SQL Server](https://docs.microsoft.com/azure/governance/policy/samples/require-sql-12) installeras på en virtuell IaaS-dator.

Principer kan begränsas till resurser, resursgrupper, prenumerationer och hanteringsgrupper. Du kan inkludera principerna i definitionerna för [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints/overview) och tillämpa dem flera gånger i din molnegendom.
