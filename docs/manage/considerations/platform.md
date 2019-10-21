---
title: Plattforms åtgärder – moln hantering och åtgärder
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Plattforms åtgärder – moln hantering och åtgärder
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: aab6dbe2ff8b1037a86317d00d717b4b22052c59
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558056"
---
# <a name="platform-operations-in-cloud-management"></a>Plattforms åtgärder i moln hantering

En bas linje för moln hantering som sträcker sig över [inventering och synlighet](./inventory.md), [operativa krav](./operational-compliance.md)och [skydd och återställning](./protect.md) kan ge en tillräckligt stor moln hanterings nivå för de flesta arbets belastningar i IT-portföljen. Men det är sällan tillräckligt för att stödja hela portföljen. Den här artikeln bygger på det vanligaste nästa steget i moln hantering, portfölj åtgärder.

En snabb undersökning av till gångarna i IT-portföljen markerar mönster över de arbets belastningar som stöds. Inom dessa arbets belastningar finns det ett antal vanliga plattformar. Beroende på de tidigare tekniska besluten inom företaget kan dessa plattformar vara mycket olika. För vissa organisationer kommer det att vara ett tungt beroende av SQL Server, Oracle eller andra data plattformar med öppen källkod. I andra organisationer kan commonalities vara rotad på värd plattformarna för virtuella datorer eller behållare. Andra kan ha ett gemensamt beroende av program eller ERP-system (Enterprise Resource Planning) som SAP, Oracle eller andra.

Genom att förstå dessa commonalities kan moln hanterings teamet specialisera sig på högre stöd nivåer för de prioriterade plattformarna.

## <a name="establish-a-service-catalog"></a>Upprätta en tjänst katalog

Målet med plattforms åtgärder är att skapa pålitliga och upprepnings bara lösningar som kan utnyttjas av ett moln antagande team för att leverera en plattform som ger en högre affärs åtagande nivå. Detta åtagande kan minska sannolikheten eller frekvensen för stillestånds tid, vilket förbättrar tillförlitligheten. Åtagandet kan också minska mängden data förlust eller tid att återställa, om ett systemfel inträffar. Detta åtagande omfattar ofta pågående, centraliserade åtgärder som stöd för plattformen.

När moln hanterings teamet har högre nivåer av drift hantering och specialisering som är relaterade till vissa plattformar, läggs dessa plattformar till i en växande tjänst katalog. Den tjänst katalogen ger självbetjänings distribution av plattformar i en speciell konfiguration, som följer pågående plattforms åtgärder. Under affärs justerings-konversationen kan moln hanterings-och moln strategi team föreslå service Catalog-lösningar på ett sätt som gör det möjligt för verksamheten att förbättra Tillförlitlighets-, drift-och återställnings åtaganden i en kontrollerad, repeterbar process.

Vissa organisationer hänvisar till en tidig fas tjänst katalog som en "godkänd lista" som referens. Den främsta skillnaden är att en tjänst katalog har pågående operativa åtaganden från moln Center. En "godkänd lista" är liknande, eftersom den innehåller en för hands godkänd lista med lösningar som ett team kan använda i molnet, men det är vanligt vis en drifts förmån som är kopplad till "godkända listor"-program. Ungefär som debatten mellan centrala IT och CCoE, är skillnaden en av prioriteterna. En tjänst katalog förutsätter en lämplig avsikt men ger drift, styrning och säkerhets guardrails som påskyndar innovationen. En "godkänd lista" hindrar innovation tills åtgärder, efterlevnad och säkerhets portar kan skickas för en lösning. Båda är livskraftiga lösningar men kräver att ett företag fattar beslut om diskret prioritering för att investera mer i innovation eller efterlevnad.

### <a name="building-the-service-catalog"></a>Skapa tjänst katalogen

Moln hantering fungerar sällan med att leverera en tjänst katalog i en silo. En korrekt utveckling av katalogen kräver ett partnerskap i Central IT eller i molnet med Expert Center (CCoE). Den här metoden är mest effektiv när en IT-organisation når en CCoE-nivå, men kan implementeras tidigare.

När du skapar tjänst katalogen i en CCoE-modell, bygger moln plattforms teamet på önskad tillstånds plattform. Moln styrnings-och moln säkerhets teamen verifierar styrning och efterlevnad i distributionen. Moln hanterings teamet upprättar pågående åtgärder för plattformen. Cloud Automation-teamet paketerar plattformen för skalbar, repeterbar distribution.

När paketet har paketerats kan moln hanterings teamet lägga till paketet i den växande tjänst katalogen. Härifrån kan moln implementerings teamet använda det paketet eller andra i katalogen under distributionen. När lösningen går till produktion får företaget extra fördelar med förbättrad drifts hantering och potentialen för mindre avbrott i verksamheten.

