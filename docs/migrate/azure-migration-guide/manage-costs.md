---
title: Mekanismer för migreringsfokuserad kostnadskontroll
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig hur du ställer in budgetar, betalningar och få bättre förståelse kring faktureringen av dina Azure-resurser.
author: bandersmsft
ms.author: banders
ms.date: 08/08/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: c6b195a69622a4934f257090650a8ba6ce884025
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024815"
---
# <a name="migration-focused-cost-control-mechanisms"></a>Mekanismer för migreringsfokuserad kostnadskontroll

Molnet medför ett par förändringar i hur vi arbetar, oavsett vår roll i det tekniska teamet. Kostnaden är ett bra exempel på den här ändringen. Tidigare behövde ekonomiavdelningen och IT-ledningen endast fundera på kostnaden för IT-tillgångar (infrastruktur, appar och data). Molnet ger varje medlem i den möjlighet att fatta och agera på beslut som bättre stöder slutanvändaren. Den möjligheten medför ett ansvar för att vara kostnadsmedveten när dessa beslut fattas.

Den här artikeln beskriver de verktyg som kan hjälpa dig att fatta vägrundade beslut före, under och efter en migrering till Azure.

Verktygen i den här artikeln omfattar:

> - Azure Migrate
> - Priskalkylator för Azure
> - TCO-kalkylator för Azure
> - Azure Cost Management
> - Azure Advisor

Processerna som beskrivs i den här artikeln kan också kräva ett partnerskap med IT-chefer, ekonomi eller affärsprogramägare. Information om hur du samarbetar med de här rollerna finns i artikeln Ramverk för molnimplementering om att upprätta en kostnadseffektiv organisation (som kommer under tredje kvartalet 2019).

<!-- markdownlint-disable MD024 MD025 -->

# <a name="estimate-vm-costs-prior-to-migrationtabestimatevmcosts"></a>[Beräkna molnkostnader för virtuella datorer före migreringen](#tab/EstimateVMCosts)

Före migreringen av en tillgång (infrastruktur, app eller data) finns det en möjlighet att uppskatta kostnader och begränsa storleken utifrån observerade prestandakriterier för dessa tillgångar. Uppskattning av kostnader har två syften: det tillåter kostnadskontroll och ger en kontrollpunkt för att säkerställa att den aktuella budgeten tar hänsyn till nödvändiga prestandakrav.

## <a name="cost-calculators"></a>Kostnadskalkylatorer

För manuella kostnadsberäkningar finns det två smidiga kalkylatorer som kan ge en snabb kostnadsuppskattning baserat på arkitekturens arbetsbelastning som ska migreras.

