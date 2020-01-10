---
title: Grundläggande koncept för Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig grundläggande begrepp och termer som används i Azure samt hur begreppen är relaterade till varandra.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: a3b773c4715b064413cb07d15d750b1204ddf90a
ms.sourcegitcommit: 7df593a67a2e77b5f61c815814af9f0c36ea5ebd
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/09/2020
ms.locfileid: "75781512"
---
# <a name="azure-fundamental-concepts"></a>Grundläggande koncept för Azure

Lär dig grundläggande begrepp och termer som används i Azure samt hur begreppen är relaterade till varandra.

## <a name="azure-terminology"></a>Azure-terminologi

Det är bra att känna till följande definitioner när du påbörjar arbetet med Azure-molnimplementering:

- **Resurs:** En entitet som hanteras av Azure. Exempel är virtuella Azure-datorer, virtuella nätverk och lagringskonton.
- **Prenumeration:** En logisk behållare för dina resurser. Varje Azure-resurs är bara associerad med en enskild prenumeration. Att skapa en prenumeration är det första steget i att implementera Azure.
- **Azure-konto:** Den e-postadress som du anger när du skapar en Azure-prenumeration är Azure-kontot för prenumerationen. Den part som är kopplad till e-postkontot ansvarar för de månatliga kostnader som debiteras för resurserna i prenumerationen. När du skapar ett Azure-konto anger du kontaktuppgifter och faktureringsinformation, till exempel ett kreditkort. Du kan använda samma Azure-konto (e-postadress) för flera prenumerationer. Varje prenumeration är bara associerad med ett enskilt Azure-konto.
- **Konto administratör:** Den part som är kopplad till den e-postadress som används för att skapa en Azure-prenumeration. Konto administratören ansvarar för att betala för alla kostnader som uppkommer av prenumerationens resurser.
- **Azure Active Directory (Azure AD):** Microsoft Cloud-baserad identitets-och åtkomst hanterings tjänst. Azure AD gör att dina medarbetare kan logga in och få åtkomst till resurser.
- **Azure AD-klient:** En dedikerad och betrodd instans av Azure AD. En Azure AD-klientorganisation som skapas automatiskt när organisationen för första gången registrerar sig för en Microsoft-molntjänstprenumeration som Microsoft Azure, Microsoft Intune eller Office 365. En Azure-klientorganisation representerar en enskild organisation.
- **Azure AD-katalog:** Varje Azure AD-klient har en enda, dedikerad och betrodd katalog. Katalogen innehåller klientorganisationens användare, grupper och appar. Katalogen används för att utföra funktioner för identitet och åtkomsthantering för klientorganisationsresurser. En katalog kan associeras med flera prenumerationer, men varje prenumeration är bara associerad med en enskild katalog.
- **Resurs grupper:** Logiska behållare som du använder för att gruppera relaterade resurser i en prenumeration. Varje resurs kan endast finnas i en resursgrupp. Resurs grupper tillåter mer detaljerad gruppering i en prenumeration. Används ofta för att representera en samling till gångar som krävs för att stödja en arbets belastning, ett program eller en specifik funktion i en prenumeration.
- **Hanterings grupper:** Logiska behållare som du använder för en eller flera prenumerationer. Du kan definiera en hierarki för hanteringsgrupper, prenumerationer, resursgrupper och resurser för att effektivt hantera åtkomst, principer och efterlevnad genom arv.
- **Region:** En uppsättning Azure-datacenter som distribueras inuti en latens-definierad perimeter. Datacentren är anslutna via ett dedikerat, regionalt nätverk med låg svarstid. De flesta Azure-resurser körs i en specifik Azure-region.

## <a name="azure-subscription-purposes"></a>Syften med Azure-prenumeration

En Azure-prenumeration har flera olika syften. En Azure-prenumeration är:

