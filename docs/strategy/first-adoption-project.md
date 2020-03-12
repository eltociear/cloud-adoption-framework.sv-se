---
title: Det första molnimplementeringsprojektet
description: Använd ramverket för moln införande för Azure för att lära dig processerna för moln införande och driften av arbets belastningar som finns i molnet.
author: BrianBlanchard
ms.author: brblanch
ms.date: 5/19/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 18b247665b8a371a9949ebaf838d3833a56067a3
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092489"
---
<!-- markdownlint-disable MD026 -->

# <a name="first-cloud-adoption-project"></a>Det första molnimplementeringsprojektet

Det finns en inlärnings kurva och ett tids åtagande som är kopplat till moln implementerings planeringen. Även för erfarna grupper tar det tid att planera tid: tid för att anpassa intressenter, tid för att samla in och analysera data, tid för att verifiera långsiktiga beslut och tid för att justera personer, processer och teknik. I de flesta effektiva implementerings ansträngningar ökar planeringen parallellt med införande, vilket förbättrar med varje version och med varje migrering till molnet. Det är viktigt att förstå skillnaden mellan en moln implementerings plan och en moln införande strategi. Du behöver en väldefinierad strategi för att under lätta och vägleda implementeringen av en moln implementerings plan.

Moln implementerings ramverket för Azure beskriver processerna för moln införande och driften av arbets belastningar som finns i molnet. Var och en av processerna i stegen definiera strategi, plan, redo, antagande och drift kräver små expansioner av teknik-, verksamhets-och drifts kunskaper. En del av dessa kunskaper kan komma från riktad utbildning. Men många av dem har faktiskt erhållits genom praktisk erfarenhet.

Att starta en första införande-process parallellt med utvecklingen av planen ger vissa fördelar:

- Upprätta en tillväxt tänkesätt för att uppmuntra inlärning och utforskning
- Ge teamet möjlighet att utveckla nödvändiga kunskaper
- Skapa situationer som främjar nya metoder för samarbete
- Identifiera kunskaps luckor och potentiella partnerskaps behov
- Tillhandahålla konkreta indata till planen

## <a name="first-project-criteria"></a>Första projekt kriterier

Ditt första införande projekt bör anpassas efter dina [motivation](./motivations.md) för moln införande. När det är möjligt bör det första projektet även Visa framsteg mot ett definierat [affärs resultat](./business-outcomes/business-outcome-template.md).

## <a name="first-project-expectations"></a>Första förväntningar för projektet

Ditt teams första antagande projekt kommer förmodligen att leda till en produktions distribution av något slag. Men det är inte alltid fallet. Fastställ rätt förväntningar tidigt. Här är några saker som du kan ställa in:

- Det här projektet är en källa för inlärning.
- Det här projektet kan resultera i produktions distributioner, men det kräver förmodligen ytterligare arbete först.
- Resultatet av det här projektet är en uppsättning tydliga krav för att tillhandahålla en längre produktions lösning.

## <a name="first-project-examples"></a>Första projekt exempel

Den här listan innehåller ett exempel på ett första projekt för varje motivations kategori för att stödja föregående villkor:

- **Kritiska affärs händelser:** När en viktig affärs händelse är den främsta motivation, kan implementeringen av ett verktyg som [Azure Site Recovery](../migrate/azure-migration-guide/migrate.md?tabs=Tools#azure-site-recovery) vara ett lämpligt första projekt. Under migreringen kan du använda det här verktyget för att snabbt migrera data Center till gångar. Men under det första projektet kan du använda det rent som ett haveri beredskaps verktyg för att minska beroendet av Disaster Recovery-tillgångar i data centret.

- **Motivation i migreringen:** När migrering är den främsta motivationen är det klokt att börja med migreringen av en icke-kritisk arbets belastning. [Installations guiden för Azure](../ready/azure-setup-guide/index.md) och [Azure migration guide](../migrate/azure-migration-guide/index.md) kan ge vägledning om migreringen av din första arbets belastning.

- **Nyskapande motivation:** När innovation är den främsta motivation kan skapandet av en riktad dev/test-miljö vara ett fantastiskt första projekt.

Ytterligare exempel på första antagande projekt är:

- **Verksamhets kontinuitet och haveri beredskap (BCDR):** Utöver Azure Site Recovery kan du implementera flera BCDR-strategier som ett första projekt.
- **Inproduktion:** Distribuera en inproduktion instans av en arbets belastning.
- **Arkiv:** Kall lagring kan belasta Data Center resurser. Att flytta data till molnet är en solid Quick Win.
- **Slut på support (EOS):** Att migrera till gångar som har nått slutet av support är en annan snabb chans som bygger tekniska kunskaper. Det kan också vara ett kostnads fritt sätt att undvika dyra support avtal eller licens kostnader.
- **VDI (Virtual Desktop Interface):** Att skapa virtuella skriv bord för fjärran slutna anställda kan ge en snabb chans. I vissa fall kan det här första tillämpnings projektet också minska beroendet av kostsamma privata nätverk för att ge en offentlig Internet anslutning.
- **Utveckling/testning:** Ta bort dev/test från lokala miljöer för att ge utvecklare kontroll, flexibilitet och självbetjänings kapacitet.
- **Enkla appar (mindre än fem):** Modernisera och migrera en enkel app för att snabbt få utvecklare och drifts upplevelser.
- **Prestanda labb:** När du behöver storskalig prestanda i en labb inställning använder du molnet för att snabbt och kostnads effektivt tillhandahålla dessa labb under en kort tid.
- **Data plattform:** Skapa en data Lake med skalbar beräkning för analys, rapportering eller Machine Learning-arbetsbelastningar och migrera till hanterade databaser med hjälp av dump/Restore-metoder eller data migrations tjänster.

## <a name="next-steps"></a>Nästa steg

När det första projektet för att införa moln har påbörjats kan moln strategi teamet förvandla sin uppmärksamhet till den långsiktiga [moln implementerings planen](../plan/index.md).

> [!div class="nextstepaction"]
> [Bygg din moln införande plan](../plan/index.md)
