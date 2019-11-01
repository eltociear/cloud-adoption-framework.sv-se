---
title: 'Utveckling av molnet: förutsäga och påverka'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introduktion till utveckling av moln – predict och inflytande
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 83165e21882b4979d0fb3b104fa4f2c12aed326c
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/31/2019
ms.locfileid: "73239466"
---
# <a name="predict-and-influence"></a>Förutspå och påverka

Det finns två klasser av program i den digitala ekonomin: historisk och förutsäga. Många kund behov kan bara uppfyllas genom att använda historiska data, inklusive data i nära real tid. De flesta lösningar fokuserar främst på att samla in data, i ögonblick. De bearbetar och delar dessa data tillbaka till kunden i form av en digital eller omgivande upplevelse.

När förutsägande modellering blir mer kostnads effektivt och lättillgängligt, kund support för att söka efter erfarenheter som leder till bättre beslut och åtgärder. Men det behöver inte alltid leda till en förutsägelse lösning. I de flesta fall kan en historisk vy tillhandahålla tillräckligt med data för att hjälpa kunden att fatta ett beslut på egen hand.

Kunderna har tyvärr en Myopic vy som leder till beslut baserat på deras omedelbara omgivning och inflytande. I takt med att alternativ och beslut växer i tal och effekter, kan det hända att Myopic-vyn inte leder till att kunden behöver uppfyllas. Samtidigt som hypotesen är beprövad i skala kan företaget som tillhandahåller lösningen se flera tusen eller miljon tals kund beslut. Det är möjligt att se mönster och påverkan av dessa mönster. Förutsägbara funktioner är en bra investering när det krävs en förståelse av dessa mönster för att fatta beslut som uppfyller kundernas behov.

## <a name="examples-of-predictions-and-influence"></a>Exempel på förutsägelser och inflytande

Användning av data för att göra förutsägelser kan ses i olika program och i olika miljöer.

- **eCommerce:** Föreslagna objekt är ett exempel på förutsägelse. Webbplatsen kan föreslå produkter som kan vara värda att lägga till i din varukorg, baserat på vad andra har köpt tillsammans.
- **Justerad verklighet:** IoT erbjuder fler avancerade exempel. En enhet på en sammansättnings linje upptäcker en ökning i en dator temperatur. En molnbaserad förutsägelse modell avgör hur du svarar. Baserat på den förutsägelsen instrueras en annan enhet att sakta ned sammansättnings linjen tills datorn kan svalna.
- **Konsument produkter:** Mobil telefoner, smart hem, även om din bil innehåller vissa delar av förutsägelse funktioner genom att föreslå aktiviteter baserat på faktorer som plats eller tid på dagen. När förutsägelsen och den första hypotesen är justerade påverkar dessa förutsägelser dina beteenden. När båda blir mycket mogna leder förutsägelsen till åtgärder, till exempel en bil bil.

## <a name="developing-predictive-capabilities"></a>Utveckla förutsägelse funktioner

