---
title: Utvärdera den digitala egendomen
description: Det här avsnittet i Azures migreringsguide hjälper dig att utvärdera din miljö för att avgöra vad som ska migreras och vilka migreringsmetoder som ska beaktas.
author: matticusau
ms.author: mlavery
ms.date: 08/08/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 9c4d5bac8046cc27399b2be7bc0b8ce82ea65769
ms.sourcegitcommit: 238e7a06b56950cebdcc8f75924849fc995e6ff2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/12/2020
ms.locfileid: "77173391"
---
# <a name="assess-the-digital-estate"></a>Utvärdera den digitala egendomen

Vid en idealisk migrering skulle varje tillgång (infrastruktur, app eller data) vara kompatibel med en molnplattform och redo för migrering. I verkligheten är det inte allting som bör migreras till molnet. Dessutom är inte alla tillgångar kompatibla med molnplattformarna. Innan du migrerar en arbetsbelastning till molnet är det viktigt att utvärdera arbetsbelastningen och varje relaterad tillgång (infrastruktur, appar och data).

Resurserna i det här avsnittet hjälper dig att utvärdera din miljö och avgöra om den är lämplig att migrera, samt vilka metoder som skulle kunna användas.

<!-- markdownlint-disable MD025 -->

# <a name="toolstabtools"></a>[Verktyg](#tab/Tools)

Följande verktyg hjälper dig att utvärdera din miljö för att avgöra lämpligheten för en migrering och den bästa metoden att använda. Information om hur du väljer rätt verktyg för migreringen finns i [Cloud Adoption Frameworks beslutsguide för migreringsverktyg](../../decision-guides/migrate-decision-guide/index.md).

## <a name="azure-migrate"></a>Azure Migrate

Azure Migrate-tjänsten utvärderar lokal infrastruktur, program och data för migrering till Azure. Tjänsten utvärderar de lokala resursernas migreringslämplighet, utför prestandabaserad storleksanpassning och tillhandahåller uppskattningar av vad det kostar att köra lokala resurser i Azure. Om du överväger ”Lift and Shift”-migreringar eller om du är i ett tidigt utvärderingsskede av migreringen är den här tjänsten något för dig. När du har slutfört utvärderingen kan du utföra migreringen med Azure Migrate.

![Översikt över Azure Migrate](./media/assess/azuremigrate-overview-1.png)

### <a name="create-a-new-server-migration-project"></a>Skapa ett nytt servermigreringsprojekt

Följ stegen nedan för att komma igång med en utvärdering av servermigrering med Azure Migrate:

1. Välj **Azure Migrate**.
1. I **översikten** klickar du på **Utvärdera och migrera servrar**.
1. Välj **Lägg till verktyg**.
1. I **Discover, assess and migrate servers** (Identifiera, utvärdera och migrera servrar) klickar du på **Lägg till verktyg**.
1. I **Migrera projekt** väljer du din Azure-prenumeration och skapar en resursgrupp om du inte har någon.
1. I **Projektinformation** anger du projektnamnet och geografin där du vill skapa projektet och klickar på **Nästa**.
1. I **Välj utvärderingsverktyg** väljer du **Hoppa över att lägga till ett utvärderingsverktyg just nu** > Nästa.
1. I **Välj migreringsverktyg** väljer du  **Azure Migrate: Servermigrering > Nästa**.
1. I **Review + add tools** (Granska + lägg till verktyg)
granskar du inställningarna och klickar på **Lägg till verktyg**
1. När du har lagt till verktyget visas det i **Azure Migrate-projekt > Servrar > Migreringsverktyg**.

::: zone target="chromeless"

::: form action="Blade[#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview]" submitText="Assess and migrate servers" :::

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
- Om du har datorer utan Internetanslutning måste du dessutom ladda ned och installera Log Analytics-gatewayen på dem.

<!-- markdownlint-disable MD024 -->

### <a name="learn-more"></a>Läs mer

- [Använda lösningen Tjänstkarta i Azure](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)
- [Azure Migrate och Tjänstkarta: Visualisering av beroenden](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization)

