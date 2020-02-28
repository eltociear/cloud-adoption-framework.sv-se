---
title: Förutse och påverka kund beteendet
description: Använd förutsägande modellering för att utveckla förutsägande funktioner genom data, insikter, mönster, förutsägelser och interaktioner.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: e299025afcbf1066411f8d4792fe739663d46c74
ms.sourcegitcommit: 10637acba8c857a6f5aa8c4a80c0649903f60402
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/28/2020
ms.locfileid: "78171114"
---
# <a name="predict-and-influence"></a>Förutspå och påverka

Det finns två klasser av program i den digitala ekonomin: *historisk* och *förutsäga*. Många kund behov kan bara uppfyllas genom att använda historiska data, inklusive nästan real tids data. De flesta lösningar fokuserar främst på att aggregera data för tillfället. De bearbetar och delar dessa data tillbaka till kunden i form av en digital eller omgivande upplevelse.

När förutsägande modellering blir mer kostnads effektiv och lättillgänglig, kan kunder efter frågas om våra erfarenheter som leder till bättre beslut och åtgärder. Det kräver dock inte alltid en förutsägelse lösning. I de flesta fall kan en historisk vy tillhandahålla tillräckligt med data för att hjälpa kunden att fatta ett beslut på egen hand.

Kunderna tar tyvärr ofta en Myopic vy som leder till beslut baserat på deras omedelbara omgivning och inflytande. När alternativ och beslut växer i antal och konsekvenser kan den Myopic-vyn inte betjäna kundens behov. Samtidigt som hypotesen är beprövad i skala kan företaget som tillhandahåller lösningen se flera tusen eller miljon tals kund beslut. Den här stora bild metoden gör det möjligt att se breda mönster och påverkan av dessa mönster. Förutsägbara funktioner är en bra investering när det är nödvändigt att förstå dessa mönster för att fatta beslut som passar kunden bäst.

## <a name="examples-of-predictions-and-influence"></a>Exempel på förutsägelser och inflytande

En mängd olika program och omgivande upplevelser använder data för att göra förutsägelser:

- **E-handel:** Baserat på vad andra liknande konsumenter har köpt, föreslår en e-handelswebbplats produkter som kan vara värda att lägga till i din varukorg.
- **Justerad verklighet:** IoT erbjuder mer avancerade instanser av förutsägbara funktioner. En enhet på en sammansättnings rad kan till exempel upptäcka en ökning av datorns temperatur. En molnbaserad förutsägelse modell avgör hur du svarar. Baserat på denna förutsägelse saktar en annan enhet ned monterings linjen tills datorn kan svalna.
- **Konsument produkter:** Mobil telefoner, smart hus, till och med din bil, alla använder förutsägande funktioner, som de utnyttjar för att föreslå användar beteende baserat på faktorer som plats eller tid på dagen. När en förutsägelse och den första hypotesen är justerade leder förutsägelsen till åtgärd. I ett mycket tidigt skede kan den här justeringen göra produkter som en självdrivande bil en verklighet.

## <a name="develop-predictive-capabilities"></a>Utveckla förutsägande funktioner

