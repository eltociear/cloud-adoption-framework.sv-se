---
title: Styrningsdesign för en enkel arbetsbelastning
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vägledning för att konfigurera Azure styrnings kontroller så att en användare kan distribuera en enkel arbets belastning.
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 28ab035dd2440ede657dbcbd7066b78778bc09e8
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027397"
---
# <a name="governance-design-for-a-simple-workload"></a>Styrningsdesign för en enkel arbetsbelastning

Målet med den här vägledningen är att hjälpa dig att lära dig att utforma en resurs styrnings modell i Azure som stöd för ett enda team och en enkel arbets belastning. Du kommer att titta på en uppsättning hypotetiska styrnings krav och sedan gå igenom flera exempel på implementeringar som uppfyller dessa krav.

I det grundläggande implementerings skedet är vårt mål att distribuera en enkel arbets belastning till Azure. Detta resulterar i följande krav:

- Identitets hantering för en enskild **arbets belastnings ägare** som ansvarar för att distribuera och underhålla den enkla arbets belastningen. Arbets belastnings ägaren kräver behörighet att skapa, läsa, uppdatera och ta bort resurser samt behörighet att delegera dessa rättigheter till andra användare i identitets hanterings systemet.
- Hantera alla resurser för den enkla arbets belastningen som en enda hanterings enhet.

## <a name="licensing-azure"></a>Licensiering av Azure

Innan du börjar utforma vår styrnings modell är det viktigt att förstå hur Azure är licensierat. Detta beror på att de administrativa konton som är kopplade till Azure-licensen har den högsta åtkomst nivån till dina Azure-resurser. Dessa administrativa konton utgör grunden för din styrnings modell.

