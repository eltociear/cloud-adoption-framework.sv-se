---
title: Vad är molnredovisning?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Förklaring av begreppet moln redovisning
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 62eea92ae85faa396cc36e062735ab2ed182b012
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/11/2019
ms.locfileid: "70905750"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-cloud-accounting"></a>Vad är molnredovisning?

Molnet ändrar hur IT-konton för kostnader, enligt beskrivningen i [skapa en finans modell för moln omvandling](financial-models.md). Olika modeller för IT-redovisning är mycket enklare att stödja på grund av hur molnet allokerar kostnader. Det är därför viktigt att förstå hur du ska ta hänsyn till moln kostnader innan du påbörjar en moln omvandlings resa. Den här artikeln beskriver de vanligaste moln redovisnings modellerna för IT.

## <a name="traditional-it-accounting-cost-center-model"></a>Traditionell IT-redovisning (modell för kostnads ställe)

Det är ofta viktigt att betrakta det som ett kostnads ställe. I den traditionella IT-redovisningen konsoliderar den inköps kraften för alla IT-tillgångar. Som vi påpekade i artikeln [finans modeller](financial-models.md) , kan inköps konsolideringen omfatta program varu licenser, återkommande avgifter för CRM-licensiering, köp av anställdas datorer och andra stora kostnader.

När det fungerar som ett kostnads ställe, visas det uppfattade värdet på det i stor utsträckning via ett hanterings objektiv. Den här uppfattningen gör det svårt för tavlan eller andra chefer att förstå det sanna värde som det tillhandahåller. Anskaffnings kostnaderna tenderar att skeva en vy av den genom att väga ytterligare ett mervärde av organisationen. I den här vyn förklaras varför den ofta är tilldelad i CHEFens eller COOs ansvars områden. Den här uppfattningen är begränsad och kan vara kort siktad.

## <a name="central-it-accounting-profit-center-model"></a>Central IT-redovisning (vinst Center modell)

Vissa CIO: er har valt en central IT-modell för redovisning för att lösa vyn kostnads ställe. I den här typen av modell behandlas den som en konkurrerande affär senhet och en peer för att producera affär senheter. I vissa fall kan den här modellen vara helt logisk. Vissa organisationer har till exempel en professionell IT-avdelning som genererar en intäkts ström. Ofta genererar centrala IT-modeller inte betydande intäkter, vilket gör det svårt att motivera modellen.

Oberoende av intäkts modellen är centrala IT-modeller unika på grund av hur IT-enhetens konton har för kostnader. I en traditionell IT-modell registrerar IT-teamet kostnader och betalar kostnaderna från delade medel som drift och underhåll (O & M) eller ett dedikerat vinst-och förlust konto (P & L).

I en central IT-källmodell, markerar IT-teamet de tjänster som tillhandahålls för att redovisa kostnader för till gång, hantering och andra beräknade kostnader. Sedan faktureras konkurrerande affär senheter för de markerade tjänsterna. I den här modellen förväntas informations chef att hantera de P & L som är kopplade till försäljningen av dessa tjänster. Detta kan skapa inflata IT-kostnader och konkurrens mellan centrala IT-och affär senheter, särskilt när det behövs för att minska kostnaderna eller inte uppfyller de överenskomna service avtal. När en teknik eller marknads förändring skulle uppstå skulle en ny teknik orsaka avbrott i Central IT s & L, vilket gör transformeringen svår.

## <a name="chargeback"></a>Återbetalning

Ett av de vanliga första stegen för att ändra dess rykte som ett kostnads ställe är att implementera en åter betalnings modell för redovisning. Den här modellen är särskilt vanlig i mindre företag eller mycket effektiva IT-organisationer. I åter betalnings modellen behandlas eventuella IT-kostnader som är associerade med en speciell affär senhet som en drifts kostnad i affär senhetens budget. Den här metoden minskar den ackumulerade kostnaden för den, vilket gör att affärs värden kan visas tydligare.

I en äldre lokal modell är åter betalning svår att realisera eftersom någon fortfarande måste bära stora kapital utgifter och avskrivning. Den pågående konverteringen från kapital utgifter till drifts kostnader som är förknippade med användningen är en svår redovisnings övning. Det här är en viktig anledning till att skapa den traditionella IT-modellen och den centrala IT-redovisningen. Modell för drifts kostnader i Cloud cost accounting är nästan nödvändigt om du vill kunna leverera en åter betalnings modell effektivt.

Men du bör inte implementera den här modellen utan att ta hänsyn till konsekvenserna. Här följer några konsekvenser som är unika för en åter betalnings modell:

- Återdebiteringen resulterar i en enorm minskning av den övergripande IT-budgeten. För IT-organisationer som inte är effektiva eller kräver omfattande komplexa tekniska kunskaper i drift eller underhåll, kan den här modellen exponera dessa utgifter på ett dåligt sätt.
- Att förlora kontrollen är en vanlig konsekvens. I mycket politiska miljöer kan Återdebiteringen leda till förlust av kontroll och personal som omallokeras till företaget. Detta kan skapa betydande ineffektivhet och minska dess förmåga att konsekvent uppfylla service avtal eller projekt krav.
- Svårt att redovisa delade tjänster är ett annat vanligt resultat. Om organisationen har vuxit genom förvärv och bär teknisk skuld på grund av detta är det troligt att en hög procent andel delade tjänster måste upprätthållas för att alla system ska fungera effektivt.

Moln transformationer innehåller lösningar på dessa och andra konsekvenser som är kopplade till en åter betalnings modell. Men var och en av dessa lösningar omfattar implementerings-och drifts kostnader. Informations chefen och ekonomi chefen bör noggrant väga in en åter betalnings modells och nack delar innan du överväger en.

## <a name="showback-or-awareness-back"></a>Showback eller medvetenhet – bak

För större företag är en showback eller en medvetenhet-back modell ett säkrare första steg i över gången från kostnads ställe till värde Center. Den här modellen påverkar inte finansiell redovisning. I själva verket ändras inte P & LS för varje organisation. Den största skiftet är i tänkesätt och medvetenhet. I en showback eller en medvetenhets backs modell hanterar den centraliserade, konsoliderade köp kraften som en agent för verksamheten. I rapporterar tillbaka till verksamheten, används alla direkta kostnader till den relevanta affär senheten, vilket minskar den uppskattade budgeten som används direkt av IT. DEN planerar också budgetar baserat på behoven hos de tillhör ande affär senheterna, vilket gör det lättare för kostnader som är kopplade till rent IT-initiativ bättre.

Den här modellen ger balans mellan en sann åter betalnings modell och mer traditionella modeller av IT-redovisning.

## <a name="impact-of-cloud-accounting-models"></a>Påverkan av modeller för moln redovisning

Valet av redovisnings modeller är avgörande i system design. Valet av redovisnings modell kan påverka prenumerations strategier, namngivnings standarder, tagga standarder och utformning av principer och skisser.

När du har arbetat med företaget för att fatta beslut om en moln redovisnings modell och [globala marknader](global-markets.md)har du tillräckligt med information för att [utveckla en Azure Foundation](../ready/index.md).

> [!div class="nextstepaction"]
> [Utveckla en Azure Foundation](../ready/index.md)
