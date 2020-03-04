---
title: Introduktion till guiden för Azure-migrering
description: Lär dig att effektivt migrera din organisations tjänster till Azure med stegvis vägledning.
author: matticusau
ms.author: mlavery
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 4d2bb420609bb703a1f32b0912eb9c17ccabe4e9
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78225513"
---
# <a name="azure-migration-guide-before-you-start"></a>Azure-migreringsguiden: Innan du börjar

[Metoden för Cloud Adoption Framework-migrering](../index.md) vägleder läsare genom en iterativ process för migrering av en arbetsbelastning eller en liten samling arbetsbelastningar per utgåva. I varje iteration följs processen för att bedöma, migrera, optimera och flytta upp för att se till att arbetsbelastningarna är redo för att uppfylla produktionskraven. Den molnoberoende processen kan vägleda migreringen till alla molnleverantörer.

Den här guiden visar en förenklad version av processen när du migrerar från din lokala miljö till **Azure**.

::: zone target="docs"

> [!TIP]
> Visa den här guiden i Azure-portalen om du vill ha en interaktiv upplevelse. Gå till [Azure Quickstart Center](https://portal.azure.com/?feature.quickstart=true#blade/Microsoft_Azure_Resources/QuickstartCenterBlade) i Microsoft Azure-portalen, välj **Migrera din miljö till Azure** och följ instruktionerna.

::: zone-end

## <a name="migration-tools"></a>[Migreringsverktyg](#tab/MigrationTools)

Den här guiden är den rekommenderade metoden för din första migrering till Azure, eftersom den introducerar dig till metodiken och de molnbaserade verktyg som vanligtvis används vid migrering till Azure. Verktygen presenteras på följande sidor:

> [!div class="checklist"]
>
> - **Utvärdera varje arbetsbelastnings tekniska anpassning.** Kontrollera teknisk beredskap och lämplighet för migrering.
> - **Migrera dina tjänster.** Utför den faktiska migreringen genom att replikera lokala resurser till Azure.
> - **Hantera kostnader och fakturering.** Förstå de verktyg som krävs för att kontrollera kostnaderna i Azure.
> - **Optimera och flytta upp.** Optimera för kostnads- och prestandabalans innan du flyttar upp din arbetsbelastning till produktion.
> - **Få hjälp.** Få hjälp och stöd under migreringen eller aktiviteter efter migrering.

Det förutsätts att en landningszon redan har distribuerats, i enlighet med de bästa metoderna i [Cloud Adoption Framework-beredskapsmetoden](../../ready/index.md).

## <a name="when-to-use-this-guide"></a>[När du bör använda den här guiden](#tab/WhenToUseThisGuide)

Även om de verktyg som beskrivs i den här guiden stöder en mängd olika migreringsscenarier fokuserar den här guiden på projekt med begränsat omfång och _minimal komplexitet_. Avgör huruvida den här migreringsguiden är lämpligt för ditt projekt genom att se om följande villkor gäller för din situation:

- Arbetsbelastningarna för den första migreringen är inte verksamhetskritiska och innehåller inte känsliga data.
- Du migrerar en homogen miljö.
- Endast ett fåtal affärsenheter behöva inriktas för att slutföra migreringen.
- Du planerar att inte automatisera hela migreringen.
- Du migrerar ett litet antal servrar.
- Beroendemappningen för de komponenter som ska migreras är enkel att definiera.
- Din bransch har minimala regelkrav som är relevanta för den här migreringen.

Om något av dessa villkor inte gäller för din situation bör du i stället överväga [guiden för utökat omfång](../expanded-scope/index.md). Vi rekommenderar även att du begär hjälp från något av våra Microsoft-team eller partner för att genomföra migreringar som kräver guiden för utökat omfång. Kunder som tar hjälp av Microsoft eller certifierade partner lyckas bättre i dessa scenarier. Mer information om hur du begär hjälp finns i den här guiden.

<!-- markdownlint-enable MD033 -->

::: zone target="docs"

Mer information finns i:

- [Guiden för utökat omfång](../expanded-scope/index.md)

::: zone-end