> [!NOTE]
> Om din organisation har ett befintligt [Microsoft-Enterprise-avtal](https://www.microsoft.com/licensing/licensing-programs/enterprise.aspx) som inte innehåller Azure kan du lägga till Azure genom att göra ett åtagande åtagande. Mer information finns i [licens för Azure för företaget](https://azure.microsoft.com/pricing/enterprise-agreement) .

När Azure lades till i organisationens Enterprise-avtal uppmanas din organisation att skapa ett **Azure-konto**. När kontot skapas skapas en Azure- **konto ägare** , samt en Azure Active Directory-klient (Azure AD) med ett **globalt administratörs** konto. En Azure AD-klient är en logisk konstruktion som representerar en säker, dedikerad instans av Azure AD.

![Azure-konto med Azure konto hanteraren och global administratör](../../_images/govern/design/governance-3-0.png)
för Azure AD*figur 1 – ett Azure-konto med en global administratör för konto hanteraren och Azure AD.*

## <a name="identity-management"></a>Identitetshantering

Azure litar bara på Azure [AD](https://docs.microsoft.com/azure/active-directory) för att autentisera användare och ge användarna åtkomst till resurser, så Azure AD är vårt identitets hanterings system. Den globala Azure AD-administratören har den högsta behörighets nivån och kan utföra alla åtgärder som rör identitet, inklusive att skapa användare och tilldela behörigheter.

Vårt krav är identitets hantering för en enskild **arbets belastnings ägare** som ansvarar för att distribuera och underhålla den enkla arbets belastningen. Arbets belastnings ägaren kräver behörighet att skapa, läsa, uppdatera och ta bort resurser samt behörighet att delegera dessa rättigheter till andra användare i identitets hanterings systemet.

Vår globala Azure AD-administratör kommer att skapa **arbets belastnings ägar** kontot för arbets belastnings ägaren:

![Azure AD global-administratören skapar arbets Belastningens ägar](../../_images/govern/design/governance-1-2.png)
konto*bild 2 – Azure AD global-administratören skapar användar kontot för arbets belastnings ägare.*

Du kan inte tilldela resurs åtkomst behörighet förrän den här användaren har lagts till i en **prenumeration**, så du kommer att göra det i följande två avsnitt.

## <a name="resource-management-scope"></a>Resurs hanterings omfång

När antalet resurser som distribueras av din organisation växer växer även komplexiteten med att hantera resurserna. Azure implementerar en logisk container-hierarki som gör det möjligt för din organisation att hantera dina resurser i grupper på olika nivåer av granularitet, även kallat **omfattning**.

Den översta nivån av resurs hanterings omfång är **prenumerations** nivån. En prenumeration skapas av Azures **konto ägare**, som upprättar det ekonomiska åtagandet och ansvarar för att betala för alla Azure-resurser som är associerade med prenumerationen:

![Azure-kontots ägare skapar en](../../_images/govern/design/governance-1-3.png)
prenumerations*bild 3 – Azures konto ägare skapar en prenumeration.*

När prenumerationen har skapats associerar Azure- **konto ägaren** en Azure AD-klient med prenumerationen och den här Azure AD-klienten används för att autentisera och auktorisera användare:

![Azure-kontots ägare associerar Azure AD-klienten med](../../_images/govern/design/governance-1-4.png)
prenumerations*figuren 4 – Azures konto ägare kopplar Azure AD-klienten till prenumerationen.*

Du kanske har märkt att det inte finns någon användare som är associerad med prenumerationen, vilket innebär att ingen har behörighet att hantera resurser. I verkligheten är **konto ägaren** ägare till prenumerationen och har behörighet att vidta åtgärder på en resurs i prenumerationen. **Konto ägaren** är dock mer än troligt vis en ekonomi person i din organisation och ansvarar inte för att skapa, läsa, uppdatera och ta bort resurser – dessa aktiviteter utförs av **arbets Belastningens ägare**. Därför måste du lägga till **arbets belastnings ägaren** till prenumerationen och tilldela behörigheter.

Eftersom **kontots ägare** för närvarande är den enda användaren med behörighet att lägga till **arbets belastnings ägaren** till prenumerationen lägger de till **arbets belastnings ägaren** till prenumerationen:

![Azure-kontots ägare lägger till * * arbets Belastningens ägare * *](../../_images/govern/design/governance-1-5.png)
till prenumerations*bilden 5 – Azure-kontots ägare lägger till arbets belastnings ägaren till prenumerationen.*

Azure- **kontots ägare** beviljar behörigheter till **arbets belastnings ägaren** genom att tilldela en [rollbaserad åtkomst kontroll (RBAC)](https://docs.microsoft.com/azure/role-based-access-control) roll. RBAC-rollen anger en uppsättning behörigheter som **arbets belastnings ägaren** har för en enskild resurs typ eller en uppsättning resurs typer.

Observera att **konto ägaren** i det här exemplet har tilldelat den [inbyggda **ägar** rollen](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner):

![* * Arbets Belastningens ägare * * tilldelades den inbyggda ägar rollen](../../_images/govern/design/governance-1-6.png)
*bild 6 – arbets belastnings ägaren har tilldelats den inbyggda ägar rollen.*

Den inbyggda **ägar** rollen beviljar alla behörigheter till **arbets belastnings ägaren** i prenumerations omfånget.

> [!IMPORTANT]
> Azure- **kontots ägare** ansvarar för det finansiella åtagande som är associerat med prenumerationen, men **arbets Belastningens ägare** har samma behörigheter. **Konto ägaren** måste ha förtroende för **arbets belastnings ägaren** för att distribuera resurser som ingår i prenumerations budgeten.

Nästa nivå av hanterings omfång är **resurs grupps** nivån. En resurs grupp är en logisk behållare för resurser. Åtgärder som tillämpas på resurs grupps nivå gäller för alla resurser i en grupp. Det är också viktigt att notera att behörigheter för varje användare ärvs från nästa nivå, om de inte uttryckligen ändras i det aktuella omfånget.

Vi illustrerar detta genom att titta på vad som händer när **arbets belastnings ägaren** skapar en resurs grupp:

![* * Arbets Belastningens ägare * * skapar en resurs](../../_images/govern/design/governance-1-7.png)
grupp*bild 7 – arbets belastnings ägaren skapar en resurs grupp och ärver den inbyggda ägar rollen i resurs grupps omfånget.*

Återigen ger den inbyggda **ägar** rollen alla behörigheter till **arbets belastnings ägaren** i resurs grupps omfånget. Som vi nämnt tidigare ärvs rollen från prenumerations nivån. Om en annan roll tilldelas den här användaren i det här omfånget gäller den bara för detta omfång.

Den lägsta nivån av hanterings omfång finns på **resurs** nivån. Åtgärder som tillämpas på resurs nivå gäller endast för själva resursen. Samtidigt ärvs behörigheter på resurs nivå från resurs gruppens omfång. Låt oss till exempel ta en titt på vad som händer om **arbets belastnings ägaren** distribuerar ett [virtuellt nätverk](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) till resurs gruppen:

![* * Arbets Belastningens ägare * * skapar en](../../_images/govern/design/governance-1-8.png)
resurs*bild 8 – arbets belastnings ägaren skapar en resurs och ärver den inbyggda ägar rollen i resurs omfånget.*

**Arbets belastnings ägaren** ärver ägar rollen i resurs omfånget, vilket innebär att arbets belastnings ägaren har alla behörigheter för det virtuella nätverket.

## <a name="implementing-the-basic-resource-access-management-model"></a>Implementera den grundläggande resurs åtkomst hanterings modellen

Vi går vidare och lär dig hur du implementerar styrnings modellen som har utformats tidigare.

Din organisation kräver ett Azure-konto för att börja. Om din organisation har ett befintligt [Microsoft-Enterprise-avtal](https://www.microsoft.com/licensing/licensing-programs/enterprise.aspx) som inte innehåller Azure kan du lägga till Azure genom att göra ett åtagande åtagande. Mer information finns i [licens för Azure för företaget](https://azure.microsoft.com/pricing/enterprise-agreement) .

När ditt Azure-konto har skapats anger du att en person i din organisation ska vara ägare av Azure- **kontot**. En Azure Active Directory-klient (Azure AD) skapas sedan som standard. Ditt Azure- **kontos ägare** måste [skapa användar kontot](https://docs.microsoft.com/azure/active-directory/add-users-azure-active-directory) för den person i din organisation som är **arbets belastnings ägare**.

Därefter måste ditt Azure- **kontos ägare** [skapa en prenumeration](https://docs.microsoft.com/partner-center/create-a-new-subscription) och [associera Azure AD-klienten](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory) med den.

Slutligen, nu när prenumerationen har skapats och din Azure AD-klient är kopplad till den, kan du [lägga till **arbets belastnings ägaren** till prenumerationen med den inbyggda **ägar** rollen](https://docs.microsoft.com/azure/billing/billing-add-change-azure-subscription-administrator#assign-a-user-as-an-administrator-of-a-subscription).

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Distribuera en grundläggande arbets belastning till Azure](../../infrastructure/virtual-machines/basic-workload.md)
> [!div class="nextstepaction"]
> [Lär dig mer om resurs åtkomst för flera team](./governance-multiple-teams.md)
