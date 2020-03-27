---
title: Guide för IT Cloud Security readiness
description: Lär dig hur du förbereder IT (Chief information Security Office) för moln omvandling och stegvis styrning.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: dc82f4d8ad21bcbb9d36b00fbdad1f91d6d4ec2c
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80356947"
---
<!-- cSpell:ignore CISO -->

# <a name="ciso-cloud-readiness-guide"></a>IT Cloud readiness guide

Microsofts vägledning som ramverket för moln införande är inte placerad för att fastställa eller vägleda de unika säkerhets begränsningarna i tusentals företag som stöds av den här dokumentationen. När du flyttar till molnet är rollen som säkerhets tjänsteman eller IT (Chief information Security) inte supplanted av moln teknik. Det stämmer att IT och kontoret i IT blir mer kornigt och integrerat. Den här guiden förutsätter att läsaren är bekant med IT-processer och försöker att modernisera dessa processer för att aktivera moln omvandling.

Moln införande möjliggör tjänster som inte ofta beaktas i traditionella IT-miljöer. Självbetjänings-eller automatiserade distributioner utförs ofta av program utveckling eller andra IT-team som inte traditionellt justeras till produktions distributionen. I vissa organisationer har affärs komponenter liknande funktioner för självbetjäning. Detta kan utlösa nya säkerhets krav som inte behövs i den lokala världen. Centraliserad säkerhet är mer utmanande, och säkerheten blir ofta ett delat ansvar för verksamheten och IT-kulturen. Den här artikeln hjälper dig att förbereda en IT för den metoden och delta i stegvisa styrningar.

<!-- markdownlint-disable MD026 -->

## <a name="how-can-a-ciso-prepare-for-the-cloud"></a>Hur kan en IT-chef förbereda sig för molnet?

Precis som de flesta principer är principerna för säkerhet och styrning inom en organisation att växa ekologiskt. När säkerhets incidenter sker kan de forma en princip för att informera användarna och minska sannolikheten för upprepade förekomster. Även om det är naturligt skapar den här metoden princip överdriven storlek och tekniska beroenden. Moln omvandlings resan skapar en unik möjlighet att modernisera och återställa principer. När du förbereder en omvandlings resa kan IT skapa omedelbara och mätbara värden genom att betjäna den primära från intressenter i en [princip granskning](./cloud-policy-review.md).

I en sådan granskning är rollen för IT att skapa en säker balans mellan begränsningarna i befintliga principer/efterlevnad och den förbättrade säkerhets position för moln leverantörer. Det kan ta många formulär att mäta det här förloppet, ofta mäts det i antalet säkerhets principer som kan avlastas på ett säkert sätt till moln leverantören.

**Överföring av säkerhets risker:** När tjänster flyttas till infrastruktur som en tjänst (IaaS) som värd modeller, antar företaget mindre direkt risk för maskin varu etablering. Risken tas inte bort, i stället överförs den till moln leverantören. Om en moln leverantörs metod för maskin varu etablering ger samma nivå av risk minskning, i en säker upprepnings bar process, tas risken för maskin varu etablering bort från företagets IT-ansvar och överförs till molnet CSP. Detta minskar det övergripande säkerhets risk företaget som den ansvarar för hantering, även om risken fortfarande bör spåras och granskas regelbundet.

När lösningar flyttas ytterligare "upp stack" för att införliva PaaS-(Platform as a Service) eller SaaS-modeller (program vara som en tjänst) kan ytterligare risker undvikas eller överföras. När risken har flyttats till en moln leverantör kan kostnaden för att köra, övervaka och verkställa säkerhets principer eller andra principer för efterlevnad också vara säker.

**Tillväxt tänkesätt:** Ändringen kan vara skrämmande för både affärs-och teknik implementerare. När IT leder till en tillväxt tänkesätt i en organisation har vi funnit att dessa naturliga oroliga har ersatts av ökad intresse för säkerhet och policy efterlevnad. Genom att följa en [princip granskning](./cloud-policy-review.md), en omvandlings resa eller enkla implementerings recensioner med en tillväxt tänkesätt, gör det möjligt för teamet att flytta snabbt men inte till kostnaden för en rättvis och hanterbar risk profil.

## <a name="resources-for-the-chief-information-security-officer"></a>Resurser för säkerhets tjänsteman för Chief information

Kunskap om molnet är grundläggande för att nå en [princip granskning](./cloud-policy-review.md) med en växande tänkesätt. Följande resurser kan hjälpa IT att bättre förstå säkerhets position för Microsofts Azure-plattform.

Säkerhets plattforms resurser:

- [Livs cykel för säkerhets utveckling, interna granskningar](https://www.microsoft.com/sdl)
- [Obligatorisk säkerhetsutbildning, bakgrunds kontroller](https://downloads.cloudsecurityalliance.org/star/self-assessment/StandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx)
- [Testning av inträngande, intrångs identifiering, DDoS, granskningar och loggning](https://www.microsoft.com/trustcenter/Security/AuditingAndLogging)
- [Tillstånds Data Center](https://www.microsoft.com/cloud-platform/global-datacenters), fysisk säkerhet, [säkert nätverk](https://docs.microsoft.com/azure/security/security-network-overview)
- [Microsoft Azure säkerhets svar i molnet (PDF)](https://aka.ms/SecurityResponsePaper)

Sekretess och kontroller:

- [Hantera dina data hela tiden](https://www.microsoft.com/trustcenter/Privacy/You-own-your-data)
- [Kontroll på data plats](https://www.microsoft.com/trustcenter/Privacy/Where-your-data-is-located)
- [Ge data åtkomst på dina villkor](https://www.microsoft.com/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms)
- [Svara på juridisk tillämpning](https://www.microsoft.com/trustcenter/Privacy/Responding-to-govt-agency-requests-for-customer-data)
- [Stränga sekretess standarder](https://www.microsoft.com/TrustCenter/Privacy/We-set-and-adhere-to-stringent-standards)

Fastställ

- [Microsoft Säkerhetscenter](https://www.microsoft.com/trustcenter/default.aspx)
- [Hubb för vanliga kontroller](https://www.microsoft.com/trustcenter/Common-Controls-Hub)
- [Check lista för Cloud Services noggrannhet](https://www.microsoft.com/trustcenter/Compliance/Due-Diligence-Checklist)
- [Efterlevnad av tjänst, plats och bransch](https://www.microsoft.com/trustcenter/Compliance/default.aspx)

Oh

- [Hur Microsoft skyddar kund information i Azure-tjänster](https://www.microsoft.com/trustcenter/Transparency/default.aspx)
- [Hur Microsoft hanterar data platser i Azure-tjänster](https://azuredatacentermap.azurewebsites.net)
- [Vem i Microsoft kan komma åt dina data på vilka villkor](https://www.microsoft.com/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms)
- [Hur Microsoft skyddar kund information i Azure-tjänster](https://www.microsoft.com/trustcenter/Transparency/default.aspx)
- [Granska certifiering för Azure-tjänster, OH-hubb](https://www.microsoft.com/trustcenter/Compliance/default.aspx)

## <a name="next-steps"></a>Nästa steg

Det första steget för att vidta åtgärder i en styrnings strategi är en [princip granskning](./cloud-policy-review.md). [Princip och efterlevnad](./index.md) kan vara en användbar guide under princip granskningen.

> [!div class="nextstepaction"]
> [Förbereda för en princip granskning](./cloud-policy-review.md)
