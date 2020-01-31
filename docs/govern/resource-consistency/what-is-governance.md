---
title: Vad är styrning av molnresurser?
description: Förklaring moln resurs styrning på Azure
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 9277bf82d9034108b478536a699f96918c38ae0d
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807282"
---
<!-- markdownlint-disable MD026 -->

# <a name="cloud-resource-governance"></a>Resurs styrning i molnet?

I [Hur fungerar Azure?](../../getting-started/what-is-azure.md)och du har lärt dig att Azure är en samling servrar och nätverks maskin vara som kör virtualiserad maskin vara och program vara för användarens räkning. Azure gör det möjligt för din organisations program utveckling och IT-avdelningar att bli flexibla genom att göra det enkelt att skapa, läsa, uppdatera och ta bort resurser efter behov.

Men även om obegränsad till resurser kan göra utvecklare mer flexibla kan det leda till oväntade kostnader. Till exempel kan ett utvecklings team godkännas för att distribuera en uppsättning resurser för testning men glömma att ta bort dem när testningen är klar. De här resurserna fortsätter att Periodisera kostnader trots att de inte längre är godkända eller nödvändiga.

Lösningen är resurs åtkomst styrning. **Styrning** är den ständiga processen för att hantera, övervaka och granska användningen av Azure-resurser för att uppfylla målen och kraven i din organisation.

<!-- markdownlint-disable MD034 -->

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE2ii94]

<!-- markdownlint-enable MD034 -->

Dessa krav är unika för varje organisation, vilket innebär att det inte är praktiskt att anpassa alla metoder för styrning. I stället är det upp till varje organisation att utforma sin styrnings modell med hjälp av Azures två huvudsakliga styrnings verktyg: **rollbaserad åtkomst kontroll (RBAC)** och **resurs princip**.

RBAC definierar roller och roller som definierar vilka åtgärder som tillåts för varje användare som tilldelats rollen. **Ägar** rollen tillåter till exempel alla åtgärder (skapa, läsa, uppdatera och ta bort) på en resurs, medan rollen **läsare** bara tillåter Läs åtgärder. Roller kan definieras brett och appliceras på många resurs typer, eller definieras mer restriktivt och tillämpas bara på några få resurs typer.

Resurs principer definierar regler för att skapa resurser. En resurs princip kan till exempel begränsa SKU: n för en virtuell dator till en viss förgodkännd storlek. En annan resurs princip kan framtvinga tillämpningen av en tagg för ett tilldelat kostnads ställe när begäran görs för att skapa resursen.

När du konfigurerar dessa verktyg är det viktigt att balansera styrning och organisationens rörlighet. Den mer restriktiva styrnings principen, desto mindre Agile är dina utvecklare och IT-anställda. En restriktiv styrnings princip kan kräva mer manuella steg som kräver att en utvecklare fyller i ett formulär eller skickar ett e-postmeddelande till en medlem i styrnings teamet för att skapa en resurs manuellt. Styrnings teamet har begränsad kapacitet och kan bli en Flask hals, vilket leder till att utvecklings teamen väntar på att deras resurser ska skapas, eller resurser som inte behöver resurser debiteras innan de tas bort.

## <a name="next-steps"></a>Nästa steg

Nu när du förstår begreppet moln resurs styrning kan du läsa mer om hur resurs åtkomst hanteras i Azure.

> [!div class="nextstepaction"]
> [Lär dig mer om resurs åtkomst i Azure](./resource-access-management.md)
