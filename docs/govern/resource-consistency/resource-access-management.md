---
title: Åtkomsthantering av resurser i Azure
description: 'Förklaring av resurs åtkomst hanterings konstruktioner i Azure: Azure Resource Manager, prenumerationer, resurs grupper och resurser'
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 825c220bda1c560c5d7bf07bcae649017525ff53
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76805633"
---
# <a name="resource-access-management-in-azure"></a>Åtkomsthantering av resurser i Azure

[Moln styrning](../index.md) beskriver de fem disciplinerna i moln styrning, som innehåller resurs hantering. [Vad är resurs åtkomst styrning](./index.md) ytterligare förklarar hur resurs åtkomst hantering passar in i disciplinen för resurs hantering. Innan du går vidare och lär dig hur du utformar en styrnings modell är det viktigt att förstå resurs åtkomst hanterings kontrollerna i Azure. Konfigurationen av dessa resurs åtkomst hanterings kontroller utgör grunden för din styrnings modell.

Börja med att ta en närmare titt på hur resurser distribueras i Azure.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-an-azure-resource"></a>Vad är en Azure-resurs?

I Azure refererar termen _resurs_ till en entitet som hanteras av Azure. Till exempel kallas virtuella datorer, virtuella nätverk och lagrings konton för Azure-resurser.

![diagram över en resurs](../../_images/govern/design/governance-1-9.png)
*figur 1 – en resurs.*

## <a name="what-is-an-azure-resource-group"></a>Vad är en Azure-resurs grupp?

Varje resurs i Azure måste tillhöra en [resurs grupp](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). En resurs grupp är helt enkelt en logisk konstruktion som grupperar flera resurser så att de kan hanteras som en enda enhet _baserat på livs cykel och säkerhet_. Till exempel kan resurser som delar samma livs cykel, till exempel resurser för ett [program på n-nivå](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier) , skapas eller tas bort som en grupp. Använd ett annat sätt: allt som är sammankopplat, som hanteras tillsammans och som är inaktuella tillsammans, hamnar tillsammans i en resurs grupp.

![diagram över en resurs grupp som innehåller en resurs](../../_images/govern/design/governance-1-10.png)
*figur 2 – en resurs grupp innehåller en resurs.*

Resurs grupper och de resurser som de innehåller är associerade med en Azure- **prenumeration**.

## <a name="what-is-an-azure-subscription"></a>Vad är en Azure-prenumeration?

En Azure-prenumeration liknar en resurs grupp i så att den är en logisk konstruktion som grupperar samman resurs grupper och deras resurser. En Azure-prenumeration är dock också kopplad till de kontroller som används av Azure Resource Manager. Ta en närmare titt på Azure Resource Manager om du vill veta mer om relationen mellan den och en Azure-prenumeration.

![diagram över en Azure-prenumeration](../../_images/govern/design/governance-1-11.png)
*figur 3 – en Azure-prenumeration.*

## <a name="what-is-azure-resource-manager"></a>Vad är Azure Resource Manager?

I [Hur fungerar Azure?](../../getting-started/what-is-azure.md) du har lärt dig att Azure innehåller en "klient del" med många tjänster som dirigerar alla funktioner i Azure. En av dessa tjänster är [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager)och den här tjänsten är värd för det RESTful-API som används av klienter för att hantera resurser.

![diagram över Azure Resource Manager](../../_images/govern/design/governance-1-12.png)
*bild 4-Azure Resource Manager.*

