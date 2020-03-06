---
title: Rekommenderade regler för namngivning och taggar
description: Lär dig mer om resurs namns-och taggnings rekommendationer som syftar till att stödja företagets moln införande ansträngningar.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: readiness, fasttrack-edit
ms.openlocfilehash: 915e974e3968e873c8cf23ec7696f66469f01c82
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78342022"
---
# <a name="recommended-naming-and-tagging-conventions"></a>Rekommenderade regler för namngivning och taggar

Att organisera molnbaserade till gångar på ett sätt som hjälper till att hantera krav på drifts hantering och support, är en vanlig utmaning i stora moln implementerings ansträngningar. Genom att använda väldefinierade system för namngivning och metadatataggar för molnbaserade resurser kan IT-personal snabbt hitta och hantera resurser. Väldefinierade namn och taggar bidrar också till att samordna molnkostnaderna med företagets team genom att använda redovisningsmekanismer som debiterar eller visar utgifter för avdelningar.

Azure Architecture Centerens vägledning om [namngivnings regler och begränsningar för Azure-resurser](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming) ger allmänna rekommendationer och plattforms begränsningar. Följande diskussion utökar den här vägledningen med mer detaljerade rekommendationer som syftar till att ge stöd för besluts ansträngningar i företags moln.

Resursnamn kan vara svåra att ändra. Prioritera att upprätta en omfattande namngivnings konvention innan du påbörjar en stor moln distribution.

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

### <a name="resource-naming"></a>Resursnamngivning

