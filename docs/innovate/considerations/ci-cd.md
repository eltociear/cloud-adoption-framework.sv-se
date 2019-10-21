---
title: 'Utveckling av molnet: öka implementeringen'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introduktion till utveckling av molnet – ge ett förstärknings beslut
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/24/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 727686b70c7fb604274f74da7a043f589f79fa4c
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557224"
---
# <a name="empower-adoption"></a>Förbättra införandet

Det ultimata testet av innovation är att kunden reagera på din uppfinning. Skulle hypotesen visa sig vara sann? Använder kunderna lösningen? Skalar den för att uppfylla behoven för den önskade procent andelen av användarna? Viktigast av detta ska de fortsätta att komma tillbaka? Ingen av dessa frågor kan tillfrågas förrän MVP-lösningen har distribuerats. I den här artikeln fokuserar vi på disciplinen för att fatta beslut.

## <a name="reducing-friction-to-adoption"></a>Minska friktionen för att anta

Det finns några viktiga friktions punkter att införa som kan minimeras genom en kombination av teknik och processer. För läsare som är bekanta med CI/CD-eller DevOps-processer verkar följande vara mycket likt. Fokus för den här artikeln är att upprätta en utgångs punkt för moln implementerings team, som kommer att få nya slingor för utveckling och feedback av bränsle. Längre tid kan den här start punkten växa till robusta CI/CD-eller DevOps-metoder som de produkter och team som är mogna.

