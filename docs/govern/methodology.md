---
title: Metod för moln styrning
description: Upprätta grundläggande förståelse för de metoder som används för molnstyrning i Cloud Adoption Framework.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/04/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 402ebf52583ae5e94de52057133990656d8009b5
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807095"
---
# <a name="cloud-governance-methodology"></a>Metod för moln styrning

Molnintegreringen är en resa, inte ett mål. Längsmed vägen finns det tydliga milstolpar och reella affärsvinster. Dock är det svårt att förutse det slutliga resultatet när företagets resa inleds. Molnstyrning gör resan säker och hjälper företaget att hålla rätt kurs.

Ramverket för moln införande tillhandahåller styrnings guider som beskriver upplevelsen av fiktiva företag, som baseras på de verkliga kundernas upplevelser. Varje guide följer kunden genom alla styrningsaspekter i molnimplementeringen.

## <a name="envision-an-end-state"></a>Föreställ dig ett slutresultat

En resa utan ett mål blir bara ett planlöst irrande. Det är viktigt att upprätta en stor del av slut läget innan du börjar med det första steget. Följande informationsgrafik kan fungera som en referensram för slutresultatet. Det är inte din start punkt, men det visar det potentiella målet.

![Informationsgrafik av Cloud Adoption Framework-styrningsmodellen](../_images/operational-transformation-govern-highres.png)

Cloud Adoption Framework-styrningsmodellen identifierar områden som är viktiga under resans gång. Varje område relaterar till olika typer av risker som företaget måste hantera i takt med att man implementerar fler molntjänster. I det här ramverket identifierar styrningsguiden åtgärder som molnstyrningsteamet måste vidta. De olika principerna i Cloud Adoption Framework-styrningsmodellen beskrivs utförligare under resans gång. De generella principerna är som följer:

**Företags principer:** Företags principer enhets styrning av molnet. Styrningsguiden fokuserar på specifika aspekter i företagsprincipen:

- **Affärs risker:** Identifiera och förstå företags risker.
- **Princip och efterlevnad:** Att konvertera risker till princip satser som stöder eventuella krav på efterlevnad.
- **Processer:** Se till att de angivna principerna efterlevs.

**Fem ämnes områden i moln styrning:** Dessa ämnes områden har stöd för företags principer. Varje område skyddar företaget mot potentiella fallgropar:

- Kostnadshantering
- Grundläggande säkerhet
- Resurskonsekvens
- Grundläggande identitet
- Distributionsacceleration

Företagsprinciper fungerar i grunden som ett tidigt varningssystem för att identifiera potentiella problem. Områdena skyddar företaget och hjälper till att hantera risker.

## <a name="grow-to-the-end-state"></a>Utvecklas mot slutresultatet

Eftersom styrningskraven förändras genom hela molnimplementeringsresan krävs en ny styrningsstrategi. Företag kan inte längre vänta på att ett litet team ska garantera absolut säkerhet genom hela resan *innan man tar det första steget*. Affärsresultat förväntas komma snabbare och smidigare. IT-styrningen måste också vara flexibel och hålla jämna steg med verksamhetens krav för att vara användbar under molnintegreringen och för att förhindra ”skugg-IT”.

En **inkrementell styrningsstrategi** kan främja detta. Vid inkrementell styrning krävs en liten uppsättning företagsprinciper, processer och verktyg för att upprätta en grund för implementeringen och styrningen. Den här grunden kallas för en **MVP (Minimum Viable Product)** . En MVP gör att styrningsteamet snabbt kan integrera styrning i implementeringar i hela implementeringslivscykeln. En MVP kan upprättas när som helst under molnimplementeringsprocessen. Det är dock en bra idé att anta en MVP så tidigt som möjligt.

Möjligheten att snabbt svara på föränderliga risker gör att molnstyrningsteamet kan arbeta på nya sätt. Molnstyrningsteamet kan samarbeta med molnstrategiteamet och bana vägen för molnimplementeringsteamen genom att staka ut riktningar och snabbt se till att riskerna som är associerade med implementeringsplanerna hanteras effektivt. Dessa JIT-styrningslager (Just-In-Time) kallas för **styrningsiterationer**. Med den här metoden ligger styrningsstrategiteamet steget före implementeringsteamen.

Följande diagram visar en enkel styrnings-MVP och tre styrningsiterationer. Under iterationerna definieras ytterligare företagsprinciper avsedda att hantera nya risker. Genom distributionsaccelerationsprocessen tillämpas sedan ändringarna i varje distribution.

![Exempel på inkrementell styrningsförbättring](../_images/govern/incremental-governance-example.png)

> [!NOTE]
> Styrning ersätter inte viktiga funktioner såsom säkerhet, nätverk, identitet, ekonomi, DevOps eller drift. Längs vägen förekommer interaktioner med och beroenden mellan medlemmar i de olika funktionerna. Dessa medlemmar bör ingå i molnstyrningsteamet för att påskynda beslut och åtgärder.

## <a name="next-steps"></a>Nästa steg

Använd verktyget Cloud adoption Framework [styrning](https://cafbaseline.com) för att bedöma din omvandlings resa och hjälpa dig att identifiera luckor i organisationen över sex viktiga domäner som definieras i ramverket.

> [!div class="nextstepaction"]
> [Utvärdera din omvandlings resa](./benchmark.md)
