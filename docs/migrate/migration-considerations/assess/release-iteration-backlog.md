---
title: Upprepnings- och publiceringseftersläpning
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Skapa en upprepnings- och publiceringseftersläpning
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: d2dddb4893a2781da38969949972fa516e32b46c
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025406"
---
# <a name="manage-change-in-an-incremental-migration-effort"></a>Hantera ändringar i en stegvis migreringsåtgärd

I den här artikeln förutsätter vi att migreringsprocesserna är stegvisa till sin natur och körs parallellt [med styrningsprocessen](../../../govern/index.md). Samma riktlinjer kan dock användas för att fylla i inledande uppgifter i en uppdelad arbetsstruktur för traditionella vattenfallsmetoder för ändringshantering.

## <a name="release-backlog"></a>Versionseftersläpning

En *versionseftersläpning* består av en serie tillgångar (virtuella datorer, databaser, filer och program, bland annat) som måste migreras innan en arbetsbelastning kan frisläppas för produktionsanvändning i molnet. Under varje upprepning dokumenterar och uppskattar implementeringsteamet för molnet de åtgärder som krävs för att flytta varje tillgång till molnet. Se avsnittet "upprepningseftersläpning" som följer.

## <a name="iteration-backlog"></a>Upprepningseftersläpning

En *upprepningseftersläpning* är en lista över det detaljerade arbete som krävs för att migrera ett bestämt antal tillgångar från den befintliga digitala egendomen till molnet. Posterna i den här listan lagras ofta i form av arbetsobjekt i ett flexibelt hanteringsverktyg, till exempel Azure DevOps.

Innan du startar den första upprepningen anger implementeringsteamet för molnet en varaktighet för upprepningen, normalt mellan två och fyra veckor. Tidsramen är viktig för att kunna skapa en start- och slutperiod för varje uppsättning genomförda aktiviteter. Med konsekventa körningsfönster blir det enkelt att mäta hastigheten (migreringstakten) och anpassningen till föränderliga affärsbehov.

Före varje upprepning granskar teamet versionseftersläpningen och estimerar insatsen och prioriteringarna för de tillgångar som ska migreras. Därefter åtar man sig att leverera ett specifikt antal överenskomna migreringar. När implementeringsteamet för molnet har beslutat om detta blir listan över aktiviteter *den aktuella upprepningseftersläpningen*.

Under varje upprepning arbetar gruppmedlemmarna som ett självorganiserande team för att uppfylla åtaganden i den aktuella upprepningseftersläpningen.

## <a name="next-steps"></a>Nästa steg

När en upprepningseftersläpning har definierats och godkänts av implementeringsteamet för molnet kan [godkännanden för ändringshantering](./approve.md) slutföras.

> [!div class="nextstepaction"]
> [Godkänna arkitekturändringar inför migrering](./approve.md)
