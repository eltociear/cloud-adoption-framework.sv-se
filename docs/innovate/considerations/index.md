---
title: Innovation i den digitala ekonomin
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig mer om teorin kring molninnovation i Cloud Adoption Framework
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 2417241e2dc607b005f32c9c647cc88913167148
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72556589"
---
# <a name="innovation-in-the-digital-economy"></a>Innovation i den digitala ekonomin

Den digitala ekonomin är en allt viktigare faktor i nästan alla branscher. Under den tidigare industriella revolutionen var bensin, transportband och mänsklig uppfinningsrikedom viktiga för att driva innovationen på marknaden. Produkternas kvalitet, pris och logistik bidrog till att utveckla marknaden när företagen försökte leverera bättre produkter till kunderna snabbare. Den digitala ekonomin förändrar hur kunderna interagerar med företagen. Det har lett till att sätten att differentiera sig på marknaden också har ändrats. I den digitala ekonomin är kunderna mindre intresserade av logistiken och mer av helhetsupplevelsen kring att använda en produkt. Det här skiftet beror på att vi interagerar direkt med tekniken i våra dagliga liv och att värdet i de här interaktionerna börjar realiseras.

I innovationsfasen i Cloud Adoption Framework ligger fokus på att förstå kundernas behov och att snabbt skapa innovationer som formar hur kunderna interagerar med dina produkter. Vi kommer att illustrera en metod för att tillvarata värdet hos en MVP (minimal livskraftig produkt). Vi kommer också att mappa vanliga beslut i innovationscykeln så att du får bättre förståelse för hur molnet kan frigöra innovation och skapa relationer till dina kunder.

## <a name="innovate-methodology"></a>Metoder kring innovation

I den här bilden illustreras den enkla innovationsmetoden i Cloud Adoption Framework. I efterföljande artiklar i det här avsnittet kommer vi gå igenom hur du etablerar grundläggande processer, metoder och mekanismer för att identifiera och driva innovationen på företaget.

![Diagram över innovationsmetoden i Cloud Adoption Framework](../../_images/innovate/innovate-methodology.png)

I den här artikelserien bygger vi vidare på den här metoden på två sätt:

- Börja alltid med kundens implementering och skapa feedbackslingor som bygger upp kundrelationen via slingan ”skapa-mät-lär dig”.
- Sedan kan du undersöka olika metoder att utveckla de digitala innovationer som sätter implementeringen i fokus.

I följande avsnitt går vi igenom innovationsmetoden och vilka åtaganden som krävs för att lyckas med den här metoden.

## <a name="formula-for-innovation"></a>Formel för innovation

Lyckad innovation handlar inte om någon stor, omvälvande händelse eller något magiskt under. Framgång inom innovation är mer av ett balansnummer, vilket vi kan visa med en enkel ekvation: **Innovation = uppfinning + implementering**.

Innovationen sker i skärningspunkten mellan uppfinning och införande. Den verkliga innovationen är resultatet av att långsamt justera den mänskliga upplevelsen med hjälp av nya metoder, processer och ny teknik. I den här formeln handlar uppfinningar om att skapa en ny lösning som uppfyller en kunds behov. Implementeringen handlar om att börja använda den nya lösningen så att det mänskliga beteendet och interaktionen formas. Det krävs flera iterationer, datadrivna beslut, konstant inlärning och utvecklingsfokus för att hitta rätt balans mellan uppfinning och implementering. Dessutom krävs det teknik som kan hålla jämna steg med de obegränsade möjligheterna till att lära sig nya saker i dagens digitala samhälle.

Molnet är ofta en bra plattform för uppfinningar, eller de tekniska aspekterna av innovationen. Tyvärr faller de flesta bra idéerna på den svåra implementeringen snarare än på idéstadiet. Om processen ska lyckas måste utvecklingsteamet alltid börja med en implementering som test för innovationen. Det är därför som den här metoden börjar med implementering. För att kunna använda den här metoden måste teamet komma överens om följande tre åtaganden:

- [Åtagande att prioritera kunden över tekniken](#commitment-to-prioritize-customers-over-technology)
- [Åtagande om transparens](#commitment-to-transparency)
- [Åtagande för en iterativ process](#commitment-to-iteration)

## <a name="cultural-commitments"></a>Kulturella åtaganden

För att använda [innovationsmetoden](../index.md) krävs några kulturella åtaganden så att måtten som beskrivs i artikeln ska kunna användas effektivt. Innan ni byter metod för att effektivisera innovationen måste implementeringsteamet och ledningen vara redo att göra dessa viktiga åtaganden.

## <a name="commitment-to-prioritize-customers-over-technology"></a>Åtagande att prioritera kunden över tekniken

Varje utvecklingsteam har en uppsättning verktyg eller tekniker som de är vana vid. Det är en bra idé att använda den här styrkan och det ni redan kan. Om innovationen ska lyckas måste teamen dock också ha fokus på kundens behov och den hypotes som testas. Ibland kanske de inte passar så bra ihop med ett visst verktyg eller en viss arkitektur. För att lyckas med innovationen måste utvecklingsteamet ha ett öppet sinne. Under uppfinningsfasen måste de tekniska besluten baseras på kundens behov snarare än teamets preferenser.

## <a name="commitment-to-transparency"></a>Åtagande om transparens

För att förstå hur en innovationsmetod kan mätas är det viktigt att först förstå åtagandet om transparens. Innovationen kan bara blomstra i en miljö med **utvecklingsfokus**. Utvecklingsfokus handlar om att kulturen är inriktad på att lära sig av alla erfarenheter. En lyckad innovation och kontinuerlig inlärning börjar med ett åtagande om transparens kring måtten. Det krävs ett modigt molnimplementeringsteam för att göra det här åtagandet. Åtagandet är dock meningslöst om det inte matchas av ett åtagande att bevara transparensen även i ledningsgruppen och molnstrategiteamet.

Transparens är viktigt eftersom mätningen av hur kunden påverkas inte handlar om rätt eller fel. Mätningarna handlar inte heller om arbetets kvalitet eller hur implementeringsteamet har presterat. De representerar snarare än möjlighet till utveckling och att bättre kunna uppfylla kundernas behov. Om innovationsmåtten missbrukas kommer den här kulturen snabbt att dö ut. I slutänden leder det till att måtten manipuleras, vilket i sin tur leder till att uppfinningen misslyckas samt att personalen och ledningen som manipulerat måtten gör ett sämre jobb. Chefer och personal bör undvika att använda mått annat än som möjligheter att lära sig och att förbättra MVP-lösningen.

## <a name="commitment-to-iteration"></a>Åtagande för en iterativ process

Det finns egentligen bara en enda grundsanning för samtliga innovationscykler &mdash; det blir inte rätt på första försöket. Mått kan hjälpa er att förstå vilka justeringar som måste göras för att ni ska nå önskade resultat. Ändringar som leder till önskade resultat baseras på iterationer av processen ”skapa-mät-lär dig”. Molnimplementeringsteamet och molnstrategiteamet måste åta sig att använda ett iterativt arbetssätt redan innan utvecklingsfokus eller ”skapa-mät-lär dig” kan ha någon effekt.

## <a name="next-steps"></a>Nästa steg

Innan du skapar nästa fantastiska uppfinning ska du påbörja kundens implementering genom att lära dig mer om [feedbackslingan ”skapa-mät-lär dig”](./adoption.md).

> [!div class="nextstepaction"]
> [Kundimplementering med feedbackslingan ”skapa-mät-lär dig”](./adoption.md)
