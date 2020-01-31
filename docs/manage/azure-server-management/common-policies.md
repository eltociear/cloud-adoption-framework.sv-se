---
title: Vanliga Azure Policys exempel
description: Vanliga Azure Policys exempel
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 7020ffed2395d6c22f835d66cd1c539b525f37c3
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808132"
---
# <a name="common-azure-policy-examples"></a>Vanliga Azure Policys exempel

[Azure policy](https://docs.microsoft.com/azure/governance/policy/overview) kan hjälpa dig att använda styrning för dina moln resurser. Den här tjänsten kan hjälpa dig att skapa guardrails som garanterar företagets efterlevnad av styrnings princip krav. Använd antingen Azure Portal-eller PowerShell-cmdletar för att skapa principer. Den här artikeln innehåller PowerShell-cmdlet-exempel.

> [!NOTE]
> Med Azure Policy distribueras inte tillämpnings principer (**deployIfNotExists**) automatiskt till befintliga virtuella datorer. Reparation krävs för att virtuella datorer ska vara kompatibla. Mer information finns i [Reparera inkompatibla resurser med Azure policy](https://docs.microsoft.com/azure/governance/policy/how-to/remediate-resources).

## <a name="common-policy-examples"></a>Vanliga princip exempel

I följande avsnitt beskrivs några principer som ofta används.

### <a name="restrict-resource-regions"></a>Begränsa resurs regioner

Reglering av regler och principer beror ofta på kontrollen av den fysiska plats där resurser distribueras. Du kan använda en inbyggd princip för att tillåta att användare bara skapar resurser i vissa tillåtna Azure-regioner.

Du hittar den här principen i portalen genom att söka efter "location" på sidan princip definition. Eller kör denna cmdlet för att hitta principen:

```powershell
Get-AzPolicyDefinition | Where-Object { ($_.Properties.policyType -eq "BuiltIn") -and ($_.Properties.displayName -like "*location*") }
```

Följande skript visar hur du tilldelar principen. Ändra `$SubscriptionID` värdet så att det pekar på den prenumeration som du vill tilldela principen. Innan du kör skriptet använder du cmdleten [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) för att logga in.

```powershell
#Specify the value for $SubscriptionID.
$SubscriptionID = <subscription ID>
$scope = "/subscriptions/$SubscriptionID"

#Replace the -Name GUID with the policy GUID you want to assign.
$AllowedLocationPolicy = Get-AzPolicyDefinition -Name "e56962a6-4747-49cd-b67b-bf8b01975c4c"

#Replace the locations with the ones you want to specify.
$policyParam = '{"listOfAllowedLocations":{"value":["eastus","westus"]}}'
New-AzPolicyAssignment -Name "Allowed Location" -DisplayName "Allowed locations for resource creation" -Scope $scope -PolicyDefinition $AllowedLocationPolicy -Location eastus -PolicyParameter $policyparam
```

Du kan också använda det här skriptet för att tillämpa de andra principerna som beskrivs i den här artikeln. Ersätt bara GUID på raden som anger `$AllowedLocationPolicy` med GUID för den princip som du vill använda.

### <a name="block-certain-resource-types"></a>Blockera vissa resurs typer

En annan vanlig inbyggd princip som används för att kontrol lera kostnader kan också användas för att blockera vissa resurs typer.

Om du vill hitta den här principen i portalen söker du efter "tillåtna resurs typer" på princip definitions sidan. Eller kör denna cmdlet för att hitta principen:

```powershell
Get-AzPolicyDefinition | Where-Object { ($_.Properties.policyType -eq "BuiltIn") -and ($_.Properties.displayName -like "*allowed resource types") }
```

När du har identifierat den princip som du vill använda kan du ändra PowerShell-exemplet i avsnittet [begränsa resurs områden](#restrict-resource-regions) för att tilldela principen.

### <a name="restrict-vm-size"></a>Begränsa VM-storlek

Azure erbjuder ett brett utbud av VM-storlekar för att stödja olika arbets belastningar. För att kontrol lera budgeten kan du skapa en princip som endast tillåter en delmängd av VM-storlekar i dina prenumerationer.

### <a name="deploy-antimalware"></a>Distribuera program mot skadlig kod

Du kan använda den här principen för att distribuera ett Microsoft *IaaSAntimalware* -tillägg med en standard konfiguration till virtuella datorer som inte skyddas av program mot skadlig kod.

Princip-GUID är `2835b622-407b-4114-9198-6f7064cbe0dc`.

Följande skript visar hur du tilldelar principen. Om du vill använda skriptet ändrar du `$SubscriptionID` värdet så att det pekar på den prenumeration som du vill tilldela principen. Innan du kör skriptet använder du cmdleten [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) för att logga in.

```powershell
#Specify the value for $SubscriptionID.
$SubscriptionID = <subscription ID>
$scope = "/subscriptions/$SubscriptionID"

$AntimalwarePolicy = Get-AzPolicyDefinition -Name "2835b622-407b-4114-9198-6f7064cbe0dc"

#Replace location “eastus” with the value that you want to use.
New-AzPolicyAssignment -Name "Deploy Antimalware" -DisplayName "Deploy default Microsoft IaaSAntimalware extension for Windows Server" -Scope $scope -PolicyDefinition $AntimalwarePolicy -Location eastus –AssignIdentity

```

## <a name="next-steps"></a>Nästa steg

Lär dig mer om andra server hanterings verktyg och tjänster som är tillgängliga.

> [!div class="nextstepaction"]
> [Verktyg och tjänster för Azure Server Management](./tools-services.md)
