---
title: 'Redo: Rekommenderade regler för namngivning och taggar'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Den här artikeln innehåller detaljerad information om resursnamn och taggar som bidrar till molnimplementeringen för företag.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: readiness
ms.openlocfilehash: 61d0ff1dc1967656a30b8583acf5b7f7d9d0759f
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70819782"
---
# <a name="ready-recommended-naming-and-tagging-conventions"></a>Redo: Rekommenderade regler för namngivning och taggar

Omorganisation av molnbaserade resurser på sätt som bidrar till driftsstyrning och som kan hantera redovisningskrav är en utmaning som är vanlig vid en övergång till molnet. Genom att använda väldefinierade system för namngivning och metadatataggar för molnbaserade resurser kan IT-personal snabbt hitta och hantera resurser. Väldefinierade namn och taggar bidrar också till att samordna molnkostnaderna med företagets team genom att använda redovisningsmekanismer som debiterar eller visar utgifter för avdelningar.

Azure Architecture Centers [namnkonventioner för Azure-resurser](/azure/architecture/best-practices/naming-conventions) innehåller allmänna rekommendationer om namngivningskonventioner och diskussioner om namngivningsbegränsningar och regler för plattformar. Följande diskussion utökar den allmänna vägledningen med mer detaljerade rekommendationer som syftar till att ge stöd för företags molnimplementeringar.

Resursnamn kan vara svåra att ändra. Be dina molnimplementeringsteam att prioritera att etablera en omfattande namngivningskonvention innan du påbörjar en omfattande molndistribution.

> [!NOTE]
> Alla företag har olika organisations- och hanteringskrav. Rekommendationerna i den här artikeln fungerar som en utgångspunkt för diskussioner i dina molnimplementeringsteam.
>
> Medan dessa diskussioner pågår kan du använda följande mall för att avbilda namngivnings- och etikettbesluten du fattar när du anpassar dessa rekommendationer till dina specifika företagsbehov.
>
> Ladda ned [mall för namngivnings- och etikettkonventionspårning](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx).

## <a name="naming-and-tagging-resources"></a>Namngivnings- och etikettresurser

En namngivnings- och etikettstrategi omfattar information om företaget och verksamheten, såsom delar av resursnamn och metadatataggar:

- Den affärsrelaterade sidan av denna strategi säkerställer att resursnamn och taggar innehåller den organisatoriska information som krävs för att identifiera teamen. Använd en resurs tillsammans med företagsägare som ansvarar för resurskostnader.
- Den driftrelaterade sidan garanterar att namn och taggar innehåller information som IT-teamet använder för att identifiera arbetsbelastning, program, miljö, allvarsgrad och annan information som är användbar för att hantera resurser.

### <a name="resource-naming"></a>Resursnamngivning

