---
title: Förbättringar av säkerhets bas linje disciplin
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Förbättringar av säkerhets bas linje disciplin
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 8ad6b84a67bb81459fbd78ebe413a93c1a58e099
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027444"
---
# <a name="security-baseline-discipline-improvement"></a>Förbättringar av säkerhets bas linje disciplin

Säkerhets bas linje disciplin fokuserar på sätt att etablera principer som skyddar nätverket, till gångar och viktigast av de data som kommer att finnas i en moln leverantörs lösning. Inom fem ämnes områden i moln styrning innehåller säkerhets bas linjen klassificering av den digitala fastigheten och data. Den innehåller också dokumentation om risker, affärs toleranser och strategier för minskning av säkerheten för data, till gångar och nätverk. Från ett tekniskt perspektiv omfattar detta även inblandning i beslut om [kryptering](../../decision-guides/encryption/index.md), [nätverks krav](../../decision-guides/software-defined-network/index.md), [hybrid identitets strategier](../../decision-guides/identity/index.md)och de [processer](./compliance-processes.md) som används för att utveckla principer för moln säkerhets bas linjen.

Den här artikeln beskriver några potentiella uppgifter som företaget kan delta i för att utveckla och mogna säkerhets bas linjen. Dessa uppgifter kan delas upp i planering, uppbyggnad, införande och drifts faser för implementering av en moln lösning, som sedan upprepas på att tillåta utveckling av en [stegvis metod för moln styrning](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Fyra faser i antagandet](../../_images/govern/adoption-phases.png)

*Figur 1 – implementerings faser för den stegvisa metoden för moln styrning.*

