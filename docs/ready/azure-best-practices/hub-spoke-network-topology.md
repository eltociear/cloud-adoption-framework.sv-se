---
title: Nätverkstopologi med nav och ekrar
description: Lär dig mer om topologier för nav och ekrar för mer effektiv hantering av vanliga kommunikations-eller säkerhets krav.
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: 1d3d3de47ac46b775e94c89fc390cce84cb647a2
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433995"
---
<!-- cSpell:ignore tracsman jonor rossort NVAs -->

# <a name="hub-and-spoke-network-topology"></a>Nätverkstopologi med nav och ekrar

*Hubb och ekrar* är en nätverksmodell för effektiv hantering av vanlig kommunikation och säkerhetskrav. Det bidrar också till att undvika begränsningar i Azure-prenumerationen. Den här modellen riktar sig mot följande överväganden:

- **Kostnadsbesparingar och hanteringseffektivitet**. Genom att centralisera tjänster som kan delas av flera arbetsbelastningar, till exempel virtuella nätverksinstallationer (NVA) och DNS-servrar, på en enda plats kan IT-avdelningen minska kostnaderna för överflödiga resurser och hantering.
- **Hantera prenumerationsbegränsningar**. Stora molnbaserade arbetsbelastningar kan behöva flera resurser än det som tillåts i en enda Azure-prenumeration. Med peer-anslutning av arbetsbelastningar i virtuella nätverk från olika prenumerationer till en central hubb löser du dessa problem. Mer information finns i [prenumerations gränser](https://docs.microsoft.com/azure/azure-subscription-service-limits).
- **Separering av problem**. Du kan distribuera enskilda arbetsbelastningar mellan centrala IT-team och arbetsbelastningsteam.

Mindre molnegendomar har kanske inte nytta av den ökade strukturen och kapaciteten i den här modellen. Men större moln implementerings ansträngningar bör överväga att implementera en nätverks arkitektur för hubb och eker om de har något av de problem som anges ovan.

> [!NOTE]
> Azure Reference arkitekturer-platsen innehåller exempel på mallar som du kan använda som grund för att implementera egna nav-och eker-nätverk:
>
> - [Implementera en nätverkstopologi för nav och ekrar i Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
> - [Implementera en nätverkstopologi med nav och ekrar med delade tjänster i Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)

## <a name="overview"></a>Översikt

![Exempel på en nätverkstopologi för nav och ekrar][1]

Som du ser i diagrammet stöder Azure två typer av nav och eker-design. Det har stöd för kommunikation, delade resurser och centraliserade säkerhetsprinciper (”Vnet Hub” i diagrammet) eller en virtuell WAN-typ (”Virtual WAN” i diagrammet) för storskaliga kommunikationer från gren till gren eller gren till Azure.

En hubb är en central nätverkszon som styr och kontrollerar inkommande eller utgående trafik mellan zoner: Internet, lokalt och ekrar. NAV-och eker-topologin ger IT-avdelningen ett effektivt sätt att tillämpa säkerhets principer på en central plats. Det minskar också risken för felaktig konfiguration och exponering.

Hubben innehåller ofta de gemensamma tjänstkomponenter som ekrarna använder. Följande exempel är gemensamma centrala tjänster:

- Windows Server Active Directory-infrastrukturen som krävs för användarautentisering av tredje part som får åtkomst från ej betrodda nätverk innan de får åtkomst till arbetsbelastningarna i ekern. Det inkluderar relaterade Active Directory Federation Services (AD FS).
- En DNS-tjänst för att matcha namn på arbetsbelastningen i ekrarna, för att komma åt resurser lokalt och på Internet om [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview) inte används.
- En PKI (Public Key Infrastructure) för att implementera enkel inloggning på arbetsbelastningar.
- Flödeskontroll av TCP- och UDP-trafik mellan ekrarnas nätverkszoner och Internet.
- Flödeskontroll mellan ekrar och lokalt.
- Vid behov, flödeskontroll mellan två ekrar.

Du kan minimera redundans, förenkla hanteringen och minska den totala kostnaden genom att använda den delade hubbinfrastrukturen för att stödja flera ekrar.

Rollen för varje eker kan vara värd för olika typer av arbetsbelastningar. Ekrarna ger också en modulär metod för upprepningsbara distributioner av samma arbetsbelastningar. Exempel är utveckling och testning, testning av användar godkännande, mellanlagring och produktion.

Ekrarna kan också särskilja och aktivera olika grupper i din organisation. Ett exempel är Azure DevOps-grupper. I en eker är det möjligt att distribuera en grundläggande arbetsbelastning eller komplexa arbetsbelastningar på flera nivåer med trafikkontroll mellan nivåerna.

## <a name="subscription-limits-and-multiple-hubs"></a>Prenumerationsbegränsningar och flera hubbar

I Azure distribueras alla komponenter, oavsett typ, i en Azure-prenumeration. Isolering av Azure-komponenter i olika Azure-prenumerationer kan uppfylla kraven på olika affärslinjer, till exempel att ställa in differentierade nivåer av åtkomst och auktorisering.

En enda hubb och eker-implementering kan skala upp till ett stort antal ekrar. Men precis som med varje IT-system finns det plattformsgränser. Hubb-distributionen är kopplad till en enskild Azure-prenumeration som har begränsningar. Ett exempel är ett maximalt antal virtuella nätverks peer-datorer. Läs mer i [Azure-prenumeration och tjänstbegränsningar, kvoter och begränsningar](https://docs.microsoft.com/azure/azure-subscription-service-limits).

I fall där gränser kan vara ett problem kan du skala upp arkitekturen ytterligare genom att utöka modellen från en enda hubb och eker till ett kluster med hubbar och ekrar. Du kan sammankoppla flera hubbar i en eller flera Azure-regioner med hjälp av peering av virtuella nätverk, Azure ExpressRoute, ett virtuellt WAN-nätverk eller ett plats-till-plats-VPN.

![Kluster med hubbar och ekrar][2]

Introduktionen av flera hubbar ökar systemets kostnader och hantering. Detta är endast motiverat av skalbarhet, systemgränser eller redundans och regional replikering för användarprestanda eller haveriberedskap. I scenarier som kräver flera hubbar bör alla hubbar sträva efter att erbjuda samma uppsättning tjänster för att underlätta driften.

## <a name="interconnection-between-spokes"></a>Samtrafik mellan ekrar

Det är möjligt att implementera komplexa arbetsbelastningar i en enda eker. Du kan implementera konfigurationer med flera nivåer med hjälp av undernät (en för varje nivå) i samma virtuella nätverk och genom att använda nätverkssäkerhetsgrupper för att filtrera flödena.

En arkitekt kan vilja distribuera en arbetsbelastning på flera nivåer i flera virtuella nätverk. Med peering av virtuella nätverk kan ekrar ansluta till andra ekrar i samma hubb eller i olika hubbar.

Ett typiskt exempel på det här scenariot när programbearbetningsservrar finns i en eker eller virtuellt nätverk. Databasen distribueras i en annan eker- eller ett virtuellt nätverk. I det här fallet är det enkelt att koppla ekrarna med peering av virtuella nätverk och undvika att överföra genom hubben. Lösningen är att utföra en noggrann arkitektur och säkerhets granskning för att se till att kringgå navet inte kringgår viktiga säkerhets-och gransknings punkter som bara finns i hubben.

![Ekrar som ansluter till varandra och en hubb][3]

Ekrar kan också vara sammankopplade till en eker som fungerar som hubb. Den här metoden skapar en hierarki på två nivåer: ekern på den högre nivån (nivå 0) blir hubb för nedre ekrar (nivå 1) i hierarkin. Ekrarna för en nav-och eker-implementering krävs för att vidarebefordra trafiken till den centrala hubben så att trafiken kan vidarebefordra till sitt mål i antingen det lokala nätverket eller det offentliga Internet. En arkitektur med två nivåer av hubbar introducerar komplex routning som tar bort fördelarna med en enkel hubb och eker-relation.

<!-- images -->

[1]: ../../_images/azure-best-practices/network-hub-spoke-high-level.png "Exempel på en hög nivå med hubb och eker"
[2]: ../../_images/azure-best-practices/network-hub-spokes-cluster.png "Kluster med hubbar och ekrar"
[3]: ../../_images/azure-best-practices/network-spoke-to-spoke.png "Eker-till-eker"
