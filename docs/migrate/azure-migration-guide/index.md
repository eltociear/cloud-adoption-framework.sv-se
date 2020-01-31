---
title: Introduktion till guiden för Azure-migrering
description: Lär dig att effektivt migrera din organisations tjänster till Azure med stegvis vägledning.
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 6f5592c93bb78b14a85e37ffa67ffea697a12345
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807044"
---
::: zone target="docs"

# <a name="azure-migration-guide-before-you-start"></a>Azure-migreringsguiden: Innan du börjar

::: zone-end

::: zone target="chromeless"

# <a name="before-you-start"></a>Innan du börjar

::: zone-end

Innan du migrerar resurser till Azure behöver du välja den migreringsmetod och de funktioner som du kommer att använda för att styra och skydda din miljö. Den här guiden leder dig genom beslutsprocessen.

::: zone target="docs"

> [!TIP]
> Visa den här guiden i Azure-portalen om du vill ha en interaktiv upplevelse. Gå till [Azure Quickstart Center](https://portal.azure.com/?feature.quickstart=true#blade/Microsoft_Azure_Resources/QuickstartCenterBlade) i Microsoft Azure-portalen, välj **Migrera din miljö till Azure** och följ instruktionerna.

::: zone-end

# <a name="overviewtaboverview"></a>[Översikt](#tab/Overview)

Den här guiden leder dig igenom grunderna i att migrera program och resurser från din lokala miljö till Azure. Den är utformad för migreringsomfång med minimal komplexitet. Du kan avgöra huruvida den här guiden passar för din migrering genom att gå till fliken **När du bör använda den här guiden**.

När du migrerar till Azure kan du migrera dina program som de är med hjälp av IaaS-baserade VM-lösningar (detta kallas migrering med _värdbyte_ eller _lift and shift_), eller så har du kanske flexibiliteten att använda hanterade tjänster och andra molnbaserade funktioner för att modernisera dina program. Mer information om de här alternativen finns på fliken **Migreringsalternativ**. När du utvecklar en migreringsstrategi bör du överväga följande:

- Kommer mina migrerande program att fungera i molnet?
- Vilken är den bästa strategin (vad gäller teknik, verktyg och migreringar) för mitt program? Se Microsoft Cloud Adoption Frameworks [beslutsguide för migreringsverktyg](../../decision-guides/migrate-decision-guide/index.md) för mer information.
- Hur minimerar jag nedtid under migreringen?
- Hur begränsar jag kostnaderna?
- Hur gör jag för att spåra resurskostnader och fakturera dem på rätt sätt?
- Hur säkerställer jag att vi efterlever och uppfyller regler?
- Hur gör jag för att uppfylla juridiska krav för datasuveränitet i vissa länder?

Den här guiden ger svar på dessa frågor. Där finns förslag på uppgifter och funktioner som du kan överväga när du förbereder distribution av resurser i Azure, däribland följande:

> [!div class="checklist"]
>
> - **Konfigurera förutsättningar.** Planera och förbered för migrering.
> - **Utvärdera den tekniska lämpligheten.** Kontrollera teknisk beredskap och lämplighet för migrering.
> - **Hantera kostnader och fakturering.** Gå igenom kostnaderna för dina resurser.
> - **Migrera dina tjänster.** Utför den faktiska migreringen.
> - **Organisera dina resurser.** Lås resurser som är kritiska för ditt system och tagga resurser för att spåra dem.
> - **Optimera och transformera.** Använd tillfället efter migrering för att granska resurserna.
> - **Skydda och hantera.** Kontrollera att miljön är säker och att den övervakas korrekt.
> - **Få hjälp.** Få hjälp och stöd under migreringen eller aktiviteter efter migrering.

::: zone target="docs"

I [Styrning i Azure](https://docs.microsoft.com/azure/security/governance-in-azure) kan du lära dig mer om att organisera och strukturera prenumerationer, hantera distribuerade resurser och uppfylla företagets policykrav.

::: zone-end

# <a name="when-to-use-this-guidetabwhentousethisguide"></a>[När du bör använda den här guiden](#tab/WhenToUseThisGuide)

Även om de verktyg som beskrivs i den här guiden stöder en mängd olika migreringsscenarier fokuserar den här guiden på projekt med begränsat omfång och _minimal komplexitet_. Avgör huruvida den här migreringsguiden är lämpligt för ditt projekt genom att se om följande villkor gäller för dig:

- Du migrerar en homogen miljö.
- Endast ett fåtal affärsenheter behöva inriktas för att slutföra migreringen.
- Du planerar att inte automatisera hela migreringen.
- Du migrerar ett litet antal servrar.
- Beroendemappningen för de komponenter som ska migreras är enkel att definiera.
- Din bransch har minimala regelkrav som är relevanta för den här migreringen.

Om något av dessa villkor _inte_ gäller för din situation bör du i stället överväga [guiden för utökat omfång](../expanded-scope/index.md). Vi rekommenderar även att du begär hjälp från något av våra Microsoft-team eller partner för att genomföra migreringar som kräver guiden för utökat omfång. Kunder som tar hjälp av Microsoft eller certifierade partner lyckas bättre i dessa scenarier. Mer information om hur du begär hjälp finns i den här guiden.

<!-- markdownlint-enable MD033 -->

::: zone target="docs"

Mer information finns i:

- [Guiden för utökat omfång](../expanded-scope/index.md)

::: zone-end

# <a name="migration-optionstabmigrationoptions"></a>[Migreringsalternativ](#tab/MigrationOptions)

Du kan utföra en molnmigrering på flera olika sätt. Vissa passar bättre för en del scenarier än andra. När du avgör hur du ska migrera din miljö bör du överväga följande alternativ vid valet av migreringsstrategi:

- **Värdbyte:** Värdbyte kallas även ”lift and shift” och innebär att flytta det aktuella tillståndet till Azure med minimala ändringar i den övergripande arkitekturen.
- **Refaktorisering:** PaaS-alternativ (plattform som en tjänst) kan minska de driftskostnader som är associerade med många program. Det kan vara bra att utföra viss refaktorisering av ett program så att det passar en PaaS-modell. Detta avser även programutvecklingsprocessen med att refaktorisera kod så att ett program kan leverera nya affärsmöjligheter.
- **Arkitekturomarbetning:** Vissa föråldrade program är inte kompatibla med molnleverantörer på grund av arkitektoniska beslut som togs när programmet skapades. I de fallen kan programmets arkitektur behöva omarbetas som en del av migreringen.
- **Återskapa:** I vissa situationer kan de ändringar som krävs för att migrera ett program vara för stora för att motivera ytterligare investering, och då måste lösningen återskapas.
- **Ersätta:** Lösningar implementeras vanligtvis med hjälp av den bästa tekniken som finns då de byggs. I vissa fall kan moderna SaaS-program (programvara som en tjänst) uppfylla alla funktioner som tillhandahålls av det värdhanterade programmet. I dessa scenarier kan en arbetsbelastning schemaläggas för framtida ersättning, vilket gör att den inte längre övervägs som en del av migreringen.

::: zone target="chromeless"

Dessa metoder är inte ömsesidigt uteslutande – till exempel använder din första migrering kanske en **värdbytesmodell**, men då kan du välja att implementera **refaktorisering** eller **arkitekturomarbetning** som en del av fasen för optimering efter migrering. Detta beskrivs närmare i avsnittet **Optimera och transformera** i den här guiden.

::: zone-end

::: zone target="docs"

Dessa metoder är inte ömsesidigt uteslutande – till exempel använder din första migrering kanske en **värdbytesmodell**, men då kan du välja att implementera **refaktorisering** eller **arkitekturomarbetning** som en del av fasen för optimering efter migrering. Detta beskrivs närmare i avsnittet [Optimera och transformera](./optimize-and-transform.md) i den här guiden.

::: zone-end

![Infografik med migreringsalternativen](../../_images/migrate/migration-options.png)
