---
title: Skalning med flera Azure-prenumerationer
description: Lär dig att skala med flera Azure-prenumerationer.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 6a893ce6f8620b31fcf23d8c3e8581e95035bdcf
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76799802"
---
# <a name="scale-with-multiple-azure-subscriptions"></a>Skala med flera Azure-prenumerationer

Organisationer behöver ofta mer än en Azure-prenumeration till följd av resurs begränsningar och andra styrnings överväganden. Det är viktigt att ha en strategi för att skala dina prenumerationer.

## <a name="production-and-nonproduction-workloads"></a>Arbets belastningar för produktion och inte produktion

När du distribuerar din första produktions arbets belastning i Azure bör du börja med två prenumerationer: en för din produktions miljö och en för din IT-miljö (dev/test).

![En grundläggande prenumerations modell som visar nycklar bredvid rutor som är märkta med "produktion" och "inproduktion"](../../_images/ready/basic-subscription-model.png)

Vi rekommenderar den här metoden av flera orsaker:

- Azure har vissa prenumerationserbjudanden för arbetsbelastningar för utveckling/testning. Dessa erbjudanden ger rabatterade priser på Azure-tjänster och -licensiering.
- Dina produktions-och distributions miljöer kommer förmodligen att ha olika uppsättningar av Azure-principer. Genom att använda separata prenumerationer blir det enkelt att tillämpa varje specifik principuppsättning på prenumerationsnivån.
- Du kanske vill ha vissa typer av Azure-resurser i en utveckling/test-prenumeration för testning. Med en separatprenumeration kan du använda dessa resurstyper utan att göra dem tillgängliga i produktionsmiljön.
- Du kan använda dev/test-prenumerationer som isolerade sandbox-miljöer. Sådana sandlådor gör det möjligt för administratörer och utvecklare att snabbt bygga upp och riva ned hela uppsättningar av Azure-resurser. Den här isoleringen kan också hjälpa till med dataskydd och säkerhetsproblem.
- Rimliga kostnadströsklar varierar förmodligen mellan produktions- och dev/test-prenumerationer.

## <a name="other-reasons-for-multiple-subscriptions"></a>Andra orsaker till flera prenumerationer

Andra situationer kan kräva ytterligare prenumerationer. Tänk på följande när du utökar din molnegendom.

