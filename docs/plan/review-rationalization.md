---
title: Granska rationaliseringbeslut
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Granska rationaliseringbeslut
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: a5ccbe2f3dd754914997ccba7b49ba47505dffa3
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73564146"
---
# <a name="review-rationalization-decisions"></a>Granska rationaliseringbeslut

Under den inledande strategin och planerings fasen rekommenderar vi att du använder en [stegvis rationalisering](../digital-estate/rationalize.md#incremental-rationalization) Metod för den digitala egendomen. Men den här metoden bäddar in vissa antaganden i de resulterande besluten. Vi rekommenderar moln strategi teamet och moln implementerings teamen att granska dessa beslut med låg belastning på arbets belastnings dokumentationen. Den här granskningen är också en lämplig tid att engagera affärs intressenter och direktörens sponsor i beslut om framtida tillstånd.

> [!IMPORTANT]
> Ytterligare verifiering av rationalisering-beslut sker under utvärderings fasen av migreringen. Den här verifieringen fokuserar på affärs granskning av rationalisering för att justera resurserna på lämpligt sätt.

Om du vill validera rationalisering-beslut kan du använda följande frågor för att under lätta en konversation med verksamheten. Frågorna grupperas efter den sannolika rationalisering-justeringen.

## <a name="innovation-indicators"></a>Innovations indikatorer

Om den gemensamma granskningen av följande frågor resulterar i ett "Ja"-svar kan en arbets belastning vara en bättre kandidat för innovation. Sådan arbets belastning migreras inte via en hiss och Shift eller modernisera modell. I stället skapas affärs logiken eller data strukturerna igen som ett nytt eller rekonstruktions program. Den här metoden kan vara mer arbets krävande och tids krävande. Men för en arbets belastning som representerar betydande affärs avkastning är investeringen berättigad.

- Skapar du en marknads differentiering i programmen i den här arbets belastningen?
- Finns det en föreslagen eller godkänd investering som syftar till att förbättra upplevelsen som är associerade med program i den här arbets belastningen?
- Gör data i den här arbets belastningen nya produkt-eller tjänst erbjudanden tillgängliga?
- Finns det en föreslagen eller godkänd investering som syftar till att dra nytta av de data som är kopplade till den här arbets belastningen?
- Kan verkningarna av marknads differentieringen eller nya erbjudanden kvantifieras? I så fall, kommer den att göra en justering av den ökade kostnaden för innovation under antagandet av molnet?

Följande två frågor kan hjälpa dig att ta med tekniska scenarier på hög nivå i rationalisering-granskningen. Svar på "Ja" för att antingen kunna identifiera olika sätt att redovisa eller minska kostnaderna som är kopplade till innovation.

- Kommer data strukturerna eller affärs logiken att ändras under antagandet av molnet?
- Används en befintlig distributions pipeline för att distribuera den här arbets belastningen till produktion?

Om svaret på frågan är "Ja" bör teamet överväga att ta med den här arbets belastningen som en innovation-kandidat. Teamet bör minst flagga den här arbets belastningen för arkitektur granskning för att identifiera modernisering-möjligheter.

## <a name="migration-indicators"></a>Migrations indikatorer

Migrering är ett snabbare och billigare sätt att införa molnet. Men det går inte att dra nytta av möjligheter att förnya. Svara på följande frågor innan du investerar i innovation. De kan hjälpa dig att avgöra om en migrerings modell är mer tillämplig för en arbets belastning.

- Är käll koden som stöder det här programmet stabil? Förväntar du dig att den ska förbli stabil och oförändrad under tids ramen för den här versions cykeln?
- Stöder den här arbets belastningen produktions affärs processerna idag? Kommer det att göra det under hela den här versions cykeln?
- Är det en prioritet som den här moln implementerings ansträngningen förbättrar stabiliteten och prestandan för den här arbets belastningen?
- Är kostnads minskningen kopplad till arbets belastningen ett mål under den här ansträngningen?
- Minskar drifts komplexiteten för den här arbets belastningen under den här ansträngningen?
- Begränsas innovationen av den aktuella arkitekturen eller IT-processen?

Om svaret på någon av dessa frågor är "Ja" bör du överväga en migrerings modell för den här arbets belastningen. Den här rekommendationen gäller även om arbets belastningen är en kandidat för innovation.

Utmaningar i drifts komplexitet, kostnader, prestanda eller stabilitet kan hindra affärs returer. Du kan använda molnet för att snabbt skapa förbättringar som rör dessa utmaningar. Om det är tillämpligt rekommenderar vi att du använder metoden för migrering för att först stabilisera arbets belastningen. Sedan kan du utöka Innovations möjligheterna i den stabila och smidiga moln miljön. Den här metoden ger kortsiktiga returer och minskar den kostnad som krävs för att köra långsiktig ändring.

> [!IMPORTANT]
> I flyttnings modeller ingår stegvis modernisering. Användning av PaaS-arkitekturer (Platform as a Service) är en gemensam aspekt av migrerings aktiviteter. Det kan också finnas mindre konfigurations ändringar som använder dessa plattforms tjänster. Gräns för migrering definieras som en material ändring i affärs logiken eller stödjande verksamhets strukturer. Sådan förändring betraktas som en Innovations ansträngning.

## <a name="update-the-project-plan"></a>Uppdatera projekt planen

De kunskaper som krävs för migreringen av migrering skiljer sig från de kunskaper som krävs för en Innovations ansträngning. Vi rekommenderar att du tilldelar migrerings-och Innovations insatser till olika team under implementeringen av en moln implementerings plan. Varje team har sin egen upprepnings-, versions-och planerings cadences. Genom att tilldela separata team får du flexibiliteten att underhålla en moln implementerings plan samtidigt som du får en redovisning av innovationer och migrering.

När du hanterar moln implementerings planen i Azure DevOps, återspeglas hanteringen genom att ändra det överordnade arbetsobjektet (eller episka) från molnbaserad migrering till moln innovation. Den här diskreta ändringen bidrar till att se till att alla deltagare i moln implementerings planen snabbt kan spåra den nödvändiga ansträngningen och ändringar av reparations åtgärder. Den här spårningen hjälper också till att justera rätt tilldelningar till relevant moln antagande team.

För stora, komplexa implementerings planer med flera distinkta projekt bör du överväga att uppdatera upprepnings vägen. Om du ändrar sökväg till områden blir arbets belastningen bara synlig för det team som har tilldelats den sökvägen. Den här ändringen kan göra arbetet enklare för moln implementerings teamet genom att minska antalet synliga aktiviteter. Men det ökar komplexiteten för projekt hanterings processerna.

## <a name="next-steps"></a>Nästa steg

[Definiera iterationer och versioner](./iteration-paths.md) för att börja planera arbetet.

> [!div class="nextstepaction"]
> [Definiera iterationer och versioner](./iteration-paths.md) för att börja planera arbetet.
