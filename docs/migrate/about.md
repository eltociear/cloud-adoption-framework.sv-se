---
title: Molnmigrering
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introduktion till molnmigreringsinnehåll
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 1bf9497684c1043d23eec48b1ab5d5f1f12ef752
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70829961"
---
# <a name="cloud-migration-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Molnmigrering i Microsoft Cloud Adoption Framework för Azure

Molnmigrering är processen att flytta befintliga digitala tillgångar till en molnplattform. Med den här metoden replikeras befintliga tillgångar till molnet med minimala ändringar. När ett program eller en arbetsbelastning driftsätts i molnet, övergår användarna från den befintliga lösningen till molnlösningen. Molnmigrering är ett sätt att effektivt belastningsutjämna en molnportfölj. Det här är ofta den snabbaste och mest flexibla metoden på kort sikt. Däremot kan det hända att vissa fördelar med molnet inte kan utnyttjas med den här lösningen utan ytterligare framtida ändringar. Företag och medelstora kunder använder den här metoden för att påskynda ändringen, undvika planerade kapitalutgifter samt minska pågående driftskostnader.

## <a name="cloud-migration-guidance"></a>Vägledning till molnmigrering

Vägledningen i det här avsnittet av Cloud Adoption Framework är utformad för två syften:

- Erbjuda åtgärdsinriktade migreringsguider för händelser som kunderna ofta upplever. Varje guide innehåller den process och de verktyg som behövs för att lyckas vid en molnmigrering. Designvägledningen är av nödvändighet specifik för Azure. Alla andra rekommendationer i de här guiderna skulle kunna tillämpas som en del av en molnagnostisk eller flermolnsinriktad metod.
- Den hjälper läsarna att skapa personliga migreringsplaner som kan uppfylla en mängd olika affärsbehov, däribland migrering till flera offentliga moln. Till detta används en detaljerad vägledning för utvecklingen av processer, roller och ansvar, samt styrning av ändringshantering.

Det här innehållet är avsett att användas av teamet för molnimplementering. Det är även relevant för molnarkitekter som behöver utveckla en stark grund inom molnmigrering.

## <a name="intended-audience"></a>Målgrupp

Vägledningen i Cloud Adoption Framework berör verksamheten, tekniken och kulturen hos företag. Det här avsnittet riktar sig i synnerhet till programägare, ändringshanteringspersonal (till exempel projektkontor och ledning), ekonomi- och verksamhetschefer, samt teamet för molnimplementering. Det finns olika beroenden bland dessa profiler som kräver en förenkling av de molnarkitekter som använder vägledningen. Delaktigheten med dessa grupper kan vara ett engångsprojekt, men i vissa fall resulterar det i återkommande interaktioner med dessa andra profiler.

Molnarkitekten fungerar som strateg och ledare för att sammanföra dessa målgrupper. Innehållet i den här samlingen guider är utformad för att hjälpa molnarkitekten att stödja rätt konversation med rätt målgrupp för att främja de beslut som behövs. Affärsomvandling som drivs av molnet är beroende av molnarkitektrollen för att kunna fatta beslut för företaget och IT-verksamheten.

**Molnarkitektsspecialisering i det här avsnittet:** Avsnitt av Cloud Adoption Framework representerar olika specialiseringar eller varianter av molnarkitektsrollen. Det här avsnittet är utformat för molnarkitekter med ämnesexpertkunskaper om den befintliga lokala miljön och hur den påverkar migreringsalternativen.

**Ansvarsfördelning:** I många företag finns det en ansvarsfördelning som begränsar åtkomsten till produktionssystem eller segment i företagsmiljön. I dessa fall blir migreringsprocessen mer komplicerad. Ibland kan dessa roller och ansvarsområden kräva flera molnarkitekter för att kunna hantera hela migreringsprocessen.

**Partnerskapsalternativ** I var och en av de här processerna kommer teamen att lära sig nya färdigheter och metoder för det tekniska utförandet. Att förbättra de tekniska färdigheterna hos de befintliga teammedlemmarna är ett alternativ under körningen. Att anställa ytterligare personal är ett annat alternativ. Ett partnersamarbete med tredje part kan ofta ge en betydande acceleration och riskminskning. Med [partnerskapsalternativen](./migration-considerations/assess/partnership-options.md) kan du få hjälp att fatta beslut om hur du väljer det bästa partneralternativet.

## <a name="next-steps"></a>Nästa steg

För läsare som vill följa den här guiden från början till slut är det här innehållet en hjälp vid utvecklingen av en robust strategi för molnmigreringen. Vägledningen guidar läsaren genom teori och implementering av denna strategi.

Som ett första steg rekommenderar vi att läsarna använder [Azures migreringsguide](./azure-migration-guide/index.md) för att förstå den standarduppsättning av verktyg och metoder som behövs vid en normal migrering. Därefter kan den grundläggande vägledningen utökas för läsare som behöver [komplexa migreringsscenarier](./expanded-scope/index.md), [metodtips för migrering](./azure-best-practices/index.md) och [migreringsöverväganden](./migration-considerations/index.md).

> [!div class="nextstepaction"]
> [Guide för Azure-migrering](./azure-migration-guide/index.md)
