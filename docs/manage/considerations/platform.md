---
title: Plattforms åtgärder i moln hantering
description: Bygg en förståelse av beroendet inom din organisation för vanliga plattforms åtgärder i moln hantering.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 3480d0411e1a16eed18d14859cbb997706ccccb4
ms.sourcegitcommit: da7ebd67a0ebf29361f093f00e10217b212a2eb2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/01/2020
ms.locfileid: "80527630"
---
# <a name="platform-operations-in-cloud-management"></a>Plattforms åtgärder i moln hantering

En moln hanterings bas linje som sträcker sig över [inventering och synlighet](./inventory.md), [operativa krav](./operational-compliance.md)och [skydd och återställning](./protect.md) kan ge en tillräckligt stor moln hanterings nivå för de flesta arbets belastningar i IT-portföljen. Men den bas linjen är sällan tillräckligt för att stödja hela portföljen. Den här artikeln bygger på det vanligaste nästa steget i moln hantering, portfölj åtgärder.

En snabb undersökning av till gångarna i IT-portföljen visar mönster över de arbets belastningar som stöds. Inom dessa arbets belastningar kommer det att finnas vanliga plattformar. Beroende på de tidigare tekniska besluten inom företaget kan dessa plattformar variera mycket.

För vissa organisationer kommer det att vara mycket beroende av SQL Server, Oracle eller andra data plattformar med öppen källkod. I andra organisationer kan commonalities vara rotad på värd plattformarna för virtuella datorer (VM) eller behållare. Andra kan ha ett gemensamt beroende av program eller ERP-system (Enterprise Resource Planning), till exempel SAP, Oracle eller andra.

Genom att förstå dessa commonalities kan moln hanterings teamet specialisera sig på högre support nivåer för de prioriterade plattformarna.

## <a name="establish-a-service-catalog"></a>Upprätta en tjänst katalog

Målet med plattforms åtgärder är att skapa pålitliga och upprepnings bara lösningar, som moln implementerings teamet kan använda för att leverera en plattform som ger en högre affärs åtagande nivå. Detta åtagande kan minska sannolikheten eller frekvensen för stillestånd, vilket förbättrar tillförlitligheten. Om ett systemfel uppstår kan åtagandet också minska mängden data förlust eller tid att återställa. Ett sådant åtagande innehåller ofta pågående, centraliserade åtgärder som stöd för plattformen.

När moln hanterings teamet har högre nivåer av drift hantering och specialisering som är relaterade till vissa plattformar, läggs dessa plattformar till i en växande tjänst katalog. Tjänst katalogen ger självbetjänings distribution av plattformar i en speciell konfiguration, som följer pågående plattforms åtgärder. Under affärs anpassnings konversationen kan moln hanterings-och moln strategi team föreslå tjänster för tjänst katalog som ett sätt för verksamheten att förbättra tillförlitlighet, drift tid och återställnings åtaganden i en kontrollerad, repeterbar process.

Vissa organisationer refererar till en tjänst katalog för tidiga faser som en _godkänd lista_. Den främsta skillnaden är att en tjänst katalog har pågående operativa åtaganden från vårt Expert Center (CCoE). En godkänd lista är liknande, där den innehåller en förgodkännen lista över lösningar som ett team kan använda i molnet. Men vanligt vis finns det ingen drifts förmån som är kopplad till program på en godkänd lista.

Ungefär som debatten mellan centrala IT och CCoE, är skillnaden en av prioriteterna. En tjänst katalog förutsätter en lämplig avsikt men ger drift, styrning och säkerhets guardrails som påskyndar innovationen. En godkänd lista hindrar innovation tills åtgärder, efterlevnad och säkerhets portar kan skickas för en lösning. Båda lösningarna är livskraftiga, men de kräver att företaget fattar beslut om diskret prioritering för att investera mer i innovation eller efterlevnad.

### <a name="build-the-service-catalog"></a>Bygg tjänst katalogen

Moln hantering fungerar sällan med att leverera en tjänst katalog i en silo. En korrekt utveckling av katalogen kräver ett partnerskap i Central IT eller CCoE. Den här metoden är mest effektiv när en IT-organisation når en CCoE-nivå, men kan implementeras tidigare.

När du skapar tjänst katalogen i en CCoE-modell bygger moln plattforms teamet på önskad plattform. Moln styrnings-och moln säkerhets teamen verifierar styrning och efterlevnad i distributionen. Moln hanterings teamet upprättar pågående åtgärder för plattformen. Och Cloud Automation-teamet paketerar plattformen för skalbar och upprepnings bara distribution.

När plattformen har paketerats kan moln hanterings teamet lägga till den i den växande tjänst katalogen. Därifrån kan moln implementerings teamet använda paketet eller andra i katalogen under distributionen. När lösningen går till produktion inser företaget de extra fördelarna med förbättrad drift hantering och potentiellt försämrade verksamhets avbrott.