- **Ett juridiskt avtal.** Varje prenumeration är associerad med ett [Azure-erbjudande](https://azure.microsoft.com/support/legal/offer-details) (till exempel en kostnadsfri utvärderingsversion eller betala per användning). Varje erbjudande har en speciell prisplan, förmåner och tillhörande villkor. Du väljer ett Azure-erbjudande när du skapar en prenumeration.
- **Ett betalnings avtal.** När du skapar en prenumeration anger du betalningsinformation för den prenumerationen, till exempel ett kreditkortsnummer. Varje månad beräknas kostnaderna för de resurser som distribuerats till den prenumerationen och debiteras via den betalningsmetoden.
- **En gräns för skalning.** Gränser för skala definieras för en prenumeration. Prenumerationens resurser får inte överskrida de inställda skalnings gränserna. Det finns till exempel en gräns för det antal virtuella datorer som du kan skapa i en enstaka prenumeration.
- **En administrativ gränser.** En prenumeration kan fungera som en gräns för administration, säkerhet och principer. Azure innehåller även andra mekanismer för att uppfylla dessa behov, till exempel hanteringsgrupper, resursgrupper och rollbaserad åtkomstkontroll.

## <a name="azure-subscription-considerations"></a>Överväganden för Azure-prenumerationer

När du skapar en Azure-prenumeration gör du flera viktiga val för prenumerationen:

- **Vem ansvarar för att betala för prenumerationen?** Den part som är kopplad till den e-postadress som du anger när du skapar en prenumeration som standard är prenumerationens konto administratör. Den part som är kopplad till den här e-postadressen ansvarar för att betala för alla kostnader som uppkommer av prenumerationens resurser.
- **Vilket Azure-erbjudande är jag intresserad av?** Varje prenumeration är associerad med ett specifikt [Azure-erbjudande](https://azure.microsoft.com/support/legal/offer-details). Du kan välja det Azure-erbjudande som bäst uppfyller dina behov. Om du till exempel vill använda en prenumeration för att köra arbets belastningar som inte är produktion kan du välja Dev/Test – betala per användning erbjudandet eller det Enterprise Dev/Test erbjudandet.

> [!NOTE]
> När du registrerar dig för Azure kan du se frasen *skapa ett Azure-konto*. Du skapar ett Azure-konto när du skapar en Azure-prenumeration och associerar prenumerationen med ett e-postkonto.

## <a name="azure-administrative-roles"></a>Administrativa roller i Azure

Azure definierar tre typer av roller för administration av prenumerationer, identiteter och resurser:

- Administratörsroller för klassiska prenumerationer
- Roller för rollbaserad åtkomstkontroll i Azure (RBAC)
- Administratörsroller för Azure Active Directory (AD Azure)

Rollen kontoadministratör för en Azure-prenumeration tilldelas till det e-postkonto som används för att skapa Azure-prenumerationen. Kontoadministratören är faktureringsägare för prenumerationen. Kontoadministratören kan hantera prenumerationsuppgifterna i [Azure-kontocenter](https://account.azure.com/Subscriptions).

Som standard tilldelas även rollen tjänstadministratör för en prenumeration till det e-postkonto som används för att skapa Azure-prenumerationen. Tjänstadministratören har behörighet till prenumerationen som motsvarar den RBAC-baserade ägarrollen. Tjänstadministratören har även fullständig åtkomst till Azure-portalen. Kontoadministratören kan ändra tjänstadministratören till annat e-postkonto.

När du skapar en Azure-prenumeration kan du associera den med en befintlig Azure AD-klientorganisation. Annars skapas en ny Azure AD-klientorganisation med en associerad katalog. Rollen global administratör i Azure AD-katalogen tilldelas till det e-postkonto som används för att skapa Azure AD-prenumerationen.

Ett e-postkonto kan associeras med flera Azure-prenumerationer. Kontoadministratören kan överföra en prenumeration till ett annat konto.

En detaljerad beskrivning av de roller som definieras i Azure finns i [Administratörsroller för klassiska prenumerationer, Azure RBAC-roller och administratörsroller för Azure AD](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

## <a name="subscriptions-and-regions"></a>Prenumerationer och regioner

Varje Azure-resurs är logiskt associerad med endast en enskild prenumeration. När du skapar en resurs väljer du vilken Azure-prenumeration som den resursen ska distribueras till. Du kan flytta en resurs till en annan prenumeration senare.

En prenumeration är inte knuten till någon specifik Azure-region. Varje Azure-resurs distribueras dock till endast en region. Du kan ha resurser i flera regioner som är associerade med samma prenumeration.

> [!NOTE]
> De flesta Azure-resurser distribueras till en specifik region. Vissa resurstyper betraktas dock som globala resurser, till exempel principer som du anger med hjälp av Azure Policy-tjänsterna.

## <a name="related-resources"></a>Relaterade resurser

Följande resurser innehåller detaljerad information om de begrepp som beskrivs i den här artikeln:

- [Hur fungerar Azure?](../../getting-started/what-is-azure.md)
- [Åtkomsthantering av resurser i Azure](../../govern/resource-consistency/resource-access-management.md)
- [Översikt över Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)
- [Rollbaserad åtkomstkontroll (RBAC) för Azure-resurser](https://docs.microsoft.com/azure/role-based-access-control/overview)
- [Vad är Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis)
- [Associera eller lägga till en Azure-prenumeration till Azure Active Directory-klienten](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory)
- [Topologier för Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-topologies)
- [Prenumerationer, licenser, konton och klientorganisationer för Microsofts molnerbjudanden](https://docs.microsoft.com/office365/enterprise/subscriptions-licenses-accounts-and-tenants-for-microsoft-cloud-offerings)

## <a name="next-steps"></a>Nästa steg

Nu när du förstår de grundläggande Azure-begreppen kan du lära dig hur du [skalar med flera Azure-prenumerationer](../azure-best-practices/scaling-subscriptions.md).

> [!div class="nextstepaction"]
> [Skala med flera Azure-prenumerationer](../azure-best-practices/scaling-subscriptions.md)
