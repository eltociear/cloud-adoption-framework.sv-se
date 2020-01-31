---
title: Nödvändiga komponenter för att migrera till Azure
description: Nödvändiga komponenter för att migrera till Azure
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 9baf2c9fdd307125e80fa77d8b2be54bec15b931
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806993"
---
::: zone target="chromeless"

# <a name="prerequisites"></a>Krav

::: zone-end

::: zone target="docs"

# <a name="prerequisites-for-migrating-to-azure"></a>Nödvändiga komponenter för att migrera till Azure

::: zone-end

Resurserna i det här avsnittet hjälper dig att förbereda den aktuella miljön för migrering till Azure.

# <a name="overviewtaboverview"></a>[Översikt](#tab/Overview)

Exempel på orsaker till att migrera till Azure är att ta bort risker som är kopplade till äldre maskinvara, minska kapitalkostnaden, frigöra datacenterutrymme och snabbt realisera avkastning (ROI).

- **Eliminera äldre maskinvara.** Du kan ha program som finns på en infrastruktur som närmar sig livscykelns eller supportens slut, antingen lokalt eller hos en värdleverantör. Migrering till molnet utgör en attraktiv lösning på utmaningen eftersom möjligheten att migrera ”i befintligt skick” gör att teamet snabbt kan lösa den nuvarande utmaningen med infrastrukturlivscykel och sedan rikta sin uppmärksamhet mot långsiktig planering för programlivscykel och optimering i molnet.
- **Hantera supportens slut för programvara.** Du kan ha program som är beroende av annan programvara eller operativsystem som närmar sig supportens slut. Om du flyttar till Azure kan det innebära utökade supportalternativ för dessa beroenden eller andra migreringsalternativ som minimerar omstruktureringskrav för att hantera dina program framöver. Se till exempel [utökade supportalternativ för Windows Server 2008 och SQL Server 2008](https://azure.microsoft.com/blog/announcing-new-options-for-sql-server-2008-and-windows-server-2008-end-of-support).
- **Minska kapitalkostnaden.** Att vara värd för din egen serverinfrastruktur kräver betydande investeringar i maskinvara, programvara, elektricitet och personal. Att migrera till en molnlösning kan ge betydande minskningar av kapitalkostnaden. För att uppnå bästa möjliga minskningar av kapitalkostnaden kan en omstrukturering av lösningen krävas. Men en ”i befintligt skick”-migrering är ett mycket bra första steg.
- **Frigör datacenterutrymme.** Du kan välja Azure för att utöka datacenterkapaciteten. Ett sätt att göra det är att använda molnet som en utökning av de lokala funktionerna.
- **Realisera snabbt avkastning på investering.** Att få avkastning på investering (ROI) är mycket enklare med molnlösningar, eftersom molnbetalningsmodellen ger bra användningsinsikter och främjar en kultur för att realisera avkastning på investering.

Vart och ett av scenarierna ovan kan vara startpunkter för att utöka ditt molnfotavtryck med en annan metod (ändra värdtjänster, struktur, arkitektur, utformning eller ersätt).

## <a name="migration-characteristics"></a>Migreringsegenskaper

Guiden förutsätter att din digitala egendom före migreringen främst består av lokal värdbaserad infrastruktur och kan omfatta värdbaserade affärskritiska program. Efter en lyckad migrering kan din dataegendom till stor del se ut som den gjorde lokalt, men med infrastrukturen i molnresurser. Alternativt är den idealiska dataegendomen en variant av din aktuella dataegendom, eftersom den har aspekter av din lokala infrastruktur med komponenter som har omstrukturerats för att optimera och utnyttja molnplattformen.

Fokus för migreringen är att uppnå:

- Åtgärd av livscykelns slut för äldre maskinvara.
- Minskning av kapitalkostnaden.
- Avkastning på investering.

> [!NOTE]
> En ytterligare fördel med migreringen är modellen med ytterligare programvarusupport för Windows 2008, Windows 2008 R2, SQL Server 2008 och SQL Server 2008 R2. Mer information finns i:
>
> - [Windows Server 2008 och Windows Server 2008 R2](https://www.microsoft.com/cloud-platform/windows-server-2008).
> - [SQL Server 2008 och SQL Server 2008 R2](https://www.microsoft.com/sql-server/sql-server-2008).

# <a name="understand-migration-approachestabapproach"></a>[Förstå migreringsmetoder](#tab/Approach)

Den strategi och de verktyg som du använder för att migrera ett program till Azure beror huvudsakligen på dina affärsmål, teknikkrav och tidslinjer samt på en djup förståelse för den faktiska arbetsbelastning och de tillgångar (infrastruktur, appar och data) som migreras.

Innan du fastställer din molnmigreringsstrategi analyserar du kandidatprogram för att identifiera deras kompatibilitet med molnvärdtekniker. Använd Cloud Adoption Frameworks [beslutsguide för migreringsverktyg](../../decision-guides/migrate-decision-guide/index.md) som hjälp att komma igång med processen.

En IaaS-fokuserad migrering, där servrar (tillsammans med deras associerade program och data) får ny värd i molnet med hjälp av virtuella datorer (VM), är ofta den enklaste metoden för att flytta arbetsbelastningar till molnet. Men tänk på att korrekt konfigurering, skydd och underhåll av virtuella datorer kan kräva mer tid och IT-kunskaper jämfört med att använda PaaS-tjänster i Azure. Om du överväger att använda Azure Virtual Machines bör du tänka på att det kräver löpande underhåll för korrigering, uppdatering och hantering av VM-miljön.

När du utvärderar arbetsbelastningar för migrering identifierar du program som inte skulle kräva avsevärd modifiering för att köras med PaaS-tekniker, till exempel Azure App Service eller initierare som Azure Kubernetes Service. De apparna bör vara de första kandidaterna för modernisering och molnoptimering.

## <a name="learn-more"></a>Läs mer

- [Cloud Adoption Frameworks beslutsguide för migreringsverktyg](../../decision-guides/migrate-decision-guide/index.md)
- [Rationalisering – fem punkter](../../digital-estate/5-rs-of-rationalization.md)

# <a name="planning-checklisttabchecklist"></a>[Checklista för planering](#tab/Checklist)

Innan du påbörjar en migrering måste du uppfylla vissa förutsättningar. De exakta detaljerna för de här aktiviteterna varierar beroende på miljön som migreras. I allmänhet gäller följande checklista:

> [!div class="checklist"]
>
> - **Identifiera intressenter:** Identifiera de viktiga personer som har en roll eller ett intresse i resultatet av migreringen.
> - **Identifiera viktiga milstolpar:** För att effektivt planera tidslinjerna för migreringen identifierar du viktiga milstolpar.
> - **Identifiera migreringsstrategin:** Bestäm vilka av de fem punkterna för rationalisering du ska använda.
> - **Utvärdera den tekniska lämpligheten:** Validera teknisk beredskap och lämplighet för migrering och fastställ vilken nivå av stöd du kan behöva från externa partner eller Azure Support.
> - **Migreringsplanering:** Utför den detaljerade utvärderingen och planeringen som krävs för att förbereda dina tillgångar (infrastruktur, appar och data) samt Azure-infrastruktur för migreringen.
> - **Testa migreringen:** Validera migreringsplanen genom att utföra en testmigrering med begränsat omfång.
> - **Migrera dina tjänster:** Utför den faktiska migreringen.
> - **Efter migreringen:** Förstå vad som krävs när du har migrerat miljön till Azure.

Förutsatt att du väljer en metod med ny värd för migrering är följande aktiviteter också relevanta:

> [!div class="checklist"]
>
> - **Styrningsjustering:** Har enighet nåtts avseende justering av styrning med migreringsgrunden?
> - **Nätverk:** En nätverksstrategi bör väljas och justeras utifrån IT-säkerhetskrav.
> - **Identitet:** En hybrididentitetsstrategi bör justeras så att den passar planen för identitetshantering och molnimplementering.

::: zone target="docs"

<!-- markdownlint-disable MD024 -->

## <a name="learn-more"></a>Läs mer

- [Rationalisering – fem punkter](../../digital-estate/5-rs-of-rationalization.md)
- [Beslutsguide för migreringsverktyg](../../decision-guides/migrate-decision-guide/index.md)
- [Cloud Adoption Frameworks checklista för planering](../migration-considerations/prerequisites/planning-checklist.md)

::: zone-end
