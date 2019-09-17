---
title: Skapa en finansiell modell för molnomvandling
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Så här skapar du en finans modell för moln omvandling.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: 75f19fcdc9f23066d5a6471cd79c0a6a00869554
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028269"
---
# <a name="create-a-financial-model-for-cloud-transformation"></a>Skapa en finansiell modell för molnomvandling

Att skapa en finansiell modell som korrekt representerar det fullständiga affärs värdet för alla moln omvandlingar kan vara komplicerat. Finansiella modeller och affärs motiveringar tenderar att variera för olika organisationer. I den här artikeln fastställs några formler och det finns några saker som ofta saknas när grund skapar finansiella modeller.

## <a name="return-on-investment"></a>Avkastning på investeringar

Avkastning på investering (ROI) är ofta ett viktigt kriterium för C-sviten eller tavlan. ROI används för att jämföra olika sätt att investera begränsade kapital resurser. Formeln för ROI är ganska enkel. Den information du behöver för att skapa varje indata till formeln är kanske inte lika enkel. ROI är i princip mängden avkastning som skapats från en första investering. Den visas vanligt vis som en procents ATS:

![AVKASTNINGen är lika med (vinst från investering minus kostnad för investering) dividerat med kostnaden för investeringen](../_images/strategy/formula-roi.png)

I nästa avsnitt kommer vi att gå igenom de data du behöver för att beräkna den första investeringen och vinsten från investeringen (intäkter).

## <a name="calculating-initial-investment"></a>Beräkna initial investering

Initial investering är den kapital kostnad och drift kostnad som krävs för att slutföra en omvandling. Klassificeringen av kostnader kan variera beroende på redovisnings modeller och ekonomi preferenser. Den här kategorin omfattar exempelvis objekt som professionella tjänster att transformera, program varu licenser som används endast under omvandlingen, kostnaden för moln tjänster under omvandlingen och eventuellt kostnad för avlönade anställda under omvandlingen .

Lägg till dessa kostnader för att skapa en uppskattning av den första investeringen.

## <a name="calculating-the-gain-from-investment"></a>Beräkna vinsten från investeringen

Att beräkna vinsten från investeringar kräver ofta en andra formel som är specifika för affärs resultat och tillhör ande tekniska ändringar. Att beräkna intäkter är svårare än att beräkna kostnads minskningar.

Om du vill beräkna intäkter behöver du två variabler:

![Vinst från investering är lika med intäkts delta plus kostnads delta](../_images/strategy/formula-gain-from-investment.png)

Dessa variabler beskrivs i följande avsnitt.

## <a name="revenue-deltas"></a>Intäkts delta

Intäkts delta bör vara prognostiserat i partnerskap med affärs intressenter. När affärs intressenterna är överens om en inkomst påverkan kan den användas för att förbättra uppdraget.

## <a name="cost-deltas"></a>Kostnads delta

Kostnads delta är mängden ökning eller minskning som orsakas av omvandlingen. Oberoende variabler kan påverka kostnads delta. Intäkter baseras i stort sett på hårda kostnader som minskning av kapital kostnader, kostnads nedsättning, drifts kostnads minskningar och värdeminskning. I följande avsnitt beskrivs några kostnads delta att tänka på.

### <a name="depreciation-reduction-or-acceleration"></a>Minskning eller acceleration av avskrivning

För vägledning om avskrivning kan du prata med ekonomi chefen eller ekonomi teamet. Följande information är avsedd att fungera som en allmän referens för avskrivnings avsnittet.

När kapitalet investeras i förvärvet av en till gång, kan denna investering användas för finansiella eller skattemässiga orsaker för att skapa kontinuerliga förmåner över den förväntade livs längd av till gången. Vissa företag ser avskrivning som en positiv skatte förmån. Andra ser det som en genomförd, löpande kostnad som liknar andra återkommande utgifter som hänförs till den årliga IT-budgeten.

Prata med ekonomi kontoret för att ta reda på om Eli minering av avskrivning är möjligt och om det skulle göra ett positivt bidrag till kostnads delta.

### <a name="physical-asset-recovery"></a>Återställning av fysisk till gång

I vissa fall kan pensionerade till gångar säljas som en källa till intäkten. Den här intäkten är ofta fördelad i kostnads minskning för enkelhetens skull. Men det är verkligen en ökning av intäkterna och kan beskattas som sådan. Prata med ekonomi kontoret för att förstå det här alternativets viabilitet och hur du kan ta hänsyn till de resulterande intäkterna.

