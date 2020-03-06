---
title: Utvärdera varje arbetsbelastning och förfina planer
description: Det här avsnittet i Azures migreringsguide hjälper dig att utvärdera din miljö för att avgöra vad som ska migreras och vilka migreringsmetoder som ska beaktas.
author: matticusau
ms.author: mlavery
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 40e62a05101e14fcd7507011d521521e58920ffc
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78225538"
---
# <a name="assess-each-workload-and-refine-plans"></a>Utvärdera varje arbetsbelastning och förfina planer

Resurserna i den här guiden hjälper dig att utvärdera varje arbetsbelastning, utmaningsantaganden för varje arbetsbelastnings lämplighet för migrering och att slutföra arkitektoniska beslut om migreringsalternativ.

<!-- markdownlint-disable MD025 -->

# <a name="tools"></a>[Verktyg](#tab/Tools)

Om du inte följer anvisningarna i länkarna ovan behöver du troligtvis data och ett utvärderingsverktyg för att fatta välgrundade beslut om migrering. Azure Migrate är det inbyggda verktyget för att utvärdera **och** migrera till Azure. Om du inte redan har gjort det kan du använda de här stegen för att skapa ett nytt servermigreringsverktyg för samla in nödvändiga data.

## <a name="azure-migrate"></a>Azure Migrate

Azure Migrate utvärderar lokal infrastruktur, program och data för migrering till Azure. Den här tjänsten:

- Utvärderar migreringens lämplighet för lokala tillgångar.
- Utför prestandabaserad storleksbestämning.
- Tillhandahåller kostnadsuppskattningar för att köra lokala tillgångar i Azure.

Om du överväger en ”Lift and Shift”-metod eller om du är i ett tidigt utvärderingsskede av migreringen är den här tjänsten något för dig. När du har slutfört utvärderingen kan du utföra migreringen med Azure Migrate.

![Översikt över Azure Migrate](./media/assess/azure-migrate-overview-1.png)

### <a name="create-a-new-server-migration-project"></a>Skapa ett nytt servermigreringsprojekt

Påbörja en utvärdering av servermigrering med Azure Migrate med följande steg:

1. Välj **Azure Migrate**.
1. I **översikten** väljer du **Utvärdera och migrera servrar**.
1. Välj **Lägg till verktyg**.
1. I **Identifiera, utvärdera och migrera servrar** väljer du **Lägg till verktyg**.
1. I **Migrera projekt** väljer du din Azure-prenumeration och skapar en resursgrupp om du inte har någon.
1. I **Projektinformation** anger du projektnamnet och geografin där du vill skapa projektet och klickar sedan på **Nästa**.
1. I **Välj utvärderingsverktyg** väljer du **Hoppa över att lägga till ett utvärderingsverktyg just nu** > Nästa.
1. I **Välj migreringsverktyg** väljer du  **Azure Migrate: Servermigrering > Nästa**.
1. I **Granska + lägg till verktyg**
granskar du inställningarna och väljer sedan **Lägg till verktyg**.
1. När du har lagt till verktyget visas det i **Azure Migrate-projekt > Servrar > Migreringsverktyg**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview]" submitText="Assess and migrate servers" :::

::: zone-end

::: zone target="docs"

### <a name="learn-more"></a>Läs mer