> [!NOTE]
> Att skapa en tjänst katalog kräver en stor del av arbetet och tiden från flera team. Genom att använda tjänst katalogen eller vitlista som en hantera-mekanism går det långsamt. När innovation är en prioritet bör tjänst kataloger utvecklas parallellt med andra antagande ansträngningar.

## <a name="defining-your-own-platform-operations"></a>Definiera dina egna plattforms åtgärder

Hanterings verktyg och processer kan förbättra plattforms åtgärder. Men det är ofta inte tillräckligt för att uppnå det önskade stabilitets-och Tillförlitlighets läget. Sanna plattforms åtgärder kräver en fokus på pelare för arkitektur kvalitet. När en plattform motiverar en djupare investering i driften bör följande fem pelare beaktas innan plattformen blir en del av en tjänst katalog:

1. Skalbarhet: möjligheten för ett system att hantera ökad belastning.
2. Tillgänglighet: den andel av tiden som ett system är funktionellt och fungerar.
3. Återhämtning: möjligheten för ett system att återställa efter fel och fortsätta att fungera.
4. Hantering: drifts processer som håller ett system som körs i produktion.
5. Säkerhet: skydda program och data från hot.

[Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/guide/pillars) innehåller en metod för att utvärdera vissa arbets belastningar för att nå dessa pelare, i syfte att förbättra den övergripande verksamheten. Dessa pelare kan användas för både plattforms åtgärder och arbets belastnings åtgärder.

## <a name="getting-started-with-specific-platforms"></a>Komma igång med vissa plattformar

För vanliga Azure-kunder är följande vanliga plattformar, som enkelt kan motivera en investering i plattforms åtgärder. Moln hanterings team börjar med dessa när de utformar plattforms drifts krav eller en fullständig tjänst katalog.

### <a name="paas-data-operations"></a>PaaS data åtgärder

Data är ofta den första plattformen för att garantera plattforms åtgärdernas investeringar. När data finns i en PaaS-miljö (Platform as a Service) är det möjligt för affärs intressenter att begära en minskad återställnings period för att minimera data förlust. Beroende på programmets beskaffenhet kan de också begära en minskning av RTO. I båda fallen kan arkitekturen som stöder PaaS-baserade data lösningar enkelt hantera en viss ökad hanterings nivå.

I de flesta fall är kostnaden för att förbättra hanterings åtaganden enkelt motiverad, även för program som inte är verksamhets kritiska. Den här förbättringen av plattforms åtgärder är så vanlig, så att många moln hanterings team ser det mer som en förbättrad bas linje, i stället för att behandla det som en riktig plattforms drifts förbättring.

### <a name="iaas-data-operations"></a>IaaS data åtgärder

När data finns i en traditionell IaaS-lösning (Infrastructure as a Service) kan arbetet för att förbättra RTO och återställningen vara betydligt högre. Men affärs intressenter vill uppnå bättre hanterings åtaganden påverkas sällan av ett PaaS vs. IaaS-beslut. Om allt, en förståelse av de grundläggande skillnaderna i arkitekturen, kan bli ombedd att be om PaaS-lösningar eller åtaganden som matchar vad som är tillgängligt på PaaS-lösningar. Modernisering av IaaS-dataplattformar bör betraktas som ett första steg i plattforms åtgärder.

När modernisering inte är ett alternativ prioriterar moln hanterings teamen ofta IaaS-baserade dataplattformar som en första nödvändig tjänst i tjänst katalogen. Genom att erbjuda verksamheten ett val mellan fristående data servrar och klustrade data lösningar med hög tillgänglighet blir affärs åtagandet mycket lättare att förenkla. En grundläggande förståelse för de operativa förbättringarna och de ökade kostnaderna är att man ska kunna fatta det bästa beslutet för affärs processerna och stödja arbets belastningar.

### <a name="other-common-platform-operations"></a>Andra vanliga plattforms åtgärder

Förutom dataplattformar brukar virtuella dator värdar vara en gemensam plattform för drift förbättringar. Moln plattforms-och moln hanterings team kommer oftast att investera i förbättringar av VMWare-värdar eller container lösningar för att förbättra stabiliteten och tillförlitligheten hos värdarna, som har stöd för de virtuella datorerna, vilka strömförsörjnings arbets belastningar. Lämpliga åtgärder på en värd eller behållare kan förbättra återställnings-/RTO för flera arbets belastningar. Den här metoden skapar förbättrade affärs åtaganden, men distribuerar investeringen. Bättre åtaganden och minskade kostnader gör det mycket enklare att justera förbättringar av moln hantering och plattforms åtgärder.

## <a name="next-steps"></a>Nästa steg

Tillsammans med förbättringar av plattforms åtgärder, kommer moln hanterings team också att fokuseras på att förbättra arbets belastnings [åtgärder](./workload.md) för de 20 högsta% eller färre arbets belastningarna i produktionen.

> [!div class="nextstepaction"]
> [Förbättra arbets belastnings åtgärder](./workload.md)