Lösningar som konsekvent ger exakta förutsägande funktioner omfattar ofta fem huvud egenskaper: data, insikter, mönster, förutsägelser och interaktioner. Varje krävs för att utveckla förutsägbara funktioner. I likhet med alla fantastiska innovationer kräver utvecklingen av förutsägande funktioner ett [åtagande att upprepa](./index.md#commitment-to-iteration). I varje iteration skulle en eller flera av följande egenskaper vara mogna för att validera allt mer komplexa kund Hypotheses.

![Steg för att förutsäga funktioner](../../_images/innovate/predict-and-influence.png)

> [!CAUTION]
> Om kunden hypotes som har utvecklats från artikeln [om att utveckla med kund empati](./build.md) innehåller förutsägande funktioner, kan den här artikeln vara tillämplig. Men förutsägande funktioner kräver betydande investeringar av tid och energi. När förutsägande funktioner är [tekniska toppar](./build.md#reduce-complexity-and-delay-technical-spikes), i stället för en källa med kund värde, rekommenderar vi att du fördröjer förutsägelser tills kunden hypotesen har validerats i stor skala.

## <a name="data"></a>Data

Det enklaste av egenskaperna ovan är data. Var och en av de föregående disciplinerna för att utveckla digitala uppfinningar genererar data. Dessa data kan bidra till utvecklingen av förutsägelser. Mer information om hur du hämtar data till en förutsägelse lösning finns i artiklarna om [democratizing-data](./data.md) eller att [interagera med enheter](./devices.md).

Ett antal data källor kan användas för att leverera förutsägbara funktioner:

## <a name="insights"></a>Insikter

Ämnes experter utnyttjar data om kundernas behov och beteenden för att utveckla grundläggande affärs insikter från en studie av rå data. Dessa insikter kan hitta förekomster av önskade kund beteenden (eller alternativa oönskade resultat). Under iterationer av förutsägelserna kan dessa insikter hjälpa till att identifiera potentiella korrelationer, vilket kan ha en orsakssamband till positiva resultat. Vägledning om hur du aktiverar ämnes experter för att utveckla insikter finns i artikeln om [democratizing-data](./data.md).

## <a name="patterns"></a>Mönster

Mänskligt problem med identifiering av mönster på stora data volymer. Datorer har utformats för detta ändamål. Maskin inlärning påskyndar det syftet genom att identifiera mönster i en stor mängd data, vilket kallas maskin inlärnings modell. Dessa mönster tillämpas sedan genom Machine Learning-algoritmer för att förutsäga vad som händer när en ny uppsättning data punkter matas in i algoritmerna.

Använda insikter som en start punkt, maskin inlärnings tåg och använder förutsägande modeller för data för att öka versaler i mönstren i data. Genom flera iterationer av utbildning, testning och införande av dessa modeller och algoritmer kan du förutsäga framtida resultat på ett korrekt sätt.

[Azure Machine Learning service](https://docs.microsoft.com/azure/machine-learning/service/overview-what-is-azure-ml) är det molnbaserade verktyget i Azure för att skapa och träna modeller baserat på dina data. Det här verktyget innehåller också ett [arbets flöde för att påskynda utvecklingen av Machine Learning-algoritmer](https://docs.microsoft.com/azure/machine-learning/service/concept-azure-machine-learning-architecture). Det här arbets flödet kan användas för att utveckla algoritmer med hjälp av Visual-gränssnittet eller python.

För mer robusta maskin inlärnings modeller tillhandahåller [ml-tjänster i Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview) en maskin inlärnings plattform som bygger på Apache Hadoop kluster. Den här metoden gör det möjligt för mer detaljerad kontroll över de underliggande klustren, lagrings enheterna och Compute-noderna. Att använda Azure HDInsight ger också mer avancerad integrering via verktyg som scaler och sparker för att skapa förutsägelser baserade på integrerade och inmatade data, till och med att arbeta med data från en ström. Lösningen för att [förutsäga](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-scaler-sparkr) den här typen av flygning visar var och en av dessa avancerade funktioner för att förutse fördröjningar i flygningen utifrån väder förhållanden HDInsight-lösningen tillåter också företags kontroller, till exempel data säkerhet, nätverks åtkomst och prestanda övervakning till operationalisera-mönster.

## <a name="predictions"></a>Förutsägelser

När ett mönster har skapats och tränats kan det tillämpas med hjälp av API: er som kan göra förutsägelser under leverans av en digital upplevelse. De flesta av dessa API: er bygger på en vältränad modell som baseras på ett mönster i dina data. I takt med att fler kunder distribuerar vanliga arbets belastningar till molnet kan moln leverantörer tillhandahålla vanliga förutsägelse-API: er för att möjliggöra snabbare införande av förutsägelser.

[Azure Cognitive Services](https://docs.microsoft.com/azure/cognitive-services) är ett exempel på en FÖRUTSÄGande API-version av en moln leverantör. Den här tjänsten innehåller förutsägelse-API: er för innehålls moderatorer, avvikelse identifiering eller förslag på att anpassa innehåll. Dessa API: er är redo att användas baserat på vanliga innehålls mönster, som Microsoft har använt för att träna modeller. Vart och ett av dessa API: er gör förutsägelser baserat på data som du matar in i API: et.

[Azure Machine Learning tjänst](https://docs.microsoft.com/azure/machine-learning) möjliggör distribution av anpassade, inbyggda algoritmer som du kan skapa och träna enbart baserat på dina egna data. Lär dig mer om att distribuera förutsägelser med Azure Machine Learning [här](https://docs.microsoft.com/azure/machine-learning/service/how-to-deploy-and-where).

I artikeln om att konfigurera [HDInsight-kluster](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-provision-linux-clusters) diskuterar vi processerna för att exponera förutsägelser som utvecklats för ml-tjänster på Azure HDInsight.

## <a name="interactions"></a>Interaktioner

När en förutsägelse görs tillgänglig via ett API kan förutsägelsen användas för att påverka kundernas beteenden. Detta påverkar interaktions formen. En interaktion med en Machine Learning-algoritm sker i din andra digitala eller omgivande upplevelse. När data samlas in via programmet eller miljön körs dessa data via Machine Learning-algoritmerna. När algoritmen förutsäger ett resultat kan denna förutsägelse delas tillbaka med kunden genom den befintliga upplevelsen.

Lär dig mer om interaktioner inom en [justerad verklighets lösning](./devices.md#adjusted-reality)för mer information om hur du skapar en interaktion i en omgivnings upplevelse.

## <a name="next-steps"></a>Nästa steg

Baserat på den kunskap som vunnits om [uppfinningarna](./invention.md) i den innovativa [metod](./index.md) du känner till har de tekniska verktyg som krävs för att [bygga med empati](./build.md).

> [!div class="nextstepaction"]
> [Bygg med empati](./build.md)
