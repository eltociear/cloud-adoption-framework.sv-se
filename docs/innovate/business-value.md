---
title: Bygg enighet om affärs värdet för moln innovation
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig att bygga enighet om affärs värdet för utveckling av molnet.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 643da95396a4983c2642fabcf21340264d0cd1c9
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683346"
---
# <a name="building-consensus-on-the-business-value-of-innovation"></a>Skapa enighet om affärs värdet för innovation

Det första steget för att utveckla nya innovationer är att identifiera hur innovationen ska driva affärs värde. Den här övningen ställer en rad frågor som framhäver vikten av att investera mer tid för att definiera affärs värde.

## <a name="qualifying-questions"></a>Kvalificerande frågor

Innan du utvecklar någon lösning (i molnet eller lokalt) ska du validera dina affärs värde kriterier:

1. Vilka definierade kund behov har vi sökt för att åtgärda den här lösningen?
2. Vilka möjligheter skulle den här lösningen skapa för verksamheten?
3. Vilka affärs resultat skulle uppnås med den här lösningen?
4. Vilken av företagets motivation skulle betjänas med den här lösningen?

Om svaren på alla fyra frågorna är väl dokumenterade kanske du inte behöver resten av den här övningen. Som tur är kan den här dokumentationen enkelt testas. Om du vill testa både dokumentationen och din allmänna justering, ska du vara värd för ett kort möte med engagerande affärs intressenter och ett separat kort möte med teamet med engagerad utveckling. I båda mötena ställer du de fyra frågorna ovan och jämför resultaten.

> [!NOTE]
> Den befintliga dokumentationen **bör inte** delas med någon av teamen före mötet. Om den här justeringen är sann, ska GUID-Hypotheses refereras till (eller förbättras ännu) av medlemmar i varje grupp.

> [!WARNING]
> Under lätta mötet. Detta är ett justerings test, inte en anpassnings övning. När du startar mötet, se till att deltagarna är medvetna om målet att testa riktad justering med befintliga avtal i teamet. Upprätta en tids gräns. Genomför fem minuter per fråga och ange en timer för var och en. Stäng frågan på fem minuter, även om svaret inte har överenskommits på.

Om svaren är riktnings beroende av varandra, men representerar olika språk och intressen i varje grupp, kan du fundera på att använda en Victory. Du är redo att fortsätta med utveckling av lösningen.

Om ett eller två av svaren är riktnings rätt justerade, känner du igen att ditt hårda arbete är inställt. Du är redan bättre justerad än de flesta organisationer. Framtida framgångar är mycket troligt, med mindre fortsatta investeringar i justeringen. Granska följande avsnitt för idéer som kan hjälpa dig att bygga ytterligare anpassningar.

Om något av teamen inte kan svara på alla fyra frågor på trettio minuter, så kan det vara en stor inverkan på den här ansträngningen och andra åtgärder. Tänk noga noga med följande avsnitt.

## <a name="address-the-big-picture-first"></a>Adressera den stora bilden först

Ramverket för moln införande följer en före skriven sökväg genom strategi, plan, redo och att anta. Moln innovation passar i den här processens antagande fas. När svaren på frågorna 3 och 4 ovan (resultat och motivation) inte justeras, betyder det att något missades under strategi fasen för moln införande livs cykel. Flera av följande scenarier är förmodligen i spel.

- **Justerings möjlighet:** Om affärs intressenter inte kan komma överens om motivation och affärs resultat som är relaterade till en moln Innovations ansträngning, är det ett symtom på en större utmaning. Övningarna i [moln strategi fasen](../strategy/index.md) kan vara användbara när du utvecklar anpassningar mellan affärs intressenter. Dessutom rekommenderar vi starkt att samma intressenter utgör ett [moln strategi team](../organize/cloud-strategy.md) som uppfyller regelbundet.

- **Kommunikations möjlighet:** När utvecklings teamet inte kan komma överens om motivation och affärs resultat, kan det vara ett symtom på strategiska kommunikations luckor. Att granska moln strategin med moln implementerings teamet kan snabbt lösa den här blockeringen. I flera veckor efter granskningen bör laget upprepa kvalificerings frågorna.

