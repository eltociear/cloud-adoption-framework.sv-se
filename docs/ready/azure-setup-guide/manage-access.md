---
title: Hantera åtkomsten till Azure-miljön
description: Lär dig hur du ställer in åtkomstkontroll för din Azure-miljö med rollbaserad åtkomstkontroll (RBAC).
author: LijuKodicheraJayadevan
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC, setup
ms.localizationpriority: high
ms.openlocfilehash: 5fedbb5164da05b166d8a42d8d1ceaf43ee95185
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80354447"
---
<!-- cSpell:ignore LijuKodicheraJayadevan -->

# <a name="manage-access-to-your-azure-environment-with-role-based-access-controls"></a>Hantera åtkomst till Azure-miljön med rollbaserad åtkomstkontroll

En viktig del av din styrningsstrategi i Azure är att hantera vem som ska ha åtkomst till Azure-resurser och prenumerationer. Du rekommenderas att tilldela gruppbaserade åtkomstbehörigheter. Att hantera grupper i stället för enskilda användare förenklar underhållet av åtkomstprinciper, ger konsekvent åtkomsthantering för team och minskar eventuella konfigurationsfel. Rollbaserad åtkomstkontroll i Azure (RBAC) är den primära metoden för att hantera åtkomst i Azure.

Med RBAC kan du detaljstyra åtkomsten till resurser i Azure. Du kan hantera vem som ska ha åtkomst till olika Azure-resurser, vad de kan göra med resurserna och till vilka områden de ska ha åtkomst.

När du planerar din strategi för åtkomstkontroll ska du ge användarna den lägsta behörighet som krävs för att de ska kunna utföra sitt arbete. I följande diagram visas ett föreslaget mönster för RBAC-tilldelning.

![Diagram som visar RBAC-roller](./media/manage-access/role-examples.png)

När du planerar din strategi för åtkomstkontroll rekommenderar vi att du samarbetar med personer i ditt företag som är ansvariga för följande: säkerhet och efterlevnad, IT-administration och företagsarkitektur.

Ramverk för molnimplementering ger ytterligare vägledning om hur [du använder rollbaserad åtkomstkontroll](../considerations/roles.md) som en del av molnimplementeringen.

::: zone target="chromeless"

## <a name="actions"></a>Åtgärder

**Bevilja åtkomst till resursgrupper:**

Bevilja användaråtkomst till en resursgrupp:

1. Gå till **Resursgrupper**.
1. Välj en resursgrupp.
1. Välj **Åtkomstkontroll (IAM)** .
1. Välj **+ Lägg till** > **Lägg till rolltilldelning**.
1. Välj en roll och tilldela sedan åtkomst till en användare, grupp eller tjänstens huvudnamn.

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Resources/Subscriptions/ResourceGroups]" submitText="Go to resource groups" ::: form-end

**Bevilja åtkomst till prenumerationer:**

Bevilja användaråtkomst till en prenumeration:

1. går du till **Prenumerationer**.
1. Välj en prenumeration.
1. Välj **Åtkomstkontroll (IAM)** .
1. Välj **+Lägg till** > **Lägg till rolltilldelning**.
1. Välj en roll och tilldela sedan åtkomst till en användare, grupp eller tjänstens huvudnamn.

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to subscriptions" ::: form-end

::: zone-end

::: zone target="docs"

## <a name="grant-resource-group-access"></a>Ge åtkomst till resursgrupper

Bevilja användaråtkomst till en resursgrupp:

1. Gå till [Resursgrupper](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2FSubscriptions%2FResourceGroups).
1. Välj en resursgrupp.
1. Välj **Åtkomstkontroll (IAM)** .
1. Välj **+Lägg till** > **Lägg till rolltilldelning**.
1. Välj en roll och tilldela sedan åtkomst till en användare, grupp eller tjänstens huvudnamn.

## <a name="grant-subscription-access"></a>Ge åtkomst till prenumerationer

Bevilja användaråtkomst till en prenumeration:

1. går du till [Prenumerationer](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).
1. Välj en prenumeration.
1. Välj **Åtkomstkontroll (IAM)** .
1. Välj **+Lägg till** > **Lägg till rolltilldelning**.
1. Välj en roll och tilldela sedan åtkomst till en användare, grupp eller tjänstens huvudnamn.

## <a name="learn-more"></a>Läs mer

Du kan läsa mer här:

- [Vad är rollbaserad åtkomstkontroll (RBAC)?](https://docs.microsoft.com/azure/role-based-access-control/overview)
- [Ramverk för molnimplementering: Använd rollbaserad åtkomstkontroll](../considerations/roles.md)

::: zone-end
