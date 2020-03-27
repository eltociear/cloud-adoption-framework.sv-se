---
title: Skapa dina första Azure-prenumerationer
description: Börja ditt antagande av Azure genom att skapa dina första prenumerationer.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 4e2a538c91328e7153f7f5ed37d07b8dbbeb4ea0
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359834"
---
# <a name="create-your-initial-azure-subscriptions"></a>Skapa dina första Azure-prenumerationer

Starta ditt Azure-antagande genom att skapa en första uppsättning prenumerationer. Lär dig vilka prenumerationer du ska börja med baserat på dina ursprungliga krav.

## <a name="your-first-two-subscriptions"></a>Dina första två prenumerationer

Börja med att skapa två prenumerationer:

- Skapa en Azure-prenumeration som innehåller dina produktions arbets belastningar.
- Skapa en andra prenumeration som inte fungerar som utvecklings-och test miljö, med hjälp av ett [Azure dev/test-erbjudande](https://azure.microsoft.com/pricing/dev-test) för lägre prissättning.

![En första prenumerations modell som visar nycklar bredvid rutor med etiketten "produktion" och "ej produktion"](../../_images/ready/initial-subscription-model.png)

Den här metoden har många fördelar:

- Genom att använda separata prenumerationer för produktions-och produktions miljöer skapas en gräns som gör hanteringen av dina resurser enklare och säkrare.
- Azure har speciella erbjudanden för utveckling och testning av prenumerationer för arbets belastningar som inte är för produktion. Dessa erbjudanden ger rabatterade priser på Azure-tjänster och program varu licenser.
- Dina produktions-och distributions miljöer kommer förmodligen att ha olika uppsättningar av Azure-principer. Genom att använda separata prenumerationer blir det enkelt att tillämpa varje distinkt princip på prenumerations nivån.
- Du kan tillåta vissa typer av Azure-resurser i din prenumeration för inte produktion i testnings syfte. Du kan aktivera dessa resurs leverantörer i din prenumeration utan produktion utan att göra dem tillgängliga i din produktions miljö.
- Du kan använda dev/test-prenumerationer som isolerade sandbox-miljöer. Med de här sand lådorna kan administratörer och utvecklare snabbt bygga upp och riva ned hela uppsättningar av Azure-resurser. Den här isoleringen kan också hjälpa till med dataskydd och säkerhetsproblem.
- De tröskelvärden för acceptabla kostnader som du definierar varierar förmodligen mellan produktions-och dev-och test prenumerationer.

## <a name="sandbox-subscriptions"></a>Sandbox-prenumerationer

Om du har nyskapande mål som en del av din strategi för moln införande bör du överväga att skapa en eller flera sandbox-prenumerationer. Du kan använda säkerhets principer för att hålla dessa test prenumerationer isolerade från produktions-och produktions miljöerna. Användare kan enkelt experimentera med Azure-funktioner i dessa isolerade miljöer. Använd ett Azure dev/test-erbjudande för att skapa dessa prenumerationer.

![En första prenumerations modell som visar nycklar bredvid rutor som är märkta med "produktion", "ej produktion" och "sand boxar"](../../_images/ready/initial-subscription-model-with-sandboxes.png)

## <a name="shared-services-subscription"></a>Prenumeration på delade tjänster

Om du planerar att **ha fler än 1 000 virtuella datorer eller beräknings instanser i molnet inom 24 månader**, skapar du en annan Azure-prenumeration som värd för delade tjänster. Detta förbereder dig i förväg för att stödja din företags arkitektur för slutanvändare.

![En första prenumerations modell som visar nycklar bredvid rutorna "produktion" och "delade tjänster"](../../_images/ready/initial-subscription-model-with-shared-services.png)

## <a name="next-steps"></a>Nästa steg

Granska orsakerna till varför du kanske vill [skapa ytterligare Azure-prenumerationer](./scale-subscriptions.md) för att uppfylla dina krav.

> [!div class="nextstepaction"]
> [Skapa ytterligare prenumerationer för att skala din Azure-miljö](./scale-subscriptions.md)
