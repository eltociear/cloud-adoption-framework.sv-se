---
title: Delta via appar för digital uppfinning
description: Lär dig hur du skapar app-lösningar för att forma data och skapa upplevelser som engagerar kunder och stöder innovation.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 85939b1932f7eaf5f40b43bb54e75aa30e53d941
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433399"
---
# <a name="engage-through-applications"></a>Delta i program

Data är den nya oljan som beskrivs i [demokratisera identifieringen av data](./data.md). IT-bränslen de flesta innovationer i den digitala ekonomin. För att bygga på den analoga funktionen, är program de bränsle stationer och den infrastruktur som krävs för att få dessa bränslen till höger.

I vissa fall räcker endast data för att ändra och möta kundernas behov. Oftare kräver lösningar på kund behov program för att forma data och skapa en upplevelse. Program är det sätt som vi använder för att engagera användaren. De är start sidan för de processer som krävs för att svara på kund utlösare. De är kunder som tillhandahåller vägledning om data och mottagning. Den här artikeln sammanfattar flera principer som kan hjälpa dig att justera dig med rätt program lösning, baserat på Hypotheses som ska verifieras.

![Engagera via appar](../../_images/innovate/engage-via-apps.png)

## <a name="shared-code"></a>Delad kod

Team som snabbt och noggrant svarar på kundfeedback, marknads förändringar och möjligheter att utveckla vanligt vis leder till sina respektive marknader i innovation. Den första principen i innovativa program summeras i [Översikt över tillväxten tänkesätt](./learn.md#growth-mindset): "dela koden". Med tiden uppstår innovation från ett kulturellt fokus. För att upprätthålla innovation krävs olika perspektiv och bidrag.

För att vara redo för innovation bör all program utveckling börja med en delad kod lagrings plats. Det mest antagna verktyget för att hantera kod databaser är [GitHub](https://guides.github.com), vilket gör att du snabbt kan skapa en delad kod lagrings plats. [Azure databaser](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops) är också en uppsättning versions kontroll verktyg i Azure DevOps-tjänster som du kan använda för att hantera din kod. Azure databaser erbjuder två typer av versions kontroll:

- [Git](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git): distribuerad versions kontroll
- [Team Foundation versions kontroll (TFVC)](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc): centraliserad versions kontroll

## <a name="citizen-developers"></a>Medborgarutvecklare

Professionella utvecklare är en viktig del av innovationen. När en hypotes bevisar sig korrekt i skala, krävs professionella utvecklare för att stabilisera och förbereda lösningen för skalning. De flesta principer som hänvisas till i den här artikeln kräver support från professionella utvecklare. De nuvarande trenderna föreslår tyvärr att det finns en större efter frågan för professionella utvecklare än utvecklare. Dessutom kan det vara mindre fördelaktigt att den här innovationen är tillräcklig när en professionell utveckling bedöms vara nödvändig. Som svar på de här utmaningarna ger medborgarna av medborgarna ett sätt att skala utvecklings insatser och påskynda tidigt hypotes testning.

Användningen av medborgarna kan vara livskraftig och effektiv när tidig Hypotheses kan val IDE ras via verktyg som [PowerApps](https://docs.microsoft.com/powerapps/powerapps-overview) for app Interfaces, [AI Builder](https://docs.microsoft.com/powerapps/use-ai-builder) för processer och förutsägelser, [Microsoft Flow](https://docs.microsoft.com/flow) för arbets flöden och [Power BI](https://docs.microsoft.com/power-bi) för data förbrukning.

> [!NOTE]
> När du använder medborgare-utvecklare för att testa Hypotheses, är det tillrådligt att ha några professionella utvecklare som vill ha support, granskning och vägledning. När en hypotes har validerats i skala kommer en process för att överföra programmet till en mer robust programmerings modell att påskynda återställningen av innovationen. Genom att involvera professionella utvecklare i process definitionerna tidigt på, kan du inse renare över gångar senare.

## <a name="intelligent-experiences"></a>Intelligenta upplevelser

Smarta upplevelser kombinerar hastigheten och skalningen av moderna webb program med information om kognitiva tjänster och robotar. Var och en av dessa tekniker kan vara tillräckligt för att uppfylla kundernas behov. När de har kombinerats med varandra, utvidgas spektrumet av behov som kan uppfyllas med en digital upplevelse, samtidigt som utvecklings kostnaderna.

### <a name="modern-web-apps"></a>Moderna webbappar

När ett program eller en miljö krävs för att uppfylla ett kund behov kan moderna webb program vara det snabbaste sättet att gå till. Moderna webb upplevelser kan engagera interna eller externa kunder snabbt och möjliggöra snabb iteration av lösningen.

### <a name="infusing-intelligence"></a>Berika med intelligens

Maskin inlärning och artificiell intelligens är allt tillgängligt för utvecklare. Med förutsägbara funktioner får utvecklare bättre till gång till en bred spridning av vanliga API: er med förutsägelse funktioner för att bättre uppfylla behoven hos kunden genom utökad åtkomst till data och förutsägelser.

Genom att lägga till intelligens i en lösning kan du aktivera tal till text, text översättning, visuellt innehåll och till och med visuell sökning. Med dessa utökade funktioner är det enklare för utvecklare att skapa lösningar som utnyttjar intelligens för att skapa en interaktiv och modern upplevelse.

### <a name="bots"></a>Robotar

Robotar ger en upplevelse som upplever mindre som att använda en dator och mer som att hantera en person, minst med en intelligent robot. De kan användas för att skifta enkla, repetitiva uppgifter (till exempel att göra en middags bokning eller samla in profil information) till automatiserade system som kanske inte längre kräver direkt mänsklig inblandning. Användare är inversa till en robot via text, interaktiva kort och tal. En bot-interaktion kan variera från en snabb fråga och svara på en sofistikerad konversation som intelligent ger till gång till tjänster.

Robotar är mycket som moderna webb program: de bor på Internet och använder API: er för att skicka och ta emot meddelanden. Vad som finns i en robot varierar mycket beroende på vilken typ av bot det är. Modern bot-programvara är beroende av en trave med teknik och verktyg för att leverera allt mer komplexa upplevelser på olika plattformar. En enkel robot kan dock bara ta emot ett meddelande och eko meddelandet tillbaka till användaren med mycket lite kod.

Robotar kan göra samma saker som andra typer av program vara: läsa och skriva filer, använda databaser och API: er och hantera vanliga beräknings aktiviteter. Det som gör robotar unikt är användningen av mekanismer som är allmänt reserverade för kommunikation från människa till människa.

## <a name="cloud-native-solutions"></a>Moln – inbyggda lösningar

Molnbaserade program byggs från grunden och de är optimerade för moln skalning och prestanda. Molnbaserade program skapas vanligt vis med hjälp av mikrotjänster, Server lös, händelsebaserade eller containerbaserade metoder. Oftast använder Cloud-inhemska lösningar en kombination av mikrotjänsters arkitekturer, hanterade tjänster och kontinuerlig leverans för att uppnå tillförlitlighet och snabbare tid till marknaden.

En molnbaserad lösning gör det möjligt för centraliserade utvecklings grupper att upprätthålla kontrollen över affärs logiken utan att behöva monolitisk, centraliserade lösningar. Den här typen av lösning skapar också en fäst punkt för att öka konsekvensen för inblandning av medborgarna och moderna upplevelser. Dessutom ger Cloud-inhemska lösningar en innovation Accelerator genom att frigöra medborgarna och professionella utvecklare att utveckla säkert och med minsta möjliga Blocker.

## <a name="innovate-through-existing-solutions"></a>Förnya genom befintliga lösningar

Många kund Hypotheses kan bäst levereras med en modern version av en befintlig lösning. När den aktuella affärs logiken uppfyller kundernas behov (eller verkligen kommer nära) kan du påskynda innovationen genom att bygga vidare på en modern lösning.

De flesta former av modernisering, inklusive lätt omstrukturering av programmet, ingår i metoderna för [migrering](../../migrate/index.md) i moln införande ramverket. Metodiken vägleder moln implementerings team genom processen att migrera en [digital fastighet](../../digital-estate/index.md) till molnet. [Azure migration guide](../../migrate/azure-migration-guide/index.md) är ett effektiviserat tillvägagångs sätt för samma metod, vilket är lämpligt för ett litet antal arbets belastningar eller till och med ett enda program.

När en lösning har migrerats och förberetts finns det en mängd olika sätt att skapa nya, innovativa lösningar för kundernas behov. Till exempel kan [medborgarna](#citizen-developers) i Hypotheses testa, eller professionella utvecklare kan skapa [intelligenta upplevelser](#intelligent-experiences) eller [molnbaserade lösningar](#cloud-native-solutions).

### <a name="extend-an-existing-solution"></a>Utöka en befintlig lösning

Att utöka en lösning är en vanlig form av modernisering. Detta kan vara den snabbaste vägen till innovation när följande är sant för kunden hypotes:

- Befintlig affärs logik bör uppfylla (eller kommer nära möte) som befintliga kund behov.
- En förbättrad upplevelse skulle bättre möta behoven hos en specifik kunds kohort.
- Affärs logiken som krävs av den minsta lönsamma produkt lösningen (MVP) har centraliserats, vanligt vis via en design på [N-nivå](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier), webb tjänster, API eller [mikrotjänster](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/microservices) . Den här metoden består av att omsluta den befintliga lösningen inom en ny upplevelse som finns i molnet. I Azure skulle den här lösningen troligen leva i Azure App Services.

### <a name="rebuild-an-existing-solution"></a>Återskapa en befintlig lösning

Om ett program inte kan utökas enkelt kan du behöva återföra lösningen. I den här metoden migreras arbets belastningen till molnet. När programmet har migrerats ändras eller dupliceras delar av det, som webb tjänster eller [mikrotjänster](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/microservices), som distribueras parallellt med den befintliga lösningen. Den parallella service-baserade lösningen kan behandlas som en utökad lösning. Den här lösningen skulle helt enkelt figursätta den befintliga lösningen med en ny upplevelse som finns i molnet. I Azure skulle den här lösningen troligen leva i Azure App Services.

> [!CAUTION]
> Omstrukturering eller omkonstruktion av lösningar eller Central affärs logik kan snabbt utlösa en tids krävande [teknisk insamling](./build.md#reduce-complexity-and-delay-technical-spikes)i stället för en källa till kund värde. Detta är en risk för innovation, särskilt tidigt i hypotes validering. Med en kreativitet i utformningen av en lösning bör det finnas en sökväg till MVP som inte kräver omfabrik av befintliga lösningar. Det är klokt att skjuta upp omstrukturering tills den första hypotesen kan val IDE ras i stor skala.

## <a name="operating-model-innovations"></a>Innovationer om drifts modeller

Förutom moderna, innovativa metoder för att skapa appar, har det funnits viktiga innovationer i app- *åtgärder*. Dessa metoder har gjort många organisations rörelser. En av de mest framträdande är [moln Center för](../../organize/cloud-center-of-excellence.md) den bästa drifts modellen. När företaget är fullt bemannat och mogna har affärs teamen möjlighet att tillhandahålla sitt eget operativa stöd för en lösning.

Typen av självbetjänings drifts hanterings modell som finns i ett moln Center med hög kvalitet gör det möjligt för bättre kontroller och snabbare iterationer i lösnings miljön. Dessa mål uppnås genom att du överför drifts kontroll och ansvar till affärs teamet.

Om du försöker skala eller möta global efter frågan för en befintlig lösning, kan den här metoden räcka för att validera en kund hypotes. När en lösning har migrerats och blivit något förmodern kan affärs teamet skala den för att testa en rad Hypotheses. Dessa omfattar vanligt vis kund kohorter som är intresserade av prestanda, global distribution och andra kund behov som har hindrats av IT-driften.

## <a name="reduce-overhead-and-management"></a>Minska omkostnader och hantering

Det är bara att underhålla i en lösning, desto längre tid kommer lösningen att iterera. Det innebär att du kan påskynda innovationen genom att minska effekten av åtgärder på den tillgängliga bandbredden.

För att förbereda för många iterationer som krävs för att leverera en innovativ lösning är det viktigt att tänka på. Minimera till exempel drift belastningar tidigt i processen genom att prioritera Server alternativ. I Azure kan program utan Server alternativ innehålla [Azure App Service](https://docs.microsoft.com/azure/app-service/overview) eller [behållare](https://docs.microsoft.com/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-rearchitect-container-sql).

I parallellt tillhandahåller Azure Data alternativ utan server, vilket också minskar kostnaderna. I [Azures produkt katalog](https://docs.microsoft.com/azure) finns databas alternativ som är värdar för data utan behov av en fullständig data plattform.

## <a name="next-steps"></a>Nästa steg

Beroende på hypotes och lösning kan principerna i den här artikeln hjälpa dig att utforma appar som uppfyller MVP-definitioner och engagera användare. Härnäst följer principerna för att [fatta beslut](./ci-cd.md), vilket ger dig möjlighet att snabbt och effektivt hämta program och data till kundernas händer.

> [!div class="nextstepaction"]
> [Förbättra införandet](./ci-cd.md)
