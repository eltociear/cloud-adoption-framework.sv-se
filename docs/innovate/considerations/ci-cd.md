---
title: 'Utveckling av molnet: öka implementeringen'
description: Introduktion till utveckling av molnet – ge ett förstärknings beslut
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: a3c726443e62140dba997ae4a1ff89593f72e6e6
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808523"
---
# <a name="empower-adoption"></a>Underlätta implementeringen

Det ultimata testet av innovation är att kunden reagera på din uppfinning. Skulle hypotesen visa sig vara sann? Använder kunderna lösningen? Skalar den för att uppfylla behoven för den önskade procent andelen av användarna? Viktigast av detta ska de fortsätta att komma tillbaka? Ingen av dessa frågor kan tillfrågas förrän den lägsta produkt-och MVP-lösningen har distribuerats. I den här artikeln ska vi fokusera på disciplinen för att fatta beslut.

## <a name="reduce-friction-that-affects-adoption"></a>Minska friktion som påverkar införande

Det finns några viktiga friktions punkter att införa som kan minimeras genom en kombination av teknik och processer. För läsare med kunskaper om kontinuerlig integrering (CI) och kontinuerlig distribution (CD) eller DevOps-processer är följande bekant. I den här artikeln upprättas en utgångs punkt för moln implementerings team som arbetar med utveckling och feedback av bränslen. I framtiden kan den här start punkten gynna mer robusta CI/CD-eller DevOps-metoder som de produkter och team som är mogna.

