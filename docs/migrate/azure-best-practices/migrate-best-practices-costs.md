---
title: Kostnads-och storleks arbets belastningar som migrerats till Azure
description: Använd ramverket för moln införande för Azure för att lära dig metod tips för kostnads-och storleks arbets belastningar som migrerats till Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 89ac6886756c304d8acae5a4180a9715d336a92e
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79311922"
---
# <a name="best-practices-for-costing-and-sizing-workloads-migrated-to-azure"></a>Metodtips för kostnad och storleksändring av arbetsbelastningar som migreras till Azure

När du planerar och utformar en migrering ger ett fokus på kostnader den bästa Azure-migreringen på lång sikt. Under ett migreringsprojekt är det viktigt att alla team (såsom ekonomi, ledning och utveckling) förstår kostnaderna.

- Inför migreringen är det viktigt att uppskatta kostnaderna för migreringen med en baslinje för budgetmål per månad, kvartal och år.
- Efter migreringen bör du optimera kostnaderna, kontinuerligt övervaka arbetsbelastningarna och planera för framtida användningsmönster. Migrerade resurser kan starta som en typ av arbetsbelastning, men därefter ändras till en annan typ beroende på användning, kostnad och ändrade affärsförutsättningar.

Den här artikeln beskriver metodtips för kostnads- och storleksuppskattning före och efter migreringen.

> [!IMPORTANT]
> Metodtipsen och åsikter i den här artikeln baseras på de plattformar och tjänster som är tillgängliga för Azure vid tidpunkten på den skrevs. Funktioner förändras ständigt. Vissa rekommendationer kan kanske inte tillämpas på din distribution så välj vad som passar dig bäst.

## <a name="before-migration"></a>Före migreringen

Innan du flyttar dina arbetsbelastningar till molnet ska du beräkna månadskostnaden för att köra dem i Azure. Proaktiv hantering av molnkostnaderna hjälper dig att följa din budget för driftskostnader. Om budgeten är begränsad bör du ta hänsyn till detta innan du migrerar. Överväg att konvertera arbetsbelastningar till Azures lösningar utan server för att minska kostnaderna i förekommande fall.

Metodtipsen i det här avsnittet hjälper dig att uppskatta kostnader, utföra storleksändringar för virtuella datorer och lagringsenheter, använda Azure Hybrid Benefit, använda reserverade virtuella datorer och beräkna molnutgifter för olika prenumerationer.

## <a name="best-practice-estimate-monthly-workload-costs"></a>Bästa praxis: varje månad beräkna kostnaderna för arbetsbelastning

Det finns flera verktyg som du kan använda för att beräkna din månadsfaktura för migrerade arbetsbelastningar.

- **Pris kalkylator för Azure:** Du väljer de produkter som du vill beräkna, till exempel virtuella datorer och lagrings enheter. Mata in kostnaderna i priskalkylatorn för att skapa en uppskattning.

 ![pris Kalkylatorn för Azure](./media/migrate-best-practices-costs/pricing.png) *pris Kalkylatorn för Azure*

- **Azure Migrate:** För att beräkna kostnaderna måste du granska och ta hänsyn till alla resurser som krävs för att köra dina arbets belastningar i Azure. För att hämta dessa data skapar du en förteckning över dina tillgångar, inklusive servrar, virtuella datorer, databaser och lagringsutrymmen. Du kan använda Azure Migrate för att samla in den här informationen.

- Azure Migrate identifierar och utvärderar din lokala miljö och inventerar den.
- Azure Migrate kan kartlägga och visa beroenden mellan virtuella datorer så att du får en fullständig översikt.
- En Azure Migrate-utvärdering innehåller uppskattade kostnader.
  - Beräkningskostnader: använder Virtuella Azure-datorstorlek som rekommenderas när du skapar en utvärdering, Azure Migrate använder Billing-API för att beräkna uppskattade månatliga kostnader för virtuell dator. Uppskattningen tar hänsyn till operativsystem, programvaruförsäkring, reserverade instanser, drifttid för virtuella datorer samt plats- och valutainställningar. Den sammanställer kostnaden för alla virtuella datorer i utvärderingen och beräknar en total månatlig kostnadsberäkning.
  - Kostnaden för lagring: Azure Migrate beräknar totala månatliga kostnader för lagring genom att sammanställa lagringskostnaderna för alla virtuella datorer i en utvärdering. Du kan beräkna den månatliga lagringskostnaden för en viss dator genom att lägga ihop månadskostnaden för alla diskar som är kopplade till den.

    ![AzureMigrate](./media/migrate-best-practices-costs/assess.png)
    *Azure Migrate-utvärdering*

