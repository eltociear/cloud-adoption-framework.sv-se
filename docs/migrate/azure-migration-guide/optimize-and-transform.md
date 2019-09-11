---
title: Optimera och transformera
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Optimera och transformera
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: c44bcd45783ee6ea61bbbe33b6b76ce7034eca2c
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818905"
---
# <a name="optimize-and-transform"></a>Optimera och transformera

Nu när du har migrerat dina tjänster till Azure, tar nästa fas vid där du ska granska lösningen för möjliga optimeringsområden. Det kan till exempel innebära granskning av lösningens design, anpassning av tjänsternas storlek och kostnadsanalys.

Den här fasen är också en möjlighet att optimera din miljö och genomföra eventuella omvandlingar av miljön. Till exempel kanske du har utfört en migrering av typen ”rehost”, och när dina tjänster nu körs på Azure kan du gå tillbaka till lösningskonfigurationen eller de förbrukade tjänsterna och eventuellt utföra viss ”omstrukturering”, i syfte att modernisera och förbättra lösningens funktioner.

# <a name="right-size-assetstaboptimize"></a>[Rätt storlek på tillgångarna](#tab/optimize)

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

Observera att ändring av storleken på virtuella datorer för produktion kan orsaka avbrott i tjänsten. Försök att välja rätt storlek för dina virtuella datorer innan du flyttar upp dem till produktion.


::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

- [Hantera reservationer för Azure-resurser](/azure/billing/billing-manage-reserved-vm-instance)
- [Ändra storlek på en virtuell Windows-dator](/azure/virtual-machines/windows/resize-vm)
- [Ändra storlek på en virtuell Linux-dator med Azure CLI](/azure/virtual-machines/linux/change-vm-size)

Partner kan använda Partner Center för att granska användningen.

- [Storleksändring av virtuell Microsoft Azure-dator för maximal reservationsanvändning](/partner-center/azure-usage)

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

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Sql%2Fservers%2Fdatabases]" submitText="Go to SQL Databases" :::

::: zone-end

# <a name="cost-managementtabmanagecost"></a>[Kostnadshantering](#tab/ManageCost)

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

- [Självstudier: Optimera kostnader utifrån rekommendationer](/azure/cost-management/tutorial-acm-opt-recommendations)
- [Förhindra oväntade avgifter med Azure-fakturering och kostnadshantering](/azure/billing/billing-getting-started)
- [Utforska och analysera kostnader med kostnadsanalys](/azure/cost-management/quick-acm-cost-analysis)

::: zone-end