- **Prioriterings möjlighet:** En moln strategi är i grunden en hypotes på företags nivå. De bästa moln strategierna är öppna för iteration och feedback. Om båda teamen förstår strategin men ändå inte kan justera svaren på dessa frågor, kan prioriteringarna vara feljusterade. En session med moln implementerings teamet och moln strategi teamet kan hjälpa dig med båda gruppernas ansträngningar. Under den här sessionen delar moln antagande teamet sina justerade svar på de stora bild frågorna. Därifrån kan en konversation mellan moln implementerings teamet och moln strategi teamet Markera möjligheter att bättre justera prioriteringar.

Dessa stora bild möjligheter visar ofta sätt att bättre justera den här lösningen med moln strategin. Den här övningen har två vanliga resultat:

- Dessa konversationer kan leda till förbättringar i moln strategin och bättre åter givning av det viktiga kund behovet. En sådan ändring kan resultera i högre exekutiv support för teamet.
- I motsatta fall kan den här konversationen Visa att investeringar i en annan lösning passar bättre för moln implementerings teamet. I detta fall bör du överväga att migrera lösningen innan du fortsätter att investera i innovation. Alternativt kan det tyda på att en unionsmedborgare krävs för att testa affärs värdet först. I båda fallen kommer det att hjälpa teamet att undvika en stor investering med begränsade affärs returer.

## <a name="address-solution-alignment"></a>Justering av adress lösning

Det är ganska vanligt att svaren på frågorna 1 och 2 (kund behov och affärs möjlighet) blir feljusterade. Detta är särskilt vanligt under tidiga faser av idéstadie och utveckling. Att hitta en balans mellan för mycket och för lite definition är utmanande för många utvecklings grupper. I ramverket för moln införande är resurs snåla metoder som bygge-mått – lär dig om feedback-slingor som det bästa sättet att besvara dessa frågor. I följande lista visas möjligheter och metoder för att skapa justering.

- **Hypotes möjlighet:** Det är vanligt att flera intressenter och utvecklings grupper har för många förväntningar för en lösning. När detta inträffar är det ett tecken på att hypotesen är för vagt. Följ rikt linjerna för att [bygga med kund empati](./considerations/build.md) för att skapa en tydligare hypotes.
- **Build-möjlighet:** När teamen är feljusterade på grund av att de inte stämmer överens med hur kunden behöver lösas, betyder det vanligt vis att teamet [försenas av en för tidig teknisk insamling](./considerations/build.md#reduce-complexity-and-delay-technical-spikes). För att hålla teamet fokuserat på kunden kan du starta den första iterationen och bygga en liten MVP för att adressera en del av hypotesen. Mer information om hur du kan flytta teamet framåt finns i [utveckla digitala uppfinningar](./considerations/invention.md).
- **Utbildnings möjligheter:** När något av teamen är feljusterat eftersom de behöver djupgående tekniska krav och omfattande funktionella krav, visar det en möjlighet att träna i smidiga metoder. När team kulturen inte är redo för smidiga processer kan det vara svårt att utveckla och hålla jämna steg på marknaden. Utbildnings resurser om DevOps och smidiga metoder finns i:
  - [Utveckla dina DevOps-metoder](https://docs.microsoft.com/learn/paths/evolve-your-devops-practices)
  - [Bygg program med Azure DevOps](https://docs.microsoft.com/learn/paths/build-applications-with-azure-devops)
  - [Distribuera program med Azure DevOps](https://docs.microsoft.com/learn/paths/deploy-applications-with-azure-devops/)

Genom att använda den här metoden och efter släpning för hanterings verktygen i varje avsnitt som anges ovan kan du skapa lösnings justering.

## <a name="next-steps"></a>Nästa steg

När affärs värdes relationen är väl justerad och kommunicerad är det dags att börja skapa din lösning. Gå tillbaka till den innovativa [övningen](./index.md) för att få vägledning om nästa steg.

> [!div class="nextstepaction"]
> [Gå tillbaka till Innovations övningarna för nästa steg](./index.md)
