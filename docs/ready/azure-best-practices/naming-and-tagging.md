---
title: Rekommenderade regler för namngivning och taggar
description: Lär dig mer om resurs namns-och taggnings rekommendationer som syftar till att stödja företagets moln införande ansträngningar.
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/05/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: readiness, fasttrack-edit
ms.openlocfilehash: 2ebb04a09c6c14b44e0237c2530144c69014f5b4
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80354514"
---
<!-- cSpell:ignore westeurope usgovia accountlookup messagequery -->

# <a name="recommended-naming-and-tagging-conventions"></a>Rekommenderade regler för namngivning och taggar

Organisera dina moln till gångar för att stödja drifts hantering och redovisnings krav. Väldefinierade konventioner för namngivning och metadata hjälper dig att snabbt hitta och hantera resurser. Dessa konventioner hjälper också till att associera moln användnings kostnader med företags team via åter betalnings-och showback-redovisning.

Azure Architecture Centerens vägledning om [namngivnings regler och begränsningar för Azure-resurser](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming) ger allmänna rekommendationer och plattforms begränsningar. Följande diskussion utökar den här vägledningen med mer detaljerade rekommendationer som syftar till att ge stöd för besluts ansträngningar i företags moln.

Det kan vara svårt att ändra resurs namn. Upprätta en omfattande namngivnings konvention innan du påbörjar en stor moln distribution.

> [!NOTE]
> Alla företag har olika organisations- och hanteringskrav. Dessa rekommendationer ger en utgångs punkt för diskussioner i dina moln implementerings team.
>
> När dessa diskussioner fortsätter använder du följande mall för att avbilda namngivnings-och taggnings besluten som du gör när du justerar rekommendationerna till dina specifika affärs behov.
>
> Ladda ned [mall för namngivnings- och etikettkonventionspårning](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx).

## <a name="naming-and-tagging-resources"></a>Namngivnings- och etikettresurser

En namngivnings- och etikettstrategi omfattar information om företaget och verksamheten, såsom delar av resursnamn och metadatataggar:

- Affärs sidan av denna strategi säkerställer att resurs namn och taggar innehåller den organisatoriska information som krävs för att identifiera teamen. Använd en resurs tillsammans med företagsägare som ansvarar för resurskostnader.
- Den driftrelaterade sidan garanterar att namn och taggar innehåller information som IT-teamet använder för att identifiera arbetsbelastning, program, miljö, allvarsgrad och annan information som är användbar för att hantera resurser.

## <a name="resource-naming"></a>Resursnamngivning

