---
title: Metod för moln styrning
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Upprätta grundläggande förståelse för de metoder som används för molnstyrning i Cloud Adoption Framework.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/04/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: cc4567495d60f76be760d532dc16a66274834396
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71029268"
---
# <a name="cloud-governance-methodology"></a>Metod för moln styrning

Molnintegreringen är en resa, inte ett mål. Längsmed vägen finns det tydliga milstolpar och reella affärsvinster. Dock är det svårt att förutse det slutliga resultatet när företagets resa inleds. Molnstyrning gör resan säker och hjälper företaget att hålla rätt kurs.

Ramverket för moln införande tillhandahåller styrnings guider som beskriver upplevelsen av fiktiva företag, som baseras på de verkliga kundernas upplevelser. Varje guide följer kunden genom alla styrningsaspekter i molnimplementeringen.

## <a name="envision-an-end-state"></a>Föreställ dig ett slutresultat

En resa utan ett mål blir bara ett planlöst irrande. Det är viktigt att formulera en övergripande vision av slutresultatet innan det första steget tas. Följande informationsgrafik kan fungera som en referensram för slutresultatet. Det är inte startpunkten, men visar det potentiella målet.

![Informationsgrafik av Cloud Adoption Framework-styrningsmodellen](../_images/operational-transformation-govern-highres.png)

Cloud Adoption Framework-styrningsmodellen identifierar områden som är viktiga under resans gång. Varje område relaterar till olika typer av risker som företaget måste hantera i takt med att man implementerar fler molntjänster. I det här ramverket identifierar styrningsguiden åtgärder som molnstyrningsteamet måste vidta. De olika principerna i Cloud Adoption Framework-styrningsmodellen beskrivs utförligare under resans gång. De generella principerna är som följer:

**Företagsprinciper:** Företagsprinciperna driver på molnstyrningen. Styrningsguiden fokuserar på specifika aspekter i företagsprincipen:

- **Affärsrisker:** Identifiera och förstå affärsrisker.
- **Principer och efterlevnad:** Förvandla risker till principformuleringar som har stöd för alla slags efterlevnadskrav.
- **Processer:** Säkerställa efterlevnad av de fastställda principerna.

**Fem molnstyrningsområden:** Dessa områden relaterar till företagsprinciperna. Varje område skyddar företaget mot potentiella fallgropar:

- Cost Management
- Grundläggande säkerhet
- Resurskonsekvens
- Grundläggande identitet
- Distributionsacceleration

Företagsprinciper fungerar i grunden som ett tidigt varningssystem för att identifiera potentiella problem. Områdena skyddar företaget och hjälper till att hantera risker.

## <a name="grow-to-the-end-state"></a>Utvecklas mot slutresultatet

Eftersom styrningskraven förändras genom hela molnimplementeringsresan krävs en ny styrningsstrategi. Företag kan inte längre vänta på att ett litet team ska garantera absolut säkerhet genom hela resan *innan man tar det första steget*. Affärsresultat förväntas komma snabbare och smidigare. IT-styrningen måste också vara flexibel och hålla jämna steg med verksamhetens krav för att vara användbar under molnintegreringen och för att förhindra ”skugg-IT”.

En **inkrementell styrningsstrategi** kan främja detta. Vid inkrementell styrning krävs en liten uppsättning företagsprinciper, processer och verktyg för att upprätta en grund för implementeringen och styrningen. Den här grunden kallas för en **MVP (Minimum Viable Product)** . En MVP gör att styrningsteamet snabbt kan integrera styrning i implementeringar i hela implementeringslivscykeln. En MVP kan upprättas när som helst under molnimplementeringsprocessen. Det är dock en bra idé att införa en MVP så tidigt som möjligt.

Möjligheten att snabbt svara på föränderliga risker gör att molnstyrningsteamet kan arbeta på nya sätt. Molnstyrningsteamet kan samarbeta med molnstrategiteamet och bana vägen för molnimplementeringsteamen genom att staka ut riktningar och snabbt se till att riskerna som är associerade med implementeringsplanerna hanteras effektivt. Dessa JIT-styrningslager (Just-In-Time) kallas för **styrningsiterationer**. Med den här metoden ligger styrningsstrategiteamet steget före implementeringsteamen.

Följande diagram visar en enkel styrnings-MVP och tre styrningsiterationer. Under iterationerna definieras ytterligare företagsprinciper avsedda att hantera nya risker. Genom distributionsaccelerationsprocessen tillämpas sedan ändringarna i varje distribution.

![Exempel på inkrementell styrningsförbättring](../_images/govern/incremental-governance-example.png)

> [!NOTE]
> Styrning ersätter inte viktiga funktioner såsom säkerhet, nätverk, identitet, ekonomi, DevOps eller drift. Längs vägen förekommer interaktioner med och beroenden mellan medlemmar i de olika funktionerna. Dessa medlemmar bör ingå i molnstyrningsteamet för att påskynda beslut och åtgärder.

## <a name="next-steps"></a>Nästa steg

Använd verktyget Cloud adoption Framework [styrning](https://cafbaseline.com) för att bedöma din omvandlings resa och hjälpa dig att identifiera luckor i organisationen över sex viktiga domäner som definieras i ramverket.

> [!div class="nextstepaction"]
> [Utvärdera din omvandlings resa](./benchmark.md)
