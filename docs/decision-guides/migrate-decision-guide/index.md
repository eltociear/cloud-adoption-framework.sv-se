---
title: Beslutsguide för migreringsverktyg
description: Använd det här beslutsträdet som ett hjälpmedel på hög nivå för valet av de bästa verktygen att använda enligt dina migreringsbeslut.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.openlocfilehash: f3d16455e3babc075bce671cfe867fedb2b4b6c7
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77708248"
---
# <a name="migration-tools-decision-guide"></a>Beslutsguide för migreringsverktyg

Den strategi och de verktyg som du använder för att migrera ett program till Azure beror huvudsakligen på dina affärsmål, teknikstrategier och tidslinjer samt på en djup förståelse för den faktiska arbetsbelastning och de tillgångar (infrastruktur, appar och data) som migreras. Följande beslutsträd är ett hjälpmedel på hög nivå för valet av de bästa verktygen att använda baserat på migreringsbeslut. Betrakta det här beslutsträdet som en utgångspunkt.

Valet att migrera med hjälp av tekniker för PaaS (plattform som en tjänst) eller IaaS (infrastruktur som en tjänst) drivs av balansen mellan kostnad, tid, befintlig teknisk skuld och långsiktiga resultat. IaaS är ofta den snabbaste vägen till molnet med ett minimum av nödvändiga ändringar av arbetsbelastningen. PaaS kan kräva ändringar i datastrukturer eller källkoden, men ger betydande långsiktiga fördelar i form av minskade driftskostnader och större teknisk flexibilitet. I följande diagram används termen _modernisera_ för att återspegla ett beslut att modernisera en tillgång under migrering och att migrera den moderniserade tillgången till en PaaS-plattform.

![Exempel på beslutsträd för migreringsverktyg.](../../_images/migrate/migration-tools-decision-tree.png)

## <a name="key-questions"></a>Viktiga frågor

Genom att besvara följande frågor kan du fatta beslut utifrån trädet ovan.

