---
title: Rekommenderad rollbaserad åtkomstkontroll
description: Rekommenderad rollbaserad åtkomstkontroll
author: rotycenh
ms.author: brblanch
ms.date: 11/28/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: BrianBlanchard
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: 2b7af250046e024393d14e37ae2985f8bf453be7
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806874"
---
# <a name="role-based-access-control"></a>Rollbaserad åtkomstkontroll

Gruppbaserade åtkomsträttigheter och -behörigheter är en bra idé. Att hantera grupper i stället för enskilda användare förenklar underhållet av åtkomstprinciper, ger konsekvent åtkomsthantering för team och minskar eventuella konfigurationsfel. Genom att tilldela användare till och ta bort användare från lämpliga grupper förblir varje användares behörigheter alltid aktuella. Azures [rollbaserade åtkomstkontroll (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/overview) erbjuder detaljerad åtkomsthantering för resurser som har organiserats efter användarroller.

En översikt över rekommenderade RBAC-rutiner som en del av en identitets-och säkerhetsstrategin finns i [Metodtips för Azure-identitetshantering och åtkomstkontroll](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices#use-role-based-access-control).

## <a name="overview-of-role-based-access-control"></a>Översikt över rollbaserad åtkomstkontroll

Genom att använda [rollbaserad åtkomstkontroll](https://docs.microsoft.com/azure/role-based-access-control/overview)kan du separera uppgifter i ditt team och endast bevilja tillräcklig åtkomst för särskilda Azure Active Directory (Azure AD)-användare, grupper, tjänsthuvudnamn eller hanterade identiteter så att de kan utföra sina uppgifter. I stället för att ge alla obegränsad behörighet i din Azure-prenumeration eller dina resurser kan du begränsa åtkomsten för varje uppsättning resurser.

[Rolldefinitioner för RBAC-roller](https://docs.microsoft.com/azure/role-based-access-control/role-definitions) är en lista med åtgärder som tillåts eller inte tillåts för användare eller grupper som har tilldelats rollen. En rolls [omfång](https://docs.microsoft.com/azure/role-based-access-control/overview#scope) anger vilka resurser som dessa definierade behörigheter gäller för. Omfånget kan anges på flera nivåer: hanteringsgrupp, prenumeration, resursgrupp och resurs. Omfång är strukturerade i en överordnad/underordnad relation.

![Hierarki för RBAC-omfång](../../_images/azure-best-practices/rbac-scope.png)

Detaljerade anvisningar för hur du tilldelar användare och grupper till särskilda roller och tilldelar roller till omfång finns i [Hantera åtkomst till Azure-resurser med rollbaserad åtkomstkontroll](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal).

När du planerar din strategi för åtkomstkontroll ska du använda en modell för minsta möjliga behörighet som endast ger användare de behörigheter som krävs för att de ska kunna utföra sina uppgifter. I följande diagram visas ett föreslaget mönster för att använda rollbaserad åtkomstkontroll med den här metoden.

![Förslag på mönster för rollbaserad åtkomstkontroll](../../_images/azure-best-practices/rbac-least-privilege.png)

> [!NOTE]
> Ju mer specifika och detaljerade behörigheter du definierar desto mer sannolikt är det att din åtkomstkontroll blir komplex och svår att hantera. Detta gäller särskilt efter hand som din molnegendom blir större. Undvik resursspecifika behörigheter. Använd istället [hanteringsgrupper](https://docs.microsoft.com/azure/governance/management-groups) för åtkomstkontroll för hela företaget och [resursgrupper](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) för åtkomstkontroll inom prenumerationer. Undvik användarspecifika behörigheter. Tilldela istället åtkomst till [grupper i Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups).

## <a name="use-built-in-rbac-roles"></a>Använd inbyggda RBAC-roller

Azure tillhandahåller en mängd inbyggda rolldefinitioner, med tre huvudsakliga åtkomstroller:

- Rollen [Ägare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) låter dig hantera allt, inklusive åtkomst till resurser.
- Rollen [Deltagare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) låter dig hantera allt, utom åtkomst till resurser.
- Rollen [Läsare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#reader) låter dig visa allting, men låter dig inte göra några ändringar.

Med dessa kärnåtkomstroller som utgångspunkt kan ytterligare inbyggda roller ge mer detaljerad kontroll för åtkomst till specifika resurstyper eller Azure-funktioner. Du kan till exempel hantera åtkomst till virtuella datorer med hjälp av följande inbyggda roller:

- Rollen [inloggning som virtuell datoradministratör](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#virtual-machine-administrator-login) kan visa virtuella datorer i portalen och logga in som _administratör_.
- Rollen [Virtuell datordeltagare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) kan hantera, men inte bevilja åtkomst till, virtuella datorer och kan heller inte hantera virtuella nätverks- eller lagringskonton som de är anslutna till.
- Rollen [inloggning som virtuell datoranvändare](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#virtual-machine-user-login) kan visa virtuella datorer i portalen och logga in som vanlig användare.

Ett annat exempel på hur du använder inbyggda roller för att hantera specifika funktioner finns i diskussionen om att kontrollera åtkomsten till kostnadsspårningsfunktioner i [Spåra kostnader mellan affärsenheter, miljöer eller projekt](../azure-best-practices/track-costs.md#provide-the-right-level-of-cost-access).

En lista med alla inbyggda roller finns i [Inbyggda roller för Azure-resurser](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles).

## <a name="use-custom-roles"></a>Använd anpassade roller

Även om rollerna som är inbyggda i Azure har stöd för ett brett utbud av åtkomstkontrollscenarier, kanske de inte uppfyller alla krav för din organisation eller ditt team. Om du till exempel har en enda grupp med användare som ansvarar för att hantera virtuella datorer och Azure SQL Database-resurser kan du skapa en anpassad roll för att optimera hanteringen av de nödvändiga åtkomstkontrollerna.

Azure RBAC-dokumentationen innehåller instruktioner om hur du [skapar anpassade roller](https://docs.microsoft.com/azure/role-based-access-control/custom-roles), tillsammans med information om [hur rolldefinitioner fungerar](https://docs.microsoft.com/azure/role-based-access-control/role-definitions).

## <a name="separation-of-responsibilities-and-roles-for-large-organizations"></a>Separering av ansvarsområden och roller för stora organisationer

Med rollbaserad åtkomstkontroll kan organisationer tilldela olika team till olika hanteringsuppgifter inom stora molnegendomar. Det gör det möjligt för centrala IT-team att styra kärnåtkomst- och säkerhetsfunktioner, samtidigt som programutvecklare och andra team får omfattande kontroll över vissa arbetsbelastningar eller resursgrupper.

De flesta molnmiljöer kan också gynnas av en strategi för åtkomstkontroll som använder flera roller och betonar en separation av ansvarsområden mellan dessa roller. Den här metoden kräver att en alla betydande ändringar av resurser eller infrastruktur måste utföras av flera roller, så att mer än en person måste granska och godkänna ändringar. Den här separationen av ansvarsområden begränsar möjligheten för en enskild person att komma åt känsliga data eller införa sårbarheter att andra teammedlemmar vet om det.

I följande tabell visas ett vanligt mönster för att dela upp IT-ansvar i separata anpassade roller:

<!-- markdownlint-disable MD033 -->

| Grupp | Namn på gemensam roll | Ansvar |
| --- | --- | --- |
| Säkerhetsåtgärder | SecOps | Allmän säkerhetstillsyn.<br/><br/> Fastställer och tillämpar säkerhetsprinciper, till exempel kryptering i vila.<br/><br/> Hanterar krypteringsnycklar.<br/><br/> Hanterar brandväggsregler. |
| Nätverksåtgärder | NetOps | Hanterar nätverkskonfiguration och -åtgärder i virtuella nätverk, till exempel vägar och peer-kopplingar. |
| Systemåtgärder | SysOps | Anger infrastrukturalternativ för processor och lagring och hanterar resurser som har distribuerats. |
| Utveckling, test och drift | DevOps | Skapar och distribuerar arbetsbelastningsfunktioner och -program.<br/><br/> Hanterar funktioner och program så att de uppfyller serviceavtalens krav och andra kvalitetsstandarder. |

<!-- markdownlint-enable MD033 -->

Fördelningen av åtgärder och behörigheter i dessa standardroller är ofta samma för dina program, prenumerationer eller hela molnegendomen, även om dessa roller utförs av olika personer på olika nivåer. Därför kan du skapa en gemensam uppsättning RBAC-rolldefinitioner som ska tillämpas på olika omfång i din miljö. Användare och grupper kan sedan tilldelas en gemensam roll, men endast för den omfång av resurser, resurs grupper, prenumerationer eller hanteringsgrupper som de ansvarar för att hantera.

I en [topologi med hubb och ekrar](../azure-best-practices/hub-spoke-network-topology.md) med flera prenumerationer kan du till exempel ha en gemensam uppsättning roll definitioner för hubben och alla ekrar för arbets belastning. En hubbprenumerations NetOps-roll kan tilldelas till personer ur organisationens IT-personal som ansvarar för att underhålla nätverk för delade tjänster som används av alla arbetsbelastningar. NetOps-rollen för en arbetsbelastningsroll kan sedan tilldelas till medlemmar i den aktuella arbetsbelastningsgruppen så att de kan konfigurera nätverk i den prenumerationen enligt deras arbetsbelastningars krav. Samma rolldefinition används för båda, men omfångsbaserade tilldelningar ser till att användarna bara har den åtkomst som de behöver för att utföra sitt jobb.
