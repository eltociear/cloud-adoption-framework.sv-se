---
title: Definiera företags princip för moln styrning
description: Lär dig hur du etablerar en princip för att avspegla och åtgärda risker.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 92c04d53e59d8876291794c5da74104ec62412a9
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806058"
---
# <a name="define-corporate-policy-for-cloud-governance"></a>Definiera företags princip för moln styrning

När du har analyserat de kända riskerna och de relaterade risk toleranserna för din organisations moln omvandlings resa, är nästa steg att upprätta en princip som uttryckligen kommer att åtgärda dessa risker och definiera de steg som krävs för att åtgärda dem när det är möjligt.

<!-- markdownlint-disable MD026 -->

## <a name="how-can-corporate-it-policy-become-cloud-ready"></a>Hur kan företagets IT-policy göras redo för molnet?

Inom traditionell styrning och inkrementell styrning skapar företagspolicy arbetsdefinitionen av styrning. De flesta IT-styrningsåtgärder syftar till att implementera teknik för att övervaka, framtvinga, driva och automatisera dessa företagspolicyer. Moln styrning bygger på liknande koncept.

![Företags styrning och styrnings discipliner](../../_images/operational-transformation-govern-highres.png)

*Bild 1 – Företagsstyrning och styrningsområden.*

Bilden ovan illustrerar förhållandet mellan affärs risk, principer och efterlevnad, samt övervakning och verk ställande av mekanismer som behöver samverka som en del av din styrnings strategi. Med de fem disciplinerna i moln styrning kan du hantera dessa interaktioner och inse din strategi.

Molnstyrning är resultatet av ett kontinuerligt implementeringsarbete över tid, eftersom en långvarig omvandling inte sker på en dag. Försök att leverera en komplett molnstyrning innan viktiga ändringar av företagspolicy har åtgärdats med hjälp av en snabb och aggressiv metod ger sällan önskat resultat. Vi rekommenderar i stället en stegvis metod.

Vad är det som skiljer sig om ett ramverk för moln införande är inköps cykeln och kan aktivera en äkta transformering. Eftersom det inte finns ett stort köp krav för kapital utgifter kan ingenjörerna börja experimentera och vidta tidigare. I de flesta företagskulturer kan eliminering av kapitalinvesteringar som hindrar implementering leda till kortare feedbackloopar, organisk tillväxt och inkrementellt genomförande.

Övergången till molnimplementering kräver en förändring i styrningen. I många organisationer möjliggör omvandling av företagspolicy förbättrad styrning och bättre efterlevnad via inkrementella policyändringar och automatiserat framtvingande av dessa ändringarna, som drivs av nyligen definierade funktioner som du konfigurerar med din molntjänstleverantör.

<!-- markdownlint-enable MD026 -->

## <a name="review-existing-policies"></a>Granska befintliga principer

Eftersom styrning är en pågående process bör policyn regelbundet granskas med IT-personal och intressenter för att säkerställa att resurser som finns i molnet fortsätter att upprätthålla efterlevnaden av företagets övergripande mål och krav. Din förståelse av nya risker och godtagbar tolerans kan ge upphov till en [granskning av befintliga policyer](./cloud-policy-review.md) i syfte att fastställa den styrningsnivå som krävs och är lämplig för organisationen.

> [!TIP]
> Om din organisation använder leverantörer eller andra betrodda affärs partner, kan en av de största affärs riskerna som du anser vara brist på efterlevnad av [reglernas efterlevnad](./regulatory-compliance.md) av dessa externa organisationer. Den här risken kan ofta inte åtgärdas och kan i stället kräva en strikt efterlevnad av krav från alla parter. Se till att du har identifierat och förstått eventuella krav på tredje part innan du påbörjar en princip granskning.

## <a name="create-cloud-policy-statements"></a>Skapa moln princips instruktioner

Molnbaserade IT-principer upprättar krav, standarder och mål som din IT-personal och automatiserade system behöver stöd för. Princip beslut är en primär faktor i din [moln arkitekturs design](./governance-alignment.md) och hur du implementerar [principerna](./processes.md)för att följa dessa processer.

Enskilda moln princips instruktioner är rikt linjer för att åtgärda specifika risker som identifieras under riskbedömningen. Även om dessa principer kan integreras i din större dokumentation om företags principer, kan moln princips instruktioner som diskuteras i moln implementerings ramverket vara en mer koncis Sammanfattning av riskerna och planer för att hantera dem. Varje definition bör innehålla dessa delar av informationen:

- **Affärs risk:** En sammanfattning av risken som den här principen kommer att åtgärda.
- **Princip instruktion:** En kortfattad förklaring av princip kraven och målen.
- **Design eller teknisk vägledning:** Rekommendationer, specifikationer eller annan vägledning för att stödja och genomdriva den här principen som IT-team och utvecklare kan använda när de utformar och skapar sina moln distributioner.

Om du behöver hjälp med att definiera principer kan du läsa igenom de [styrnings discipliner](../governance-disciplines.md) som introducerades i styrnings avsnittet Översikt. Artiklarna för var och en av dessa ämnes områden innehåller exempel på vanliga affärs risker som påträffas när du flyttar till molnet och exempel principerna som används för att åtgärda dessa risker (till exempel kan du se Cost Management disciplins [definitioner för exempel principer](../cost-management/policy-statements.md)).

## <a name="incremental-governance-and-integrating-with-existing-policy"></a>Stegvis styrning och integrering med befintlig policy

Planerade tillägg i din moln miljö bör alltid vara testats för att följa den befintliga principen och principen har uppdaterats för att det ska uppstå problem som inte redan omfattas. Du bör också utföra regelbunden [granskning av moln principer](./cloud-policy-review.md) för att se till att moln principen är uppdaterad och synkroniserad med en ny företags policy.

Behovet av att integrera moln principen med dina äldre IT-principer beror i stort sett på hur lång tid det tar för dina moln styrnings processer och storleken på din moln egendom. Se artikeln om [stegvis styrning och policy MVP](./index.md) för en bredare diskussion om hur du hanterar princip integrering under din moln omvandling.

## <a name="next-steps"></a>Nästa steg

När du har definierat principerna kan du skapa en arkitektur design guide för IT-personal och utvecklare med åtgärds bara vägledning.

> [!div class="nextstepaction"]
> [Anpassa din styrnings design guide med företags policy](./governance-alignment.md)
