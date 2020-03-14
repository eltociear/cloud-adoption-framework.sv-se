---
title: Vägledning för företags testning under migrering
description: Lär dig hur företags testning används för att begära verifiering av att lösningens prestanda är i linje med förväntningar och inte hindrar affärs processer.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 675eda4aeb2109c21c2e3f47a100a985fd6e2861
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79311769"
---
# <a name="guidance-for-business-testing-uat-during-migration"></a>Vägledning för verksamhetstestning (UAT) under migrering

Acceptanstest för användare betraktas traditionellt som en IT-aktivitet, och kan under en affärsomvandling struktureras helt av IT-avdelningen. Ofta genomförs dock denna aktivitet effektivast som en affärsfunktion. IT stöder sedan denna affärsaktivitet genom att underlätta testning, utveckla testplaner och automatisera tester när så är möjligt. Även om IT ofta kan agera som ett surrogat för testning finns det ingen riktig ersättning för direkt observation av verkliga användare som försöker använda en ny lösning inom kontexten för en verktyg eller replikerad affärsprocess.

> [!NOTE]
> När automatiserad testning är gångbar är det ett mycket kraftfullare och kostnadseffektivare sätt att testa system. Dock fokuserar molnmigreringar främst på äldre system eller åtminstone stabila produktionssystem. Dessa system hanteras ofta inte av noggranna och väl underhållna automatiserade tester. Den här artikeln förutsätter att det inte finns sådana tester tillgängliga vid tidpunkten för migrering.

Efter automatiserad testning kommer testning av processen och teknikändringar av privilegierade användare. Privilegierade användare är personer som ofta kör en verklig process som kräver interaktion med ett teknikverktyg eller en uppsättning med verktyg. De kan representeras av en extern kund som använder en e-handelswebbplats för att införskaffa varor eller tjänster. Privilegierade användare kan även representeras av en grupp medarbetare som kör en affärsprocess, till exempel kundtjänst som hjälper kunder och spelar in sina upplevelser.

Målet med affärstestning är att begära validering från privilegierade användare för att intyga att den nya lösningen fungerar enligt förväntningarna och inte hindrar affärsprocesser. Om det målet inte uppfylls fungerar affärstestning som en feedbackloop som kan hjälpa till att definiera varför och hur arbetsbelastningen inte uppfyller förväntningarna.

## <a name="business-activities-during-business-testing"></a>Affärsaktiviteter under affärstestning

Under affärstestningen sköts den första iterationen manuellt och direkt med kunderna. Detta är den mest gedigna men även den mest tidsödande formen av feedbackloop.

- **Identifiera privilegierade användare.** Företaget har vanligtvis en bättre förståelse för de privilegierade användare som påverkas mest av en teknisk ändring.
- **Informera och förbereda privilegierade användare.** Se till att privilegierade användare förstår affärsmålen, önskade resultat och förväntade ändringar av affärsprocesser. Förbered dem och deras chefsstruktur för testningsprocessen.
- **Delta i tolkning av feedbackloopen.** Hjälp IT-personalen att förstå effekten av olika feedbackpunkter från privilegierade användare.
- **Klargöra processförändring.** När omvandling kan utlösa en ändring i affärsprocesser bör ändringen och eventuella efterföljande effekter kommuniceras.
- **Prioritera feedback.** Hjälp IT-teamet att prioritera feedback baserat på affärspåverkan.

Ibland kan IT använda analytiker eller produktägare som hanterar de beskrivna aktiviteterna för affärstestning. Dock rekommenderas företagsdeltagande starkt. Det leder sannolikt till gynnsamma affärsresultat.

## <a name="it-activities-during-business-testing"></a>IT-aktiviteter under affärstestning

IT fungerar som en av mottagarna av resultatet av affärstestning. De feedbackloopar som bildas vid affärstestning blir senare arbetsuppgifter som definierar teknisk förändring eller processändring. Som mottagare förväntas IT hjälpa till med själva testningen, insamling av feedback och hantering av resulterande tekniska åtgärder. De typiska aktiviteter som IT utför under affärstestning är:

- Tillhandahålla struktur och logistik för affärstestning.
- Underlätta testningen.
- Tillhandahålla verktyg och en process för att registrera feedback.
- Hjälpa företaget att prioritera och validera feedback.
- Utveckla planer för att agera utefter tekniska ändringar.
- Identifiera befintliga automatiserade tester som kan effektivisera testning som utförs av privilegierade användare.
- För ändringar som kan kräva upprepad distribution eller testning bör man undersöka testningsprocesser, definiera riktmärken och skapa automation för att ytterligare effektivisera testning som utförs av privilegierade användare.

## <a name="next-steps"></a>Nästa steg

I samband med affärstestning kan [optimering av migrerade tillgångar](./optimize.md) förbättra kostnader och prestanda för arbetsbelastningar.

> [!div class="nextstepaction"]
> [Prestandatesta och ändra storlek på molntillgångar](./optimize.md)
