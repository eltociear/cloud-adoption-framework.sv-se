---
title: 'Moln innovation: delta i program'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introduktion till utveckling av moln – delta i program
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 3db2349e3c1da7c80f3089ea187a3de72d006d1f
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683302"
---
# <a name="engage-through-applications"></a>Delta i program

Som beskrivs i artikeln om [democratizing data](./data.md)är data den nya oljan. IT-bränslen de flesta innovationer i den digitala ekonomin. För att bygga på den analoga funktionen är program den bränsle Station och infrastruktur som krävs för att få det här bränslet i rätt händer.

I vissa fall är det tillräckligt med data för att kunna ändra och möta kundernas behov. Oftare kräver lösningen av kund behov program för att forma data och skapa en upplevelse. Program är det sätt som vi använder för att engagera användaren. De är start sidan för de processer som krävs för att svara på kund utlösare. De är kunderna för att tillhandahålla vägledning om data och mottagning. Den här artikeln beskriver några principer som hjälper dig att justera rätt program lösning, baserat på Hypotheses som ska verifieras.

![Engagera via appar](../../_images/innovate/engage-via-apps.png)

## <a name="shared-code"></a>Delad kod

Team som kan reagera snabbare och på ett exakt sätt svara på kundfeedback, marknads förändringar och möjligheter att utveckla, kommer att leda sina respektive marknader i innovationen. Den första principen i innovativa program beskrivs i [Översikt över tillväxt tänkesätt](./learn.md#growth-mindset), "dela koden". Innovation över tid kan bara komma från ett kulturellt fokus. För att upprätthålla innovation krävs olika perspektiv och bidrag.

För att vara redo för innovation bör all program utveckling börja med en delad kod lagrings plats. Det vanligaste verktyget för att hantera kod databaser är [GitHub](https://guides.github.com/), vilket gör att du kan skapa en delad kod lagring med några få klick. Du kan också använda [Azure databaser](/azure/devops/repos/get-started/what-is-repos?view=azure-devops) -funktionen i Azure DevOps för att skapa en [git](/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git) -eller [Team Foundation](/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc) -lagringsplats.

## <a name="citizen-developers"></a>Medborgare-utvecklare

Professionella utvecklare är en viktig del av innovationen. När en hypotes bevisar sig korrekt i skala, krävs professionella utvecklare för att stabilisera och förbereda lösningen för skalning. De flesta principer som hänvisas till i den här artikeln kräver support från professionella utvecklare. De aktuella trenderna föreslår tyvärr att det finns fler öppnare för professionella utvecklare, och det finns utvecklare. Dessutom kan det vara mindre fördelaktigt att öka kostnaderna och arbets takten när det är nödvändigt med tuffa yrkes utveckling. Medborgare-utvecklare ger ett sätt att skala utvecklings insatser och påskynda tidigt hypotes testning.

Medborgarna kan vara en bra idé när tidiga Hypotheses kan verifieras med hjälp av verktyg som [PowerApps](https://docs.microsoft.com/powerapps/powerapps-overview) for app Interfaces, [AI Builder](/powerapps/use-ai-builder) för processer och förutsägelser, [Microsoft Flow](https://docs.microsoft.com/flow) för arbets flöden eller [Power BI](https://docs.microsoft.com/power-bi) för data bruk.

> [!NOTE]
> När du använder medborgarna för att testa Hypotheses, rekommenderar vi att professionella utvecklare tillhandahåller support, granskning och vägledning. När en hypotes har validerats i stor skalar en process för att överföra programmet till en stabilare programmerings modell, vilket påskyndar återställningarna i innovationen. Att involvera professionella utvecklare i tidiga process definitioner kan resultera i renare över gångar senare.

## <a name="intelligent-experiences"></a>Intelligenta upplevelser

Smarta upplevelser kombinerar hastigheten och skalningen av moderna webb program, med information om kognitiva tjänster och robotar. Var och en kan vara tillräckligt för att uppfylla kundernas behov. Kombinerat det spektrum av behov som kan uppfyllas med en digital upplevelse är expanderad, men utvecklings investeringar kan fortfarande finnas.

### <a name="modern-web-apps"></a>Moderna webb program

När ett program eller en miljö krävs för att uppfylla ett kund behov kan moderna webb program vara det snabbaste sättet att möta detta behov. Moderna webb upplevelser kan engagera interna eller externa kunder snabbt och möjliggöra snabb iteration av lösningen.

### <a name="infusing-intelligence"></a>Startgroparna intelligens

Maskin inlärning och artificiell intelligens blir allt mer tillgängligt för utvecklare. Den breda tillgängligheten för vanliga API: er med förutsägande funktioner, gör att utvecklare bättre kan uppfylla behoven hos kunden genom utökad åtkomst till data och förutsägelser.

Genom att lägga till intelligens i en lösning kan du aktivera tal till text, text översättning, visuellt innehåll och till och med visuell sökning. Med dessa utökade funktioner är det enklare för utvecklare att skapa lösningar som utnyttjar intelligens för att skapa en interaktiv och modern upplevelse.

### <a name="bots"></a>Robotar

Robotar ger en upplevelse som upplever mindre som att använda en dator och mer som att hantera en person eller minst en intelligent robot. De kan användas för att skifta enkla, repetitiva uppgifter, som att ta en middag eller samla in profil information, på automatiserade system som inte längre kräver direkt mänsklig inblandning. Användare är kopplade till en robot med hjälp av text, interaktiva kort och tal. En bot-interaktion kan vara en snabb fråga och ett avancerat samtal, och det kan vara en sofistikerad konversation som intelligent ger till gång till tjänster.

Robotar är mycket som moderna webb program, lever på Internet och använda API: er för att skicka och ta emot meddelanden. Vad som finns i en robot varierar mycket beroende på vilken typ av bot det är. Modern bot-programvara är beroende av en trave med teknik och verktyg för att leverera allt mer komplexa upplevelser på en mängd olika plattformar. En enkel robot kan dock bara ta emot ett meddelande och eko meddelandet tillbaka till användaren med mycket lite kod.

Robotar kan göra samma saker som andra typer av program vara kan göra-läsa och skriva filer, använda databaser och API: er och utföra vanliga beräknings uppgifter. Det som gör robotar unikt är användningen av mekanismer som är allmänt reserverade för kommunikation från människa till människa.

## <a name="cloud-native-solutions"></a>Moln – inbyggda lösningar

Inbyggda moln program byggs från grunden. Inbyggda moln program är optimerade för moln skalning och prestanda. Molnbaserade program skapas vanligt vis med hjälp av mikrotjänster, Server lös, händelsebaserade eller containerbaserade metoder. De flesta vanliga moln lösningar utnyttjar en kombination av mikrotjänsters arkitekturer, hanterade tjänster och kontinuerlig leverans för att uppnå tillförlitlighet och snabbare tid till marknaden.

En molnbaserad lösning gör det möjligt för centraliserade utvecklings grupper att upprätthålla kontrollen över affärs logiken, utan att behöva monolitisk centraliserade lösningar. Den här typen av lösning skapar också ett ankare för att öka konsekvensen mellan medborgarna och moderna upplevelser. Dessutom ger Cloud-inhemska lösningar en innovation Accelerator genom att frigöra medborgarna och professionella utvecklare att utveckla säkert och med minimala Blocker.

## <a name="innovate-through-existing-solutions"></a>Förnya genom befintliga lösningar

Många kund Hypotheses kan bäst levereras med en modern version av en befintlig lösning. När den aktuella affärs logiken uppfyller kundernas behov (eller verkligen kommer nära) kan du påskynda innovationen genom att bygga vidare på en modern lösning.

De flesta former av modernisering, inklusive lätt omstrukturering av programmet, ingår i metoderna för [migrering](../../migrate/index.md) i moln införande ramverket. Metoden vägleder moln implementerings team genom processerna för att migrera en [digital egendom](../../digital-estate/index.md) till molnet. [Azure migration guide](../../migrate/azure-migration-guide/index.md) är ett effektiviserat tillvägagångs sätt för samma metod, vilket är lämpligt för ett litet antal arbets belastningar eller till och med ett enda program.

När du har migrerat och förvarat finns det en mängd olika sätt att använda lösningen för att skapa nya innovativa lösningar för kund behov. Till exempel kan [medborgare-utvecklare](#citizen-developers) testa Hypotheses eller professionella utvecklare kan skapa [intelligenta upplevelser](#intelligent-experiences) eller [molnbaserade lösningar](#cloud-native-solutions).

### <a name="extend-an-existing-solution"></a>Utöka en befintlig lösning

Att utöka en lösning är en vanlig form av modernisering. Detta kan vara den snabbaste vägen till innovation när följande är sant för kunden hypotes:

- Befintlig affärs logik bör uppfylla (eller kommer nära möte) som befintliga kund behov.
- En förbättrad upplevelse skulle bättre möta behoven hos en specifik kunds kohort.
- Affärs logiken som krävs av MVP-lösningen har centraliserats, vanligt vis via en design för [N-nivå](/azure/architecture/guide/architecture-styles/n-tier), webb tjänster, API eller [mikrotjänster](/azure/architecture/guide/architecture-styles/microservices) . Den här metoden består av att omsluta den befintliga lösningen med en ny upplevelse som finns i molnet. I Azure skulle den här lösningen troligen leva i Azure App Services.

### <a name="rebuild-an-existing-solution"></a>Återskapa en befintlig lösning

Om ett program inte kan utökas enkelt kan du behöva återföra lösningen. I den här metoden migreras arbets belastningen till molnet. När den har migrerats ändras eller dupliceras delar av programmet, som webb tjänster eller [mikrotjänster](/azure/architecture/guide/architecture-styles/microservices), som distribueras parallellt med den befintliga lösningen. Den parallella service-baserade lösningen kan behandlas som en utökad lösning. Den här lösningen skulle helt enkelt figursätta den befintliga lösningen med en ny upplevelse som finns i molnet. I Azure skulle den här lösningen troligen leva i Azure App Services.

> [!CAUTION]
> Omstrukturering eller omkonstruktion av lösningar eller Central affärs logik kan snabbt bli en tids krävande [teknisk insamling](./build.md#reduce-complexity-and-delay-technical-spikes), i stället för en källa till kund värde. Detta är en risk för innovation, särskilt tidigt i hypotes validering. Med en kreativitet i utformningen av en lösning bör det finnas en sökväg till MVP som inte kräver omfabrik av befintliga lösningar. Det är klokt att skjuta upp omstrukturering tills den första hypotesen kan val IDE ras i stor skala.

## <a name="operating-model-innovations"></a>Innovationer om drifts modeller

Förutom modern innovation som är till för att skapa appar har det varit nyheter om apparnas användning. Metoderna har gjort många organisations rörelser. En av de mest framträdande är en rörelse mot [moln Center med](../../organize/cloud-center-of-excellence.md) hög prestanda för drift modeller. När företaget är fullt bemannat och mogna har affärs teamen möjlighet att tillhandahålla sitt eget operativa stöd för en lösning.

Typen av självbetjänings modell för drifts hantering, som finns i ett moln Center med hög kvalitet, ger bättre kontroller och snabbare upprepningar i lösnings miljön. Detta åstadkommer du genom att överföra drifts kontroll och ansvar till affärs teamet.

När målet är att skala eller uppfylla global efter frågan för en befintlig lösning, kan den här metoden räcka för att validera en kund hypotes. När du har migrerat och något som är nyställt skulle affärs teamet kunna skala lösningar för att testa en rad Hypotheses avseende kund kohorter som är intresserade av prestanda, global distribution eller andra kund behov. verksamhetshanteraren.

## <a name="reduce-overhead-and-management"></a>Minska omkostnader och hantering

Det är bara att underhålla i en lösning, desto längre tid kommer lösningen att iterera. Påskynda innovation genom att minska påverkan på tillgänglig hastighet.

För att förbereda för många iterationer som krävs för att leverera en innovativ lösning är det viktigt att tänka på. Minimera drifts bördan tidigt i processen genom att prioritera Server alternativ.

I Azure kan program utan Server alternativ innehålla [Azure App Service](https://docs.microsoft.com/azure/app-service/overview) eller [behållare](https://docs.microsoft.com/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-rearchitect-container-sql).

I parallellt tillhandahåller Azure Data alternativ utan server, vilket också minskar kostnaderna. [Listan med databas produkter](https://docs.microsoft.com/azure/#pivot=products&panel=databases) innehåller alternativ för att vara värd för data, utan att det krävs någon fullständig data plattform.

## <a name="next-steps"></a>Nästa steg

Beroende på hypotes och lösning kan principerna i den här artikeln hjälpa dig att utforma appar som uppfyller MVP-definitioner och engagera användare. Härnäst är principerna för att [fatta antagande](./ci-cd.md), som diskuterar olika sätt att snabbt få fram program och data till kundernas händer snabbare.

> [!div class="nextstepaction"]
> [Förbättra införandet](./ci-cd.md)