Följande bild visar tre klienter: [PowerShell](https://docs.microsoft.com/powershell/azure/overview), [Azure Portal](https://portal.azure.com)och [Azure CLI](https://docs.microsoft.com/cli/azure):

![diagram över Azure-klienter som ansluter till Azure Resource Manager API](../../_images/govern/design/governance-1-13.png)
*bild 5 – Azure-klienter ansluter till Azure Resource Manager RESTful-API: et.*

Även om dessa klienter ansluter till Azure Resource Manager med RESTful-API: et omfattar inte Azure Resource Manager funktioner för att hantera resurser direkt. I stället har de flesta resurs typer i Azure sin egen [**resurs leverantör**](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#terminology).

![Azure Resource providers](../../_images/govern/design/governance-1-14.png)
*figur 6 – Azure Resource providers.*

När en klient gör en begäran för att hantera en resurs, ansluter Azure Resource Manager till resurs leverantören för den resurs typen för att slutföra begäran. Om exempelvis en klient gör en begäran om att hantera en virtuell dator resurs, ansluter Azure Resource Manager till **Microsoft. Compute** Resource Provider.

![Azure Resource Manager ansluter till Microsoft. Compute Resource Provider](../../_images/govern/design/governance-1-15.png)
*figur 7-Azure Resource Manager ansluter till **Microsoft. Compute** Resource-providern för att hantera den resurs som anges i klient förfrågan.*

Azure Resource Manager kräver att klienten anger en identifierare för både prenumerationen och resurs gruppen för att kunna hantera den virtuella dator resursen.

Nu när du har lärt dig hur Azure Resource Manager fungerar går du tillbaka till diskussionen om hur en Azure-prenumeration är kopplad till de kontroller som används av Azure Resource Manager. Innan en resurs hanterings förfrågan kan utföras av Azure Resource Manager kontrol leras en uppsättning kontroller.

Den första kontrollen är att en begäran måste göras av en verifierad användare, och Azure Resource Manager har en betrodd relation med [Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory) för att tillhandahålla funktioner för användar identitet.

![Azure Active Directory](../../_images/govern/design/governance-1-16.png)
*bild 8-Azure Active Directory.*

I Azure AD är användarna segmenterade i **klienter**. En klient är en logisk konstruktion som representerar en säker, dedikerad instans av Azure AD som vanligt vis är kopplad till en organisation. Varje prenumeration är associerad med en Azure AD-klient.

![en Azure AD-klient som är associerad med en prenumeration](../../_images/govern/design/governance-1-17.png)
*figur 9 – en Azure AD-klient som är associerad med en prenumeration.*

Varje klientbegäran för att hantera en resurs i en viss prenumeration kräver att användaren har ett konto i den associerade Azure AD-klienten.

Nästa kontroll är en kontroll att användaren har tillräcklig behörighet för att utföra begäran. Behörigheter tilldelas till användare med hjälp av [rollbaserad åtkomst kontroll (RBAC)](https://docs.microsoft.com/azure/role-based-access-control).

![användare som tilldelats RBAC-roller](../../_images/govern/design/governance-1-18.png)
*figur 10. Varje användare i klienten tilldelas en eller flera RBAC-roller.*

En RBAC-roll anger en uppsättning behörigheter som en användare kan utföra på en speciell resurs. När rollen tilldelas till användaren tillämpas dessa behörigheter. Den [inbyggda **ägar** rollen](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) gör det till exempel möjligt för en användare att utföra åtgärder på en resurs.

Nästa kontroll är en kontroll av att begäran tillåts enligt de inställningar som angetts för [Azures resurs princip](https://docs.microsoft.com/azure/governance/policy). Azure Resource policies anger vilka åtgärder som tillåts för en speciell resurs. En Azure-resurs princip kan till exempel ange att användarna endast får distribuera en speciell typ av virtuell dator.

![Azures resurs princip](../../_images/govern/design/governance-1-19.png)
*Bild 11. Resurs princip för Azure.*

Nästa kontroll är en kontroll av att begäran inte överskrider en gräns för [Azure-prenumeration](https://docs.microsoft.com/azure/azure-subscription-service-limits). Varje prenumeration har till exempel en gräns på 980 resurs grupper per prenumeration. Om en begäran tas emot för att distribuera ytterligare en resurs grupp när gränsen har uppnåtts, nekas den.

![Azure Resource Limits](../../_images/govern/design/governance-1-20.png)
*figur 12. Resurs gränser i Azure.*

Den slutgiltiga kontrollen är en kontroll av att begäran finns i det finansiella åtagande som är associerat med prenumerationen. Om förfrågan till exempel är att distribuera en virtuell dator, verifierar Azure Resource Manager att prenumerationen har tillräckligt med betalnings information.

![ett finansiellt åtagande som är associerat med en prenumeration](../../_images/govern/design/governance-1-21.png)
*figur 13. Ett finansiellt åtagande är associerat med en prenumeration.*

## <a name="summary"></a>Sammanfattning

I den här artikeln har du lärt dig hur resurs åtkomst hanteras i Azure med hjälp av Azure Resource Manager.

## <a name="next-steps"></a>Nästa steg

Nu när du förstår hur du hanterar resurs åtkomst i Azure går du vidare till Lär dig hur du utformar en styrnings modell [för en enkel arbets belastning](./governance-simple-workload.md) eller [flera team](./governance-multiple-teams.md) med hjälp av dessa tjänster.

> [!div class="nextstepaction"]
> [En översikt över styrning](../index.md)