- [Priskalkylatorn](https://azure.microsoft.com/pricing/calculator) för Azure ger kostnadsberäkningar baserat på manuella registrerade Azure-produkter.
- Beslut kräver ibland en jämförelse av framtida molnkostnader och de aktuella lokala kostnaderna. [Kalkylatorn för total ägandekostnad (TCO)](https://azure.microsoft.com/pricing/tco/calculator) kan ge en sådan jämförelse.

Dessa manuella kostnadskalkylatorer kan användas fristående för att beräkna potentiella utgifter och besparingar. De kan också användas tillsammans med Azure Migrate kostnadsprognosverktyg för att justera kostnadsförväntningarna så att de passar alternativa arkitektur- eller prestandabegränsningar.

## <a name="azure-migrate-calculations"></a>Azure Migrate-beräkningar

**Krav:** Resten av den här fliken förutsätter att läsaren redan har fyllt i Azure Migrate med en samling tillgångar (infrastruktur, appar och data) som ska migreras. Föregående artikel om utvärderingar innehåller instruktioner om hur du samlar in inledande data. När data har fyllts följer du nästa steg för att uppskatta månadskostnaden baserat på de data som samlas in.

Azure Migrate beräknar **månatliga kostnader** baserat på data som samlas in av insamlaren och tjänstkartan. Följande steg läser in kostnadsuppskattningarna:

1. Gå till bladet Azure Migrate-utvärdering i portalen.
1. På projektsidan **Översikt** klickar du på **+Skapa utvärdering**.
1. Klicka på **Visa alla** för att granska utvärderingsegenskaperna.
1. Skapa gruppen och ange ett gruppnamn.
1. Välj de datorer som du vill lägga till i gruppen.
1. Klicka på **Skapa utvärdering** för att skapa gruppen och utvärderingen.
1. När utvärderingen har skapats kan du se den i Översikt > Instrumentpanel.
1. I området Bedömningsinformation i bladet navigering väljer du **Kostnadsinformation.**

Beräkningen som skapas och som visas nedan identifierar de månatliga kostnaderna för beräkning och lagring, vilket ofta utgör den största delen av molnkostnaderna.

![compute-storage-monthly-cost-estimate.png](./media/manage-costs/compute-storage-monthly-cost-estimate.png)
*Bild 1 – vyn Kostnadsinformation för en utvärdering i Azure Migrate.*

## <a name="additional-resources"></a>Ytterligare resurser

- [Ställa in och granska en utvärdering med Azure Migrate](https://docs.microsoft.com/azure/migrate/tutorial-assess-vmware#set-up-an-assessment)
- En mer omfattande plan om kostnadshantering över ett större antal tillgångar (infrastruktur, appar och data) finns i [styrningsmodellen i Ramverk för molnimplementering](../../govern/guides/index.md). I synnerhet riktlinjerna för [Cost Management-disciplin](../../govern/cost-management/index.md) och [förbättringar av Cost Management i handboken för stora företag](../../govern/guides/complex/cost-management-improvement.md).

# <a name="estimate-and-optimize-vm-costs-during-and-after-migrationtabestimateoptimize"></a>[Beräkna och optimera kostnader för virtuella datorer under och efter migrering](#tab/EstimateOptimize)

Om du uppskattar kostnaden före migrering får du ett konkret mål för kostnadsförväntningarna. Det ger också möjlighet att överväga prestanda- och kostnadsbehoven för varje tillgång (infrastruktur, appar och data) som ska migreras. Men det är fortfarande en uppskattning. När du har migrerat och belastat tillgången kan mer exakta kostnadsberäkningar utföras baserat på den faktiska eller syntetiska belastningen.

## <a name="azure-advisor-cost-recommendations"></a>Kostnadsrekommendationer från Azure Advisor

Inom 24 timmar efter migrering av tillgångar (infrastruktur, appar och data) till Azure börjar Azure Advisor övervaka varje tillgångs prestanda för att ge dig feedback om tillgången. En datapunkt från feedbacken handlar om balansen mellan kostnad och användning.

Följande steg innehåller kostnadsrekommendationer för tillgångar (infrastruktur, appar och data) i dina aktuella prenumerationer:

1. Gå till bladet **Azure Advisor** i portalen. I det vänstra navigeringsfönstret i Azure Portal klickar du på **Advisor**. Om du inte ser Advisor i den vänstra rutan väljer du **Alla tjänster**. I tjänstmenyfönstret under **Övervakning och hantering** väljer du **Advisor**.
1. Advisor-instrumentpanelen visar en sammanfattning av dina rekommendationer för alla valda prenumerationer. Du kan välja de prenumerationer som du vill att rekommendationerna ska visas för i listrutan prenumerationsfilter.
1. Om du vill se kostnadsrekommendationerna väljer du fliken Kostnad.

## <a name="azure-cost-management"></a>Azure Cost Management

Azure Cost Management kan ge en mer omfattande vy över utgiftsvanor, inklusive en detaljerad överblick över kostnader och utgiftstrender över tid. För stora eller komplexa migreringar kan den här vyn ge de insikter som krävs för att fatta generella beslut om kostnadshantering.

Krav: Resten av den här fliken förutsätter att läsaren har slutfört installationen av Azure Cost Management i samband med genomförandet av guiden för Azure-beredskap. Mer information om hur du konfigurerar Azure Cost Management finns den här [artikeln i guiden för Azure-beredskap](../../ready/azure-readiness-guide/manage-costs.md). När data har fyllts följer du nästa steg för att uppskatta månadskostnaden baserat på de data som samlas in.

Följande steg läser in kostnadsanalysdata för Azure Cost Management för dina prenumerationer:

1. Navigera till bladet **Cost Management + Fakturering** i portalen. Om du inte ser Cost Management + Fakturering i den vänstra rutan klickar du på **Alla tjänster**. I tjänstmenyfönstret under **Övervakning och hantering** väljer du **Cost Management + Fakturering**.
1. På bladet Cost Management + Fakturering väljer du **Cost Management** i det vänstra navigeringsfönstret för det öppna bladet och börja analysera och optimera molnkostnaderna.
1. På bladet Cost Management väljer du **Kostnadsanalys**.
    1. Använd reglaget **Omfång** för att växla till ett annat omfång i kostnadsanalysen.

Med den här analysen kan du granska totala kostnader, budget (om tillgängligt) och ackumulerade kostnader. Varje beräkning kan visas per tjänst, per resurs och över tid. Framför allt kan kostnader analyserar per tagg. Korrekt namngivning och taggning av tillgångar (infrastruktur, appar och data) är en förutsättning för goda styrnings- och kostnadshanteringsprocesser. Lämpliga taggar ger bättre hantering av kostnader och tydlig insyn om effekten av prestanda- och kostnadsoptimering.

## <a name="additional-resources"></a>Ytterligare resurser

- En mer omfattande plan om kostnadshantering över ett större antal tillgångar (infrastruktur, appar och data) finns i [styrningsmodellen i Ramverk för molnimplementering](../../govern/guides/index.md). I synnerhet riktlinjerna för [Cost Management-disciplin](../../govern/cost-management/index.md) och [stegvisa förbättringar av Cost Management i handboken för stora företag](../../govern/guides/complex/cost-management-improvement.md).
- Mer information om Azure Advisor finns i [Sänk tjänstekostnaderna med Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations).
- Mer information om Azure Cost Management finns i [Förstå och arbeta med omfattningar](https://docs.microsoft.com/azure/cost-management/understand-work-scopes) och [Utforska och analysera kostnader med kostnadsanalys](https://docs.microsoft.com/azure/cost-management/quick-acm-cost-analysis).

# <a name="tips-and-tricks-to-optimize-coststabtipstricks"></a>[Tips och knep för att optimera kostnader](#tab/TipsTricks)

Utöver de verktyg som beskrivs i den här artikeln finns det några tips och knep som kan hjälpa dig att snabbt minska de övergripande molnkostnaderna. Här följer några tips på hög nivå som du bör känna till:

## <a name="avoid-unnecessary-spending"></a>Undvik onödiga utgifter

De flesta tillgångar (infrastruktur, appar och data) i ett befintligt kan migreras till molnet i teorin. Det innebär dock inte att de borde göra det. Under utvärderingen av varje arbetsbelastning bör du bekräfta att arbetsbelastningen ska migreras. Artikeln i Ramverk för molnimplementering om [stegvis rationalisering](../../digital-estate/rationalize.md) kan hjälpa dig att avgöra vilka tillgångar som ska migreras.

## <a name="reduce-waste"></a>Undvik slöseri

När du har distribuerat din infrastruktur i Azure är det viktigt att se till att den används. Det enklaste sättet att börja spara omedelbart är att granska resurserna och ta bort alla som inte används.

## <a name="reduce-overprovisioning"></a>Minska överetablering

Även de bästa uppskattningarna riskerar att ha överetablerade och underutnyttjade tillgångar (infrastruktur, appar och data). Granska dessa tillgångar med verktygen i de föregående två flikarna för att identifiera sätt att minska storleken på tillgångarna så att de bättre motsvarar prestandakraven och därmed minska kostnaderna.

## <a name="take-advantage-of-available-discounts"></a>Dra nytta av tillgängliga rabatter

Prata med din Microsoft-kontorepresentant för att förstå hur du kan dra nytta aktuella rabatter. Här följer några exempel på rabatter som ofta används för att minska kostnaderna.

## <a name="azure-reservations"></a>Azure-reservationer

Med [Azure-reservationer](https://docs.microsoft.com/azure/billing/billing-save-compute-costs-reservations) kan du förskottsbetala för ett till tre års virtuella datorer eller SQL-databasprocessorkapacitet. Förskottsbetalning gör att du kan få rabatt på de resurser du använder. Med Azure-reservationer kan du minska dina kostnader för virtuella datorer eller SQL-databasprocessorer avsevärt med upp till 72 procent jämfört med löpande kostnader med antingen ett eller tre års förskottsbetalning. Reservation ger en rabatt och påverkar inte de virtuella datorerna eller SQL-databasernas körningsstatus.

## <a name="use-azure-hybrid-benefit"></a>Använd Azure Hybrid Benefit

Om du redan har Windows Server- eller SQL Serverlicenser i dina lokala distributioner kan du använda programmet [Azure Hybrid Benefit](https://azure.microsoft.com/pricing/hybrid-benefit) för att spara i Azure. Med den Windows Server-förmånen täcker vi kostnaden för operativsystemet (på upp till två virtuella datorer). Du betalar bara för basberäkningskostnaderna. Du kan använda befintliga SQL Server licenser för att spara upp till 55 procent på vCore-baserade SQL Database-alternativ. Alternativen omfattar SQL Server för virtuella Azure-datorer och SQL Server Integration Services.

## <a name="low-priority-vms-with-batch"></a>Lågprioriterade virtuella datorer med Batch

För bakgrundsprocesser med låg prioritet erbjuder Batch ett sätt att hantera de virtuella datorerna för bakgrundstjänsterna och sänka kostnaderna. Det är dock viktigt att förstå inverkan på prestandan för [Batch för virtuella datorer med låg prioritet](https://docs.microsoft.com/azure/batch/batch-low-pri-vms) innan du väljer det rabatterade alternativet.

## <a name="additional-resources"></a>Ytterligare resurser

En mer omfattande plan om kostnadshantering över ett större antal tillgångar (infrastruktur, appar och data) finns i [styrningsmodellen i Ramverk för molnimplementering](../../govern/guides/index.md). I synnerhet riktlinjerna för [Cost Management-disciplin](../../govern/cost-management/index.md) och [stegvisa förbättringar av Cost Management i handboken för styrning av stora företag](../../govern/guides/complex/cost-management-improvement.md).
