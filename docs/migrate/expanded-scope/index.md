---
title: Checklista för molnmigrering med utökat omfång
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Checklista för molnmigrering med utökat omfång
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: ee164f75b4f3748fce027d0c6c98db5200dcdd71
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548496"
---
# <a name="expanded-scope-for-cloud-migration"></a>Utökat omfång för molnmigrering

[Azure-migreringsguiden](../azure-migration-guide/index.md) i Cloud Adoption Framework är den rekommenderade startpunkten för läsare som är intresserade av en värdbytesmigrering till Azure, vilket även kallas ”lift and shift”-migrering. Guiden vägleder dig genom ett antal förutsättningar, verktyg och metoder för att migrera virtuella datorer till molnet.

Den här guiden är en effektiv baslinje som du gör dig bekant med den här typen av migrering, men den inbegriper vissa antaganden. Dessa antaganden gör guiden relevant för många som läser Cloud Adoption Framework genom att tillhandahålla en förenklad metod för migreringar. I det här Cloud Adoption Framework-avsnittet behandlas vissa migreringsscenarier med utökat omfång, vilket ger vägledning till projekt som de antagandena inte gäller för.

## <a name="cloud-migration-expanded-scope-checklist"></a>Checklista för molnmigrering med utökat omfång

I följande checklista visas vanliga komplexitetsområden som kan kräva att migreringens omfång utökas bortom [Azure-migreringsguiden](../azure-migration-guide/index.md).

### <a name="business-driven-scope-expansion"></a>En utökning av omfånget baserad på verksamheten

- **[Balansera portföljen](./balance-the-portfolio.md):** Teamet för molnstrategi är intresserade av att investera mer i migrering (värdbyte av befintliga arbetsbelastningar och program med minimala ändringar) eller innovation (refaktorisering eller återskapande av de arbetsbelastningar eller program som använder modern molnteknik). Ofta är balans mellan de två prioriteringarna nyckeln till framgång. I den här guiden balansering av portföljen för molnimplementering ett övergripande ämne som behandlas i varje migreringsprocess.
- **[Stöd för globala marknader](../../decision-guides/regions/index.md):** Verksamheten verkar i flera geografiska områden med olika krav för datasuveränitet. För att uppfylla de kraven bör ytterligare överväganden tas med i beräkningen för granskningen av förutsättningar och distributionen av tillgångar under migrering.

### <a name="technology-driven-scope-expansion"></a>En utökning av omfånget baserad på tekniken

- **[VMware-migrering](./vmware-host.md):** Migrering av VMware-värdar kan effektivisera migreringsprocessen. Varje migrerad VMware-värd kan flytta flera arbetsbelastningar till molnet med metoden ”lift and shift”. Efter migreringen kan de virtuella datorerna och arbetsbelastningarna stanna kvar i VMware eller migreras till modernare molnfunktioner.
- **[SQL Server-migrering](./sql-migration.md):** Migrering av SQL-servrar kan effektivisera migreringsprocessen. Varje migrerad SQL-server kan flytta flera databaser och tjänster, vilket kan effektivisera flytten av arbetsbelastningarna.
- **[Flera datacenter](./multiple-datacenters.md):** Att migrera flera datacenter ökar komplexiteten avsevärt. Under processerna för utvärdering, optimering och hantering måste ytterligare överväganden diskuteras så att de mer komplicerade miljöerna tas med i beräkningen.
- **[Datakraven överskrider nätverkskapaciteten](./network-capacity-exceeded.md):** Företag väljer ofta att migrera till molnet eftersom kapaciteten, hastigheten och stabiliteten hos ett befintligt datacenter inte längre räcker till. Tyvärr ökar dessa begränsningar komplexiteten i migreringsprocessen, vilket gör att ytterligare planering krävs under processerna för utvärdering och migrering.
- **[Strategi för styrning eller efterlevnad](./governance-or-compliance.md):** När styrning och efterlevnad är viktiga för att en migrering ska lyckas krävs ytterligare samarbete mellan IT-styrningsteamen och teamen för molnimplementering.

Om någon av dessa svårigheter förekommer i ditt scenario kommer det här Cloud Adoption Framework-avsnittet sannolikt att ge den typ av vägledning du behöver för att anpassa omfånget i migreringsprocesserna på rätt sätt.

Vart och ett av de här scenarierna behandlas av de olika artiklarna i det här Cloud Adoption Framework-avsnittet.

## <a name="next-steps"></a>Nästa steg

Bläddra i innehållsförteckningen till vänster för att åtgärda specifika behov eller omfångsändringar. Alternativt kan den första omfångsförbättringen i listan, [Balansera portföljen](./balance-the-portfolio.md), vara en bra utgångspunkt när du granskar de här scenarierna.

> [!div class="nextstepaction"]
> [Balansera portföljen](./balance-the-portfolio.md)
