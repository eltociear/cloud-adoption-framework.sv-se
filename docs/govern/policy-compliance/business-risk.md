---
title: Förstå affärs risk under molnbaserad migrering
description: Använd ramverket för moln införande för Azure för att lära dig mer om riskhanterings processer som hjälper dig att utvärdera, förstå, balansera och åtgärda migrerings risker.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 729a359f5ea44d77c691acb0a22477eed7cecb44
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77709438"
---
<!-- markdownlint-disable MD026 -->

# <a name="understand-business-risk-during-cloud-migration"></a>Förstå affärs risk under molnbaserad migrering

En förståelse av affärs risk är en av de viktigaste elementen i en moln omvandling. Risk enhets princip, och den påverkar övervaknings-och tvångs krav. Risken påverkar kraftigt hur vi hanterar den digitala egendomen, lokalt eller i molnet.

<!-- markdownlint-enable MD026 -->

## <a name="relativity-of-risk"></a>Relativitet av risk

Risken är relativ. Ett litet företag med några få IT-tillgångar, i en stängd byggnad har liten risk. Om du lägger till användare och en Internet anslutning med åtkomst till dessa till gångar är risken intensifierad. När det små företaget växer till Fortune 500-status är riskerna exponentiellt mer. Som intäkter, affärs processer, antal anställda och IT-tillgångar ackumuleras, risker och sammanslagning. IT-tillgångar som hjälper till att skapa intäkter är av påtaglig risk för att stoppa den inkomst strömmen i händelse av ett avbrott. Varje ögonblick av drift stopp motsvarar förluster. På samma sätt som data ackumuleras ökar risken för att kunderna skadas.

I den traditionella lokala världen har IT-avdelningen fokus på att utvärdera risker, skapa processer för att hantera dessa risker och distribuera system för att säkerställa att åtgärder vidtas. Dessa ansträngningar fungerar för att utjämna risker som krävs för att fungera i en ansluten, modern företags miljö.

## <a name="understand-business-risks-in-the-cloud"></a>Förstå affärs risker i molnet

Under en omvandling finns samma relativa risker.

- Vid tidig experimentering distribueras några till gångar med lite till inga relevanta data. Risken är liten.
- När den första arbets belastningen distribueras hamnar en liten risk. Denna risk åtgärdas enkelt genom att välja ett program med låg risk med en liten användar bas.
- När fler arbets belastningar är online förändras riskerna vid varje version. Nya appar går in i real tid och risker.
- När ett företag ser till att de första 10-20 programmen är online är risk profilen mycket annorlunda än när 1000th-programmen går in i molnet.

De till gångar som har samlats in i den traditionella, lokala egendom som troligen har ackumulerats över tid. Verksamhets-och IT-teamens mognads grad växer förmodligen på liknande sätt. Den parallella tillväxten kan tenderar att skapa några onödiga policy bagage.

Under en moln omvandling har både affärs-och IT-teamen möjlighet att återställa principerna och bygga nya med en vuxen tänkesätt.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-a-business-risk-mvp"></a>Vad är en Business risk MVP?

En **minimal livskraftig produkt** används ofta för att definiera den minsta enhet av något som kan producera ett materiell värde. I en affärs risks MVP börjar moln styrnings teamet med antagandet att vissa till gångar kommer att distribueras till en moln miljö vid en viss tidpunkt. Det är okänt vad dessa till gångar är för tillfället, och teamet kan vara osäker på vilka typer av data som lagras på dessa till gångar.

När du planerar för affärs risk kan moln styrnings teamet bygga för sämsta fall scenario och mappa varje möjlig princip till molnet. Att identifiera alla potentiella affärs risker för alla moln användnings scenarier kan dock ta lång tid och ansträngning, vilket kan fördröja implementeringen av styrningen till dina moln arbets belastningar. Detta rekommenderas inte, men är ett alternativ.

En MVP-metod kan till exempel göra det möjligt för teamet att definiera en start punkt och en uppsättning antaganden som skulle vara sanna för de flesta/alla till gångar. Den här Business riskfyllda MVP: er har stöd för inledande små skalnings-eller test moln distributioner och används sedan som bas för att gradvis identifiera och åtgärda nya risker när affärs behoven uppstår eller ytterligare arbets belastningar läggs till i din moln miljö. Med den här processen kan du tillämpa styrningar i moln införande processen.

Nedan följer några grundläggande exempel på affärs risker som kan ingå som en del av en MVP:

- Alla till gångar riskerar att tas bort (genom fel, misstag eller underhåll).
- Alla till gångar riskerar att generera för mycket utgifter.
- Alla till gångar kan komprometteras av svaga lösen ord eller oskyddade inställningar.
- Alla till gångar med öppna portar som exponeras för Internet är utsatta för angrepp.

Ovanstående exempel är avsedda att skapa MVP-affärsrisker som en teori. Den faktiska listan är unik för alla miljöer.
När Business risk MVP har upprättats kan de konverteras till [principer](./index.md) för att reparera varje risk.

<!-- markdownlint-enable MD026 -->

## <a name="incremental-risk-mitigation"></a>Stegvis risk minskning

I takt med att din organisation distribuerar fler arbets belastningar till molnet, kommer utvecklings team att använda ökande mängder moln resurser. Vid varje iteration skapas nya till gångar och mellanlagras. Vid varje version är arbets belastningar lättillgängliga för produktions befordran. Var och en av dessa cykler har möjlighet att introducera tidigare oidentifierade affärs risker.

Under förutsättning att en affärs risk MVP är start punkten för dina inledande moln implementerings ansträngningar kan styrningen parallellt med din ökande användning av moln resurser. När moln styrnings teamet arbetar parallellt med moln implementerings team, kan tillväxten av affärs risker åtgärdas när de identifieras, vilket ger en stabil kontinuerlig modell för utveckling av styrnings förfallon.

Varje mellanliggande till gång kan enkelt klassificeras efter risk. Dokument för data klassificering kan skapas eller skapas parallellt med mellanlagrings cykler. Risk profil och exponerings punkter kan också dokumenteras. Med tiden kan en mycket tydlig vy av affärs risker fokuseras över hela organisationen.

Med varje iteration kan moln styrnings teamet arbeta med moln strategi teamet för att snabbt kunna kommunicera nya risker, kompromisser och potentiella kostnader. Detta ger affärs deltagarna och IT-ledarna till partner i vuxen, välgrundade beslut. Dessa beslut meddelar sedan princip förfallo tid. Vid behov ändras principen för att producera nya arbets objekt för förgrunden av kärn infrastruktur system. När ändringar av mellanlagrade system krävs har moln implementerings teamen tillräckligt med tid för att göra ändringar, medan företaget testar de mellanlagrade systemen och utvecklar en användar implementerings plan.

Den här metoden minimerar risker, samtidigt som teamet kan förflytta sig snabbt. Det garanterar också att risker åtgärdas och löses före distributionen.

## <a name="next-steps"></a>Nästa steg

Lär dig hur du utvärderar risk tolerans under moln införande.

> [!div class="nextstepaction"]
> [Utvärdera risk tolerans](./risk-tolerance.md)
