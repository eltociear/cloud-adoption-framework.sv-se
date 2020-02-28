---
title: Metoder för att planera för digital egendom
description: Förstå egenskaperna och kraven för top-down arbets belastnings driven, till gångs driven eller stegvisa metoder för planering av digital egendom.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: governance
ms.openlocfilehash: f2a589844b4564bb787db0efe4d796b7e5576309
ms.sourcegitcommit: 10637acba8c857a6f5aa8c4a80c0649903f60402
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/28/2020
ms.locfileid: "78170045"
---
# <a name="approaches-to-digital-estate-planning"></a>Metoder för att planera för digital egendom

Planering av elektronisk fastighets plan kan ta flera formulär beroende på de resultat och den befintliga egendomens storlek. Det finns olika metoder som du kan vidta. Det är viktigt att ställa in förväntningar avseende metoden tidigt i planerings cykler. Oklar förväntningar leder ofta till fördröjningar som är kopplade till ytterligare insamlings övningar för inventering. Den här artikeln beskriver tre metoder för analys.

## <a name="workload-driven-approach"></a>Arbets belastnings driven metod

Den bästa bedömnings metoden utvärderar säkerhets aspekter. Säkerhet omfattar kategorisering av data (hög, medel eller låg inverkan på företaget), efterlevnad, suveränitet och säkerhets risk krav. Den här metoden utvärderar arkitektur komplexitet på hög nivå. Den utvärderar aspekter som autentisering, data struktur, latens krav, beroenden och förväntad för program.

Den uppifrån och ned-metoden mäter också programmets operativa krav, till exempel service nivåer, integrering, underhålls fönster, övervakning och insikter. När alla dessa aspekter har analyser ATS och beaktats, vilket resulterande Poäng som återspeglar den relativa svårigheten att migrera det här programmet till varje moln plattform: IaaS, PaaS och SaaS.

Dessutom utvärderar utvärderingen de finansiella fördelarna med programmet, till exempel drift effektivitet, TCO, avkastning på investeringar och andra lämpliga finansiella mått. Utvärderingen undersöker också säsongs beroende för programmet (t. ex. finns det år då efter frågan har uppnåddes?) och total beräknings belastning.

Den tittar också på de typer av användare som den har stöd för (vardaglig/expert, alltid/ibland inloggad) och nödvändig skalbarhet och elastiskhet. Slutligen är utvärderingen klar genom att undersöka verksamhets kontinuitet och återhämtnings krav, samt beroenden för att köra programmet om det skulle uppstå ett avbrott i tjänsten.

> [!TIP]
> Den här metoden kräver intervjuer och anecdotal feedback från affärs-och teknik intressenter. Tillgänglighet för viktiga individer är den största risken för tids inställning. Anecdotal-karaktären hos data källorna gör det svårare att skapa korrekta kostnads-eller tids uppskattningar. Planera scheman i förväg och validera eventuella data som samlas in.

## <a name="asset-driven-approach"></a>Till gångs driven metod

Den till gångs drivna metoden tillhandahåller en plan som baseras på till gångar som stöder ett program för migrering. I den här metoden hämtar du statistik användnings data från en konfigurations hanterings databas (CMDB) eller andra verktyg för infrastruktur utvärdering.

Den här metoden förutsätter vanligt vis en IaaS modell för distribution som en bas linje. I den här processen utvärderar analysen attributen för varje till gång: minne, antal processorer (processor kärnor), lagrings utrymme för operativ system, data enheter, nätverkskort (NIC), IPv6, utjämning av nätverks belastning, klustring, operativ system version, databas version (vid behov), domäner som stöds och komponenter från tredje part eller program varu paket, bland annat. De till gångar som du har inventerat i den här metoden är sedan justerade med arbets belastningar eller program för gruppering och beroende mappning.

> [!TIP]
> Den här metoden kräver en omfattande källa för statistik användnings data. Den tid som krävs för att genomsöka inventeringen och samla in data är den största risken för tids fördröjning. Data källorna på låg nivå kan sakna beroenden mellan till gångar eller program. Planera för att genomsöka lagret minst en månad. Verifiera beroenden före distributionen.

## <a name="incremental-approach"></a>Stegvis metod

Vi föreslår starkt en stegvis metod, eftersom vi gör för många processer i moln implementerings ramverket. När det gäller digital fastighets planering som motsvarar en Multiphase process:

- **Ursprunglig kostnads analys:** Om ekonomisk validering krävs börjar du med en till gångs driven metod, som beskrivs ovan, för att få en inledande kostnads beräkning för hela den digitala fastigheten, utan någon rationalisering. Detta upprättar en benchmark för värsta fall scenario.

- **Planera migrering:** När du har monterat ett moln strategi team skapar du en första migrering genom att använda en arbets belastnings driven metod som baseras på deras kollektiva kunskaper och begränsade från intressenter-intervjuer. Den här metoden skapar snabbt en förenklad arbets belastnings utvärdering för att utveckla samarbetet.

- **Versions planering:** Vid varje version rensas den återstående migreringen och prioriteras för att fokusera på den mest relevanta företags påverkan. Under den här processen väljs nästa fem till tio arbets belastningar som prioriterade versioner. I det här läget investerar moln strategi teamet tiden för att slutföra en fullständig arbets belastnings driven metod. Den här utvärderingen försenas tills en version justeras bättre på tiden för intressenter. Dessutom försenas investeringen i fullständig analys tills företaget börjar se resultatet från tidigare ansträngningar.

- **Körnings analys:** Innan du migrerar, säkerhetskopierar eller replikerar en till gång kan du utvärdera den både individuellt och som en del av en samlad version. I det här läget kan data från den inledande till gångs metoden granskas för att säkerställa korrekt storlek och operativa begränsningar.

> [!TIP]
> Den här stegvisa metoden möjliggör effektiviserad planering och snabba resultat. Det är viktigt att alla parter som berörs förstår tillvägagångs sättet för försenade besluts fattande. Det är lika viktigt att antaganden som görs i varje steg dokumenteras för att undvika att information går förlorad.

## <a name="next-steps"></a>Nästa steg

När du har valt en metod kan inventeringen samlas in.

> [!div class="nextstepaction"]
> [Samla in inventerings data](./inventory.md)
