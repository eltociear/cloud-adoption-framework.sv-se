---
title: Hantera kostnader och fakturering för Azure-resurser
description: Använd Cloud Adoption Framework för att lära dig hur du ställer in budgetar, betalningar och får bättre förståelse om faktureringen av dina Azure-resurser.
author: dchimes
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC, setup
ms.localizationpriority: high
ms.openlocfilehash: 0f91ed2c09b2511304a59bc8768507f737ec6c76
ms.sourcegitcommit: 011332538dbc6774b732f7b9f2b89d6c8aa90c36
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/10/2020
ms.locfileid: "79024034"
---
<!-- cSpell:ignore dchimes -->

# <a name="manage-costs-and-billing-for-your-azure-resources"></a>Hantera kostnader och fakturering för dina Azure-resurser

Kostnadshantering är den process där du effektivt planerar och styr kostnaderna i företaget. Kostnadshanteringsuppgifter utförs normalt av ekonomi-, hanterings- och appteamen. Azure Cost Management kan hjälpa dig att planera kostnadsmedvetet. Det hjälper även till att effektivt analysera kostnader och vidta åtgärder för att optimera molnutgifter.

Mer information om hur du integrerar molnkostnadshantering i organisationen finns i [Spåra kostnader mellan affärsenheter, miljöer och projekt](../azure-best-practices/track-costs.md) i artikeln om Cloud Adoption Framework.

## <a name="manage-your-costs-with-azure-cost-management"></a>Hantera dina kostnader med Azure Cost Management

I Azure Cost Management finns ett antal sätt att förutse och hantera kostnader:

- Med **Analysera molnkostnader** kan du utforska och analysera dina kostnader. Du kan se aggregerade kostnader för ditt konto eller ackumulerade kostnader över tid.
- Med **Övervaka med budgetar** kan du skapa en budget och sedan konfigurera aviseringar som varnar dig om du är på väg att överstiga den.
- **Optimera med rekommendationer** hjälper dig att identifiera resurser som är inaktiva eller som sällan används, så att du kan vidta åtgärder för att optimera din resursanvändning.
- **Hantera fakturor och betalningar** för att få insyn i dina investeringar i molnet.

::: zone target="docs"

### <a name="predict-and-manage-costs"></a>Förutse och hantera kostnader

1. Gå till [Kostnadshantering och fakturering](https://portal.azure.com/#blade/Microsoft_Azure_Billing/ModernBillingMenuBlade/Overview).
1. Välj **Cost Management**.
1. Utforska funktionerna som hjälper dig att analysera och optimera molnkostnader.

### <a name="manage-invoices-and-payment-methods"></a>Hantera fakturor och betalningsmetoder

1. Gå till [Kostnadshantering och fakturering](https://portal.azure.com/#blade/Microsoft_Azure_Billing/ModernBillingMenuBlade/Overview).
1. Välj **Fakturor** eller **Betalningsmetoder** från avsnittet **Fakturering** i det vänstra fönstret.

## <a name="billing-and-subscription-support"></a>Support för fakturering och prenumeration

Vi erbjuder Azure-kunder fakturerings- och prenumerationssupport dygnet runt alla dagar i veckan. Skapa en supportbegäran om du behöver hjälp med att använda Azure.

### <a name="create-a-support-request"></a>Skapa en supportbegäran

Gör så här för att skicka in en ny supportbegäran:

1. Gå till [Hjälp + Support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview).
1. Välj **Ny supportbegäran**.

### <a name="view-a-support-request"></a>Visa en supportbegäran

Gör så här för att visa dina supportbegäranden och deras status:

1. Gå till [Hjälp + Support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview).
1. Välj **Alla supportbegäranden**.

## <a name="learn-more"></a>Läs mer

Du kan läsa mer här:

- [Dokumentation om Azure-fakturering och kostnadshantering](https://docs.microsoft.com/azure/billing)
- [Ramverk för molnimplementering: Spåra kostnader för affärsenheter, miljöer och projekt](../azure-best-practices/track-costs.md)
- [Ramverk för molnimplementering: Styrningsdisciplin för kostnadshantering](../../govern/cost-management/index.md)

::: zone-end

::: zone target="chromeless"

## <a name="actions"></a>Åtgärder

**Förutse och hantera kostnader:**

1. Gå till **Kostnadshantering och fakturering**.
1. Välj **Cost Management**.

**Hantera fakturor och betalningsmetoder:**

1. Gå till **Kostnadshantering och fakturering**.
1. Välj **Fakturor** eller **Betalningsmetoder** från avsnittet **Fakturering** i det vänstra fönstret.

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/ModernBillingMenuBlade/Overview]" submitText="Go to Cost Management + Billing" ::: form-end

**Support för fakturering och prenumeration:**

Vi erbjuder Azure-kunder fakturerings- och prenumerationssupport dygnet runt alla dagar i veckan. Skapa en supportbegäran om du behöver hjälp med att använda Azure.

**Skapa en supportbegäran:**

Gör så här för att skicka in en ny supportbegäran:

1. Gå till **Hjälp + Support**.
2. Välj **Ny supportbegäran**.

**Visa en supportbegäran:** Gör så här för att visa dina supportbegäranden och deras status:

1. Gå till **Hjälp + Support**.
2. Välj **Alla supportbegäranden**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview]" submitText="Go to Help + Support" ::: form-end

::: zone-end