Som det beskrivs i [mått för kund påverkan](./measure.md), kräver positiv verifiering av alla hypotes upprepning och bestämning. Du får mycket fler avbrott än WINS under en Innovations cykel. Detta är normalt. Men när en kund behöver, hypotes och lösning justeras i skala, ändras världen snabbt. Den här artikeln syftar till att minimera [tekniska toppar](./build.md#reduce-complexity-and-delay-technical-spikes) som saktar ned innovation, men som ändå ser till att du behåller några rena bästa metoder. På så sätt blir det lättare för IT-utformningen att leverera på aktuella kund behov.

## <a name="empowering-adoption-the-maturity-model"></a>Besluts förstärkning: förfallo modell

Det främsta målet med [förnyelse metoden](./index.md) är att bygga upp kund partnerskap och påskynda feedback-slingor, vilket leder till marknads innovationer. I följande bild och avsnitt beskrivs de första implementeringar som har stöd för den här metoden.

![Förbättra införandet: förfallo modellen](../../_images/innovate/empower-adoption-maturity.png)

- [Delad lösning](#shared-solution): upprätta en central lagrings plats för alla aspekter av lösningen.
- [Feedback-slingor](#feedback-loops): se till att feedback-slingor kan hanteras på ett konsekvent sätt via iterationer.
- [Kontinuerlig integrering](#continuous-integration): Bygg och konsolidera regelbundet lösningen.
- [Tillförlitlig testning](#reliable-testing): validera lösnings kvalitet och förväntade ändringar för att säkerställa att dina test mått är tillförlitliga.
- [Lösnings distribution](#solution-deployment): distribuera lösningar så att teamet snabbt kan dela ändringar med kunderna.
- [Integrerad mätning](#integrated-measurements): Lägg till inlärnings mått i feedback-slingan för att ta bort en fullständig analys av hela teamet.

För att minimera tekniska toppar antar vi att förfallo tiden inlednings vis är låg för var och en av dessa principer. Men den dagliga planeringen fortsätter genom att justera till verktyg och processer som kan skalas när Hypotheses blir mer detaljerad. I Azure ger [GitHub](https://guides.github.com) och [Azure DevOps](https://docs.microsoft.com/azure/devops) små team att komma igång med lite friktion. Dessa team kan växa för att inkludera tusentals utvecklare som samarbetar kring skalnings lösningar och testar hundratals kund Hypotheses. Resten av den här artikeln visar plan Big/start-metoden för att göra det möjligt att fatta beslut över var och en av dessa principer.

## <a name="shared-solution"></a>Delad lösning

Som det beskrivs i [mått för kund påverkan](./measure.md), kräver positiv verifiering av alla hypotes upprepning och bestämning. Du får mycket fler avbrott än WINS under en Innovations cykel. Detta är normalt. Men när en kund behöver, hypotes och lösning justeras i skala, ändras världen snabbt.

När du skalar innovation finns det inget värdefullt verktyg än en delad kodbas för lösningen. Tyvärr finns det inget tillförlitligt sätt att förutsäga vilken iteration eller vilken MVP som ger den vinnande kombinationen. Därför är det aldrig för tidigt att upprätta en delad kodbas eller lagrings plats. Detta är den [tekniska insamling](./build.md#reduce-complexity-and-delay-technical-spikes) som aldrig ska förskjutas. När teamet itererar genom olika MVP-lösningar möjliggör en delad lagrings platsen enkel samarbete och snabbare utveckling. När du gör ändringar i lösningen och drar nedåt inlärnings mått kan du återställa till en tidigare, mer effektiv version av lösningen.

Det vanligaste verktyget för att hantera kod databaser är [GitHub](https://guides.github.com), vilket gör att du kan skapa en delad kod lagring med bara några få klick. Dessutom kan [Azure databaser](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops) -funktionen i Azure DevOps användas för att skapa en [git](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git) -eller [Team Foundation](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc) -lagringsplats.

## <a name="feedback-loops"></a>Feedbackslingor

Att göra kund delen av lösningen är nyckeln till att skapa kund samarbeten under Innovations cykler. Detta sker delvis genom att [mäta kund påverkan](./measure.md). Den kräver konversationer och direkt testning med kunden. Båda genererar feedback som måste hanteras effektivt.

Varje återkopplings punkt är en potentiell lösning på kund behovet. Mer viktigt är att varje bit av direkt kundfeedback representerar en möjlighet att förbättra samarbetet. Om feedback gör det till en MVP-lösning, kommer du att fira med kunden. Även om vissa synpunkter inte är åtgärds bara, är det helt enkelt att bli transparent med beslutet att bli av med att göra en [växande tänkesätt](./learn.md#growth-mindset) och fokusera på [kontinuerlig inlärning](./learn.md#continuous-learning).

[Azure DevOps](https://docs.microsoft.com/azure/devops) innehåller metoder för att [begära, tillhandahålla och hantera feedback](https://docs.microsoft.com/azure/devops/project/feedback). Vart och ett av dessa verktyg centraliserar feedback så att teamet kan vidta åtgärder och tillhandahålla uppföljning av en genomskinlig feedback-slinga.

## <a name="continuous-integration"></a>Kontinuerlig integrering

Eftersom antaganden skalas och en hypotes är närmare den sanna innovationen i stor skala, är antalet mindre Hypotheses som testas att växa snabbt. För riktiga feedback-slingor och smidiga implementerings processer är det viktigt att var och en av dessa Hypotheses är integrerad och att du har stöd för den främsta hypotesen bakom innovationen. Det innebär att du också måste gå snabbt till att förnya och växa, vilket kräver flera utvecklare för att testa variationer i Core hypotesen. För senare utveckling av steg kan du behöva flera team av utvecklare, varje byggnad mot en delad lösning. Kontinuerlig integrering är det första steget mot hantering av alla rörliga delar.

I kontinuerlig integrering slås kod ändringar ofta samman i huvud grenen. Automatiserade bygg-och test processer se till att koden i huvud grenen alltid är produktions kvalitet. Detta säkerställer att utvecklare arbetar tillsammans för att utveckla delade lösningar som ger korrekta och tillförlitliga feedback-slingor.

Azure-DevOps och [Azure-pipeliner](https://docs.microsoft.com/azure/devops/pipelines) ger kontinuerlig integrering med bara några få klick i GitHub eller flera andra lagrings platser.
Läs mer om [kontinuerlig integrering](https://docs.microsoft.com/azure/devops/learn/what-is-continuous-integration)eller mer information finns i [praktiska labb övningar](https://www.azuredevopslabs.com/labs/azuredevops/continuousintegration). Det finns även lösnings arkitekturer för att påskynda skapandet av dina [CI/CD-pipeliner via Azure DevOps](https://azure.microsoft.com/solutions/devops).

## <a name="reliable-testing"></a>Tillförlitlig testning

Fel i alla lösningar kan skapa falska positiva eller falska negativa negativa tal. Oväntade fel kan lätt leda till fel tolkning av användar mått. De kan också generera negativa synpunkter från kunder som inte korrekt representerar testet av din hypotes.

Vid tidiga iterationer av en MVP-lösning förväntas defekter. tidiga antaganden kanske till och med tycker att de är kära. I tidiga versioner är test av godkännanden vanligt vis icke. En aspekt av att skapa med empati avser dock valideringen av behovet och hypotesen. Båda kan slutföras genom enhets tester på en kod nivå och manuella acceptans test före distributionen. Tillsammans ger dessa en viss tillförlitlighet för testning. Du bör sträva efter att automatisera en väldefinierad serie med build-, enhets-och acceptans test. Dessa säkerställer pålitliga mått som är relaterade till mer detaljerade anpassningar till hypotesen och den resulterande lösningen.

Funktionen [Azure-testplaner](https://docs.microsoft.com/azure/devops/test/track-test-status?view=azure-devops) innehåller verktyg för att utveckla och driva test planer under manuell eller automatiserad test körning.

## <a name="solution-deployment"></a>Lösningsdistribution

Det kanske är den mest meningsfulla aspekten av att ge dig möjlighet att styra lanseringen av en lösning till kunder. Genom att tillhandahålla en självbetjänings-eller automatiserad pipeline för att släppa ut en lösning till kunder kan du påskynda feedback-slingan. Genom att göra det möjligt för kunder att snabbt interagera med ändringar i lösningen kan du bjuda in dem till processen. Den här metoden utlöser också snabbare tester av Hypotheses, vilket minskar antaganden och eventuell möjlighet att arbeta.

Det finns flera metoder för distribution av lösningar. Följande motsvarar de tre vanligaste:

- **Kontinuerlig distribution** är den mest avancerade metoden, eftersom den automatiskt distribuerar kod ändringar till produktion. För vuxen team som testar mogna Hypotheses kan kontinuerlig distribution vara mycket värdefull.
- Vid tidiga utvecklings faser kan **kontinuerlig leverans** vara mer lämpligt. I kontinuerlig leverans distribueras alla kod ändringar automatiskt till en produktions miljö. Utvecklare, företags besluts fattare och andra i teamet kan använda den här miljön för att kontrol lera att deras arbete är produktions klart. Du kan också använda den här metoden för att testa en hypotes med kunder utan att påverka pågående affärs aktiviteter.
- **Manuell distribution** är den minst avancerade metoden för versions hantering. Som namnet antyder distribuerar någon i teamet manuellt de senaste kod ändringarna. Den här metoden är fel känsligt, otillförlitligt och betraktas som ett antimönster av de mest erfarna teknikerna.

Under den första iterationen av en MVP-lösning är manuell distribution vanligt, trots föregående utvärdering. När lösningen är mycket flytande och kundfeedback är okänd, finns det en betydande risk för att återställa hela lösningen (eller till och med Core hypotesen). Här är den allmänna regeln för manuell distribution: inget kund bevis, ingen distributions automatisering.

Att investera tidigt kan leda till förlorad tid. Det kan vara viktigt att skapa beroenden på den versions pipeline som gör teamet mer motstånds kraftiga mot en tidig Pivot Pivot. Efter de första iterationerna eller när kunden feedback föreslår potentiell framgång, bör en mer avancerad distributions modell snabbt antas.

I alla stadier av hypotes validering ger Azure-DevOps och [Azure-pipeliner](https://docs.microsoft.com/azure/devops/pipelines) kontinuerlig leverans och kontinuerliga distributions möjligheter. Läs mer om [kontinuerlig leverans](https://docs.microsoft.com/azure/devops/learn/what-is-continuous-delivery)eller ta en titt på [praktiska labb övningar](https://www.azuredevopslabs.com/labs/azuredevops/continuousdeployment). Lösnings arkitekturen kan också påskynda skapandet av dina [CI/CD-pipeliner via Azure DevOps](https://azure.microsoft.com/solutions/devops).

## <a name="integrated-measurements"></a>Integrerade mätningar

När du [mäter kund påverkan](./measure.md)är det viktigt att förstå hur kunderna reagerar på ändringar i lösningen. Dessa data, som kallas *telemetri*, ger insikter om vilka åtgärder en användare (eller kohort av användare) vidtog när de arbetade med lösningen. Från dessa data är det enkelt att få en kvantitativ validering av hypotesen. Dessa mått kan sedan användas för att justera lösningen och generera mer detaljerade Hypotheses. De här diskreta ändringarna bidrar mogna till den första lösningen i efterföljande iterationer, vilket i slut ändan upprepas i stor skala.

I Azure tillhandahåller [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) verktyg och gränssnitt för att samla in och granska data från kund upplevelser. Du kan använda dessa observationer och insikter för att förfina efter släpning med hjälp av [Azure-kort](https://docs.microsoft.com/azure/devops/boards).

## <a name="next-steps"></a>Nästa steg

När du har fått en förståelse för de verktyg och processer som krävs för att göra det, är det dags att undersöka en mer avancerad Innovations disciplin: [interagera med enheter](./devices.md). Den här disciplinen kan hjälpa till att minska barriärerna mellan fysiska och digitala upplevelser, vilket gör lösningen ännu enklare att införa.

> [!div class="nextstepaction"]
> [Interagera med enheter](./devices.md)
