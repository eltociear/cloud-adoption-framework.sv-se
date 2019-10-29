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
ms.openlocfilehash: 7073df6b697da49429d4086d9f8f3f113583e52d
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557099"
---
# <a name="operational-compliance-in-azure"></a>Driftsmässig efterlevnad i Azure

Driftsmässig efterlevnad är den andra disciplinen i varje baslinje för molnhantering.

![Baslinje för molnhantering](../../_images/manage/management-baseline.png)

Genom att förbättra den driftmässiga efterlevnaden går det att minska riskerna för avbrott som är relaterade till konfigurationsförändringar och säkerhetsriskerna som är relaterade till system som inte korrigeras på korrekt sätt.

Följande tabell visar det rekommenderade minimikravet för alla baslinjer för hantering för alla företagsomspännande miljöer.

|Process  |Verktyg  |Syfte  |
|---------|---------|---------|
|Uppdateringshantering|Uppdateringshantering|Hantering och schemaläggning av uppdateringar|
|Policyframtvingande|Azure Policy|Principtillämpning för att säkerställa miljö- och gästefterlevnad|
|Miljö Konfiguration|Azure Blueprint|Automatisk efterlevnad för kärntjänster|

::: zone target="docs"

## <a name="update-management"></a>Uppdateringshantering

::: zone-end
::: zone target="chromeless"

## <a name="update-managementtabupdatemanagement"></a>[Hantering av uppdateringar](#tab/UpdateManagement)

::: zone-end

Datorer som hanteras med Uppdateringshantering använder följande konfigurationer för att utföra utvärdering och uppdateringsdistributioner:

- Microsoft Monitoring Agent (MMA) för Windows eller Linux
- Önskad PowerShell-tillståndskonfiguration (DSC) för Linux
- Automation Hybrid Runbook Worker
- Microsoft Update eller Windows Server Update Services (WSUS) för Windows-datorer

Mer information finns i [Lösning för hantering av uppdateringar](https://docs.microsoft.com/azure/automation/automation-update-management)

> [!WARNING]
> Innan du använder uppdateringshantering måste du publicera virtuella datorer eller en hel prenumeration i Log Analytics och Azure Automation.
> Publiceringen kan göras på två sätt. Ett av dessa bör följas innan du fortsätter med uppdateringshanteringen.
>
> - [Enstaka virtuell dator](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-single-vm)
> - [Hel prenumeration](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-at-scale)

### <a name="manage-updates"></a>Hantera uppdateringar

Gör följande om du vill tillämpa en princip för en resursgrupp:

1. Gå till [Azure Automation](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts).
2. Välj ett av de **Automation-konton** som visas.
3. Leta reda på avsnittet **Konfigurationshantering** i portalen.
4. Inventering, ändringshantering och tillståndskonfiguration kan användas för att kontrollera status och driftsmässig efterlevnad för de hanterade virtuella datorerna.

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

Azure Policy används i styrningsprocesser. Men är också en viktig del i molnhanteringsprocesser. Förutom att granska och reparera Azure-resurser kan Azure Policy granska inställningarna i en dator. Verifieringen utförs av gästkonfigurationstillägget och klienten. Tillägget kontrollerar inställningar via klienten, till exempel:

- Operativsystemets konfiguration
- Programkonfiguration eller förekomst
- Miljöinställningar

För närvarande granskar Azure Policy-gästkonfigurationen endast inställningar i datorn. Den tillämpar inte konfigurationer.

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

Azure Blueprint gör det möjligt för molnarkitekter och centrala IT-grupper att definiera en upprepningsbar uppsättning med Azure-resurser som implementerar och tillämpar en organisations standarder, mönster och krav. Med Azure Blueprint kan utvecklingsteam snabbt skapa nya miljöer med vetskapen om att de är skapade med organisatorisk efterlevnad och innehåller en uppsättning inbyggda komponenter – som nätverk – för att påskynda utveckling och leverans.

Skisser är en deklarativ metod för att dirigera distribution av flera resursmallar och andra artefakter som:

- Rolltilldelningar.
- Principtilldelningar.
- Azure Resource Manager-mallar.
- Resursgrupper.

Genom att använda en skiss kan du framtvinga driftsmässig efterlevnad i en miljö, om detta inte redan har gjorts av molnstyrningsteamet.

### <a name="create-a-blueprint"></a>Skapa en skiss

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

### <a name="publish-a-blueprint"></a>Publicera en skiss

Så här publicerar du skissartefakter till din prenumeration:

::: zone target="chromeless"

1. Gå till **Skisser – Skissdefinitioner**.
1. Välj skissen som du skapade i föregående steg.
1. Granska skissdefinitionen och välj **Publicera skiss.**
1. Ange en **version** (t.ex. 1.0) och eventuella **ändringsanmärkningar** och välj sedan **Publicera**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints]" submitText="Blueprint definitions" :::

::: zone-end

::: zone target="docs"

1. Gå till [Skisser – Skissdefinitioner](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints).
1. Välj skissen som du skapade i föregående steg.
1. Granska skissdefinitionen och välj **Publicera skiss.**
1. Ange en **version** (t.ex. 1.0) och eventuella **ändringsanmärkningar** och välj sedan **Publicera**.

### <a name="learn-more"></a>Läs mer

Du kan läsa mer här:

- [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints)
- [Ramverk för molnimplementering: Beslutsguide för resurskonsekvens](../../decision-guides/resource-consistency/index.md)
- [Standardbaserade skissexempel](https://docs.microsoft.com/azure/governance/blueprints/samples/index#standards-based-blueprint-samples)

::: zone-end