En lämplig namngivningskonvention sätter samman resursnamn genom att använda viktig resursinformation som delar av resursens namn. Med dessa [rekommenderade namngivnings konventioner](#example-names)heter en offentlig IP-resurs för en produktion av SharePoint-arbetsbelastning som detta: `pip-sharepoint-prod-westus-001`.

Från namnet kan du snabbt identifiera resurstypen, dess associerade arbetsbelastning, distributionsmiljön och den Azure-region som är värd för den.

### <a name="naming-scope"></a>Namngivningsomfång

Alla typer av Azure-resurser har ett omfång som definierar nivån som resurs namn måste vara unika. En resurs måste ha ett unikt namn inom sitt omfång.

Ett virtuellt nätverk har till exempel en resursgrupps omfång, vilket innebär att det bara kan finnas ett nätverk med namnet `vnet-prod-westus-001` i en specifik resursgrupp. Andra resursgrupper kan ha sitt eget virtuella nätverk med namnet `vnet-prod-westus-001`. Ett annat exempel är undernät, som är begränsade till virtuella nätverk. Det innebär att varje undernät inom ett virtuellt nätverk måste ha ett unikt namn.

Vissa resursnamn, till exempel PaaS-tjänster med offentliga slutpunkter eller DNS-taggar för virtuella datorer har globala omfång, vilket innebär att de måste vara unika för hela Azure-plattformen.

Resursnamnen har längdbegränsningar. Det är viktigt att avväga innehållet i ett namn med dess omgång och längd när du utformar din namngivningskonvention. Mer information om namngivningsregler för tillåtna tecken, omfattningar och namnlängder för resurstyper finns i [Namngivningskonventioner för Azure-resurser.](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming)

### <a name="recommended-naming-components"></a>Rekommenderade namndelar

När du utformar din namngivningskonvention ska du identifiera viktig information som du vill visa i ett resursnamn. Olika typer av information är relevanta för olika resurstyper. Följande lista innehåller exempel på information som är användbar när du skapar resursnamn.

Se till att namndelarnas längd inte överskrider gränsen för resursnamn.

| Namndel            | Beskrivning                                                                                                                                                                                                      | Exempel                                         |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------|
| Affärsenhet               | Avdelning på toppnivå för ditt företag som äger prenumerationen eller arbetsbelastningen som resursen tillhör. I mindre organisationer kan den här komponenten representera en enskild avdelning. | _fin_, _mktg_, _product_, _it_, _corp_           |
| Prenumerationstyp           | Sammanfattande beskrivning av syftet med den prenumeration som innehåller resursen. Delas ofta upp enligt typ av distributionsmiljö eller specifika arbetsbelastningar.                                                       | _Prod_, _delad_, _klient_                       |
| Namn på program eller tjänst | Namnet på programmet, arbetsbelastningen eller tjänsten som resursen ingår i.                                                                                                                                    | _navigator_, _emissions_, _sharepoint_, _hadoop_ |
| Distributionsmiljö      | Stadiet i utvecklingslivscykeln för arbetsbelastningen som stöds av resursen.                                                                                                                              | _Prod_, _dev_, _frågor och svar_, _fas_, _test_             |
| Region                      | Den Azure-region där resursen har distribuerats.                                                                                                                                                                 | _väst_, _eastus2_, _westeurope_, _usgovia_     |

### <a name="recommended-resource-type-prefixes"></a>Rekommenderade prefix för resurstyp

Varje arbetsbelastning kan bestå av många enskilda resurser och tjänster. Om du använder prefix för resurstyp i dina resursnamn är det enklare att identifiera program- eller tjänstkomponenter.

I följande lista visas rekommenderade prefix för Azure-resurstyper som du kan använda när du definierar namnkonventionerna.

<!-- cSpell:disable -->

### <a name="general"></a>Allmänt

| Tillgångstyp                      | Namn-prefix |
|---------------------------------|-------------|
| Resursgrupp                  | rg-         |
| Definition av princip               | politik     |
| API Management-tjänstinstans | APIM       |

### <a name="networking"></a>Nätverk

| Tillgångstyp                       | Namn-prefix |
|----------------------------------|-------------|
| Virtuellt nätverk                  | vnet-       |
| Undernät                           | snet-       |
| Nätverks gränssnitt (NIC)          | nic-        |
| Offentlig IP-adress                | pip-        |
| Belastningsutjämnare (intern)         | lbi-        |
| Belastningsutjämnare (extern)         | lbe-        |
| Nätverkssäkerhetsgrupp (NSG)     | nsg-        |
| Program säkerhets grupp (grupperna) | grupperna        |
| Lokal nätverksgateway            | lgw-        |
| Virtuell nätverksgateway          | vgw-        |
| VPN-anslutning                   | cn-         |
| Programgateway              | agw-        |
| Routningstabell                      | styra      |
| Traffic Manager-profil          | traf-       |

### <a name="compute-and-web"></a>Compute och Web

| Tillgångstyp                  | Namn-prefix |
|-----------------------------|-------------|
| Virtuell dator             | vm          |
| Skaluppsättning för virtuella datorer   | VMSS       |
| Tillgänglighetsuppsättning            | låta      |
| Lagringskonto för virtuell dator          | stvm        |
| Azure Arc-ansluten dator | arcm-       |
| Container instans          | ACI        |
| AKS-kluster                 | AKS        |
| Service Fabric-kluster      | form         |
| App Service-miljö     | ASE        |
| App Service-plan            | projektplan       |
| Webbapp                     | mobilappar        |
| Funktionsapp                | FUNC       |
| Molntjänst               | gör        |
| Notification Hubs           | ntf-        |
| Notification Hubs namnrymd | ntfns-      |

### <a name="databases"></a>Databaser

| Tillgångstyp                     | Namn-prefix |
|--------------------------------|-------------|
| Azure SQL Database Server      | SQL        |
| Azure SQL-databas             | sqldb-      |
| Cosmos DB databas             | Cosmos     |
| Azure-cache för Redis-instans | redis-      |
| MySQL-databas                 | mysql-      |
| PostgreSQL-databas            | psql       |
| Azure SQL Data Warehouse       | sqldw-      |
| Azure Synapse Analytics        | tillståndet        |
| SQL Server Stretch Database    | sqlstrdb-   |

### <a name="storage"></a>Storage

| Tillgångstyp       | Namn-prefix |
|------------------|-------------|
| Lagringskonto  | St          |
| Azure StorSimple | ssimp       |

### <a name="ai--machine-learning"></a>AI + Machine Learning

| Tillgångstyp                       | Namn-prefix |
|----------------------------------|-------------|
| Azure Cognitive Search           | srch-       |
| Azure Cognitive Services         | kugg hjuls        |
| Azure Machine Learning-arbetsyta | mlw-        |

### <a name="analytics-and-iot"></a>Analys och IoT

| Tillgångstyp                      | Namn-prefix |
|---------------------------------|-------------|
| Azure Analysis Services server  | som         |
| Azure Databricks arbets yta      | dbw-        |
| Azure Stream Analytics          | asa-        |
| Azure Data Factory              | automatisk        |
| Data Lake Store konto         | DLS         |
| Data Lake Analytics konto     | dla         |
| Händelsehubb                       | evh-        |
| HDInsight – Hadoop-kluster      | Hadoop     |
| HDInsight – HBase-kluster       | HBase      |
| HDInsight – Kafka-kluster       | Kafka      |
| HDInsight-Spark-kluster       | Spark      |
| HDInsight – Storm-kluster       | stort      |
| HDInsight-ML-kluster | MLS        |
| IoT Hub                         | IoT        |
| Power BI Embedded               | PBI        |

### <a name="integration"></a>Integrering

| Tillgångstyp        | Namn-prefix |
|-------------------|-------------|
| Logic Apps        | logiskt      |
| Service Bus       | sb-         |
| Service Bus kö | sbq-        |
| Service Bus ämne | sbt-        |

### <a name="management-and-governance"></a>Hantering och styrning

| Tillgångstyp              | Namn-prefix |
|-------------------------|-------------|
| Skiss               | BP         |
| Nyckelvalv               | 3,0         |
| Log Analytics-arbetsyta | kvorumloggen        |
| Application Insights    | appi-       |
| Recovery Services-valv | rsv-        |

### <a name="migration"></a>Migrering

| Tillgångstyp                          | Namn-prefix |
|-------------------------------------|-------------|
| Azure Migrate projekt               | migr-       |
| Database Migration Service instans | DMS        |
| Recovery Services-valv             | rsv-        |

<!-- cSpell:enable -->

## <a name="metadata-tags"></a>Metadatataggar

Om du använder metadatataggar med i dina molnresurser kan du inkludera information om tillgångar som inte kunde inkluderas i resursnamnet. Du kan använda den informationen till att utföra mer avancerad filtrering och rapportering av resurser. Du vill att dessa taggar ska innehålla sammanhang om resursens associerade arbetsbelastning eller program, driftkrav och ägarskapsinformation. Den här informationen kan användas av IT-avdelningen eller affärsteam för att hitta resurser eller generera rapporter om resursanvändning och fakturering.

De taggar som du fäster på resurser och de taggar som behövs eller är valfria varierar mellan olika organisationer. Följande lista innehåller exempel på vanliga taggar som speglar viktiga sammanhang och information om en resurs. Använd den här listan som utgångspunkt för att upprätta egna taggkonventioner.

| Taggnamn                  | Beskrivning                                                                                                                                                                                                          | Nyckel               | Exempelvärde                                              |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|------------------------------------------------------------|
| Programnamn          | Namnet på programmet, tjänsten eller arbetsbelastningen som resursen är associerad med.                                                                                                                                       | _ApplicationName_ | _{appnamn}_                                               |
| Godkännarens namn             | Person som ansvarar för att godkänna kostnader relaterade till den här resursen.                                                                                                                                                     | _Approver_        | _{e-post}_                                                  |
| Budget krävs/godkänd  | Pengar som har tilldelats programmet, tjänsten eller arbetsbelastningen.                                                                                                                                                          | _BudgetAmount_    | _{\$}_                                                     |
| Affärsenhet             | Avdelning på toppnivå för ditt företag som äger prenumerationen eller arbetsbelastningen som resursen tillhör. I mindre organisationer kan den här taggen representera en enskild avdelning. | _BusinessUnit_    | _Ekonomi_, _marknadsföring_, _{produkt namn}_ , _Corp_, _delad_ |
| Kostnadsställe               | Kostnadsställe som associeras med resursen.                                                                                                                                                                | _CostCenter_      | _{värde}_                                                 |
| Haveriberedskap         | Programmet, arbetsbelastningen eller tjänstens affärskritiskhet.                                                                                                                                                       | _DR_              | _Verksamhets kritisk_, _kritisk_, _viktig_                |
| Projektets slutdatum   | Datum då programmet, arbetsbelastningen eller tjänsten har schemalagts för utsättning.                                                                                                                                         | _EndDate_         | _{datum}_                                                   |
| Miljö               | Programmet, arbetsbelastningen eller tjänstens distributionsmiljö.                                                                                                                                                     | _Env_             | _Prod_, _dev_, _frågor och svar_, _fas_, _test_                       |
| Ägarens namn                | Programmet, arbetsbelastningen eller tjänstens ägare.                                                                                                                                                                      | _Ägare_           | _{e-post}_                                                  |
| Beställarens namn            | Användare som beställde utvecklingen av det här programmet.                                                                                                                                                                 | _Requestor_       | _{e-post}_                                                  |
| Tjänsteklass             | Serviceavtalsnivå för programmet, arbetsbelastningen eller tjänsten.                                                                                                                                              | _ServiceClass_    | _Dev_, _brons_, _silver_, _guld_                          |
| Projektets startdatum | Datum då programmet, arbetsbelastningen eller tjänsten först distribuerades.                                                                                                                                                  | _StartDate_       | _{datum}_                                                   |

## <a name="example-names"></a>Exempel namn

I följande avsnitt finns några exempel namn för vanliga typer av Azure-resurser i en distribution av företags moln.

<!-- cSpell:disable -->

<!-- markdownlint-disable MD024 MD033 -->

### <a name="example-names-general"></a>Exempel namn: allmänt

| Tillgångstyp                      | Omfång                              | Format                                                      | Exempel                                                                                                                |
|---------------------------------|------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Prenumeration                    | Redovisning <br/>Enterprise-avtal | \<Affärsenhet\>-\<Prenumerationstyp\>-\<\#\#\#\>          | <ul><li>mktg-prod-001 </li><li>corp-shared-001 </li><li>fin-client-001</li></ul>                                        |
| Resursgrupp                  | Prenumeration                       | RG-\<app eller tjänst namn\>-\<prenumerations typ\>-\<\#\#\#\> | <ul><li>rg-mktgsharepoint-prod-001 </li><li>rg-acctlookupsvc-share-001 </li><li>rg-ad-dir-services-shared-001</li></ul> |
| API Management-tjänstinstans | Global                             | APIM-\<app-eller tjänst namn\>                                | APIM – Navigator-Prod                                                                                                     |

### <a name="example-names-networking"></a>Exempel namn: nätverk

| Tillgångstyp                   | Omfång           | Format                                                               | Exempel                                                                                                                      |
|------------------------------|-----------------|----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| Virtuellt nätverk              | Resursgrupp  | vnet-\<Subscription type\>-\<Region\>-\<\#\#\#\>                     | <ul><li>vnet-shared-eastus2-001 </li><li>vnet-prod-westus-001 </li><li>vnet-client-eastus2-001</li></ul>                      |
| Undernät                       | Virtuellt nätverk | snet-\<subscription\>-\<subregion\>-\<\#\#\#\>                       | <ul><li>snet-shared-eastus2-001 </li><li>snet-prod-westus-001 </li><li>snet-client-eastus2-001</li></ul>                      |
| Nätverks gränssnitt (NIC)      | Resursgrupp  | nic-\<\#\#\>-\<vmname\>-\<subscription\>\<\#\#\#\>                   | <ul><li>nic-01-dc1-shared-001 </li><li>nic-02-vmhadoop1-prod-001 </li><li>nic-02-vmtest1-client-001</li></ul>                 |
| Offentlig IP-adress            | Resursgrupp  | pip-\<vm name or app name\>-\<Environment\>-\<subregion\>-\<\#\#\#\> | <ul><li>pip-dc1-shared-eastus2-001 </li><li>pip-hadoop-prod-westus-001</li></ul>                                              |
| Lastbalanserare                | Resursgrupp  | lb-\<app name or role\>\<Environment\>\<\#\#\#\>                     | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-dev-001</li></ul>                                                        |
| Nätverkssäkerhetsgrupp (NSG) | Undernät eller NIC   | NSG-\<princip namn eller app-namn\>-\<\#\#\#\>                           | <ul><li>nsg-weballow-001 </li><li>nsg-rdpallow-001 </li><li>nsg-sqlallow-001 </li><li>nsg-dnsbloked-001</li></ul>             |
| Lokal nätverksgateway        | Virtuell gateway | LGW-\<prenumerations typ\>-\<region\>-\<\#\#\#\>                      | <ul><li>LGW-Shared-eastus2-001 </li><li>LGW-Prod-väst-001 </li><li>LGW-client-eastus2-001</li></ul>                         |
| Virtuell nätverksgateway      | Virtuellt nätverk | vgw-\<prenumerations typ\>-\<region\>-\<\#\#\#\>                      | <ul><li>vgw-Shared-eastus2-001 </li><li>vgw-Prod-väst-001 </li><li>vgw-client-eastus2-001</li></ul>                         |
| Plats-till-plats-anslutning      | Resursgrupp  | cn-\<local gateway name\>-to-\<virtual gateway name\>                | <ul><li>CN-LGW-Shared-eastus2-001-till-vgw-Shared-eastus2-001 </li><li>CN-LGW-Shared-eastus2-001-till-delad-väst-001</li></ul> |
| VPN-anslutning               | Resursgrupp  | cn-\<prenumeration1\>\<region1\>-till-\<prenumeration2\>\<region2\>-     | <ul><li>cn-shared-eastus2-to-shared-westus </li><li>cn-shared-eastus2-to-shared-westus</li></ul>                                  |
| Routningstabell                  | Resursgrupp  | Route-\<väg tabell namn\>                                           | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-dev-001</li></ul>                                                        |
| DNS-etikett                    | Global          | \<En post för en virtuell dator\>.[\<region\>.cloudapp.azure.com]                   | <ul><li>dc1.westus.cloudapp.azure.com </li><li>web1.eastus2.cloudapp.azure.com</li></ul>                                      |

### <a name="example-names-compute-and-web"></a>Exempel namn: Compute och Web

| Tillgångstyp                  | Omfång          | Format                                                              | Exempel                                                                                                                          |
|-----------------------------|----------------|---------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| Virtuell dator             | Resursgrupp | vm\<policy name or appname\>\<\#\#\#\>                              | <ul><li>vmnavigator001 </li><li>vmsharepoint001 </li><li>vmsqlnode001 </li><li>vmhadoop001</li></ul>                              |
| Lagringskonto för virtuell dator          | Global         | stvm\<performance type\>\<appname or prodname\>\<region\>\<\#\#\#\> | <ul><li>stvmstcoreeastus2001 </li><li>stvmpmcoreeastus2001 </li><li>stvmstplmeastus2001 </li><li>stvmsthadoopeastus2001</li></ul> |
| Webbapp                     | Global         | app-\<app-namn\>-\<miljö\>-\<\#\#\#\>. [{azurewebsites.net}]   | <ul><li>app-navigator-prod-001.azurewebsites.net </li><li>app-accountlookup-dev-001.azurewebsites.net</li></ul>                   |
| Funktionsapp                | Global         | FUNC-\<app-namn\>-\<miljö\>-\<\#\#\#\>. [{azurewebsites.net}]  | <ul><li>func-navigator-prod-001.azurewebsites.net </li><li>func-accountlookup-dev-001.azurewebsites.net</li></ul>                 |
| Molntjänst               | Global         | \<app-namn\>-\<miljö\>-\<\#\#\#\>. [{cloudapp.net}]        | <ul><li>could-navigator-prod-001.azurewebsites.net </li><li>could-accountlookup-dev-001.azurewebsites.net</li></ul>                   |
| Notification Hub            | Resursgrupp | NTF-\<app-namn\>-\<miljö\>                                    | <ul><li>NTF – Navigator-Prod </li><li>NTF-utsläpp – dev</li></ul>                                                                   |
| Notification Hubs namnrymd | Global         | ntfns-\<app-namn\>-\<miljö\>                                  | <ul><li>ntfns – Navigator-Prod </li><li>ntfns-utsläpp – dev</li></ul>                                                               |

### <a name="example-names-databases"></a>Exempel namn: databaser

| Tillgångstyp                     | Omfång              | Format                                 | Exempel                                                                  |
|--------------------------------|--------------------|----------------------------------------|---------------------------------------------------------------------------|
| Azure SQL Database Server      | Global             | SQL-\<app-namn\>-\<miljö\>       | <ul><li>SQL-Navigator-Prod </li><li>SQL-utsläpp – utveckling</li></ul>           |
| Azure SQL-databas             | Azure SQL Database | SQLDB-\<databas namn >-\<miljö\> | <ul><li>SQLDB – användare-Prod </li><li>SQLDB – användare – dev</li></ul>               |
| Cosmos DB databas             | Global             | Cosmos-\<app-namn\>-\<miljö\>    | <ul><li>Cosmos – Navigator-Prod </li><li>Cosmos-utsläpp – dev</li></ul>     |
| Azure-cache för Redis-instans | Global             | redis-\<App Name\>-\<Environment\>     | <ul><li>redis-navigator-prod </li><li>redis-emissions-dev</li></ul>       |
| MySQL-databas                 | Global             | mysql-\<App Name\>-\<Environment\>     | <ul><li>mysql-navigator-prod </li><li>mysql-emissions-dev</li></ul>       |
| PostgreSQL-databas            | Global             | psql-\<app-namn\>-\<miljö\>      | <ul><li>psql – Navigator-Prod </li><li>psql-utsläpp – dev</li></ul>         |
| Azure SQL Data Warehouse       | Global             | sqldw-\<App Name\>-\<Environment\>     | <ul><li>sqldw-navigator-prod </li><li>sqldw-emissions-dev</li></ul>       |
| SQL Server Stretch Database    | Azure SQL Database | -\<App Name\>-\<Environment\>  | <ul><li>sqlstrdb-navigator-prod </li><li>sqlstrdb-emissions-dev</li></ul> |

### <a name="example-names-storage"></a>Exempel namn: lagring

| Tillgångstyp                        | Omfång  | Format                                                                        | Exempel                                                              |
|-----------------------------------|--------|-------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| Lagrings konto (allmänt bruk)     | Global | st\<storage name\>\<\#\#\#\>                                                  | <ul><li>stnavigatordata001 </li><li>stemissionsoutput001</li></ul>    |
| Lagrings konto (diagnostikloggar) | Global | stdiag\<första två bokstäverna i prenumerationsnamnet och numret\>\<region\>\<\#\#\#\> | <ul><li>stdiagsh001eastus2001 </li><li>stdiagsh001westus001</li></ul> |
| Azure StorSimple                  | Global | ssimp\<App Name\>\<Environment\>                                              | <ul><li>ssimpnavigatorprod </li><li>ssimpemissionsdev</li></ul>       |

### <a name="example-names-ai--machine-learning"></a>Exempel namn: AI + Machine Learning

| Tillgångstyp                       | Omfång          | Format                            | Exempel                                                          |
|----------------------------------|----------------|-----------------------------------|-------------------------------------------------------------------|
| Azure Cognitive Search           | Global         | srch-\<App Name\>-\<Environment\> | <ul><li>srch-navigator-prod </li><li>srch-emissions-dev</li></ul> |
| Azure Cognitive Services         | Resursgrupp | kugg hjuls-\<app-namn\>-\<miljö\>  | <ul><li>kugg hjuls – Navigator-Prod </li><li>kugg hjuls-utsläpp – dev</li></ul>   |
| Azure Machine Learning-arbetsyta | Resursgrupp | mlw-\<app-namn\>-\<miljö\>  | <ul><li>mlw – Navigator-Prod </li><li>mlw-utsläpp – dev</li></ul>   |

### <a name="example-names-analytics-and-iot"></a>Exempel namn: Analytics och IoT

| Tillgångstyp                  | Omfång          | Format                              | Exempel                                                              |
|-----------------------------|----------------|-------------------------------------|-----------------------------------------------------------------------|
| Azure Data Factory          | Global         | ADF –\<app-namn\>\<miljö\>     | <ul><li>ADF – Navigator – Prod </li><li>ADF – utsläpp – dev</li></ul>       |
| Azure Stream Analytics      | Resursgrupp | asa-\<App Name\>-\<Environment\>    | <ul><li>asa-navigator-prod </li><li>asa-emissions-dev</li></ul>       |
| Data Lake Analytics konto | Global         | dla\<App Name\>\<Environment\>      | <ul><li>dlanavigatorprod </li><li>dlaemissionsdev</li></ul>           |
| Data Lake Storage konto   | Global         | dls\<App Name\>\<Environment\>      | <ul><li>dlsnavigatorprod </li><li>dlsemissionsdev</li></ul>           |
| Händelsehubb                   | Global         | evh-\<App Name\>-\<Environment\>    | <ul><li>evh-navigator-prod </li><li>evh-emissions-dev</li></ul>       |
| HDInsight – HBase-kluster   | Global         | HBase-\<app-namn\>-\<miljö\>  | <ul><li>HBase – Navigator-Prod </li><li>HBase-utsläpp – dev</li></ul>   |
| HDInsight – Hadoop-kluster  | Global         | Hadoop-\<app-namn\>-\<miljö\> | <ul><li>Hadoop-Navigator-Prod </li><li>Hadoop-utsläpp – dev</li></ul> |
| HDInsight-Spark-kluster   | Global         | Program namn för Spark-\<\>-\<miljö\>  | <ul><li>Spark-Navigator-Prod </li><li>Spark-utsläpp – dev </li></ul>  |
| IoT Hub                     | Global         | IoT-\<app-namn\>-\<miljö\>    | <ul><li>IoT-Navigator-Prod </li><li>IoT – utsläpp – dev</li></ul>       |
| Power BI Embedded           | Global         | PBI-\<app-namn\>\<miljö\>     | <ul><li>PBI – Navigator-Prod </li><li>PBI-utsläpp – dev</li></ul>       |

### <a name="example-names-integration"></a>Exempel namn: integration

| Tillgångstyp        | Omfång       | Format                                                     | Exempel                                                      |
|-------------------|-------------|------------------------------------------------------------|---------------------------------------------------------------|
| Service Bus       | Global      | sb-\<App Name\>-\<Environment\>.[{servicebus.windows.net}] | <ul><li>sb-navigator-prod </li><li>sb-emissions-dev</li></ul> |
| Service Bus kö | Service Bus | sbq-\<query descriptor\>                                   | <ul><li>sbq-messagequery</li></ul>                            |
| Service Bus ämne | Service Bus | SBT –\<frågans beskrivare\>                                   | <ul><li>sbt-messagequery</li></ul>                            |
