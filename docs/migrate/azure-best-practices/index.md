---
title: Bästa praxis för Azure-migrering
description: Använd Cloud Adoption Framework för Azure för att lära dig hur du implementerar de verktyg som behövs för att följa regelverket för migrering till molnet.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 22f2718775b194196f65672f0cbc1712d0a3a4ac
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433549"
---
# <a name="best-practices-for-cloud-migration"></a>Regelverk för migrering till molnet

[Azure-migreringsguiden](../azure-migration-guide/index.md) i Cloud Adoption Framework är den rekommenderade startpunkten om du är intresserad av migrering till Azure. Guiden vägleder dig genom ett antal verktyg och grundläggande metoder för att migrera virtuella datorer till molnet. Det här avsnittet av Cloud Adoption Framework beskriver många regelverk som går utöver de grundläggande molnbaserade verktygen.

## <a name="cloud-migration-best-practice-checklist"></a>Checklista för regelverk för migrering till molnet

I följande checklista visas vanliga komplexitetsområden som kan kräva att migreringens omfång utökas bortom [Azure-migreringsguiden](../azure-migration-guide/index.md).

### <a name="business-driven-scope-expansion"></a>En utökning av omfånget baserad på verksamheten

- **[Stöd för globala marknader](./multiple-regions.md):** Verksamheten verkar i flera geografiska områden med olika krav för datasuveränitet. För att uppfylla de kraven bör ytterligare överväganden tas med i beräkningen för granskningen av förutsättningar och distributionen av tillgångar under migrering.

### <a name="technology-driven-scope-expansion"></a>En utökning av omfånget baserad på tekniken

- **[VMware-migrering](./vmware-host.md):** Migrering av VMware-värdar kan effektivisera migreringsprocessen. Varje migrerad VMware-värd kan flytta flera arbetsbelastningar till molnet med metoden ”lift and shift”. Efter migreringen kan de virtuella datorerna och arbetsbelastningarna stanna kvar i VMware eller migreras till modernare molnfunktioner.
- **[SQL Server-migrering](./sql-migration.md):** Migrering av SQL-servrar kan effektivisera migreringsprocessen. Varje migrerad SQL-server kan flytta flera databaser och tjänster, vilket kan effektivisera flytten av arbetsbelastningarna.
- **[Flera datacenter](./multiple-datacenters.md):** Att migrera flera datacenter ökar komplexiteten avsevärt. Under processerna för utvärdering, optimering och hantering måste ytterligare överväganden diskuteras så att de mer komplicerade miljöerna tas med i beräkningen.
- **[Datakraven överskrider nätverkskapaciteten](./network-capacity-exceeded.md):** Företag väljer ofta att migrera till molnet eftersom kapaciteten, hastigheten och stabiliteten hos ett befintligt datacenter inte längre räcker till. Tyvärr ökar dessa begränsningar komplexiteten i migreringsprocessen, vilket gör att ytterligare planering krävs under processerna för utvärdering och migrering.
- **[Strategi för styrning eller efterlevnad](./governance-or-compliance.md):** När styrning och efterlevnad är viktiga för att en migrering ska lyckas krävs ytterligare samarbete mellan IT-styrningsteamen och teamen för molnimplementering.

Om någon av dessa svårigheter förekommer i ditt scenario kommer det här Cloud Adoption Framework-avsnittet sannolikt att ge den typ av vägledning du behöver för att anpassa omfånget i migreringsprocesserna på rätt sätt.

Vart och ett av de här scenarierna behandlas av de olika artiklarna i det här Cloud Adoption Framework-avsnittet.

## <a name="next-steps"></a>Nästa steg

Bläddra i innehållsförteckningen till vänster för att åtgärda specifika behov eller omfångsändringar. Alternativt kan den första omfångsförbättringen i listan, [Stöd för globala marknader](./multiple-regions.md), vara en bra utgångspunkt när du granskar de här scenarierna.

> [!div class="nextstepaction"]
> [Stöd för globala marknader](./multiple-regions.md)
