---
title: Identitets bas mått, indikatorer och risk tolerans
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Identitets bas mått, indikatorer och risk tolerans
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: ad0b06cad7aefc70eea6366eb9ef2b5844c871a6
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026794"
---
# <a name="identity-baseline-metrics-indicators-and-risk-tolerance"></a>Identitets bas mått, indikatorer och risk tolerans

Den här artikeln är avsedd att hjälpa dig att kvantifiera affärs risk toleransen när det gäller identitets bas linjen. Genom att definiera mått och indikatorer kan du skapa ett affärs ärende för att göra en investering som förfaller i disciplinen för identitets bas linjen.

## <a name="metrics"></a>Mått

Identitets bas linjer fokuserar på att identifiera, autentisera och auktorisera individer, grupper av användare eller automatiserade processer och ge dem lämplig åtkomst till resurser i dina moln distributioner. Som en del av din riskanalys vill du samla in data som är relaterade till dina identitets tjänster för att avgöra hur mycket risker du möter och hur viktiga investeringar i identitets styrningen är till dina planerade moln distributioner.

Följande är exempel på användbara mått som du bör samla för att utvärdera risk tolerans inom identitets bas linjen:

- **Identitets systemets storlek.** Totalt antal användare, grupper eller andra objekt som hanteras via dina identitets system.
- **Övergripande storlek på infrastruktur för katalog tjänster.** Antal katalog skogar, domäner och innehavare som används av din organisation.
- **Beroende av äldre eller lokala autentiseringsmekanismer.** Antal arbets belastningar som är beroende av äldre autentiseringsmekanismer eller Multi-Factor Authentication-tjänster från tredje part.
- **Omfattningen av moln distributions katalog tjänster.** Antal katalog skogar, domäner och klienter som du har distribuerat till molnet.
- **Cloud-distribuerade Active Directory-servrar.** Antalet Active Directory-servrar som distribuerats till molnet.
- **Cloud-distribuerade organisationsenheter.** Antalet Active Directory organisationsenheter (OU) som distribuerats till molnet.
- **Federationens omfattning.** Antal identitets bas system som är federerade med din organisations system.
- **Utökade användare.** Antal användar konton med utökad åtkomst till resurser eller hanterings verktyg.
- **Användning av rollbaserad åtkomst kontroll.** Antal prenumerationer, resurs grupper eller enskilda resurser som inte hanteras via rollbaserad åtkomst kontroll (RBAC).
- **Autentiserings anspråk.** Antalet lyckade och misslyckade autentiseringsförsök för användare.
- **Authorization-anspråk.** Antalet lyckade och misslyckade försök för användare att komma åt resurser.
- **Komprometterade konton.** Antal användar konton som har komprometterats.

## <a name="risk-tolerance-indicators"></a>Risk tolerans indikatorer

Risker som rör identitets bas linjen är i stort sett relaterade till komplexiteten i organisationens identitets infrastruktur. Om alla användare och grupper hanteras med hjälp av en enda katalog eller en molnbaserad identitets leverantör med minimal integrering med andra tjänster, är risk nivån sannolikt liten. I takt med att dina affärs behov växer kan dina identitets bas system behöva stöd för mer komplicerade scenarier, till exempel flera kataloger som stöder din interna organisation eller federation med externa identitets leverantörer. När de här systemen blir mer komplexa ökar risken.

I det tidiga skedet av moln införande arbetar du med IT-säkerhetsteamet och affärs intressenterna för att identifiera [affärs risker](./business-risks.md) som är relaterade till identiteten. ta sedan reda på en acceptabel bas linje för identitets risk tolerans. Det här avsnittet av moln implementerings ramverket innehåller exempel, men detaljerade risker och bas linjer för ditt företag eller distributioner kan vara olika.

När du har en bas linje kan du fastställa de lägsta benchmark-värden som representerar en oacceptabel ökning av dina identifierade risker. Dessa riktmärken fungerar som utlösare för när du behöver vidta åtgärder för att åtgärda dessa risker. Här följer några exempel på hur identiteter som är relaterade till statistik, till exempel de som beskrivs ovan, kan motivera en ökad investering i identitets bas linjen.

- **Utlösare för användar konto nummer.** Ett företag med mer än _x_ -användare, grupper eller andra objekt som hanteras i dina identitets system kan dra nytta av investeringar i identitets bas disciplinen för att säkerställa en effektiv styrning över ett stort antal konton.
- **Lokal identitet beroende utlösare.** Ett företag som planerar att migrera arbets belastningar till molnet som kräver äldre autentiserings-eller multifaktorautentisering bör investera i identitets bas linjen för att minska riskerna som rör omfabriker eller ytterligare moln infrastruktur distribution.
- **Katalog tjänsters komplexitets utlösare.** Ett företag som underhåller mer än _x_ -nummer of_ enskilda skogar, domäner eller katalog klienter bör investera i identitets bas linjen för att minska riskerna med konto hantering och de effektivitets problem som rör flera användare autentiseringsuppgifterna sprids över flera system.
- **Utlösare för molnbaserade katalog tjänster.** Ett företag som är värd för _x_ -Active Directory Server (virtuella datorer) som finns i molnet, eller har _x_ organisationsenheter (OU) som hanteras på dessa molnbaserade servrar, kan dra nytta av investeringar i identitets bas disciplinen för att optimera integrering med alla lokala eller andra externa identitets tjänster.
- **Federations utlösare.** Ett företag som implementerar identitets Federation med _x_ externa identitets bas linje system kan dra nytta av investeringar i identitets bas disciplinen för att säkerställa konsekvent organisations policy över Federations medlemmar.
- **Utökad åtkomst utlösare.** Ett företag med mer än _x%_ av användare med förhöjd behörighet till hanterings verktyg och resurser bör överväga att investera i identitets bas disciplinen för att minimera risken för oavsiktlig överetablering av åtkomst till användare.
- **RBAC-utlösare.** Ett företag med under _x%_ av resurser som använder rollbaserad åtkomst kontroll metoder bör överväga att investera i identitets bas disciplinen för att identifiera optimerade sätt att tilldela användar åtkomst till resurser.
- **Autentiserings haveri utlösare.** Ett företag där autentiseringsfel representerar mer än _x%_ av försöken bör investera i identitets bas punkten för att säkerställa att autentiseringsmetoder inte är under externa angrepp och att användarna kan använda autentiseringsmetoderna Bra.
- **Utlösa auktoriseringsfel.** Ett företag där åtkomst försök nekas mer än _x%_ av tiden bör investera i identitets bas punkten för att förbättra programmet och uppdatering av åtkomst kontroller och identifiera potentiellt skadliga åtkomst försök.
- **Komprometterad konto utlösare.** Ett företag med mer än _x_ komprometterade konton bör investera i bas linjen för identitets bas linjer för att förbättra hållfastheten och säkerheten för autentiseringsmekanismer och förbättra mekanismer för att åtgärda risker som rör komprometterade konton.

De exakta mått och utlösare som du använder för att mäta risk toleransen och nivån av investering i identitets bas linjen är specifika för din organisation, men exemplen ovan bör fungera som en användbar bas för diskussioner i din organisation för moln styrning.

## <a name="next-steps"></a>Nästa steg

Använda [mallen för moln hantering](./template.md), dokument mått och tolerans indikatorer som överensstämmer med den aktuella moln implementerings planen.

Granska exempel på bas linje principer för identitet som utgångs punkt för att utveckla principer som åtgärdar specifika affärs risker som överensstämmer med dina moln implementerings planer.

> [!div class="nextstepaction"]
> [Granska exempel principer](./policy-statements.md)