> [!NOTE]
> Att skapa en tjänst katalog kräver en stor del av arbetet och tiden från flera team. Genom att använda tjänst katalogen eller den godkända listan som en hantera-mekanism går det långsamt. När innovation är en prioritet bör tjänst kataloger utvecklas parallellt med andra antagande ansträngningar.

## <a name="define-your-own-platform-operations"></a>Definiera dina egna plattforms åtgärder

Även om hanterings verktyg och processer kan hjälpa till att förbättra plattforms åtgärder, som ofta inte räcker till för att uppnå önskade stabilitets-och Tillförlitlighets tillstånd. Sanna plattforms åtgärder kräver en fokus på pelare för arkitektur kvalitet. När en plattform motiverar en djupare investering i driften bör följande fem pelare beaktas innan plattformen blir en del av en tjänst katalog:

- **Skalbarhet:** Möjligheten för ett system att hantera ökad belastning.
- **Tillgänglighet:** Den procent andel av tiden som ett system fungerar och fungerar.
- **Återhämtning:** Möjligheten för ett system att återställa efter fel och fortsätta att fungera.
- **Hantering:** De drifts processer som upprätthåller ett system som körs i produktion.
- **Säkerhet:** Skydda program och data från hot.

[Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/guide/pillars) innehåller en metod för att utvärdera vissa arbets belastningar för att nå dessa pelare, i syfte att förbättra den övergripande verksamheten. Dessa pelare kan användas för både plattforms åtgärder och arbets belastnings åtgärder.

## <a name="get-started-with-specific-platforms"></a>Kom igång med vissa plattformar

De plattformar som diskuteras i nästa avsnitt är vanliga för vanliga Azure-kunder och de kan enkelt motivera en investering i plattforms åtgärder. Moln hanterings team börjar med dem när de utformar plattforms drifts krav eller en fullständig tjänst katalog.

### <a name="paas-data-operations"></a>PaaS data åtgärder

Data är ofta den första plattformen för att garantera plattforms åtgärdernas investeringar. När data finns i en PaaS-miljö (Platform as a Service) är det möjligt för affärs intressenter att begära ett reducerat återställnings punkt mål för att minimera data förlust. Beroende på programmets beskaffenhet kan de också begära en minskning av återställnings tids mål (RTO). I båda fallen kan arkitekturen som stöder PaaS-baserade data lösningar enkelt hantera en ökad nivå av hanterings support.

I de flesta fall är kostnaden för att förbättra hanterings åtaganden enkelt motiverad, även för program som inte är verksamhets kritiska. Den här förbättringen av plattforms åtgärder är så vanlig att många moln hanterings grupper ser det mer som en förbättrad bas linje, snarare än som en riktig plattforms drifts förbättring.

### <a name="iaas-data-operations"></a>IaaS data åtgärder

När data finns i en traditionell lösning för infrastruktur som en tjänst (IaaS) kan arbetet för att förbättra återställnings-och RTO vara betydligt högre. Men affärs intressenterna vill uppnå bättre hanterings åtaganden påverkas sällan av ett PaaS jämfört med IaaS-beslut. Om det är något, kan en förståelse av de grundläggande skillnaderna i arkitekturen uppmana företaget att fråga efter PaaS-lösningar eller åtaganden som matchar vad som är tillgängligt på PaaS-lösningar. Modernisering av IaaS-dataplattformar bör betraktas som ett första steg i plattforms åtgärder.

När modernisering inte är ett alternativ prioriterar moln hanterings teamen ofta IaaS-baserade dataplattformar som en första nödvändig tjänst i tjänst katalogen. Genom att ge verksamheten ett val mellan fristående data servrar och klustrade data lösningar med hög tillgänglighet blir affärs åtagandet mycket lättare att under lätta. En grundläggande förståelse för de operativa förbättringarna och de ökade kostnaderna innebär att verksamheten fattar det bästa beslutet för affärs processer och stöd för arbets belastningar.

### <a name="other-common-platform-operations"></a>Andra vanliga plattforms åtgärder

Förutom dataplattformar brukar virtuella dator värdar vara en gemensam plattform för drift förbättringar. Moln plattforms-och moln hanterings team investerar oftast i förbättringar av VMware-värdar eller container lösningar. Sådana investeringar kan förbättra stabiliteten och tillförlitligheten hos värdarna, som har stöd för de virtuella datorerna, vilket i sin tur påverkar arbets belastningarna. Lämpliga åtgärder på en värd eller behållare kan förbättra återställnings-eller RTO för flera arbets belastningar. Den här metoden skapar förbättrade affärs åtaganden, men distribuerar investeringen. Förbättrade åtaganden och minskade kostnader kombinerar för att göra det mycket enklare att justera förbättringar av moln hantering och plattforms åtgärder.

## <a name="next-steps"></a>Nästa steg

På parallellt med förbättringar av plattforms åtgärder fokuserar moln hanterings team även på att förbättra [arbets](./workload.md) belastningen för de 20 procent eller färre produktions arbets belastningarna.

> [!div class="nextstepaction"]
> [Förbättra arbets belastnings åtgärder](./workload.md)