En lämplig namngivningskonvention sätter samman resursnamn genom att använda viktig resursinformation som delar av resursens namn. Med dessa [rekommenderade namngivnings konventioner](#sample-naming-convention)heter en offentlig IP-resurs för en produktion av SharePoint-arbetsbelastning som detta: `pip-sharepoint-prod-westus-001`.

Från namnet kan du snabbt identifiera resurstypen, dess associerade arbetsbelastning, distributionsmiljön och den Azure-region som är värd för den.

#### <a name="naming-scope"></a>Namngivningsomfång

Alla typer av Azure-resurser har ett omfång som definierar nivån som resurs namn måste vara unika. En resurs måste ha ett unikt namn inom sitt omfång.

Ett virtuellt nätverk har till exempel en resursgrupps omfång, vilket innebär att det bara kan finnas ett nätverk med namnet `vnet-prod-westus-001` i en specifik resursgrupp. Andra resursgrupper kan ha sitt eget virtuella nätverk med namnet `vnet-prod-westus-001`. Ett annat exempel är undernät, som är begränsade till virtuella nätverk. Det innebär att varje undernät inom ett virtuellt nätverk måste ha ett unikt namn.

Vissa resursnamn, till exempel PaaS-tjänster med offentliga slutpunkter eller DNS-taggar för virtuella datorer har globala omfång, vilket innebär att de måste vara unika för hela Azure-plattformen.

Resursnamnen har längdbegränsningar. Det är viktigt att avväga innehållet i ett namn med dess omgång och längd när du utformar din namngivningskonvention. Mer information om namngivningsregler för tillåtna tecken, omfattningar och namnlängder för resurstyper finns i [Namngivningskonventioner för Azure-resurser.](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming)

#### <a name="recommended-naming-components"></a>Rekommenderade namndelar

När du utformar din namngivningskonvention ska du identifiera viktig information som du vill visa i ett resursnamn. Olika typer av information är relevanta för olika resurstyper. Följande lista innehåller exempel på information som är användbar när du skapar resursnamn.

Se till att namndelarnas längd inte överskrider gränsen för resursnamn.

| Namndel | Beskrivning | Exempel |
| --- | --- | --- |
| Affärsenhet | Avdelning på toppnivå för ditt företag som äger prenumerationen eller arbetsbelastningen som resursen tillhör. I mindre organisationer kan den här komponenten representera en enskild avdelning. | _fin_, _mktg_, _product_, _it_, _corp_ |
| Prenumerationstyp | Sammanfattande beskrivning av syftet med den prenumeration som innehåller resursen. Delas ofta upp enligt typ av distributionsmiljö eller specifika arbetsbelastningar. | _Prod_, _delad_, _klient_ |
| Namn på program eller tjänst | Namnet på programmet, arbetsbelastningen eller tjänsten som resursen ingår i. | _navigator_, _emissions_, _sharepoint_, _hadoop_ |
| Distributionsmiljö | Stadiet i utvecklingslivscykeln för arbetsbelastningen som stöds av resursen. | _Prod_, _dev_, _frågor och svar_, _fas_, _test_ |
| Region | Den Azure-region där resursen har distribuerats. | _väst_, _eastus2_, _westeurope_, _usgovia_ |

#### <a name="recommended-resource-type-prefixes"></a>Rekommenderade prefix för resurstyp

Varje arbetsbelastning kan bestå av många enskilda resurser och tjänster. Om du använder prefix för resurstyp i dina resursnamn är det enklare att identifiera program- eller tjänstkomponenter.

I följande lista visas rekommenderade prefix för Azure-resurstyper som du kan använda när du definierar namnkonventionerna.

| Resurstyp                       | Resursnamnprefix |
| ----------------------------------- | -------------------- |
| Resursgrupp                      | rg-                  |
| Tillgänglighetsuppsättning                    | låta               |
| API Management-tjänst              | Application                 |
| Virtuellt nätverk                     | vnet-                |
| Virtuell nätverksgateway             | vnetgw-              |
| Gateway-anslutning                  | cn-                  |
| Undernät                              | snet-                |
| Nätverkssäkerhetsgrupp              | nsg-                 |
| Routningstabell                         | styra               |
| Virtuell dator                     | vm                   |
| Azure Arc-anslutna datorer        | arcm-                |
| Lagringskonto för virtuell dator                  | stvm                 |
| Offentlig IP-adress                           | pip-                 |
| Belastningsutjämnare (intern)            | ILB                 |
| Belastningsutjämnare (extern)            | Elb                 |
| NIC                                 | nic-                 |
| Nyckelvalv                           | 3,0                  |
| AKS-kluster                         | AKS                 |
| AKS-behållare                       | CON                 |
| Service Bus                         | sb-                  |
| Service Bus kö                   | sbq-                 |
| Service Bus ämne                   | sbt-                 |
| App Service-plan                    | projektplan                |
| Webbapp                             | mobilappar                 |
| Funktionsapp                        | FUNC                |
| Logikapp                           | logiskt               |
| Molntjänst                       | gör                 |
| Azure SQL Database Server           | SQL                 |
| Azure SQL-databas                  | sqldb-               |
| Cosmos DB databas                  | Cosmos              |
| Azure cache för Redis-cache         | redis-               |
| MySQL-databas                      | mysql-               |
| PostgreSQL-databas                 | psql                |
| Azure SQL Data Warehouse            | sqldw-               |
| SQL Server Stretch Database         | sqlstrdb-            |
| Lagringskonto                     | St                   |
| Azure StorSimple                    | ssimp                |
| Azure Search                        | srch-                |
| Azure Cognitive Services            | kugg hjuls                 |
| Azure Machine Learning-arbetsyta    | mlw-                 |
| Azure Data Lake Storage             | DLS                  |
| Azure Data Lake Analytics           | dla                  |
| Azure HDInsight – Spark             | hdis-                |
| Azure HDInsight – Hadoop            | hdihd-               |
| Azure HDInsight – R Server          | hdir-                |
| Azure HDInsight – HBase             | hdihb-               |
| Power BI Embedded                   | PBI                 |
| Azure Stream Analytics              | asa-                 |
| Azure Data Factory                  | automatisk                 |
| Händelsehubb                           | evh-                 |
| IoT Hub                             | IoT                 |
| Notification Hub                   | ntf-                 |
| Notification Hubs namnrymd         | ntfns-               |
| Log Analytics-arbetsyta             | kvorumloggen                 |
| Application Insights                | appi-                |
| Recovery Services valv             | rsv-                 |

### <a name="metadata-tags"></a>Metadatataggar

Om du använder metadatataggar med i dina molnresurser kan du inkludera information om tillgångar som inte kunde inkluderas i resursnamnet. Du kan använda den informationen till att utföra mer avancerad filtrering och rapportering av resurser. Du vill att dessa taggar ska innehålla sammanhang om resursens associerade arbetsbelastning eller program, driftkrav och ägarskapsinformation. Den här informationen kan användas av IT-avdelningen eller affärsteam för att hitta resurser eller generera rapporter om resursanvändning och fakturering.

De taggar som du fäster på resurser och de taggar som behövs eller är valfria varierar mellan olika organisationer. Följande lista innehåller exempel på vanliga taggar som speglar viktiga sammanhang och information om en resurs. Använd den här listan som utgångspunkt för att upprätta egna taggkonventioner.

| Taggnamn                  | Beskrivning                                                                                                                                                                                                    | Nyckel               | Exempelvärde                                   |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------|
| Programnamn          | Namnet på programmet, tjänsten eller arbetsbelastningen som resursen är associerad med.                                                                                                                                 | _ApplicationName_ | _{appnamn}_                                    |
| Godkännarens namn             | Person som ansvarar för att godkänna kostnader relaterade till den här resursen.                                                                                                                                               | _Approver_        | _{e-post}_                                       |
| Budget krävs/godkänd  | Pengar som har tilldelats programmet, tjänsten eller arbetsbelastningen.                                                                                                                                                    | _BudgetAmount_    | _{\$}_                                          |
| Affärsenhet             | Avdelning på toppnivå för ditt företag som äger prenumerationen eller arbetsbelastningen som resursen tillhör. I mindre organisationer kan den här taggen representera en enskild avdelning. | _BusinessUnit_    | _Ekonomi_, _marknadsföring_, _{produkt namn}_ , _Corp_, _delad_ |
| Kostnadsställe               | Kostnadsställe som associeras med resursen.                                                                                                                                                          | _CostCenter_      | _{värde}_                                      |
| Haveriberedskap         | Programmet, arbetsbelastningen eller tjänstens affärskritiskhet.                                                                                                                                                | _DR_              | _Verksamhets kritisk_, _kritisk_, _viktig_         |
| Projektets slutdatum   | Datum då programmet, arbetsbelastningen eller tjänsten har schemalagts för utsättning.                                                                                                                                  | _EndDate_         | _{datum}_                                        |
| Miljö               | Programmet, arbetsbelastningen eller tjänstens distributionsmiljö.                                                                                                                                              | _Env_             | _Prod_, _dev_, _frågor och svar_, _fas_, _test_                    |
| Ägarens namn                | Programmet, arbetsbelastningen eller tjänstens ägare.                                                                                                                                                                | _Ägare_           | _{e-post}_                                       |
| Beställarens namn            | Användare som beställde utvecklingen av det här programmet.                                                                                                                                                          | _Requestor_       | _{e-post}_                                       |
| Tjänsteklass             | Serviceavtalsnivå för programmet, arbetsbelastningen eller tjänsten.                                                                                                                                       | _ServiceClass_    | _Dev_, _brons_, _silver_, git _guld_                     |
| Projektets startdatum | Datum då programmet, arbetsbelastningen eller tjänsten först distribuerades.                                                                                                                                           | _StartDate_       | _{datum}_                                        |

## <a name="sample-naming-convention"></a>Exempel på namngivningskonvention

I följande avsnitt finns exempel på namngivningssystem för vanliga typer av Azure-resurser som distribueras i samband med en molndistribution för företag.

<!-- markdownlint-disable MD033 -->

### <a name="subscriptions"></a>Prenumerationer

| Tillgångstyp   | Omfång                        | Format                                             | Exempel                                     |
|--------------|------------------------------|----------------------------------------------------|----------------------------------------------|
| Prenumeration | Konto/företagsavtal | \<Affärsenhet\>-\<Prenumerationstyp\>-\<\#\#\#\> | <ul><li>mktg-prod-001 </li><li>corp-shared-001 </li><li>fin-client-001</li></ul> |

### <a name="resource-groups"></a>Resursgrupper

| Tillgångstyp     | Omfång        | Format                                                     | Exempel                                                                            |
|----------------|--------------|------------------------------------------------------------|-------------------------------------------------------------------------------------|
| Resursgrupp | Prenumeration | RG-\<app eller tjänst namn\>-\<prenumerations typ\>-\<\#\#\#\> | <ul><li>rg-mktgsharepoint-prod-001 </li><li>rg-acctlookupsvc-share-001 </li><li>rg-ad-dir-services-shared-001</li></ul> |

### <a name="virtual-networking"></a>Virtuellt nätverk

| Tillgångstyp               | Omfång           | Format                                                                | Exempel                                                                                              |
|--------------------------|-----------------|-----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| Azure Virtual Network          | Resursgrupp  | vnet-\<Subscription type\>-\<Region\>-\<\#\#\#\>                      | <ul><li>vnet-shared-eastus2-001 </li><li>vnet-prod-westus-001 </li><li>vnet-client-eastus2-001</li></ul>                                  |
| Virtuell gateway för virtuellt nätverk     | Virtuellt nätverk | vnetgw-v-\<prenumerations typ\>-\<region\>-\<\#\#\#\>                 | <ul><li>vnetgw-v-Shared-eastus2-001 </li><li>vnetgw-v-Prod-väst-001 </li><li>vnetgw-v-client-eastus2-001</li></ul>                   |
| Virtuell lokal nätverksgateway       | Virtuell gateway | vnetgw-l-\<prenumerations typ\>-\<region\>-\<\#\#\#\>                 | <ul><li>vnetgw-l-Shared-eastus2-001 </li><li>vnetgw-l-Prod-väst-001 </li><li>vnetgw-l-client-eastus2-001</li></ul>                   |
| Plats-till-plats-anslutningar | Resursgrupp  | cn-\<local gateway name\>-to-\<virtual gateway name\>                 | <ul><li>cn-l-gw-shared-eastus2-001-to-v-gw-shared-eastus2-001 </li><li>cn-l-gw-shared-eastus2-001-to-shared-westus-001</li></ul> |
| Anslutningar till virtuellt nätverk         | Resursgrupp  | cn-\<prenumeration1\>\<region1\>-till-\<prenumeration2\>\<region2\>-      | <ul><li>cn-shared-eastus2-to-shared-westus </li><li>cn-shared-eastus2-to-shared-westus</li></ul>                                     |
| Undernät                   | Virtuellt nätverk | snet-\<subscription\>-\<subregion\>-\<\#\#\#\>                       | <ul><li>snet-shared-eastus2-001 </li><li>snet-prod-westus-001 </li><li>snet-client-eastus2-001</li></ul>                                  |
| Nätverkssäkerhetsgrupp   | Undernät eller NIC   | nsg-\<policy name or appname\>-\<\#\#\#\>                             | <ul><li>nsg-weballow-001 </li><li>nsg-rdpallow-001 </li><li>nsg-sqlallow-001 </li><li>nsg-dnsbloked-001</li></ul>                                  |
| Offentlig IP-adress                | Resursgrupp  | pip-\<vm name or app name\>-\<Environment\>-\<subregion\>-\<\#\#\#\> | <ul><li>pip-dc1-shared-eastus2-001 </li><li>pip-hadoop-prod-westus-001</li></ul>                                                 |

### <a name="azure-virtual-machines"></a>Azure Virtual Machines

| Tillgångstyp         | Omfång          | Format                                                              | Exempel                                                                             |
|--------------------|----------------|---------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Azure Virtual Machines    | Resursgrupp | vm\<policy name or appname\>\<\#\#\#\>                              | <ul><li>vmnavigator001 </li><li>vmsharepoint001 </li><li>vmsqlnode001 </li><li>vmhadoop001</li></ul>                              |
| Lagringskonto för virtuell dator | Global         | stvm\<performance type\>\<appname or prodname\>\<region\>\<\#\#\#\> | <ul><li>stvmstcoreeastus2001 </li><li>stvmpmcoreeastus2001 </li><li>stvmstplmeastus2001 </li><li>stvmsthadoopeastus2001</li></ul> |
| DNS-etikett          | Global         | \<En post för en virtuell dator\>.[\<region\>.cloudapp.azure.com]                  | <ul><li>dc1.westus.cloudapp.azure.com </li><li>web1.eastus2.cloudapp.azure.com</li></ul>                        |
| Azure Load Balancer      | Resursgrupp | lb-\<app name or role\>\<Environment\>\<\#\#\#\>                    | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-dev-001</li></ul>                                          |
| NIC                | Resursgrupp | nic-\<\#\#\>-\<vmname\>-\<subscription\>\<\#\#\#\>                  | <ul><li>nic-01-dc1-shared-001 </li><li>nic-02-vmhadoop1-prod-001 </li><li>nic-02-vmtest1-client-001</li></ul>            |

### <a name="paas-services"></a>PaaS-tjänster

| Tillgångstyp           | Omfång  | Format                                                              | Exempel                                                                                 |
|----------------------|--------|---------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| Azure Web Apps       | Global | app-\<app-namn\>-\<miljö\>-\<\#\#\#\>. [{azurewebsites.net}] | <ul><li>app-navigator-prod-001.azurewebsites.net </li><li>app-accountlookup-dev-001.azurewebsites.net</li></ul> |
| Azure Functions      | Global | FUNC-\<app-namn\>-\<miljö\>-\<\#\#\#\>. [{azurewebsites.net}] | <ul><li>func-navigator-prod-001.azurewebsites.net </li><li>func-accountlookup-dev-001.azurewebsites.net</li></ul> |
| Azure Cloud Services | Global | \<app-namn\>-\<miljö\>-\<\#\#\#\>. [{cloudapp.net}]       | <ul><li>could-navigator-prod-001.azurewebsites.net </li><li>could-accountlookup-dev-001.azurewebsites.net</li></ul>   |

### <a name="azure-service-bus"></a>Azure Service Bus

| Tillgångstyp         | Omfång       | Format                                                     | Exempel                           |
|--------------------|-------------|------------------------------------------------------------|------------------------------------|
| Azure Service Bus        | Global      | sb-\<App Name\>-\<Environment\>.[{servicebus.windows.net}] | <ul><li>sb-navigator-prod </li><li>sb-emissions-dev</li></ul> |
| Azure Service Bus-köer | Service Bus | sbq-\<query descriptor\>                                   | <ul><li>sbq-messagequery</li></ul>                   |
| Azure Service Bus ämnen | Service Bus | SBT –\<frågans beskrivare\>                                   | <ul><li>sbt-messagequery</li></ul>                   |

### <a name="databases"></a>Databaser

| Tillgångstyp                          | Omfång              | Format                                | Exempel                                       |
|-------------------------------------|--------------------|---------------------------------------|------------------------------------------------|
| Azure SQL Database Server           | Global             | SQL-\<app-namn\>-\<miljö\>      | <ul><li>SQL-Navigator-Prod </li><li>SQL-utsläpp – utveckling</li></ul>           |
| Azure SQL Database                  | Azure SQL Database | SQLDB-\<databas namn >-\<miljö\>| <ul><li>SQLDB – användare-Prod </li><li>SQLDB – användare – dev</li></ul>               |
| Azure Cosmos DB                     | Global             | Cosmos-\<app-namn\>-\<miljö\>   | <ul><li>Cosmos – Navigator-Prod </li><li>Cosmos-utsläpp – dev</li></ul>       |
| Azure Cache for Redis               | Global             | redis-\<App Name\>-\<Environment\>    | <ul><li>redis-navigator-prod </li><li>redis-emissions-dev</li></ul>       |
| Azure Database for MySQL            | Global             | mysql-\<App Name\>-\<Environment\>    | <ul><li>mysql-navigator-prod </li><li>mysql-emissions-dev</li></ul>       |
| Azure Database for PostgreSQL       | Global             | psql-\<app-namn\>-\<miljö\>     | <ul><li>psql – Navigator-Prod </li><li>psql-utsläpp – dev</li></ul>         |
| Azure SQL Data Warehouse            | Global             | sqldw-\<App Name\>-\<Environment\>    | <ul><li>sqldw-navigator-prod </li><li>sqldw-emissions-dev</li></ul>       |
| SQL Server Stretch Database         | Azure SQL Database | -\<App Name\>-\<Environment\> | <ul><li>sqlstrdb-navigator-prod </li><li>sqlstrdb-emissions-dev</li></ul> |

### <a name="storage"></a>Storage

| Tillgångstyp                              | Omfång  | Format                                                                        | Exempel                                   |
|-----------------------------------------|--------|-------------------------------------------------------------------------------|--------------------------------------------|
| Azure Storage-konto – allmän användning     | Global | st\<storage name\>\<\#\#\#\>                                                  | <ul><li>stnavigatordata001 </li><li>stemissionsoutput001</li></ul>    |
| Azure Storage-konto – diagnostikloggar | Global | stdiag\<första två bokstäverna i prenumerationsnamnet och numret\>\<region\>\<\#\#\#\> | <ul><li>stdiagsh001eastus2001 </li><li>stdiagsh001westus001</li></ul> |
| Azure StorSimple                        | Global | ssimp\<App Name\>\<Environment\>                                              | <ul><li>ssimpnavigatorprod </li><li>ssimpemissionsdev</li></ul>       |

### <a name="ai--machine-learning"></a>AI + Machine Learning

| Tillgångstyp                       | Omfång          | Format                            | Exempel                               |
|----------------------------------|----------------|-----------------------------------|----------------------------------------|
| Azure Search                     | Global         | srch-\<App Name\>-\<Environment\> | <ul><li>srch-navigator-prod </li><li>srch-emissions-dev</li></ul> |
| Azure Cognitive Services         | Resursgrupp | kugg hjuls-\<app-namn\>-\<miljö\>   | <ul><li>kugg hjuls – Navigator-Prod </li><li>kugg hjuls-utsläpp – dev</li></ul>     |
| Azure Machine Learning-arbetsyta | Resursgrupp | mlw-\<app-namn\>-\<miljö\>   | <ul><li>mlw – Navigator-Prod </li><li>mlw-utsläpp – dev</li></ul>     |

### <a name="analytics"></a>Analytics

| Tillgångstyp                | Omfång  | Format                             | Exempel                                 |
|---------------------------|--------|------------------------------------|------------------------------------------|
| Azure Data Factory        | Global | ADF –\<app-namn\>\<miljö\>    | <ul><li>ADF – Navigator – Prod </li><li>ADF – utsläpp – dev</li></ul>     |
| Azure Data Lake Storage   | Global | dls\<App Name\>\<Environment\>     | <ul><li>dlsnavigatorprod </li><li>dlsemissionsdev</li></ul>         |
| Azure Data Lake Analytics | Global | dla\<App Name\>\<Environment\>     | <ul><li>dlanavigatorprod </li><li>dlaemissionsdev</li></ul>         |
| Azure HDInsight – Spark   | Global | hdis-\<App Name\>-\<Environment\>  | <ul><li>hdis-navigator-prod </li><li>hdis-emissions-dev </li></ul>  |
| Azure HDInsight – Hadoop  | Global | hdihd-\<App Name\>-\<Environment\> | <ul><li>hdihd-hadoop-prod </li><li>hdihd-emissions-dev</li></ul>    |
| Azure HDInsight – R Server| Global | hdir-\<App Name\>-\<Environment\>  | <ul><li>hdir-navigator-prod </li><li>hdir-emissions-dev</li></ul>   |
| Azure HDInsight – HBase   | Global | hdihb-\<App Name\>-\<Environment\> | <ul><li>hdihb-navigator-prod </li><li>hdihb-emissions-dev</li></ul> |
| Power BI Embedded         | Global | PBI-\<app-namn\>\<miljö\>    | <ul><li>PBI – Navigator-Prod </li><li>PBI-utsläpp – dev</li></ul> |

### <a name="data-streams--internet-of-things-iot"></a>Data strömmar/Sakernas Internet (IoT)

| Tillgångstyp                         | Omfång          | Format                             | Exempel                                 |
|------------------------------------|----------------|------------------------------------|------------------------------------------|
| Azure Stream Analytics             | Resursgrupp | asa-\<App Name\>-\<Environment\>   | <ul><li>asa-navigator-prod </li><li>asa-emissions-dev</li></ul>     |
| Azure IoT Hub                      | Global         | IoT-\<app-namn\>-\<miljö\>   | <ul><li>IoT-Navigator-Prod </li><li>IoT – utsläpp – dev</li></ul>     |
| Azure Event Hubs                   | Global         | evh-\<App Name\>-\<Environment\>   | <ul><li>evh-navigator-prod </li><li>evh-emissions-dev</li></ul>     |
| Azure Notification Hubs            | Resursgrupp | NTF-\<app-namn\>-\<miljö\>   | <ul><li>NTF – Navigator-Prod </li><li>NTF-utsläpp – dev</li></ul>     |
| Azure Notification Hubs-namnområde  | Global         | ntfns-\<app-namn\>-\<miljö\> | <ul><li>ntfns – Navigator-Prod </li><li>ntfns-utsläpp – dev</li></ul> |