- Prenumerationer har olika gränser för olika resurstyper. Till exempel är antalet virtuella nätverk i en prenumeration begränsat. När en prenumeration närmar sig någon av dess gränser måste du skapa en annan prenumeration och lägga till nya resurser där.

  Läs mer i [Azure-prenumeration och tjänstbegränsningar, kvoter och begränsningar](https://docs.microsoft.com/azure/azure-subscription-service-limits).

- Varje prenumeration kan implementera egna principer för distributions bara resurs typer och regioner som stöds.

- Prenumerationer i offentliga moln regioner och statliga eller myndighets moln regioner har olika begränsningar. Dessa styrs ofta av olika dataklassificeringsnivåer mellan miljöer.

- Om du helt åtskiljer olika uppsättningar av användare av säkerhets- eller efterlevnadsskäl kan du behöva separata prenumerationer. Till exempel kan nationella myndighets organisationer behöva begränsa en prenumerations åtkomst till endast medborgarna.

- Olika prenumerationer kan ha olika typer av erbjudanden, var och ett med sina egna villkor.

- Förtroendeproblem kan uppstå mellan ägarna till en prenumeration och ägaren av de resurser som ska distribueras. Om du använder en annan prenumeration med olika ägarskap kan du undvika de här problemen, men en måste också anse nätverks-och data skydds problem som kommer att uppstå i den här distributionen.

- Bestämda ekonomiska eller geopolitiska kontroller kan kräva olika ekonomiska arrangemang för specifika prenumerationer. Dessa problem kan omfatta överväganden av data suveränitet, företag med flera dotter bolag eller separat redovisning och fakturering för affär senheter i olika länder och olika valutor.

- Azure-resurser som skapas med den klassiska distributionsmodellen bör isoleras i en egen prenumeration. Säkerheten för klassiska resurser skiljer sig från de resurser som distribueras via Azure Resource Manager. Det går inte att använda Azure-principer för klassiska resurser.

- Tjänstadministratörer som använder klassiska resurser har samma behörigheter som RBAC-ägare (rollbaserad åtkomstkontroll) för en prenumeration. Det är svårt att tillräckligt begränsa dessa tjänstadministratörers åtkomst i en prenumeration som blandar klassiska resurser och Resource Manager-resurser.

Du kan också välja att skapa ytterligare prenumerationer av andra affärsrelaterade eller tekniska skäl som är specifika för din organisation. Det kan finnas ytterligare kostnader för inkommande och utgående data mellan prenumerationer.

Du kan flytta många typer av resurser från en prenumeration till en annan eller använda automatiserade distributioner för att migrera resurser till en annan prenumeration. Mer information finns i [Flytta Azure-resurser till en annan resursgrupp eller prenumeration](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources).

## <a name="manage-multiple-subscriptions"></a>Hantera flera prenumerationer

Om du bara har ett fåtal prenumerationer är det relativt enkelt att hantera dem oberoende av varandra. Men om du har många prenumerationer bör du överväga att skapa en hierarki för hanteringsgrupper för att förenkla hanteringen av dina prenumerationer och resurser.

Hanterings grupper möjliggör effektiv hantering av åtkomst, principer och efterlevnad för en organisations prenumerationer. Varje hanteringsgrupp är en container för en eller flera prenumerationer.

Hanterings grupper är ordnade i en enkel hierarki. Du definierar den här hierarkin i din Azure Active Directory (Azure AD)-klient organisation så att den överensstämmer med organisationens struktur och behov. Den översta nivån kallas för *rothanteringsgruppen.* Du kan definiera upp till sex nivåer av hanteringsgrupper i hierarkin. Varje prenumeration finns bara i en hanteringsgrupp.

Azure har fyra hanteringsnivåer: hanteringsgrupper, prenumerationer, resursgrupper och resurser. Åtkomst eller principer som tillämpas på en nivå i hierarkin tillämpas också på nivåerna under denna. En resursägare eller en prenumerationsägare kan inte ändra en nedärvd princip. Den här begränsningen förbättrar styrningen.

> [!NOTE]
> Observera att tagg arv inte är tillgängligt för tillfället, men blir snart tillgängligt.

Genom att förlita dig på den här arvsmodellen kan du ordna prenumerationerna i hierarkin så att varje prenumeration följer lämpliga principer och säkerhetskontroller.

![De fyra omfångsnivåerna för att organisera dina Azure-resurser](../../ready/azure-setup-guide/media/organize-resources/scope-levels.png)

Alla tilldelningar av användaråtkomst eller principtilldelning för rothanteringsgruppen gäller för alla resurser inom katalogen. Tänk efter noga vilka objekt du definierar i det här omfånget. Inkludera endast de tilldelningar som du måste ha.

När du ursprungligen definierar din hanteringsgrupphierarki skapar du först rothanteringsgruppen. Sedan flyttar du alla befintliga prenumerationer i katalogen till rothanteringsgruppen. Nya prenumerationer skapas alltid i rothanteringsgruppen. Du kan senare flytta dem till en annan hanterings grupp.

När du flyttar en prenumeration till en befintlig hanteringsgrupp ärver den principerna och rolltilldelningarna från hanteringsgruppshierarkin ovanför den. När du har etablerat flera prenumerationer för dina Azure-arbetsbelastningar bör du skapa ytterligare prenumerationer som innehåller Azure-tjänster som andra prenumerationer delar.

![Exempel på ett hierarkiträd för hanteringsgrupp](../../_images/ready/management-group-hierarchy.png)

Mer information finns i [Organisera dina resurser med hanteringsgrupper i Azure](https://docs.microsoft.com/azure/governance/management-groups).

## <a name="tips-for-creating-new-subscriptions"></a>Tips för att skapa nya prenumerationer

- Identifiera vem som ska ansvara för att skapa nya prenumerationer.
- Bestäm vilka resurser som ska ingå i en prenumeration som standard.
- Bestäm hur alla standardprenumerationer ska se ut. I överväganden ingår RBAC-åtkomst, principer, taggar och infrastrukturresurser.
- Använd om möjligt ett [huvudnamn för tjänsten](https://docs.microsoft.com/azure/azure-resource-manager/grant-access-to-create-subscription) för att skapa nya prenumerationer. Definiera en säkerhetsgrupp som kan begära nya prenumerationer via ett automatiserat arbetsflöde.
- Om du är en Enterprise-avtalskund (EA) kan du be Azure-supporten att blockera skapandet av icke-EA-prenumerationer för din organisation.

## <a name="related-resources"></a>Relaterade resurser

- [Grundläggande koncept för Azure](../considerations/fundamental-concepts.md).
- [Organisera dina resurser i Azure-hanteringsgrupper](https://docs.microsoft.com/azure/governance/management-groups).
- [Utöka åtkomst för att hantera alla Azure-prenumerationer och hanteringsgrupper](https://docs.microsoft.com/azure/role-based-access-control/elevate-access-global-admin).
- [Flytta Azure-resurser till ny resursgrupp eller prenumeration](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources).

## <a name="next-steps"></a>Nästa steg

Granska [rekommenderade namngivnings- och taggningskonventioner](./naming-and-tagging.md) som du följer när du distribuerar dina Azure-resurser.

> [!div class="nextstepaction"]
> [Rekommenderade regler för namngivning och taggar](./naming-and-tagging.md)