- [Översikt över Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview)
- [Migrera fysiska eller virtualiserade servrar till Azure](https://docs.microsoft.com/azure/migrate/tutorial-migrate-physical-virtual-machines)
- [Azure Migrate i Azure-portalen](https://portal.azure.com/#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview)

::: zone-end

## <a name="service-map"></a>Tjänstkarta

Tjänstkarta identifierar automatiskt programkomponenter i Windows- och Linux-system och mappar kommunikationen mellan olika tjänster. Med Tjänstkarta kan du se dina servrar på samma sätt som du tänker på dem, dvs. som sammankopplade system som levererar kritiska tjänster. Tjänstkarta visar anslutningar mellan servrar, processer, inkommande och utgående anslutningssvarstid, samt portar i valfri TCP-ansluten arkitektur, utan att det krävs någon konfiguration förutom installationen av en agent.

Azure Migrate använder Tjänstkarta till att förbättra rapporteringsfunktioner och beroenden i miljön. Fullständig information om den här integreringen finns i [Visualisering av beroenden](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization). Om du använder Azure Migration-tjänsten krävs det inte några ytterligare steg för att konfigurera och få fördelarna med Tjänstkarta. Följande anvisningar gäller om du vill använda Tjänstkarta för andra syften eller projekt.

### <a name="enable-dependency-visualization-using-service-map"></a>Aktivera visualisering av beroenden med Tjänstkarta

Om du vill använda beroendevisualisering måste du ladda ned och installera agenter på varje lokal dator som du vill analysera.

- [Microsoft Monitoring Agent (MMA)](https://docs.microsoft.com/azure/log-analytics/log-analytics-agent-windows) måste vara installerad på varje dator.
- [Microsofts beroendeagent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud#install-the-dependency-agent-on-windows) måste vara installerad på varje dator.
- Om du har datorer utan Internetanslutning ska du ladda ned och installera Log Analytics-gatewayen på dem.

<!-- markdownlint-disable MD024 -->

### <a name="learn-more"></a>Läs mer

- [Använda lösningen Tjänstkarta i Azure](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)
- [Azure Migrate och Tjänstkarta: Visualisering av beroenden](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization)

# <a name="challenge-assumptions"></a>[Utmaningsantaganden](#tab/Challenge-Assumptions)

Vid en idealisk migrering skulle varje tillgång (infrastruktur, app eller data) vara kompatibel med en molnplattform och redo för migrering eller modernisering. I verkligheten bör inte alla arbetsbelastningar migreras till molnet. Alla tillgångar är inte kompatibla med molnplattformarna. Innan du migrerar en arbetsbelastning till molnet ska du utvärdera varje arbetsbelastning och alla beroende tillgångar (infrastruktur, appar och data).

[Planmetodiken för Cloud Adoption Framework](../../plan/index.md) råder läsarna att använda [stegvis rationalisering](../../digital-estate/rationalize.md#incremental-rationalization) och metoder för att [prioritera tio](../../digital-estate/rationalize.md#release-planning) för att utvärdera och planera för migreringen. Den här guiden innehåller också detaljerade metodtips för [att använda Azure Migrate för att utvärdera din digitala egendom](../../plan/contoso-migration-assessment.md).

Länkarna ovan pekar på att antaganden är acceptabla och ofta uppmuntras under planeringsstegen för migreringen. Men nu är det dags att vidta åtgärder. De här antagandena bör begränsas för varje arbetsbelastnings grund innan du migrerar till molnet.

## <a name="two-steps-of-incremental-rationalization"></a>Två steg för stegvis rationalisering

Två lika stora steg krävs för att du ska kunna leverera [stegvis rationalisering](../../digital-estate/rationalize.md#incremental-rationalization). Båda stegen kräver data och insikter i miljön. Men varje metod tar hänsyn till mängden tid detaljerad information som krävs för att lyckas med migreringen.

- **[Lanseringsplanering utifrån ”prioritera 10”-metoden ](../../digital-estate/rationalize.md#release-planning):** Under den inledande rationaliseringen och versionsplaneringen ska endast en av de [fem punkterna för rationalisering](../../digital-estate/5-rs-of-rationalization.md) användas i utvärderingen. Beräkna och planera baserat på det rationaliseringsalternativ som bäst överensstämmer med de övergripande motiveringarna som definieras i [dokumentet om molnimplementeringsstrategier](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).

- **Detaljerad utvärdering av varje arbetsbelastning:** De antaganden som är kopplade till lanseringsplanering utifrån ”prioritera 10”-metoden tillräckliga för att skapa en plan. Men samma antaganden kan orsaka betydande problem om de inte utvärderas innan migreringen.

## <a name="challenge-assumptions-and-update-the-plan"></a>Utmaningsantaganden och uppdatering av planen

Granska utvärderingsdata i Azure Migrate eller det valda utvärderingsverktyget. Dessa data ger insikter om kompatibilitetsproblem, reparationskrav, storleksförslag och andra överväganden.

Innan du migrerar bör du använda dessa data tillsammans med identifieringskonversationer med produktägaren, utvecklingsteamet, administratörer och andra för att utvärdera möjligheten att migrera denna speciella arbetsbelastning. Använd den här identifieringen för att utmana grundantaganden om den här arbetsbelastningen. Om resultatet ändrar migrerings- eller implementeringsplanen uppdaterar du planen enligt detta.

Det första steget i att utmana dessa antaganden är en [granskning av alla 5 punkter](../../digital-estate/rationalize.md).

    - Fungerar den antagna rationaliseringsmetoden för den här arbetsbelastningen? Är det det bästa sättet?
    - Kommer [replikeringens funktion](../migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication) påverka migreringen av arbetsbelastningen?
    - Kräver den här arbetsbelastningen [åtgärdsaktiviteter](../migration-considerations/assess/evaluate.md) innan migreringen?

Sådana här typer av frågor hjälper till att utmana antaganden och leder till den bästa metoden för varje arbetsbelastning.

En utökad lista över frågor och en definierad process för att validera antaganden finns i [översikten över förbättringar av utvärderingsprocessen](../migration-considerations/assess/index.md).

# <a name="scenarios-and-stakeholders"></a>[Scenarier och intressenter](#tab/Scenarios)

## <a name="scenarios"></a>Scenarier

Den här guiden beskriver följande scenarier:

- **Äldre maskinvara:** Migrera för att ta bort ett beroende på äldre maskinvara där supporten eller livscykeln snart upphör.
- **Kapacitetstillväxt:** Öka kapaciteten för tillgångar (infrastruktur, appar och data) som den aktuella infrastrukturen inte kan tillhandahålla.
- **Modernisering av datacenter:** Utöka eller modernisera ditt datacenter med molnteknik för att säkerställa att verksamheten förblir aktuell och konkurrenskraftig.
- **Program- eller tjänstmodernisering:** Uppdatera dina program så att de utnyttjar molnets inbyggda funktioner. Även om du valt att genomföra en migreringsstrategi som innebär byte av värd i första hand är det brukligt att se till att det finns möjligheter att skapa planer för granskning av program och tjänster, samt eventuell modernisering i migreringen.

### <a name="organizational-alignment-and-stakeholders"></a>Organisatorisk anpassning och intressenter

Den fullständiga listan med intressenter kan variera mellan migreringsprojekten. Det är bäst att anta att du inte känner till alla intressenter i början av planeringen för en migrering, eftersom intressenter ofta bara identifieras under vissa faser i projektet. Innan du startar ett migreringsprojekt kan du dock identifiera viktiga verksamhetsledare från ekonomi, IT-infrastruktur och programgrupper som har intresse i din organisations övergripande molnmigrering.

Att upprätta ett kärnteam för molnstrategin med dessa viktiga intressenter på hög nivå, kan vara till hjälp när du förbereder din organisation på molnimplementeringen och dina övergripande åtgärder för molnmigreringen. Det här teamet ansvarar för att förstå molnteknikerna och migreringsprocesserna, identifiera affärsmotiveringen för migreringar och fastställa de bästa lösningarna för migreringen. De hjälper också till att identifiera och arbeta med specifika program- och affärsintressenter för att säkerställa en lyckad migrering.

Mer information om hur du förbereder din organisation för molnmigreringen finns i Cloud Adoption Framework-guiden om den [inledande organisatoriska anpassningen](../../plan/initial-org-alignment.md).

# <a name="timelines"></a>[Tidslinjer](#tab/Timelines)

Kunderna tycker vanligen att migreringsscenariot i den här guiden kan slutföras inom en till sex månader.

När du utvärderar tidslinjen för migreringen bör du överväga:

- **Tillgångar (infrastruktur, appar och data) som ska migreras:** Antalet och mångfalden av tillgångar.
- **Personalens beredskap:** Är personalen redo att hantera den nya miljön eller behöver de utbildning?
- **Finansiering:** Har du lämpligt godkännande och budget för att slutföra migreringen?
- **Ändringshantering:** Har företaget specifika krav angående ändringsimplementering och godkännande?
- **Segmentföreskrifter:** Måste du följa segment- eller branschföreskrifter?

# <a name="cost-management"></a>[Kostnadshantering](#tab/ManageCost)

Att utvärdera din miljö ger en bra möjlighet att inkludera ett kostnadsanalyssteg. Med hjälp av de data som samlats in vid utvärderingen bör du kunna analysera och förutse kostnaderna. Den här kostnadsförutsägelsen bör innehålla både förbrukningskostnader för tjänsten samt eventuella engångskostnader (till exempel ökad mängd inkommande data).

Under migreringen finns det vissa faktorer som påverkar beslut och körning:

- **Storlek på den digitala egendomen:** Att förstå storleken på din digitala egendom har en direkt påverkan på de beslut och de resurser som krävs för att utföra migreringen.
- **Redovisningsmodeller:** Gå från en strukturerad modell för kapitalkostnader till en modell med rörliga driftskostnader.

::: zone target="docs"

Följande resurser innehåller relaterad information:

- [Beräkna molnkostnader](../migration-considerations/assess/estimate.md)

::: zone-end
