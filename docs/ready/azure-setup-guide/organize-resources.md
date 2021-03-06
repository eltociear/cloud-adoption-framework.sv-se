---
title: Organisera Azure-resurser effektivt
description: Förstå regelverken du behöver för att effektivt organisera dina Azure-resurser för enkel hantering.
author: laraaleite
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC, setup
ms.localizationpriority: high
ms.openlocfilehash: 6ed6e547156a2fa9f07a49460fedd94a8ceb152b
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80354349"
---
<!-- cSpell:ignore laraaleite profx fsubscriptions fresource -->

# <a name="organize-your-azure-resources"></a>Organisera dina Azure-resurser

Det är viktigt att organisera molnbaserade resurser för att skydda, hantera och spåra kostnader som rör dina arbetsbelastningar. Definiera en hierarki för hanteringsgrupper, följ en vanlig namngivningskonvention och tillämpa taggning av resurser för att organisera dina resurser.

<!-- markdownlint-disable MD024 MD025 -->

<!-- cSpell:disable-next-line -->
# <a name="azure-management-groups-and-hierarchy"></a>[Hanteringsgrupper och hierarkier i Azure](#tab/AzureManagmentGroupsAndHierarchy)

Azure har fyra hanteringsnivåer: hanteringsgrupper, prenumerationer, resursgrupper och resurser. I den här bilden visas förhållandet mellan dessa nivåer.

   ![Diagram som visar relationen mellan nivåer i hanteringshierarkin](./media/organize-resources/scope-levels.png)

- **Hanteringsgrupper:** Dessa grupper är containrar som hjälper dig att hantera åtkomst, principer och efterlevnad för flera prenumerationer. Alla prenumerationer i en hanteringsgrupp ärver automatiskt de villkor som tillämpas för hanteringsgruppen.
- **Prenumerationer:** En prenumeration associerar användarkonton och de resurser som kontona har skapat med varandra på ett logiskt sätt. För varje prenumeration finns gränser eller kvoter för mängden resurser som kan skapas och användas. Organisationer kan använda prenumerationer till att hantera kostnader och de resurser som skapas av användare, grupper och projekt.
- **Resursgrupper:** En resursgrupp är en logisk container som Azure-resurser (t.ex. webbappar, databaser och lagringskonton) distribueras och hanteras i.
- **Resurser:** Resurser är instanser av tjänster du skapar som virtuella datorer, lagring och SQL-databaser.

## <a name="scope-of-management-settings"></a>Hanteringsinställningarnas omfattning

Du kan tillämpa hanteringsinställningar som principer och rollbaserad åtkomst på valfri hanteringsnivå. Den nivå nu väljer avgör hur brett inställningen tillämpas. Lägre nivåer ärver inställningar från högre nivåer. När du till exempel skapar en princip för en prenumeration gäller principen även för alla resursgrupper och resurser i prenumerationen.

Vanligtvis är det bra att tillämpa kritiska inställningar på högre nivåer och projektspecifika krav på lägre nivåer. Till exempel vill du kanske se till att alla resurser för din organisation har distribuerats till vissa regioner. Det gör du med en princip för prenumerationen som anger tillåtna platser. När andra användare i organisationen lägger till nya resursgrupper och resurser framtvingas de tillåtna platserna automatiskt. Läs mer om principer i avsnittet om säkerhet, styrning och efterlevnad i den här guiden.

Om du bara har ett fåtal prenumerationer är det relativt enkelt att hantera dem oberoende av varandra. Men om du har många prenumerationer bör du överväga att skapa en hierarki för hanteringsgrupper för att förenkla hanteringen av dina prenumerationer och resurser. Mer information finns i [Organisera och hantera dina Azure-prenumerationer](../azure-best-practices/organize-subscriptions.md).

När du planerar din efterlevnadsstrategi rekommenderar vi att du samarbetar med personer i organisationen med följande roller: säkerhet och efterlevnad, IT-administration, företagsarkitekter, nätverkspersonal och inköp.

::: zone target="docs"

## <a name="create-a-management-level"></a>Skapa en hanteringsnivå

Du kan skapa en hanteringsgrupp, ytterligare prenumerationer eller resursgrupper.

