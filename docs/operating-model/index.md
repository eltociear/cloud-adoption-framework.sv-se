---
title: Introduktion till driftsmodellen
description: Använd Cloud Adoption Framework för Azure för att lära dig hur du etablerar en driftsmodell för molnet.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: operating-model
ms.openlocfilehash: 4f28ec6b7c70f98ccea2fc718f44ebfa450caf52
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80428922"
---
# <a name="establish-an-operating-model-for-the-cloud"></a>Upprätta en driftsmodell för molnet

Molnimplementering är ett iterativt arbete där fokus ligger på arbetet som utförs i molnet. I molnstrategin beskrivs den digitala omvandlingen, och den är ett stöd i verksamheten när teamen jobbar med olika implementeringsprojekt. Med en ordentlig planering och beredskap kan du se till att de här viktiga elementen lyckas. Alla steg i molnimplementeringen motsvarar konkreta projekt med hanterbara mål, tidsramar och budgetar.

De här implementeringsåtgärderna är relativt enkla att spåra och mäta, även om de beräknas omfatta flera iterationer och versioner. Varje fas i implementeringens livscykel är viktig. Under varje fas kan det uppstå hinder relaterade till verksamheten, företagskulturen och den teknik som används. Varje fas är även starkt beroende av den underliggande driftsmodellen.

**Om implementeringen beskriver vad som görs så definierar driftsmodellen den underliggande strukturen för vem som gör det och hur det ska genomföras.**

”Kultur slår strategi med hästlängder”. Driftsmodellen är i praktiken IT-kulturens essens indelad i ett antal mätbara processer. När molnet underbyggs av en kraftfull driftsmodell kommer kulturen att bidra till strategin och skynda på implementeringen så att affärsvärdena kan realiseras i verksamheten. Om implementeringen å andra sidan lyckas utan någon driftsmodell så kan resultatet vara imponerande, men tyvärr mycket kortvarigt. Om implementeringen ska lyckas i längden måste den utvecklas parallellt med driftsmodellen.

## <a name="establish-your-operating-model"></a>Upprätta din driftsmodell

Befintliga driftsmodeller kan skalas och anpassas till molnimplementeringen. En modern driftsmodell hjälper dig att eliminera icke-tekniska hinder som försvårar molnimplementeringen.

Det här avsnittet om Cloud Adoption Framework beskriver en praktiskt tillämpbar driftsmodell som underlättar icke-tekniska beslut. Den här driftsmodellen består av tre metoder som hjälper dig att skapa en egen driftsmodell för molnet:

- [Styra](../govern/index.md): Garantera konsekvens för alla implementeringsåtgärder. Anpassa till styrnings- eller efterlevnadskrav för att upprätthålla en välhanterad molnöverskridande miljö.
- [Hantera](../manage/index.md): Anpassa pågående processer för den operativa hanteringen av teknik för att maximera värdet och minimera störningar.
- [Organisera](../organize/index.md): I takt med att driftsmodellen utvecklas så gör även organisationen av team och resurser det, vilket i sin tur stärker utvecklingen.

## <a name="align-operating-models"></a>Justera driftsmodeller

Molnet och den digitala ekonomin har visat på behovet av att använda flera olika driftsmodeller. Ibland beror det här på att flera olika offentliga moln måste hanteras. Vanligare är att det beror på övergången från en lokal drift till molnet. I båda fallen är det viktigt att anpassa driftsmodellerna efter varandra så att du får bästa möjliga resultat och så lite redundans som möjligt.

Analytikerna förutspår att vi kommer använda flera moln och allt större volymer i framtiden. För många kunder börjar det här redan bli verklighet. Det kan dessvärre uppstå betydande svårigheter när flera olika moln ska hanteras. Dubbletter av resurser, processer, kunskaper och teknik leder till ökade kostnader, inte de besparingar som utlovades i samband med övergången till molnet. För att undvika den här trenden bör kunderna använda en specialiserad driftsmodell. När driftsmodellerna anpassas bör det alltid finnas en **allmän driftsmodell**. Du kan använda fler **specialiserade driftsmodeller** för specifika scenarier där du måste hantera avvikelser från den allmänna modellen.

- **Allmän driftsmodell:** Den allmänna driftsmodellen är anpassad efter en enda offentlig eller privat molnplattform. I modellen definieras standarder, policyer och processer för den här plattformen. Den här driftsmodellen bör vara central i utvecklingen av molnstrategin. I den här modellen är målet att använda den primära molnleverantören för större delen av molnimplementeringen.

- **Specialiserad driftsmodell:** För vissa affärsresultat kanske en annan molnleverantör passar bättre. När det finns ett relevant användningsfall kan standarder, policyer och processer från den allmänna driftsmodellen användas hos den nya molnleverantören, men justeras så att de passar bättre för det specialiserade användningsfallet.

Om Azure är den primära plattformen så kan du ha nytta av vägledningarna och metodtipsen i respektive avsnitt ovan när du ska ta fram en egen driftsmodell. Materialet är dock anpassat efter att alla kanske inte har bestämt sig för Azure som primär plattform. Teorin i de olika avsnitten gäller därför även driftsmodeller för offentliga eller privata moln av liknande typ.

## <a name="next-steps"></a>Nästa steg

Styrning är det första steget när du skapar en driftsmodell för molnet.

> [!div class="nextstepaction"]
> [Lär dig mer om molnstyrning](../govern/index.md)