En lämplig namngivningskonvention sätter samman resursnamn genom att använda viktig resursinformation som delar av resursens namn. Med de rekommenderade namngivningskonventionerna som beskrivs [längre fram i den här artikeln](#sample-naming-convention) har en offentlig IP-resurs för en SharePoint-arbetsbelastning följande namn: `pip-sharepoint-prod-westus-001`.

Från namnet kan du snabbt identifiera resurstypen, dess associerade arbetsbelastning, distributionsmiljön och den Azure-region som är värd för den.

#### <a name="naming-scope"></a>Namngivningsomfång

Alla typer av Azure-resurser har ett omfång som definierar hur dessa tillgångar kan hanteras i förhållande till andra resurstyper. När det gäller namngivningskonventioner innebär detta att en resurs måste ha ett unikt namn inom dess omfång.

Ett virtuellt nätverk har till exempel en resursgrupps omfång, vilket innebär att det bara kan finnas ett nätverk med namnet `vnet-prod-westus-001` i en specifik resursgrupp. Andra resursgrupper kan ha sitt eget virtuella nätverk med namnet `vnet-prod-westus-001`. Ett annat exempel är undernät, som är begränsade till virtuella nätverk. Det innebär att varje undernät inom ett virtuellt nätverk måste ha ett unikt namn.

Vissa resursnamn, till exempel PaaS-tjänster med offentliga slutpunkter eller DNS-taggar för virtuella datorer har globala omfång, vilket innebär att de måste vara unika för hela Azure-plattformen.

Resursnamnen har längdbegränsningar. Det är viktigt att avväga innehållet i ett namn med dess omgång och längd när du utformar din namngivningskonvention. Mer information om namngivningsregler för tillåtna tecken, omfattningar och namnlängder för resurstyper finns i [Namngivningskonventioner för Azure-resurser.](/azure/architecture/best-practices/naming-conventions)

#### <a name="recommended-naming-components"></a>Rekommenderade namndelar

När du utformar din namngivningskonvention ska du identifiera viktig information som du vill visa i ett resursnamn. Olika typer av information är relevanta för olika resurstyper. Följande lista innehåller exempel på information som är användbar när du skapar resursnamn.

Se till att namndelarnas längd inte överskrider gränsen för resursnamn.

| Namndel | Beskrivning | Exempel |
| --- | --- | --- |
| Affärsenhet | Avdelning på toppnivå för ditt företag som äger prenumerationen eller arbetsbelastningen som resursen tillhör. I mindre organisationer kan den här komponenten representera en enskild avdelning. | *fin*, *mktg*, *product*, *it*, *corp* |
| Prenumerationstyp | Sammanfattande beskrivning av syftet med den prenumeration som innehåller resursen. Delas ofta upp enligt typ av distributionsmiljö eller specifika arbetsbelastningar. | *Prod,* s*hared, client* |
| Namn på program eller tjänst | Namnet på programmet, arbetsbelastningen eller tjänsten som resursen ingår i. | *navigator*, *emissions*, *sharepoint*, *hadoop* |
| Distributionsmiljö | Stadiet i utvecklingslivscykeln för arbetsbelastningen som stöds av resursen. | *prod, dev, qa, stage, test* |
| Region | Den Azure-region där resursen har distribuerats. | *westus, eastus2, westeurope, usgovia* |

#### <a name="recommended-resource-type-prefixes"></a>Rekommenderade prefix för resurstyp

Varje arbetsbelastning kan bestå av många enskilda resurser och tjänster. Om du använder prefix för resurstyp i dina resursnamn är det enklare att identifiera program- eller tjänstkomponenter.

I följande lista visas rekommenderade prefix för Azure-resurstyper som du kan använda när du definierar namnkonventionerna.

| Resurstyp                       | Resursnamnprefix |
| ----------------------------------- | -------------------- |
| Resource group                      | rg-                  |
| Azure Virtual Network                     | vnet-                |
| Virtuell nätverksgateway             | vnet-gw-             |
| Gateway-anslutning                  | cn-                  |
| Subnet                              | snet-                |
| Nätverkssäkerhetsgrupp              | nsg-                 |
| Azure virtuella maskiner                    | vm-                  |
| Lagringskonto för virtuell dator                  | stvm                 |
| Offentlig IP                           | pip-                 |
| Azure Load Balancer                       | lb-                  |
| NIC                                 | nic-                 |
| Azure Service Bus                         | sb-                  |
| Azure Service Bus-köer                  | sbq-                 |
| Azure App Service-appar                    | azapp-               |
| Azure Functions-appar                       | azfun-               |
| Azure Cloud Services                      | azcs-                |
| Azure SQL Database                  | sqldb-               |
| Azure Cosmos DB (tidigare Azure DocumentDB) | cosdb-               |
| Azure Cache for Redis               | redis-               |
| Azure Database for MySQL            | mysql-               |
| Azure SQL Data Warehouse                  | sqldw-               |
| SQL Server Stretch Database         | sqlstrdb-            |
| Azure Storage                       | stor                 |
| Azure StorSimple                          | ssimp                |
| Azure Search                        | srch-                |
| Azure Cognitive Services                  | cs-                  |
| Azure Machine Learning-arbetsyta    | aml-                 |
| Azure Data Lake Storage             | DLS                  |
| Azure Data Lake Analytics           | dla                  |
| Azure HDInsight – Spark                   | hdis-                |
| Azure HDInsight – Hadoop                  | hdihd-               |
| Azure HDInsight – R Server                | hdir-                |
| Azure HDInsight – HBase                   | hdihb-               |
| Inbäddat Power BI                   | pbiemb               |
| Azure Stream Analytics                    | asa-                 |
| Azure Data Factory                        | df-                  |
| Azure Event Hubs                           | evh-                 |
| Azure IoT Hub                       | aih-                 |
| Azure Notification Hubs                   | anh-                 |
| Azure Notification Hubs-namnområde          | anhns-               |

### <a name="metadata-tags"></a>Metadatataggar

Om du använder metadatataggar med i dina molnresurser kan du inkludera information om tillgångar som inte kunde inkluderas i resursnamnet. Du kan använda den informationen till att utföra mer avancerad filtrering och rapportering av resurser. Du vill att dessa taggar ska innehålla sammanhang om resursens associerade arbetsbelastning eller program, driftkrav och ägarskapsinformation. Den här informationen kan användas av IT-avdelningen eller affärsteam för att hitta resurser eller generera rapporter om resursanvändning och fakturering.

De taggar som du fäster på resurser och de taggar som behövs eller är valfria varierar mellan olika organisationer. Följande lista innehåller exempel på vanliga taggar som speglar viktiga sammanhang och information om en resurs. Använd den här listan som utgångspunkt för att upprätta egna taggkonventioner.

| Taggnamn                  | Beskrivning                                                                                                                                                                                                    | Nyckel               | Exempelvärde                                   |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------|
| Programnamn          | Namnet på programmet, tjänsten eller arbetsbelastningen som resursen är associerad med.                                                                                                                                 | *ApplicationName* | *{appnamn}*                                    |
| Godkännarens namn             | Person som ansvarar för att godkänna kostnader relaterade till den här resursen.                                                                                                                                               | *Approver*        | *{e-post}*                                       |
| Budget krävs/godkänd  | Pengar som har tilldelats programmet, tjänsten eller arbetsbelastningen.                                                                                                                                                    | *BudgetAmount*    | *{\$}*                                          |
| Affärsenhet             | Avdelning på toppnivå för ditt företag som äger prenumerationen eller arbetsbelastningen som resursen tillhör. I mindre organisationer kan den här taggen representera en enskild avdelning. | *BusinessUnit*    | *EKONOMI, MARKNADSFÖRING, {produktnamn}, CORP, DELAD* |
| Kostnadsställe               | Kostnadsställe som associeras med resursen.                                                                                                                                                          | *CostCenter*      | *{värde}*                                      |
| Haveriberedskap         | Programmet, arbetsbelastningen eller tjänstens affärskritiskhet.                                                                                                                                                | *DR*              | *Verksamhetskritisk, Kritisk, Viktig*         |
| Projektets slutdatum   | Datum då programmet, arbetsbelastningen eller tjänsten har schemalagts för utsättning.                                                                                                                                  | *EndDate*         | *{datum}*                                        |
| Miljö               | Programmet, arbetsbelastningen eller tjänstens distributionsmiljö.                                                                                                                                              | *Env*             | *Prod, Dev, QA, Stage, Test*                    |
| Ägarens namn                | Programmet, arbetsbelastningen eller tjänstens ägare.                                                                                                                                                                | *Ägare*           | *{e-post}*                                       |
| Beställarens namn            | Användare som beställde utvecklingen av det här programmet.                                                                                                                                                          | *Requestor*       | *{e-post}*                                       |
| Tjänsteklass             | Serviceavtalsnivå för programmet, arbetsbelastningen eller tjänsten.                                                                                                                                       | *ServiceClass*    | *Dev, Brons, Silver, Guld*                     |
| Projektets startdatum | Datum då programmet, arbetsbelastningen eller tjänsten först distribuerades.                                                                                                                                           | *StartDate*       | *{datum}*                                        |

## <a name="sample-naming-convention"></a>Exempel på namngivningskonvention

I följande avsnitt finns exempel på namngivningssystem för vanliga typer av Azure-resurser som distribueras i samband med en molndistribution för företag.

### <a name="subscriptions"></a>Prenumerationer

| Tillgångstyp   | Omfång                        | Format                                             | Exempel                                     |
|--------------|------------------------------|----------------------------------------------------|----------------------------------------------|
| Subscription | Konto/företagsavtal | \<Affärsenhet\>-\<Prenumerationstyp\>-\<\#\#\#\> | <ul><li>mktg-prod-001 </li><li>corp-shared-001 </li><li>fin-client-001</li></ul> |

### <a name="resource-groups"></a>Resursgrupper

| Tillgångstyp     | Omfång        | Format                                                     | Exempel                                                                            |
|----------------|--------------|------------------------------------------------------------|-------------------------------------------------------------------------------------|
| Resource group | Subscription | rg-\<App / Service name\>-\<Subscription type\>-\<\#\#\#\> | <ul><li>rg-mktgsharepoint-prod-001 </li><li>rg-acctlookupsvc-share-001 </li><li>rg-ad-dir-services-shared-001</li></ul> |

### <a name="virtual-networking"></a>Virtuellt nätverk

| Tillgångstyp               | Omfång           | Format                                                                | Exempel                                                                                              |
|--------------------------|-----------------|-----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| Azure Virtual Network          | Resource group  | vnet-\<Subscription type\>-\<Region\>-\<\#\#\#\>                      | <ul><li>vnet-shared-eastus2-001 </li><li>vnet-prod-westus-001 </li><li>vnet-client-eastus2-001</li></ul>                                  |
| Virtuell gateway för virtuellt nätverk     | Virtuellt nätverk | vnet-gw-v-\<Subscription type\>-\<Region\>-\<\#\#\#\>                 | <ul><li>vnet-gw-v-shared-eastus2-001 </li><li>vnet-gw-v-prod-westus-001 </li><li>vnet-gw-v-client-eastus2-001</li></ul>                   |
| Virtuell lokal nätverksgateway       | Virtuell gateway | vnet-gw-l-\<Subscription type\>-\<Region\>-\<\#\#\#\>                 | <ul><li>vnet-gw-l-shared-eastus2-001 </li><li>vnet-gw-l-prod-westus-001 </li><li>vnet-gw-l-client-eastus2-001</li></ul>                   |
| Plats-till-plats-anslutningar | Resource group  | cn-\<local gateway name\>-to-\<virtual gateway name\>                 | <ul><li>cn-l-gw-shared-eastus2-001-to-v-gw-shared-eastus2-001 </li><li>cn-l-gw-shared-eastus2-001-to-shared-westus-001</li></ul> |
| Anslutningar till virtuellt nätverk         | Resource group  | cn-\<prenumeration1\>\<region1\>-till-\<prenumeration2\>\<region2\>-      | <ul><li>cn-shared-eastus2-to-shared-westus </li><li>cn-shared-eastus2-to-shared-westus</li></ul>                                     |
| Subnet                   | Virtuellt nätverk | snet-\<subscription\>-\<subregion\>-\<\#\#\#\>                       | <ul><li>snet-shared-eastus2-001 </li><li>snet-prod-westus-001 </li><li>snet-client-eastus2-001</li></ul>                                  |
| Nätverkssäkerhetsgrupp   | Undernät eller NIC   | nsg-\<policy name or appname\>-\<\#\#\#\>                             | <ul><li>nsg-weballow-001 </li><li>nsg-rdpallow-001 </li><li>nsg-sqlallow-001 </li><li>nsg-dnsbloked-001</li></ul>                                  |
| Offentlig IP                | Resource group  | pip-\<vm name or app name\>-\<Environment\>-\<subregion\>-\<\#\#\#\> | <ul><li>pip-dc1-shared-eastus2-001 </li><li>pip-hadoop-prod-westus-001</li></ul>                                                 |

### <a name="azure-virtual-machines"></a>Azure virtuella maskiner

| Tillgångstyp         | Omfång          | Format                                                              | Exempel                                                                             |
|--------------------|----------------|---------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Azure virtuella maskiner    | Resource group | vm\<policy name or appname\>\<\#\#\#\>                              | <ul><li>vmnavigator001 </li><li>vmsharepoint001 </li><li>vmsqlnode001 </li><li>vmhadoop001</li></ul>                              |
| Lagringskonto för virtuell dator | Global         | stvm\<performance type\>\<appname or prodname\>\<region\>\<\#\#\#\> | <ul><li>stvmstcoreeastus2001 </li><li>stvmpmcoreeastus2001 </li><li>stvmstplmeastus2001 </li><li>stvmsthadoopeastus2001</li></ul> |
| DNS-etikett          | Global         | \<En post för en virtuell dator\>.[\<region\>.cloudapp.azure.com]                  | <ul><li>dc1.westus.cloudapp.azure.com </li><li>web1.eastus2.cloudapp.azure.com</li></ul>                        |
| Azure Load Balancer      | Resource group | lb-\<app name or role\>\<Environment\>\<\#\#\#\>                    | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-dev-001</li></ul>                                          |
| NIC                | Resource group | nic-\<\#\#\>-\<vmname\>-\<subscription\>\<\#\#\#\>                  | <ul><li>nic-01-dc1-shared-001 </li><li>nic-02-vmhadoop1-prod-001 </li><li>nic-02-vmtest1-client-001</li></ul>            |

### <a name="paas-services"></a>PaaS-tjänster

| Tillgångstyp     | Omfång  | Format                                                              | Exempel                                                                                 |
|----------------|--------|---------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| Azure App Service    | Global | azapp-\<App Name\>-\<Environment\>-\<\#\#\#\>.[{azurewebsites.net}] | <ul><li>azapp-navigator-prod-001.azurewebsites.net </li><li>azapp-accountlookup-dev-001.azurewebsites.net</li></ul> |
| Azure Functions App   | Global | azfun-\<App Name\>-\<Environment\>-\<\#\#\#\>.[{azurewebsites.net}] | <ul><li>azfun-navigator-prod-001.azurewebsites.net </li><li>azfun-accountlookup-dev-001.azurewebsites.net</li></ul> |
| Azure Cloud Services | Global | azcs-\<App Name\>-\<Environment\>-\<\#\#\#\>.[{cloudapp.net}]       | <ul><li>azcs-navigator-prod-001.azurewebsites.net </li><li>azcs-accountlookup-dev-001.azurewebsites.net</li></ul>   |

### <a name="azure-service-bus"></a>Azure Service Bus

| Tillgångstyp         | Omfång       | Format                                                     | Exempel                           |
|--------------------|-------------|------------------------------------------------------------|------------------------------------|
| Azure Service Bus        | Global      | sb-\<App Name\>-\<Environment\>.[{servicebus.windows.net}] | <ul><li>sb-navigator-prod </li><li>sb-emissions-dev</li></ul> |
| Azure Service Bus-köer | Service Bus | sbq-\<query descriptor\>                                   | <ul><li>sbq-messagequery</li></ul>                   |

### <a name="databases"></a>Databaser

| Tillgångstyp                          | Omfång              | Format                                | Exempel                                       |
|-------------------------------------|--------------------|---------------------------------------|------------------------------------------------|
| Azure SQL Database                  | Global             | sqldb-\<App Name\>-\<Environment\>    | <ul><li>sqldb-navigator-prod </li><li>sqldb-emissions-dev</li></ul>       |
| Azure Cosmos DB (tidigare Azure DocumentDB) | Global             | cosdb-\<App Name\>-\<Environment\>    | <ul><li>cosdb-navigator-prod </li><li>cosdb-emissions-dev</li></ul>       |
| Azure Cache for Redis               | Global             | redis-\<App Name\>-\<Environment\>    | <ul><li>redis-navigator-prod </li><li>redis-emissions-dev</li></ul>       |
| Azure Database for MySQL            | Global             | mysql-\<App Name\>-\<Environment\>    | <ul><li>mysql-navigator-prod </li><li>mysql-emissions-dev</li></ul>       |
| Azure SQL Data Warehouse                  | Global             | sqldw-\<App Name\>-\<Environment\>    | <ul><li>sqldw-navigator-prod </li><li>sqldw-emissions-dev</li></ul>       |
| SQL Server Stretch Database         | Azure SQL Database | -\<App Name\>-\<Environment\> | <ul><li>sqlstrdb-navigator-prod </li><li>sqlstrdb-emissions-dev</li></ul> |

### <a name="storage"></a>Storage

| Tillgångstyp                              | Omfång  | Format                                                                        | Exempel                                   |
|-----------------------------------------|--------|-------------------------------------------------------------------------------|--------------------------------------------|
| Azure Storage-konto – allmän användning     | Global | st\<storage name\>\<\#\#\#\>                                                  | <ul><li>stnavigatordata001 </li><li>stemissionsoutput001</li></ul>    |
| Azure Storage-konto – diagnostikloggar | Global | stdiag\<första två bokstäverna i prenumerationsnamnet och numret\>\<region\>\<\#\#\#\> | <ul><li>stdiagsh001eastus2001 </li><li>stdiagsh001westus001</li></ul> |
| Azure StorSimple                              | Global | ssimp\<App Name\>\<Environment\>                                              | <ul><li>ssimpnavigatorprod </li><li>ssimpemissionsdev</li></ul>       |

### <a name="ai--machine-learning"></a>AI + Machine Learning

| Tillgångstyp                       | Omfång          | Format                            | Exempel                               |
|----------------------------------|----------------|-----------------------------------|----------------------------------------|
| Azure Search                     | Global         | srch-\<App Name\>-\<Environment\> | <ul><li>srch-navigator-prod </li><li>srch-emissions-dev</li></ul> |
| Azure Cognitive Services               | Resource group | cs-\<App Name\>-\<Environment\>   | <ul><li>cs-navigator-prod </li><li>cs-emissions-dev</li></ul>     |
| Azure Machine Learning-arbetsyta | Resource group | aml-\<App Name\>-\<Environment\>  | <ul><li>aml-navigator-prod </li><li>aml-emissions-dev</li></ul>   |

### <a name="analytics"></a>Analytics

| Tillgångstyp                | Omfång  | Format                             | Exempel                                 |
|---------------------------|--------|------------------------------------|------------------------------------------|
| Azure Data Factory        | Global | df-\<App Name\>\<Environment\>     | <ul><li>df-navigator-prod </li><li>df-emissions-dev</li></ul>       |
| Azure Data Lake Storage   | Global | dls\<App Name\>\<Environment\>     | <ul><li>dlsnavigatorprod </li><li>dlsemissionsdev</li></ul>         |
| Azure Data Lake Analytics | Global | dla\<App Name\>\<Environment\>     | <ul><li>dlanavigatorprod </li><li>dlaemissionsdev</li></ul>         |
| Azure HDInsight – Spark         | Global | hdis-\<App Name\>-\<Environment\>  | <ul><li>hdis-navigator-prod </li><li>hdis-emissions-dev </li></ul>  |
| Azure HDInsight – Hadoop        | Global | hdihd-\<App Name\>-\<Environment\> | <ul><li>hdihd-hadoop-prod </li><li>hdihd-emissions-dev</li></ul>    |
| Azure HDInsight – R Server      | Global | hdir-\<App Name\>-\<Environment\>  | <ul><li>hdir-navigator-prod </li><li>hdir-emissions-dev</li></ul>   |
| Azure HDInsight – HBase         | Global | hdihb-\<App Name\>-\<Environment\> | <ul><li>hdihb-navigator-prod </li><li>hdihb-emissions-dev</li></ul> |
| Inbäddat Power BI         | Global | pbiemb\<App Name\>\<Environment\>  | <ul><li>pbiem-navigator-prod </li><li>pbiem-emissions-dev</li></ul> |

### <a name="internet-of-things-iot"></a>Sakernas Internet (IoT)

| Tillgångstyp                         | Omfång          | Format                             | Exempel                                 |
|------------------------------------|----------------|------------------------------------|------------------------------------------|
| Azure Stream Analytics på IoT Edge | Resource group | asa-\<App Name\>-\<Environment\>   | <ul><li>asa-navigator-prod </li><li>asa-emissions-dev</li></ul>     |
| Azure IoT Hub                      | Global         | aih-\<App Name\>-\<Environment\>   | <ul><li>asa-navigator-prod </li><li>aih-emissions-dev</li></ul>     |
| Azure Event Hubs                          | Global         | evh-\<App Name\>-\<Environment\>   | <ul><li>evh-navigator-prod </li><li>evh-emissions-dev</li></ul>     |
| Azure Notification Hubs                   | Resource group | anh-\<App Name\>-\<Environment\>   | <ul><li>evh-navigator-prod </li><li>evh-emissions-dev</li></ul>     |
| Azure Notification Hubs-namnområde         | Global         | anhns-\<App Name\>-\<Environment\> | <ul><li>anhns-navigator-prod </li><li>anhns-emissions-dev</li></ul> |