Lösningar som konsekvent ger exakta förutsägande funktioner omfattar ofta fem huvud egenskaper: *data*, *insikter*, *mönster*, *förutsägelser*och *interaktioner*. Varje aspekt krävs för att utveckla förutsägbara funktioner. I likhet med alla fantastiska innovationer kräver utvecklingen av förutsägande funktioner ett [åtagande att upprepa](./index.md#commitment-to-iteration). I varje iteration är en eller flera av följande egenskaper förmogna för att validera allt mer komplexa kund Hypotheses.

![Steg för att förutsäga funktioner](../../_images/innovate/predict-and-influence.png)

> [!CAUTION]
> Om kund hypotesen som utvecklats i [build med kund empati](./build.md) innehåller förutsägande funktioner, kan principerna som beskrivs där också tillämpas. Förutsägbara funktioner kräver dock betydande investeringar av tid och energi. När förutsägande funktioner är [tekniska toppar](./build.md#reduce-complexity-and-delay-technical-spikes), i stället för en källa till verkligt kund värde, rekommenderar vi att du fördröjer förutsägelser tills Kundens Hypotheses har validerats i stor skala.

## <a name="data"></a>Data

Data är den viktigaste delen av de egenskaper som anges ovan. Varje ämnes område för utveckling av digitala uppfinningar genererar data. Dessa data bidrar naturligtvis till utveckling av förutsägelser. Mer information om hur du hämtar data till en förutsägelse lösning finns i [Democratizing data](./data.md) and [interagerar med enheter](./devices.md).

En mängd olika data källor kan användas för att leverera förutsägbara funktioner:

## <a name="insights"></a>Insikter

Ämnes experter använder data om kundernas behov och beteenden för att utveckla grundläggande affärs insikter från en studie av rå data. Dessa insikter kan hitta förekomster av önskade kund beteenden (eller också oönskade resultat). Under iterationer av förutsägelserna kan dessa insikter hjälpa till att identifiera potentiella korrelationer som slutligen kan generera positiva resultat. Vägledning om hur du aktiverar ämnes experter för att utveckla insikter finns i [Democratizing data](./data.md).

## <a name="patterns"></a>Mönster

Personer har alltid försökt identifiera mönster i stora data mängder. Datorer har utformats för detta ändamål. Maskin inlärning påskyndar fråge funktionen genom att identifiera exakta sådana mönster, en kunskap som omfattar Machine Learning-modellen. Dessa mönster används sedan genom Machine Learning-algoritmer för att förutsäga resultatet när en ny uppsättning data matas in i algoritmerna.

Med hjälp av insikter som en start punkt utvecklar maskin inlärning och använder förutsägande modeller för att få inblick i mönstren i data. Genom flera iterationer av utbildning, testning och införande kan dessa modeller och algoritmer förutse framtida resultat.

[Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/service/overview-what-is-azure-ml) är den molnbaserade tjänsten i Azure för att skapa och träna modeller baserat på dina data. Det här verktyget innehåller också ett [arbets flöde för att påskynda utvecklingen av Machine Learning-algoritmer](https://docs.microsoft.com/azure/machine-learning/service/concept-azure-machine-learning-architecture). Det här arbets flödet kan användas för att utveckla algoritmer via ett visuellt gränssnitt eller python.

För mer robusta maskin inlärnings modeller tillhandahåller [ml-tjänster i Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview) en maskin inlärnings plattform som bygger på Apache Hadoop kluster. Den här metoden ger mer detaljerad kontroll över de underliggande klustren, lagrings enheterna och Compute-noderna. Azure HDInsight erbjuder också mer avancerad integrering med verktyg som scaler och sparker för att skapa förutsägelser baserade på integrerade och inmatade data, även att arbeta med data från en ström. Lösningen för att [förutsäga fördröjningen](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-scaler-sparkr) visar var och en av dessa avancerade funktioner när de används för att förutse fördröjningar i flygningen baserat på väder förhållanden. HDInsight-lösningen tillåter också företags kontroller, till exempel data säkerhet, nätverks åtkomst och prestanda övervakning till operationalisera-mönster.

## <a name="predictions"></a>Förutsägelser

När ett mönster har skapats och tränats kan du använda det via API: er som kan göra förutsägelser under leverans av en digital upplevelse. De flesta av dessa API: er bygger på en vältränad modell som baseras på ett mönster i dina data. I takt med att fler kunder distribuerar vardags arbets belastningar till molnet leder de förutsägelse-API: er som används av moln leverantörer till allt snabbare införande.

[Azure Cognitive Services](https://docs.microsoft.com/azure/cognitive-services) är ett exempel på ett förutsägande API som skapats av en moln leverantör. Den här tjänsten innehåller förutsägelse-API: er för innehålls moderatorer, avvikelse identifiering och förslag på att anpassa innehåll. Dessa API: er är klara att använda och baseras på välkända innehålls mönster, som Microsoft har använt för att träna modeller. Var och en av dessa API: er gör förutsägelser baserat på de data som du matar in i API: et.

Med [Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning) kan du distribuera anpassade, inbyggda algoritmer som du kan skapa och träna utifrån enbart på dina egna data. Lär dig mer om att distribuera förutsägelser med [Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/service/how-to-deploy-and-where).

[Konfigurera HDInsight-kluster](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-provision-linux-clusters) diskuterar processerna för att exponera förutsägelser som utvecklats för ml-tjänster på Azure HDInsight.

## <a name="interactions"></a>Interaktioner

När en förutsägelse har gjorts tillgänglig via ett API kan du använda den för att påverka kundens beteende. Detta påverkar form av interaktioner. En interaktion med en Machine Learning-algoritm sker i din andra digitala eller omgivande upplevelse. När data samlas in via programmet eller miljön körs de via Machine Learning-algoritmer. När algoritmen förutsäger ett resultat kan denna förutsägelse delas tillbaka med kunden genom den befintliga upplevelsen.

Lär dig mer om hur du skapar en omgivande upplevelse genom en [justerad verklighets lösning](./devices.md#adjusted-reality).

## <a name="next-steps"></a>Nästa steg

Tack för att du har bekantat dig med [ämnes områden för uppfinning](./invention.md) och den innovativa [metoden](./index.md)är du nu redo att lära dig att [bygga med kund empati](./build.md).

> [!div class="nextstepaction"]
> [Bygg med empati](./build.md)
