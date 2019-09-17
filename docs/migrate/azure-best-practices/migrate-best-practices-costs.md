---
title: Metodtips för tar och storlek arbetsbelastningar migreras till Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Hämta metodtips för kostnad och storleksändring av arbetsbelastningar som migreras till Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b358c4d07e4adb30c0420c9d1b3bc85c25e9ce95
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024944"
---
# <a name="best-practices-for-costing-and-sizing-workloads-migrated-to-azure"></a>Metodtips för tar och storlek arbetsbelastningar migreras till Azure

När du planerar och utformar en migrering ger ett fokus på kostnader den bästa Azure-migreringen på lång sikt. Under ett migreringsprojekt är det viktigt att alla team (såsom ekonomi, ledning och utveckling) förstår kostnaderna.

- Inför migreringen är det viktigt att uppskatta kostnaderna för migreringen med en baslinje för budgetmål per månad, kvartal och år.
- Efter migreringen bör du optimera kostnaderna, kontinuerligt övervaka arbetsbelastningar och planera för framtida användningsmönster. Migrerade resurser kan starta som en typ av arbetsbelastning, men därefter ändras till en annan typ beroende på användning, kostnad och ändrade affärsförutsättningar.

Den här artikeln beskriver Metodtips för kostnadshantering och ändra storlek på före och efter migreringen.

> [!IMPORTANT]
> Bästa praxis och yttranden som beskrivs i den här artikeln baseras på Azure-plattformen och bearbeta funktioner som är tillgängliga vid tidpunkten för skrivning. Funktioner och möjligheter ändras med tiden. Inte alla rekommendationer gäller för din distribution, så Välj vad som passar dig.

## <a name="before-migration"></a>Före migreringen

Innan du flyttar dina arbetsbelastningar till molnet ska du beräkna månadskostnaden för att köra dem i Azure. Proaktiv hantering av molnkostnaderna hjälper dig att följa din budget för driftskostnader. Om budgeten är begränsad bör du ta hänsyn till detta innan du migrerar. Överväg att konvertera arbetsbelastningar till Azures lösningar utan server för att minska kostnaderna i förekommande fall.

Metodtipsen i det här avsnittet hjälper dig att uppskatta kostnader, utföra storleksändringar för virtuella datorer och lagringsenheter, använda Azure Hybrid Benefit, använda reserverade virtuella datorer och beräkna molnutgifter för olika prenumerationer.

## <a name="best-practice-estimate-monthly-workload-costs"></a>Metodtips: Uppskatta månadskostnader arbetsbelastningar

Det finns flera verktyg som du kan använda för att beräkna din månadsfaktura för migrerade arbetsbelastningar.

- **Priskalkylator för Azure:** Du väljer de produkter som du vill beräkna, till exempel virtuella datorer och lagringsenheter. Mata in kostnaderna i priskalkylatorn för att skapa en uppskattning.

 ![Priskalkylator för Azure](./media/migrate-best-practices-costs/pricing.png) *Priskalkylator för Azure*

- **Azure Migrate:** För att beräkna kostnaderna måste du granska och ta hänsyn till alla resurser som krävs för att köra dina arbetsbelastningar i Azure. För att hämta dessa data skapar du en förteckning över dina tillgångar, inklusive servrar, virtuella datorer, databaser och lagringsutrymmen. Du kan använda Azure Migrate för att samla in den här informationen.

- Azure Migrate identifierar och utvärderar din lokala miljö för att visa en förteckning.
- Azure Migrate kan mappa och visa beroenden mellan virtuella datorer så att du har en bild.
- En Azure Migrate-utvärdering innehåller uppskattade kostnader.
  - Beräkna kostnader: Med hjälp av storleken på den virtuella Azure-datorn som rekommenderas när du skapar utvärderingen använder Azure Migrate fakturerings-API:et för att beräkna uppskattade månatliga kostnader för den virtuella datorn. Uppskattningen tar hänsyn till operativsystem, programvaruförsäkring, reserverade instanser, drifttid för virtuella datorer samt plats- och valutainställningar. Den sammanställer kostnaden för alla virtuella datorer i utvärderingen och beräknar en total månatlig kostnadsberäkning.
  - Lagringskostnad: Azure Migrate beräknar en total månatlig lagringskostnad genom att addera lagringskostnaderna för alla virtuella datorer i en utvärdering. Du kan beräkna den månatliga lagringskostnaden för en viss dator genom att lägga ihop månadskostnaden för alla diskar som är kopplade till den.

    ![AzureMigrate](./media/migrate-best-practices-costs/assess.png)
    *Azure Migrate-utvärdering*