**Läs mer:**

- [Använda](https://azure.microsoft.com/pricing/calculator) priskalkylatorn för Azure.
- [Hämta en översikt](https://docs.microsoft.com/azure/migrate/migrate-overview) över Azure Migrate.
- [Läs om](https://docs.microsoft.com/azure/migrate/concepts-assessment-calculation) Azure Migrate-utvärderingar.
- [Läs mer](https://docs.microsoft.com/azure/dms/dms-overview) om Azure Database Migration Service.

## <a name="best-practice-right-size-vms"></a>Bästa praxis: storleksanpassa virtuella datorer

Du kan välja olika alternativ när du distribuerar virtuella Azure-datorer för att stödja arbetsbelastningar. Varje typ av virtuell dator har specifika funktioner och olika kombinationer av processor, minne och diskar. De virtuella datorerna grupperas enligt nedan:

**Typ** | **Detaljer** | **Använd**
--- | --- | ---
**Generellt syfte** | Balanserat förhållande mellan processor och minne. | Bra för testning och utveckling, små till medelstora databaser och webbservrar med låg till medelhög trafik.
**Beräkningsoptimerad** | Högt förhållande mellan processor och minne. | Bra för webbservrar med medelhög trafik, nätverkstillämpningar, batchprocesser och programservrar.
**Minnesoptimerad** | Högt minne-till-CPU. | Bra för relationsdatabaser, mellanstora till stora cacheminnen och minnesinterna analyser.
**Lagringsoptimerad** | Högt diskgenomflöde och I/O. | Bra för stordata-, SQL- och NoSQL-databaser.
**GPU-optimerad** | Specialiserade virtuella datorer. En eller flera GPU:er. | Tung grafik- och videoredigering.
**Höga prestanda** | Den snabbaste och mest kraftfulla processorn. Virtuella datorer med valfritt nätverksgränssnitt för stora dataflöden (RDMA) | Kritiska appar som kräver hög prestanda.

- Det är viktigt att förstå prisskillnaderna mellan de olika virtuella datorerna och deras långsiktiga effekt på budgeten.
- Varje typ innehåller flera virtuella datorserier.
- När du väljer en virtuell dator i en serie kan du dessutom bara skala upp och ned den virtuella datorn inom ramen för den serien. Till exempel kan en DSv2\_2 skala upp till DSv2\_4, men den kan inte ändras till en annan serie, till exempel Fsv2\_2.

**Läs mer:**

- [Lär dig](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) mer om typer av och storlekar på virtuella datorer och se samband mellan storlekar och typer.
- [Planera](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs) storlek på virtuell dator.
- [Läs](https://docs.microsoft.com/azure/migrate/contoso-migration-assessment) det här exemplet på en utvärdering för det påhittade företaget Contoso.

## <a name="best-practice-select-the-right-storage"></a>Bästa praxis: Välj rätt lagring

Det kan vara kostsamt och tidskrävande att justera och underhålla lokalt lagringsutrymme (SAN eller NAS) och nätverken som de ligger på. Fildata migreras vanligtvis till molnet för att förenkla driften och hanteringen. Microsoft erbjuder flera alternativ för att flytta data till Azure och du måste fatta beslut om dessa alternativ. Om du väljer rätt lagringstyp för data kan din organisation spara tusentals kronor varje månad. Några saker att tänka på:

- Data som inte används mycket och som inte är affärs kritiska behöver inte placeras på den dyraste lagringen.
- Å andra sidan bör verksamhetskritiska data förvaras på högre nivå.
- När du planerar migreringen bör du inventera dina data och organisera dem efter prioritet så att de kan placeras på den lämpligaste lagringen. Överväg både budget och kostnader, samt prestanda. Kostnaden bör inte nödvändigtvis vara den huvudsakliga beslutsfaktorn. Om du väljer det billigaste alternativet kan du exponera arbetsbelastningen för prestanda- och tillgänglighetsrisker.

### <a name="storage-data-types"></a>Typer av lagringsdata

Azure erbjuder olika typer av lagringsdata.

<!--markdownlint-disable MD033 -->

**Datatyp** | **Detaljer** | **Användning**
--- | --- |  ---
**Blobbar** | Optimerade för att lagra stora mängder ostrukturerade objektdata, exempelvis text eller binära data<br/><br/> | Få åtkomst till data var du än är över HTTP/HTTPS. | Används för streaming och scenarier där åtkomst sker från oväntade platser. Till exempel, för att tillhandahålla bilder och dokument direkt i en webbläsare, streama video och ljud samt lagra data för säkerhetskopiering och haveriberedskap.
**Filer** | Hanterade filresurser som nås via SMB 3.0 | Används när du migrerar lokala filresurser och för flera sätt att få åtkomst/ansluta till fildata.
**Diskar** | Baserat på sidblobbar.<br/><br/> Disktyp (hastighet): Standard (Hårddisk eller SSD)- eller Premium (SSD).<br/><br/>Diskhantering: ohanterade (du hantera Diskinställningar och lagring) eller hanterad (du väljer typ av disk och Azure hanterar disken åt dig). | Använd Premium-diskar för virtuella datorer. Använd hanterade diskar för enkel hantering och skalning.
**Köer** | Lagra och hämta stora mängder meddelanden som nås via autentiserade anrop (HTTP eller HTTPS) | Anslut programkomponenter med asynkron meddelandekö.
**Tabeller** | Lagra tabeller. | Nu del av tabell-API:et för Azure Cosmos DB.

<!--markdownlint-enable MD033 -->

### <a name="access-tiers"></a>Åtkomstnivåer

Azure-lagring har olika alternativ för åtkomst till blockblobbdata. Genom att välja rätt åtkomstnivå lagrar du blockblobbdata på det mest kostnadseffektiva sättet som finns.

<!--markdownlint-disable MD033 -->

**Typ** | **Detaljer** | **Användning**
--- | --- | ---
**Frekvent** | Högre lagringskostnad än lågfrekvent. Lägre åtkomstavgifter än lågfrekvent.<br/><br/>Detta är standardnivån. | Används för aktiva data som används ofta.
**Lågfrekvent** | Lägre lagringskostnad än frekvent. Högre åtkomstavgifter än frekvent.<br/><br/> Lagring i minst 30 dagar. | Kortsiktig lagring, data är tillgängliga men används sällan.
**Arkiv** | Används för enskilda blockblobbar.<br/><br/> Det mest kostnadseffektiva alternativet för lagring. Dataåtkomst är dyrare än frekvent och lågfrekvent. | Används för data som kan tolerera flera timmars fördröjning vid hämtning och som finns kvar på arkivnivån i minst 180 dagar.

<!--markdownlint-enable MD033 -->

### <a name="storage-account-types"></a>Lagringskontotyper

Azure erbjuder olika typer av lagringskonton och prestandanivåer.

<!--markdownlint-disable MD033 -->

**Kontotyp** | **Detaljer** | **Användning**
--- | --- | ---
**Generell användning v2 Standard** | Stöder blobbar (block, sida, tillägg), filer, diskar, köer och tabeller.<br/><br/> Har stöd för åtkomstnivåerna frekvent, lågfrekvent och arkiv. ZRS stöds. | Används för de flesta scenarier och de flesta typer av data. Standardlagringskonton kan antingen baseras på HDD eller SDD.
**General användning v2 Premium** | Stöder blobblagringsdata (sidblobbar). Har stöd för åtkomstnivåerna frekvent, lågfrekvent och arkiv. ZRS stöds.<br/><br/> Lagrad på SSD. | Microsoft rekommenderar att du använder detta för alla virtuella datorer.
**Generell användning v1** | Åtkomstnivåer stöds inte. Stöder inte ZRS | Används om du har appar som behöver en klassisk Azure-distributionsmodell.
**Blob** | Specialiserat lagringskonto för lagring av ostrukturerade objekt. Tillhandahåller blockblobbar och tilläggsblobbar (ej lagringstjänster för fil, kö, tabell eller disk). Ger samma hållbarhet, tillgänglighet, skalbarhet och prestanda som Generell användning v2. | du kan inte lagra sidblobbar på dessa konton och därför kan du inte lagra VHD-filer. Du kan ange att åtkomstnivån ska vara frekvent eller lågfrekvent.

<!--markdownlint-enable MD033 -->

### <a name="storage-redundancy-options"></a>Alternativ för lagringsredundans

Lagringskonton kan använda olika typer av redundans för återhämtning och hög tillgänglighet.

**Typ** | **Detaljer** | **Användning**
--- | --- | ---
**Lokalt redundant lagring (LRS)** | Skyddar mot ett lokalt avbrott genom att replikera inom en enskild lagringsenhet till en separat feldomän och uppdateringsdomän. Behåller flera kopior av dina data i samma datacenter. Ger en beständighet på minst 99,999999999 % (9 decimaler) för objekt under ett år. | Överväg om din app lagrar data som enkelt kan rekonstrueras.
**Zonredundant lagring (ZRS)** | Skyddar mot datacenteravbrott genom att replikera över tre lagringskluster i samma region. Varje lagringskluster är fysiskt åtskilt och förvaras i en egen tillgänglighetszon. Ger en beständighet på minst 99,9999999999 % (10 decimaler) för objekt under ett år genom att flera kopior av data förvaras i flera datacenter eller flera regioner. | Fundera på om du behöver konsekvens, hållbarhet och hög tillgänglighet. Den skyddar kanske inte mot en regional katastrof där flera zoner påverkas permanent.
**Geografiskt redundant lagring (GRS)** | Skyddar mot avbrott i en hel region genom att replikera data till en sekundär region som ligger hundratals kilometer från den primära. Ger en beständighet på minst 99,99999999999999 % (14 decimaler) för objekt under ett år. | En replik kanske inte är tillgänglig om inte Microsoft initierar sekundär redundans. In redundans uppstår är läs- och skrivåtkomst tillgängligt.
**Läsåtkomst till geografiskt redundant lagring (RA-GRS)** | Liknar GRS. Ger en beständighet på minst 99,99999999999999 % (14 decimaler) för objekt under ett år | Tillhandahåller och 99,99 % lästillgänglighet genom att tillåta läsåtkomst från den andra regionen som används för GRS.

**Läs mer:**

- [Se](https://azure.microsoft.com/pricing/details/storage) prissättning för Azure Storage.
- [Lär dig](https://docs.microsoft.com/azure/storage/common/storage-import-export-service) mer om Azure-import/-export för migrering av stora mängder data till Azure-blobbar och -filer.
- [Jämför](https://docs.microsoft.com/azure/storage/common/storage-decide-blobs-files-disks?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) blobbar, filer och datatyper för disklagring.
- [Läs mer](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers) om åtkomstnivåer.
- [Se](https://docs.microsoft.com/azure/storage/common/storage-account-overview?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) olika typer av lagringskonton.
- Lär dig mer om [lagringsredundans](https://docs.microsoft.com/azure/storage/common/storage-redundancy), [LRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), [ZRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-zrs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), [GRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) och [GRS med läsåtkomst](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#read-access-to-data-in-the-secondary-region).
- [Läs mer](https://docs.microsoft.com/azure/storage/files/storage-files-introduction) om Azure Files.

## <a name="best-practice-take-advantage-of-azure-hybrid-benefits"></a>Bästa praxis: dra nytta av Azure Hybrid-förmåner

Tack vare åratals programvaruinvesteringar i system som Windows Server och SQL Server har Microsoft en unik möjlighet att ge kunderna mervärde i molnet med avsevärda rabatter som andra molnleverantörer ofta inte kan slå.

En integrerad lokal/Azure-baserad produktportfölj från Microsoft ger konkurrens- och kostnadsfördelar. Om du för närvarande har ett operativsystem eller annan programvarulicens genom Software Assurance (SA) kan du ta med dig dessa licenser till molnet genom Azure Hybrid Benefit.

**Läs mer:**

- [Ta en titt på](https://azure.microsoft.com/pricing/hybrid-benefit) kalkylatorn för besparingar med Azure Hybrid Benefit.
- [Läs mer om](https://azure.microsoft.com/pricing/hybrid-benefit) Azure Hybrid Benefit för Windows Server.
- Se [Prisvägledning för virtuella SQL Server Azure-datorer](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance).

## <a name="best-practice-use-reserved-vm-instances"></a>Bästa praxis: använda reserverade VM-instanser

Molnplattformar är vanligtvis konfigurerade för löpande betalning. Modellen har vissa brister eftersom du inte nödvändigtvis vet hur dynamiska dina arbetsbelastningar kommer att vara. När du anger tydliga avsikter för en arbetsbelastning bidrar du till infrastrukturplaneringen.

Med reserverade instanser för virtuell dator med Azure kan du förskottsbetala för instansen i ett eller tre år.

- Förskottsbetalning ger rabatt på de resurser du använder.
- Du kan avsevärt minska kostnaden för virtuella datorer, SQL Database Compute, Azure Cosmos DB eller andra resurskostnader med upp till 72 % jämfört med löpande betalning.
- Reservation ger en rabatt och påverkar inte resursernas körningsstatus.
- Du kan avbryta reserverade instanser.

![Reserverade instanser](./media/migrate-best-practices-costs/reserve.png)
*Reserverade virtuella Azure-datorer*

**Läs mer:**

- [Läs mer om](https://docs.microsoft.com/azure/billing/billing-save-compute-costs-reservations) Azure-reservationer.
- [Läs](https://azure.microsoft.com/pricing/reserved-vm-instances/#faq) vanliga frågor och svar om reserverade Azure-instanser.
- [Hämta prisvägledning](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) för virtuella SQL Server Azure-datorer.

## <a name="best-practice-aggregate-cloud-spend-across-subscriptions"></a>Bästa praxis: sammanställd molnutgift mellan prenumerationer

Det är oundvikligt att du kommer att ha fler än en Azure-prenumeration. Du kan till exempel behöva ytterligare en prenumeration för att skapa en gräns mellan utveckling och produktion, eller du kanske har en plattform där varje kund måste ha en separat prenumeration. Att kunna samla in datarapporter över alla prenumerationer på en enda plattform är en värdefull funktion.

Du kan göra detta med Azure Cost Management-API:er. Därefter, när du har sammanställt data i en enda källa, till exempel Azure SQL, kan du använda verktyg som Power BI för att tolka dina data. Du kan skapa sammanställda prenumerationsrapporter och detaljerade rapporter. För användare som behöver proaktiva insikter om kostnads hantering kan du till exempel skapa särskilda vyer av kostnader baserat på avdelning, resurs grupp osv. Du behöver inte ge dem fullständig åtkomst till Azures fakturerings data.

**Läs mer:**

- [Få en översikt](https://docs.microsoft.com/azure/billing/billing-consumption-api-overview) över Azure Consumption-API:et.
- [Lär dig](https://docs.microsoft.com/power-bi/desktop-connect-azure-consumption-insights) mer om att ansluta till Azure Consumption Insights i Power BI Desktop.
- [Lär dig](https://docs.microsoft.com/azure/billing/billing-manage-access) hantera åtkomst till faktureringsinformation för Azure med rollbaserad åtkomstkontroll (RBAC).

## <a name="after-migration"></a>Efter migrering

Efter en lyckad migrering av dina arbetsbelastningar och några veckor efter insamlingen av förbrukningsdata kommer du att ha en tydlig uppfattning om dina resurskostnader.

- När du analyserar data kan du börja skapa en budgetbaslinje för resursgrupper och resurser i Azure.
- När du sedan vet var din molnbudget används kan du analysera hur kostnaderna kan minskas ytterligare.

Metodtipsen i detta avsnitt är bland annat att använda Azure Cost Management för budgetering och analys, övervaka resurser och införa budgetar för varje resursgrupp och optimera övervakning, lagring och virtuella datorer.

## <a name="best-practice-use-azure-cost-management"></a>Bästa praxis: Använd Azure kostnadshantering

Microsoft tillhandahåller Azure Cost Management så att du kan hålla koll på dina utgifter:

- Hjälper dig att övervaka och kontrollera utgifter för Azure och optimera användningen av dina resurser.
- Granskar hela prenumerationen och alla dess resurser och tar fram rekommendationer.
- Innehåller ett fullständigt API för att integrera externa verktyg och redovisningssystem.
- Spårar resursanvändningen och hanterar molnkostnader i en enda enhetlig vy.
- Ger omfattande driftsrelaterade och ekonomiska insikter som hjälper dig att fatta välgrundade beslut.

I Cost Management kan du:

- **Skapa en budget:** Skapa en budget för ekonomiskt ansvar.
  - Du kan ta hänsyn till de tjänster som du förbrukar eller prenumererar på under en viss period (varje månad, varje kvartal, varje år) och en omfattning (prenumerationer/resursgrupper). Du kan till exempel skapa en prenumerationsbudget för Azure per månad, kvartal eller år.
    - När du har skapat en budget visas den i kostnadsanalysen. Att se sin budget i förhållande till aktuella utgifter är ett av de första stegen för att analysera kostnader och utgifter.
  - E-postmeddelanden kan skickas när en budgettröskel överskrids.
  - Du kan exportera kostnadshanteringsdata till Azure-lagring, där de kan analyseras.

    ![Cost Management-budget](./media/migrate-best-practices-costs/budget.png)
    *Azure Cost Management-budget*

- **Gör en kostnads analys:** Få en kostnads analys för att utforska och analysera dina organisations kostnader för att hjälpa dig att förstå hur kostnader periodiseras och identifiera utgifts trender.
  - Kostnadsanalys är tillgängligt för EA-användare.
  - Du kan visa kostnadsanalysdata för olika omfång, inklusive per avdelning, konto, prenumeration eller resursgrupp.
  - Du kan få en kostnadsanalys som visar den totala kostnaden för den aktuella månaden och de ackumulerade dagliga kostnaderna.

    ![Cost Management-analys](./media/migrate-best-practices-costs/analysis.png)
    *Azure Cost Management-analys*
- **Få rekommendationer:** Få rekommendationer om Advisor som visar hur du kan optimera och förbättra effektiviteten.

**Läs mer:**

- [Hämta en översikt](https://docs.microsoft.com/azure/cost-management/overview) över Azure Cost Management.
- [Lär dig att](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices) optimera din molninvestering med Azure Cost Management.
- [Lär dig att](https://docs.microsoft.com/azure/cost-management/use-reports) använda Azure Cost Management-rapporter.
- [Hämta en](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/billing/TOC.json) självstudiekurs om att optimera kostnader med hjälp av rekommendationer.
- [Granska](https://docs.microsoft.com/rest/api/consumption/budgets) Azure Consumption-API:et.

## <a name="best-practice-monitor-resource-utilization"></a>Bästa praxis: övervaka resursutnyttjandet

I Azure betalar du för det du använder när resurser förbrukas och endast då. Debitering för virtuella datorer sker när en virtuell dator tilldelas och du debiteras inte efter att den virtuella datorn har frigjorts. Med detta i åtanke bör du övervaka vilka virtuella datorer som används och kontrollera storleken på dina virtuella datorer.

- Utvärdera regelbundet arbetsbelastningarna för dina virtuella datorer för att fastställa baslinjer.
- Om din arbetsbelastning används kraftigt från måndag till fredag från 08.00 till 18.00 men knappast utanför denna tid kan du nedgradera dina virtuella datorer för den mindre aktiva tiden. Det kan innebära att du ändrar storlek på de virtuella datorerna eller använder skaluppsättningar för de virtuella datorerna för att ändra deras skala uppåt eller nedåt automatiskt.
- Vissa företag sätter de virtuella datorerna i ”viloläge” genom att placera dem i en kalender som anger när de ska vara tillgängliga och när de inte behövs.
- Förutom att övervaka dina virtuella datorer för du övervaka andra nätverksresurser, till exempel ExpressRoute och virtuella nätverksgatewayer så att de inte används för mycket eller för lite.
- Du kan övervaka användningen av virtuella datorer med hjälp av Microsoft-verktyg som Azure Cost Management, Azure Monitor och Azure Advisor. Verktyg från tredje part är också tillgängliga.

**Läs mer:**

- Få en översikt över [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) och [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview).
- [Få](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations) kostnadsrekommendationer från Advisor.
- [Lär dig [optimera kostnader baserat på rekommendationer](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/billing/TOC.json) och [undvika oväntade avgifter](https://docs.microsoft.com/azure/billing/billing-getting-started).
- Lär dig mer om [Azure Resource Optimization (ARO) Toolkit](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practice-implement-resource-group-budgets"></a>Bästa praxis: Implementera resource group budgetar

Resursgrupper används ofta för att representera kostnadsgränser. Tillsammans med det här användningsmönstret fortsätter Azure-teamet att utveckla nya och förbättrade sätt att spåra och analysera resursutgifter på olika nivåer, inklusive möjligheten att skapa budgetar för resursgrupper och resurser.

- En resursgruppsbudget hjälper dig att följa kostnader som är kopplade till en resursgrupp.
- Du kan utlösa aviseringar och köra många olika spelböcker när budgetgränsen uppnås eller överskrids.

**Läs mer:**

- [Läs mer om att ](https://docs.microsoft.com/azure/billing/billing-cost-management-budget-scenario)hantera kostnader med Azure Budgets.
- [Följ en självstudie](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/billing/TOC.json) för att skapa och hantera en budget med Azure.

## <a name="best-practice-optimize-azure-monitor-retention"></a>Bästa praxis: Optimera Azure Monitor kvarhållning

När du flyttar resurser till Azure och aktiverar diagnostisk loggning för dem skapar du stora mängder loggdata. Vanligt vis skickas dessa loggdata till ett lagringskonto som är mappat till en Log Analytics-arbetsyta.

- Ju längre dessa loggdata kvarhålls desto mer data har du.
- Loggdata kan se ut på många sätt och vissa resurser kommer att skapa mer loggdata än andra.
- På grund av regler och efterlevnad är det troligt att du måste kvarhålla loggdata för vissa resurser längre än för andra.
- Du måste noggrant avväga optimeringen av dina logglagringskostnader och kvarhållandet av de loggdata du behöver.
- Vi rekommenderar att du utvärderar och ställer in loggningen direkt när du har slutfört migreringen så att du inte debiteras för att kvarhålla loggar utan anledning.

**Läs mer:**

- [Lär dig](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-usage-and-estimated-costs) mer om användningsövervakning och beräknade kostnader.

## <a name="best-practice-optimize-storage"></a>Bästa praxis: Optimera lagring

Om du har följt metodtipsen för att välja lagring före migreringen kan du förmodligen dra nytta av några fördelar. Men det finns förmodligen fler lagringskostnader som du fortfarande kan optimera. Med tiden kan blobbar och filer bli inaktuella. Dessa data kanske inte längre används men du kanske måste kvarhålla dem av juridiska skäl under en längre tid. Därför kanske du inte behöver lagra dem på den högpresterande lagring som du använde för den ursprungliga migreringen.

Att identifiera och flytta inaktuella data till billigare lagringsområden kan ha stor inverkan på din månatliga lagringsbudget. Azure erbjuder många olika sätt att identifiera och lagra inaktuella data.

- Dra nytta av åtkomstnivåer för Generell användning v2-lagring och flytta mindre viktiga data från nivån frekvent till lågfrekvent och arkiv.
- Använd StorSimple för att flytta inaktuella data baserat på anpassade principer.

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers) om åtkomstnivåer.
- [Få en översikt](https://docs.microsoft.com/azure/azure-monitor/overview) över StorSimple och [StorSimple-prissättning](https://azure.microsoft.com/pricing/details/storsimple).

## <a name="best-practice-automate-vm-optimization"></a>Bästa praxis: automatisera VM optimering

Det ultimata målet med att köra en virtuell dator i molnet är att maximera CPU, minne och använt diskutrymme. Om du identifierar virtuella datorer som inte är optimerade eller har frekventa perioder när de virtuella datorerna inte används är det klokt att antingen stänga ned dem eller skala ned dem med hjälp av skaluppsättningar för virtuella datorer.

Du kan optimera en virtuell dator med Azure Automation, skaluppsättningar för virtuella datorer, automatisk avstängning och skript eller lösningar från tredje part.

**Läs mer:**

- [Lär dig hur](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-vertical-scale-reprovision) du använder vertikal automatisk skalning.
- [Schemalägg](https://azure.microsoft.com/updates/azure-devtest-labs-schedule-vm-auto-start) en autostart för en virtuell dator.
- [Lär dig ](https://docs.microsoft.com/azure/automation/automation-solution-vm-management) starta eller stoppa virtuella datorer när de inte används i Azure Automation.
- [Hämta mer information] om [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) och [verktyget](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit)Azure Resource Optimization (ARO).

## <a name="best-practices-use-logic-apps-and-runbooks-with-budgets-api"></a>Bästa praxis: Använd Logic Apps och runbooks med budgetar API

Azure tillhandahåller ett REST API som har åtkomst till din kundfaktureringsinformation.

- Du kan använda budget-API:et för att integrera externa system och arbetsflöden som utlöses av mått som du skapar från API-data.
- Du kan hämta användnings- och resursdata till ditt dataanalysverktyg.
- Azures API:er för resursanvändning och RateCard kan hjälpa dig att korrekt förutse och hantera dina kostnader.
- API:erna implementeras som en resursprovider och ingår i de API:er som exponeras av Azure Resource Manager.
- Budget-API:et kan integreras med Azure Logic Apps och Runbooks.

**Läs mer:**

- [Läs mer](https://docs.microsoft.com/rest/api/consumption/budgets) om Budget-API:et.
- [Få insikter](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) om Azure-användning med fakturerings-API:et.

## <a name="best-practice-implement-serverless-technologies"></a>Bästa praxis: Implementera serverfria tekniken

Arbetsbelastningar på virtuella datorer migreras ofta i befintligt skick för att undvika driftstopp. Virtuella datorer kan ofta vara värdar för aktiviteter som är tillfälliga, tar kort tid att köra eller körs under många timmar. Virtuella datorer som kör schemalagda uppgifter, såsom schemaläggaren i Windows eller PowerShell-skript är exempel på detta. När de här uppgifterna inte körs debiteras du ändå för den virtuella datorn och disklagring.

Efter migreringen kan du efter en grundlig granskning av de här typerna av aktiviteter överväga att migrera dem till serverlös teknik, till exempel Azure Functions eller Azure Batch-jobb. Med den här lösningen behöver du inte längre hantera och underhålla de virtuella datorerna, vilket sparar ytterligare pengar.

**Läs mer:**

- Läs mer om [Azure Functions](https://azure.microsoft.com/services/functions).
- Läs om [Azure Batch](https://azure.microsoft.com/services/batch).

## <a name="next-steps"></a>Nästa steg

Läs andra metodtips:

- [Metodtips](./migrate-best-practices-security-management.md) för säkerhet och hantering efter migrering.
- [Metodtips](./migrate-best-practices-networking.md) för nätverk efter migrering.