### <a name="create-a-management-group"></a>Skapa en hanteringsgrupp

Skapa en hanteringsgrupp som hjälper dig att hantera åtkomst, principer och efterlevnad för flera prenumerationer.

1. går du till [Hanteringsgrupper](https://portal.azure.com/#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade).
2. Välj **Lägg till hanteringsgrupp**.

### <a name="create-a-subscription"></a>Skapa en prenumeration

Använd prenumerationer till att hantera kostnader och de resurser som skapas av användare, grupper och projekt.

1. går du till [Prenumerationer](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).
1. Välj **Lägg till**.

### <a name="create-a-resource-group"></a>Skapa en resursgrupp

Skapa en resursgrupp där du kan lagra resurser som webbappar, databaser och lagringskonton som delar samma livscykel, behörigheter och principer.

1. Gå till [Resursgrupper](https://portal.azure.com/#create/Microsoft.ResourceGroup).
1. Välj **Lägg till**.
1. Välj den **prenumeration** som du vill skapa resursgruppen under.
1. Ange ett namn för **resursgruppen**.
1. Välj en **region** för resursgruppens plats.

## <a name="learn-more"></a>Läs mer

Du kan läsa mer här:

- [Grunderna i Azure](../considerations/fundamental-concepts.md)
- [Skapa dina första prenumerationer](../azure-best-practices/initial-subscriptions.md)
- [Skapa ytterligare Azure-prenumerationer för att skala din Azure-miljö](../azure-best-practices/scale-subscriptions.md)
- [Organisera och hantera dina Azure-prenumerationer](../azure-best-practices/organize-subscriptions.md)
- [Ordna resurser med hanteringsgrupper i Azure](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview)
- [Förstå åtkomsthantering av resurser i Azure](../../govern/resource-consistency/resource-access-management.md)
- [Tjänstbegränsningar för prenumerationer](https://docs.microsoft.com/azure/azure-subscription-service-limits)

::: zone-end

::: zone target="chromeless"

## <a name="actions"></a>Åtgärder

**Skapa en hanteringsgrupp:**

Skapa en hanteringsgrupp som hjälper dig att hantera åtkomst, principer och efterlevnad för flera prenumerationer.

1. går du till **Hanteringsgrupper**.
1. Välj **Lägg till hanteringsgrupp**.

::: form action="OpenBlade[#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade]" submitText="Go to Management groups" :::

**Skapa ytterligare en prenumeration:**

Använd prenumerationer till att hantera kostnader och de resurser som skapas av användare, grupper och projekt.

1. går du till **Prenumerationer**.
1. Välj **Lägg till**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to Subscriptions" :::

**Skapa en resursgrupp:**

Skapa en resursgrupp där du kan lagra resurser som webbappar, databaser och lagringskonton som delar samma livscykel, behörigheter och principer.

1. Gå till **Resursgrupper**.
1. Välj **Lägg till**.
1. Välj den **prenumeration** som du vill skapa resursgruppen under.
1. Ange ett namn för **resursgruppen**.
1. Välj en **region** för resursgruppens plats.

::: form action="Create[#create/Microsoft.ResourceGroup]" submitText="Create a resource group" :::

::: zone-end

# <a name="naming-standards"></a>[Namngivningsregler](#tab/NamingStandards)

Namngivningsreglerna hjälper dig att enkelt identifiera resurser i Microsoft Azure-portalen, på en faktura och i skript för automatisering. En namngivnings- och etikettstrategi omfattar information om företaget och verksamheten, såsom delar av resursnamn:

- Den affärsrelaterade sidan av denna strategi säkerställer att resursnamn innehåller den organisatoriska information som krävs för att identifiera teamen. Använd en resurs tillsammans med företagsägare som ansvarar för resurskostnader.

- Den operativa sidan bör se till att namnen innehåller den information som IT-teamen behöver. Använd informationen som identifierar arbetsbelastning, program, miljö, prioritet och annan information som är användbar för att hantera resurser.

Olika resurstyper har olika [namngivningsregler och begränsningar](https://docs.microsoft.com/azure/azure-resource-manager/management/resource-name-rules). Mer information och rekommendationer till hjälp för företags molnimplementeringsåtgärder, finns i [vägledning för namngivning och taggning](../azure-best-practices/naming-and-tagging.md) Ramverk för molnimplementering.

Följande tabell innehåller namngivningsmönster för några exempeltyper av Azure-resurser.

::: zone target="docs"

>[!TIP]
>Undvik specialtecken (`-` eller `_`) som det första eller sista tecknet i ett namn. De här tecknen orsakar de flesta valideringsfel.

::: zone-end

| Entitet | Omfång | Längd | Skiftläge | Giltiga tecken | Föreslaget mönster | Exempel |
| --- | --- | --- | --- | --- | --- | --- |
|Resursgrupp |Prenumeration |1–90 |Skiftlägesokänsligt |Alfanumeriskta, understreck, parenteser, bindestreck och punkt (förutom i slutet) samt Unicode-tecken |`<service short name>-<environment>-rg` |`profx-prod-rg` |
|Tillgänglighetsuppsättning |Resursgrupp |1–80 |Skiftlägesokänsligt |Alfanumeriskt, understreck och bindestreck |`<service-short-name>-<context>-as` |`profx-sql-as` |
|Tagga |Associerad entitet |512 (namn), 256 (värde) |Skiftlägesokänsligt |Alfanumeriskt |`"key" : "value"` |`"department" : "Central IT"` |

# <a name="resource-tags"></a>[Resurstaggar](#tab/ResourceTags)

Taggar är användbara för att snabbt identifiera dina resurser och resursgrupper. Du kan ordna Azure-resurser i kategorier genom att lägga till taggar. Varje tagg består av ett namn och ett värde. Du kan till exempel använda namnet ”Miljö” och värdet ”Produktion” för alla resurser i produktionsmiljön. Taggar ska innehålla sammanhang om resursens associerade arbetsbelastning eller program, driftkrav och ägarskapsinformation.

När du har lagt till taggar kan du hämta alla resurserna i din prenumeration med det taggnamnet och taggvärdet. Med taggar kan du hämta relaterade resurser från olika resursgrupper, vilket är användbart när du ska ordna resurser för fakturering eller hantering.

Du kan också använda taggar till mycket annat. Vanliga användningsområden är:

- **Metadata och dokumentation:** Administratörer kan enkelt se detaljer om de resurser som de arbetar med genom att använda en tagg, till exempel ”ProjectOwner”.
- **Automation:** Du kan ha skript som körs regelbundet och utför åtgärder baserat på ett taggvärde, som ”ShutdownTime” eller ”DeprovisionDate”.
- **Kostnadsoptimering:** I Azure Cost Management kan du använda taggen för kostnadsställe som ett filter för att rapportera avgifter baserat på en grupp- eller avdelningsanvändning.

Varje resurs eller resursgrupp kan innehålla upp till 50 taggnamn-/taggvärdepar. Den här begränsningen gäller dock bara taggar som läggs till direkt för resursgruppen eller resursen.

Mer taggningsrekommendationer och exempel finns i [vägledningen om taggning](../azure-best-practices/naming-and-tagging.md) i Ramverk för molnimplementering.

::: zone target="docs"

## <a name="apply-a-resource-tag"></a>Lägga till en resurstagg

Så här lägger du till en tagg för en resursgrupp:

1. Gå till [Resursgrupper](https://ms.portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2fSubscriptions%2fResourceGroups).
1. Välj en resursgrupp.
1. Välj **Tilldela taggar**.
1. Ange ett nytt namn och värde eller välj ett befintligt namn och värde från listrutan.

## <a name="learn-more"></a>Läs mer

Du kan läsa mer i [Använda taggar till at organisera dina Azure-resurser](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

::: zone-end

::: zone target="chromeless"

## <a name="action"></a>Åtgärd

**Lägga till en resurstagg:**

Så här lägger du till en tagg för en resursgrupp:

1. Gå till **Resursgrupper**.
1. Välj en resursgrupp.
1. Välj **Taggar**.
1. Ange ett nytt namn och värde eller välj ett befintligt namn och värde.

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2FSubscriptions%2FResourceGroups]" submitText="Go to resource groups" :::

::: zone-end