### <a name="operational-cost-reductions"></a>Reducering av drifts kostnader

Återkommande utgifter som krävs för att driva ett företag kallas ofta drifts kostnader. Detta är en bred kategori. I de flesta bokförings modeller innehåller den:

- Program varu licensiering.
- Värd kostnader.
- Elektriska fakturor.
- Fastighets hyror.
- Kyl utgifter.
- Tillfällig personal som krävs för åtgärder.
- Utrustnings hyror.
- Ersättnings delar.
- Underhålls kontrakt.
- Reparera tjänster.
- Tjänster för verksamhets kontinuitet och haveri beredskap (BCDR).
- Andra utgifter som inte kräver godkännande av kapital utgifter.

Den här kategorin innehåller en av de mest tjänande deltarna. När du överväger en molnbaserad migrering är tiden som du investerat i att göra den här listan uttömmande sällan onödigt. Fråga CHEFs-och finansierings frågor för att se till att alla operativa kostnader redovisas.

### <a name="cost-avoidance"></a>Kostnads snedvridning

När en drifts kostnad förväntas men ännu inte har godkänts i en godkänd budget kanske den inte får plats i en kostnads reduktions kategori. Om till exempel VMware-och Microsoft-licenser måste omförhandlas och betalas nästa år, är de inte helt kvalificerade kostnader än. Minskning av de förväntade kostnaderna behandlas som drifts kostnader för att kunna beräkna kostnads beräkningar. De bör dock kallas "kostnads snedvridning" tills förhandlingen och budget godkännandet har slutförts.

### <a name="soft-cost-reductions"></a>Reducering av mjuka kostnader

På vissa företag kan mjuka kostnader som minskning av drifts komplexitet eller minskning i heltids personal för drift av ett Data Center också inkluderas i Cost delta. Men även mjuka kostnader kanske inte är en bra idé. När du inkluderar mjuka kostnads minskningar infogar du ett ej dokumenterat antagande om att minskningen skapar avsevärda kostnads besparingar. Teknik projekt resulterar sällan i faktisk återställning av mjuka kostnader.

### <a name="headcount-reductions"></a>Minska antalet anställda

Tids besparingar för personal inkluderas ofta under reducering av mjuka kostnader. När tids besparingarna mappas till den faktiska minskningen av IT-lönen eller personaling kan de beräknas separat som en minskning av antalet anställda.

Detta innebär att de kunskaper som behövs lokalt mappar i allmänhet till en liknande (eller högre) kunskaps uppsättning som krävs i molnet. De är därför vanligt vis avstängda efter en molnbaserad migrering.

Ett undantag uppstår när drift kapaciteten tillhandahålls av en tredje part eller en provider för hanterade tjänster (MSP). Om IT-systemen hanteras av en tredje part kan drifts kostnaderna ersättas av en molnbaserad lösning eller en molnbaserad MSP. En molnbaserad MSP fungerar förmodligen effektivare och kan eventuellt sänkas till en lägre kostnad. Om så är fallet, hör drift kostnads minskningarna i beräkningen av hård kostnaden.

### <a name="capital-expense-reductions-or-avoidance"></a>Minskning av kapital kostnader eller undvikande

Kapital kostnader skiljer sig något från drifts kostnader. I allmänhet drivs den här kategorin av uppdaterings cykler eller data Center expansion. Ett exempel på en data Center expansion skulle vara ett nytt högpresterande kluster som är värd för en stor data lösning eller ett informations lager. Den här kostnaden passar normalt in i en utgifts kategori för kapital. Vanligare är de grundläggande uppdaterings cyklerna. Vissa företag har stela maskin varu uppdaterings cykler, vilket innebär att till gångar tas ur bruk och byts ut i en vanlig cykel (vanligt vis var tredje, fem eller åtta år). Dessa cykler sammanfaller ofta med till gångs lån eller prognostiserad livs längd för utrustning. När en uppdaterings cykel träffar, ritas kapital kostnader för att förvärva ny utrustning.

Om en uppdaterings cykel godkänns och budgeteras kan moln omvandlingen hjälpa till att eliminera kostnaden. Om en uppdaterings cykel planeras men ännu inte har godkänts kan moln omvandlingen undvika kapital utgifter. Båda minskningarna läggs till i kostnad delta.

## <a name="next-steps"></a>Nästa steg

Lär dig mer om modeller för [moln redovisning](./cloud-accounting.md) .

> [!div class="nextstepaction"]
> [Moln redovisning](./cloud-accounting.md)
