---
title: Driftsmässig efterlevnad i Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Säkerställ stabilitet i verksamheten med ökad driftsmässig efterlevnad
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: b5a94ab41bff26371621acc5e62ae19d9fd02e5c
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565489"
---
# <a name="operational-compliance-in-azure"></a>Driftsmässig efterlevnad i Azure

_Driftsmässig efterlevnad_ är den andra disciplinen i varje baslinje för molnhantering.

![Baslinje för molnhantering](../../_images/manage/management-baseline.png)

Genom att förbättra den driftmässiga efterlevnaden går det att minska riskerna för avbrott som är relaterade till konfigurationsförändringar och säkerhetsriskerna som är relaterade till system som inte korrigeras på korrekt sätt.

Den här tabellen beskriver det föreslagna minimikravet för en hanteringsbaslinje för miljöer i företagsklass.

|Process  |Verktyg  |Syfte  |
|---------|---------|---------|
|Uppdateringshantering|Uppdateringshantering|Hantering och schemaläggning av uppdateringar|
|Policyframtvingande|Azure Policy|Principtillämpning för att säkerställa miljö- och gästefterlevnad|
|Miljökonfiguration|Azure Blueprint|Automatisk efterlevnad för kärntjänster|

::: zone target="docs"

## <a name="update-management"></a>Uppdateringshantering

::: zone-end
::: zone target="chromeless"

## <a name="update-managementtabupdatemanagement"></a>[Hantering av uppdateringar](#tab/UpdateManagement)

::: zone-end

Datorer som hanteras med Uppdateringshantering använder följande konfigurationer för utvärdering och uppdateringsdistribution:

- Microsoft Monitoring Agent (MMA) för Windows eller Linux
- Önskad PowerShell-tillståndskonfiguration (DSC) för Linux
- Azure Automation Hybrid Runbook Worker
- Microsoft Update eller Windows Server Update Services (WSUS) för Windows-datorer

Mer information finns i avsnittet om [Uppdateringshantering](https://docs.microsoft.com/azure/automation/automation-update-management).

> [!WARNING]
> Innan du använder Uppdateringshantering måste du registrera virtuella datorer eller en hel prenumeration i Log Analytics och Azure Automation.
>
> Publiceringen kan göras på två sätt:
>
> - [Enstaka virtuell dator](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-single-vm)
> - [Hel prenumeration](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-at-scale)
>
> Du bör ha en innan du fortsätter med Uppdateringshantering.

### <a name="manage-updates"></a>Hantera uppdateringar

Gör följande om du vill tillämpa en princip för en resursgrupp:

1. Gå till [Azure Automation](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts).
1. Välj **Automation-konton** och välj ett av kontona i listan.
1. Gå till **Konfigurationshantering**.
1. **Inventering**, **Ändringshantering** och **Tillståndskonfiguration** kan användas för att kontrollera status och efterlevnad för de hanterade virtuella datorerna.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts]" submitText="Assign Policy" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

## <a name="azure-policy"></a>Azure Policy

::: zone-end
::: zone target="chromeless"

## <a name="azure-policytabazurepolicy"></a>[Azure Policy](#tab/AzurePolicy)

::: zone-end

Azure Policy används i styrningsprocesser. Men är också en viktig del i molnhanteringsprocesser. Azure Policy kan granska och reparera Azure-resurser och kan även granska inställningar på en dator. Verifieringen utförs av gästkonfigurationstillägget och klienten. Tillägget kontrollerar inställningar via klienten, till exempel:

- Operativsystemets konfiguration.
- Programkonfiguration eller förekomst.
- Miljöinställningar.

Azure Policy-gästkonfigurationen granskar för närvarande bara inställningar på datorn. Den tillämpar inte konfigurationer.

::: zone target="chromeless"

### <a name="action"></a>Åtgärd

Tilldela en inbyggd princip till en hanteringsgrupp, prenumeration eller resursgrupp.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted]" submitText="Assign Policy" :::

::: zone-end

::: zone target="docs"

### <a name="apply-a-policy"></a>Tillämpa en princip

Gör följande om du vill tillämpa en princip för en resursgrupp:

1. går du till [Azure Policy](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted).
1. Välj **Tilldela en princip**.

### <a name="learn-more"></a>Läs mer

Du kan läsa mer här:

- [Azure Policy](https://docs.microsoft.com/azure/azure-policy)
- [Azure Policy – gästkonfiguration](https://docs.microsoft.com/azure/governance/policy/concepts/guest-configuration)
- [Ramverk för molnimplementering: Beslutsguide för principframtvingande](../../decision-guides/policy-enforcement/index.md)

## <a name="azure-blueprints"></a>Azure Blueprint

::: zone-end
::: zone target="chromeless"

## <a name="azure-blueprintstabazureblueprints"></a>[Azure Blueprint](#tab/AzureBlueprints)

::: zone-end

Med Azure Blueprints kan molnarkitekter och centrala IT-grupper definiera en upprepningsbar uppsättning Azure-resurser. Dessa resurser implementerar och följer organisationens standarder, mönster och krav.

Med Azure Blueprints kan utvecklingsteam snabbt bygga och etablera nya miljöer. Utvecklingsteam kan också vara säkra på att de följer organisationens efterlevnadskrav. De gör detta med hjälp av en uppsättning inbyggda komponenter som nätverkskomponenter för att påskynda utvecklingen och leveransen.

Skisser är en deklarativ metod för att dirigera distributionen av olika resursmallar och andra artefakter som:

- Rolltilldelningar.
- Principtilldelningar.
- Azure Resource Manager-mallar.
- Resursgrupper.

Genom att använda en skiss kan du framtvinga efterlevnad i en miljö, om detta inte görs av molnstyrningsteamet.

### <a name="create-a-blueprint"></a>Skapa en skiss

Så här skapar du en skiss:

::: zone target="chromeless"

1. Gå till **Skisser – komma igång**.
1. Välj **Skapa** i fönstret **Skapa en skiss**.
1. Filtrera listan över skisser och välj lämplig skiss.
1. Ange skissens namn i rutan **Namn på skiss**.
1. Välj **Definitionens plats** och välj lämplig plats.
1. Välj **Nästa: Artefakter >>** och granska artefakterna som ingår i skissen.
1. Välj **Spara utkast**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted]" submitText="Create a blueprint" :::

::: zone-end

::: zone target="docs"

1. Gå till [Skisser – komma igång](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted).
1. Välj **Skapa** i fönstret **Skapa en skiss**.
1. Filtrera listan över skisser och välj lämplig skiss.
1. Ange skissens namn i rutan **Namn på skiss**.
1. Välj **Definitionens plats** och välj lämplig plats.
1. Välj **Nästa: Artefakter >>** och granska artefakterna som ingår i skissen.
1. Välj **Spara utkast**.

::: zone-end

### <a name="publish-a-blueprint"></a>Publicera en skiss

Så här publicerar du skissartefakter till din prenumeration:

::: zone target="chromeless"

1. Gå till **Skisser – Skissdefinitioner**.
1. Välj skissen som du skapade i föregående steg.
1. Granska skissdefinitionen och välj **Publicera skiss.**
1. Ange en version, t.ex. ”1.0”, i rutan **Version**.
1. Skriv dina anteckningar i rutan **Ändra anteckningar**.
1. Välj **Publicera**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints]" submitText="Blueprint definitions" :::

::: zone-end

::: zone target="docs"

1. Gå till [Skisser – Skissdefinitioner](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints).
1. Välj skissen som du skapade i föregående steg.
1. Granska skissdefinitionen och välj **Publicera skiss.**
1. Ange en version, t.ex. ”1.0”, i rutan **Version**.
1. Skriv dina anteckningar i rutan **Ändra anteckningar**.
1. Välj **Publicera**.

<!-- markdownlint-disable MD024 -->

### <a name="learn-more"></a>Läs mer

Du kan läsa mer här:

- [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints)
- [Ramverk för molnimplementering: Beslutsguide för resurskonsekvens](../../decision-guides/resource-consistency/index.md)
- [Standardbaserade skissexempel](https://docs.microsoft.com/azure/governance/blueprints/samples/index#standards-based-blueprint-samples)

::: zone-end