# <a name="scenarios-and-stakeholderstabscenarios"></a>[Scenarier och intressenter](#tab/Scenarios)

## <a name="scenarios"></a>Scenarier

Den här guiden fokuserar på följande scenarier:

- **Äldre maskinvara:** Du migrerar för att ta bort ett beroende på äldre maskinvara där supporten eller livscykeln snart upphör.
- **Kapacitetstillväxt:** Du måste öka kapaciteten för tillgångar (infrastruktur, appar och data) som den aktuella infrastrukturen inte kan tillhandahålla.
- **Modernisering av datacenter:** Du måste utöka eller modernisera ditt datacenter med molnteknik för att säkerställa att verksamheten förblir aktuell och konkurrenskraftig.
- **Program- eller tjänstmodernisering:** Du vill uppdatera dina program så att de utnyttjar molnets inbyggda funktioner. Även om du valt att genomföra en migreringsstrategi som innebär byte av värd i första hand är det brukligt att se till att det finns möjligheter att skapa planer för granskning av program och tjänster, samt eventuell modernisering i migreringen.

### <a name="organizational-alignment-and-stakeholders"></a>Organisatorisk anpassning och intressenter

Den fullständiga listan med intressenter kan variera mellan migreringsprojekten. Det är bäst att anta att du inte känner till alla intressenter i början av planeringen för en migrering, eftersom intressenter ofta bara identifieras under vissa faser i projektet. Innan du startar ett migreringsprojekt kan du dock identifiera viktiga verksamhetsledare från ekonomi, IT-infrastruktur och programgrupper som har intresse i din organisations övergripande molnmigrering.

Att upprätta ett kärnteam för molnstrategin med dessa viktiga intressenter på hög nivå, kan vara till hjälp när du förbereder din organisation på molnimplementeringen och dina övergripande åtgärder för molnmigreringen. Det här teamet ansvarar för att förstå molnteknikerna och migreringsprocesserna, identifiera affärsmotiveringen för migreringar och fastställa de bästa lösningarna för migreringen. De hjälper också till att identifiera och arbeta med specifika program- och affärsintressenter för att säkerställa en lyckad migrering.

Mer information om hur du förbereder din organisation på molnmigreringen finns i Cloud Adoption Framework-artikeln om den [inledande organisatoriska anpassningen](../../plan/initial-org-alignment.md).

# <a name="timelinestabtimelines"></a>[Tidslinjer](#tab/Timelines)

I allmänhet ser kunderna att migreringsscenariot i den här guiden kan slutföras inom en till sex månader.

Några viktiga faktorer att tänka på när man utvärderar tidslinjen för migreringen är:

- **Tillgångar (infrastruktur, appar och data) som ska migreras:** Antalet och mångfalden av tillgångar.
- **Personalens beredskap:** Är personalen redo att hantera den nya miljön eller behöver de utbildning?
- **Finansiering:** Har du lämpligt godkännande och budget för att slutföra migreringen?
- **Ändringshantering:** Har företaget specifika krav angående ändringsimplementering och godkännande?
- **Segmentföreskrifter:** Måste du följa segment- eller branschföreskrifter?

# <a name="cost-managementtabmanagecost"></a>[Kostnadshantering](#tab/ManageCost)

Utvärderingen av din miljö bjuder på ett perfekt tillfälle att inkludera ett kostnadsanalyssteg. Med hjälp av de data som samlats in vid utvärderingen bör du kunna analysera och förutse kostnaderna. Den här kostnadsförutsägelsen bör innehålla både förbrukningskostnader för tjänsten samt eventuella engångskostnader (till exempel ökad mängd inkommande data).

Under migreringen finns det vissa faktorer som påverkar beslut och körning:

- **Storlek på den digitala egendomen:** Att förstå storleken på din digitala egendom har en direkt påverkan på de beslut och de resurser som krävs för att utföra migreringen.
- **Redovisningsmodeller:** Gå från en strukturerad modell för kapitalkostnader till en modell med rörliga driftskostnader.

::: zone target="docs"

Följande resurser innehåller relaterad information:

- [Beräkna molnkostnader](../migration-considerations/assess/estimate.md)

::: zone-end