Det är omöjligt för något dokument att redovisa kraven i alla företag. I den här artikeln beskrivs de föreslagna minimi-och potentiella exempel aktiviteterna för varje fas i processens mognads process. Det första målet med dessa aktiviteter är att hjälpa dig att skapa en [policy MVP](../guides/index.md#an-incremental-approach-to-cloud-governance) och upprätta ett ramverk för stegvisa princip förbättringar. Ditt moln styrnings team måste bestämma hur mycket du ska investera i dessa aktiviteter för att förbättra funktionerna för styrning av säkerhets linjer.

> [!CAUTION]
> Varken de minsta eller potentiella aktiviteter som beskrivs i den här artikeln är justerade med specifika företags principer eller krav för tredje parts efterlevnad. Den här vägledningen är utformad för att hjälpa till att under lätta de konversationer som kommer att leda till justering av båda kraven med en modell för moln styrning.

## <a name="planning-and-readiness"></a>Planering och beredskap

Den här fasen av styrnings mognads bryggor förenar indelningen mellan affärs resultat och insats bara strategier. Under den här processen definierar ledarskaps gruppen vissa mått, mappar dessa mått till den digitala egendomen och börjar planera den totala migreringen.

**Minsta antal föreslagna aktiviteter:**

- Utvärdera verktygskedjan alternativ för [säkerhets bas linjen](./toolchain.md) .
- Utveckla ett utkast till rikt linjer för arkitektur och distribuera till viktiga intressenter.
- Utbilda och involvera de personer och grupper som påverkas av rikt linjerna för arkitektur utveckling.
- Lägg till prioriterade säkerhets uppgifter i efter släpning för migreringen.

**Potentiella aktiviteter:**

- Definiera ett schema för data klassificering.
- Genomför en planerings process för digital egendom för att inventera de aktuella IT-resurserna som driver dina affärs processer och stöd åtgärder.
- Genomför en [princip granskning](../../govern/policy-compliance/cloud-policy-review.md) för att påbörja processen med att ställa befintliga säkerhets principer för företags IT och definiera MVP-principer som behandlar kända risker.
- Granska din moln plattforms säkerhets rikt linjer. För Azure finns dessa på [Microsofts plattform för tjänst förtroende](https://www.microsoft.com/trustcenter/stp/default.aspx).
- Ta reda på om din säkerhets bas linje princip innehåller en [livs cykel för säkerhets utveckling](https://www.microsoft.com/securityengineering/sdl).
- Utvärdera företags risker i nätverket, data och till gångar baserat på nästa till tre versioner och mäta din organisations tolerans för dessa risker.
- Granska Microsofts [främsta trender i cybersäkerhet](https://www.microsoft.com/security/operations/security-intelligence-report) -rapporten för att få en översikt över det aktuella säkerhets landskapet.
- Överväg att utveckla en säkerhets roll för [DevOps](https://www.microsoft.com/en-us/securityengineering/devsecops) i din organisation.

<!-- "en-us" location is required for the URL above. -->

## <a name="build-and-predeployment"></a>Bygg och för distribution

Det krävs flera tekniska och tekniska krav för att kunna migrera en miljö. Den här processen fokuserar på beslut, beredskap och kärn infrastrukturen som fortsätter med migreringen.

**Minsta antal föreslagna aktiviteter:**

- Implementera din [verktygskedjan för säkerhets bas linjer](./toolchain.md) genom att distribuera i en för distributions fas.
- Uppdatera dokument för arkitektur rikt linjer och distribuera till viktiga intressenter.
- Implementera säkerhets aktiviteter på den förväntade migreringen.
- Utveckla utbildningsmaterial och dokumentation, medvetenhets kommunikation, stimulans åtgärder och andra program för att hjälpa att använda användar införande.

**Potentiella aktiviteter:**

- Fastställ organisationens [krypterings](../../decision-guides/encryption/index.md) strategi för data som hanteras av molnet.
- Utvärdera din moln distributions [identitets](../../decision-guides/identity/index.md) strategi. Bestäm hur din molnbaserade identitets lösning ska fungera eller integreras med lokala identitets leverantörer.
- Fastställ nätverks gräns principer för din [SDN-design (Software Defined Networking)](../../decision-guides/software-defined-network/index.md) för att säkerställa säkra virtualiserade nätverksfunktioner.
- Utvärdera organisationens åtkomst principer med [lägsta behörighet](https://docs.microsoft.com/azure/active-directory/users-groups-roles/roles-delegate-by-task) och Använd uppgiftsbaserade roller för att ge åtkomst till vissa resurser.
- Tillämpa säkerhets-och övervaknings metoder för alla moln tjänster och virtuella datorer.
- Automatisera [säkerhets principer](../../decision-guides/policy-enforcement/index.md) där det är möjligt.
- Granska säkerhets bas linje policyn och Fastställ om du behöver ändra dina planer enligt rikt linjer för bästa praxis, till exempel de som beskrivs i [livs cykeln för säkerhets utveckling](https://www.microsoft.com/securityengineering/sdl).

## <a name="adopt-and-migrate"></a>Införa och migrera

Migrering är en stegvis process som fokuserar på förflyttning, testning och införande av program eller arbets belastningar i en befintlig digital egendom.

**Minsta antal föreslagna aktiviteter:**

- Migrera din [säkerhets bas linje verktygskedjan](./toolchain.md) från för distribution till produktion.
- Uppdatera dokument för arkitektur rikt linjer och distribuera till viktiga intressenter.
- Utveckla utbildningsmaterial och dokumentation, medvetenhets kommunikation, stimulans åtgärder och andra program för att hjälpa att använda användar införande.

**Potentiella aktiviteter:**

- Granska den senaste säkerhets bas linjen och hot informationen för att identifiera eventuella nya affärs risker.
- Mäta din organisations tolerans för att hantera nya säkerhets risker som kan uppstå.
- Identifiera avvikelser från principen och tillämpa korrigeringar.
- Justera säkerhets-och åtkomst kontroll automatiseringen för att säkerställa att den maximala principen efterlevs.
- Kontrol lera att de bästa metoderna som definierats under konstruktions-och för distributions faserna är korrekt utförda.
- Granska åtkomst principerna med minst behörighet och justera åtkomst kontroller för att maximera säkerheten.
- Testa säkerhets bas linjen verktygskedjan mot dina arbets belastningar för att identifiera och lösa eventuella sårbarheter.

## <a name="operate-and-post-implementation"></a>Drift och efter implementering

När omvandlingen är klar måste styrning och åtgärder vara aktiva för den naturliga livs cykeln för ett program eller en arbets belastning. Den här fasen av styrnings förfallo tid fokuserar på de aktiviteter som vanligt vis kommer efter att lösningen har implementerats och omvandlings cykeln börjar stabilisera sig.

**Minsta antal föreslagna aktiviteter:**

- Verifiera och förfina din [säkerhets bas linje verktygskedjan](./toolchain.md).
- Anpassa meddelanden och rapporter för att varna dig om potentiella säkerhets problem.
- Förfina rikt linjerna för arkitekturen för att vägleda framtida införande processer.
- Kommunicera och utbilda de berörda teamen regelbundet för att se till att det pågår rikt linjerna för arkitekturen.

**Potentiella aktiviteter:**

- Identifiera mönster och beteende för dina arbets belastningar och konfigurera övervaknings-och rapporterings verktyg för att identifiera och meddela dig om onormal aktivitet, åtkomst eller Resursanvändning.
- Uppdatera kontinuerligt dina övervaknings-och rapporterings principer för att identifiera de senaste säkerhets problemen, sårbarheter och attacker.
- Ha procedurer på plats för att snabbt stoppa obehörig åtkomst och inaktivera resurser som kan ha komprometterats av en angripare.
- Läs regelbundet över de senaste säkerhets metoderna och tillämpa rekommendationer för dina säkerhets principer, automatiserings-och övervaknings funktioner där det är möjligt.

## <a name="next-steps"></a>Nästa steg

Nu när du förstår begreppet Cloud Security styrning kan du gå vidare till Lär dig mer om [vilken vägledning för säkerhet och bästa metoder Microsoft tillhandahåller](./azure-security-guidance.md) för Azure.

> [!div class="nextstepaction"]
> [Lär dig mer om säkerhets vägledning för Azure](./azure-security-guidance.md)
> -[Introduktion till Azure Security](https://docs.microsoft.com/azure/security/azure-security)
> [Lär dig mer om loggning, rapportering och övervakning](../../decision-guides/logging-and-reporting/index.md)