**Läs mer:**

- [Använd](https://azure.microsoft.com/pricing/calculator) Azures priskalkylator.
- [Få en översikt](https://docs.microsoft.com/azure/migrate/migrate-overview) av Azure Migrate.
- [Läs om](https://docs.microsoft.com/azure/migrate/concepts-assessment-calculation) Azure Migrate-utvärderingar.
- [Läs mer](https://docs.microsoft.com/azure/dms/dms-overview) om Azure Database Migration Service.

## <a name="best-practice-right-size-vms"></a>Metodtips: Rätt storlek på virtuella datorer

Du kan välja olika alternativ när du distribuerar virtuella Azure-datorer för att stödja arbetsbelastningar. Varje typ av virtuell dator har specifika funktioner och olika kombinationer av processor, minne och diskar. De virtuella datorerna grupperas enligt nedan:

**Typ** | **Detaljer** | **Använd**
--- | --- | ---
**Generellt syfte** | Balanserat förhållande mellan processor och minne. | Bra för testning och utveckling, små till medelstora databaser och webbservrar med låg till medelhög trafik.
**Beräkningsoptimerad** | Högt förhållande mellan processor och minne. | Bra för webbservrar med medelhög trafik, nätverkstillämpningar, batchprocesser och programservrar.
**Minnesoptimerad** | Högt minne-till-CPU. | Bra för relationsdatabaser, mellanstora till stora cacheminnen och minnesinterna analyser.
**Lagringsoptimerad** | Högt diskgenomflöde och I/O. | Bra för stordata, SQL och NoSQL-databaser.
**GPU-optimerad** | Virtuella specialdatorer. En eller flera grafikprocessorer. | Tung grafik och videoredigering.
**Höga prestanda** | Snabbaste och mest kraftfulla CPU. Virtuella datorer med valfritt högt dataflöde nätverksgränssnitt (RDMA) | Kritiska appar med höga prestanda.

- Det är viktigt att förstå prisskillnaderna mellan de olika virtuella datorerna och deras långsiktiga effekt på budgeten.
- Varje typ innehåller flera virtuella datorserier.
- När du väljer en virtuell dator i en serie kan du dessutom bara skala upp och ned den virtuella datorn inom ramen för den serien. Till exempel en DSv2\_2 kan skala upp till DSv2\_4, men det kan inte ändras till en annan serie, till exempel Fsv2\_2.

**Lära sig mer:**

- [Läs mer](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) om VM-typer och storlek och kartan storlek till typer.
- [Planera](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs) storlek på virtuell dator.
- [Läs](https://docs.microsoft.com/azure/migrate/contoso-migration-assessment) det här exemplet på en utvärdering för det påhittade företaget Contoso.

## <a name="best-practice-select-the-right-storage"></a>Metodtips: Välj rätt lagring

Det kan vara kostsamt och tidskrävande att justera och underhålla lokalt lagringsutrymme (SAN eller NAS) och nätverken som de ligger på. Fildata (lagring) migreras ofta till molnet för att minska operativa och hanteringsproblem. Microsoft erbjuder flera alternativ för att flytta data till Azure och du behöver fatta beslut om dessa alternativ. Välja rätt lagringstyp för data kan spara din organisation flera tusen dollar varje månad. Några saker:

- Data som inte är används mycket, och inte sina verksamhetskritiska, behöver inte placeras på det dyraste lagringsutrymmet.
- Viktiga affärskritiska data måste däremot finnas på högre nivå lagringsalternativ.
- Under migrering, göra en förteckning över data och klassificera den efter prioritet, för att mappa den till den lämpligaste lagringen. Överväg att budget och kostnader samt prestanda. Kostnad bör inte nödvändigtvis vara den huvudsakliga beslutsfattande faktorn. Välja det billigaste alternativet kan exponera arbetsbelastningen att prestanda och tillgänglighet risker.

### <a name="storage-data-types"></a>Storage-datatyper

Azure tillhandahåller olika typer av lagringsdata.

<!--markdownlint-disable MD033 -->

**Datatyp** | **Detaljer** | **Användning**
--- | --- |  ---
**Blobbar** | Optimerad för att lagra stora mängder Ostrukturerade objekt, till exempel text eller binära data<br/><br/> | Åtkomst till data överallt via HTTP/HTTPS. | Använd för scenarier med strömmande och slumpmässig åtkomst. Till exempel för att tillhandahålla bilder och dokument direkt till en webbläsare, strömma video och ljud och lagra återställningsdata för säkerhetskopiering och haveriberedskap.
**Filer** | Hanterade filresurser som nås via SMB 3.0 | Använda när du migrerar lokala filresurser, och för att ge flera nätverksanslutningar till fildata.
**Diskar** | Baserat på sidblobbar.<br/><br/> Disktyp (hastighet): Standard (HDD eller SSD) eller Premium (SSD).<br/><br/>Diskhantering: Ohanterad (du hanterar diskinställningar och lagringsutrymme) eller hanterad (du väljer disktyp och Azure hanterar disken åt dig). | Använd Premium-diskar för virtuella datorer. Använda hanterade diskar för enkel hantering och skalning.
**köer** | Store och hämta stora mängder meddelanden som kan nås via autentiserade anrop (HTTP eller HTTPS) | Anslut appkomponenter med asynkrona meddelandeköer.
**Tabeller** | Store tabeller. | Nu en del av Azure Cosmos DB Table API.

<!--markdownlint-enable MD033 -->

### <a name="access-tiers"></a>Åtkomstnivåer

Azure storage tillhandahåller olika alternativ för åtkomst till block blob-data. Att välja rätt åtkomstnivå hjälper till att säkerställa att du lagrar block blob-data på det mest kostnadseffektiva sättet.

<!--markdownlint-disable MD033 -->

**Typ** | **Detaljer** | **Användning**
--- | --- | ---
**hot** | Högre lagringskostnad än lågfrekvent. Lägre åtkomstavgifter än lågfrekvent.<br/><br/>Det här är den standardlagringsnivån. | Används för data i aktiv användning som används ofta.
**Lågfrekvent** | Lägre lagringskostnad än hot (frekvent). Högre åtkomstavgifter än hot (frekvent).<br/><br/> Store för minst 30 dagar. | Store kortsiktig, data är tillgänglig men används sällan.
**Arkiv** | Används för enskilda blockblob-objekt.<br/><br/> Mest kostnadseffektiva alternativ för lagring. Åtkomst till data är dyrare än heta och kalla. | Används för data som kan tolerera server timmars svarstid för hämtning och förblir på nivån i minst 180 dagar.

<!--markdownlint-enable MD033 -->

### <a name="storage-account-types"></a>Storage-kontotyper

Azure tillhandahåller olika typer av lagringskonton och prestandanivåer.

<!--markdownlint-disable MD033 -->

**Kontotyp** | **Detaljer** | **Användning**
--- | --- | ---
**Generell användning v2 Standard** | Har stöd för blobar (blockera, sidan, Lägg till) filer, diskar, köer och tabeller.<br/><br/> Stöder åtkomstnivåerna varm, kall och Arkiv. ZRS stöds. | Används för de flesta scenarier och de flesta typer av data. Standardlagringskonton kan antingen baseras på HDD eller SDD.
**General användning v2 Premium** | Har stöd för Blob storage-data (sidblob). Stöder åtkomstnivåerna varm, kall och Arkiv. ZRS stöds.<br/><br/> Lagras på SSD. | Microsoft rekommenderar för alla virtuella datorer.
**Generell användning v1** | Åtkomst lagringsnivåer stöds inte. Stöder inte ZRS | Använd om apparna måste den klassiska distributionsmodellen.
**Blob** | Specialiserat lagringskonto för lagring av Ostrukturerade objekt. Tillhandahåller blockblobbar och tilläggsblobbar endast (ingen fil, kö, tabell eller Disk storage-tjänster). Innehåller samma tillförlitlighet, tillgänglighet, skalbarhet och prestanda som generell användning v2. | Du kan inte lagra sidblobbar i dessa konton och därför kan inte lagra VHD-filer. Du kan ange en åtkomstnivå till frekvent eller lågfrekvent.

<!--markdownlint-enable MD033 -->

### <a name="storage-redundancy-options"></a>Alternativ för lagringsredundans

Storage-konton kan använda olika typer av redundans för ökad flexibilitet och hög tillgänglighet.

**Typ** | **Detaljer** | **Användning**
--- | --- | ---
**Lokalt redundant lagring (LRS)** | Skyddar mot ett lokalt avbrott genom att replikera inom en enskild lagringsenhet till en separat feldomän och uppdateringsdomän. Behåller flera kopior av dina data i ett datacenter. Innehåller minst 99,999999999% (11 9\'s) objektshållbarhet under ett givet år. | Överväg om din app lagrar data som enkelt kan rekonstrueras.
**Zonredundant lagring (ZRS)** | Skyddar mot datacenteravbrott genom att replikera över tre lagringskluster i samma region. Varje lagringskluster är fysiskt åtskilt och förvaras i en egen tillgänglighetszon. Ger en beständighet på minst 99,9999999999 % (10 decimaler) för objekt under ett år genom att flera kopior av data förvaras i flera datacenter eller flera regioner. | Fundera på om du behöver konsekvens, hållbarhet och hög tillgänglighet. Den skyddar kanske inte mot en regional katastrof där flera zoner påverkas permanent.
**Geografiskt redundant lagring (GRS)** | Skyddar mot avbrott i en hel region genom att replikera data till en sekundär region som ligger hundratals kilometer från den primära. Innehåller minst 99,99999999999999% (16 9\'s) objektshållbarhet under ett givet år. | Replikdata är inte tillgängligt om inte Microsoft initierar en växling till den sekundära regionen. In redundans uppstår är läs- och skrivåtkomst tillgängligt.
**Läsåtkomst till geografiskt redundant lagring (RA-GRS)** | Liknar GRS. Innehåller minst 99,99999999999999% (16 9\'s) objektshållbarhet under ett givet år | Innehåller och 99,99% läsningstillgänglighet genom att läsåtkomst tillåts från den andra regionen som används för GRS.

**Lära sig mer:**

- [Granska](https://azure.microsoft.com/pricing/details/storage) priser för Azure Storage.
- [Lär dig mer om](https://docs.microsoft.com/azure/storage/common/storage-import-export-service) Azure Import/Export för migrering stora mängder data till Azure-blobar och filer.
- [Jämför](https://docs.microsoft.com/azure/storage/common/storage-decide-blobs-files-disks?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) blobar, filer och datatyper för disk-lagring.
- [Läs mer](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers) om åtkomstnivåerna.
- [Granska](https://docs.microsoft.com/azure/storage/common/storage-account-overview?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) olika typer av lagringskonton.
- Lär dig mer om [lagringsredundans](https://docs.microsoft.com/azure/storage/common/storage-redundancy), [LRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), [ZRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-zrs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), [GRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), och [Read-access GRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#read-access-geo-redundant-storage).
- [Läs mer](https://docs.microsoft.com/azure/storage/files/storage-files-introduction) om Azure Files.

## <a name="best-practice-take-advantage-of-azure-hybrid-benefits"></a>Metodtips: Dra nytta av fördelarna med Azure Hybrid

Tack vare åratals programvaruinvesteringar i system som Windows Server och SQL Server har Microsoft en unik möjlighet att ge kunderna mervärde i molnet med avsevärda rabatter som andra molnleverantörer ofta inte kan slå.

En integrerad Microsoft på lokal/Azure produktportfölj genererar konkurrenskraftiga och kostnad fördelar. Om du har ett operativsystem eller andra programvarulicenser genom software assurance (SA), kan du ta dessa licenser med dig till molnet för med Azure Hybrid-förmånen.

**Lära sig mer:**

- [Ta en titt på](https://azure.microsoft.com/pricing/hybrid-benefit) kalkylator för besparingar Hybrid-förmånen.
- [Läs mer](https://azure.microsoft.com/pricing/hybrid-benefit) om Hybrid-förmånen för Windows Server.
- Se [Prisvägledning för virtuella SQL Server Azure-datorer](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance).

## <a name="best-practice-use-reserved-vm-instances"></a>Metodtips: Reserverade instanser för virtuell dator

Molnplattformar är vanligtvis konfigurerade för löpande betalning. Den här modellen anger hur många nackdelarna, eftersom du inte nödvändigtvis vet hur dynamiskt arbetsbelastningar blir. När du anger Rensa avsikter för en arbetsbelastning kan bidra du till infrastrukturplanering.

Med hjälp av Azure reserverade VM-instanser, du betalar i förskott för ett eller tre år, VM-instans.

- Förskottsbetalning ger en rabatt på de resurser du använder.
- Du kan avsevärt minska VM, SQL database-beräkning, Azure Cosmos DB eller andra resurskostnader med upp till 72% jämfört med användningsbaserad betalning.
- Reservationer ger en rabatt på fakturering och påverka inte körtiden för dina resurser.
- Du kan avbryta reserverade instanser.

![Reserverade instanser](./media/migrate-best-practices-costs/reserve.png)
*reserverade virtuella datorer i Azure*

**Lära sig mer:**

- [Lär dig mer om](https://docs.microsoft.com/azure/billing/billing-save-compute-costs-reservations) Azure reservationer.
- [Läs](https://azure.microsoft.com/pricing/reserved-vm-instances/#faq) reserverade instanser vanliga frågor och svar.
- [Hämta prisvägledning](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) för virtuella SQL Server Azure-datorer.

## <a name="best-practice-aggregate-cloud-spend-across-subscriptions"></a>Metodtips: Aggregera molnutgifter över prenumerationer

Det är oundvikligt att du kommer att ha fler än en Azure-prenumeration. Till exempel behöva en ytterligare prenumeration för att avgränsa utveckling och produktion gränser eller du kanske har en plattform som kräver en separat prenumeration för varje klient. Att ha möjlighet att samla in data rapportering för alla prenumerationer i en enda plattform är en viktig funktion.

Om du vill göra detta måste använda du Azure Cost Management API: er. Sedan efter datainsamling i en enda källa, till exempel Azure SQL, kan du använda verktyg som Power BI till att visa aggregerade data. Du kan skapa sammanställda prenumerationsrapporter och detaljerade rapporter. För användare som behöver proaktiva insikter om kostnadshantering kan du skapa särskilda vyer för kostnader baserat på avdelning, resursgrupp m.m. Du behöver inte ge dem fullständig åtkomst till faktureringsdata för Azure.

**Lära sig mer:**

- [Få en översikt](https://docs.microsoft.com/azure/billing/billing-consumption-api-overview) för API i Azure-förbrukning.
- [Lär dig mer om](https://docs.microsoft.com/power-bi/desktop-connect-azure-consumption-insights) ansluter till Azure Consumption Insights i Power BI Desktop.
- [Lär dig hur du](https://docs.microsoft.com/azure/billing/billing-manage-access) hantera åtkomst till faktureringsinformation för Azure med hjälp av rollbaserad åtkomstkontroll (RBAC).

## <a name="after-migration"></a>Efter migrering

Efter en lyckad migrering av dina arbetsbelastningar och ett par veckors samlar in förbrukningsdata, får du en tydlig bild av resurser kostnader.

- När du analyserar data kan du börja Generera en budget baslinje för Azure-resursgrupper och resurser.
- Du kan sedan analysera hur du ytterligare minska kostnaderna när du förstår där din cloud budget spenderas.

Metodtipsen i detta avsnitt är bland annat att använda Azure Cost Management för budgetering och analys, övervaka resurser och införa budgetar för varje resursgrupp och optimera övervakning, lagring och virtuella datorer.

## <a name="best-practice-use-azure-cost-management"></a>Metodtips: Använd Azure Cost Management

Microsoft tillhandahåller Azure Cost Management så att du kan hålla koll på dina utgifter:

- Hjälper dig att övervaka och kontrollera utgifter för Azure och optimera användningen av dina resurser.
- Går igenom hela prenumerationen och alla dess resurser och lämnar rekommendationer.
- Ger en fullständig API för att integrera externa verktyg och finansiella system för rapportering.
- Spårar resursanvändningen och hantera molnkostnader med en enda enhetlig vy.
- Tillhandahåller omfattande drift och ekonomi analyser för att hjälpa dig att fatta välgrundade beslut.

I Cost Management kan du:

- **Skapa en budget:** Skapa en budget för ekonomiskt ansvar.
  - Du kan ta hänsyn till de tjänster som du förbrukar eller prenumererar på under en viss period (varje månad, varje kvartal, varje år) och en omfattning (prenumerationer/resursgrupper). Du kan till exempel skapa en prenumerationsbudget för Azure per månad, kvartal eller år.
    - När du har skapat en budget, visas den i kostnadsanalys. Visa din budget mot aktuell kostnad är en av de första stegen som behövs när du analyserar dina kostnader och utgifter.
  - E-postmeddelanden kan skickas när budgetgränser nås.
  - Du kan exportera kostnadshanteringsdata till Azure-lagring, där de kan analyseras.

    ![Cost Management-budget](./media/migrate-best-practices-costs/budget.png)
    *Azure Cost Management-budget*

- **Skapa en kostnadsanalys:** Ta fram en kostnadsanalys för att utforska och analysera dina driftskostnader och hjälpa dig att förstå hur utgifter skapas samt identifiera utgiftstrender.
  - Kostnadsanalys är tillgängligt för EA-användare.
  - Du kan visa kostnadsanalysdata för olika omfång, inklusive per avdelning, konto, prenumeration eller resursgrupp.
  - Du kan få en kostnadsanalys som visar den totala kostnaden för den aktuella månaden och de ackumulerade dagliga kostnaderna.

    ![Cost Management-analys](./media/migrate-best-practices-costs/analysis.png)
    *Azure Cost Management-analys*
- **Ta fram rekommendationer:** Få rekommendationer från Advisor som visar hur du kan optimera och förbättra effektiviteten.

**Läs mer:**

- [Få en översikt](https://docs.microsoft.com/azure/cost-management/overview) av Azure Cost Management.
- [Lär dig hur du](https://docs.microsoft.com/azure/cost-management/cost-mgt-best-practices) optimera din molninvestering med Azure Cost Management.
- [Lär dig hur du](https://docs.microsoft.com/azure/cost-management/use-reports) Användarrapporter för Azure Cost Management.
- [Hämta en självstudiekurs](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations?toc=/azure/billing/TOC.json) om hur du optimerar kostnaderna från rekommendationer.
- [Granska](https://docs.microsoft.com/rest/api/consumption/budgets) Azure Consumption-API:et.

## <a name="best-practice-monitor-resource-utilization"></a>Metodtips: Övervaka resursutnyttjande

I Azure betalar du för det du använder när resurser förbrukas och endast då. Debitering för virtuella datorer sker när en virtuell dator tilldelas och du debiteras inte efter att den virtuella datorn har frigjorts. Med detta i åtanke bör du övervaka virtuella datorer som används och kontrollera VM-storlek.

- Utvärdera kontinuerligt dina VM-arbetsbelastningar för att fastställa baslinjer.
- Om din arbetsbelastning är används mycket måndag till fredag kl. 8: 00 till 18: 00, men knappt används utanför dessa tider, kan du till exempel nedgradera virtuella datorer utanför Högbelastningstider. Detta kan innebära att ändra VM-storlekar eller virtuell dator använder skalningsuppsättningar för virtuella datorer automatisk skalning upp eller ned.
- Vissa företag ”viloläge”, virtuella datorer genom att sätta dem i en kalender som anger när de ska vara tillgängliga och när de inte behövs.
- Förutom att övervaka dina virtuella datorer för du övervaka andra nätverksresurser, till exempel ExpressRoute och virtuella nätverksgatewayer så att de inte används för mycket eller för lite.
- Du kan övervaka användningen av virtuella datorer med hjälp av Microsoft-verktyg som Azure Cost Management, Azure Monitor och Azure Advisor. Verktyg från tredje part är också tillgängliga.

**Lära sig mer:**

- Få en översikt över [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) och [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview).
- [Hämta](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations) Advisor kostnad rekommendationer.
- [Lär dig [optimera kostnader baserat på rekommendationer](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations?toc=/azure/billing/TOC.json) och [undvika oväntade avgifter](https://docs.microsoft.com/azure/billing/billing-getting-started).
- Lär dig mer om [Azure Resource Optimization (ARO) Toolkit](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practice-implement-resource-group-budgets"></a>Metodtips: Implementera budgetar för resursgrupper

Resursgrupper används ofta för att representera kostnadsgränser. Tillsammans med det här användningsmönstret fortsätter Azure-teamet att utveckla nya och förbättrade sätt att spåra och analysera resource utgifter på olika nivåer, inklusive möjligheten att skapa budgetar på resursgruppen och resurser.

- En resurs grupp budget kan du spåra kostnaderna för en resursgrupp.
- Du kan utlösa aviseringar och köra en mängd olika spelböcker som budgeten har uppnåtts eller överskridits.

**Lära sig mer:**

- [Lär dig hur du](https://docs.microsoft.com/azure/billing/billing-cost-management-budget-scenario) hantera kostnader med Azure-budget.
- [Följ en självstudie](https://docs.microsoft.com/azure/cost-management/tutorial-acm-create-budgets?toc=/azure/billing/TOC.json) för att skapa och hantera en budget med Azure.

## <a name="best-practice-optimize-azure-monitor-retention"></a>Metodtips: Optimera Azure Monitor-kvarhållning

När du flyttar resurser till Azure och aktiverar diagnostisk loggning för dem skapar du stora mängder loggdata. Den här loggdata skickas vanligtvis till ett lagringskonto som är mappad till en Log Analytics-arbetsyta.

- Ju längre loggkvarhållningsperiod för data, Ju mer data du har.
- Inte alla loggdata är lika, och vissa resurser genererar mer loggdata än andra.
- På grund av bestämmelser och efterlevnad är det troligt att du måste behålla loggdata för vissa resurser som är längre än andra.
- Du bör gå igenom en noggrann rad mellan optimera dina kostnader för lagring av loggen och se till att loggdata som du behöver.
- Vi rekommenderar att utvärdera och konfigurera loggning omedelbart när du har slutfört en migrering, så att du inte är utgiftsgräns pengar behålla loggar av ingen betydelse.

**Lära sig mer:**

- [Lär dig](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-usage-and-estimated-costs) mer om användningsövervakning och beräknade kostnader.

## <a name="best-practice-optimize-storage"></a>Metodtips: Optimera lagring

Om du har följt metodtipsen för att välja lagring före migreringen kan du förmodligen dra nytta av några fördelar. Det finns dock förmodligen ytterligare lagringskostnader som du kan optimera. Med tiden blir blobar och filer inaktuella. Data kan inte användas längre, men regelkrav kan innebära att du behöver att hålla en viss tid. Därför kan du inte behöva lagra den på den lagring med höga prestanda som du använde för den ursprungliga migreringen.

Identifiera och flytta inaktuella data till billigare lagring kan ha en stor inverkan på din månatliga storage budget och kostnadsbesparingar. Azure tillhandahåller många sätt att hjälpa dig att identifiera och sedan lagra den här inaktuella data.

- Dra nytta av åtkomstnivåer för lagring för generell användning v2, flytta mindre viktiga data från frekvent till lågfrekvent lagring och arkiverad nivåerna.
- Använd StorSimple för att flytta inaktuella data baserat på anpassade principer.

**Lära sig mer:**

- [Läs mer](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers) om åtkomstnivåerna.
- [Få en översikt](https://docs.microsoft.com/azure/azure-monitor/overview) över StorSimple och [StorSimple-prissättning](https://azure.microsoft.com/pricing/details/storsimple).

## <a name="best-practice-automate-vm-optimization"></a>Metodtips: Automatisera optimering av virtuella datorer

Det ultimata målet med att köra en virtuell dator i molnet är att maximera CPU, minne och använt diskutrymme. Om du identifierar virtuella datorer som inte är optimerade eller har frekventa perioder när de virtuella datorerna inte används är det klokt att antingen stänga ned dem eller skala ned dem med hjälp av skaluppsättningar för virtuella datorer.

Du kan optimera en virtuell dator med Azure Automation, skaluppsättningar för virtuella datorer, automatisk avstängning och skript eller lösningar från tredje part.

**Läs mer:**

- [Lär dig hur du](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-vertical-scale-reprovision) Använd vertikal automatisk skalning.
- [Schema](https://azure.microsoft.com/updates/azure-devtest-labs-schedule-vm-auto-start) autostart för en virtuell dator.
- [Lär dig hur du](https://docs.microsoft.com/azure/automation/automation-solution-vm-management) starta eller stoppa virtuella datorer utanför arbetstid i Azure Automation.
- [Hämta mer information] om [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) och [verktyget](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit)Azure Resource Optimization (ARO).

## <a name="best-practices-use-logic-apps-and-runbooks-with-budgets-api"></a>Metodtips: Använda Logic Apps och Runbooks med budget-API

Azure tillhandahåller ett REST API som har åtkomst till din kundfaktureringsinformation.

- Du kan använda budgetar API: et för att integrera externa system och arbetsflöden som utlöses av mått som du skapar från API-data.
- Du kan hämta användnings-och resurs till din önskade dataanalysverktyg.
- Azures API:er för resursanvändning och RateCard kan hjälpa dig att korrekt förutse och hantera dina kostnader.
- API: er implementeras som en Resursprovider och ingår i API: er som exponeras av Azure Resource Manager.
- Budgetar API kan integreras med Azure Logic Apps och Runbooks.

**Lära sig mer:**

- [Läs mer](https://docs.microsoft.com/rest/api/consumption/budgets) om budgetar API.
- [Få insikter](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) om Azure-användning med fakturerings-API:et.

## <a name="best-practice-implement-serverless-technologies"></a>Metodtips: Implementera serverlös teknik

Arbetsbelastningar på virtuella datorer migreras ofta i befintligt skick för att undvika driftstopp. Ofta virtuella datorer kan vara värd för uppgifter som är tillfälligt, tar en kort period ska köras, eller också många timmar. Till exempel uppgift virtuella datorer som kör schemalagda aktiviteter, till exempel Windows scheduler eller PowerShell-skript. Om dessa uppgifter inte är igång kan du ändå absorbera VM och disk kostnader för lagring.

Efter migreringen kan du efter en grundlig granskning av de här typerna av aktiviteter överväga att migrera dem till serverlös teknik, till exempel Azure Functions eller Azure Batch-jobb. Med den här lösningen behöver du inte längre hantera och underhålla de virtuella datorerna, vilket sparar ytterligare pengar.

**Läs mer:**

- Läs mer om [Azure Functions](https://azure.microsoft.com/services/functions).
- Läs om [Azure Batch](https://azure.microsoft.com/services/batch).

## <a name="next-steps"></a>Nästa steg

Granska andra metodtips:

- [Bästa praxis](./migrate-best-practices-security-management.md) för säkerhet och hantering efter migreringen.
- [Bästa praxis](./migrate-best-practices-networking.md) för nätverk efter migreringen.
