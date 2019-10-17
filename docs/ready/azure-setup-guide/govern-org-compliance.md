---
title: Styrning, säkerhet och efterlevnad i Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lär dig hur du ställer in styrning, säkerhet och efterlevnad i Azure-miljön.
author: tvuylsteke
ms.author: kfollis
ms.date: 09/27/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC, setup
ms.localizationpriority: high
ms.openlocfilehash: c43cf0d12ba26ee0298e79f2f6b90cc5773b2df6
ms.sourcegitcommit: b30952f08155513480c6b2c47a40271c2b2357cf
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/15/2019
ms.locfileid: "72379058"
---
# <a name="governance-security-and-compliance-in-azure"></a>Styrning, säkerhet och efterlevnad i Azure

När du skapar en företagsprincip och planerar dina styrningsstrategier kan du använda verktyg och tjänster som Azure Policy, Azure Blueprints och Azure Security Center för att genomföra och automatisera organisationens styrningsbeslut. Innan du börjar planera styrningen bör du använda [verktyget Governance Benchmark](https://cafbaseline.com) för att identifiera eventuella brister i din organisations metod för molnstyrning. Mer information om hur du utvecklar styrningsprocesser finns i [vägledningen Ramverk för molnimplementering för styrning i Azure](../../govern/index.md).

# <a name="azure-blueprintstabazureblueprints"></a>[Azure Blueprint](#tab/AzureBlueprints)

Azure Blueprint gör det möjligt för molnarkitekter och centrala IT-grupper att definiera en upprepningsbar uppsättning med Azure-resurser som implementerar och tillämpar en organisations standarder, mönster och krav. Med Azure Blueprint kan utvecklingsteam snabbt skapa nya miljöer med vetskapen om att de är skapade med organisatorisk efterlevnad och innehåller en uppsättning inbyggda komponenter – som nätverk – för att påskynda utveckling och leverans.

Skisser är en deklarativ metod för att dirigera distribution av flera resursmallar och andra artefakter som:

- Rolltilldelningar.
- Principtilldelningar.
- Azure Resource Manager-mallar.
- Resursgrupper.

## <a name="create-a-blueprint"></a>Skapa en skiss

Så här skapar du en skiss:

::: zone target="chromeless"

1. Gå till **Skisser – komma igång**.
1. I området **Skapa en skiss** väljer du **Skapa**.
1. Filtrera listan över skisser och välj lämplig skiss.
1. Ange **Namn på skiss** och välj **Definitionens plats**.
1. Klicka på **Nästa: Artefakter >>** och granska artefakterna som ingår i skissen.
1. Klicka på **Spara utkast**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted]" submitText="Create a blueprint" :::

::: zone-end

::: zone target="docs"

1. Gå till [Skisser – komma igång](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted).
1. I området **Skapa en skiss** väljer du **Skapa**.
1. Filtrera listan över skisser och välj lämplig skiss.
1. Ange **Namn på skiss** och välj **Definitionens plats**.
1. Klicka på **Nästa: Artefakter >>** och granska artefakterna som ingår i skissen.
1. Klicka på **Spara utkast**.

::: zone-end

## <a name="publish-a-blueprint"></a>Publicera en skiss

Så här publicerar du skissartefakter till din prenumeration:

::: zone target="chromeless"

1. Gå till **Skisser – Skissdefinitioner**.
1. Välj skissen som du skapade i föregående steg.
1. Granska skissdefinitionen och välj **Publicera skiss.**
1. Ange en **version** (t.ex. _1.0_) och eventuella **ändringsanmärkningar** och välj sedan **Publicera**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints]" submitText="Blueprint definitions" :::

::: zone-end

::: zone target="docs"

1. Gå till [Skisser – Skissdefinitioner](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints).
1. Välj skissdefinitionen som du skapade i föregående steg.
1. Granska skissdefinitionen och välj **Publicera skiss.**
1. Ange en **version** (t.ex. _1.0_) och eventuella **ändringsanmärkningar** och välj sedan **Publicera**.

::: zone-end

::: zone target="docs"

## <a name="learn-more"></a>Läs mer

Du kan läsa mer här:

- [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints)
- [Ramverk för molnimplementering: Beslutsguide för resurskonsekvens](../../decision-guides/resource-consistency/index.md)
- [Standardbaserade skissexempel](/azure/governance/blueprints/samples/index#standards-based-blueprint-samples)

::: zone-end

# <a name="azure-policytabazurepolicy"></a>[Azure Policy](#tab/AzurePolicy)

Azure Policy är en tjänst som används till att skapa, tilldela och hantera principer. De här principerna tillämpar regler för dina resurser så att resurserna efterlever dina företagsstandarder och serviceavtal. Azure Policy söker igenom dina resurser och identifierar resurser som inte är kompatibla med principerna du tillämpar. Du kan till exempel ha en princip som endast tillåter körning av en viss typ av virtuell dator i miljön. När du implementerar den här principen utvärderas alla befintliga virtuella datorer i miljön och de nya virtuella datorer som distribueras. Vid utvärderingen genereras efterlevnadshändelser som du kan använda i övervakning och rapportering.

Överväg att använda vanliga principer för att:

- Tillämpa taggning för resurser och resursgrupper.
- Begränsa regioner för distribuerade resurser.
- Begränsa dyra SKU:er för specifika resurser.
- Granska användningen av viktiga valfria funktioner som hanterade Azure-diskar.

::: zone target="chromeless"

## <a name="action"></a>Åtgärd

Tilldela en inbyggd princip till en hanteringsgrupp, prenumeration eller resursgrupp.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted]" submitText="Assign Policy" :::

::: zone-end

::: zone target="docs"

## <a name="apply-a-policy"></a>Tillämpa en princip

Gör följande om du vill tillämpa en princip för en resursgrupp:

1. går du till [Azure Policy](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted).
1. Välj **Tilldela en princip**.

## <a name="learn-more"></a>Läs mer

Du kan läsa mer här:

- [Azure Policy](https://docs.microsoft.com/azure/azure-policy)
- [Ramverk för molnimplementering: Beslutsguide för principframtvingande](../../decision-guides/policy-enforcement/index.md)

::: zone-end

# <a name="azure-security-centertabazuresecuritycenter"></a>[Azure Security Center](#tab/AzureSecurityCenter)

Azure Security Center är en viktig del i din styrningsstrategi. Det hjälper dig att hålla koll på säkerheten eftersom det:

- Ger en enhetlig vy över säkerheten för alla dina arbetsbelastningar.
- Samlar in, söker efter och analyserar säkerhetsdata från flera olika källor, till exempel brandväggar och andra partnerlösningar.
- Ger säkerhetsrekommendationer för att åtgärda problem innan de kan utnyttjas.
- Kan användas för att tillämpa säkerhetsprinciper för arbetsbelastningar i hybridmoln för att säkerställa att säkerhetsstandarder efterlevs.

Många av säkerhetsfunktioner, som säkerhetsprinciper och rekommendationer, är tillgängliga utan kostnad. En del av de mer avancerade funktionerna som just-in-time-åtkomst till virtuella datorer och stöd för hybridarbetsbelastningar är tillgängliga på Standard-nivån för Security Center. Just-in-time-åtkomst till virtuella datorer kan minska nätverkets angreppsyta genom att åtkomsten till hanteringsportar på de virtuella Azure-datorerna begränsas.

> [!TIP]
> Azure Security Center är aktiverat som standard i alla prenumerationer. Vi rekommenderar att du aktiverar datainsamling från virtuella datorer så att Azure Security Center kan installera agenten och börja samla in data.

::: zone target="docs"

Om du vill utforska Azure Security Center går du till [Azure-portalen](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0).

## <a name="learn-more"></a>Läs mer

Du kan läsa mer här:

- [Azure Security Center](https://docs.microsoft.com/azure/security-center)
- [Just-in-time-åtkomst till virtuella datorer](https://docs.microsoft.com/azure/security-center/security-center-just-in-time#how-does-just-in-time-access-work)
- [Standard-nivån jämfört med den kostnadsfria nivån](https://azure.microsoft.com/pricing/details/security-center)
- [Ramverk för molnimplementering: Översikt över området säkerhetsbaslinje](../../govern/security-baseline/index.md)

::: zone-end

::: zone target="chromeless"

## <a name="action"></a>Åtgärd

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end
