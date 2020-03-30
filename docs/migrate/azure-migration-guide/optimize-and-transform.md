---
title: Optimera och flytta upp
description: Lär dig hur du granskar lösningen för möjliga optimeringsområden, till exempel lösningens design, anpassning av tjänsternas storlek och kostnadsanalys.
author: matticusau
ms.author: mlavery
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: eff32a369c55011cea8fb8ace2e7bfae28680eda
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80353874"
---
<!-- markdownlint-disable MD025 DOCSMD001 -->

# <a name="test-optimize-and-promote"></a>Testa, optimera och flytta upp

Nu när du har migrerat dina tjänster till Azure, tar nästa fas vid där du ska granska lösningen för möjliga optimeringsområden. Det kan till exempel innebära granskning av lösningens design, anpassning av tjänsternas storlek och kostnadsanalys.

Den här fasen är också en möjlighet att optimera din miljö och genomföra eventuella omvandlingar av miljön. Till exempel kanske du har utfört en migrering av typen ”rehost”, och när dina tjänster nu körs på Azure kan du gå tillbaka till lösningskonfigurationen eller de förbrukade tjänsterna och eventuellt utföra viss ”omstrukturering”, i syfte att modernisera och förbättra lösningens funktioner.

Resten av den här artikeln fokuserar på verktyg för att optimera den migrerade arbetsbelastningen. När balansen mellan prestanda och kostnad har uppnåtts är en arbetsbelastning redo att uppgraderas till produktion. Vägledning om kampanjalternativ finns i avsnittet om processförbättringar på [Optimera och flytta upp](../migration-considerations/optimize/index.md).

# <a name="right-size-assets"></a>[Rätt storlek på tillgångarna](#tab/optimize)

Storleken på alla Azure-tjänster som tillhandahåller en förbrukningsbaserad kostnadsmodell kan ändras via Azure Portal, CLI eller PowerShell. Det första steget för att korrigera storleken på en tjänst är att granska användningsstatistiken. Tjänsten Azure Monitor ger till gång till statistiken. Du kan behöva konfigurera insamlingen av mätvärden för tjänsten som du analyserar, och tillåta en lämplig tid för insamling av meningsfulla data baserat på mönstren i arbetsbelastningen.

1. Gå till **Övervaka**.
1. Välj **Mått** och konfigurera diagrammet så att det visar statistiken för tjänsten du ska analysera.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/metrics]" submitText="Go to Monitor" :::

::: zone-end

Här följer några vanliga tjänster som du kan ändra storlek på.

## <a name="resize-a-virtual-machine"></a>Ändra storlek på en virtuell dator

Azure Migrate analyserar den rätta storleken som en del av utvärderingsfasen inför migreringen, och virtuella datorer som migreras med det här verktyget kommer förmodligen redan att vara storleksanpassade baserat på migreringskraven.

För virtuella datorer som skapas eller migreras med andra metoder, eller i fall där kraven för virtuella datorer efter migreringen behöver ändras, kanske du vill anpassa storleken på den virtuella datorn ytterligare.

1. Gå till **Virtuella datorer**.
1. Välj den virtuella dator du vill använda i listan.
1. Välj **Storlek** och önskad ny storlek i listan. Du kan behöva justera filtren för att hitta den storlek du behöver.
1. Välj **Ändra storlek**.

Ändringar av storleken på virtuella datorer för produktion kan orsaka avbrott i tjänsten. Försök att välja rätt storlek för dina virtuella datorer innan du flyttar upp dem till produktion.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

- [Hantera reservationer för Azure-resurser](https://docs.microsoft.com/azure/billing/billing-manage-reserved-vm-instance)
- [Ändra storlek på en virtuell Windows-dator](https://docs.microsoft.com/azure/virtual-machines/windows/resize-vm)
- [Ändra storlek på en virtuell Linux-dator med Azure CLI](https://docs.microsoft.com/azure/virtual-machines/linux/change-vm-size)

Partner kan använda Partner Center för att granska användningen.

- [Storleksändring av virtuell Microsoft Azure-dator för maximal reservationsanvändning](https://docs.microsoft.com/partner-center/azure-usage)

::: zone-end

## <a name="resize-a-storage-account"></a>Ändra storlek på ett lagringskonto

1. Gå till **Lagringskonton**.
1. Välj önskat lagringskonto.
1. Välj **Konfigurera** och justera egenskaperna för lagringskontot så att de överensstämmer med dina krav.
1. Välj **Spara**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Storage%2FStorageAccounts]" submitText="Go to Storage Accounts" :::

::: zone-end

## <a name="resize-a-sql-database"></a>Ändra storlek på en SQL-databas

1. Gå till **SQL-databaser** eller **SQL-servrar** och välj sedan servern.
1. Välj den önskade databasen.
1. Välj **Konfigurera** och önskad ny storlek på tjänstnivå.
1. Välj **Använd**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Sql%2FServers%2FDatabases]" submitText="Go to SQL Databases" :::

::: zone-end

# <a name="cost-management"></a>[Kostnadshantering](#tab/ManageCost)

Det är viktigt att utföra löpande kostnadsanalys och granskning. Det ger dig möjlighet att ändra storlek på resurserna efter behov för att balansera kostnad och arbetsbelastning.

Azure Cost Management tillhandahåller tillsammans med Azure Advisor rekommendationer för kostnadsoptimering. Azure Advisor hjälper dig att optimera och förbättra effektiviteten genom att identifiera inaktiva och underutnyttjade resurser.

1. Välj **Kostnadshantering och fakturering**.
1. Välj **Advisor-rekommendationer** och **fliken** kostnader.
1. Använd **Påverkan** och **Potentiella årliga besparingar** för att granska potentiella fördelar.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/ModernBillingMenuBlade/Overview]" submitText="Go to Cost Management + Billing" :::

::: zone-end

Du kan också använda **Advisor** och välja fliken **Kostnader** för att identifiera rekommendationer för potentiella kostnadsminskningar.

> [!TIP]
> För tjänster som inte kräver kontinuerlig tillgänglighet kan du underlätta kostnadshanteringen genom att implementera en lösning för att starta, stoppa eller pausa tjänsten efter behov (till exempel virtuella Azure-datorer eller Azure SQL Data Warehouse).
>

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Expert/AdvisorBlade]" submitText="Go to Azure Advisor" :::

::: zone-end

::: zone target="docs"

- [Självstudier: Optimera kostnader utifrån rekommendationer](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations)
- [Förhindra oväntade avgifter med Azure-fakturering och kostnadshantering](https://docs.microsoft.com/azure/billing/billing-getting-started)
- [Utforska och analysera kostnader med kostnadsanalys](https://docs.microsoft.com/azure/cost-management/quick-acm-cost-analysis)

::: zone-end