- **Skulle modernisering av programplattformen under migreringen vara en god investering av tid, energi och budget?** PaaS-tekniker som Azure App Service eller Azure Functions kan öka distributionsflexibiliteten och minska komplexiteten i att hantera virtuella datorer för att värdhantera program. Program kan dock behöva refaktorisering innan de kan dra nytta av dessa molnbaserade funktioner, vilket potentiellt ökar tidsåtgången och kostnaderna för ett migreringsprojekt. Om ditt program kan migrera till PaaS-tekniker med mycket få ändringar är det sannolikt en bra kandidat för modernisering. Om det skulle krävas omfattande refaktorisering kan en migrering med hjälp av IaaS-baserade virtuella datorer vara ett bättre alternativ.
- **Skulle modernisering av dataplattformen under migreringen vara en god investering av tid, energi och budget?** Som med programmigrering erbjuder Azure PaaS-hanterade lagringsalternativ som Azure SQL Database, Cosmos DB och Azure Storage betydande fördelar vad gäller hantering och flexibilitet, men migrering till dessa tjänster kan kräva refaktorisering av befintliga data och de program som använder dessa data. Dataplattformar kräver ofta betydligt mindre refaktorisering än programplattformen. Därför är det mycket vanligt att dataplattformen moderniseras även om programplattformen förblir som den är. Om dina data kan migreras till en hanterad datatjänst med mycket få ändringar utgör de en bra kandidat för modernisering. Data som skulle kräva omfattande tidsåtgång eller kostnader för refaktorisering för att kunna dra nytta av dessa PaaS-tjänster är kanske bättre att migrera med hjälp av IaaS-baserade virtuella datorer som stämmer bättre överens med befintliga värdfunktioner.
- **Körs ditt program för närvarande på dedikerade virtuella datorer eller delar det värdhantering med andra program?** Program som körs på dedikerade virtuella datorer kan enklare migreras till PaaS-hanteringsalternativ än program som körs på delade servrar.
- **Kommer din datamigrering att överskrida nätverksbandbredden?** Nätverkskapaciteten mellan dina lokala datakällor och Azure kan utgöra en flaskhals för datamigrering. Om de data du behöver överföra stöter på bandbreddsbegränsningar som förhindrar effektiv eller tidsenlig migrering kan du behöva överväga alternativa eller offlinebaserade överföringsmekanismer. Cloud Adoption Frameworks [artikel om migreringsreplikering](../../migrate/migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication) går igenom hur replikeringsbegränsningar kan påverka migreringsarbete. Som en del av din migreringsutvärdering bör du diskutera med IT-teamen för att kontrollera om din lokala bandbredd och WAN-bandbredden uppfyller migreringskraven. Se även [migreringsscenariot med utökat omfång för de tillfällen då lagringskrav överstiger nätverkskapaciteten under en migrering](../../migrate/expanded-scope/network-capacity-exceeded.md#suggested-prerequisites).
- **Använder ditt program en befintlig DevOps-pipeline?** I många fall kan Azure-pipelines enkelt refaktoriseras för distribution av program till molnbaserade värdmiljöer.
- **Har dina data komplexa krav för datalagring?** Produktionsprogram kräver vanligtvis datalagring som har hög tillgänglighet och erbjuder AlwaysOn-funktion samt liknande funktioner för tjänstens drifttid och kontinuitet. Azure PaaS-baserade alternativ för hanterad databas, till exempel Azure SQL Database, Azure Database for MySQL och Azure Cosmos DB, erbjuder serviceavtal med 99,99 % drifttid. På motsvarande sätt erbjuder IaaS-baserade SQL Server på virtuella Azure-datorer serviceavtal för enskilda instanser med en garanti på 99,95 %. Om dina data inte kan moderniseras till att använda PaaS-lagringsalternativ kommer en garanti för högre IaaS-drifttid att omfatta mer komplexa datalagringsscenarier såsom att köra SQL Server AlwaysOn-kluster och kontinuerligt synkronisera data mellan instanser. Detta kan innebära betydande värd- och hanteringskostnader. Därför är det viktigt att balansera krav på drifttid, moderniseringsarbetet och den övergripande budgetinverkan när du överväger alternativ för datamigrering.

## <a name="innovation-and-migration"></a>Innovation och migrering

I linje med Cloud Adoption Frameworks betoning på arbete med [inkrementell migrering](../../migrate/index.md#migration-implementation) utesluter inte ett inledande beslut om migreringsstrategi och verktyg framtida innovationsprojekt för att uppdatera ett program till att utnyttja möjligheter som erbjuds av Azure-plattformen. Ett stort inledande migreringsprojekt kan fokusera på värdbyte via en IaaS-metod, men du bör planera att regelbundet utvärdera din portfölj med molnhanterade program på nytt för att undersöka optimeringsmöjligheter.

## <a name="learn-more"></a>Läs mer

- **[Grunderna för molnet: Översikt över beräkningsalternativ i Azure](https://docs.microsoft.com/azure/architecture/guide/technology-choices/compute-overview):** Innehåller information om funktionerna i Azure IaaS- och PaaS-beräkningsalternativ.
- **[Grunderna för molnet: Välj rätt datalager](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview):** Beskriver PaaS-lagringsalternativ som finns tillgängliga på Azure-plattformen.
- **[Migrering med utökat omfång: Datakraven överskrider nätverkskapaciteten under ett migreringsprojekt](../../migrate/expanded-scope/network-capacity-exceeded.md):** Beskriver alternativa mekanismer för datamigrering för scenarier där datamigrering hindras av tillgänglig nätverksbandbredd.
- **[SQL Database: Välj rätt alternativ för SQL Server i Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas#business-motivations-for-choosing-databases-managed-instances-or-sql-virtual-machines):** Beskrivning av alternativen affärsmotiveringarna för valet att värdhantera dina SQL Server-arbetsbelastningar i en miljö med värdhanterad infrastruktur (IaaS) eller en värdhanterad tjänst (PaaS).