En beskrivning av hur man [mäter kund påverkan](./measure.md)kräver positiv verifiering av hypotesen iteration och bestämning. Du får fler fler avbrott än WINS under en Innovations cykel. Detta är normalt. Men när kund behovet, hypotesen och lösningen justeras i skala, ändras världen snabbt. Den här artikeln syftar till att minimera [teknisk insamling](./build.md#reduce-complexity-and-delay-technical-spikes) som skulle göra innovationen långsammare, men se till att det finns några heltäckande bästa metoder. På så sätt blir det lättare för dig att få till gång till framtida framgångar, men du kan leverera på aktuella kund behov.

## <a name="empowering-adoption---maturity-model"></a>Förstärkning av implementerings förfallo modell

Det främsta målet med [förnyelse metoden](./index.md) är att bygga upp kund partnerskap och påskynda feedback-slingor, vilket leder till marknads innovationer.
Följande bild och avsnitt i innehållet beskriver de första implementeringar som har stöd för metoden.

![Öka modell för införande-förfall](../../_images/innovate/empower-adoption-maturity.png)

- [Delad lösning](#shared-solution): upprätta en central lagrings plats för alla aspekter av lösningen.
- [Feedback-slingor](#feedback-loops): se till att feedback-slingor kan hanteras konsekvent via iterationer.
- [Kontinuerlig integrering](#continuous-integration): Bygg och konsolidera regelbundet lösningen.
- [Tillförlitlig testning](#reliable-testing): validera lösnings kvalitet och förväntade ändringar av enheten för att säkerställa åtgärder.
- [Lösnings distribution](#solution-deployment): distribution av en lösning som gör det möjligt för teamet att snabbt dela ändringar med kunder.
- [Integrerad mätning](#integrated-measurements): Lägg till inlärnings mått i feedback-slingan för att ta bort en fullständig analys av hela teamet.

För minimerade tekniska toppar är förfallo dagen inlednings vis låg för var och en av dessa principer. Men planera framåt genom att justera till verktyg och processer som kan skalas när Hypotheses blir mer detaljerade. I Azure ger kombinationen av [GitHub](https://guides.github.com) och [Azure DevOps](https://docs.microsoft.com/azure/devops) små team att komma igång med lite friktion. Utöka sedan till tusentals utvecklare att samar beta kring skalnings lösningar som testar hundratals Hypotheses. Resten av den här artikeln illustrerar planen stor, en liten metod för att göra det möjligt att fatta beslut över var och en av dessa principer.

## <a name="shared-solution"></a>Delad lösning

En beskrivning av hur man [mäter kund påverkan](./measure.md)kräver positiv verifiering av hypotesen iteration och bestämning. Du får fler fler avbrott än WINS under en Innovations cykel. Detta är normalt. Men när kund behovet, hypotesen och lösningen justeras i skala, ändras världen snabbt.

När du skalar innovationer finns det inget värdefullt verktyg än en delad kodbas för lösningen. Sadly, det finns inget sätt att förutsäga vilken iteration eller vilken MVP som ger den vinnande kombinationen. Därför är det aldrig för tidigt att upprätta en delad kodbas eller lagrings plats. Detta är den [tekniska insamling](./build.md#reduce-complexity-and-delay-technical-spikes) som aldrig ska förskjutas. När teamet upprepas genom olika MVP-lösningar kan en delad lagrings platsen vara enkel att samar beta och påskyndad utveckling. När ändringar i lösningen resulterar i en negativ inverkan på inlärnings mått, kan versions kontroll tillåta en återställning till den tidigare, mer effektiva versionen av lösningen.

Det vanligaste verktyget för att hantera kod databaser är [GitHub](https://guides.github.com) som gör det möjligt att skapa en delad kod lagring med några få klick. Dessutom kan [Azure databaser](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops) -funktionen i Azure DevOps användas för att skapa en [git](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git) -eller [Team Foundation](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc) -lagringsplats.

## <a name="feedback-loops"></a>Feedback-slingor

Den nyckel som används för att skapa kund partnerskap under Innovations cykler är att göra kunden till en del av lösningen. Detta görs med en armarna längd genom att [mäta kund påverkan](./measure.md). Mer noggrant kräver den konversationer och direkt testning med kunden. Båda resulterar i feedback som måste hanteras.

Varje återkopplings punkt är en potentiell lösning på kund behovet. Det är viktigt att varje bit av feedback direkt från en kund är en möjlighet att förbättra samarbetet. Om feedback gör den till en MVP-lösning, kan du fira den med kunden. Även om feedbacken inte kan åtgärdas, är det helt enkelt att bli transparent med beslutet att göra en prioritering av feedbacken, vilket visar en [tillväxt tänkesätt](./learn.md#growth-mindset) och ett fokus på [kontinuerlig inlärning](./learn.md#continuous-learning).

[Azure DevOps](https://docs.microsoft.com/azure/devops) innehåller metoder för att [begära, tillhandahålla och hantera feedback](https://docs.microsoft.com/azure/devops/project/feedback). Vart och ett av dessa verktyg centraliserar feedback så att teamet kan vidta åtgärder och rapportera feedback, vilket ger en genomskinlig feedback-slinga.

## <a name="continuous-integration"></a>Kontinuerlig integrering

Eftersom antaganden skalas och en hypotes växer närmare den faktiska innovationen i stor skala, kommer antalet mindre Hypotheses som ska testas att växa snabbt. För riktiga feedback-slingor och smidiga införande processer är det viktigt att var och en av dessa Hypotheses är integrerade och stöder den främsta hypotesen bakom innovationen. Tyvärr måste du också gå snabbt till förnyat och växa, vilket kräver flera utvecklare som testar varianterna av den viktigaste hypotesen. Vid senare skedes utvecklings arbete kan det krävas flera team av utvecklare varje byggnad mot en delad lösning. Kontinuerlig integrering är det första steget mot hantering av olika rörliga delar.

I kontinuerlig integrering slås kod ändringar ofta samman i huvud grenen. Automatiserade bygg-och test processer säkerställer att kod i huvud grenen alltid är produktions kvalitet. På så sätt kan utvecklare samar beta för att utveckla delade lösningar som ger korrekta och tillförlitliga feedback-slingor.

Azure-DevOps och [Azure-pipelines](https://docs.microsoft.com/azure/devops/pipelines) tillhandahåller kontinuerliga integrerings funktioner med några få klickningar, för GitHub eller flera andra lagrings platser.
Läs mer om [kontinuerlig integrering](https://docs.microsoft.com/azure/devops/learn/what-is-continuous-integration) eller kör [praktiska labbet](https://www.azuredevopslabs.com/labs/azuredevops/continuousintegration) för mer information. Det finns även lösnings arkitekturer för att påskynda skapandet av dina [CI/CD-pipeliner med Azure DevOps](https://azure.microsoft.com/solutions/devops).

## <a name="reliable-testing"></a>Reliable test

Fel i alla lösningar kan skapa falska positiva eller falska negativa negativa tal. Oväntade fel kan lätt leda till fel tolkning av användar mått. Det kan också leda till negativ feedback från kunder som inte korrekt representerar testet av din hypotes.

Vid tidiga iterationer av en MVP-lösning förväntas defekter, och vi kan till och med upptäcka dem. I tidiga versioner kommer godkännande testningen troligen inte att finnas. En aspekt av att skapa med empati är dock valideringen av behovet och hypotesen. Båda kan slutföras genom enhets tester på en kod nivå och manuella acceptans test innan distributionen. Tillsammans ger dessa ett visst sätt att testa tillförlitlighet. Längre sikt en väldefinierad serie med build-, enhets-och acceptans test bör automatiseras för att säkerställa att pålitliga Mät värden som är relaterade till mer fina kärnor justeras mot hypotesen och den resulterande lösningen.

[Azures testplaner](https://docs.microsoft.com/azure/devops/test/track-test-status?view=azure-devops) innehåller verktyg för att utveckla och driva test planer under manuell eller automatiserad test körning.

## <a name="solution-deployment"></a>Lösningsdistribution

Kanske är den mest meningsfulla aspekten av att införa en bättre möjlighet att styra lanseringen av en lösning till kunderna. Genom att tillhandahålla en självbetjänings-eller automatiserad pipeline för att släppa en lösning på kunder kan du påskynda feedback-slingan. Att låta kunderna interagera med ändringar i lösningen snabbt, bjuder in kunden i processen. Det gör det också enklare att testa Hypotheses, minska antaganden och möjlighet att arbeta.

Det finns flera metoder för att distribuera lösningar, följande tre vanligaste metoder:

- Den mest avancerade metoden, **kontinuerlig distribution**, distribuerar automatiskt kod ändringar till produktion. För vuxen team som testar vuxen Hypotheses kan kontinuerlig distribution vara mycket värdefull.
- Vid tidiga utvecklings faser kan **kontinuerlig leverans** vara lämpligare. I kontinuerlig leverans distribueras alla kod ändringar automatiskt till en produktions miljö. Utvecklare, företags besluts fattare och andra i teamet kan använda den här miljön för att kontrol lera att deras arbete är produktions klart. Det kan också användas för att testa en hypotes med kunder, utan att påverka pågående affärs aktiviteter.
- **Manuell distribution** är den minst avancerade metoden för versions hantering. Som namnet antyder skulle någon i teamet manuellt distribuera de senaste kod ändringarna. Den här metoden är fel känsligt, otillförlitligt och betraktas som ett antimönster av de mest erfarna teknikerna.

Under den första iterationen av en MVP-lösning är manuell distribution en vanlig metod, trots beskrivningen ovan. När lösningen är mycket flytande och kundfeedback är okänd, finns det en betydande risk för att återställa hela lösningen (eller till och med Core hypotesen). Den allmänna regeln för manuell distribution: inget kund bevis, ingen distributions automatisering. Att investera tidigt kan leda till förlorad tid. Det kan vara viktigare att skapa beroenden på den lanserings pipeline som gör gruppen mer motstånds kraftig mot en tidig Pivot Pivot. Efter de första iterationerna eller när kunden feedback föreslår potentiell framgång, bör en mer avancerad distributions modell snabbt antas.

I alla stadier av hypotes validering ger Azure-DevOps och [Azure-pipeliner](https://docs.microsoft.com/azure/devops/pipelines) kontinuerlig leverans och kontinuerliga distributions möjligheter med bara några få klick. Läs mer om [kontinuerlig leverans](https://docs.microsoft.com/azure/devops/learn/what-is-continuous-delivery) eller kör [praktiska labbet](https://www.azuredevopslabs.com/labs/azuredevops/continuousdeployment) för mer information. Lösnings arkitekturer kan också påskynda skapandet av dina [CI/CD-pipeliner med Azure DevOps](https://azure.microsoft.com/solutions/devops).

## <a name="integrated-measurements"></a>Integrerade mätningar

När du [mäter kund påverkan](./measure.md)är det viktigt att förstå hur kunderna reagerar på ändringar i lösningen. Dessa data kallas telemetri och ger insikter om vilka åtgärder en användning (eller kohort av användare) vidtog när lösningen användes. Från dessa data är det enkelt att få en kvantitativ validering av hypotesen. Dessa mått kan sedan användas för att justera lösningen och generera mer detaljerade Hypotheses. De här diskreta ändringarna bidrar mogna till den första lösningen i efterföljande iterationer, vilket i slut ändan upprepas i stor skala.

I Azure tillhandahåller [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) verktyg och gränssnitt för att samla in och granska data från kund upplevelser. Dessa observationer och insikter kan användas för att förfina efter släpning med hjälp av [Azure-kort](https://docs.microsoft.com/azure/devops/boards).

## <a name="next-steps"></a>Nästa steg

Med en förståelse för de verktyg och processer som krävs för att göra det, är det dags att undersöka en mer avancerad Innovations disciplin, [interagera med enheter](./devices.md). Det kan bidra till att minska barriärerna mellan fysiska och digitala upplevelser, vilket gör lösningen ännu enklare att införa.

> [!div class="nextstepaction"]
> [Interagera med enheter](./devices.md)
