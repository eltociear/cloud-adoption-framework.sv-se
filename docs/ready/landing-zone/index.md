---
title: Vad är en landningszon
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig hur en landningszon fungerar som den grundläggande byggstenen i alla typer av miljöer för molnimplementering.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 6db16b50115f2ba145dd4980dc5d57867f438de7
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78228367"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-a-landing-zone"></a>Vad är en landningszon?

Infrastruktur som kod är en naturlig övergång under de flesta molnimplementeringsåtgärder. Distribution av dina första landningszoner i molnet är en vanlig startpunkt för att gå över till skapandet av en kodbaserad miljö. I den här artikeln får du hjälp att förstå termen _landningszon_ och andra relaterade villkor.

## <a name="landing-zone-definition"></a>Definition av landningszon

En landningszon är den grundläggande byggstenen i alla typer av miljöer för molnimplementering. Termen _landningszon_ refererar till en logisk konstruktion som fångar allt som måste vara sant för att den önskade molnimplementeringen ska kunna användas.

**Omfång:** En fullt fungerande landningszon tar hänsyn till alla plattformsresurser som krävs för att stödja kundens implementeringsbehov.

**Refaktorisering:** En fullt fungerande landningszon är den sista slutprodukten för alla iterationer av Cloud Adoption Framework-beredskapsmetoden. Under varje iteration kommer den kodbas som definierar landningszonen att omstruktureras eller expanderas. Efter omstrukturering kan landningszonen ändras eller omdistribueras för att möjliggöra nya behov för molnimplementering.

**Mål:** Målet med landningszonmetoden är att skapa en gemensam uppsättning konsekventa plattformsimplementeringar. De konsekventa implementeringarna måste finnas för att dina program ska få åtkomst till nödvändiga komponenter när de distribueras. Varje landningszoniteration måste därför utformas och distribueras i enlighet med kraven i molnimplementeringsplanen och strategin för prenumerationens design.

**Principsyfte:** Principsyftet med landningszonen är att se till att när ett program hamnar i Azure ska den obligatoriska ”grunderna” redan finnas på plats.

## <a name="landing-zone-usage"></a>Användning av landningszon

Landningszoner skiljer nödvändigtvis mellan IaaS- eller PaaS-antagande. Landningszoner är dock utformade för att stödja implementeringsplanen genom att uppfylla prenumerationsstrategin. Att stödja implementeringsplanen kan kräva flera landningszoner med en blandning av nödvändiga komponenter.

Syftet med och omfattningen av den övergripande implementeringsplanen för molnet definierar vad ”grunderna” kräver. Ytterligare hanteringskrav för styrning, efterlevnad, säkerhet och drift kommer sannolikt att läggas till i det inledande landningszonomfånget. Under tidiga steg i antagandet kan landningszoner omfatta mindre ”grunder” som ett resultat av definierade krav och acceptabla risker.  När det finns flera landningszoner är det mycket vanligt att varje landningszon är beroende av hubbar som tillhandahåller de nödvändiga kontrollerna via en delad tjänstmodell.

## <a name="related-terms"></a>Relaterade villkor

- **Delade tjänster:** Arbetsbelastningar har ofta delade beroenden som används av många olika arbetsbelastningar. Metoden för delade tjänster flyttar många av dessa vanliga beroenden till en logisk konstruktion.

- **Modell av typen hub-spoke:** Implementeringen av metoden för delade tjänster är av modellen hub-spoke. I den här modellen är hubben en enda logisk konstruktion för att vara värd för alla delade tjänster. Landningszoner fungerar sedan som ekrar som strålar ut från hubben, baserat på vanliga beroenden.

- **Oberoende landningszon:** Vissa sätt att initiera zoner behöver inte särskilt anropa en dedikerad hubb. Detta visas vanligtvis när alla produktionstillgångar (appar, data och virtuella datorer) i molnimplementeringsplanen kan värdbaseras, hanteras och regleras på ett säkert sätt i en enda miljö.

## <a name="next-steps"></a>Nästa steg

Om du vill börja använda landningszoner [väljer du den första landningszonen](./first-landing-zone.md).

> [!div class="nextstepaction"]
> [Välj din första landningszon](./first-landing-zone.md)
